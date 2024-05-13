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
J'ai commencé à faire des MR pour les différents projet sur lesquels j'ai implémenté la lib