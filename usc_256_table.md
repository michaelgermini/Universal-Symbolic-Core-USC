Universal Symbolic Core — Table étendue USC‑256 (v0.1)
======================================================

Portée
------

- **USC‑256** : corps universel étendu, pour IA globales, systèmes complexes, disciplines scientifiques.
- **Objectif** : compléter **USC‑128** avec **128 symboles supplémentaires** (`ID 128..255`) couvrant :
  - **Physique**
  - **Chimie**
  - **Biologie / Médecine**
  - **Espace / Cartographie**
  - **Topologie / Graphes avancés**
  - **Mathématiques avancées**
  - **Information / Calcul**
  - **Meta / Discipline / Versioning**

Invariants
----------

- **IDs 0–95** : USC‑96 (noyau).
- **IDs 96–127** : USC‑128 (math/logique/sciences élémentaires).
- **IDs 128–255** : USC‑256 (couches disciplinaires).
- **Sous‑ensemble stable** :
  - USC‑96 ⊂ USC‑128 ⊂ USC‑256.

Encodage
--------

- Niveau **symbolique** : ID entier dans \[0, 255\].
- Niveau **binaire** :
  - une implémentation simple peut utiliser **1 octet = 1 symbole** (0–255),
  - les champs de **version / mode** (96/128/256) sont gérés dans l’**en‑tête de trame**, pas dans l’ID lui‑même.

Table USC‑256 — nouveaux symboles (128–255)
-------------------------------------------

> Remarque : cette table est une **proposition v0.1** soigneusement structurée mais encore perfectible.

### Bloc 128–143 : Physique (PHYS‑*)

| ID  | SYMBOL        | CLASS | GLOSS                                               |
|-----|---------------|-------|-----------------------------------------------------|
| 128 | PHYS-POS      | PHYS  | position / vecteur de position                     |
| 129 | PHYS-VEL      | PHYS  | vitesse                                            |
| 130 | PHYS-ACC      | PHYS  | accélération                                      |
| 131 | PHYS-MOM      | PHYS  | quantité de mouvement                              |
| 132 | PHYS-FORCE    | PHYS  | force (vecteur)                                    |
| 133 | PHYS-PRESS    | PHYS  | pression                                           |
| 134 | PHYS-TEMP     | PHYS  | température                                       |
| 135 | PHYS-DENS     | PHYS  | densité                                           |
| 136 | PHYS-CHARGE   | PHYS  | charge électrique                                 |
| 137 | PHYS-POT      | PHYS  | potentiel (ex. électrique, gravitationnel)        |
| 138 | PHYS-FIELD    | PHYS  | champ physique                                   |
| 139 | PHYS-FLUX     | PHYS  | flux (à travers une surface)                      |
| 140 | PHYS-WAVE     | PHYS  | onde (physique)                                   |
| 141 | PHYS-PARTICLE | PHYS  | particule                                        |
| 142 | PHYS-RAD      | PHYS  | rayonnement                                      |
| 143 | PHYS-SPIN     | PHYS  | spin / moment intrinsèque                         |

### Bloc 144–159 : Chimie (CHEM‑*)

| ID  | SYMBOL        | CLASS | GLOSS                                               |
|-----|---------------|-------|-----------------------------------------------------|
| 144 | CHEM-ELEM     | CHEM  | élément chimique (abstrait)                        |
| 145 | CHEM-ATOM     | CHEM  | atome                                              |
| 146 | CHEM-MOL      | CHEM  | molécule                                           |
| 147 | CHEM-BOND     | CHEM  | liaison chimique                                  |
| 148 | CHEM-ION      | CHEM  | ion                                               |
| 149 | CHEM-PH       | CHEM  | pH                                                 |
| 150 | CHEM-CONC     | CHEM  | concentration                                     |
| 151 | CHEM-REACTION | CHEM  | réaction chimique                                |
| 152 | CHEM-CATALYST | CHEM  | catalyseur                                        |
| 153 | CHEM-SOLVENT  | CHEM  | solvant                                           |
| 154 | CHEM-SOLUTE   | CHEM  | soluté                                            |
| 155 | CHEM-PHASE    | CHEM  | phase (solide, liquide, gaz, plasma)             |
| 156 | CHEM-ENTHALPY | CHEM  | enthalpie                                         |
| 157 | CHEM-ENTROPY  | CHEM  | entropie thermodynamique                         |
| 158 | CHEM-EQUIL    | CHEM  | équilibre chimique                               |
| 159 | CHEM-RATE     | CHEM  | vitesse de réaction                              |

### Bloc 160–175 : Biologie / Médecine (BIO‑*, MED‑*)

| ID  | SYMBOL        | CLASS | GLOSS                                               |
|-----|---------------|-------|-----------------------------------------------------|
| 160 | BIO-CELL      | BIO   | cellule                                            |
| 161 | BIO-TISSUE    | BIO   | tissu biologique                                  |
| 162 | BIO-ORGAN     | BIO   | organe                                            |
| 163 | BIO-SYSTEM    | BIO   | système biologique (ex. respiratoire)            |
| 164 | BIO-GENE      | BIO   | gène                                              |
| 165 | BIO-PROTEIN   | BIO   | protéine                                         |
| 166 | BIO-DNA       | BIO   | ADN                                               |
| 167 | BIO-RNA       | BIO   | ARN                                               |
| 168 | MED-DISEASE   | MED   | maladie / pathologie                              |
| 169 | MED-SYMPTOM   | MED   | symptôme                                          |
| 170 | MED-DIAG      | MED   | diagnostic                                        |
| 171 | MED-TREAT     | MED   | traitement / thérapie                             |
| 172 | MED-DRUG      | MED   | médicament                                        |
| 173 | MED-DOSE      | MED   | dose                                              |
| 174 | MED-RISK      | MED   | facteur de risque                                 |
| 175 | MED-OUTCOME   | MED   | issue / résultat clinique                         |

### Bloc 176–191 : Espace / Cartographie (SPACE‑*, MAP‑*)

| ID  | SYMBOL        | CLASS | GLOSS                                               |
|-----|---------------|-------|-----------------------------------------------------|
| 176 | SPACE-STAR    | SPACE | étoile                                             |
| 177 | SPACE-PLANET  | SPACE | planète                                            |
| 178 | SPACE-MOON    | SPACE | lune / satellite naturel                           |
| 179 | SPACE-AST     | SPACE | astéroïde                                          |
| 180 | SPACE-GALAXY  | SPACE | galaxie                                            |
| 181 | SPACE-NEBULA  | SPACE | nébuleuse                                         |
| 182 | SPACE-ORBIT   | SPACE | orbite                                             |
| 183 | SPACE-TRAJ    | SPACE | trajectoire                                       |
| 184 | MAP-LAT       | MAP   | latitude                                          |
| 185 | MAP-LON       | MAP   | longitude                                         |
| 186 | MAP-ALT       | MAP   | altitude / élévation                              |
| 187 | MAP-COORD     | MAP   | coordonnée spatiale (vecteur position)           |
| 188 | MAP-AREA      | MAP   | aire / région                                     |
| 189 | MAP-BOUND     | MAP   | frontière / limite                                |
| 190 | MAP-ROUTE     | MAP   | route / chemin                                   |
| 191 | MAP-POI       | MAP   | point d’intérêt                                   |

### Bloc 192–207 : Topologie / Graphes avancés (TOPO‑*, GRAPH‑*)

| ID  | SYMBOL         | CLASS | GLOSS                                              |
|-----|----------------|-------|----------------------------------------------------|
| 192 | GRAPH-PATH     | GRAPH | chemin dans un graphe                             |
| 193 | GRAPH-CYCLE    | GRAPH | cycle                                             |
| 194 | GRAPH-DEGREE   | GRAPH | degré d’un nœud                                  |
| 195 | GRAPH-COMP     | GRAPH | composante connexe                               |
| 196 | GRAPH-CENT     | GRAPH | centralité                                       |
| 197 | GRAPH-FLOW     | GRAPH | flot / flux dans un réseau                       |
| 198 | GRAPH-CUT      | GRAPH | coupe / séparation                               |
| 199 | GRAPH-CLUSTER  | GRAPH | cluster / communauté                             |
| 200 | TOPO-OPEN      | TOPO  | ensemble ouvert                                  |
| 201 | TOPO-CLOSED    | TOPO  | ensemble fermé                                   |
| 202 | TOPO-BOUNDARY  | TOPO  | frontière topologique                            |
| 203 | TOPO-CONNECTED | TOPO  | espace connexe                                   |
| 204 | TOPO-HOLE      | TOPO  | trou / lacune topologique                        |
| 205 | TOPO-HOMOTOPY  | TOPO  | classe d’homotopie                               |
| 206 | TOPO-MANIFOLD  | TOPO  | variété                                         |
| 207 | TOPO-METRIC    | TOPO  | espace métrique                                  |

### Bloc 208–223 : Math avancées (MATH2‑*)

| ID  | SYMBOL        | CLASS  | GLOSS                                             |
|-----|---------------|--------|---------------------------------------------------|
| 208 | MATH2-GROUP   | MATH2  | groupe (algèbre)                                 |
| 209 | MATH2-RING    | MATH2  | anneau                                           |
| 210 | MATH2-FIELD   | MATH2  | corps (field)                                    |
| 211 | MATH2-VSPACE  | MATH2  | espace vectoriel                                 |
| 212 | MATH2-BASIS   | MATH2  | base d’un espace vectoriel                       |
| 213 | MATH2-EIGEN   | MATH2  | valeur / vecteur propre                          |
| 214 | MATH2-MEASURE | MATH2  | mesure (théorie de la mesure)                    |
| 215 | MATH2-SIGMA   | MATH2  | σ‑algèbre                                        |
| 216 | MATH2-TOPO    | MATH2  | espace topologique (objet mathématique)          |
| 217 | MATH2-CAT     | MATH2  | catégorie                                        |
| 218 | MATH2-FUNCTOR | MATH2  | foncteur                                         |
| 219 | MATH2-NAT     | MATH2  | transformation naturelle                         |
| 220 | MATH2-LIMIT   | MATH2  | limite catégorique / colimite                    |
| 221 | MATH2-ALG     | MATH2  | structure algébrique générale                    |
| 222 | MATH2-ORDER   | MATH2  | ordre partiel / total                            |
| 223 | MATH2-LATTICE | MATH2  | treillis                                         |

### Bloc 224–239 : Information / Calcul (INFO‑*, COMP‑*)

| ID  | SYMBOL         | CLASS | GLOSS                                             |
|-----|----------------|-------|---------------------------------------------------|
| 224 | INFO-BIT       | INFO  | bit d’information                                |
| 225 | INFO-BYTE      | INFO  | octet                                            |
| 226 | INFO-ENTROPY   | INFO  | entropie de Shannon                              |
| 227 | INFO-CHANNEL   | INFO  | canal de communication                           |
| 228 | INFO-CAPACITY  | INFO  | capacité de canal                                |
| 229 | INFO-CODE      | INFO  | code / schéma de codage                          |
| 230 | INFO-NOISE     | INFO  | bruit                                            |
| 231 | INFO-ERROR     | INFO  | erreur de transmission                           |
| 232 | COMP-ALGO      | COMP  | algorithme                                       |
| 233 | COMP-MACHINE   | COMP  | machine (de calcul, abstraite ou concrète)       |
| 234 | COMP-STATE     | COMP  | état de calcul                                   |
| 235 | COMP-AUTOMATON | COMP  | automate                                         |
| 236 | COMP-COMPLEX   | COMP  | complexité algorithmique                         |
| 237 | COMP-RANDOM    | COMP  | aléatoire / source de hasard                     |
| 238 | COMP-PROG      | COMP  | programme                                        |
| 239 | COMP-MEM       | COMP  | mémoire                                          |

### Bloc 240–255 : Meta / Discipline / Versioning (META‑*, DISC‑*, RSV‑*)

| ID  | SYMBOL        | CLASS | GLOSS                                              |
|-----|---------------|-------|----------------------------------------------------|
| 240 | DISC-PHYS     | DISC  | tag de domaine : physique                          |
| 241 | DISC-CHEM     | DISC  | tag de domaine : chimie                            |
| 242 | DISC-BIO      | DISC  | tag de domaine : biologie                          |
| 243 | DISC-MED      | DISC  | tag de domaine : médecine                          |
| 244 | DISC-SPACE    | DISC  | tag de domaine : espace / astronomie               |
| 245 | DISC-MATH     | DISC  | tag de domaine : mathématiques                     |
| 246 | DISC-COMP     | DISC  | tag de domaine : informatique / calcul             |
| 247 | DISC-INFO     | DISC  | tag de domaine : théorie de l’information          |
| 248 | META-VERSION  | META  | version du schéma / protocole                      |
| 249 | META-SOURCE   | META  | source / provenance (métadonnée)                   |
| 250 | META-CONFID   | META  | confiance / certitude de l’information             |
| 251 | META-TIMESTAMP| META  | horodatage / temps d’enregistrement                |
| 252 | META-AUTHOR   | META  | auteur / émetteur                                  |
| 253 | RSV-FUTURE-1  | RSV   | réservé pour future extension 1                    |
| 254 | RSV-FUTURE-2  | RSV   | réservé pour future extension 2                    |
| 255 | RSV-FUTURE-3  | RSV   | réservé pour future extension 3                    |

Exemple de message USC‑256
--------------------------

Intention (informelle) :  
> “Un satellite mesure la température et la pression à une position donnée et envoie les données.”

Séquence conceptuelle :

1. `ENT-MACHINE` (87) + `DISC-SPACE` (244) → machine spatiale (satellite)
2. `ENT-ACTION` (93) + `OP-MEAS` (34)
3. `PHYS-TEMP` (134), `PHYS-PRESS` (133)
4. `MAP-COORD` (187) + `AX-SPACE` (6)
5. `ENT-DATA` (83) + `ENT-SIGNAL` (82) + `INFO-CHANNEL` (227)

Séquence d’IDs (exemple) :

`[87, 244, 93, 34, 134, 133, 187, 6, 83, 82, 227]`

Interop & discipline
--------------------

- Chaque **DISC‑*** sert de **tag de contexte disciplinaire** :
  - permet à une IA de filtrer / organiser les symboles par domaine,
  - permet à des systèmes limités (par ex. uniquement médicaux) de ne charger qu’un sous‑ensemble.
- Les symboles PHYS‑*, CHEM‑*, BIO‑*, etc. peuvent être mappés :
  - à des **ontologies RDF/OWL** standard (ex. FMA, SNOMED, ChEBI),
  - à des **vocabulaires disciplinaires** existants, sans changer l’ID USC.

Résumé des couches
------------------

- **USC‑96** : noyau ontologique / relationnel / opérationnel minimal.
- **USC‑128** : ajoute math/logique/sciences de base.
- **USC‑256** : ajoute couches disciplinaires structurées pour physique, chimie, bio/med, espace, topo/graphes, math avancées, info/calcul et métadonnées.


