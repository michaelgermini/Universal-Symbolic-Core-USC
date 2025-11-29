PARTIE VI — ANNEXES TECHNIQUES  
Annexe E — Comparatif USC vs Unicode vs ASCII vs UTF‑8
======================================================

Cette annexe compare l’USC aux encodages textuels classiques (ASCII, Unicode, UTF‑8) selon plusieurs axes.

Limites
-------

**ASCII / Unicode / UTF‑8** :

- conçoivent le problème de base comme : “comment représenter des **caractères** humains ?” ;
- ne définissent pas de sémantique canonique pour :
  - les mots,
  - les phrases,
  - les concepts ;
- acceptent, voire supposent, la **polysémie** et la variation culturelle ;
- ne fournissent aucun cadre pour :
  - raisonner au niveau conceptuel,
  - garantir l’unicité d’un sens donné.

**USC** :

- ne vise pas la représentation de caractères ou de textes ;
- se limite volontairement à un **alphabet conceptuel borné** (96/128/256 symboles) ;
- impose l’absence de polysémie et la stabilité des symboles ;
- ne gère pas :
  - la typographie,
  - les langues humaines,
  - les détails de rendu.

Avantages
---------

**ASCII / Unicode / UTF‑8** :

- excellents pour :
  - l’échange de texte humain ;
  - la compatibilité entre systèmes et langues ;
  - l’archivage de documents.  
- disposent d’un écosystème gigantesque (libs, outils, OS, standards).

**USC** :

- excellents pour :
  - la communication **machine‑machine** à haute densité sémantique ;
  - l’annotation conceptuelle de données et de modèles ;
  - les systèmes contraints (radio bas débit, IoT, air‑gapped) ;
  - les scénarios de **souveraineté cognitive** (réduction de l’empreinte linguistique).

USC ne remplace pas Unicode dans son rôle ; il fournit une **couche différente** pour des besoins différents.

Compression
-----------

ASCII / Unicode / UTF‑8 :

- encodent des caractères ; la densité d’information conceptuelle dépend :
  - de la langue,
  - du style,
  - du contexte ;  
- un même concept peut nécessiter :
  - plusieurs mots,
  - plusieurs phrases,
  - des répétitions.

USC :

- encode des **concepts** directement ;
- vise une densité de l’ordre de 10:1 (ou plus) par rapport au texte pour des contenus techniques ;
- pour des scénarios bien structurés (télémétrie, missions, expériences) :
  - quelques dizaines de symboles USC peuvent résumer ce qui prendrait des centaines de caractères en texte.

En contrepartie :

- l’homme lit plus facilement du texte Unicode ;  
- des outils sont nécessaires pour visualiser / éditer du USC de manière conviviale.

Auditabilité
------------

ASCII / Unicode / UTF‑8 :

- les logs textuels sont lisibles par des humains ;
- mais :
  - fortement redondants ;
  - ambigus ;
  - difficiles à comparer automatiquement ;
  - sujets à des problèmes de confidentialité / empreinte.

USC :

- structure nativement :
  - les entités (`ENT-*`),
  - les relations (`REL-*`),
  - les opérations (`OP-*`),
  - les structures (`STR-*`), etc. ;
- facilite :
  - le hashing symbolique des raisonnements ;
  - la signature de traces ;
  - la comparaison automatique de messages ;
  - la reconstruction de graphes de décision.  
- permet une **auditabilité cryptographique** des IA, en reliant :
  - des traces USC,
  - des hachages,
  - des signatures (cf. Partie V).

En résumé :

- ASCII / Unicode / UTF‑8 sont des **encodages de surface** pour le texte ;
- USC est un **encodage de profondeur** pour les concepts.  
Les deux couches sont complémentaires et peuvent coexister dans des systèmes modernes.

