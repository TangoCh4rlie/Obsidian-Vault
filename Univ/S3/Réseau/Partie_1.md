# 1) Notion préalables
[[Univ/S3/Réseau/Ressources/révisions]]
### A quoi ca sert?

### Comment ca marche?

Chaque port a un numéro et chaque port est associer a un service spécifique.

ex : ftp port 21

_Note les port peuvent etre fermé pour des raisons de sécurité (trojan peut access a des ports ouvert)_

### Comment ca marche (technique)

Permet d’identifier la connection entre le client et le serveur

Les ports inferieurs a 1024 sont réservé aux applications coté serveur, supperieur a 1024 c’est pr le coté client (au hazard)

## 2) Protocole TCP (Transmision controle protocole)

### Notions préalables

Fonctionne sur la couche 4 (transport)

Il fiabilise le protocole IP (c’est pr ca TCP/IP)

### Fonctionnalités

Etablismement et fermeture de la connection, controle de flux et de l’aquitement des données.

### Segement TCP

**********voir cours**********

**Numéro de séquence** : numéro du premier octet de ce segment

**Numéro d’aquittement** : numéro du prochain octet attendu

**Longeur d’entete** : exprime en mot de 32 bits

**Réservé : réservé** pour un futur usage

**URG** : champ a 1 si ce sont des données urgentes (en lien avec le champ pointeur d’urgence)

**ACK** : champ a 1 si la veleur du champ numéro d’acquitement doit etre pris en compte (peut ne pas avoir d’acquitement)

**PSH** et **RST** sont des bits indicateurs (non significatif dans le cadre de ce scours)

**SYN** : champ à 1 si c’est un paquet d’ouverture de connexion

**FIN** : champ à 1 si c’est un paquet de fermeture de connexion

**Fenêtre**: nombre d’octet que l’utilisateur peut recevoir sans envoyer d’acquitement

**Checksum**: CRC

**Pointeur d’urgence**: numéro d’octet à traiter en priorité si le champ URG est à 1

## 3) Dialogue TCP

### Etablissement d’une connection

Les numéro de scéquence sont fixé aléatoirement en début de session.

Demande de connection vec un paquet SIN

**********voir schema cours**********

Si ya pas de réponse on renvoit la même plusieur fois mais pas avec le meme labs de temps entre les requettes

Si le port est fermé il revoit un paquet avec le RST à 1

### Fermeture de connection

**********voir schema cours**********

### Envoie de données

La taille de la fenetre est envoyé a chaque echange et elle va pouvoir varier d’un envoi a l’autre dans un meme dialogue d’une machine a une autre.

**********voir schema cours**********

# CH2,DNS

## 1) Vocabulaire préalable

→ 1 adresse FQDN

Chaque machine possede une adresse FQDN (composé du nom de la machine et du domaine auquel elle appartient)

→ 2 Resolution directe/inverse

Dans un réseau quand on a un DNS on connais que le nom de la machine et pas son adresse ip or on a vu qu’il était indispensable de connaitre l’adresse ip d’une machine pour pouvoir dialoguer avec elle. (on peut mettre son url soir l’IP dans un navigateur) Lors d’un dialogue de A vers B, A doit connaître l’adresse ip de B, et donc elle va la demander au serveur dns qui va effectuer une résolution de nom, dans ce sens on parle de résolution de nom directe CAD on part de l’adresse FQDN vers l’adresse IP (l’inverse on part de l’adresse ip pour obtenir l’adresse FQDN)

→ 3 resolution de nom

Deux moyens de stocker les infos pour faire la résolution de nom

- Par fichier host (au lieux de mettre l’adresse ip on met l’adresse FQDN des machines avec leur adresse IP dans un fichier) (solution envisageable pour les petits domaines car ce fichier doit se trouver sur chaque machine)
- Par serveur DNS / serveur de nom (on installe sur une machine du domaine un serveur de nom, chaque machine connais l’adresse ip du serveur DNS, dès qu’une machine veux effectuer une recherche de nom elle questionne le DNS, l’admin lui n’a qu’a config le serveur de nom pour tout le réseau)

## 2) Problématiques liées à l’utilisation d’un serveur DNS

→ 1 Panne d’un serveur DNS

Le serveur DNS est un élément vital d’un réseau, si il tombe en panne les machines du réseau sont incapable de communiquer entres elles

- Saturation : beaucoup de demandes de résolution de nom il ne supporte pas le trafic réseau et est saturé
- Le réseau reliant le serveur DNS aux machines peut tomber en panne (panne matériel)

→ 2 Amélioration de la résistance aux pannes

Pour améliorer la résistance aux pannes on utilise un serveur de nom secondaire qui est en back-up, tout comme le serveur primaire il va être capable de faire de la résolution directe ou inverse (rappel: un DSN peut être utilisé entre plusieurs réseaux). Le DNS secondaire s’installe lorsque le DNS principale est encore en route, tout DNS secondaire doit connaitre l’adresse ip du DNS primaire, lorsqu’on lance le secondaire il va aller questionner le serveur le primaire pour demander une copie des informations utile à la résolution de nom (sachant que pour un domaine donné il ne peut y avoir qu’un seul DNS primaire par contre autant de secondaire qu’on veut).

→ 3 En cas de panne d’un serveur DNS secondaire

Chaque machine doit connaitre une liste de serveur DNS qu’ils soient primaire ou secondaire, la machine interroge ces DNS dans l’ordre d’apparition de la liste, si le premier ne répond pas il va aller interroger le deuxième et ainsi de suite (NB: le premier de la liste n’est pas forcément un DNS primaire), on va donc faire de la répartition de charge pour éviter que toutes les machines interrogent le même DNS. En mettant plusieurs DNS on évite des problèmes de pannes.

→ 4 MAJ des servers DNS

Pour les DNS secondaire la mise a jour est automatique, chaque secondaire va interroger périodiquement le serveur primaire pour savoir si ses informations sont à jours, si ce n’est pas le cas il va récupérer une copie des informations du serveur primaire qui sont utile à la résolution de nom. Le problème qu’on peut rencontrer et le suivant si le secondaire interroge le primaire à un instant T et qu’il est a jour, quelques min plus tard l’admin met a jour le DNS primaire, sauf que le DNS secondaire va attendre un certain temps avant de vérifier si il est a jour. Deux solutions au pb :

- l’admin force le DNS secondaire à se mettre à jour
- il utilise le système de notification (option présente sur le serveur primaire, il doit connaitre sur les adresses IP des serveurs secondaires qui va leur envoyer un msg dès qu’il y a une mise a jour pour qu’il vienne la récupérer

## 3) Notion de zone

Les zones directe permettent de faire la résolution de nom directe.

Les zones inverse permettent de faire la résolution de nom inverse.

******Exemple dans le cours******

## 4) Les fichiers de zone

Fichier texte qui va décrire la zone, il y a donc 1 fichier par zone. Le fichier est composé d’enregistrement (différents enregistrement MX pour les mails….) ordre important car sinon ca ne fonctionne pas (SOA, NS, A/PTR)

- Enregistrement NS permet de spécifier les serveurs de nom qui ont autorité sur la zone. (ex: [DNS-A.toto.fr](http://DNS-A.toto.fr). IN NS [DNS-A.toto.fr](http://DNS-A.toto.fr).)
- Enregistrement SOA permet de fixer les paramètres présent même si il n’y à pas de DNS secondaire ([tuto.fr](http://tuto.fr). IN SOA [DNS-A.toto.fr](http://DNS-A.toto.fr). [admin@DNS-A.toto.fr](mailto:admin@DNS-A.toto.fr).( 32;_version_ 10800;_rafrechissement_ 600;_nouvelle tentative_ 86400;_obsolete_ 3600);_durée vie_
- Enregistrement A uniquement dans le fichier de zone directe, il va permettre de faire la correspondance entre le nom de la machine et son adresse IP (ex: [pc1.toto.fr](http://pc1.toto.fr). IN A 192.168.1.2)
- Enregistrement PTR uniquement dans le fichier de zone inverse, il va permettre de faire la correspondance entre IP d’une machine et son nom (ex: 2.1.168.192.IN-ADDR.APRA IN PTR [pc1.toto.fr](http://pc1.toto.fr).)

# NAT

Objectifs:

- lutter contre la pénurie d’adresse IP (avant l’arrivé d’IPV6)
- sécurité : rendre certaines machines du réseau interne invisible de l’extérieur

Pourquoi:

- Une entreprise connecté à Internet doit acheter des adresses à son FAI
- Même s’il y a beaucoup de machines dans es réseaux interne, peu ont besoin d’un accès direct à internet

Fonctionnement:

- Fonctionnalité présente dans les Firewall et/ou les routeurs
- Fait de la translation d’adresse ⇒ traduit une adresse du réseau privé interne en une adresse publique accessible par l’extérieur (avoir une adresse privé en interne pour la transformer en adresse publique
- En interne, utiliser une adresse privée permanente
- En externe, utiliser une adresse publique permanente ou temporaire
- Etablir une correspondance entre les adresses privées et les adresses publiques
- RAPPLE adresses privées
- 10.X.X.X, 172.16.X.X à 172.31.X.X, 192.168.X.X
- Pour des réseaux privés non connectés à internet

Type de translation

- Translation statique → l’association d’adresse privé/publique est permanent
- Translation dynamique ⇒ les adresses publiques sont prises dans un pool d’adresses, et elles retournent au pool en fin d’utilisation (fin de session ou d”lai de non utilisation de la connexion)

Mécanisme

- Pour chaque datagramme entrant ou sortant, NAT vérifie la présence de l’adresse dans la table
- Si elle y est, on modifie l’adresse et le CRC
- Sinon, on envoie un message ICMP “destinataire inconnu”

# PAT

Fonctionnement

- On associe une adresse privée et un port privé à une adresse publique et un port publique
- On peut avoir une seule adresse publique pour plusieurs adresses privés et une adresse privée peut demander plusieurs connections vers l’extérieur
- Utilisation d’une table de translation: flemme

Pourquoi

- NAT limité par le nombre d’adresses publique possible
- NAT n’est pas supporté par tous les portocoles

# Configuration CISCO

Terminologie

- Inside local address ILA : adresse IP à l’intérieur d’un réseau d’extrémité, généralement une adresse privée, non routanle internet.
- Inside Global Address IGA : adresse IP publique qui représente sur l’internet une adresse ip locale interne

## Configuration NAT :

monRouteur(config)#interface nom Interface monRouteur(config-iffip nat inside monKouteur(config-if)#exit monRouteur(config)# interface nom Interface monRouteur (config-if)#ip nat outside monRouteur(config-if)#exit monRouteur(config)Hip nat pool nom Pool IP _début IP fin netmask masque

Pour des questions de sécurité, on peut rajouter ces lignes (les ACL seront étudiées ultérieurement)

monRouteur(config)#ip nat inside source list numéro ACL pool nom Pool monRouteur (config)#access-list numéro ACL permit IP source masque

[Partie 2](Partie_2)