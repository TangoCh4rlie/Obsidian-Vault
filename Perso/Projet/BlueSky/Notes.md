J'ai fait tourner le programme 2 heure environ et j'ai des fichier de 300 000 utilisateur, je vais essayer de le faire tourner sur un kube pour qu'il puisse en récupérer plus.

Le script avait fait 13 000 appel API et avait traité 2847 utilisateur ce qui est vraiment peu.
Je pense qu'il n'y aura pas de problème au niveau des restrictions de call API qui sont limité au nombre de 35 000 par heure par IP.


UPDATE 26/01/2025

J'ai plusieurs difficultés :
- Le temps de récupération des 25 000 000 utilisateur est vraiment long mais avec des techniques de treading et de scaling vertical je pense que ce n'est pas un facteur limitant
- Le volume de données récupérer, 20 Mo pour seulement 1000 utilisateurs traités soit théoriquement 500 000 Mo pour tous les utilisateur. Une solutions serait de fragmenter ce gros fichier pour qu'il soit plus simple de le manipuler pour le traitement.
- Je ne peux pas en vu de la durée et de l'espace de stockage théorique demandé faire tourner ca sur ma machine. Il va falloir louer des serveurs.
- Si je souhaite plus tard faire des représentations du réseau il me faudra louer des machines.

500 Go sur CloudFlare r2 ca coute 7,5 euro



