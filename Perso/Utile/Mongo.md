Pour faire un sort en reverse il faut mettre une -1
Il est possible de faire des regex pour matcher sur des strings
`db.restaurant.find({"address": {$regex: "Park Avenue"}}, {_id: 0,name: 1, type_of_food: 1}).sort({"type_of_food": -1}).pretty()`


on peut utiliser le $jsonSchema pour vérifier la structure la structure d'un document par exemple dans un find ou un aggregate


Au moment de la conception de la base de donnée il faut utiliser une approche Query-driven (concevoir la structure de la bd en fonction des cas d'utilisation, il faut définir des "wrokflows" pour définir les use cases)

définir 
- le scanario
- la nature des données traités (big data, données en temps réel, données analytiques)
- nature des accès  (read/write, taille, fréquence)
- contraintes métier