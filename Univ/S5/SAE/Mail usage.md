*Voici l'utilisation de l'outil d'envoi de mail de l'ERP du groupe 3.*
### Prérequis
Avoir l'api de lancé ainsi que le front.
### Utilisation
Rendez vous [ici](http://localhost:4200/mail) pour accéder à la page de mail. Sur cette première vu vous aurez la possibilité de : 
	- Sélectionner un template de mail (si il y en a en base de données)
	- Modifier le template sélectionné
	- Envoyer un mail avec le template sélectionné
	- Rédiger un nouveau template

La modification d'un template est sensiblement la même interface que l'édition d'un nouveau template. Il vous sera possible d'insérer des éléments pré-fait tel que des titres, des sous-titres, des images et des liens.
Une fois le template modifié ou créé vous pourrez le sélectionner pour envoyer un mail avec ce template.
Il vous faudra sélectionner un expéditeur, un objet et remplir les valeurs dynamiques du template. Les cc et cci ne sont pas nécessaires.
Les valeurs dynamique du template se mettrons à jour toutes seules dans le rendu sur la droite.
Une fois le mail rédigé vous pouvez envoyer votre mail. Si vous envoyez un mail pour la première fois depuis le lancement de l'api à un expéditeur, il vous faudra attendre 60 seconde. Tant que vous n'êtes pas renvoyé sur la page /mail le mail n'a pas été envoyé.

### Techniquement
L'api se compose d'une 


