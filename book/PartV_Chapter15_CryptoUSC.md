PARTIE V — SÉCURITÉ & SOUVERAINETÉ  
Chapitre 15 — Cryptographie USC‑native
=====================================

15.1 Espaces symboliques comme vecteurs cryptographiques
--------------------------------------------------------

Les séquences de symboles USC peuvent être vues comme des **vecteurs dans un espace discret** de dimension réduite (96, 128 ou 256).  
Cela en fait des candidats naturels pour :

- des **entrées de fonctions de hachage** ;
- des **vecteurs d’état** dans des protocoles d’authentification ;
- des **identifiants de messages** ou de sessions.

Propriétés intéressantes :

- l’alphabet est **borné et normalisé** (IDs 0–255 au maximum) ;
- la sémantique de chaque symbole est **canonique** ;
- les séquences ont souvent une structure interne (bi‑/tri‑grammes, graphes) qui peut être exploitée pour :
  - détecter des mutations sémantiquement incohérentes ;
  - définir des notions de **distance conceptuelle** entre messages.

Une “cryptographie USC‑native” ne remplace pas les primitives cryptographiques classiques (AES, SHA‑2/3, etc.), mais :

- elle les **spécialise** à des messages conçus dès le départ comme symboliques ;
- elle introduit des mécanismes supplémentaires :
  - détection de corruption sémantique (pas seulement binaire),
  - engagement sur des structures conceptuelles plutôt que sur des octets bruts.

15.2 USC dans le chiffrement quantique
--------------------------------------

Les protocoles de chiffrement quantique (QKD, distribution de clés, etc.) fournissent des **clés secrètes** exploitables ensuite par des schémas classiques.  
USC s’insère dans cette chaîne à deux niveaux :

1. niveau **clé / session** :  
   - les clés dérivées d’un protocole quantique peuvent servir à chiffrer des messages USC‑MML ;  
   - la structure symbolique des messages permet :
     - un contrôle plus fin de ce qui est protégé (par ex. certains blocs seulement) ;
     - une classification disciplinaire (`DISC-*`) pour ajuster les politiques de chiffrement.
2. niveau **métadonnées de sécurité** :  
   - les symboles `AX-INF`, `META-CONFID`, `META-SOURCE`, `META-TIMESTAMP` peuvent :  
     - représenter explicitement des étiquettes de sécurité,  
     - être inclus dans la partie authentifiée des messages chiffrés.

Ainsi, un système utilisant QKD et USC peut :

- chiffrer des flux conceptuels compacts ;
- attacher à chaque message USC :
  - son niveau de confidentialité,
  - son domaine (`DISC-*`),
  - son horodatage sécurisé.

15.3 USC pour l’authentification offline
----------------------------------------

Dans les contextes offline ou faiblement connectés (cf. Partie IV, Chapitre 13), il est souvent nécessaire de :

- **authentifier** un appareil, un agent ou un message ;
- sans accès à une infrastructure en ligne (PKI, serveurs d’authentification, etc.).

USC peut aider à construire des schémas d’authentification offline basés sur :

- des **séquences de symboles** pré‑partagées ;
- des **challenges conceptuels** plutôt que purement numériques.

Exemples de mécanismes :

- un appareil embarque un **profil USC secret** (séquence de symboles et règles associées) ;
- lors d’une authentification, une station de contrôle envoie :
  - un challenge partiellement USC (par ex. “combinaison d’`ENT-*` et de `OP-*`”) ;
  - l’appareil doit répondre avec une séquence conforme à des règles convenues ;
- la réponse est ensuite passée dans une fonction de hachage classique, comparée à une valeur attendue.

Ce type de mécanisme :

- ajoute une couche **sémantique** à l’authentification ;
- peut être plus robuste à certains types de clonage naïf (copie brute des octets) ;
- facilite des mécanismes d’authentification “humain + machine” (l’opérateur peut vérifier un motif USC compréhensible).

15.4 Hashing symbolique
------------------------

Le **hashing symbolique** consiste à appliquer des fonctions de hachage à :

- des séquences de symboles USC ;
- ou à des graphes conceptuels USC + MML.

Objectifs :

- garantir l’intégrité des raisonnements, décisions, hypothèses ;
- permettre des comparaisons rapides :
  - de messages,
  - de versions de modèles,
  - de traces de raisonnement.

Pipeline typique :

1. sérialiser une structure USC (séquence ou graphe) dans un format canonique :  
   - ordre des symboles bien défini ;
   - gestion des identifiants internes de nœuds ;
   - normalisation des métadonnées (META-*).
2. appliquer une fonction de hachage (SHA‑2/3, BLAKE2/3, etc.) ;
3. stocker le hash dans :
   - un champ externe (base de données, journal) ;
   - ou un symbole USC dédié (par exemple via une extension future).

Deux structures USC ayant le même hash :

- sont extrêmement susceptibles d’être identiques (au format près) ;
- peuvent être traitées comme deux représentations du **même raisonnement** ou du **même message**.

Le hashing symbolique est utilisé dans :

- les journaux d’audit (cf. 12.8 et Chapitre 16) ;
- les protocoles de consensus entre IA (accord sur un graphe USC donné) ;
- les architectures de type “Merkle tree” symbolique, où chaque nœud représente une partie d’un raisonnement.

15.5 Canonisation signée
------------------------

La **canonisation signée** désigne le processus par lequel :

- un raisonnement, un message, une hypothèse ou un modèle USC est :
  - mis sous une forme **canonique** (structure et sérialisation normalisées) ;
  - puis **signé** par une entité (humaine, IA, organisation).

Étapes principales :

1. **Canonisation** :  
   - tri ou ordonnancement déterministe des éléments ;
   - élimination des variations purement syntaxiques (ordre des champs, espacements, etc.) ;
   - définition d’un format unique pour la structure USC/MML.
2. **Hachage** :  
   - calcul d’un hash sur cette représentation canonique.
3. **Signature** :  
   - application d’une signature numérique (clé privée d’une entité) sur ce hash ;
   - association de la signature à des métadonnées USC (`META-AUTHOR`, `META-SOURCE`, `META-TIMESTAMP`).

Résultat :

- tout système disposant de :
  - la clé publique correspondante,
  - la représentation canonique,
peut vérifier que :

- le contenu n’a pas été altéré ;
- la signature provient bien de l’entité déclarée ;
- la date, la source, le domaine (DISC-*) sont ceux annoncés.

La canonisation signée est essentielle pour :

- des **protocoles d’accord entre IA** (publication de résultats, d’hypothèses, de modèles) ;
- des **archives longues durées** (messages scientifiques, décisions critiques) ;
- des **systèmes de responsabilité** (qui a produit quelle hypothèse / décision).

L’USC joue ici un double rôle :

- fournir la **matière conceptuelle** à canoniser et signer ;
- fournir les **symboles** pour décrire les métadonnées de signature et de vérification au sein même des messages.

15.6 Protocole type : trace USC → hash → signature → vérification
-----------------------------------------------------------------

Cette section décrit un protocole complet, de bout en bout, pour :

- produire une **trace de raisonnement USC** ;
- la **canoniser** ;
- la **hacher** ;
- la **signer** ;
- et la **vérifier** ultérieurement.

Étape 1 — Production de la trace USC
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Une IA exécute un raisonnement aboutissant à une décision critique (par ex. validation d’une hypothèse scientifique, commande envoyée à un système autonome).

Elle génère une trace structurée :

- graphe USC+MML décrivant :
  - les entités en jeu (`ENT-*`) ;
  - les relations (`REL-*`) ;
  - les opérations effectuées (`OP-*`) ;
  - les données et mesures (`NUM-*`, `UNIT-*`, éventuellement SCI/PHYS/MED) ;
  - les conditions/logiques (`CTRL-*`, `LOG-*`).

Cette trace correspond à un arbre ou graphe conforme à l’Annexe B (EBNF).

Étape 2 — Canonisation
~~~~~~~~~~~~~~~~~~~~~~~

La trace est transformée en **représentation canonique** :

- tri déterministe :
  - ordre des nœuds selon un critère stable (ex. ordre lexical des IDs, profondeur, identifiants internes) ;
- normalisation :
  - format unique des nombres ;
  - ordre fixe des champs (`meta`, `body`, etc.) ;
  - absence d’éléments redondants ;
- sérialisation :
  - texte structuré (JSON, MML, autre) ou binaire, mais **uniquement dans une forme documentée comme canonique**.

Pseudo‑code (schématique) :

```text
function canonicalize(trace_usc):
    normalized = normalize_ids_and_fields(trace_usc)
    ordered    = deterministic_sort(normalized)
    serialized = serialize_to_canonical_form(ordered)
    return serialized
```

Étape 3 — Hashing symbolique
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

On applique ensuite une fonction de hachage cryptographique à la forme canonique :

```text
canon = canonicalize(trace_usc)
hash  = HASH(canon)   # SHA‑256, SHA‑3, BLAKE3, etc.
```

Ce `hash` est :

- un condensé binaire de la trace ;
- stocké dans :
  - un journal externe ;
  - et/ou un champ de métadonnées USC (`META-HASH`, dans une future extension) ;
  - et/ou intégré dans des structures de type Merkle tree.

Étape 4 — Signature
~~~~~~~~~~~~~~~~~~~

Une entité (humaine, organisation, IA mandatée) signe ce `hash` avec sa **clé privée** :

```text
signature = SIGN(private_key, hash)
```

Les métadonnées associées :

- `META-AUTHOR` : symbole USC représentant l’auteur ou son identifiant ;
- `META-SOURCE` : système ou composant source ;
- `META-TIMESTAMP` : horodatage (UNIX time, autre) ;
- éventuellement `META-CONFID` : niveau de confiance.

La trace canonique, son hash et sa signature sont regroupés dans un enregistrement :

```text
record = {
    "canon": canon,
    "hash": hash,
    "signature": signature,
    "meta": {
        "author": META-AUTHOR,
        "source": META-SOURCE,
        "timestamp": META-TIMESTAMP
    }
}
```

Étape 5 — Vérification
~~~~~~~~~~~~~~~~~~~~~~~

Lors d’un audit ultérieur, un vérificateur :

1. Reprend la trace canonique `canon` (reconstruite ou relue).  
2. Recalcule `hash' = HASH(canon)` avec la même fonction.  
3. Vérifie l’égalité `hash' == hash` stocké.  
4. Vérifie la signature :

```text
valid = VERIFY(public_key, hash, signature)
```

Si toutes les vérifications passent, le vérificateur peut conclure que :

- la trace n’a pas été modifiée ;
- elle correspond bien à la signature de l’entité déclarée ;
- les métadonnées associées (auteur, source, timestamp) sont authentiques, sous réserve de la confiance dans l’infrastructure de clés.

Lien avec USC
~~~~~~~~~~~~~

Tout au long de ce protocole :

- USC fournit
  - le **vocabulaire conceptuel** (les symboles de la trace) ;
  - les **métadonnées standardisées** (`META-*`, `DISC-*`) ;
- la cryptographie fournit
  - les fonctions de hachage ;
  - les mécanismes de signature / vérification.

Ainsi, on obtient un pipeline complet et générique “trace USC → hash → signature → vérification” applicable à :

- des raisonnements IA,
- des décisions critiques,
- des modèles et hypothèses scientifiques,
- des protocoles d’accord entre agents.

