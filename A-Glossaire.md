[← Chapitre précédent](05-Diagnostiquer-et-securiser.md) · [Sommaire](Readme.md)

# Glossaire

Les termes du cours, dans l'ordre alphabétique. Le numéro entre crochets
renvoie à la couche OSI concernée, quand il y en a une.

## De A à I

| Terme | Définition |
|---|---|
| **Adresse IP** [3] | Adresse logique d'une interface, attribuée par l'administrateur ou par DHCP : 32 bits en IPv4, 128 bits en IPv6. Elle reste la même de bout en bout. |
| **Adresse MAC** [2] | Adresse physique d'une carte réseau, sur 48 bits. Elle ne vaut que sur le réseau local et change à chaque routeur traversé. |
| **ARP** [2-3] | *Address Resolution Protocol*. Trouve l'adresse MAC qui correspond à une adresse IP du réseau local, par une question envoyée en diffusion. |
| **Bit** [1] | Plus petite unité d'information, 0 ou 1. PDU de la couche Physique. |
| **Datagramme** [4] | Nom de la PDU d'UDP. Désigne plus largement un message envoyé sans connexion préalable. |
| **Désencapsulation** | Retrait successif des en-têtes à la réception, de la couche 1 vers la couche 7. |
| **DHCP** [7] | *Dynamic Host Configuration Protocol*. Attribue automatiquement adresse IP, masque, passerelle et serveurs DNS. |
| **Diffusion** (*broadcast*) [2] | Envoi à tous les équipements du réseau local, adresse MAC `ff:ff:ff:ff:ff:ff`. |
| **DNS** [7] | *Domain Name System*. Traduit un nom (`intranet.example.com`) en adresse IP. |
| **Encapsulation** | Ajout successif d'un en-tête par chaque couche à l'émission, de la couche 7 vers la couche 1. |
| **En-tête** (*header*) | Informations ajoutées devant les données par une couche, à l'intention de la couche de même niveau sur la machine distante. |
| **FCS** [2] | *Frame Check Sequence*. Queue de trame Ethernet (4 octets) qui permet de détecter une trame altérée. |
| **ICMP** [3] | *Internet Control Message Protocol*. Messages de contrôle et d'erreur d'IP, utilisés par `ping` et `traceroute`. |
| **IETF** | *Internet Engineering Task Force*. Organisme qui élabore les normes d'Internet, publiées sous forme de RFC. |
| **ISO** | Organisation internationale de normalisation, auteur du modèle OSI (norme ISO 7498). |

## De N à V

| Terme | Définition |
|---|---|
| **NAT** [3] | *Network Address Translation*. Remplacement d'une adresse IP par une autre au passage d'un routeur, typiquement une adresse privée par une adresse publique. |
| **OSI** | *Open Systems Interconnection*. Modèle de référence en sept couches publié par l'ISO en 1984. |
| **Paquet** [3] | PDU de la couche Réseau : l'en-tête IP et ce qu'il transporte. |
| **Pare-feu** | Équipement ou logiciel qui filtre le trafic. Selon son type, il lit les couches 3 et 4, ou jusqu'à la couche 7. |
| **Passerelle par défaut** [3] | Routeur auquel un poste confie tout paquet destiné à un autre réseau que le sien. |
| **PDU** | *Protocol Data Unit*. Unité de données propre à une couche : bits, trame, paquet, segment, données. |
| **Port** [4] | Numéro sur 16 bits qui désigne un service ou un programme sur une machine : 22 pour SSH, 443 pour HTTPS. |
| **Protocole** | Ensemble de règles qui régit le dialogue entre deux couches de même niveau sur deux machines différentes. |
| **RFC** | *Request For Comments*. Documents publics qui définissent les protocoles d'Internet : RFC 791 pour IPv4, RFC 793 pour TCP. |
| **Routeur** [3] | Équipement qui relie des réseaux différents et achemine les paquets d'après leur adresse IP de destination. |
| **Segment** [4] | PDU de TCP : l'en-tête TCP et les données qu'il transporte. |
| **Service** | Ce qu'une couche offre à la couche immédiatement supérieure, sur la même machine. |
| **Socket** [4] | Couple adresse IP + port, par exemple `10.0.20.15:443`. |
| **Switch** (commutateur) [2] | Équipement qui relie les appareils d'un même réseau local et achemine les trames d'après leur adresse MAC de destination. |
| **TCP** [4] | *Transmission Control Protocol*. Transport fiable, orienté connexion, qui garantit l'ordre et la livraison des données. |
| **Trame** [2] | PDU de la couche Liaison : en-tête Ethernet, paquet, FCS. |
| **TTL** [3] | *Time To Live*. Compteur de l'en-tête IP, diminué de 1 à chaque routeur ; le paquet est détruit à 0. |
| **UDP** [4] | *User Datagram Protocol*. Transport léger, sans connexion ni garantie de livraison. |
| **VLAN** [2] | Réseau local virtuel : découpage d'un même switch en plusieurs réseaux isolés les uns des autres. |

---

[← Chapitre précédent](05-Diagnostiquer-et-securiser.md) · [Sommaire](Readme.md)
