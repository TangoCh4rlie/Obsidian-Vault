### database-connection.js (3)
- mot de passe en clair
- pas de vérification des paramètres (possibilité d'injection sql)
- ne pas exporter la constante connexion pour que d'autres parties de l'app aient un accès directe à la base de donnée. Simplement exporter authenticate qui se charge de toute la partie connexion à la basse de donnée. De plus la constante connexion n'est utilisé a aucun autre endroit dans le code
### helpers/chantier.js (4)
- Faire une requête avec un ```SELECT * FROM chantier where numero = ?``` avec le numéro en paramètre de la fonction query. Il n'y aura jamais plusieurs chantier avec le même numéro puisque  numéro est la clef primaire donc aucun risque d'avoir deux chantier en sortie. De plus ce n'est pas très optimisé de retourner à chaque fois toute la table chantier puis seulement après de trier. On pourrais aussi remplacer l'* par seulement les champs qui nous intéresse réellement au lieux de tout récupérer.
  Cela permettrai la suppression de la méthode find ce qui allègerai le code.
- petit oubli lors de la gestion de l'erreur, il faudrait utiliser le gestion d'erreur personnalisé avec ```throw new PersonnalError('Error when querying', e);```
- paramètre inutile ```params```
- query avec concaténation de chaines de charactères possibilité d'injection sql
- nom de putRandomChantier ne corrspond pas réelement a ce que fait la fonction,celle ci peuple la base de donnée il auait été plus correct de l'appeler CreaterRandomChantier
- les fonctions ne vérifient pas si l'utilisateur est connecté ou si il a les droits pour effectuer ces actions on aurait pu utiliser les méthodes créés dans token-utils.js pour vérifier si l'utilisateur est bien connecté et si on token jwt est encore valable
- pour la fonction putrandomchantier il serait préferable de passer des valeurs en paramètre pour le peuplement
### routes/chantier.js
- pas de verification du contenu saisit par l'utilisateur de l'api
- gestion d'erreur nul puisqu que des codes 500
- uiliser un post et non pas un put pour la création d'un chantier
### helpers/user.js (4)

- pas de hash du mot de passe le mdp est donc stocké en clair dans la bdd
- pas e gestion d'erreur
- utilisation du like comme on connais exactment le contenu des chaines que l'on comprare on peu utiliser un like pour minimisr les risques de résultats inatndu
- je pense que le promise de findIncludeUser et de createUser n'est pas nécésaire dans ce cas pusique la fonction qury retourne déja une promesse
### token-utils.js(5)
- temps d'expiration du token plutot fair un refresh token porblèm si vol du token
- pas de gestion d'erreur donc plus dificile pour le debogage si la fonction verifyAndExtractToken ne marche pas par exemple
- dans crate token il srai préferable de créer une copie de l'objet user pour après pouvoir effectuer des modifications et non pas sur l'objet qui passé en paramètre et qui est retourné en fin de fonction
- certaines methodes ne sont jamais appelé autre part dans le projet
- l'algo de chiffremnt HS256 est basé seulement sur une clef secrete si celle ci viens a leak ou est volé alors la sécurité est mise en jeu on pourrait se baser sur un algo de chifremnt avec ujn syssèm de clé publique/privés
### random-utils.js (2)
- Utilisation de noms de variable pas très explicite, ne facilite pas la compréhesion du code.
- aussi chaine de char pas fou
### Index.js (6)
- Variable plus explicite
- Chaine de char pas fou, de plus cette chaine est utilisé a d'autrs endoit dans le code, pourquoi pas la stocker dans un fichier auquel les fonction en ayant besoin peuvent se référer
- Pas d'async
- variable c inutile puisque pas passé en paramètre, on pourrait retirer tout le code en rapport avec cette variable pour simplifier le code
- Simplifier au maximum les endpoint, faire des appels de fonctions aux nom explicite pour clarifier et simplifier le code pour tendre vers un endpoint comme le ```/session/signin``` et non pas comme le ```/session/signup```
- Status code de retour
### db.sql (10)
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
- pas de test
- pas de doc
- Pas de requête préparé

