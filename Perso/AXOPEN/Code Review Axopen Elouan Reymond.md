### database-connection.js
- mot de passe en clair
- pas de vérification des paramètres (possibilité d'injection sql)
- ne pas exporter la constante connection pour que d'autres parties de l'app aient un acces directe à la base de donnée. Simplement explorter authenticate qui se charge de toute la partie connection a la basse de donnée. De plus la constante connection n'est utilisé a aucun autre endroit dans le code
### helpers/chantier.js
### routes/chantier.js
### helpers/user.js

- Pas de requette préparé
### token-utils.js
### random-utils.js
### Index.js
- Variable plus explicite
- Chaine de char pas fou
- Pas d'async
### db.sql
- Char et pas varchar
### générales
- ne pas push le .env
- création de la base de donnée avec un orm pour avoir une meilleur adaptabilité et une meilleure réutilisabilité du projet

