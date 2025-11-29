PARTIE III — STRUCTURES INTERNES DU USC  
Chapitre 7 — Classes symboliques
================================

7.1 Symboles primitifs (AX‑*, ENT‑* de base)
-------------------------------------------

Les **symboles primitifs** constituent la base ontologique de l’USC.  
Ils sont principalement répartis entre les classes :

- `AX-*` : axiomes ontologiques ;
- `ENT-*` : entités génériques.

Les axiomes (`AX-*`) définissent les **types de réalité** minimaux pris en charge par l’USC :

- `AX-ENT` : entité, “ce qui est” ;
- `AX-STA` : état d’une entité ;
- `AX-EVT` : événement (changement d’état) ;
- `AX-VAR` : variable / paramètre ;
- `AX-TIME`, `AX-SPACE` : dimensions fondamentales ;
- `AX-MAT`, `AX-ENE` : matière et énergie ;
- `AX-INF` : information ;
- `AX-ID` : identité ;
- `AX-PROB` : probabilité ;
- `AX-CAUS` : causalité ;
- `AX-PART`, `AX-WHOLE`, `AX-SYS` : partie, tout, système.

Les entités (`ENT-*`) représentent des **instances conceptuelles génériques** :

- `ENT-AGENT`, `ENT-OBJECT`, `ENT-SYSTEM`, `ENT-ENV`, `ENT-RESOURCE`, etc. ;
- certaines sont plus spécialisées, ex. `ENT-HUMAN`, `ENT-MACHINE`, `ENT-ORGANISM`.

Rôle des symboles primitifs :

- servir de **points d’ancrage** pour tous les autres symboles (REL, OP, STR, etc.) ;
- permettre à une IA de construire des graphes de connaissance où :
  - chaque nœud est une entité (`ENT-*`) ;
  - chaque nœud est typé et situé dans un cadre ontologique (`AX-*`).

Une implémentation USC SHOULD traiter les symboles `AX-*` et `ENT-*` comme les **briques les plus stables**, rarement modifiées d’une version à l’autre.

7.2 Symboles relationnels (REL‑*)
---------------------------------

Les symboles `REL-*` décrivent les **liens** entre entités, états, événements ou autres symboles USC.

Exemples (USC‑96) :

- hiérarchie et typage :
  - `REL-SUB` : “est un type de” (is‑a) ;
  - `REL-PART-OF` : “fait partie de” ;
- possession et attributs :
  - `REL-HAS` : “a / possède” ;
  - `REL-SIM` : “est similaire à” ;
  - `REL-OPP` : “est opposé à” ;
- ordre et structure :
  - `REL-BEFORE`, `REL-AFTER` : ordre temporel ;
  - `REL-IN`, `REL-OUT`, `REL-NEAR`, `REL-CONNECT` : inclusion / proximité / connexion.

Rôle :

- structurer des **graphes de connaissance** ;
- exprimer des taxonomies, des partonomies, des réseaux causaux ;
- fournir la base pour des raisonnements de type :
  - héritage de propriétés (`REL-SUB`) ;
  - agrégation / composition (`REL-PART-OF`) ;
  - contraintes spatiales ou temporelles (`REL-IN`, `REL-BEFORE`, etc.).

Les symboles `REL-*` MUST être interprétés comme des **relations binaires** (au minimum) entre entités ou états, même si des arités plus élevées peuvent être représentées via des structures (cf. Chapitre 8).

7.3 Symboles d’opération (OP‑*)
-------------------------------

Les symboles `OP-*` représentent des **opérations conceptuelles**, c’est‑à‑dire des transformations qui :

- prennent des entités, états ou valeurs comme **entrées** ;
- produisent des entités, états ou valeurs comme **sorties**.

Exemples (USC‑96) :

- gestion des entités :
  - `OP-DEF` : définir une nouvelle entité ou relation ;
  - `OP-REF` : référencer une entité existante ;
- mesure et comparaison :
  - `OP-MEAS` : mesurer (input → valeur) ;
  - `OP-COMP` : comparer ;
- opérations numériques :
  - `OP-ADD`, `OP-SUB`, `OP-MUL`, `OP-DIV`, `OP-MOD`, `OP-MAX`, `OP-MIN`, `OP-AVG` ;
- transformations :
  - `OP-ENC`, `OP-DEC` : encoder / décoder ;
  - `OP-MOVE` : déplacer ;
  - `OP-CONVERT` : convertir (type, unité, représentation).

Dans USC‑128 et USC‑256, d’autres opérations plus spécialisées peuvent apparaître, mais elles restent des **spécialisations** conceptuelles des mêmes familles.

Une implémentation USC SHOULD modéliser `OP-*` comme des **fonctions** ou procédures, dans un style proche des langages fonctionnels / logiques :

- type d’entrée (signature) ;
- type de sortie ;
- pré‑conditions et post‑conditions éventuelles.

7.4 Symboles structurels (STR‑*, GRAPH‑*, TOPO‑*)
-------------------------------------------------

Les symboles structurels décrivent la **forme** des données et des concepts :

- `STR-*` (USC‑96) :
  - `STR-SEQ` : séquence ordonnée ;
  - `STR-SET` : ensemble sans ordre, sans doublons ;
  - `STR-LIST` : liste ordonnée avec doublons possibles ;
  - `STR-GRAPH`, `STR-NODE`, `STR-EDGE` : graphe et ses composants ;
  - `STR-TREE` : arbre ;
  - `STR-MAP` : dictionnaire (clé → valeur).
- `GRAPH-*`, `TOPO-*` (USC‑256) :
  - chemins, cycles, composantes connexes, centralité, flots, coupes, clusters ;
  - ouverts, fermés, frontières, connexité, trous, variétés, espaces métriques.

Rôle :

- donner une forme explicite aux structures manipulées par l’USC (au‑delà d’une simple liste de symboles) ;
- permettre de décrire :
  - des graphes de concepts ;
  - des topologies d’espace ou de réseau ;
  - des structures de données logiques (maps, listes, ensembles).

Une implémentation d’USC combinée à MML PEUT représenter :

- les structures MML (séquences, nœuds, liens) via `STR-*` ;
- les diagnostics de graphe ou propriétés topologiques via `GRAPH-*`, `TOPO-*`.

7.5 Symboles de couches (DISC‑*, META‑*)
---------------------------------------

Les symboles de couches ajoutent des informations sur le **contexte disciplinaire** et les **métadonnées** :

- `DISC-*` : tags de domaine (USC‑256) ;
  - `DISC-PHYS`, `DISC-CHEM`, `DISC-BIO`, `DISC-MED`, `DISC-SPACE`, `DISC-MATH`, `DISC-COMP`, `DISC-INFO` ;
- `META-*` : métadonnées ;
  - `META-VERSION`, `META-SOURCE`, `META-CONFID`, `META-TIMESTAMP`, `META-AUTHOR`.

Rôle :

- `DISC-*` :
  - indiquer dans quelle discipline principale un symbole ou un message doit être interprété ;
  - permettre à une IA de filtrer ou d’indexer les connaissances par domaine.
- `META-*` :
  - tracer la provenance, la version, la confiance et l’auteur d’une information ;
  - faciliter l’audit et la gestion du cycle de vie des messages USC.

Tout système exploitant USC‑256 SHOULD :

- utiliser `DISC-*` pour marquer les blocs conceptuels par domaine ;
- utiliser `META-*` pour annoter les messages structurants (hypothèses, décisions, mesures critiques).

7.6 Symboles de réduction / de contrôle (CTRL‑*, LOG‑*)
-------------------------------------------------------

Les symboles `CTRL-*` (USC‑96) et `LOG-*` (USC‑128) gouvernent la **logique** et le **contrôle de flux** :

- `CTRL-*` :
  - conditionnels (`CTRL-IF`, `CTRL-ELSE`) ;
  - connecteurs (`CTRL-AND`, `CTRL-OR`, `CTRL-NOT`) ;
  - quantificateurs (`CTRL-EXISTS`, `CTRL-FORALL`) ;
  - itération (`CTRL-LOOP`).  
- `LOG-*` :
  - `LOG-IMPLIES` (implication), `LOG-IFF` (équivalence) ;
  - `LOG-NEC` (nécessité), `LOG-POSS` (possibilité) ;
  - `LOG-TRUE`, `LOG-FALSE`, `LOG-TAUTO`, `LOG-CONTRA`.

Rôle :

- permettre de représenter explicitement :
  - des règles ;
  - des conditions de validité ;
  - des preuves simples ou des schémas d’inférence ;
- structurer des **séquences de raisonnement** dans un espace conceptuel :
  - si (condition) alors (conséquence) ;
  - pour tout X, si A(X) alors B(X) ;
  - la formule F est toujours vraie (tautologie) ou impossible (contradiction).

Ces symboles sont au cœur des capacités d’**auditabilité des raisonnements IA** décrites en Partie I, Chapitre 3.

7.7 Symboles mathématiques (MATH‑*, MATH2‑*)
-------------------------------------------

Les symboles `MATH-*` (USC‑128) et `MATH2-*` (USC‑256) fournissent un vocabulaire compact pour les **structures mathématiques** :

- `MATH-*` :
  - analyse : `MATH-LIM`, `MATH-DERIV`, `MATH-INTEG` ;
  - structures : `MATH-VECTOR`, `MATH-MATRIX`, `MATH-NORM`, `MATH-SET`, `MATH-FUNC`, `MATH-REL` ;
  - probabilités / statistiques : `MATH-PROB`, `MATH-EXPECT`, `MATH-VAR`, `MATH-STD` ;
  - constantes : `MATH-PI`, `MATH-E`, `MATH-INF`.
- `MATH2-*` :
  - algèbre : `MATH2-GROUP`, `MATH2-RING`, `MATH2-FIELD`, `MATH2-ALG` ;
  - espaces : `MATH2-VSPACE`, `MATH2-BASIS` ;
  - mesure : `MATH2-MEASURE`, `MATH2-SIGMA` ;
  - topologie / catégories : `MATH2-TOPO`, `MATH2-CAT`, `MATH2-FUNCTOR`, `MATH2-NAT`, `MATH2-LIMIT` ;
  - ordre : `MATH2-ORDER`, `MATH2-LATTICE`.

Rôle :

- permettre aux IA scientifiques d’encoder :
  - des modèles mathématiques,
  - des équations,
  - des propriétés structurelles,
  dans un alphabet conceptuel limité ;
- servir de pont entre les représentations internes des modèles et des langages mathématiques humains (LaTeX, MathML, etc.).

7.8 Symboles universels cosmologiques (option USC‑256)
------------------------------------------------------

Dans l’option USC‑256 la plus ambitieuse, certains symboles peuvent être interprétés comme **cosmologiques** au sens large :

- `SPACE-*` : étoiles, planètes, galaxies, trajectoires orbitales ;
- `PHYS-*` : champs, ondes, rayonnements, particules.

L’idée est de fournir un **noyau minimal** pour décrire :

- la structure de l’univers observable ;
- la dynamique des objets célestes ;
- des phénomènes physiques universels.

Ces symboles, combinés avec les axiomes (`AX-*`) et les relations (`REL-*`), permettent de construire des messages USC potentiellement interprétables par :

- des IA futures n’ayant plus accès aux langues humaines d’origine ;
- des entités non humaines (par hypothèse SETI / interstellaire), capables d’inférer la sémantique à partir de régularités physiques communes.

Cette dimension cosmologique est détaillée et étendue dans les Annexes, en particulier l’Annexe F (“USC et transmission interstellaire”).

