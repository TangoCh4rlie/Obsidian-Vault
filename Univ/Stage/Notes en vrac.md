## Deux premiers jours

Découverte des locaux

Découverte de l’équipe

Installation (signature des quelques papier plus lecture de documents pour la découverte des méthodes de travail et de fonctionnement de l’entreprise)

Installation technique (client mail, outils de communication (teams), intelliJ…)

Découverte du projet sur lequel j’allais travaillé (Greg)

Explication plus en détail du projet global de l’Auxiliaire (Frédérique) pour comprendre le projet sur lequel j’allais travaillé, beaucoup de termes techniques car le corps de métier est très complexe.

Mardi matin, j’ai commencé la programmation de la librairie que je vais implémenter dans les autres projets Spring boot donc c’est super simple ça consiste à faire faire un builder pour construire un objet de Log pour par la suite l’envoyer dans une queue Azur. Le problème c’est que la qu’elle doit être généré sur le serveur de l’auxiliaire et comme on a pas les droits je suis bloqué pour l’instant et donc j’attends ça qui devrait arriver normalement demain, j’écris ça mercredi

Aujourd’hui j’ai bien discuté avec Camille, l’équipe est vraiment super sympa et c’est top de travailler avec des gens comme ça.

### Vendredi 19/04

La librairie java initialement prévu s’est transformer en un service SpringBoot, j’ai donc du réadapter mon code cette fin de semaine pour qu’il corresponde aux critères demandés. Aujourd’hui il devrait être prêt pour passer à la deuxième phase du projet.

Je m’entend de ieux en mieux avec l’équipe et c’est vraiment plaisant de pouvoir échanger avec des gens très calé qui peuvent toujours t’aider et qui te proposent des solution pour tes problèmes

Réflexion : Chat gpt ne sert à rien en entreprise pour résoudre les problèmes que tu as, voila :)

### Semaine du 22 au 26 avril

On à commencé la semaine par une réunion ou on présentait à la chef de projet (Frédérique) les avancés sur tous les projets (ogp, ogi, extranet…) j’ai donc moi aussi pu parle de l’avancé de mon projet. (finalisation de la création du service spriingboot et début de la création du programme de récupération des données de la queue azure)

Cette semaine j’ai bien avancé sur la récupréation des log et aujourd’hui (vendredi) je commence l’intégration de mon services aux autres api (c’est complex car il faut installer les projet etc…)

Cette semaine il y a eu un code2code qui était un quizz sur des question de code (c’était bien sympa) et la semaine dernière il y a eu un Axolab présenté par Antoine sur ChatGpt 3.5 qui était vraiment sympa

Jeudi soir comme cétait le dernier jeudi du mois il y à eu un after work avec une petite retrospective du mois dernier et puis il y a eu un apéro ou j’ai pu en profiter pour discuter avec plein de monde.

### Lundi 29/04
J'ai commencé l'intégration mais le truc c'est que je suis bloqué entre guillimet par ce que j'ai besoin de spécifications techniques a propos des éléments a log :( comme j'ai qu'un seul projet a faire et pas d'autres tickets je sais pas trop quoi faire la.

### Semaine du 29/04 au 10/05
J'ai continué l'intégration de ma librairie mais petit à petit on s'est redu compte qu'il y avait pleins de petits points qu'on pouvait améliorer dans la lib. Ducoup c'était repartit pour remettre les mains dans le moteur. Finalement à la fin de la semaine dernière j'avais intégrer la lib à 4 projets (quelques vérifications sont encore a faire mais j'avance bien).
![[Avancé_du_projet_10-05.png]]
L'intégration à pas été facile sur les premier projet car j'ai du comprendre le coeur de métier qui est vraiment complexe, mais petit à petit l'intégration va de plus en plus vite.

### Lundi 13/05
J'ai commencé à faire des MR pour les différents projet sur lesquels j'ai implémenté la lib.
J'ai commencé a faire des Dashboard sur kibana pour faire de la data visualisation. Ca va nous permettre de repérer rapidement des anomalies sur les applications comme un utilisateur qui récupère pleins de contrat d'autre client...
### Mercredi 15/05
J'ai encore fait des modifications sur la lib pour pouvoir gérer les cas problématique sur les GED. Je poursuit sur le déploiement en recette des applications.
![[Avancé_du_projet_15-05.png]]
### Jeudi et vendredi 16 et 17/05
Pendant ces deux jours j'ai fait le déploiement des deux première applications sur lesquelles j'avais implémenté ma librairie. Les deux applications sont l'extranet et opg-ged. Jeudi j'ai commencé avec ogp-ged. Le déploiement m'a pris toute l'après midi par ce que je devais merge ma branche passer toutes les pipelines et puis après il a fallut déployer l'application en recette ce qui à pris du temps par ce qu'il y a eu quelques petits problème de configuration des fichier pour kube. En plus lorsque l'application à été déployé dès la première requête qu'on a fait il y a eu une NPE (null pointer exception) et donc l'appli à crasher. On a du roll back la recette sur une version stable (la précédente) et j'ai fixé les problème dans mon code pour redéployer par la suite. Heureusement ça a marché dès le deuxième coup. C'était la première fois que je faisais un déploiement en recette donc c'était très intéressant. Je pense que les prochaines fois que je ferai ce genre de chose ça prendra moins de temps.
Normalement lundi prochain je devrai avoir un server elastic en recette sur lequel je vais pouvoir faire plus concrètement des test sur les valeurs que je reçois et que je dois traiter.

### Lundi à mercredi 20 a 22/05
Je continue le déploiement, on en est à 4 sur 7 dont 1 qui ne marche pas. Je pense que ca viens du fait que je n'utilise pas l'api management et comme c'est une application externe au réseau de l'Auxiliaire je ne peux pas accéder aux services du réseau local (donc ma queue azure). Sinon j'ai gérer des nouveaux problèmes que j'aurai pu causer avec ma lib. 
Mardi le elastic de recette production et dev a été mis en place et j'ai pu le configurer avec les droit d'accès pour les utilisateurs, ainsi que les lifecycles et les templates d'index
![[Avancé_du_projet_22-05.png]]
