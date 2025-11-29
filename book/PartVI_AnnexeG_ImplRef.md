PARTIE VI — ANNEXES TECHNIQUES  
Annexe G — Implémentation de référence USC‑96 / 128 / 256
=========================================================

Portée
------

- Cette annexe fournit des **schémas d’implémentation de référence** (non normatifs) pour :
  - l’encodage / décodage de séquences USC‑96 ;
  - la structuration de messages en trames (en‑tête + payload USC) ;
  - un format JSON canonique pour le transport et le debug.
- Elle complète :
  - l’Annexe A (tables de symboles),
  - l’Annexe B (grammaire EBNF),
  - et les scénarios de la Partie IV (compatibilité réseaux & systèmes).

Encodeur / décodeur USC‑96 (pseudo‑code)
----------------------------------------

Hypothèses :

- chaque symbole USC‑96 est représenté par un **ID** dans \[0, 95\] ;
- l’encodage sur le fil utilise **1 octet par symbole** : `0XXXXXXX`, avec `XXXXXXX = ID` (7 bits).

### Encodeur USC‑96

Signature :

- `encode_usc96(ids: liste<int>) -> octets`

Pseudo‑code :

```text
function encode_usc96(ids):
    buffer = new ByteArray()

    for id in ids:
        if id < 0 or id > 95:
            raise Error("ID hors plage USC‑96")

        code7 = id              # déjà sur 7 bits
        octet = code7 & 0x7F    # forcer les 7 bits de poids faible
        # MSB = 0 pour USC‑96
        buffer.append(octet)    # 0XXXXXXX

    return buffer
```

### Décodeur USC‑96

Signature :

- `decode_usc96(data: octets) -> liste<int>`

Pseudo‑code :

```text
function decode_usc96(data):
    ids = new List<int>()

    for octet in data:
        code7 = octet & 0x7F    # ignorer le MSB
        if code7 > 95:
            raise Error("Symbole hors plage USC‑96 dans flux USC‑96 strict")

        ids.append(code7)

    return ids
```

Remarques :

- dans un protocole mixte USC‑96 / USC‑128 / USC‑256, le bit de poids fort (MSB) PEUT être utilisé :
  - comme bit de profil (0 = USC‑96/128, 1 = extension, framing, etc.) ;
  - ou laissé à 0 et géré dans l’en‑tête de trame (version, profil).

Trame binaire type
------------------

Pour le transport sur un canal binaire (TCP, LoRa, HF, etc.), une trame USC‑96 peut suivre le format suivant (exemple) :

```text
Byte 0   : MAGIC_0 (0x55)
Byte 1   : MAGIC_1 (0x43)       ; 'U' 'C' pour "USC"
Byte 2   : VERSION              ; ex. 0x01
Byte 3   : PROFILE              ; ex. 0x60 = USC‑96, 0x80 = USC‑128, 0xC0 = USC‑256
Byte 4   : LENGTH (N)           ; nombre de symboles USC dans le payload (0..255)
Bytes 5..(5+N-1) : PAYLOAD      ; N octets, chacun = 1 symbole USC‑96 encodé
Last 2 bytes     : CHECKSUM     ; ex. CRC‑16 sur bytes 0..(5+N-1)
```

Pseudo‑code de construction :

```text
function make_usc96_frame(ids):
    payload = encode_usc96(ids)
    N = length(payload)
    if N > 255:
        raise Error("Payload trop long pour ce format de trame")

    frame = new ByteArray()
    frame.append(0x55)          # MAGIC_0
    frame.append(0x43)          # MAGIC_1
    frame.append(0x01)          # VERSION
    frame.append(0x60)          # PROFILE = USC‑96
    frame.append(N)             # LENGTH
    frame.extend(payload)       # PAYLOAD

    crc = crc16(frame)          # fonction standard
    frame.append(crc & 0xFF)    # LSB
    frame.append((crc >> 8) & 0xFF)  # MSB

    return frame
```

Format JSON canonique
---------------------

Pour le debug, la documentation et certains transports (HTTP, WebSocket), un format JSON simple peut être utilisé :

```json
{
  "usc_version": "96-v1.0",
  "profile": "usc-96",
  "symbols": [1, 80, 16, 86, 93, 34, 83, 28, 88],
  "meta": {
    "disc": "DISC-MED",
    "source": "ENT-MACHINE",
    "timestamp": 1714070400
  }
}
```

Contraintes recommandées :

- `usc_version` : DOIT être une chaîne identifiant la variante (96/128/256) et la version de spec ;
- `profile` : PEUT préciser un sous‑ensemble ou un profil d’usage (ex. `"usc-96-lora"`, `"usc-128-sci"`) ;
- `symbols` : liste d’IDs USC (entiers) ;
- `meta` : objet optionnel contenant des indications de domaine (`DISC-*`), source (`META-SOURCE`), confiance (`META-CONFID`), etc.

Profil USC‑128 / USC‑256
------------------------

Les encodeurs/décodeurs pour USC‑128 / USC‑256 suivent la même logique :

- USC‑128 :
  - IDs 0–127 autorisés ;
  - encodeur/décodeur identique à USC‑96, mais sans la contrainte “≤95” ;
  - `PROFILE` différent dans l’en‑tête (par ex. 0x80).
- USC‑256 :
  - IDs 0–255 autorisés ;
  - même format 1 octet = 1 symbole ;
  - `PROFILE` adapté (par ex. 0xC0) ;
  - les profils applicatifs DOIVENT documenter :
    - quels blocs de symboles sont utilisés (PHYS-*, CHEM-*, BIO-*, etc.).

Mapping USC ↔ structures internes
---------------------------------

Pour un moteur d’IA ou un service, les structures internes peuvent suivre la grammaire de l’Annexe B :

- un “message USC” interne est un arbre ou graphe :
  - nœuds typés (`ENT-*`, `AX-*`, `OP-*`, `STR-*`, etc.) ;
  - arêtes étiquetées (`REL-*`, opérandes, attributs) ;
- les encodeurs :
  - projettent cet arbre sur une séquence de symboles (typiquement via un parcours déterministe) ;
- les décodeurs :
  - reconstruisent un arbre à partir de la séquence, selon les règles EBNF.

Les détails de ce mapping dépendent du profil, mais DOIVENT rester :

- déterministes ;
- spécifiés (documents “USC ↔ MML” par domaine ou protocole).

Résumé
------

- USC‑96, USC‑128 et USC‑256 peuvent être implémentés avec :
  - un encodeur simple (1 octet par symbole) ;
  - des trames structurées (en‑tête + payload + checksum) ;
  - un format JSON canonique pour les usages REST/WebSocket et le debug.
- Cette annexe propose une **implémentation de référence** ;  
  des implémentations réelles PEUVENT varier, tant qu’elles :
  - respectent les tables (Annexe A),
  - suivent la grammaire (Annexe B),
  - et documentent clairement leur encodage.


