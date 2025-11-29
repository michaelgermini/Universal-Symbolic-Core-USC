PARTIE VI — ANNEXES TECHNIQUES  
Annexe D — Exemples concrets d’encodage USC
===========================================

> Cette annexe illustre, par cas concrets, l’encodage de contenus en USC.

Hypothèse scientifique
----------------------

Intention (langage naturel) :  
> “Si la température d’un gaz augmente à volume constant, alors sa pression augmente.”

Profil : USC‑256 (physique + relations)  

Esquisse USC (symboles) :

- `ENT-SYSTEM` (gaz considéré comme système)  
- `PHYS-TEMP` + `REL-IN` + `ENT-SYSTEM`  
- `PHYS-PRESS` + `REL-IN` + `ENT-SYSTEM`  
- `CTRL-IF` + motif “augmentation température”  
- implicite : `CTRL-THEN` + motif “augmentation pression”

Séquence possible (simplifiée, IDs indicatifs) :

```text
ENT-SYSTEM, PHYS-TEMP, REL-IN, ENT-SYSTEM,
PHYS-PRESS, REL-IN, ENT-SYSTEM,
CTRL-IF, PHYS-TEMP, REL-GT,
PHYS-PRESS, REL-GT
```

Une représentation MML correspondante pourra :

- faire apparaître explicitement la structure conditionnelle (IF/THEN) ;
- lier les grandeurs (`PHYS-TEMP`, `PHYS-PRESS`) à un même système (`ENT-SYSTEM`).

Mission drone
-------------

Intention :  
> “Le drone D1 doit survoler une zone Z, mesurer la densité de l’air et renvoyer les données.”

Profil : USC‑256 (espace, physique, info)  

Séquence USC conceptuelle :

1. `ENT-MACHINE` + `DISC-SPACE` (drone aérien)  
2. `ENT-LOCATION` + `MAP-AREA` (zone Z)  
3. `ENT-GOAL` : survol (`OP-MOVE` vers `MAP-AREA`)  
4. `ENT-ACTION` + `OP-MEAS` + `PHYS-DENS`  
5. `ENT-DATA` + `ENT-SIGNAL` + `INFO-CHANNEL`

En forme séquentielle (symboles) :

```text
ENT-MACHINE, DISC-SPACE,
ENT-LOCATION, MAP-AREA,
ENT-GOAL, OP-MOVE, MAP-AREA,
ENT-ACTION, OP-MEAS, PHYS-DENS,
ENT-DATA, ENT-SIGNAL, INFO-CHANNEL
```

Selon les contraintes radio (LoRa, HF), cette séquence pourra être :

- compressée davantage (bi‑/tri‑grammes) ;
- répartie sur plusieurs trames (mission, exécution, rapport).

Données médicales
-----------------

Intention :  
> “Un patient humain atteint de maladie X reçoit un médicament M à la dose D ; l’état est surveillé.”

Profil : USC‑256 (bio/med)  

Séquence USC conceptuelle :

1. `ENT-HUMAN` + `DISC-MED`  
2. `MED-DISEASE` (X)  
3. `MED-DRUG` + `MED-DOSE` (M, D)  
4. `ENT-ACTION` + `MED-TREAT`  
5. `ENT-STATE` + `MED-OUTCOME` (suivi, à remplir plus tard)

Séquence (symboles génériques) :

```text
ENT-HUMAN, DISC-MED,
MED-DISEASE,
MED-DRUG, MED-DOSE,
ENT-ACTION, MED-TREAT,
ENT-STATE, MED-OUTCOME
```

Cette représentation USC peut être associée :

- à des identifiants anonymisés de patient / traitement ;
+- à des mesures numériques (NUM-*, UNIT-*) pour les doses, constantes vitales, etc.

Logique mathématique
--------------------

Intention :  
> “Pour tout réel x, si x > 0 alors x² > 0.”

Profil : USC‑128 (math + logique)  

Éléments USC :

- `MATH-SET` (ensemble des réels R) ;
- `MATH-FUNC` (fonction x ↦ x²) ;
- `CTRL-FORALL` (quantificateur universel) ;
- `REL-GT` (>) ;
- `LOG-IMPLIES` (⇒).  

Séquence conceptuelle (schématique) :

```text
CTRL-FORALL, ENT-VAR, MATH-SET,
REL-IN, ENT-VAR, MATH-SET,
CTRL-IF, ENT-VAR, REL-GT, NUM-0,
LOG-IMPLIES,
MATH-FUNC, ENT-VAR, REL-GT, NUM-0
```

où `ENT-VAR` représente une entité variable typée (x), et `NUM-0` la constante zéro.  
Une structure MML associée rendra explicite :

- le domaine de quantification (R) ;
- la condition (x > 0) ;
- la conclusion (x² > 0).

Ces exemples montrent comment des énoncés très différents (physique, missions, médecine, logique) peuvent être **unifiés** dans un même style d’encodage USC structuré.

