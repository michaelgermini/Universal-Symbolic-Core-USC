PARTIE I — PRINCIPES FONDAMENTAUX DE L’USC  
Chapitre 2 — Théorie des symboles : la compression sémantique
==============================================================

2.1 Un symbole = une unité conceptuelle atomique
------------------------------------------------

Dans l’USC, un symbole est défini comme une **unité conceptuelle atomique**.  
Cela signifie qu’il représente le plus petit fragment de sens que la norme considère comme **indivisible** dans le cadre de la couche L0.

Un symbole USC :

- NE DOIT PAS se décomposer en sous‑symboles USC ayant un sens indépendant au même niveau ;
- DOIT pouvoir être combiné avec d’autres symboles pour former :
  - des entités composées,
  - des relations complexes,
  - des structures logiques ou topologiques.

Exemples :

- `AX-TIME` représente le concept de **temps** en tant qu’axe ontologique, non la phrase “le temps qui passe” ;
- `REL-CAUSE` représente la relation de **causalité** en général, non une formule linguistique particulière (“parce que”, “à cause de”, etc.) ;
- `OP-MEAS` représente l’opération de **mesure**, indépendamment de la façon dont une langue humaine décrirait cette action.

Cette atomicité est une **convention normative** : elle ne signifie pas que le concept ne peut pas, philosophiquement, être analysé davantage, mais que, pour les besoins de la couche USC, il est traité comme unité de base.

2.2 Densité sémantique : quantification
---------------------------------------

La **densité sémantique** d’un alphabet est le rapport entre :

- la quantité de **sens distincts** qu’il permet de représenter,
- et le nombre de **symboles ou tokens** nécessaires pour les exprimer.

L’USC vise une densité sémantique élevée :

- chaque symbole porte une part importante de signification stable ;
- les séquences de symboles peuvent atteindre des **rapports de compression** de l’ordre de 10:1 ou plus par rapport au langage naturel, pour des contenus techniques.

On peut envisager, de manière informelle, une mesure de densité :

- \( D = \frac{C}{N} \)
  - où \( C \) est une estimation de la quantité de contenu conceptuel,
  - et \( N \) le nombre de symboles USC nécessaires.

L’objectif de conception de l’USC est de **maximiser D**, sous contraintes :

- de lisibilité machine,
- de stabilité sémantique,
- de compatibilité disciplinaire.

2.3 Entropie conceptuelle minimisée
-----------------------------------

La notion d’**entropie conceptuelle** renvoie ici à la dispersion et à la redondance des significations dans l’alphabet :

- un alphabet avec beaucoup de synonymes, de polysémies et de redondances aura une entropie conceptuelle élevée ;
- un alphabet où chaque symbole est bien séparé, non redondant et non ambigu aura une entropie conceptuelle plus faible.

L’USC est conçu pour :

- **minimiser** le chevauchement des significations entre symboles ;
- **réduire** le nombre de symboles au strict nécessaire ;
- **stabiliser** les définitions canoniques dans le temps.

Concrètement, cela implique lors de la définition d’un nouveau symbole :

- de vérifier qu’aucun symbole existant ne couvre déjà ce sens de manière satisfaisante ;
- de s’assurer que l’introduction du symbole n’introduit pas de **synonymie conceptuelle** interne ;
- de documenter clairement son **champ d’application** (scope) et ses **limites**.

Cette recherche de faible entropie conceptuelle distingue l’USC :

- des vocabulaires humains évolutifs, riches en redondances ;
- des ontologies proliférantes sans contrôle central strict.

2.4 Représentation sans polysémie
---------------------------------

La **polysémie** (un même signe pour plusieurs sens) est une propriété native des langues naturelles.  
Dans l’USC, la polysémie est **explicitement interdite**.

Normativement :

- un symbole USC MUST correspondre à **un seul sens canonique** ;
- si plusieurs sens sont constatés dans les usages, la norme DOIT :
  - clarifier le sens canonique conservé ;
  - éventuellement introduire de nouveaux symboles distincts ;
  - déclarer les usages ambigus comme non conformes.

Pour limiter la dérive sémantique :

- les symboles sont organisés par **classes** (`AX-*`, `REL-*`, `OP-*`, `STR-*`, `ENT-*`, etc.) ;
- chaque classe a un **rôle bien défini** :
  - `AX-*` : axiomes ontologiques,
  - `REL-*` : types de relations,
  - `OP-*` : opérations / fonctions conceptuelles,
  - `STR-*` : structures de données / topologiques,
  - `ENT-*` : entités génériques.

Ainsi, un même terme humain (par ex. “temps”) ne peut pas se retrouver :

- à la fois comme `AX-*` et comme `ENT-*` avec le même champ de sens ;
- ou comme `REL-*` et `OP-*` pour décrire deux choses différentes.

2.5 Cohérence trans‑disciplinaire par canonisation symbolique
-------------------------------------------------------------

L’USC a pour ambition de rester **valable simultanément** dans plusieurs disciplines :

- physique, chimie, biologie, médecine ;
- informatique, théorie de l’information, mathématiques ;
- sciences de l’ingénieur, systèmes industriels, robotique.

Pour cela, il adopte une stratégie de **canonisation symbolique** :

- les symboles ne sont pas définis par rapport à une discipline spécifique,
- ils sont définis au niveau **ontologique minimal** (par ex. `AX-TIME`, `AX-SPACE`, `AX-ENT`, `REL-CAUSE`).

Les disciplines viennent ensuite :

- soit affiner ces concepts dans des couches supérieures (ontologies, modèles de domaine) ;
- soit utiliser les extensions disciplinaires de USC‑256 (par ex. `PHYS-TEMP`, `CHEM-REACTION`, `BIO-CELL`).

Conséquences :

- un message USC produit par une IA médicale reste partiellement compréhensible par une IA de physique, au moins au niveau des **axiomes de base** ;
- les symboles centraux (USC‑96) peuvent être partagés entre systèmes très différents, sans être redéfinis à chaque fois.

La cohérence trans‑disciplinaire est donc garantie :

- par la stabilité des symboles de base ;
- par la séparation claire entre noyau ontologique (USC‑96) et couches disciplinaires étendues (USC‑256).


