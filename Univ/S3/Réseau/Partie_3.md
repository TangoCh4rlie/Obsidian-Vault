# I)Présentation du protocole DHCP 
(Dynamic Host Configuration Protocol)

Protocole qui fonctionne en mode client serveur, il va permettre à un client d'obtenir dynamiquement sa configuration réseau. Il simplifie l'administration réseau.
Au minimum on a l'adresse IP et le masque (information minimum que donne le serveur), ce protocole ne sert pas à configurer ni les routeurs ni les serveurs puisque ce genre de machine à besoin d'une adresse fixe. Décrit dans la RFC2131.

# II)Fonctionnement du protocole DHCP

### Généralité
Il faut un serveur qui distribue les adresse. Cette machine de base va servir de base pour toutes les requêtes DHCP et peut répondre à des requêtes de nombreux réseau.
Le principe est que le client envoie un broadcast ip dirigé (broadcast à destination d'un protocole en particulier) avec un paquet de requête DHCP, ce dernier va choisir une configuration dans le groupe disponible et il va l'alloué au client.

### Principe d'allocation des adresses
Le client loue ses informations au serveur pour la période définie par l'administrateur (notion de bail DHCP(même principe qu'un bail pour un appartement)). A l'expiration de la période de location, le client doit demander une autre adresse même si généralement l'adresse courante est reconduite. L'admin va configurer le serveur DHCP pour assigner des adresses dans un groupe prédéfini (on parle de pool d'adresses), possibilité d'avoir la passerelle et le serveur [DNS](Partie_1.md) dans la configuration. L'administrateur peut spécifier explicitement les adresses mac que le serveur DHCP peut déservir.
Sur un réseau ou il y a beaucoup de machine qui se branche et se débranche fréquemment on met des baux de courte durée puisque ca ne sert a rien de donner une adresse pour une longue durée
DHCP s'appuie sur le protocole UDP donc pas de vérification mais une réponse rapide (le risque d'erreur est moindre puisque peu de données transitent)
**Client** sur le port 67
**Serveur** sur le port 68

### Types d'allocation

- **Automatique** : le protocole DHCP attribue une adresse IP **permanente** à un client.
- **Manuelle** : C'est l'admin qui attribue l'adresse IP au client et le protocole DHCP va transférer l'adresse au client
- **Dynamique** : C'est le protocole DHCP (serveur) qui concède une adresse ip au client pendant une durée limitée (adresse n'est pas permanente)

### Fonctionnement du protocole DHCP

- Le client va envoyer une requête DHCP au server, il peut arriver que le client suggère l'adresse IP dont il à besoin (notamment lors d'un renouvellement du bail) il va donc envoyer un `DHCP DISCOVER` en broadcast
- Quand le serveur reçoit le broadcast il va déterminer si il peut desservir la requête à partir de sa propre base sinon il peut la transférer à un autre serveur DHCP.
  Si il y parvient le serveur DHCP va proposer une configuration au client avec un `DHCP OFFER`fait en unicast (minimum adr IP et masque)
- Si l'offre correspond au client il va faire un `DHCP REQUEST` il est envoyé en broadcast, qui permet de savoir quel est l'offre qui à été accepté.
- Le serveur envoie un `DHCP ACK` et c'est seulement à ce moment la que le client est configuré

C'est le cas ou tout se passe bien

- Au lieux du request le client envoie un decline pour dire qu'il ne veux pas de cette offre la (dans la plus pars des cas la machine détecte que l'adresse IP est déjà utilisé). Dans ce cas on repart au début du dialogue
- Le serveur envoie un `DHCP NACK` signifiant que le serveur va potentiellement avoir un problème (plantage ou quoi que ce soit)
  
  Lorsque le client n'a plus besoin de l'adresse il va envoyer un `DHCP RELEASE` (deconnexion, arrêt machine) pour dire au serveur que cette adresse peut être ne nouveau alloué.

[Schema](Schema_DHCP_protocole.md)

### Notion de relai

Lors que les deux machines ne sont pas sur le même réseau par ce que le routeur arrête les broadcast (même IP dirigé). Pour remédier à ça il faut indiquer au routeur qu'il est relai DHCP pour qu'il laisse passer seulement les broadcast DHCP dirigé 

#### [TD1](TD1_DHCP.md)