[Correction du ds](Correction_DS.md)
## Principe de base

### Principe de base : adressage

IPV4 une interface = une adresse

IPV6 une interface = une ou plusieurs adresses

### Principe de base : format des paquets

Format des paquets

- Le format du paquet change
- addresses plus longue
- plus d’option
- plus de fragmentation

### Principe de base : format des paquets

Acheminement Identique à l’IPV4 sur les points suivant

- Best effort
- Acheminement basé sur la notion de sous réseau
- Table de routage de même format (mais distincte de l’IPV4)
- IMCPv6 notifie les erreurs
- Protocole de routage “externe” permettant la mise a jour des tables de routages

## Les adresses IPv6

- L’adressage IPV6 est décrit dans le RFC 3513
- l’adresse est codé sur 16 octets (128 bits)
- Elle est représenté sous forme hexadécimale
- Il n’est pas nécessaire de représenter les 0 en têtes
- Les champs nuls consécutifs peuvent être abrégé (ne peut apparaitre qu’une fois)

## Adresse link local

- adresse configuré automatiquement par la station pour une interface
- permet de communiquer sur un LAN en l’absence de routeur

## Les champs de l’entete IPV6

- Version(4bits) : égale a 6
- Traffic class (8bits): classe de trafic diff serv
- Flow label (20bits) : identificateur de flux
- payload length(16bits): taille des données utiles en octets
- Next Header (8bits): identifier soit le protocole de niveau suppérieur soit la prochaine option IPv6
- hop limit (8bits) : TTL IPv4
- Source adresse et destination adresse (2x8 octets

## Le checksum

En IPV4

- les trames de niveau liaison offre généralement un contrôle du contenu de la trame par un CRC
- Idem au niveau UDP et TCP
- Vérification de recalcule systématique du checksum par les routeurs

En IPv6

- plus de checksum au niveau IP
- devient obligatoire au niveau supérieur

## Fragmentation extension

- fonctionnement indentique à IPv4
- La fragmentation ne se fait quede bout en bout : les routeurs ne fragmente pas
- Place du fragment 13 bits: nombre de mots de 8 bits

## Conclusion

Sécurité

- integration obligatoire d’IPsec à la pile TCP/IPv6

Mobilité

- solution de gestion de la mobilité au travers de méchaniqmes spécifiques : options / IMCPv6

Déploiements

Protocole toujours en evolution