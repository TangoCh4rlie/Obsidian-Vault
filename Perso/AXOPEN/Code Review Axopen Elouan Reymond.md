### database-connection.js
- mot de passe en clair
- pas de vérification des paramètres (possibilité d'injection sql)
- ne pas exporter la constante connexion pour que d'autres parties de l'app aient un accès directe à la base de donnée. Simplement exporter authenticate qui se charge de toute la partie connexion à la basse de donnée. De plus la constante connexion n'est utilisé a aucun autre endroit dans le code
### helpers/chantier.js
- Faire une requête avec un ```SELECT * FROM chantier where numero = ?``` avec le numéro en paramètre de la fonction query. Il n'y aura jamais plusieurs chantier avec le même numéro puisque  numéro est la clef primaire donc aucun risque d'avoir deux chantier en sortie. De plus ce n'est pas très optimisé de retourner à chaque fois toute la table chantier puis seulement après de trier. On pourrais aussi remplacer l'* par seulement les champs qui nous intéresse réellement au lieux de tout récupérer.
  Cela permettrai la suppression de la méthode find ce qui allègerai le code.
- petit oubli lors de la gestion de l'erreur, il faudrait utiliser le gestion d'erreur personnalisé avec ```throw new PersonnalError('Error when querying', e);```
- paramètre inutile ```params```
- query avec concaténation de chaines de charactères possibilité d'injection sql
### routes/chantier.js
### helpers/user.js

- Pas de requête préparé
### token-utils.js
### random-utils.js
- Utilisation de noms de variable pas très explicite, ne facilite pas la compréhesion du code.
### Index.js
- Variable plus explicite
- Chaine de char pas fou, de plus cette chaine est utilisé a d'autrs endoit dans le code, pourquoi pas la stocker dans un fichier auquel les fonction en ayant besoin peuvent se référer
- Pas d'async
- variable c inutile puisque pas passé en paramètre, on pourrait retirer tout le code en rapport avec cette variable pour simplifier le code
- Simplifier au maximum les endpoint, faire des appels de fonctions aux nom explicite pour clarifier et simplifier le code pour tendre vers un endpoint comme le ```/session/signin``` et non pas comme le ```/session/signup```
### db.sql
- Char et pas varchar
- email trop court
- password trop court il ne permet pas de sotcker de mot de pass hasher
- champ email verification inutile puisque vérifié avant (sinon ajouter une contrainte Check)
- pas de clé primaire pour user par exemple une colonne id pour pourvoir autoincréementer cette valeur
- (optionnel) il n'y a pas de champ nom pour permettre d'identifier facilement utilisateur
- pas de check si la valeur de fin est supérieur a celle de début (pour la cohérence) (Check SQL)
- aucune relation entre les deux tables il est donc difficile par exemple de savoir quels user est sur quel chantier
- passer le type de description en TEXT 
- potientiellement passer en mediumint mais pour seulement un gain de 1 octet :)
  pour sur passer en UNSIGNED INT
### générales
- ne pas push le fichier .env sur le repo distant
- création de la base de donnée avec un orm pour avoir une meilleur adaptabilité et une meilleure réutilisabilité du projet
- la connexion a la base de données n'est jamais fermée après les requête pour libérer les ressources, mais dans le cas d'une petite API dans ce cas ce n'est pas forcément utile

