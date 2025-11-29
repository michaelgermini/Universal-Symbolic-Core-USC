PARTIE II — ARCHITECTURE USC‑96 / USC‑128 / USC‑256  
Chapitre 5 — USC‑128 : Le Core Recommandé
=========================================

5.1 Le juste milieu entre expressivité et compacité
---------------------------------------------------

USC‑128 est l’extension **recommandée** du noyau USC‑96.  
Il ajoute 32 symboles (IDs 96–127) sans modifier les 96 premiers, de façon à :

- augmenter fortement l’**expressivité** pour les IA générales et scientifiques ;
- conserver une **taille d’alphabet modeste** (128 symboles) facile à manipuler ;
- rester compatible avec des encodages simples sur 7 bits (0–127).

USC‑128 est particulièrement adapté à :

- des IA locales ou embarquées avec des capacités raisonnables ;
- des systèmes scientifiques ou d’ingénierie ;
- des scénarios où l’on veut exprimer :
  - des concepts mathématiques avancés (limite, dérivée, intégrale, vecteurs, matrices…) ;
  - des notions de logique modale (nécessité, possibilité) ;
  - des grandeurs physiques de base (masse, force, énergie, puissance, champ, onde).

En pratique :

- les systèmes critiques à bande passante très réduite PEUVENT rester en USC‑96 ;
- les systèmes nécessitant plus de finesse scientifique DEVRAIENT adopter USC‑128 ;
- les architectures globales multi‑domaines utiliseront plutôt USC‑256.

5.2 Ajout des champs
--------------------

USC‑128 introduit trois familles principales supplémentaires (voir `usc_128_table.md` et **Annexe A**) :

1. **Mathématiques étendues (`MATH-*`) — IDs 96–111**  
   - constantes : `MATH-PI`, `MATH-E`, `MATH-INF` ;  
   - analyse : `MATH-LIM`, `MATH-DERIV`, `MATH-INTEG` ;  
   - structures : `MATH-VECTOR`, `MATH-MATRIX`, `MATH-NORM`, `MATH-SET`, `MATH-FUNC`, `MATH-REL` ;  
   - probabilités et statistiques : `MATH-PROB`, `MATH-EXPECT`, `MATH-VAR`, `MATH-STD`.

2. **Logique avancée (`LOG-*`) — IDs 112–119**  
   - connecteurs et notions modales :  
     - `LOG-IMPLIES` (implication),  
     - `LOG-IFF` (équivalence logique),  
     - `LOG-NEC` (nécessité, □),  
     - `LOG-POSS` (possibilité, ◇) ;  
   - valeurs de vérité et propriétés :  
     - `LOG-TRUE`, `LOG-FALSE`,  
     - `LOG-TAUTO` (tautologie),  
     - `LOG-CONTRA` (contradiction).

3. **Concepts scientifiques élémentaires (`SCI-*`, `UNIT-*`) — IDs 120–127**  
   - grandeurs physiques :  
     - `SCI-MASS`, `SCI-FORCE`, `SCI-ENERGY`, `SCI-POWER`, `SCI-FIELD`, `SCI-WAVE` ;  
   - unités abstraites :  
     - `UNIT-MASS`, `UNIT-ENERGY`.

Ces ajouts permettent :

- d’exprimer des **modèles scientifiques simples** directement en USC ;
- de relier des phénomènes mesurés (masse, énergie, puissance) à des structures mathématiques (vecteurs, matrices, fonctions, distributions de probabilité).

5.3 Pourquoi 128 est le “sweet spot” pour IA locale
---------------------------------------------------

Pour de nombreuses IA déployées sur une machine unique ou un petit cluster, USC‑128 offre un **équilibre optimal** :

- **Taille gérable** :
  - une table de 128 symboles reste triviale à stocker et indexer ;
  - la recherche, le décodage et la manipulation restent en \(O(1)\) ou \(O(\log N)\) avec des structures simples.
- **Couverture conceptuelle** :
  - suffisamment riche pour couvrir la plupart des tâches d’ingénierie, de data science et de modélisation scientifique courante ;
  - sans entrer encore dans le détail de toutes les disciplines comme USC‑256.
- **Simplicité d’implémentation** :
  - valeurs d’ID dans \[0,127\] → directement encodables sur 7 bits ;
  - les formats existants fondés sur des octets restent faciles à adapter.

Une IA qui projette une partie de ses raisonnements en USC‑128 peut :

- représenter des **équations simples**, des dérivées, des intégrales ;
- modéliser des **incertitudes** (probabilités, espérance, variance) ;
- décrire des **systèmes physiques** de base (forces, champs, ondes) à un niveau compact mais exploitable.

5.4 Comparaison USC‑96 / USC‑128 / USC‑256
------------------------------------------

On peut résumer les trois niveaux ainsi :

- **USC‑96 — Survie / minimal**  
  - 96 symboles ;  
  - noyau ontologique, relationnel, opérationnel, numérique et d’entités génériques ;  
  - adapté aux scénarios de forte contrainte (radio bas débit, hardware minimal).
- **USC‑128 — Efficacité / généralité**  
  - 128 symboles ;  
  - ajoute math étendues, logique avancée, bases de physique ;  
  - adapté aux IA locales, scientifiques, systèmes d’ingénierie modernes.
- **USC‑256 — Universalité / disciplines avancées**  
  - 256 symboles ;  
  - ajoute des blocs disciplinaires complets (physique détaillée, chimie, bio/med, topo/graphes, info/théorie du calcul, meta) ;  
  - adapté aux IA globales, systèmes multi‑domaines complexes.

Toute architecture utilisant USC DOIT préciser :

- la **variante minimale** requise (96, 128 ou 256) ;
- les sous‑ensembles de symboles réellement employés dans chaque module.

5.5 Structures mémorielles adaptées
-----------------------------------

Les implémentations USC‑128 peuvent choisir diverses structures de données internes :

- **Table indexée par ID** (tableau) :  
  - index = ID (0–127),  
  - valeur = métadonnées (classe, gloss, liens ontologiques) ;  
  - accès direct, très efficace pour des systèmes embarqués.
- **Table de hachage par nom de symbole** :  
  - clé = chaîne (`"AX-ENT"`, `"MATH-PI"`, `"SCI-ENERGY"`),  
  - valeur = ID + métadonnées ;  
  - utile pour des outils de développement, de debug, d’édition.
- **Structures arborescentes / graphes** :  
  - pour représenter explicitement :
    - relations de spécialisation (USC‑96 → USC‑128 → USC‑256),
    - liens entre concepts mathématiques, physiques, logiques.

Recommandations :

- les systèmes embarqués SHOULD utiliser :
  - une table compacte indexée par ID,  
  - éventuellement un petit dictionnaire pour les noms symboliques.
- les frameworks IA SHOULD maintenir :
  - un graphe conceptuel interne reliant les symboles USC‑128 entre eux,  
  - afin de faciliter la navigation, l’explication et la visualisation.

5.6 Impact sur la cohérence d’un LLM
------------------------------------

Pour un LLM ou tout modèle génératif, USC‑128 peut jouer le rôle de **point d’ancrage symbolique** :

- une partie de la chaîne de raisonnement (chain‑of‑thought) peut être :
  - compressée en USC‑128,
  - stockée ou transmise indépendamment du texte naturel ;
- des étapes critiques (hypothèses, conclusions, conditions) peuvent être :
  - exprimées en symboles `AX-*`, `REL-*`, `OP-*`, `MATH-*`, `LOG-*`, `SCI-*` ;
  - ré‑importées dans d’autres modèles avec une interprétation cohérente.

Avantages pour la cohérence :

- réduction de la dépendance au texte, donc des ambiguïtés ;
- possibilité de comparer des raisonnements de modèles différents en espace USC‑128 ;
- auditabilité accrue des décisions (cf. Chapitre 3 et Partie V).

Un LLM utilisant USC‑128 SHOULD :

- documenter le mapping entre ses tokens internes et les symboles USC‑128 ;
- proposer un mode “trace USC” dans lequel les principales étapes du raisonnement sont exportées en USC.

5.7 Symboles spécialisés pour IA scientifique
---------------------------------------------

Les symboles ajoutés en USC‑128 sont pensés pour les **IA scientifiques** et d’ingénierie :

- **Probabilités et statistiques** :
  - `MATH-PROB` (distribution de probabilité),
  - `MATH-EXPECT` (espérance),
  - `MATH-VAR` (variance),
  - `MATH-STD` (écart‑type).  
  → permettent de représenter explicitement l’incertitude et la dispersion.

- **Structures mathématiques** :
  - `MATH-VECTOR`, `MATH-MATRIX`, `MATH-NORM`, `MATH-SET`, `MATH-FUNC`, `MATH-REL`.  
  → facilitent la description de systèmes linéaires, de transformations, d’espaces de variables.

- **Grandeurs physiques élémentaires** :
  - `SCI-MASS`, `SCI-FORCE`, `SCI-ENERGY`, `SCI-POWER`, `SCI-FIELD`, `SCI-WAVE`,  
  - avec les unités abstraites `UNIT-MASS`, `UNIT-ENERGY`.  
  → fournissent un vocabulaire commun pour des IA travaillant sur des capteurs, des simulations ou des modèles physiques.

Exemple : estimation de variance de masse
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Intention informelle :  
> “Un capteur humain estime la variance d’une mesure de masse.”

Séquence USC‑128 (symboles) :

1. `ENT-HUMAN` (86)  
2. `ENT-MACHINE` (87) + `REL-PART-OF` (17)  
3. `ENT-ACTION` (93)  
4. `OP-MEAS` (34)  
5. `SCI-MASS` (120)  
6. `MATH-VAR` (110)

Séquence d’IDs :  
`[86, 87, 17, 93, 34, 120, 110]`

Cette séquence peut être :

- sérialisée en binaire (IDs 0–127 sur 7 bits chacun) ;
- enveloppée dans un message MML / DNF ;
- interprétée par d’autres IA scientifiques utilisant aussi USC‑128.

Compatibilité
-------------

Toute implémentation USC‑128 MUST :

- interpréter correctement tous les symboles USC‑96 (0–95) ;
- considérer qu’un ID `≥ 96` indique l’usage de USC‑128 ;
- ne pas redéfinir la sémantique des IDs 0–95.

Un flux limité strictement à `0..95` reste **100 % compatible USC‑96**.  
Un flux utilisant `96..127` DOIT être explicitement déclaré comme USC‑128 ou supérieur dans les métadonnées de protocole (en‑tête, version, profil).


