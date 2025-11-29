PARTIE IV — COMPATIBILITÉ & INTÉGRATION GLOBALE  
Chapitre 10 — Compatibilité Réseaux Contraints
===============================================

10.1 HF (High Frequency)
------------------------

Les bandes HF (3–30 MHz) sont utilisées pour des communications longue distance, souvent :

- fortement bruitées ;
- à bande passante réduite ;
- soumises à des phénomènes de propagation complexes (ionosphère, fading).

Exigences pour USC sur HF :

- **faible débit** : quelques dizaines à quelques centaines de bits par seconde ;
- **robustesse** : tolérance aux erreurs de bit ;
- **simplicité de démodulation** : modulation adaptée au matériel existant (modems HF, radios amateurs, etc.).

USC‑96 est le profil privilégié pour ces environnements :

- 7 bits d’information par symbole, éventuellement protégés par :
  - bits de parité,
  - codes correcteurs d’erreurs au niveau protocole ;
- trames courtes, structurées autour :
  - d’identifiants de système (`ENT-SYSTEM`, `META-SOURCE`) ;
  - d’états et risques (`ENT-STATE`, `ENT-RISK`) ;
  - d’actions minimales (`ENT-ACTION`, `OP-MEAS`, `OP-MOVE`).

Un protocole HF basé sur USC SHOULD :

- définir un en‑tête compact (version USC, profil, checksum) ;
- limiter la charge utile à un nombre restreint de symboles par trame ;
- inclure des mécanismes de répétition / redondance pour les messages critiques.

10.2 VHF / UHF
--------------

Les bandes VHF/UHF offrent généralement :

- une meilleure qualité de signal que la HF ;
- des débits utilisables plus élevés (selon la modulation et le canal) ;
- une portée plus limitée mais plus prévisible.

Dans ce contexte, USC peut :

- utiliser USC‑96 ou USC‑128 selon les besoins ;
- se combiner avec des protocoles existants (APRS, TETRA, systèmes propriétaires).

Recommandations :

- les systèmes qui transportent déjà des **trames de télémétrie** PEUVENT :
  - encapsuler la charge conceptuelle en USC ;
  - réduire la dépendance à des formats textuels (par ex. trames ASCII verbeuses) ;
- les réseaux professionnels (sécurité civile, industriel) peuvent définir des **profils USC** :
  - liste de symboles autorisés ;
  - structures de messages (état véhicule, statut mission, alerte, etc.).

10.3 LoRa
---------

LoRa (Long Range) est un protocole radio basse consommation, bas débit, très utilisé pour l’IoT.  
Ses caractéristiques en font une cible privilégiée pour USC‑96 :

- charge utile typique : quelques dizaines d’octets ;
- contraintes fortes sur :
  - la taille des messages,
  - la fréquence des transmissions,
  - l’énergie consommée.

USC sur LoRa :

- permet de remplacer des charges JSON / texte par des séquences de symboles ;
- réduit la taille des messages en exprimant directement les concepts plutôt que leurs noms littéraux ;
- facilite le décodage par des nœuds variés (capteurs, passerelles, backend IA).

Profil recommandé :

- utiliser principalement USC‑96 ;
- définir :
  - un en‑tête minimal (version USC, type de message, ID nœud) ;
  - un petit nombre de formats de trame (mesure simple, alerte, commande, ack) ;
- maintenir des **tables partagées** entre les nœuds LoRa et les serveurs de collecte.

10.4 Sigfox
-----------

Sigfox est un autre réseau IoT bas débit, encore plus restrictif que LoRa en termes de taille de message.  
Dans ce cas, la densité sémantique de l’USC est particulièrement utile :

- très peu d’octets transmis par message ;
- coût énergétique et monétaire lié au volume.

Intégration USC :

- USC‑96 MIGHT être utilisé pour encoder :
  - des événements rares mais critiques (alarme, changement d’état majeur) ;
  - des mesures fortement compressées (valeur + unité abstraite) ;
- des **profils minimaux** peuvent être définis, par ex. :
  - uniquement un sous‑ensemble de symboles ENT‑*, AX‑*, REL‑*, NUM‑* ;
  - quelques patterns n‑grammes récurrents pour les scénarios clés.

Pour Sigfox, la norme recommande :

- de documenter précisément chaque **format de message USC** ;
- de privilégier la **stabilité** des formats dans le temps (pour éviter des migrations complexes).

10.5 APRS
---------

APRS (Automatic Packet Reporting System) est un protocole largement utilisé en radio amateur pour :

- rapporter des positions,
- transmettre des télémétries simples,
- relayer des messages courts.

Aujourd’hui, APRS repose principalement sur :

- des trames textuelles structurées (mais souvent spécifiques) ;
- des conventions semi‑informelles.

USC peut être utilisé :

- comme **couche conceptuelle** sous‑jacente à APRS ;
- ou comme format interne des contenus, avant qu’ils ne soient :
  - rendus en texte pour compatibilité humaine ;
  - ou transmis sous forme binaire sur des variantes expérimentales d’APRS.

Exemple d’intégration :

- un tracker APRS encode :
  - sa position (`MAP-COORD` + `AX-SPACE`) ;
  - son état (`ENT-STATE`, `ENT-RISK` éventuelle) ;
  - son objectif (`ENT-GOAL`) ;
- le tout en USC‑96, puis :
  - soit converti en trame APRS texte “classique” ;
  - soit transmis dans un sous‑canal binaire USC interprété par des logiciels compatibles.

10.6 Transmission Morse compressée
----------------------------------

La télégraphie Morse reste, dans certains milieux (radioamateurs, militaires, exploration), une solution **extrêmement robuste** en conditions difficiles.

USC peut être projeté sur du Morse :

- en définissant un **alphabet de code** qui mappe chaque symbole USC‑96 :
  - soit sur un code Morse direct (par ex. via un identifiant de 2–3 lettres) ;
  - soit sur une séquence de chiffres/lettres optimisée ;
- en exploitant le fait que :
  - l’opérateur (humain ou machine) n’a pas besoin de connaître la langue humaine, seulement le code.

Scénarios :

- transmission de messages USC critiques en Morse lent, mais **sémantiquement dense** ;
- possibilité de décoder les messages ultérieurement avec un logiciel connaissant les tables USC.

Un profil “USC‑Morse” SHOULD :

- spécifier un mappage stable symbole USC → code Morse ;
- fournir des exemples normatifs de messages (détresse, état, commande minimale).

10.7 Encodage audio basse‑bande
-------------------------------

Enfin, USC peut être transporté sous forme de signaux audio basse‑bande, par exemple :

- tonales FSK/PSK simples ;
- DTMF ou schémas inspirés ;
- signaux encodables / décodables par des dispositifs très simples.

Objectif :

- permettre la transmission de messages USC :
  - via des canaux audio analogiques (réseaux téléphoniques anciens, radios voix, enregistrements) ;
  - ou via des médias physiques (enregistrements sur bande, disques, etc.).

Un schéma d’encodage audio USC SHOULD :

- définir une modulation (jeu de fréquences, symboles par seconde) ;
- lier directement **un symbole USC** à **une unité sonore** (ou un petit motif sonore) ;
- prévoir des signaux de synchronisation et de framing (début/fin de message, horodatage, checksum audio).

Dans tous ces réseaux contraints, USC fournit le **vocabulaire minimal** ;  
les schémas d’encodage (HF, LoRa, Morse, audio) sont des couches de transport qui peuvent évoluer sans casser la sémantique des messages.  
Des schémas et exemples supplémentaires sont fournis dans **l’Annexe C — Diagrammes de compatibilité USC** et **l’Annexe D — Exemples concrets d’encodage USC**.

