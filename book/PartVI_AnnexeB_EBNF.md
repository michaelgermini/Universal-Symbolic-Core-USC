PARTIE VI — ANNEXES TECHNIQUES  
Annexe B — EBNF officielle USC
==============================

> Cette annexe fournit une **grammaire EBNF de référence** pour la structuration de messages USC.  
> Elle est volontairement générique ; des profils plus restreints peuvent en dériver pour des usages spécifiques.

Notes générales
---------------

- La grammaire décrit des **structures logiques** (messages, expressions, structures), pas le format binaire exact sur le fil.  
- Les terminaux `SYM-USC` représentent des **symboles USC individuels** (IDs 0–255).  
- Les implémentations peuvent choisir :
  - une sérialisation binaire compacte ;
  - ou une forme textuelle structurée (ex. JSON, XML) conforme à cette EBNF.

Terminaux et non‑terminaux de base
----------------------------------

```ebnf
digit        = "0" | "1" | "2" | "3" | "4" | "5" | "6" | "7" | "8" | "9" ;

sym-id       = digit , { digit } ;         (* ID USC en décimal *)

SYM-USC      = sym-id ;                    (* référence à un symbole USC canonique *)

(* Dans une implémentation binaire, SYM-USC est porteur de l’ID (0..255) *)
```

Structure générale d’un message
-------------------------------

```ebnf
message      = header? , body ;

header       = "[" , meta-list , "]" ;

meta-list    = meta , { "," , meta } ;

meta         = meta-version
             | meta-source
             | meta-timestamp
             | meta-confid
             | meta-author ;

meta-version = "META-VERSION" , ":" , sym-id ;
meta-source  = "META-SOURCE"  , ":" , SYM-USC ;
meta-timestamp = "META-TIMESTAMP" , ":" , sym-id ;
meta-confid  = "META-CONFID"  , ":" , sym-id ;
meta-author  = "META-AUTHOR"  , ":" , SYM-USC ;

body         = expr-list ;

expr-list    = expr , { separator , expr } ;

separator    = ";" | "," | SYM-USC ;  (* par ex. STR-SEQ ou STR-SET comme séparateur conceptuel *)
```

Expressions conceptuelles
-------------------------

```ebnf
expr         = ent-expr
             | rel-expr
             | op-expr
             | struct-expr
             | numeric-expr ;

ent-expr     = [ "AX-ENT" ] , ent-sym , [ ent-qualifiers ] ;

ent-sym      = SYM-USC ;   (* attendu de classe ENT-* ou assimilé *)

ent-qualifiers = { rel-expr } ;

rel-expr     = ent-sym , rel-sym , ent-sym ;

rel-sym      = SYM-USC ;   (* attendu de classe REL-* *)

op-expr      = op-sym , "(" , arg-list , ")" ;

op-sym       = SYM-USC ;   (* attendu de classe OP-* *)

arg-list     = expr , { "," , expr } ;

numeric-expr = num-prefix? , number , [ unit ] ;

num-prefix   = SYM-USC ;   (* NUM-SIGN, NUM-PCT, NUM-RANGE, etc. *)

number       = digit , { digit } , [ "." , digit , { digit } ] ;

unit         = SYM-USC ;   (* UNIT-TIME, UNIT-LEN, UNIT-MASS, UNIT-ENERGY, etc. *)
```

Structures (séquences, graphes, arbres, maps)
---------------------------------------------

```ebnf
struct-expr  = seq-expr
             | set-expr
             | list-expr
             | graph-expr
             | tree-expr
             | map-expr ;

seq-expr     = "STR-SEQ" , "(" , expr-list , ")" ;

set-expr     = "STR-SET" , "{" , expr-list , "}" ;

list-expr    = "STR-LIST" , "[" , expr-list , "]" ;

graph-expr   = "STR-GRAPH" , "(" , node-list , ";" , edge-list , ")" ;

node-list    = node-expr , { "," , node-expr } ;

node-expr    = "STR-NODE" , "(" , SYM-USC , "," , expr? , ")" ;

edge-list    = edge-expr , { "," , edge-expr } ;

edge-expr    = "STR-EDGE" , "(" , SYM-USC , "," , SYM-USC , "," , rel-sym , ")" ;

tree-expr    = "STR-TREE" , "(" , node-expr , { "," , tree-expr } , ")" ;

map-expr     = "STR-MAP" , "(" , map-entry , { "," , map-entry } , ")" ;

map-entry    = "(" , expr , "->" , expr , ")" ;
```

Contraintes de classes symboliques
----------------------------------

La grammaire ci‑dessus est **structurelle**.  
Pour être conforme à USC, des **contraintes de classes** doivent être respectées :

- `ent-sym` DOIT être un symbole de classe `ENT-*` (ou assimilé via profil) ;
- `rel-sym` DOIT être un symbole de classe `REL-*` ;
- `op-sym` DOIT être un symbole de classe `OP-*` ;
- les unités (`unit`) DOIVENT être des symboles `UNIT-*` ;
- certains contextes PEUVENT exiger des symboles d’autres classes spécifiques (PHYS-*, MED-*, etc.).

Ces contraintes peuvent être exprimées :

- soit dans des **règles supplémentaires** (schémas de validation) ;
- soit dans des profils d’usage (par domaine, par protocole).

Profils et spécialisations
---------------------------

La grammaire EBNF de base peut être **spécialisée** en profils :

- profil USC‑96 minimal (limité aux classes AX, REL, OP, STR, CTRL, NUM, ENT) ;
- profil scientifique USC‑128 (ajout MATH, SCI, LOG) ;
- profil disciplinaire USC‑256 (ajout PHYS, CHEM, BIO, MED, SPACE, MAP, MATH2, INFO, COMP, DISC, META).

Chaque profil DOIT :

- déclarer explicitement :
  - la liste des classes symboliques autorisées ;
  - les productions EBNF effectivement utilisées ;
- fournir des **exemples normatifs** de messages valides et invalides.

Lien avec MML
-------------

La grammaire USC décrit :

- quels symboles peuvent apparaître ;
- comment ces symboles peuvent être combinés en expressions et structures.

MML décrit :

- la manière de sérialiser ces structures dans un **langage de balisage minimal** ;
- la forme exacte des arbres / graphes résultants.

Pour tout profil USC donné, il DOIT exister :

- une spécification “USC ↔ MML” définissant :
  - comment chaque production EBNF se traduit en éléments MML ;
  - comment reconstruire une structure USC à partir d’un document MML conforme.

Cette annexe fixe la **base grammaticale**. Les annexes suivantes illustrent l’usage de cette grammaire dans :

- des diagrammes de compatibilité (Annexe C) ;
- des exemples d’encodage (Annexe D) ;
- des comparaisons avec d’autres formats (Annexe E).

