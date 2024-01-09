```
docker build . --tag node_app 
```
Permet à partir d'un Dockerfile de faire une image docker *mais elle n'est pas executé*
```
docker run -it -p 4000:4000 node_app
```
Permet de **run**  une image docker avec le port qui est précisé

La syntaxe 1000:4000 signifie que 1000 sera le port sur la machine physique et 4000 le port sur le docker

`docker-composer up -d`
Permet à partir d'un docker-compose.yml de lancer plusieurs image a la fois
