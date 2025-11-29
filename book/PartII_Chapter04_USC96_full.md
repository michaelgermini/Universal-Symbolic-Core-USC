PARTIE II — ARCHITECTURE USC‑96 / USC‑128 / USC‑256  
Chapitre 4 — USC‑96 : Le Core Ultra‑Compact
===========================================

4.1 Rôle : survivre à toutes les pertes de capacité
---------------------------------------------------

USC‑96 est le **noyau ultra‑compact** du Universal Symbolic Core.  
Il est conçu pour rester exploitable lorsque presque toutes les ressources sont limitées ou dégradées :

- débit extrêmement faible (quelques bits par seconde) ;
- puissance de calcul réduite (microcontrôleurs simples) ;
- mémoire limitée ;
- canaux radio bruités ou instables.

Objectifs principaux de USC‑96 :

- fournir un **vocabulaire conceptuel minimal** couvrant :
  - les axiomes ontologiques de base (entité, état, événement, temps, espace, matière, énergie, information…) ;
  - les relations essentielles (inclusion, causalité, similarité, ordre temporel, appartenance…) ;
  - les opérations fondamentales (mesurer, comparer, additionner, déplacer, encoder, convertir…) ;
  - quelques structures abstraites (séquence, ensemble, liste, graphe, arbre…) ;
  - des nombres et unités minimales ;
  - des entités génériques (agent, objet, système, donnée, environnement, action, événement…) ;
- permettre de **continuer à décrire** :
  - l’état d’un système,
  - des mesures critiques,
  - des ordres simples,
  même dans des scénarios de dégradation maximale.

Le choix de **96 symboles** répond à un compromis :

- **expressivité suffisante** pour couvrir des scénarios réels dans plusieurs domaines ;
- **compacité binaire** (7 bits par symbole, 1 octet sur le fil avec MSB réservé) ;
- **simplicité de mise en œuvre** dans le matériel et les logiciels :
  - tables statiques de petite taille,
  - décodage direct,
  - faible coût de stockage et de transmission.

4.2 Alphabet minimal universel
------------------------------

USC‑96 définit un **alphabet minimal universel**, structuré en six grandes familles de symboles (voir `usc_96_table.md`) :

- **AX‑*** : axiomes ontologiques (IDs 0–15)  
  - ex. `AX-ENT`, `AX-STA`, `AX-EVT`, `AX-VAR`, `AX-TIME`, `AX-SPACE`, `AX-MAT`, `AX-ENE`, `AX-INF`, `AX-ID`, `AX-PROB`, `AX-CAUS`, `AX-PART`, `AX-WHOLE`, `AX-SYS` ;
- **REL‑*** : relations générales (IDs 16–31)  
  - ex. `REL-SUB`, `REL-PART-OF`, `REL-HAS`, `REL-SIM`, `REL-OPP`, `REL-CAUSE`, `REL-EFFECT`, `REL-BEFORE`, `REL-AFTER`, `REL-IN`, `REL-OUT`, `REL-NEAR`, `REL-CONNECT` ;
- **OP‑*** : opérations conceptuelles (IDs 32–47)  
  - ex. `OP-DEF`, `OP-REF`, `OP-MEAS`, `OP-COMP`, `OP-ADD`, `OP-SUB`, `OP-MUL`, `OP-DIV`, `OP-MOD`, `OP-MAX`, `OP-MIN`, `OP-AVG`, `OP-ENC`, `OP-DEC`, `OP-MOVE`, `OP-CONVERT` ;
- **STR‑*** et **CTRL‑*** : structures et contrôle (IDs 48–63)  
  - ex. `STR-SEQ`, `STR-SET`, `STR-LIST`, `STR-GRAPH`, `STR-NODE`, `STR-EDGE`, `STR-TREE`, `STR-MAP`,  
    ainsi que `CTRL-IF`, `CTRL-ELSE`, `CTRL-AND`, `CTRL-OR`, `CTRL-NOT`, `CTRL-EXISTS`, `CTRL-FORALL`, `CTRL-LOOP` ;
- **NUM‑***, **UNIT‑*** : nombres et unités minimales (IDs 64–79)  
  - ex. `NUM-0..NUM-9`, `NUM-SEP`, `NUM-SIGN`, `NUM-PCT`, `NUM-RANGE`, `UNIT-TIME`, `UNIT-LEN` ;
- **ENT‑*** : entités génériques (IDs 80–95)  
  - ex. `ENT-AGENT`, `ENT-OBJECT`, `ENT-SIGNAL`, `ENT-DATA`, `ENT-SYSTEM`, `ENT-ORGANISM`, `ENT-HUMAN`, `ENT-MACHINE`, `ENT-ENV`, `ENT-LOCATION`, `ENT-RESOURCE`, `ENT-RISK`, `ENT-GOAL`, `ENT-ACTION`, `ENT-STATE`, `ENT-EVENT`.

Principe de conception :

- tous les symboles ajoutés dans **USC‑128** et **USC‑256** DOIVENT pouvoir être :
  - rattachés à ces familles de base,
  - interprétés comme des **spécialisations** ou raffinements de ces concepts noyaux.

Ainsi, même un système limité à USC‑96 :

- peut approximer ou partiellement interpréter des messages produits avec USC‑128 / USC‑256 ;
- dispose d’un **socle de compréhension universel** pour tout échange basé sur l’USC.

4.3 Contraintes de conception
-----------------------------

USC‑96 est soumis à des contraintes normatives fortes, qui s’appliquent à chaque symbole.

- **Pas de polysémie** :  
  - un symbole USC MUST correspondre à **un seul sens canonique** ;  
  - toute utilisation divergente est considérée comme non conforme.
- **Pas de synonymie interne** :  
  - deux symboles différents NE DOIVENT PAS recouvrir le même sens ;  
  - si un cas de synonymie est détecté, la norme DOIT :
    - soit fusionner les usages sur un seul symbole,
    - soit redéfinir précisément le champ de chacun.
- **Recouvrement minimal entre familles** :  
  - un même concept ne doit pas être défini à la fois comme axiome (`AX-*`) et comme entité (`ENT-*`) avec le même rôle ;  
  - les rôles de `AX-*`, `REL-*`, `OP-*`, `STR-*`, `CTRL-*`, `NUM-*`, `ENT-*` doivent rester clairement distincts.
- **Compatibilité ascendante garantie** :  
  - les IDs 0–95 et leur sémantique sont **gelés** dès publication de la norme ;  
  - aucune version ultérieure (USC‑128, USC‑256, USC‑512…) ne peut en changer le sens ;  
  - les nouvelles versions n’ajoutent que des symboles supplémentaires (IDs plus élevés).

Toute évolution de la norme USC‑96 MUST :

- préserver les IDs existants et leurs définitions canoniques ;
- décrire explicitement les dépréciations éventuelles, sans réutiliser les IDs libérés pour un autre sens.

4.4 Bandes de symboles
----------------------

USC‑96 est organisé en **bandes fonctionnelles**. Chaque bande regroupe des symboles jouant un rôle structurel similaire.

4.4.1 Bloc logique (CTRL‑*)
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Le bloc logique contient les symboles de contrôle et de logique minimale :

- `CTRL-IF`, `CTRL-ELSE` : conditionnel simple ;
- `CTRL-AND`, `CTRL-OR`, `CTRL-NOT` : connecteurs logiques de base ;
- `CTRL-EXISTS`, `CTRL-FORALL` : quantificateurs existentiel et universel ;
- `CTRL-LOOP` : itération / boucle.

Ces symboles permettent de :

- modéliser des décisions (“si… alors… sinon…”) ;
- combiner plusieurs conditions ;
- exprimer des généralisations (“pour tout”, “il existe”) ;
- représenter des processus répétitifs.

4.4.2 Bloc relationnel (REL‑*)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Le bloc relationnel contient les relations conceptuelles de base :

- hiérarchie et composition :
  - `REL-SUB` (is‑a / sous‑type de),
  - `REL-PART-OF` (partie de),
  - `REL-HAS` (possède) ;
- comparaison et ordre :
  - `REL-SIM` (similarité),
  - `REL-OPP` (opposition),
  - `REL-EQ`, `REL-GT`, `REL-LT` ;
- structure temporelle et spatiale :
  - `REL-BEFORE`, `REL-AFTER`,
  - `REL-IN`, `REL-OUT`, `REL-NEAR`, `REL-CONNECT`.

Ces relations permettent de construire des **graphes conceptuels** :

- taxonomies,
- décompositions en parties,
- chronologies,
- topologies simples.

4.4.3 Bloc opérationnel (OP‑*)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Le bloc opérationnel regroupe les actions conceptuelles de base :

- **gestion des entités et références** :
  - `OP-DEF` (définir une entité / relation),
  - `OP-REF` (référencer quelque chose de déjà défini) ;
- **mesure et comparaison** :
  - `OP-MEAS` (mesurer : input → valeur),
  - `OP-COMP` (comparer deux valeurs / entités) ;
- **arithmétique de base** :
  - `OP-ADD`, `OP-SUB`, `OP-MUL`, `OP-DIV`, `OP-MOD`, `OP-MAX`, `OP-MIN`, `OP-AVG` ;
- **transformation et transport** :
  - `OP-ENC`, `OP-DEC` (encoder / décoder),
  - `OP-MOVE` (déplacer),
  - `OP-CONVERT` (convertir type / unité / représentation).

Ces opérations permettent d’exprimer des **comportements de système** sans dépendre d’un langage de programmation particulier.

4.4.4 Bloc d’axiomes universels (AX‑*)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Le bloc d’axiomes universels définit la base ontologique :

- types généraux :
  - `AX-ENT` (entité),
  - `AX-STA` (état),
  - `AX-EVT` (événement),
  - `AX-VAR` (variable) ;
- dimensions fondamentales :
  - `AX-TIME` (temps),
  - `AX-SPACE` (espace),
  - `AX-MAT` (matière),
  - `AX-ENE` (énergie),
  - `AX-INF` (information) ;
- propriétés conceptuelles :
  - `AX-ID` (identité),
  - `AX-PROB` (probabilité),
  - `AX-CAUS` (causalité),
  - `AX-PART` (partie),
  - `AX-WHOLE` (tout / système),
  - `AX-SYS` (système structuré).

Ces axiomes forment le **socle minimal** qui permet de donner sens aux autres symboles, dans toutes les disciplines.

4.4.5 Bloc numérique condensé (NUM‑*, UNIT‑*)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Le bloc numérique condensé contient :

- les chiffres `NUM-0` à `NUM-9` ;
- les modificateurs `NUM-SEP` (séparateur décimal), `NUM-SIGN` (signe), `NUM-PCT` (pourcentage), `NUM-RANGE` (intervalle) ;
- des unités abstraites minimales :
  - `UNIT-TIME` (unité de temps canonique),
  - `UNIT-LEN` (unité de longueur canonique).

Il permet de représenter :

- des mesures simples (valeur + unité) ;
- des rapports (pourcentages) ;
- des bornes (plages de valeurs).

Sans imposer une écriture textuelle (ex. “3.14”), USC‑96 encode la **structure numérique** de façon conceptuelle.

4.5 Utilisations typiques
-------------------------

USC‑96 est destiné à des scénarios où chaque bit transmis ou stocké doit apporter un maximum de sens.

Exemples d’utilisation :

- **IA embarquées ultra‑légères** :
  - contrôle de processus industriels local ;
  - systèmes d’alerte embarqués ;
  - assistants IA minimalistes sur microcontrôleurs.  
- **Drones, nanosatellites, robots simples** :
  - télémétrie compacte (état, position, risque, objectif) ;
  - commandes simples (déplacer vers, mesurer, rapporter).  
- **Protocoles d’urgence** :
  - messages standardisés décrivant :
    - la nature de l’urgence (ENT-RISK, ENT-STATE),
    - la cause probable (REL-CAUSE, AX-CAUS),
    - l’action recommandée (ENT-ACTION, OP-MOVE, OP-MEAS).  
- **Cryptographie symbolique** :
  - utilisation des séquences de symboles comme vecteurs pour des fonctions de hachage ;
  - signatures et engagements sur des messages USC‑96 ;
  - schémas d’authentification offline basés sur des patterns symboliques.

4.6 Espace symbolique exact
---------------------------

La définition exhaustive de l’espace symbolique USC‑96 est donnée dans `usc_96_table.md` et récapitulée dans **l’Annexe A — Tables canoniques USC‑96 / USC‑128 / USC‑256**.

Spécification normative :

- **ID** : entier dans l’intervalle \[0, 95\] ;
- **CODE7** : représentation binaire sur 7 bits, zero‑padded ;
- **Octet sur le fil** :
  - format `0XXXXXXX`, où `XXXXXXX = CODE7` ;
  - le bit de poids fort (MSB) est réservé pour des usages de framing / parité / versioning.

Exemple (informel) :

- Intention : “un humain mesure une donnée de l’environnement” ;
- Séquence conceptuelle :
  - `AX-ENT`, `ENT-HUMAN`, `ENT-ACTION`, `OP-MEAS`, `ENT-DATA`, `REL-IN`, `ENT-ENV` ;
- IDs correspondants (cf. `usc_96_table.md`) :
  - `[1, 86, 93, 34, 83, 28, 88]` ;
- Encodage :
  - chaque ID → CODE7 (7 bits),
  - chaque symbole → 1 octet `0XXXXXXX` sur le fil.

Toute implémentation conforme USC‑96 MUST :

- respecter **exactement** les IDs, symboles, classes et descriptions de `usc_96_table.md` ;
- appliquer ce schéma d’encodage ou documenter rigoureusement toute variante (et son mapping).

4.7 Chaîne complète : concept → USC → binaire → décodage
--------------------------------------------------------

Cette section illustre un flux complet, depuis un énoncé conceptuel jusqu’au flux binaire sur le fil, puis son décodage.

### Étape 1 — Concept (niveau humain / IA)

Intention :  
> “Un drone mesure la température de l’air dans une zone donnée et envoie les données.”

Concepts clés :

- entité machine (drone) ;
- localisation (zone) ;
- action de mesure ;
- grandeur physique (température) ;
- données transportées par un canal.

### Étape 2 — Expression en USC‑96

On exprime ces concepts avec les symboles USC‑96 (en ignorant les extensions disciplinaires pour l’exemple) :

- `ENT-MACHINE` — machine (drone) ;
- `ENT-LOCATION` — lieu / position (zone) ;
- `ENT-GOAL` / `ENT-ACTION` — intention et action ;
- `OP-MEAS` — opération de mesure ;
- `ENT-DATA` — donnée ;
- `ENT-SIGNAL` — signal ;
- `INFO-CHANNEL` — canal d’information (dans un profil mixte utilisant déjà INFO-*).

Séquence conceptuelle possible :

1. `AX-ENT`, `ENT-MACHINE`  
2. `ENT-LOCATION`  
3. `ENT-GOAL`, `OP-MOVE`, `ENT-LOCATION`  
4. `ENT-ACTION`, `OP-MEAS`  
5. `ENT-DATA`, `ENT-SIGNAL`, `INFO-CHANNEL`

Les IDs exacts sont déterminés par `usc_96_table.md` (et compléments éventuels), par ex. :

- `AX-ENT` = 1  
- `ENT-MACHINE` = 87  
- `ENT-LOCATION` = 89  
- `ENT-GOAL` = 92  
- `ENT-ACTION` = 93  
- `OP-MEAS` = 34  
- `ENT-DATA` = 83  
- `ENT-SIGNAL` = 82  
- `INFO-CHANNEL` (si profil) = 227 (USC‑256 ; pour un profil strict 96, un symbole proxy peut être utilisé).

Séquence d’IDs (exemple, profil mixte) :

```text
[1, 87, 89, 92, 34, 89, 93, 34, 83, 82, 227]
```

### Étape 3 — Encodage binaire pour LoRa / HF

On applique l’encodeur USC‑96 (cf. Annexe G) sur les IDs qui appartiennent à USC‑96.  
Pour les symboles hors plage (par ex. 227), deux approches sont possibles :

- utiliser un profil élargi (USC‑256) pour le lien considéré ;
- mapper `INFO-CHANNEL` sur un symbole équivalent ou proxy dans USC‑96.

Dans le cas USC‑96 pur, on conserve une séquence comme :

```text
[1, 87, 89, 92, 34, 89, 93, 34, 83, 82]
```

Chaque ID (0–95) est encodé sur 7 bits, puis dans un octet `0XXXXXXX`.  
On insère ces octets dans une trame de transport (voir Annexe G pour un exemple de trame avec en‑tête + CRC).

Sur LoRa ou HF, la couche radio transporte cette trame comme charge utile binaire.

### Étape 4 — Décodage côté réception

Au décodage :

1. Le récepteur lit la trame, valide l’en‑tête et le checksum.  
2. Il extrait le payload binaire (suite d’octets USC‑96).  
3. Il reconstruit la liste d’IDs via le décodeur (mask 0x7F sur chaque octet).  
4. Il remappe chaque ID sur son symbole canonique à l’aide de la table USC‑96.

On retrouve alors la séquence symbolique :

```text
AX-ENT, ENT-MACHINE,
ENT-LOCATION,
ENT-GOAL, OP-MOVE, ENT-LOCATION,
ENT-ACTION, OP-MEAS,
ENT-DATA, ENT-SIGNAL
```

5. Une couche supérieure (MML, application) peut reconstruire un graphe conceptuel :
   - nœud `Drone` (ENT-MACHINE) ;
   - nœud `Zone` (ENT-LOCATION) ;
   - relation “se déplacer vers” (OP-MOVE) ;
   - action “mesurer” (OP-MEAS) ;
   - sortie “donnée transmise” (ENT-DATA + ENT-SIGNAL).

Ce chemin “concept → USC → binaire → décodage” illustre comment USC‑96 peut être utilisé de bout en bout dans un système réel (drone, LoRa/HF, station sol) tout en restant compact, déterministe et interprétable.



