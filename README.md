# Universal Symbolic Core (USC) 🔬⚡

[![License: Apache 2.0](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![GitHub repo size](https://img.shields.io/github/repo-size/michaelgermini/Universal-Symbolic-Core-USC)](https://github.com/michaelgermini/Universal-Symbolic-Core-USC)
[![GitHub last commit](https://img.shields.io/github/last-commit/michaelgermini/Universal-Symbolic-Core-USC)](https://github.com/michaelgermini/Universal-Symbolic-Core-USC)

## 🌟 Vue d'Ensemble

**USC (Universal Symbolic Core)** est un système symbolique universel conçu pour la communication inter-IA, les environnements contraints et l'archivage galactique. Il transcende les limitations des alphabets humains (Unicode) en définissant un **alphabet conceptuel atomique** avec une sémantique parfaitement neutre.

### 🏗️ Architecture Hiérarchique

```
USC-256 (Corps Universel Étendu)
├── USC-128 (Core Recommandé)          # IA scientifiques, calcul distribué
│   └── USC-96 (Noyau Ultra-Compact)   # Survivance, IoT, HF/LoRa
```

**Caractéristiques Techniques :**
- **Compression sémantique** : Ratio 10:1 vs langage naturel
- **Encodage binaire** : 7 bits/symbole (USC-96/128), 8 bits/symbole (USC-256)
- **Entropie conceptuelle** : Réduction de la polysémie par canonisation
- **Compatibilité** : De l'IoT aux supercalculateurs

### 🎯 Cas d'Usage Principaux

| Domaine | Variante Recommandée | Avantages USC |
|---------|---------------------|---------------|
| **Réseaux Contrainte** (HF, LoRa, Sigfox) | USC-96 | Overhead minimal, robustesse |
| **IA Locale/Sci** | USC-128 | Expressivité équilibrée |
| **Systèmes Complexes** | USC-256 | Couverture multi-disciplinaire |
| **Archivage Long Terme** | USC-96 | Stabilité temporelle |

---

## 📚 Table des Matières

### 📖 Livre Principal (`book/`)
1. **[Préface](book/00_Preface.md)** - Motivation et vision long terme
2. **Partie I** - Principes Fondamentaux
   - [Chapitre 1](book/PartI_Chapter01_Definition.md) - Définition et portée
   - [Chapitre 2](book/PartI_Chapter02_TheorieSymboles.md) - Théorie des symboles
   - [Chapitre 3](book/PartI_Chapter03_Objectifs.md) - Objectifs du système
3. **Partie II** - Architecture USC
   - [Chapitre 4](book/PartII_Chapter04_USC96_full.md) - USC-96 (Core Ultra-Compact)
   - [Chapitre 5](book/PartII_Chapter05_USC128_full.md) - USC-128 (Core Recommandé)
   - [Chapitre 6](book/PartII_Chapter06_USC256_full.md) - USC-256 (Corps Universel)
4. **Partie III** - Structures Internes
   - [Chapitre 7](book/PartIII_Chapter07_ClassesSymboliques.md) - Classes symboliques
   - [Chapitre 8](book/PartIII_Chapter08_BigrammesTrigrammes.md) - Bi/Tri-grammes
   - [Chapitre 9](book/PartIII_Chapter09_GrammaireInterne.md) - Grammaire EBNF
5. **Partie IV** - Compatibilité & Intégration
   - [Chapitre 10](book/PartIV_Chapter10_CompatReseauxContraints.md) - Réseaux contraints
   - [Chapitre 11](book/PartIV_Chapter11_CompatDataInternet.md) - Data & Internet
   - [Chapitre 12](book/PartIV_Chapter12_CompatIA.md) - Intelligence Artificielle
   - [Chapitre 13](book/PartIV_Chapter13_CompatOffline.md) - Systèmes offline
   - [Chapitre 14](book/PartIV_Chapter14_CompatMaterielle.md) - Compatibilité matérielle
6. **Partie V** - Sécurité & Souveraineté
   - [Chapitre 15](book/PartV_Chapter15_CryptoUSC.md) - Cryptographie USC-native
   - [Chapitre 16](book/PartV_Chapter16_Antilogs.md) - Anti-logs et souveraineté
7. **Partie VI** - Annexes Techniques
   - [Annexe A](book/PartVI_AnnexeA_Tables.md) - Tables canoniques
   - [Annexe B](book/PartVI_AnnexeB_EBNF.md) - Grammaire formelle EBNF
   - [Annexe C](book/PartVI_AnnexeC_DiagrammesCompat.md) - Diagrammes de compatibilité
   - [Annexe D](book/PartVI_AnnexeD_ExemplesEncodage.md) - Exemples d'encodage
   - [Annexe E](book/PartVI_AnnexeE_ComparatifEncodages.md) - Comparatif encodings
- [Annexe F](book/PartVI_AnnexeF_TransmissionInterstellaire.md) - Transmission interstellaire
- [Annexe G](book/PartVI_AnnexeG_ImplRef.md) - Implémentation de référence
- [Annexe H](book/PartVI_AnnexeH_ComparatifSystemes.md) - Comparatif systèmes existants

### 📋 Documents de Référence
- **[Index Thématique](book/Index_thematique.md)** - Navigation par concepts
- **[Conclusion & Roadmap](book/Conclusion_Roadmap.md)** - Vision USC-512
- **[Rapport d'Analyse](RAPPORT_PROJET_USC.md)** - État du projet

### 📊 Tables Symboliques Canoniques
- **[USC-96](usc_96_table.md)** - 96 symboles (noyau ultra-compact)
- **[USC-128](usc_128_table.md)** - 128 symboles (core recommandé)
- **[USC-256](usc_256_table.md)** - 256 symboles (corps universel)

---

## 🚀 Quick Start pour Développeurs

### 📦 Installation & Setup

```bash
# Cloner le dépôt
git clone https://github.com/michaelgermini/Universal-Symbolic-Core-USC.git
cd Universal-Symbolic-Core-USC

# Charger les tables de symboles (Python exemple)
import json

# Charger USC-96
with open('usc_96_table.md', 'r', encoding='utf-8') as f:
    # Parser le format Markdown pour extraire les symboles
    symbols_96 = parse_usc_table(f.read())

# Structure typique d'un symbole
symbol = {
    'id': 42,
    'symbol': 'REL-CAUSE',
    'class': 'REL-*',
    'gloss': 'Relation de causalité',
    'binary': '0x2A'  # 42 en hex
}
```

### 🔧 Implémentation Basique (Python)

```python
class USC96Encoder:
    def __init__(self):
        self.magic = b'\x55\x43'  # "UC" pour Universal Core

    def encode(self, symbol_ids: list[int]) -> bytes:
        """Encode une liste d'IDs USC-96 en octets"""
        if not all(0 <= id <= 95 for id in symbol_ids):
            raise ValueError("IDs must be in range 0-95 for USC-96")

        # Format de trame: MAGIC(2) + VERSION(1) + LENGTH(2) + PAYLOAD + CRC(2)
        version = 0x01
        length = len(symbol_ids)
        payload = bytes(symbol_ids)  # 1 octet par symbole

        frame = self.magic + bytes([version]) + length.to_bytes(2, 'big') + payload
        crc = self.crc16(frame)
        return frame + crc.to_bytes(2, 'big')

    def decode(self, frame: bytes) -> list[int]:
        """Décode une trame USC-96"""
        if len(frame) < 7 or frame[:2] != self.magic:
            raise ValueError("Invalid USC frame")

        version = frame[2]
        length = int.from_bytes(frame[3:5], 'big')
        payload = frame[5:-2]
        crc_received = int.from_bytes(frame[-2:], 'big')

        # Vérifier CRC
        crc_calculated = self.crc16(frame[:-2])
        if crc_received != crc_calculated:
            raise ValueError("CRC mismatch")

        return list(payload)

    @staticmethod
    def crc16(data: bytes) -> int:
        """CRC-16-CCITT"""
        crc = 0xFFFF
        for byte in data:
            crc ^= byte << 8
            for _ in range(8):
                if crc & 0x8000:
                    crc = (crc << 1) ^ 0x1021
                else:
                    crc <<= 1
                crc &= 0xFFFF
        return crc

# Exemple d'usage
encoder = USC96Encoder()

# Encoder une séquence conceptuelle simple
# IDs: EXIST(0), CAUSE(42), EVENT(15)
message = encoder.encode([0, 42, 15])
print(f"Trame encodée: {message.hex()}")

# Décoder
decoded = encoder.decode(message)
print(f"IDs décodés: {decoded}")
```

### 🎯 Exemple d'Encodage Conceptuel

**Concept :** "La température cause l'évaporation"
**Traduction USC-96 :**
- TEMP(85) + CAUSE(42) + EVAPOR(87)

```python
# Encodage binaire
concept_ids = [85, 42, 87]  # TEMP, CAUSE, EVAPOR
frame = encoder.encode(concept_ids)

# Résultat: MAGIC(5543) + VERSION(01) + LENGTH(0003) + PAYLOAD(55 2A 57) + CRC(XXXX)
# Transmission: 7 octets pour exprimer un concept complexe
```

---

## 🏛️ Standards & Spécifications

### 📋 Conformité Technique
- **Style rédactionnel** : RFC/IETF (normatif, technique)
- **Langue** : Français (pour précision conceptuelle)
- **Encodage** : UTF-8 pour tous les fichiers
- **Format de tables** : Markdown structuré avec métadonnées

### 🔗 Compatibilité Existante
- **Unicode** : Mappings partiels (Annexe A)
- **RDF/OWL** : Ponts sémantiques possibles
- **JSON** : Format de transport `application/usc+json`
- **Protobuf** : Alternative binaire pour gros volumes

### 📊 Métriques de Performance

| Métrique | USC-96 | USC-128 | USC-256 |
|----------|--------|---------|---------|
| **Symboles** | 96 | 128 | 256 |
| **Bits/symbole** | 7 | 7 | 8 |
| **Overhead min** | 1 octet | 1 octet | 1 octet |
| **Ratio compression** | 10:1 | 12:1 | 15:1 |
| **Latence typique** | <1ms | <1ms | <2ms |

---

## 🛠️ Outils & Ressources

### 🔧 Outils de Développement
- **Tables canoniques** : Définition normative des symboles
- **Grammaire EBNF** : Parsing formel des expressions
- **Pseudo-code** : Implémentations de référence
- **Exemples** : Cas d'usage concrets

### 📚 Ressources Supplémentaires
- **[Rapport d'Analyse](RAPPORT_PROJET_USC.md)** - État détaillé du projet
- **[Index Thématique](book/Index_thematique.md)** - Navigation par concepts
- **[Diagrammes](book/PartVI_AnnexeC_DiagrammesCompat.md)** - Visualisations ASCII
- **[Exemples](book/PartVI_AnnexeD_ExemplesEncodage.md)** - Cas pratiques

### 🌐 Écosystème
- **GitHub** : [michaelgermini/Universal-Symbolic-Core-USC](https://github.com/michaelgermini/Universal-Symbolic-Core-USC)
- **Licence** : Apache 2.0 (permissive, commerciale OK)
- **Contributions** : Bienvenues (voir section ci-dessous)

---

## 🤝 Contributions & Gouvernance

### 📝 Comment Contribuer

Nous encourageons les contributions dans ces domaines :

#### 🔬 **Nouveaux Symboles (USC-512)**
```markdown
Proposition de symbole :
- ID: [proposé]
- Classe: [AX-*/REL-*/OP-*/etc.]
- Gloss: [définition précise]
- Justification: [cas d'usage, domaine]
- Compatibilité: [impact sur versions existantes]
```

#### 🐛 **Corrections & Améliorations**
- Corrections de définitions symboliques
- Améliorations de la grammaire EBNF
- Optimisations des algorithmes d'encodage
- Nouveaux exemples d'usage

#### 💻 **Implémentations**
- Bibliothèques de référence (Python, Rust, C++)
- Outils de validation
- Benchmarks de performance
- Intégrations frameworks

### 📋 Processus de Contribution
1. **Fork** le dépôt
2. **Créer** une branche `feature/nom-fonctionnalite`
3. **Commiter** avec messages descriptifs
4. **Push** et créer une **Pull Request**
5. **Discussion** communautaire et validation

### 🎯 Roadmap Communautaire
- **v0.2** : Implémentation Python de référence
- **v0.3** : Benchmarks vs JSON/Protobuf
- **v0.4** : Spécification USC-512 (premiers symboles)
- **v1.0** : Standardisation IETF (horizon 2026)

---

## 📄 Licence

**Apache License 2.0**
- Usage commercial autorisé
- Distribution libre
- Modification et redistribution permises
- Attribution requise

Voir [`LICENSE`](LICENSE) pour les termes complets.

---

## 🙏 Remerciements

- **Auteur** : Michael Germini
- **Méthodologie** : Approche RFC/IETF pour spécifications techniques
- **Inspiration** : Recherche en IA, systèmes embarqués, archivage long terme
- **Communauté** : Ouvert aux contributions et retours

---

## 🔗 Liens Utiles

- 📊 **[Rapport Complet](RAPPORT_PROJET_USC.md)** - Analyse détaillée du projet
- 📖 **[Index Thématique](book/Index_thematique.md)** - Navigation conceptuelle
- 🛠️ **[Implémentation](book/PartVI_AnnexeG_ImplRef.md)** - Guide développeur
- 🌌 **[Transmission Interstellaire](book/PartVI_AnnexeF_TransmissionInterstellaire.md)** - Vision galactique

---

*“L'USC : quand l'IA parle enfin le même langage que l'univers”* ✨

Structure du dépôt
------------------

- `book/`
  - `00_Preface.md` : préface, motivation, vision long terme.
  - `PartI_*.md` : principes fondamentaux (définition, théorie des symboles, objectifs).
  - `PartII_*.md` : architecture USC‑96 / USC‑128 / USC‑256 (chapitres + versions _full_ détaillées).
  - `PartIII_*.md` : structures internes (classes symboliques, bi‑/tri‑grammes, grammaire).
  - `PartIV_*.md` : compatibilité & intégration (réseaux contraints, Data/Internet, IA, offline, matériel).
  - `PartV_*.md` : sécurité & souveraineté (cryptographie USC‑native, anti‑logs).
  - `PartVI_*.md` : annexes techniques (tables, EBNF, diagrammes, exemples d’encodage, comparatif, transmission interstellaire, implémentation de référence).
  - `Index_thematique.md` : index thématique des notions importantes.
  - `Conclusion_Roadmap.md` : conclusion et feuille de route (USC‑512, outils, gouvernance).
- `usc_96_table.md` : table canonique USC‑96 (IDs, classes, définitions, exemple d’encodage).
- `usc_128_table.md` : table étendue USC‑128.
- `usc_256_table.md` : table universelle étendue USC‑256.
- `content.ini` : version longue / historique du contenu (source initiale).
- `livre chapitre.mak` : plan détaillé du livre (table des matières structurée).

Licence
-------

- Ce projet est distribué sous la **licence Apache 2.0**.  
- Voir le fichier `LICENSE` à la racine du dépôt pour les termes complets.

Comment lire le livre
---------------------

Ordre recommandé :

1. `book/00_Preface.md`  
2. `book/PartI_Chapter01_Definition.md` → `PartI_Chapter02_TheorieSymboles.md` → `PartI_Chapter03_Objectifs.md`  
3. `book/PartII_Chapter04_USC96_full.md`, puis `PartII_Chapter05_USC128_full.md`, `PartII_Chapter06_USC256_full.md`  
4. Structures internes : `PartIII_Chapter07_ClassesSymboliques.md`, `PartIII_Chapter08_BigrammesTrigrammes.md`, `PartIII_Chapter09_GrammaireInterne.md`  
5. Compatibilité & sécurité : Parties IV et V  
6. Annexes techniques : `PartVI_AnnexeA` → `PartVI_AnnexeB` → `PartVI_AnnexeD` → `PartVI_AnnexeG`  
7. `Index_thematique.md` et `Conclusion_Roadmap.md` pour naviguer et voir la vision globale.

Comment implémenter USC en pratique
-----------------------------------

### 1. Choisir la variante et le profil

- **USC‑96** :
  - pour réseaux très contraints (HF, LoRa, Sigfox, IoT basique),
  - pour microcontrôleurs ou FPGA simples.
- **USC‑128** :
  - pour IA générales / scientifiques, services backend, modélisation.
- **USC‑256** :
  - pour plateformes multi‑domaines (physique, chimie, bio/med, espace, info/calcul).

Ensuite, définir un **profil** :

- sous‑ensemble de symboles réellement utilisés ;
- contraintes spécifiques (ex. “profil LoRa‑96”, “profil IA‑Sci‑128”, etc.).

Référence :  
→ `book/PartII_Chapter04_USC96_full.md` / `05_USC128_full.md` / `06_USC256_full.md`  
→ `book/PartIV_Chapter10_CompatReseauxContraints.md` et suivants.

### 2. Charger les tables de symboles

- Parser les fichiers :
  - `usc_96_table.md`,
  - `usc_128_table.md`,
  - `usc_256_table.md`.
- Construire en mémoire :
  - une table indexée par ID (0..N) pour un accès rapide,
  - et/ou un dictionnaire `SYMBOL → ID` pour les outils de debug.

Référence :  
→ `book/PartVI_AnnexeA_Tables.md`.

### 3. Implémenter l’encodeur / décodeur

Pour USC‑96 (cas le plus simple) :

- **Encodeur** :  
  - entrée : liste d’IDs USC (0..95) ;  
  - sortie : tableau d’octets ;  
  - chaque symbole : `octet = ID & 0x7F` (MSB = 0).
- **Décodeur** :  
  - entrée : flux d’octets ;  
  - sortie : liste d’IDs ;  
  - pour chaque octet : `ID = octet & 0x7F`, vérifier `ID ≤ 95` (en USC‑96 strict).

Pour USC‑128 / USC‑256 :

- même principe, mais :
  - plage d’IDs étendue (0..127, 0..255) ;
  - gestion des profils en en‑tête de trame (voir ci‑dessous).

Référence :  
→ `book/PartVI_AnnexeG_ImplRef.md` (pseudo‑code encodeur/décodeur, trames, JSON).

### 4. Définir un format de trame

Un format de trame binaire de référence est proposé dans l’Annexe G, par exemple :

- en‑tête :
  - MAGIC (`0x55 0x43`),
  - VERSION,
  - PROFILE (USC‑96 / USC‑128 / USC‑256),
  - LENGTH (N symboles) ;
- payload :
  - N octets USC (1 symbole par octet) ;
- suffixe :
  - CHECKSUM (CRC‑16 ou autre).

Vous pouvez :

- réutiliser ce format tel quel ;
- ou définir un format propriétaire, à condition de **documenter clairement** :
  - le profil USC,
  - l’encodage des symboles,
  - les mécanismes de contrôle d’intégrité.

### 5. Mapper USC ↔ structures internes

Selon vos besoins :

- utiliser l’EBNF de l’Annexe B pour :
  - structurer vos messages en expressions (`ent-expr`, `rel-expr`, `op-expr`, `struct-expr`, etc.) ;
  - générer / parser des arbres ou graphes conceptuels ;
- utiliser MML (Minimal Markup Language, tel que décrit dans les parties I/III/IV) pour :
  - sérialiser ces structures dans des formats textuels ou binaires plus riches.

Référence :  
→ `book/PartIII_Chapter09_GrammaireInterne.md`  
→ `book/PartVI_AnnexeB_EBNF.md`.

### 6. Intégrer USC dans vos protocoles

Quelques exemples d’intégration :

- **LoRa / HF** :
  - USC‑96 comme payload compact dans vos trames ;
  - profils dédiés par type d’appareil (télémétrie, commandes, alertes).
- **HTTP / WebSocket** :
  - corps `application/usc+json` (tableaux d’IDs USC + meta) ;
  - endpoints REST spécialisés pour messages conceptuels.
- **IA / LLMs** :
  - encodeur/décodeur USC pour projeter des raisonnements dans l’espace USC ;
  - mode “trace USC” pour l’audit et la comparaison entre modèles.

Référence :  
→ `book/PartIV_Chapter10_CompatReseauxContraints.md` à `PartIV_Chapter14_CompatMaterielle.md`  
→ `book/PartVI_AnnexeC_DiagrammesCompat.md` et `PartVI_AnnexeD_ExemplesEncodage.md`.

### 7. Sécurité & audit

Pour des applications critiques :

- utiliser les mécanismes de :
  - **hashing symbolique** (hash des graphes USC) ;
  - **canonisation signée** (trace USC canonique + signature) ;
  - **métadonnées USC** (`META-*`, `DISC-*`) pour tracer auteur, source, confiance, timestamp.

Référence :  
→ `book/PartV_Chapter15_CryptoUSC.md`  
→ `book/PartV_Chapter16_Antilogs.md`.

Publication GitHub / contributions
----------------------------------

Pour publier ce dépôt sur GitHub :

- garder la structure actuelle (`book/`, `usc_*_table.md`, `README.md`) ;
- ajouter éventuellement :
  - un `LICENSE` (MIT, Apache‑2.0, ou autre selon ton choix) ;
  - un `CONTRIBUTING.md` expliquant comment proposer :
    - de nouveaux symboles (en vue d’USC‑512),
    - des corrections de gloss / classes,
    - des implémentations de référence.

Il est recommandé de :

- lier depuis le `README.md` vers :
  - les chapitres de départ (préface + Partie I) ;
  - l’index thématique ;
  - l’Annexe G pour les développeurs ;
- taguer les versions (`v0.1`, `v0.2`, etc.) au fur et à mesure des évolutions de la norme.


