[← Chapitre précédent](01-Pourquoi-des-couches.md) · [Sommaire](Readme.md) · [Chapitre suivant →](03-L-encapsulation.md)

# Le modèle OSI, couche par couche

## 🎯 Objectifs du chapitre

À la fin de ce chapitre, vous saurez :

1. Citer les sept couches du modèle OSI dans l'ordre, dans les deux sens.
2. Donner pour chaque couche son rôle, son unité de données et son type d'adresse.
3. Placer les équipements courants (hub, switch, routeur, pare-feu, proxy) sur la bonne couche.
4. Ranger un protocole courant dans sa couche.

---

## 1. Vue d'ensemble

Les couches sont numérotées **de bas en haut** : la couche 1 correspond au
support physique, la couche 7 à l'application.

| N° | Couche | Rôle | Unité de données (PDU) | Exemples |
|---|---|---|---|---|
| 7 | **Application** | Offrir des services réseau aux logiciels | Données | HTTP, DNS, SMTP, SSH, DHCP |
| 6 | **Présentation** | Mettre les données dans un format commun : encodage, compression, chiffrement | Données | UTF-8, JPEG, TLS* |
| 5 | **Session** | Ouvrir, maintenir et fermer un dialogue | Données | RPC, NetBIOS |
| 4 | **Transport** | Acheminer de bout en bout, d'un programme à un autre | Segment (TCP), datagramme (UDP) | TCP, UDP |
| 3 | **Réseau** | Acheminer entre réseaux différents : adressage logique et routage | Paquet | IPv4, IPv6, ICMP |
| 2 | **Liaison de données** | Acheminer sur le réseau local : adressage physique, détection d'erreurs | Trame | Ethernet, Wi-Fi, PPP |
| 1 | **Physique** | Transmettre des bits sous forme de signal | Bit | paire torsadée, fibre, radio |

\* TLS est souvent classé en couche 6. En pratique, il se situe entre la couche
transport et l'application.

Le terme **PDU** (*Protocol Data Unit*) désigne l'unité de données manipulée par
une couche. Chaque couche a son propre terme : on parle de **trame** Ethernet et
de **paquet** IP.

### Retenir l'ordre

Une phrase mnémotechnique par sens de lecture :

- **de 1 à 7** : **P**our **L**e **R**éseau, **T**out **S**e **P**asse **A**utomatiquement
  (Physique, Liaison, Réseau, Transport, Session, Présentation, Application) ;
- **de 7 à 1**, en anglais : **A**ll **P**eople **S**eem **T**o **N**eed **D**ata **P**rocessing
  (Application, Presentation, Session, Transport, Network, Data link, Physical).

### Couches hautes, couches basses

- Les couches **1 à 3** assurent l'**acheminement**. Elles sont mises en œuvre
  par les postes et par les équipements réseau traversés.
- Les couches **4 à 7** sont dites **de bout en bout**. Elles n'existent que sur
  les deux extrémités de l'échange, le client et le serveur. Un routeur ne
  traite pas le contenu d'une page web.

---

## 2. Couche 1 : Physique

**Rôle :** transformer les bits en signal (électrique, lumineux, radio) et
inversement. Elle définit les câbles, les connecteurs, les niveaux de tension,
les fréquences et le débit.

- **PDU** : bit ;
- **Adressage** : aucun, la couche 1 ne sait pas à qui elle transmet ;
- **Équipements** : câbles (paire torsadée cat. 6, fibre optique), connecteurs RJ45 et LC, modules SFP, répéteurs, concentrateurs (*hubs*, obsolètes) ;
- **Normes** : 1000BASE-T (Gigabit sur cuivre), 10GBASE-SR (10 Gbit/s sur fibre), la partie radio du Wi-Fi.

**Pannes courantes :** voyant de lien éteint, câble endommagé, connecteur mal
serti, fibre sale, négociation de vitesse en échec.

---

## 3. Couche 2 : Liaison de données

**Rôle :** faire circuler des **trames** entre deux équipements **du même réseau
local**, en les adressant grâce aux **adresses MAC**, et détecter les erreurs de
transmission grâce au champ de contrôle **FCS** placé en fin de trame.

- **PDU** : trame ;
- **Adressage** : adresse MAC de 48 bits, attribuée par le constructeur de la carte réseau (mais modifiable par logiciel), écrite en hexadécimal (`3c:52:82:1a:f4:07`), dont les 24 premiers bits identifient le constructeur ;
- **Équipements** : switch (commutateur), point d'accès Wi-Fi, carte réseau ;
- **Protocoles** : Ethernet (IEEE 802.3), Wi-Fi (IEEE 802.11), VLAN (IEEE 802.1Q), STP, PPP.

Un **switch** enregistre dans sa **table MAC** le port sur lequel se trouve
chaque adresse MAC. Il envoie ensuite chaque trame uniquement vers le port
concerné, alors qu'un hub la répétait sur tous ses ports.

Une trame ne franchit pas le **routeur** : pour aller plus loin, il faut une
adresse valable sur plusieurs réseaux, fournie par la couche 3. L'adresse
spéciale `ff:ff:ff:ff:ff:ff` (**diffusion** ou *broadcast*) désigne tous les
équipements du réseau local.

---

## 4. Couche 3 : Réseau

**Rôle :** acheminer des **paquets** d'un réseau à un autre jusqu'à la
destination finale, en choisissant le chemin. C'est le **routage**.

- **PDU** : paquet ;
- **Adressage** : adresse IP, logique, attribuée par l'administrateur ou par DHCP (32 bits en IPv4, par exemple `192.168.10.25` ; 128 bits en IPv6, par exemple `2001:db8::25`) ;
- **Équipements** : routeur, switch de niveau 3, pare-feu ;
- **Protocoles** : IPv4, IPv6, ICMP (utilisé par `ping`), et les protocoles de routage OSPF et BGP.

Le routeur lit l'**adresse IP de destination**, consulte sa **table de
routage** et transmet le paquet au routeur suivant. À chaque routeur traversé,
le champ **TTL** (*Time To Live*) du paquet diminue de 1. À 0, le paquet est
détruit, ce qui empêche un paquet de circuler en boucle indéfiniment.

> **À retenir :** l'adresse **MAC** identifie un équipement sur le réseau
> local, l'adresse **IP** identifie la destination finale. Le chapitre suivant
> montre que l'adresse MAC change à chaque routeur, alors que l'adresse IP reste
> la même (sauf traduction d'adresses, ou NAT).

---

## 5. Couche 4 : Transport

**Rôle :** acheminer les données **de bout en bout**, d'un **programme** à un
autre sur deux machines. Elle découpe aussi les données en segments et, avec
TCP, garantit qu'ils arrivent tous et dans l'ordre.

- **PDU** : segment (TCP), datagramme (UDP) ;
- **Adressage** : numéro de **port** sur 16 bits, de 0 à 65 535 (443 pour HTTPS, 22 pour SSH) ;
- **Équipements** : pare-feu (filtrage par port), répartiteur de charge ;
- **Protocoles** : TCP (fiable, orienté connexion), UDP (léger, sans garantie).

Une adresse IP désigne une machine, un port désigne un service sur cette
machine. Le couple **adresse IP + port** s'appelle un **socket** :
`10.0.20.15:443` désigne le service HTTPS du serveur `10.0.20.15`.

Le chapitre 4 compare TCP et UDP en détail.

---

## 6. Couches 5 et 6 : Session et Présentation

Ces deux couches ont rarement un protocole dédié dans les réseaux actuels.

- **Session (5)** : ouvrir, synchroniser et fermer un dialogue entre deux
  applications, reprendre un transfert interrompu à un point de reprise.
  Exemples : RPC, NetBIOS.
- **Présentation (6)** : s'accorder sur la **forme** des données (encodage des
  caractères en UTF-8, formats d'image ou de vidéo comme JPEG ou MP4,
  compression, chiffrement).

Dans TCP/IP, ces fonctions sont prises en charge **par les applications**. Le
modèle TCP/IP n'a donc pas de couches 5 et 6 : elles sont intégrées à sa couche
Application (chapitre 4).

---

## 7. Couche 7 : Application

**Rôle :** fournir aux logiciels les services réseau dont ils ont besoin :
afficher une page, envoyer un courriel, résoudre un nom, ouvrir une session à
distance.

- **PDU** : données (on parle aussi de *message*) ;
- **Adressage** : identifiants propres à chaque service (nom de domaine, URL, adresse de courriel) ;
- **Équipements** : proxy, pare-feu applicatif (WAF), pare-feu de nouvelle génération, répartiteur de charge applicatif ;
- **Protocoles** : HTTP/HTTPS, DNS, DHCP, SMTP, IMAP, SSH, FTP, SNMP, LDAP, RDP.

> **Attention :** Firefox, Outlook ou PuTTY ne font pas partie de la couche 7.
> Ce sont des applications qui **utilisent** des protocoles de couche 7 (HTTP,
> SMTP, SSH).

---

## 8. Jusqu'à quelle couche travaille chaque équipement ?

Un équipement "travaille" jusqu'à la couche la plus haute dont il lit les
informations pour prendre ses décisions.

| Équipement | Couches | Il décide en fonction de… |
|---|---|---|
| Hub (concentrateur) | 1 | rien : il répète le signal sur tous ses ports |
| Switch | 1 → 2 | l'adresse MAC de destination |
| Point d'accès Wi-Fi | 1 → 2 | l'adresse MAC ; il fait le pont entre radio et câble |
| Routeur, switch de niveau 3 | 1 → 3 | l'adresse IP de destination |
| Pare-feu classique | 1 → 4 | les adresses IP, le protocole et les ports |
| Proxy, WAF, pare-feu de nouvelle génération | 1 → 7 | le contenu : URL, application, utilisateur |
| Poste, serveur | 1 → 7 | toutes les couches, puisqu'il produit et consomme les données |

---

## Exercice : ranger dans les couches

Indiquez la couche OSI de chaque élément :

1. `SSH`
2. un câble catégorie 6
3. l'adresse `192.168.10.25`
4. l'adresse `3c:52:82:1a:f4:07`
5. le port `443`
6. un switch non administrable
7. `UDP`
8. le format `JPEG`
9. `ICMP`
10. la norme Wi-Fi 802.11ax, pour sa partie "trames"

<details>
<summary>Voir la correction</summary>

1. `SSH` : couche 7, Application.
2. Câble cat. 6 : couche 1, Physique.
3. `192.168.10.25` : couche 3, Réseau (adresse IPv4).
4. `3c:52:82:1a:f4:07` : couche 2, Liaison (adresse MAC).
5. Port `443` : couche 4, Transport.
6. Switch non administrable : couche 2, Liaison.
7. `UDP` : couche 4, Transport.
8. `JPEG` : couche 6, Présentation.
9. `ICMP` : couche 3, Réseau. ICMP est transporté directement par IP, sans TCP
   ni UDP.
10. Wi-Fi, partie trames : couche 2, Liaison (la partie radio relève de la
    couche 1).

</details>

---

[← Chapitre précédent](01-Pourquoi-des-couches.md) · [Sommaire](Readme.md) · [Chapitre suivant →](03-L-encapsulation.md)
