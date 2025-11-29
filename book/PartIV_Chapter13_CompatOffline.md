PARTIE IV — COMPATIBILITÉ & INTÉGRATION GLOBALE  
Chapitre 13 — Compatibilité Systèmes Offline
============================================

13.1 Air‑gapped
----------------

Les systèmes **air‑gapped** sont physiquement isolés des réseaux publics (Internet) pour des raisons de sécurité ou de souveraineté.  
Ils incluent, par exemple :

- certaines infrastructures critiques (énergie, défense, industrie) ;
- des laboratoires sensibles ;
- des environnements de développement sécurisés.

Contraintes spécifiques :

- mises à jour logicielles rares et fortement contrôlées ;
- environnements hétérogènes (OS, matériels) qui ne peuvent pas être réalignés en continu ;
- absence de services de résolution ou de métadonnées en ligne.

USC est adapté à ces contextes car :

- les tables de symboles (USC‑96 / 128 / 256) peuvent être **embarquées localement** ;
- la sémantique des symboles est stable et documentée dans un volume limité ;
- les échanges entre sous‑systèmes air‑gapped peuvent se faire :
  - via des supports physiques (clé USB, disques, QR codes, documents imprimés codant de l’USC) ;
  - via des canaux locaux (bus industriels, réseaux internes).

Un système air‑gapped compatible USC SHOULD :

- conserver une **copie versionnée** des tables USC utilisées ;
- documenter, dans ses propres spécifications internes, les profils USC autorisés ;
- prévoir des outils locaux pour :
  - visualiser,
  - auditer,
  - transformer les messages USC, sans dépendre de services externes.

13.2 SCADA
----------

Les systèmes **SCADA** (Supervisory Control And Data Acquisition) pilotent des processus industriels :

- réseaux électriques,
- usines,
- pipelines,
- stations de pompage, etc.

Ils sont souvent :

- anciens, avec des protocoles propriétaires ou obsolètes ;
- contraints en bande passante et en fiabilité ;
- soumis à de fortes exigences de sécurité.

USC peut y apporter :

- un **vocabulaire commun** pour décrire :
  - états de capteurs (`ENT-STATE`, `NUM-*`, `UNIT-*`) ;
  - commandes (`ENT-ACTION`, `OP-*`) ;
  - alarmes (`ENT-RISK`, `REL-CAUSE`) ;
- une couche conceptuelle **indépendante des protocoles** (Modbus, DNP3, OPC UA, etc.).

Intégration possible :

- passerelles SCADA PEUVENT :
  - traduire des trames natives en messages USC ;
  - exposer ces messages à des IA de supervision / diagnostic ;
- les IHM opérateur peuvent :
  - consommer des descriptions USC pour générer des vues plus cohérentes de l’état du système.

13.3 Systèmes autonomes militaires
----------------------------------

Les systèmes militaires autonomes ou semi‑autonomes (drones, véhicules, systèmes de défense) opèrent :

- dans des environnements contestés ou dégradés ;
- avec des exigences extrêmes de robustesse, de sécurité, de souveraineté.

Beaucoup de ces systèmes fonctionnent en **mode déconnecté** :

- liaisons radio intermittentes, brouillées ou inexistantes ;
- décisions prises localement par des IA embarquées.

USC peut servir :

- de **langage de commande et de rapport** entre :
  - capteurs,
  - systèmes d’armes,
  - systèmes de commandement ;
- de base commune pour :
  - décrire des règles d’engagement (symboles `REL-*`, `CTRL-*`, `LOG-*`) ;
  - exprimer des objectifs et contraintes (`ENT-GOAL`, `ENT-RISK`).

Dans ce domaine, les implémentations USC MUST :

- respecter des exigences strictes de sûreté et de sécurité ;
- documenter précisément les profils de symboles utilisés ;
- être validées par des processus de certification adaptés.

13.4 Satellites non connectés
-----------------------------

Certains satellites ou sondes spatiales :

- ne sont pas en contact permanent avec une station sol ;
- disposent de fenêtres de communication limitées ;
- peuvent être isolés pour de longues périodes.

USC est pertinent pour :

- structurer la **télémétrie** et les **télécommandes** :
  - en USC‑96 pour les liaisons les plus contraintes ;
  - en USC‑128 / 256 pour des charges plus riches (scientifiques) ;
- encoder des **scénarios d’autonomie** :
  - plans de mission exprimés en USC,
  - règles de sécurité et de reconfiguration.

Ces messages peuvent être :

- générés au sol, stockés dans le satellite, exécutés progressivement ;
- ou produits par des IA embarquées, puis renvoyés vers le sol pour analyse.

13.5 Bases logistiques isolées
------------------------------

Des bases logistiques ou scientifiques (déserts, régions polaires, sous‑marines, etc.) disposent souvent :

- de connexions limitées, coûteuses ou intermittentes ;
- de systèmes hétérogènes (anciens + modernes) devant coopérer.

USC peut être utilisé pour :

- standardiser la description :
  - des stocks (`ENT-RESOURCE`, `NUM-*`, `UNIT-*`) ;
  - des flux (`OP-MOVE`, `REL-IN`, `REL-OUT`) ;
  - des statuts (`ENT-STATE`, `ENT-RISK`) ;
- échanger des **rapports compacts** via :
  - liaisons satellites bas débit,
  - supports physiques transportés (“sneakernet”).

L’intérêt clé est la **résilience sémantique** :

- même si certains systèmes tombent en panne ou sont remplacés,
- les messages USC archivés restent interprétables par d’autres acteurs futurs.

13.6 Réseaux clandestins ou catastrophes
----------------------------------------

En situation de catastrophe majeure (cataclysme, guerre, effondrement d’infrastructures) ou dans des réseaux clandestins :

- les canaux de communication sont :
  - intermittents,
  - surveillés,
  - fortement limités en bande passante ;
- les risques de compromission sont élevés.

USC permet :

- de transmettre des **messages très denses** en information :
  - alertes,
  - instructions,
  - états de ressources et de populations ;
- d’encoder ces messages sous diverses formes :
  - radio basique,
  - audio analogique,
  - impressions papier (tableaux USC lisibles par IA ultérieurement).

Des réseaux résilients PEUVENT :

- adopter un **profil USC minimal** (quelques dizaines de symboles) ;
- définir des **codes opérationnels** basés sur des séquences USC ;
- stocker des documents de référence (tables USC, exemples) dans des archives physiques robustes.

Dans tous ces cas, la compatibilité USC‑offline vise à garantir que :

- même sans Internet ni services globaux,
- des IA et systèmes autonomes peuvent continuer à communiquer, se coordonner et préserver leurs connaissances dans un langage conceptuel stable.  
Des schémas de haut niveau pour ces scénarios sont détaillés en **Annexe C — Diagrammes de compatibilité USC**, et des exemples concrets de messages correspondants en **Annexe D — Exemples d’encodage USC**.

