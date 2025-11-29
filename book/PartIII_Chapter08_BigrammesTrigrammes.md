PARTIE III — STRUCTURES INTERNES DU USC  
Chapitre 8 — Bi‑grammes et Tri‑grammes conceptuels
===================================================

8.1 Syntaxe compressée
----------------------

Les **bi‑grammes** et **tri‑grammes conceptuels** sont des combinaisons récurrentes de 2 ou 3 symboles USC, utilisées comme **motifs de syntaxe compressée**.

- Un **bi‑gramme** USC est une paire de symboles \((S_1, S_2)\) présentant une forte cohérence sémantique et une fréquence élevée d’occurrence conjointe.
- Un **tri‑gramme** USC est un triplet \((S_1, S_2, S_3)\) jouant un rôle de motif structurel (par ex. “sujet‑relation‑objet” simplifié).

Contrairement aux n‑grammes classiques en langage naturel :

- ces combinaisons ne capturent pas de **co‑occurrences de mots**, mais de **structures conceptuelles** ;
- les symboles USC sont déjà dépourvus de polysémie, ce qui réduit l’ambiguïté des motifs.

Exemples de bi‑grammes typiques :

- `(AX-ENT, ENT-AGENT)` : déclaration d’un agent ;
- `(REL-SUB, ENT-HUMAN)` : humain comme sous‑type dans une hiérarchie ;
- `(OP-MEAS, SCI-MASS)` : opération de mesure d’une masse ;
- `(ENT-DATA, INFO-CHANNEL)` : donnée associée à un canal d’information.

Exemples de tri‑grammes typiques :

- `(ENT-AGENT, ENT-ACTION, ENT-OBJECT)` : “un agent effectue une action sur un objet” ;
- `(ENT-MACHINE, OP-MEAS, SCI-ENERGY)` : “une machine mesure une énergie” ;
- `(PHYS-FIELD, REL-IN, MAP-AREA)` : “un champ défini dans une région donnée”.

La norme USC n’impose pas un inventaire fixe de bi‑/tri‑grammes, mais elle **autorise** leur usage comme :

- unités de compression (regroupement) ;
- motifs structurants dans des grammaires supérieures (MML, EBNF USC).

8.2 Reconstruction conceptuelle par IA
--------------------------------------

Une IA utilisant USC ne se contente pas de lire des symboles isolés ; elle exploite les **motifs n‑grammes** pour :

- accélérer la compréhension ;
- prédire les structures manquantes ;
- reconstruire des représentations plus riches à partir de trames compactes.

Quand un bi‑gramme ou tri‑gramme est reconnu comme motif :

- l’IA peut lui associer une **structure interne plus détaillée** (par ex. un graphe MML, un schéma RDF, une formule logique) ;
- inversement, lors de la compression, l’IA PEUT réduire une structure détaillée à un n‑gramme USC standardisé.

Exemple :

- Trame USC brute : `(ENT-HUMAN, ENT-ACTION, OP-MEAS, SCI-FORCE, ENT-OBJECT)` ;
- L’IA apprend que `(ENT-ACTION, OP-MEAS, SCI-FORCE)` est un tri‑gramme standard “mesure de force” ;
- Elle peut reconstruire une représentation MML équivalente à :
  - un nœud “Measure” reliant :
    - un agent humain,
    - un objet,
    - une grandeur de type “force”,
    - un résultat numérique associé.

Ainsi, les bi‑/tri‑grammes servent de **pont** entre :

- la séquence symbolique compacte ;
- et une structure interne plus riche, éventuellement spécifique à chaque IA.

8.3 Densité 10:1 vs langage naturel
-----------------------------------

L’une des motivations des bi‑/tri‑grammes USC est d’atteindre des **rapports de compression sémantique** très élevés par rapport au langage naturel.

Scénario typique :

- description technique en texte : 100 à 200 mots ;
- équivalent en concepts USC :
  - ~20 à 30 symboles individuels ;
  - dont une grande partie peut être organisée en n‑grammes récurrents ;
- on obtient une densité effective de l’ordre de 10:1 (ou plus) pour des contenus structurés.

Concrètement :

- un message USC comportant 10 tri‑grammes (30 symboles) peut résumer :
  - un protocole expérimental,
  - un plan de mission,
  - un diagnostic médical de haut niveau,
  qui nécessiteraient plusieurs phrases en langue naturelle.

Cette compression est rendue possible par :

- la canonisation sémantique des symboles ;
- l’absence de polysémie ;
- la réutilisation de motifs n‑grammes standardisés.

Les bi‑/tri‑grammes ne sont pas obligatoires, mais tout système qui vise des **transmissions à très bas débit** SHOULD :

- identifier les motifs n‑grammes fréquents dans ses messages ;
- les utiliser comme unités de conception pour ses protocoles.

8.4 Exemples de trames USC → MML
--------------------------------

Cette section illustre comment des trames USC compactes, basées sur des bi‑/tri‑grammes, peuvent être **relevées** en structures MML plus détaillées.

Exemple 1 — Hypothèse scientifique simple
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Intention (informelle) :  
> “Si la température augmente alors la pression augmente, dans un système donné.”

Trame USC (séquence simplifiée) :

- `(AX-ENT, ENT-SYSTEM)`  
- `(PHYS-TEMP, REL-IN, ENT-SYSTEM)`  
- `(PHYS-PRESS, REL-IN, ENT-SYSTEM)`  
- `(CTRL-IF, PHYS-TEMP, REL-GT)`  
- `(CTRL-THEN, PHYS-PRESS, REL-GT)` *(CTRL-THEN pouvant être modélisé via `CTRL-IF` + structure)*

Cette trame peut être vue comme :

- deux tri‑grammes principaux :
  - “température dans système”, “pression dans système” ;
- un motif conditionnel “si grandeur A augmente alors grandeur B augmente”.

Reconstruction MML possible :

- un bloc `IF` contenant :
  - condition : `increase(TEMP(system))` ;
  - conséquence : `increase(PRESS(system))`.

Exemple 2 — Mission drone minimale
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Intention :  
> “Le drone D1 mesure la densité d’air sur une route donnée et envoie les données.”

Trame USC (symboles) :

1. `ENT-MACHINE` + `DISC-SPACE` (drone aérien)  
2. `ENT-LOCATION` + `MAP-ROUTE`  
3. `ENT-ACTION` + `OP-MEAS` + `PHYS-DENS`  
4. `ENT-DATA` + `ENT-SIGNAL` + `INFO-CHANNEL`

On peut y reconnaître :

- un bi‑gramme `(ENT-MACHINE, DISC-SPACE)` = “plateforme spatiale / mobile” ;
- un tri‑gramme `(ENT-ACTION, OP-MEAS, PHYS-DENS)` = “mesure de densité” ;
- un tri‑gramme `(ENT-DATA, ENT-SIGNAL, INFO-CHANNEL)` = “donnée transmise via canal”.

Reconstruction MML (schéma) :

- nœud `Mission` :
  - `agent` : machine (drone) dans contexte spatial ;
  - `target-route` : entité route avec coordonnées associées ;
  - `action` : mesurer densité de l’air ;
  - `output` : données envoyées via canal spécifique.

Exemple 3 — Donnée médicale structurée
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Intention :  
> “Un patient humain reçoit un médicament M à une dose D pour traiter une maladie X.”

Trame USC (symboles) :

1. `ENT-HUMAN` + `DISC-MED`  
2. `MED-DISEASE`  
3. `MED-DRUG` + `MED-DOSE`  
4. `ENT-ACTION` + `OP-MEAS` (éventuelle mesure d’effet)  
5. `MED-TREAT` + `MED-OUTCOME`

Motifs n‑grammes :

- `(ENT-HUMAN, DISC-MED)` : sujet médical ;  
- `(MED-DRUG, MED-DOSE)` : administration médicamenteuse ;  
- `(MED-TREAT, MED-OUTCOME)` : traitement et issue clinique.

Reconstruction MML :

- un graphe médical structuré reliant :
  - patient,
  - pathologie,
  - médication + dose,
  - éventuelles mesures d’efficacité,
  - résultat (issue).

Ces exemples montrent comment les bi‑/tri‑grammes conceptuels :

- augmentent la **densité sémantique** des trames USC ;
- facilitent la **traduction bidirectionnelle** entre :
  - messages compacts USC,
  - structures riches (MML, graphes de connaissances, ontologies).

