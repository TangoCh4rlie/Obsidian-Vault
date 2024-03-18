db.personne.updateOne({"full_name": {$eq:"Adalbéron Simon"}}, {$inc:{}})

db.personne.updateOne({"full_name":{$eq:"Aloyes Andre"}}, {$assToSet:{"cv.0.positions": {""job_title": "Comsultant BI"}}})

db.personne.updateMany({}, {$set:{"nombr_postes":0}})
