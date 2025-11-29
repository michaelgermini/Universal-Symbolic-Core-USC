PARTIE IV — COMPATIBILITÉ & INTÉGRATION GLOBALE  
Chapitre 11 — Compatibilité Data & Internet
===========================================

11.1 HTTP / TCP / QUIC
----------------------

USC ne remplace pas les protocoles de transport Internet (TCP, QUIC, HTTP).  
Il fournit une **couche conceptuelle** qui peut être encapsulée dans leurs charges utiles.

Modèle général :

- **TCP / QUIC** : transport fiable (ou quasi‑fiable) d’octets ;
- **HTTP** : sémantique requête/réponse (verbes, en‑têtes, corps) ;
- **USC** : contenu conceptuel de certaines requêtes / réponses ;
- éventuellement **MML / DNF** : structuration et sérialisation autour d’USC.

Intégration recommandée :

- HTTP REST ou RPC peut transporter :
  - des corps `application/usc+json` (séquences d’IDs USC sérialisées en JSON) ;
  - ou `application/usc+binary` (flux binaire compact) ;
  - ou encore `application/usc+mml` (USC structuré par MML).  
- Les en‑têtes HTTP PEUVENT contenir des métadonnées USC :
  - version (`META-VERSION`),
  - domaine (`DISC-*`),
  - confiance (`META-CONFID`).

Un service compatible USC SHOULD :

- publier une spécification de ses **endpoints USC** (schémas des messages, profils de symboles) ;
- traiter les messages USC comme première classe, avec conversions éventuelles vers/depuis JSON “humain”.

11.2 WebSocket minimal
----------------------

Les WebSockets fournissent un canal bidirectionnel persistant au‑dessus de TCP.  
USC peut y être utilisé comme :

- **format natif** pour les messages IA ↔ serveur ;
- ou comme **canal secondaire** dans des messages plus riches.

Schéma minimal :

- chaque message WebSocket transporte :
  - soit un tableau d’IDs USC (`[1, 80, 16, ...]`) ;
  - soit un objet structuré :
    - `{"usc_version": "128-v0.1", "symbols": [...], "meta": {...}}`.  
- les deux extrémités doivent partager :
  - la table USC utilisée (96/128/256) ;
  - les profils de symboles attendus pour chaque type de message.

Avantages :

- très faible overhead par rapport à des messages JSON verbeux ;
- capacité à faire transiter des raisonnements IA compressés en temps réel ;
- facilité d’extension : ajout de nouveaux types de messages par simple convention sur les séquences USC.

11.3 DNS‑over‑USC
-----------------

Le DNS classique résout des **noms symboliques** en adresses (IP, autres enregistrements).  
“DNS‑over‑USC” désigne l’idée de résoudre des **descripteurs conceptuels** plutôt que des simples chaînes de caractères.

Exemples de requêtes conceptuelles :

- “Donne‑moi un service `ENT-MACHINE` de type `ENT-SYSTEM` avec rôle `ENT-RESOURCE` dans le domaine `DISC-PHYS`.”  
- “Résoudre un endpoint pour un service d’analyse médicale (`DISC-MED`, `ENT-SYSTEM`, `ENT-ACTION` de type `MED-DIAG`).”

Dans un DNS‑over‑USC :

- la **clé de résolution** n’est plus seulement un nom (`example.com`), mais :
  - un petit graphe USC décrivant :
    - type de service,
    - contraintes de domaine,
    - éventuellement, exigences de sécurité ;
- la réponse peut être :
  - une adresse réseau classique ;
  - ou un descripteur plus riche (profil de service, version d’API, capacités).

La norme n’impose pas un DNS‑over‑USC standard, mais suggère que des systèmes avancés MAY :

- définir leurs propres schémas de résolution conceptuelle ;
- utiliser l’USC comme langage de requête minimal entre **répertoires de services**.

11.4 Transport crypté USC‑MML
-----------------------------

Le transport sécurisé de messages USC repose sur :

- des protocoles cryptographiques existants (TLS, QUIC, SSH, etc.) ;
- la capacité à chiffrer/anonymiser des charges utiles USC/MML.

Deux niveaux sont distingués :

- **niveau transport** :
  - utilisation de TLS/DTLS/QUIC pour chiffrer le canal ;
  - transparence vis‑à‑vis du contenu USC ;
- **niveau message symbolique** :
  - hachage, signature, chiffrement de blocs USC eux‑mêmes (cf. Partie V, Chapitre 15).

Un format typique “USC‑MML sécurisé” pourrait être :

```text
Header:
  - META-VERSION, META-TIMESTAMP, META-SOURCE
Body:
  - MML structuré, avec feuilles = symboles USC
Security:
  - H(MML+USC) stocké comme symbole ou métadonnée USC
  - signature numérique externe ou intégrée
```

Les systèmes critiques SHOULD :

- définir clairement quelles parties du message sont protégées au niveau transport et/ou au niveau symbolique ;
- prévoir des mécanismes de **vérification d’intégrité** sur les séquences USC (hashing symbolique).

11.5 Intégration native dans MCP
--------------------------------

MCP (Model Context Protocol) et autres protocoles modernes de coordination d’IA peuvent intégrer USC comme :

- format interne pour les “thoughts” (pensées intermédiaires) ;
- format d’échange entre outils, agents et orchestrateurs.

Scénario :

- un orchestrateur MCP reçoit une requête humaine ;
- il la convertit en un graphe USC (profil adapté) ;
- il distribue ce graphe à plusieurs agents IA via MCP ;
- chaque agent renvoie :
  - soit des résultats en USC ;
  - soit des transformations du graphe (ajout d’hypothèses, de preuves, de plans).

L’intégration native USC‑MCP nécessite :

- des **types de message** MCP spécifiques (`usc_message`, `usc_graph`, etc.) ;
- une documentation des profils USC autorisés dans chaque outil ;
- des convertisseurs standard entre USC et les formats textuels / JSON utilisés par MCP.

11.6 API REST compactées
------------------------

De nombreuses API REST actuelles :

- transportent des JSON très verbeux ;
- dupliquent des informations structurelles ;
- encodent des concepts sous forme de chaînes (“status": "OK", "WARN", "ERROR", etc.).

USC permet de définir des **API REST compactées** où :

- le corps des requêtes/réponses est un message USC (JSON ou binaire) ;
- les codes de statut, types d’erreurs, états, actions sont des **symboles USC** plutôt que des chaînes libres.

Exemple :

- au lieu de :
  - `{"status": "CRITICAL", "component": "motor", "code": 12}` ;
- une API USC pourrait renvoyer :
  - `{"usc_version": "96-v0.1", "symbols": [ENT-SYSTEM, ENT-RISK, ...]}`  
  (en pratique, sous forme d’IDs).

Avantages :

- réduction de la taille des messages ;
- normalisation forte des valeurs possibles ;
- meilleure interopérabilité entre implémentations de clients/serveurs.

11.7 USC comme remplacement potentiel URI / JSON (horizon 20 ans)
-----------------------------------------------------------------

À long terme, USC pourrait jouer un rôle plus radical :

- servir de **substrat conceptuel** pour :
  - identifier des ressources (remplacement partiel des URI),
  - décrire des données (remplacement partiel du JSON/XML),
  - exprimer des requêtes (complément ou alternative à certains DSL).

Hypothèse de travail (horizon 20 ans et plus) :

- les couches actuelles (URI, JSON, XML, formats ad hoc) restent, mais :
  - une part croissante des échanges machine‑machine se fait :
    - soit en USC natif,
    - soit en formats hybrides où USC est la couche de signification minimale ;
  - les URI elles‑mêmes peuvent être “typées” conceptuellement en USC (ex. préfixes ou suffixes codant des `ENT-*`, `DISC-*`, etc.).

La norme actuelle ne prescrit pas cette migration, mais :

- elle définit USC de manière à ce qu’une telle évolution soit **structurellement possible** ;
- elle fournit les bases nécessaires pour des **expérimentations progressives** dans des environnements limités (clusters d’IA, réseaux industriels, systèmes fermés).  
Des cas d’usage illustratifs de ces intégrations sont présentés dans **l’Annexe C** (diagrammes) et **l’Annexe D** (exemples d’encodage).

