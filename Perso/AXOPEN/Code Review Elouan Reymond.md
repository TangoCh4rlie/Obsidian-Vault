# Code Review NodeJs Express

Voici le compte rendu de la revue de code que j'ai fais sur le projet [node.js](https://github.com/AxopenLyon/candidature-nodejs).

## Sommaire
#### [database-connection.js](#####database-connection) 3 remarques
#### [helpers/chantier.js](#####helpers/chantier.js) 7 remarques
#### [routes/chantier.js](#####routes/chantier.js) 4 remarques
#### [helpers/user.js](#####helpers/user.js) 4 remarques
#### [token-utils.js](#####token-utils.js) 5 remarques
#### [random-utils.js](#####random-utils.js) 2 remarques
#### [index.js](#####index.js) 6 remarques
#### [db.sql](#####db.sql) 10 remarques
#### [générales](##### générales)

<br/>

##### database-connection.js

- Les identifiants de la basse de donnée dont le mot de passe sont en clair dans le code ce qui n'est pas une bonne pratique. En effet le mot de passe devrait se trouver dans le fichier .env pour qu'il ne soit pas push sur GitHub.
- Dans la fonction query les paramètres passés ne sont pas vérifiés, ainsi un acteur malveillant pourrait injecter du code pour pouvoir récupérer des données sensibles de la base de donnée (surtout que dans le cas de ce projet le mot de passe n'est pas hasher dans la base de donnée).
- Je pense qu'exporter la constante ```connection``` n'est pas une bonne pratique. En effet, je pense qu'il serait préférable de seulement exporter  ```authenticate``` et  ```query``` puisque  ```connection``` n'est jamais réutilisé autre part dans le projet. De plus, je pense qu'il est préférable qu'une seule fonction avec des vérification et des gestions d'erreur puisse établir une connexion à la base de donnée.

##### helpers/chantier.js

- Dans ``findChantier`` on pourrait modifier la requête SQL par  ```SELECT * FROM chantier where numero = ?``` avec en paramètre de la fonction le numéro du chantier que l'on souhaite rechercher. Il n'y aura jamais deux chantier avec le même numéro puisque c'est la clef primaire de la table chantier et que la valeur est auto-incrémenté à chaque nouvelles lignes inséré. Le résultat sera donc toujours mono ligne. De plus, utiliser cette méthode est plus optimiser car elle permet de ne pas récupéré toute la table à chaque requetés pour seulement après effectuer le traitement dessus. (Bonus : on pourrait remplacer l' * par les champs qui nous intéressent vraiment pour être encore plus optimisé).
- Il semble que dans ``findChantier`` la gestion d'erreur ai été oublié. On devrait rajouter ```throw new PersonnalError('Error when querying', e);```.
- Toujours dans ``findChantier``, il y a un paramètre inutile que l'on peut supprimer
- Dans le ``updateChantier`` la concaténation d'un chaine de caractères comme dans la fonction pourrait mener à une injection sql. En effet, il serait préférable d'utiliser la syntaxe avec les ? qui permet une vérification des valeurs.
- Le nom de la fonction ``putRandomChantier`` n'est pas très conventionnel puisque cette fonction sert à insérer des éléments dans la table. Pour une méthode de peuplement dans ce genre on devrai utiliser le nom ``createRandomChantier``.
- Pour la fonction ``putRandomChantier`` il serait préférable de passer les valeurs en paramètre au lieux de devoir à chaque fois modifier les valeurs dans le fichier à la main.
- Les fonctions de ce fichier ne vérifient pas si l'utilisateur qui exécute ces requêtes possède les droits pour effectuer ces action. Pour cela, on aurait pu utiliser les méthodes créé dans le fichier ``token-utils.js`` pour vérifier si l'utilisateur est bien connecté et si son token jwt est encore valable.

##### routes/chantier.js

- Le contenu saisit par l'utilisateur n'est jamais vérifier pour voir s'il correspond au format attendu, cela pourrait permettre me prévenir d'attaques par injection SQL ou bien tout simplement de vérifier l'intégrité des données.
- La gestion des codes de retour renvoyé en cas d'erreur n'est pas fait correctement. En effet, il n'es pas très utile de retourner un code d'erreur 500 puisque il n'indique presque rien au programmeur utilisant l'API. Si les codes retournés faisaient référence à une erreur précise le développeur serait plus apte à résoudre les problèmes. C'est aussi un gain de temps précieux lorsqu'on utilise une api.
- Il serait préférable d'utiliser un **PUT** à la place du **POST** pour la mise à jour d'un chantier puisque POST est conventionnellement utilisé pour ajouter une des données dans une base de donnée.
- Idem pour l'endpoint ``/delete/:numero`` il serait plus logique de faire un delete à la place d'un get puisque la fonction est de supprimer un chantier

##### helpers/user.js

- Le mot de passe n'est pas hashé avant d'être inséré dans la base de donnée ce qui n'est vraiment pas sécurisé puisque le mot de passe est en clair. Il faudrait par exemple utiliser un algorithme de chiffrement tel que SHA256 avant de stocker le mot de passe.
- La gestion d'erreur n'est pas présente, il est donc plus difficile de débugger le code.
- On pourrait utiliser un égale au lieux du ``like`` puisque l'on connais le contenu des chaines que l'on va comparer. Cela permettrait de minimiser les risques de résultats inattendu.
- Je pense que le Promise de ``findIncludeUser`` et de ``createUser`` n'est pas nécessaire dans ce cas puisque la fonction query retourne déjà une promesse.

##### token-utils.js

- Le temps d'expiration du token est beaucoup trop long, il serait préférable de faire une méthode ``refreshToken`` pour permettre de fournir un nouveau token lorsque l'ancien est expiré. Le problème ici est que si le token est volé alors il pourra être utilisé pour une longue durée.
- Pas de gestion d'erreur donc toujours difficile à débugger.
- Dans le cas de ``createToken`` il serait préférable de créer une copie de l'objet user pour après pourvoir effectuer des modification et non pas sur l'objet passé en paramètre et qui est retourné en fin de fonction
- Certaines méthodes comme ``connectedUser``, ``extractToken`` et ``verifyAndExtractToken`` ne sont jamais appelés dans le projet. Ces fonctions sont donc inutiles et elles complexifient le code.
- L'algorithme de chiffrement HS256 est basé seulement sur une clef secrète, si celle ci venait à leak ou est volé alors la sécurité est mise en jeu. On pourrait se baser sur un algo de chiffrement avec un système de clé publique/privés. 

##### random-utils.js

- Les noms de variable ne sont pas très explicite, ce qui ne facilite pas la compréhension du code.
- On pourrait utiliser une autre façon pour générer une chaine de caractère d'une longueur donnée.

##### index.js

- Les noms de variable ne sont pas très explicite, ce qui ne facilite pas la compréhension du code.
- Il y a cette chaine de caractère qui est réutiliser à plusieurs endroit dans le code. L'utilisation d'une librairie est possible ou bien stocker une seule fois dans un fichier à part cette chaine. Tous les fichiers souhaitant utiliser cette chaine n'auraient qu'a l'importer.
- L'endpoint ``/session/signup`` n'est pas en ``async`` ce qui peut être bloquant.
- La variable c dans ``/session/signup`` est inutile puisqu'elle n'est jamais transmise à aucune fonction (elle transmise mais la fonction ``createUser`` n'utilise pas cette variable). Le code est donc complexifié et cela n'apporte rien.
- On pourrait simplifier un maximum les endpoints pour qu'il n'y ai que des appels à des fonction ce qui permettrai de simplifier et de rendre le code plus lisible pour un programmeur arrivant sur le projet.
- Les codes de retour ne sont pas explicite (seulement des 500). Il faudrait faire une gestion d'erreur avec différents code de retour en fonction des erreurs retournés. L'erreur 500 indique seulement une erreur coté serveur mais n'apporte aucune précision sur la nature de celle ci. Alors que 

##### db.sql

- 