PARTIE II — ARCHITECTURE USC‑96 / USC‑128 / USC‑256  
Chapitre 4 — USC‑96 : Le Core Ultra‑Compact
===========================================

> **Statut** : squelette + résumé, détaillé ensuite en lien avec `usc_96_table.md`.

4.1 Rôle : survivre à toutes les pertes de capacité
---------------------------------------------------

- Décrire USC‑96 comme **noyau minimal** pour :
  - environnements radio très contraints,
  - microcontrôleurs limités,
  - archivage de base.  
- Expliquer pourquoi 96 symboles est un compromis entre :
  - expressivité,
  - compacité (7 bits par symbole),
  - simplicité de mise en œuvre.

4.2 Alphabet minimal universel
------------------------------

- Présenter les grandes familles de symboles de USC‑96 :
  - axiomes (AX‑*),
  - relations (REL‑*),
  - opérations (OP‑*),
  - structures (STR‑*),
  - nombres et unités minimales (NUM‑*, UNIT‑*),
  - entités génériques (ENT‑*).  
- Expliquer le principe : **tous les autres symboles USC‑128 / USC‑256 doivent pouvoir se reconstruire conceptuellement à partir de ce noyau**.

4.3 Contraintes de conception
-----------------------------

- Lister les contraintes :
  - pas de polysémie,
  - pas de synonymie interne,
  - recouvrement minimal entre symboles,
  - compatibilité ascendante garantie avec USC‑128 / USC‑256.

4.4 Bandes de symboles
----------------------

- 4.4.1 Bloc logique (CTRL‑*, quantificateurs, etc.)  
- 4.4.2 Bloc relationnel (REL‑*)  
- 4.4.3 Bloc opérationnel (OP‑*)  
- 4.4.4 Bloc d’axiomes universels (AX‑*)  
- 4.4.5 Bloc numérique condensé (NUM‑*, UNIT‑*)

Chaque sous‑section détaillera :

- les symboles concernés (en renvoyant à `usc_96_table.md`) ;
- leur rôle dans les scénarios minimaux ;
- des exemples de messages USC‑96.

4.5 Utilisations typiques
-------------------------

- IA embarquées ultra‑légères.  
- Drones, nanosats, robots simples.  
- Protocoles d’urgence (alerte, détresse, états critiques).  
- Cryptographie symbolique en petit alphabet.

4.6 Espace symbolique exact
---------------------------

- Référence directe à la table canonique : `usc_96_table.md`.  
- Définition des IDs, classes, gloss, règles d’encodage (7 bits, octet, MSB réservé).  
- Exemples de trames binaires annotées.


