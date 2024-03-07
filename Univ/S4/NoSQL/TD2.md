### TD2

db.users.updateOne({"name":{$eq:"Yaeko Hassan"}}, {$inc:{"age":-1}})


modifie selement la ligne 2
db.users.updateOne({"name":{$eq:"Yaeko Hassan"}}, {$inc:{"movies.1.rating":-1}})

modifie toutes les lignes du tab
db.users.updateOne({"name":{$eq:"Yaeko Hassan"}}, {$inc:{"movies.$[].rating":-1}})
