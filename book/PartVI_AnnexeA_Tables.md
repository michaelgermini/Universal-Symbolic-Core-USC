PARTIE VI — ANNEXES TECHNIQUES  
Annexe A — Tables canoniques USC‑96 / USC‑128 / USC‑256
=======================================================

> Cette annexe est normative pour l’inventaire des symboles.  
> Les tables détaillées sont fournies dans `usc_96_table.md`, `usc_128_table.md`, `usc_256_table.md`.

A.1 Table canonique USC‑96
--------------------------

USC‑96 définit le **noyau ultra‑compact** de l’USC.  
Les symboles sont numérotés de **0 à 95**, chacun avec :

- un ID entier,
- un nom canonique (`SYMBOL`),
- une classe (`CLASS`),
- une définition courte (`GLOSS`).

Organisation principale (rappel) :

- **0–15 : Axiomes ontologiques (`AX-*`)**  
  - `AX-ENT`, `AX-STA`, `AX-EVT`, `AX-VAR`, `AX-TIME`, `AX-SPACE`, `AX-MAT`, `AX-ENE`, `AX-INF`, `AX-ID`, `AX-PROB`, `AX-CAUS`, `AX-PART`, `AX-WHOLE`, `AX-SYS`…
- **16–31 : Relations générales (`REL-*`)**  
  - `REL-SUB`, `REL-PART-OF`, `REL-HAS`, `REL-SIM`, `REL-OPP`, `REL-CAUSE`, `REL-EFFECT`, `REL-EQ`, `REL-GT`, `REL-LT`, `REL-BEFORE`, `REL-AFTER`, `REL-IN`, `REL-OUT`, `REL-NEAR`, `REL-CONNECT`.
- **32–47 : Opérations (`OP-*`)**  
  - `OP-DEF`, `OP-REF`, `OP-MEAS`, `OP-COMP`, `OP-ADD`, `OP-SUB`, `OP-MUL`, `OP-DIV`, `OP-MOD`, `OP-MAX`, `OP-MIN`, `OP-AVG`, `OP-ENC`, `OP-DEC`, `OP-MOVE`, `OP-CONVERT`.
- **48–63 : Structures & contrôle (`STR-*`, `CTRL-*`)**  
  - `STR-SEQ`, `STR-SET`, `STR-LIST`, `STR-GRAPH`, `STR-NODE`, `STR-EDGE`, `STR-TREE`, `STR-MAP`,  
    `CTRL-IF`, `CTRL-ELSE`, `CTRL-AND`, `CTRL-OR`, `CTRL-NOT`, `CTRL-EXISTS`, `CTRL-FORALL`, `CTRL-LOOP`.
- **64–79 : Nombres & unités minimales (`NUM-*`, `UNIT-*`)**  
  - `NUM-0..NUM-9`, `NUM-SEP`, `NUM-SIGN`, `NUM-PCT`, `NUM-RANGE`, `UNIT-TIME`, `UNIT-LEN`.
- **80–95 : Entités génériques (`ENT-*`)**  
  - `ENT-AGENT`, `ENT-OBJECT`, `ENT-SIGNAL`, `ENT-DATA`, `ENT-SYSTEM`, `ENT-ORGANISM`, `ENT-HUMAN`, `ENT-MACHINE`, `ENT-ENV`, `ENT-LOCATION`, `ENT-RESOURCE`, `ENT-RISK`, `ENT-GOAL`, `ENT-ACTION`, `ENT-STATE`, `ENT-EVENT`.

L’**encodage** de USC‑96 est défini dans `usc_96_table.md` :

- 7 bits par symbole (ID 0–95), transmis comme un octet `0XXXXXXX` (MSB réservé).

A.2 Table étendue USC‑128
-------------------------

USC‑128 étend USC‑96 en ajoutant **32 symboles** (IDs 96–127) couvrant :

- mathématiques étendues (`MATH-*`) ;
- logique avancée (`LOG-*`) ;
- concepts scientifiques élémentaires (`SCI-*`, `UNIT-*`).

Organisation (voir `usc_128_table.md`) :

- **96–111 : Math étendues (`MATH-*`)**  
  - constantes (`MATH-PI`, `MATH-E`, `MATH-INF`) ;
  - analyse (`MATH-LIM`, `MATH-DERIV`, `MATH-INTEG`) ;
  - structures (`MATH-VECTOR`, `MATH-MATRIX`, `MATH-NORM`, `MATH-SET`, `MATH-FUNC`, `MATH-REL`) ;
  - probas/stat (`MATH-PROB`, `MATH-EXPECT`, `MATH-VAR`, `MATH-STD`).
- **112–119 : Logique avancée (`LOG-*`)**  
  - `LOG-IMPLIES`, `LOG-IFF`, `LOG-NEC`, `LOG-POSS`, `LOG-TRUE`, `LOG-FALSE`, `LOG-TAUTO`, `LOG-CONTRA`.
- **120–127 : Sciences élémentaires (`SCI-*`, `UNIT-*`)**  
  - `SCI-MASS`, `SCI-FORCE`, `SCI-ENERGY`, `SCI-POWER`, `SCI-FIELD`, `SCI-WAVE`, `UNIT-MASS`, `UNIT-ENERGY`.

Invariants :

- IDs 0–95 identiques à USC‑96 ;
- IDs 96–127 réservés à USC‑128 ;
- encodage sur 7 bits (0–127).

A.3 Table universelle étendue USC‑256
-------------------------------------

USC‑256 complète USC‑128 avec **128 symboles supplémentaires** (IDs 128–255), organisés par blocs disciplinaires (voir `usc_256_table.md`) :

- **128–143 : Physique (`PHYS-*`)**  
  - position, vitesse, accélération, quantité de mouvement, force, pression, température, densité, charge, potentiel, champ, flux, onde, particule, rayonnement, spin.
- **144–159 : Chimie (`CHEM-*`)**  
  - élément, atome, molécule, liaison, ion, pH, concentration, réaction, catalyseur, solvant, soluté, phase, enthalpie, entropie, équilibre, vitesse de réaction.
- **160–175 : Biologie / Médecine (`BIO-*`, `MED-*`)**  
  - cellule, tissu, organe, système, gène, protéine, ADN, ARN, maladie, symptôme, diagnostic, traitement, médicament, dose, facteur de risque, issue clinique.
- **176–191 : Espace / Cartographie (`SPACE-*`, `MAP-*`)**  
  - étoiles, planètes, lunes, astéroïdes, galaxies, nébuleuses, orbites, trajectoires, coordonnées (lat, lon, alt), aires, frontières, routes, points d’intérêt.
- **192–207 : Topologie / Graphes avancés (`GRAPH-*`, `TOPO-*`)**  
  - chemins, cycles, composantes connexes, centralité, flots, coupes, clusters, ouverts, fermés, frontières, connexité, trous, classes d’homotopie, variétés, espaces métriques.
- **208–223 : Math avancées (`MATH2-*`)**  
  - groupe, anneau, corps, espace vectoriel, base, valeurs propres, mesure, σ‑algèbre, espace topologique, catégorie, foncteur, transformation naturelle, limite catégorique, structure algébrique générale, ordre, treillis.
- **224–239 : Information / Calcul (`INFO-*`, `COMP-*`)**  
  - bit, octet, entropie de Shannon, canal, capacité, code, bruit, erreur, algorithme, machine, état de calcul, automate, complexité, aléatoire, programme, mémoire.
- **240–255 : Meta / Discipline / Réservé (`DISC-*`, `META-*`, `RSV-*`)**  
  - tags de domaine (`DISC-PHYS`, `DISC-CHEM`, `DISC-BIO`, `DISC-MED`, `DISC-SPACE`, `DISC-MATH`, `DISC-COMP`, `DISC-INFO`) ;
  - métadonnées (`META-VERSION`, `META-SOURCE`, `META-CONFID`, `META-TIMESTAMP`, `META-AUTHOR`) ;
  - IDs réservés (`RSV-FUTURE-1..3`).

Niveau binaire :

- IDs 0–255 utilisables ;
- encodage typique : 1 octet = 1 symbole (0–255), avec version/profil géré en en‑tête de protocole.

A.4 Relations internes entre symboles
-------------------------------------

Les tables USC ne sont pas de simples listes ; elles définissent un **réseau de relations internes** :

- `AX-*` fournissent les **types ontologiques** de base ;
- `ENT-*` instancient des entités rattachées à ces axes (par ex. `ENT-MACHINE` comme `AX-ENT` dans `AX-SPACE` et `AX-TIME`) ;
- `REL-*` relient :
  - entités à entités,
  - entités à états,
  - grandeurs à systèmes ;
- `OP-*` opèrent sur :
  - des entités (`OP-MOVE`),
  - des valeurs (`OP-ADD`, `OP-MEAS`),
  - des représentations (`OP-ENC`, `OP-DEC`, `OP-CONVERT`) ;
- `STR-*`, `GRAPH-*`, `TOPO-*` donnent la **forme** (séquences, graphes, espaces) ;
- `MATH-*`, `MATH2-*` fournissent les **structures mathématiques** sur lesquelles reposent les disciplines ;
- `SCI-*`, `PHYS-*`, `CHEM-*`, `BIO-*`, `MED-*` instancient des **concepts disciplinaires** ancrés dans les axiomes.

De façon informelle :

- USC‑96 capture la **structure ontologique et relationnelle** minimale ;
- USC‑128 ajoute les **structures mathématiques et physiques élémentaires** ;
- USC‑256 ajoute des **couches disciplinaires** spécialisées, qui restent compatibles ontologiquement avec le noyau.

A.5 Mappages partiels vers Unicode, RDF/OWL, JSON, MML
------------------------------------------------------

Pour s’intégrer dans l’écosystème existant, chaque symbole USC peut être relié à des représentations d’autres couches :

- **Unicode** :  
  - un bloc de **zone d’usage privé** (PUA) PEUT être réservé pour donner une graphie symbolique à chaque `SYMBOL` USC ;  
  - ceci sert surtout pour des interfaces humaines (visualisation, édition), pas pour le traitement machine.

- **RDF/OWL** :  
  - chaque `SYMBOL` USC SHOULD avoir un IRI unique (`usc:AX-TIME`, `usc:ENT-HUMAN`, etc.) ;  
  - ces IRIs peuvent être liés à des ontologies standard (ex. OWL Time, SNOMED, ChEBI) via :
    - `owl:equivalentClass`, `owl:equivalentProperty`,
    - ou des relations plus faibles (`rdfs:seeAlso`, `skos:exactMatch`).

- **JSON / XML** :  
  - les séquences USC peuvent être sérialisées en :
    - tableaux d’IDs (`"symbols": [1, 80, 16, ...]`) ;
    - ou objets enrichis (`{"id": 80, "symbol": "ENT-AGENT"}`) ;  
  - les structures USC+MML peuvent être représentées comme des arbres JSON/XML standards.

- **MML** :  
  - MML est la couche L1 de structure, USC la couche L0/L1 de contenu ;  
  - chaque nœud MML a pour feuilles des symboles USC (ou des nombres/valeurs associées à des `NUM-*`, `UNIT-*`) ;  
  - des schémas de mappage USC ↔ MML doivent être spécifiés pour chaque profil (voir Annexe B).

Ces mappages sont **partiels** par définition :  
USC vise à rester compact, conceptuel et non linguistique, là où Unicode, RDF/OWL, JSON, MML ont des objectifs plus larges.  
Cette annexe fixe seulement les points d’ancrage nécessaires pour que des ponts robustes puissent être construits entre ces mondes.

