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
