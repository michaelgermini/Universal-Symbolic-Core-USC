Universal Symbolic Core — Table canonique USC‑96 (v0.1)
======================================================

Portée
------

- **USC‑96** : noyau ultra‑compact, stable, intemporel.
- **Objectif** : liste fermée de **96 symboles** numérotés `0..95`, chacun avec :
  - un **ID décimal** (`ID`),
  - une **désignation canonique** (`SYMBOL`),
  - une **classe symbolique** (`CLASS`),
  - une **description courte** (`GLOSS`).
- **Encodage binaire** : chaque symbole USC‑96 est encodé sur **7 bits** (valeur entière `ID`).

Règle d’encodage USC‑96
-----------------------

- **ID** : entier dans \[0, 95\].
- **CODE7** : représentation binaire sur 7 bits, zero‑padded.
  - Formule : `CODE7 = binary(ID).zfill(7)`.
  - Exemple : `ID=0 → 0000000`, `ID=5 → 0000101`, `ID=95 → 1011111`.
- **Sur le fil** :
  - Chaque symbole USC‑96 est transmis comme **un octet** (1 byte).
  - Le bit de poids fort (MSB) restant (8ᵉ bit) est **réservé** pour usage futur (par ex. parité, framing, version, extension).
  - Donc : `OCTET = 0b0XXXXXXX` avec `XXXXXXX = CODE7`.

Classes symboliques de USC‑96
-----------------------------

- **AX** : Axiomes ontologiques de base.
- **REL** : Relations sémantiques générales.
- **OP** : Opérations / fonctions conceptuelles.
- **STR** : Structures de données / topologiques.
- **CTRL** : Connecteurs logiques / contrôle de flux.
- **NUM / UNIT** : Nombres et unités minimales.
- **ENT** : Entités conceptuelles génériques.

Table canonique USC‑96 (v0.1)
-----------------------------

Cette table est **fermée** pour USC‑96 v0.1.  
Les extensions iront dans **USC‑128** et **USC‑256** sans modifier ces 96 premiers IDs.

### Bloc 0–15 : Axiomes ontologiques (AX‑*)

| ID | SYMBOL   | CLASS | GLOSS                                       |
|----|----------|-------|---------------------------------------------|
| 0  | NOP      | AX    | Aucun contenu / nul / padding               |
| 1  | AX-ENT   | AX    | Entité (quelque chose qui est)             |
| 2  | AX-STA   | AX    | État (configuration d’une entité)          |
| 3  | AX-EVT   | AX    | Événement (changement d’état)              |
| 4  | AX-VAR   | AX    | Variation / paramètre variable             |
| 5  | AX-TIME  | AX    | Temps                                      |
| 6  | AX-SPACE | AX    | Espace                                     |
| 7  | AX-MAT   | AX    | Matière                                    |
| 8  | AX-ENE   | AX    | Énergie                                    |
| 9  | AX-INF   | AX    | Information                                |
| 10 | AX-ID    | AX    | Identité / unicité                         |
| 11 | AX-PROB  | AX    | Probabilité                                |
| 12 | AX-CAUS  | AX    | Causalité (cause générale)                 |
| 13 | AX-PART  | AX    | Part / composant                           |
| 14 | AX-WHOLE | AX    | Tout / système complet                     |
| 15 | AX-SYS   | AX    | Système (ensemble structuré d’entités)     |

### Bloc 16–31 : Relations générales (REL‑*)

| ID | SYMBOL       | CLASS | GLOSS                                             |
|----|--------------|-------|---------------------------------------------------|
| 16 | REL-SUB      | REL   | “est un type de” / relation d’héritage (is‑a)    |
| 17 | REL-PART-OF  | REL   | “fait partie de” (part‑of)                        |
| 18 | REL-HAS      | REL   | “a / possède” (has)                               |
| 19 | REL-SIM      | REL   | similarité / ressemblance                         |
| 20 | REL-OPP      | REL   | opposition / contraire                            |
| 21 | REL-CAUSE    | REL   | “est cause de”                                    |
| 22 | REL-EFFECT   | REL   | “est effet de”                                    |
| 23 | REL-EQ       | REL   | égalité (==)                                      |
| 24 | REL-GT       | REL   | strictement supérieur (>)                         |
| 25 | REL-LT       | REL   | strictement inférieur (<)                         |
| 26 | REL-BEFORE   | REL   | avant (temporel)                                  |
| 27 | REL-AFTER    | REL   | après (temporel)                                  |
| 28 | REL-IN       | REL   | inclusion spatiale / logique (“dans”)            |
| 29 | REL-OUT      | REL   | exclusion / extérieur (“hors de”)                |
| 30 | REL-NEAR     | REL   | proximité spatiale / métrique                    |
| 31 | REL-CONNECT  | REL   | connexion / adjacence / lien                     |

### Bloc 32–47 : Opérations (OP‑*)

| ID | SYMBOL     | CLASS | GLOSS                                             |
|----|------------|-------|---------------------------------------------------|
| 32 | OP-DEF     | OP    | définir / introduire une entité / relation       |
| 33 | OP-REF     | OP    | référencer / pointer une entité existante        |
| 34 | OP-MEAS    | OP    | mesurer (input → valeur)                          |
| 35 | OP-COMP    | OP    | comparer (deux valeurs / entités)                |
| 36 | OP-ADD     | OP    | addition                                          |
| 37 | OP-SUB     | OP    | soustraction                                      |
| 38 | OP-MUL     | OP    | multiplication                                   |
| 39 | OP-DIV     | OP    | division                                         |
| 40 | OP-MOD     | OP    | modulo / reste                                   |
| 41 | OP-MAX     | OP    | maximum                                          |
| 42 | OP-MIN     | OP    | minimum                                          |
| 43 | OP-AVG     | OP    | moyenne                                          |
| 44 | OP-ENC     | OP    | encoder (dans un autre format / canal)           |
| 45 | OP-DEC     | OP    | décoder                                          |
| 46 | OP-MOVE    | OP    | déplacer (changer de position / état spatial)    |
| 47 | OP-CONVERT | OP    | convertir (type, unité, représentation)          |

### Bloc 48–63 : Structures & contrôle (STR‑*, CTRL‑*)

| ID | SYMBOL      | CLASS | GLOSS                                               |
|----|-------------|-------|-----------------------------------------------------|
| 48 | STR-SEQ     | STR   | séquence ordonnée                                  |
| 49 | STR-SET     | STR   | ensemble (sans ordre, sans doublons)               |
| 50 | STR-LIST    | STR   | liste ordonnée (avec doublons possibles)           |
| 51 | STR-GRAPH   | STR   | graphe général                                     |
| 52 | STR-NODE    | STR   | nœud de graphe                                     |
| 53 | STR-EDGE    | STR   | arête / lien de graphe                             |
| 54 | STR-TREE    | STR   | arbre (hiérarchie)                                 |
| 55 | STR-MAP     | STR   | dictionnaire / map (clé → valeur)                  |
| 56 | CTRL-IF     | CTRL  | conditionnel “si”                                  |
| 57 | CTRL-ELSE   | CTRL  | alternative “sinon”                                |
| 58 | CTRL-AND    | CTRL  | conjonction logique (ET)                           |
| 59 | CTRL-OR     | CTRL  | disjonction logique (OU)                           |
| 60 | CTRL-NOT    | CTRL  | négation logique                                   |
| 61 | CTRL-EXISTS | CTRL  | quantificateur existentiel (∃)                     |
| 62 | CTRL-FORALL | CTRL  | quantificateur universel (∀)                       |
| 63 | CTRL-LOOP   | CTRL  | itération / boucle                                 |

### Bloc 64–79 : Nombres & unités minimales (NUM‑*, UNIT‑*)

| ID | SYMBOL     | CLASS | GLOSS                                            |
|----|------------|-------|--------------------------------------------------|
| 64 | NUM-0      | NUM   | chiffre 0                                       |
| 65 | NUM-1      | NUM   | chiffre 1                                       |
| 66 | NUM-2      | NUM   | chiffre 2                                       |
| 67 | NUM-3      | NUM   | chiffre 3                                       |
| 68 | NUM-4      | NUM   | chiffre 4                                       |
| 69 | NUM-5      | NUM   | chiffre 5                                       |
| 70 | NUM-6      | NUM   | chiffre 6                                       |
| 71 | NUM-7      | NUM   | chiffre 7                                       |
| 72 | NUM-8      | NUM   | chiffre 8                                       |
| 73 | NUM-9      | NUM   | chiffre 9                                       |
| 74 | NUM-SEP    | NUM   | séparateur décimal (point / virgule abstrait)   |
| 75 | NUM-SIGN   | NUM   | signe (+ / −)                                   |
| 76 | NUM-PCT    | NUM   | pourcentage / ratio                              |
| 77 | NUM-RANGE  | NUM   | intervalle / plage de valeurs                    |
| 78 | UNIT-TIME  | UNIT  | unité de temps abstraite (ex. seconde canonique) |
| 79 | UNIT-LEN   | UNIT  | unité de longueur abstraite                      |

### Bloc 80–95 : Entités génériques (ENT‑*)

| ID | SYMBOL      | CLASS | GLOSS                                           |
|----|-------------|-------|-------------------------------------------------|
| 80 | ENT-AGENT   | ENT   | agent (entité agissante)                       |
| 81 | ENT-OBJECT  | ENT   | objet physique / chose                          |
| 82 | ENT-SIGNAL  | ENT   | signal / message transporté                     |
| 83 | ENT-DATA    | ENT   | donnée / information structurée                 |
| 84 | ENT-SYSTEM  | ENT   | système (ensemble organisé)                     |
| 85 | ENT-ORGANISM| ENT   | organisme vivant                                |
| 86 | ENT-HUMAN   | ENT   | humain (sous‑type d’organisme)                  |
| 87 | ENT-MACHINE | ENT   | machine / dispositif artificiel                 |
| 88 | ENT-ENV     | ENT   | environnement / milieu                          |
| 89 | ENT-LOCATION| ENT   | lieu / position spatiale                        |
| 90 | ENT-RESOURCE| ENT   | ressource (énergie, matière, data…)             |
| 91 | ENT-RISK    | ENT   | risque / menace potentielle                     |
| 92 | ENT-GOAL    | ENT   | but / objectif                                  |
| 93 | ENT-ACTION  | ENT   | action / opération concrète                     |
| 94 | ENT-STATE   | ENT   | état concret d’une entité                       |
| 95 | ENT-EVENT   | ENT   | événement concret (changement d’état daté)      |

Encodage sur le fil : exemple simple
------------------------------------

Rappel : USC‑96 utilise un **octet par symbole** (`0b0XXXXXXX`), `XXXXXXX = CODE7`.

### Exemple 1 — Phrase conceptuelle minimale

Intention (informelle) :  
> “Un humain (agent) mesure une donnée de l’environnement.”

Séquence conceptuelle USC (symboles) :

1. `AX-ENT` (1) — on se place dans le cadre “entité”.
2. `ENT-AGENT` (80)
3. `REL-SUB` (16)
4. `ENT-HUMAN` (86)
5. `ENT-ACTION` (93)
6. `OP-MEAS` (34)
7. `ENT-DATA` (83)
8. `REL-IN` (28)
9. `ENT-ENV` (88)

Séquence d’IDs (décimal) :

- `1, 80, 16, 86, 93, 34, 83, 28, 88`

Si on encode naïvement chaque ID en binaire sur 7 bits, on obtient `CODE7` :

- 1   → `0000001`
- 80  → `1010000`
- 16  → `0010000`
- 86  → `1010110`
- 93  → `1011101`
- 34  → `0100010`
- 83  → `1010011`
- 28  → `0011100`
- 88  → `1011000`

Et sur le fil, chaque symbole devient un octet `0XXXXXXX` (MSB=0).  
Exemple pour `ENT-HUMAN` (ID 86) :

- ID = 86  
- CODE7 = `1010110`  
- OCTET = `01010110` (0x56 en hex)

Interopération (esquisse)
-------------------------

Cette table USC‑96 peut être mappée vers :

- **Unicode** : via un bloc privé (Private Use Area) où chaque `ID` est associé à un codepoint dédié.
- **RDF / OWL** : chaque `SYMBOL` devient un IRI stable, par ex. `usc:ENT-HUMAN`, avec :
  - `usc:ENT-HUMAN rdf:type owl:Class`,
  - `usc:REL-SUB rdf:type owl:ObjectProperty`, etc.
- **JSON / XML** : on peut représenter une séquence USC comme :

```json
{
  "usc_version": "96-v0.1",
  "symbols": [1, 80, 16, 86, 93, 34, 83, 28, 88]
}
```

ou bien en forme développée :

```json
{
  "usc_version": "96-v0.1",
  "symbols": [
    { "id": 1, "symbol": "AX-ENT" },
    { "id": 80, "symbol": "ENT-AGENT" },
    { "id": 16, "symbol": "REL-SUB" },
    { "id": 86, "symbol": "ENT-HUMAN" },
    { "id": 93, "symbol": "ENT-ACTION" },
    { "id": 34, "symbol": "OP-MEAS" },
    { "id": 83, "symbol": "ENT-DATA" },
    { "id": 28, "symbol": "REL-IN" },
    { "id": 88, "symbol": "ENT-ENV" }
  ]
}
```

Évolution
---------

- Cette table USC‑96 est une **proposition v0.1** :
  - les **IDs 0–95 sont gelés** pour USC‑96,
  - les symboles supplémentaires iront dans **USC‑128** et **USC‑256**.
- On peut dériver :
  - une table **USC‑128** qui ajoute 32 symboles (96–127) pour les math / sciences,
  - une table **USC‑256** qui complète avec des domaines disciplinaires.

Pour aller plus loin, on peut :

- définir un **mapping RDF/OWL** complet pour chaque symbole,
- spécifier un **format binaire de trame** (en-tête, longueur, checksum, etc.),
- ajouter des **exemples normatifs** pour différents cas d’usage (radio HF, stockage, inter‑IA).


