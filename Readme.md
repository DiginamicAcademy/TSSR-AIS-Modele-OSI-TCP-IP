# Introduction au modèle OSI et à TCP/IP

Ce cours présente le vocabulaire commun des métiers du réseau : les modèles en
couches, le rôle de chaque couche et le trajet d'une donnée entre un poste et un
serveur.

- **Public** : apprenants TSSR (Technicien Supérieur Systèmes et Réseaux) et
  AIS (Administrateur d'Infrastructures Sécurisées).
- **Prérequis** : utiliser un poste Windows ou Linux et un terminal ; avoir
  déjà rencontré une adresse IP.
- **Format** : exposé illustré, démonstrations en ligne de commande, quiz final.

## 🎯 Objectifs pédagogiques

À la fin de ce cours, vous saurez :

1. Expliquer pourquoi on décrit les réseaux en couches.
2. Citer les sept couches du modèle OSI, dans l'ordre, avec le rôle de chacune.
3. Associer à chaque couche son unité de données, son type d'adresse, ses équipements et quelques protocoles.
4. Décrire l'encapsulation d'une donnée, de l'application jusqu'au câble, et le chemin inverse.
5. Faire correspondre les quatre couches du modèle TCP/IP à celles d'OSI.
6. Situer une panne ou une attaque sur la bonne couche, et choisir la commande qui la vérifie.

## ❔ Pourquoi ce cours ?

Des expressions comme "problème de couche 2", "switch de niveau 3" ou
"pare-feu applicatif" font référence au modèle en couches. Ce modèle sert de
vocabulaire commun aux équipes réseau, aux éditeurs et à la documentation
technique. Les séquences suivantes (adressage IP, VLAN, routage, services
réseau, pare-feu, VPN) s'appuient dessus.

- En **TSSR**, il fournit une méthode de dépannage : on vérifie les couches une
  par une.
- En **AIS**, il permet d'organiser la sécurité : chaque couche a ses attaques
  et ses contre-mesures.

## Le parcours

Chaque étape correspond à un fichier. Les étapes se suivent dans l'ordre, chacune s'appuyant sur la précédente.

| # | Étape | Contenu |
|---|---|---|
| [01](01-Pourquoi-des-couches.md) | Pourquoi un modèle en couches ? | le problème de l'interopérabilité, protocole et service, historique des deux modèles |
| [02](02-Le-modele-OSI.md) | Le modèle OSI, couche par couche | les sept couches : rôle, unité de données, adressage, équipements, protocoles |
| [03](03-L-encapsulation.md) | L'encapsulation | en-têtes ajoutés puis retirés, trajet à travers un switch et un routeur, ARP, lecture dans Wireshark |
| [04](04-Le-modele-TCP-IP.md) | Le modèle TCP/IP | les quatre couches et leur correspondance avec OSI, TCP ou UDP, la poignée de main, les ports courants |
| [05](05-Diagnostiquer-et-securiser.md) | Diagnostiquer et sécuriser par couche | méthode de dépannage, commandes Windows et Linux, attaques et pare-feu par couche, quiz |
| [A](A-Glossaire.md) | Glossaire | définitions des termes du cours |

Les diapositives de la séance sont dans `slides.md`.
