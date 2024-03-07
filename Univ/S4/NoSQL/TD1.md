movies: 
- _id
- title
- genres
users:
- id
- name
- gender
- age
- occupation
- movies (movieid, rating, timestamp)

### Correction TD1

db.movies.distinct("genre")
db.users.find({}, {"_id": 0, "name": 1, "occupation": 1})
db.users.find({}, {"_id": 0, "name": 1, "movies.movieid": 1})
**Permet de faire de chercher un atribut dans une collection**

### TD2/3
``
db.movielens_movies.find({"genres": {$eq: "Animation"}}, {"_id": 0, "title": 1}))
db.movielens_users.find({"occupation": {$eq: "academic/educator"}}, {"_id": 0, "name": 1})
db.movielens_users.find({"movies.rating": {$gte:4}}, {"_id": 0, "movies.movieid": 1})
db.movielens_users.find({"movies.movieid": {$eq:2455}, {"_id": 0, "name": 1}})
db.movielens_movies.find({$or: [{"genres": {$ne: "Comedy"}},{"genres": {$ne: "Adventure"}}]}) 
**db.movielens_movies.find({"genres": {$nin: ["Comedy", "Adventure"]}}, {"_id": 0, "title": 1})** 
db.movielens_users.find({"age": {$lte: 16}}, {movies: 0}, {"_id": 0, "name": 1})
db.movielens_users.find({"age": {$gte: 30}}, {movies: 0}, {"_id": 0, "name": 1})
``

### TD4
``
db.movielens_movies.find({$or: [{"genres": {$eq: "Comedy"}},{"genres": {$eq: "Adventure"}}]})
db.movielens_users.find({$and: [{"age": {$gt: 20}}, {"gender": {$eq: "M"}}]}, {"_id": 0, "name": 1})
db.movielens_users.find({$and: [{"movies.movieid": {$eq: 2455}}, {"age": {$gt: 30}}]}, {"_id": 0, "name": 1})
db.movielens_users.find({"movies.movieid" {$eq: [260, 1196, 1210]}}, {"_id": 0, "name": 1})
db.movielens_users.find({"movies.movieid" {$eq: [260, 1196, 1210]}}, {"_id": 0, "name": 1})
``

### TD5

``
db.movielens_users.aggregate([{$group: {_id:"_id", nbutilisateurs:{$count:{}}}}])
db.movielens_movies.aggregate([{$group:{_id:"_id", nbfilms:{$count:{}}}}])
db.movielens_users.aggregate([{$group: {_id:null, "maxage":{$max:"$age"}}}])
db.movielens_users.aggregate([{$group: {_id:null, "age":{$avg:"$age"}}}])
``

### TD6

``
db.movielens_users.aggregate([{$match: {"gender":"F"}},{$group:{_id:"_id", nbF:{$count:{}}}}]])
``

## TP1
``
db.personne.find({}, {"_id": 1, "full_name": 1})
db.personne.find({"personnal_adress.city":{$eq:'Selma'}}, {"_id": 0, "full_name": 1})
db.personne.find({$and: [{'personal_address.city': {$eq: 'Trenton'}}, {'cv.positions.company_name': {$eq: 'Towers Watson'}}]}, {"_id": 0, "full_name": 1})
db.personne.aggregate([{$group:{_id:null,nbpers:{$count:{}}}}])
db.personne.aggregate([{$group:{_id:'_id',name:{$last:"$full_name"},agemax:{$max:"$age"}}, {$project:{"_id":0}}}])
ne sert a rien au dessus
db.personne.aggregate([{$match:{"personal_address.city":{$eq: "Ballard"}}},{$group:{_id:"_id",nbpers:{$count:{}}}}])
db.personne.aggregate([{$group:{_id:"$age", nbconscrit:{$count:{}}}}])
db.personne.aggregate([{$unwind:"$contact_pro"},{$group:{_id:"$_id",nbadr:{$count:{}}}}])
db.personne.aggregate([{$unwind:"$cv"}, {$unwind:"$cv.positions"}, {$group:{_id:"$cv.positions.company_name", nbcol:{$count:{}}}}])
``
