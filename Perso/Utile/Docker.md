`docker init` pour set up un docker directement dans un projet déjà existant

on pleut lancer des [application graphiques](https://www.youtube.com/watch?v=PUpgGtq0xSw) depuis un docker

`docker compose watch` pour auto refresh quand ya des modifs

`docker scout quickview` pour vérifier si une image contient des vulnérabilités

`build docker cloud` 

# [Podman](podman)
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

### Rerun un docker de la liste docker ps -a 
``docker start -i <name>``

Dans un fichier d'env on peut dire  ``host.containers.internal:9200`` pour pointer vers le port 9200


