PARTIE VI — ANNEXES TECHNIQUES  
Annexe C — Diagrammes de compatibilité USC
==========================================

> Cette annexe décrit, sous forme textuelle, des “diagrammes” de compatibilité entre USC et différents environnements.

Internet
--------

Schéma conceptuel simplifié :

- Couche L0/L1 : **USC + MML** (concepts + structure minimale) ;
- Couche L2 : sérialisation (JSON, binaire, DNF) ;
- Couche L3 : protocoles applicatifs (HTTP, WebSocket, gRPC, MCP, etc.) ;
- Couche L4 : transport réseau (TCP, QUIC, TLS).

Relations clés :

- USC est **agnostique** au transport : tout ce qui est requis est un canal d’octets fiable ou partiellement fiable ;
- les APIs Internet peuvent définir des **endpoints USC** :
  - entrées/sorties en USC natif ;
  - ou wrappers texte autour d’un noyau USC.

LoRa
----

Schéma :

- Application : profil USC‑96 (mesures, états, commandes) ;
- Encodage : 1 octet = 1 symbole USC, trame LoRa = en‑tête + séquence USC ;
- Transport : LoRa PHY/MAC (bande ISM, SF, etc.).

Compatibilité :

- l’application s’exprime en USC‑96 ;
- les contraintes de LoRa (taille de payload, duty cycle) guident :
  - la longueur des séquences USC ;
  - la sélection des symboles réellement utilisés.

HF
--

Schéma :

- Application : profil USC‑96 minimal (urgence, télémétrie essentielle) ;
- Encodage : mapping symbole → motif binaire/FSK/PSK adapté à la radio HF ;
- Transport : couche physique HF (3–30 MHz) + protocoles existants (AX.25, modes numériques, etc.).

Compatibilité :

- USC se superpose aux schémas HF existants comme couche conceptuelle ;
- les mêmes messages conceptuels peuvent :
  - être envoyés par HF,
  - puis être stockés / analysés dans un backend IP, sans perdre leur sens.

IA
--

Schéma multi‑couches :

- Noyau IA : représentations internes continues (vecteurs, tenseurs) ;
- Couche symbolique : USC (concepts) ;
- Couche de dialogue : texte humain, UI, API.

Compatibilité :

- les échanges **IA ↔ IA** peuvent se faire en USC ;
- les échanges **IA ↔ humain** se font en texte ou UI dérivés d’USC ;
- les logs et traces internes peuvent être **mixtes** :
  - vecteurs + USC,
  - avec possibilité de réinterprétation a posteriori.

Drones
------

Schéma :

- Bord (drone) :
  - perception → représentations internes ;
  - décision → séquences USC (“plan de vol”, “mission”, “état”) ;
  - radio → encodage USC vers LoRa/HF/UHF.  
- Sol (station) :
  - réception radio → décodage USC ;
  - supervision IA → interprétation des séquences USC ;
  - commandes → génération de nouvelles séquences USC.

Compatibilité :

- un “plan de mission” peut être :
  - défini sur le sol en USC,
  - exécuté à bord,
  - mis à jour en vol,
  - archivé pour analyse,
  sans changer de langage conceptuel.

