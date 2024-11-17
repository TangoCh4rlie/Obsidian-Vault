# Piou Fight  
  
_Cette application est une plateforme permettant à des parrains de l'université de faire affront leur piou dans les duels divertissants._  
  
> Nous n'avons pas réussi à afficher le taux de coverage sur sonarqube mais nous avons bien mis en place les tests unitaires et d'intégration.  
  
## Fonctionnement global  
  
Sur la page d'accueil du site, vous pourrez trouver la liste des parties en cours ou en attentes de challenger.  
Vous aurez également la possibilité de créer une partie en cliquant sur le bouton "Créer une partie".  
  
Seuls les parrains peuvent rejoindre une partie avec leur piou et rejoindre des parties en tant qu'arbitre.  
  
## Installation  
  
Cette application est composée de trois parties. Une première avec le front-end (Vue-js), une seconde avec le back-end (SpringBoot) et une troisième avec la base de données (MySql).  
  
> Prerequis :  
> - Docker  
> - Git  
  
Commencez par cloner les deux projets sur votre machine avec les commandes suivantes puis lancez le projet avec le docker-compose :  
```bash  
mkdir piou-fight
cd piou-fight
git clone https://forge.univ-lyon1.fr/p2201709/projet-supersympa-ra3-qualite-dev.git
git clone https://forge.univ-lyon1.fr/p2201709/projet-supersympa-ra3-qualite-dev-front.git
cd projet-supersympa-ra3-qualite-dev
echo "flyway.url=jdbc:mysql://localhost/pioufight?useSSL=false&allowPublicKeyRetrieval=trueflyway.user=root  
flyway.password=root" > gradle.properties  
./gradlew bootJar
docker compose up -d
cd ../projet-supersympa-ra3-qualite-dev-front
npm install
npm run dev
```  
  
Rendez-vous sur http://localhost:5173 pour accéder à l'application.  

Pour exécuter les tests unitaires et d'intégration, vous pouvez utiliser la commande suivante :  
```bash  
./gradlew clean test
```
  
### Explications  
  
Il y a 5 utilisateurs différents :  
- host (mot de passe : host) : C'est le parrain qui crée la partie n°1 du tableau de la page d'accueil  
- hostpiou (mot de passe : hostpiou) : C'est le piou du parrain host  
- rival (mot de passe : rival) : C'est le parrain qui rejoint la partie n°1 du tableau de la page d'accueil  
- rivalpiou (mot de passe : rivalpiou) : C'est le piou du parrain rival  
- arbitre (mot de passe : arbitre) : C'est l'arbitre qui rejoint la partie n°1 du tableau de la page d'accueil  
  
La deuxième partie qui est en exemple est une partie où il ne manque qu'un challenger dans la partie pour qu'elle commence.  
Pour cela, il suffit de se connecter avec le parrain rival et cliquer sur "Rejoindre en tant que challenger".  
Ainsi, vous pourrez voir l'état de la partie changer et vous pourrez cliquer sur "Fini ?" pour rentrer le gagnant du challenge.


