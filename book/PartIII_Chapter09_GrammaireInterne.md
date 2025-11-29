PARTIE III — STRUCTURES INTERNES DU USC  
Chapitre 9 — Grammaire symbolique interne
=========================================

9.1 Structure arborescente interne
----------------------------------

L’USC n’est pas seulement une liste plate de symboles. Dans la plupart des usages, les symboles sont organisés en **structures arborescentes** ou **graphes** :

- chaque **nœud** d’un arbre peut être :
  - un symbole USC isolé (ex. `ENT-AGENT`) ;
  - ou une structure composite (ex. une séquence, un bloc conditionnel, un graphe) ;
- les **arêtes** représentent :
  - des relations (`REL-*`) ;
  - des liens de structure (`STR-NODE`, `STR-EDGE`, etc.) ;
  - des opérandes / arguments d’opérations (`OP-*`).

Une représentation typique d’un message USC complet suit le schéma :

- niveau 0 : racine (contexte général, par ex. `ENT-SYSTEM`, `DISC-*`) ;
- niveau 1 : sous‑structures (agents, objectifs, contraintes, mesures, actions) ;
- niveau 2+ : détails (entités, relations, nombres, unités, propriétés).

Cette structuration peut être :

- explicite, via MML ou un autre langage de balisage minimal ;
- implicite, via des conventions de position dans une séquence USC (ex. tri‑grammes vus au Chapitre 8).

Une implémentation USC SHOULD :

- disposer d’un **modèle interne de graphe ou d’arbre** ;
- être capable de projeter une séquence de symboles sur cette structure ;
- conserver la possibilité de revenir à la séquence (serialisation).

9.2 Définition formelle BNF / EBNF
----------------------------------

La grammaire complète de l’USC est formalisée en EBNF dans l’Annexe B.  
Cette section en présente une **vue simplifiée** pour les principaux concepts.

Notations :

- `<SYM>` : symbole USC élémentaire (ID + nom canonique) ;
- `<SEQ>` : séquence de symboles ;
- `<EXPR>` : expression conceptuelle ;
- `<REL-EXPR>` : expression relationnelle ;
- `<OP-EXPR>` : expression opérationnelle.

Esquisse de grammaire (informelle) :

- `<message> ::= <header>? <body>`  
- `<header>  ::= <meta>*`  
- `<meta>    ::= META-VERSION | META-SOURCE | META-CONFID | META-TIMESTAMP | META-AUTHOR`  
- `<body>    ::= <expr-list>`  
- `<expr-list> ::= <expr> ( <sep> <expr> )*`  
- `<sep>     ::= STR-SEQ | STR-SET | STR-LIST`

Expressions conceptuelles :

- `<expr> ::= <ent-expr> | <rel-expr> | <op-expr> | <struct-expr>`  
- `<ent-expr> ::= (AX-ENT)? ENT-* (REL-SUB ENT-*)*`  
- `<rel-expr> ::= ENT-* REL-* ENT-*`  
- `<op-expr> ::= OP-* <arg-list>`  
- `<arg-list> ::= <expr> ( <sep> <expr> )*`  
- `<struct-expr> ::= STR-GRAPH <graph-body> | STR-TREE <tree-body> | STR-MAP <map-body>`

Ces règles ne sont pas exhaustives, mais elles montrent que :

- les symboles USC ne sont pas utilisés au hasard ;
- des **schémas structurés** de type sujet‑relation‑objet, opération‑arguments, graphe‑nœuds‑arêtes sont encouragés par la grammaire.

L’Annexe B fournit une EBNF complète, adaptée à l’implémentation de parseurs USC.

9.3 Contrainte : pas de polysémie
---------------------------------

Au niveau de la grammaire, l’interdiction de la polysémie se traduit par :

- une règle : **un symbole = un rôle grammatical principal** ;
- un encadrement : certaines positions grammaticales ne peuvent accueillir que certains types de symboles.

Par exemple :

- les positions de **tête d’expression d’entité** (`<ent-expr>`) SHOULD être remplies par des `ENT-*` ;
- les positions de **relation binaire** dans `<rel-expr>` SHOULD être remplies par des `REL-*` ;
- les positions de **tête d’expression opérationnelle** (`<op-expr>`) MUST être des `OP-*`.

Ainsi :

- `ENT-HUMAN` ne peut pas être utilisé comme relation ou opération ;
- `REL-CAUSE` ne peut pas être utilisé comme entité ;
- `OP-MEAS` ne peut pas être utilisé comme simple label d’entité.

Cette discipline grammaticale renforce :

- la clarté des messages USC ;
- la capacité des parseurs à détecter des erreurs d’usage ;
- la stabilité sémantique dans le temps.

9.4 Contrainte : entropie stable
--------------------------------

La **stabilité de l’entropie** signifie que :

- l’ajout de nouvelles productions grammaticales ou de nouveaux symboles NE DOIT PAS :
  - introduire de redondances massives ;
  - rendre ambiguë l’interprétation de structures existantes.

Au niveau de la grammaire, cela implique que :

- les nouvelles règles EBNF SHOULD :
  - s’appuyer sur des non‑terminaux existants (`<expr>`, `<rel-expr>`, `<op-expr>`, etc.) ;
  - éviter de multiplier les formes alternatives pour un même rôle ;
- les **profils d’usage** (par domaine, par protocole) DOIVENT être documentés :
  - quels symboles et règles sont utilisés ;
  - quelles constructions sont interdites ou déconseillées.

Une grammaire USC mal contrôlée aurait tendance à :

- reproduire la prolifération et la redondance des langages naturels ;
- perdre les bénéfices de compacité et de clarté recherchés par l’USC.

La norme USC encourage donc :

- un **nombre limité de schémas de phrase conceptuelle** (sujet‑relation‑objet, opération‑arguments, graphe structuré, etc.) ;
- des extension disciplinaires (USC‑256) qui se branchent sur ces schémas sans les multiplier.

9.5 Contrainte : mappage déterministe → MML
-------------------------------------------

Une exigence centrale de l’USC est la capacité à être **mappé de manière déterministe** vers MML (Minimal Markup Language), et réciproquement lorsque c’est défini.

Cela signifie que :

- pour chaque **construction grammaticale USC valide**, il existe :
  - au moins une représentation MML canonique correspondante ;
  - une fonction de traduction bien spécifiée ;
- deux parseurs indépendants, partant d’un même message USC, DOIVENT produire la même structure MML (à isomorphisme près).

Conséquences sur la grammaire :

- les productions EBNF USC sont conçues pour se **caler** sur les briques de MML :
  - séquences,
  - nœuds typés,
  - relations étiquetées,
  - attributs et valeurs ;
- la grammaire USC évite :
  - des constructions contextuelles difficiles à sérialiser ;
  - des dépendances d’ordre purement positionnel non reflétées en structure MML.

En pratique, pour un sous‑ensemble donné de l’USC, il DOIT exister :

- un document de spécification “USC ↔ MML” décrivant :
  - quelles règles EBNF USC sont autorisées dans ce sous‑ensemble ;
  - comment chaque règle se traduit dans les structures MML ;
- des exemples normatifs de :
  - messages USC,
  - structures MML correspondantes,
  - éventuellement, formes textuelles dérivées (JSON, XML, RDF, etc.).

Cette contrainte de mappage déterministe garantit que l’USC n’est pas un langage fermé sur lui‑même, mais une **couche L0/L1** intégrable dans des stacks plus larges (cf. Partie I, Chapitre 1 et Partie IV).

