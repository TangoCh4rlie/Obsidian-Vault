2025-03-24
[[univ]]

------------------------------------------------------------------------
[[Univ/S6/sae/Schemas|Schemas]]
Liste des formations 
- [x] INFORMATIQUE

Parcours
- [ ] avoir une notion de volume horaire par parcours
- [x] RA
- [x] AGED
- [x] DACS

Année / Semestre
- [x] 3 années avec 2 semestre dans chaque année


### Prévoir le changement automatique d'années des étudiant ainsi que du statut
- [ ] avoir un bouton pour passer  d'une année a l'autre (api: OK)
- [x] pouvoir supprimer des utilisateurs si il ne sont plus a l'université
- [ ] sélectionner les étudiants a ne pas faire monter (redoubler)

- faire un import a partir d'un fichier CSV avec le P et les groupe/année/parcours

- [x] pouvoir modifier ls informations classe / année / parcours

### Prévoir l'affichage des ressources par parcours / semestre
- [ ] ajouter / supprimer une ressource

Ressources / SAE
- [ ] clé primaire avec l'année / parcours / semestre / formation
- [ ] volume horaire de TP / TD / CM par ressources
- [ ] affectation d'enseignant
- [ ] lien tomuss
- [ ] description
- [ ] Affichage des ressources en manque d'enseignants


Enseignants :
- [ ] Affichage des modules affectés et nombres d'heures
- [ ] Validation ou refus des resources à enseigner

Vue admin / responsable :
- [ ] Liste des enseignants avec leur charge horaire
- [ ] Gestion des heures totales enseignées


------------------------------------------------------------------------

### Prio 2

FACILE:
- [ ] Calcul du nombre d'heures par semaine par groupe
- [ ] Calcul du nombre d'heure par semaine par enseignant

RELOU:
- [ ] Distribution des heures par semaine dans le semestre
- [ ] Affichage des N semaines
- [ ] Modification par modules des heures dans le semestre par groupe et alternance
- [ ] Export calendrier


#### Gasel??
Comment faire

sous la forme d'un récapitulatif
enseignant il a fait quoi? quelles sont les heures qui ont été fait par le prof (sur chaque module combien de TD CM TP... et par parcours)



### Questions
- [x] Import/Export des parcours et semestres (en quoi ça consiste)
- [ ] Gestion nombre de groupes par formation de l'année
- [ ] Ajout logiciels nécessaire pour le module
- [x] Extraction de syllabus avec la description et données de la ressource
- [x] Affichage des heures EDT VS modules prévus
- [x] Gasel
- [x] Ajout d'heures allouées en enseignement et HRS
- [ ] comme gerer le cas des premières années qui n'ont pas de parcours? un parcours TC (tronc commun)

Bonjour,

Je me permets de vous envoyer un mail à propos de la SAE. J'ai quelques questions à propos du module sur lequel je vais travailler ce semestre. J'ai repris point par point le tableau Excel que vous nous avez fourni pour le module "Formation".

- "Import/Export des parcours et semestres" : Si je comprends bien, c'est avoir la possibilité d'importer un semestre, une année ou un parcours ? Est-ce qu'il ne serait pas plus pertinent de pouvoir importer des ressources qui seront par la suite rattaché à des années / semestres / parcours ?
- "Extraction de syllabus avec la description et données de la ressource" : Qu'est-ce qu'est syllabus et qu'elles sont les interactions que vous souhaitez avoir ?
- "Affichage des heures EDT VS modules prévus" : Je ne comprends pas bien ce que vous voulez comparer. Est ce que le but est de voir les incohérences entre l'emploi du temps et les horaires assigner au professeur ?
- A propos de toute la partie GASEL : Est ce que nous avons des accès pour pouvoir comprendre plus précisément l'outil ? Quels sont les moyens de communications avec cette application (api, documentation...)? Je n'ai pas réussi à me connecter sur https://gasel.univ-lyon1.fr/
- "Ajout d'heures allouées en enseignement et HRS" : Que signifie HRS et quels sont les tâches précises à réaliser, je ne suis pas sur de bien comprendre.

Cordialement,
Elouan Reymond











Dans le cadre d'un travail de cours, j'ai du reprendre un projet existant d'un étudiant pour l'améliorer et développer des nouvelles fonctionnalités
Pour le contexte le site est un ERP qui permet la gestion d'une école, j'ai travaillé sur la partie ressource c'est a dire : les enseignants, élèves, les modules de cours, la gestion du nombre d'heure et des affectations de professeurs...

Voici le contenu du rapport qui à été rédigé par les ancien étudiant :

III.7 - Gestion des ressources
Membres en charge : Lomé BORDES, Abd-El-Rahmen GHERIBI, Camille MORFIN, Baptiste TRICOT
III.7.A - Description générale du module
Le module de gestion des ressources ne concerne pas directement les étudiants, mais les enseignants et le personnel administratif.
Il s’agit de la mise en place et de l’affectation des ressources, les matières correspondant aux programmes pédagogiques nationaux. Le but de ce module est de donner un accès simplifié à toutes les ressources enseignées et de permettre l’affectation et le suivi des enseignants directement depuis l’ERP.
III.7.B - Acteurs et utilisateurs
La gestion des ressources académiques et enseignantes passe par l’action des acteurs suivants :
Les enseignants : permanents ou vacataires, ils sont affectés à une ressource en fonction de leurs compétences et indiquent leurs disponibilités pour pouvoir mettre en place l’emploi du temps.
Le personnel administratif : tout personnel dont le rôle est de créer les ressources à partir des sources officielles, ainsi que de vérifier l’équité dans l’affectation des heures d’enseignement et l’effectivité de celles-ci (administrateur, responsable de formation…).
III.7.C - Fonctionnalités attendues
Il est prévu pour le module de gestion des ressources de comporter les fonctionnalités suivantes :
Notification des modifications
Notifier les enseignants pour toute nouvelle affectation et modification liée à leurs enseignements.
Élaboration de statistiques
Élaborer des statistiques sur la répartition des cours et des heures par type de cours et par formation pour aider à la planification future.
III.7.D - Fonctionnalités développées
Les fonctionnalités suivantes ont pu être développées :
Ajouter des maquettes
Ajouter les maquettes définissant les ressources annuelles par type et année de formation.











Affichage des ressources
Afficher la liste de toutes les ressources avec leur description (intitulé, description, code Apogée, heures par type de cours, semestre, compétences concernées…).
Génération d’un récapitulatif personnel
Générer un récapitulatif dédié aux enseignants indiquant leurs heures d’enseignement par module ainsi que les groupes auxquels ils enseignent.
Génération d’un récapitulatif global
Générer un récapitulatif annuel global, dédié au personnel administratif, des heures d’enseignement par enseignant avec un affichage résumé et un affichage détaillé (groupe, année, formation, module, type de cours…).

Affectation des enseignants
Affecter les enseignants aux cours et sous-cours (TP / TD / CM / PE) en fonction de leurs disponibilités et de leurs compétences.
Validation des heures d’enseignement
Valider ou non les heures effectives d’un enseignant (heures d’enseignement bel et bien dispensées par rapport au nombre prévu) pour les envoyer à l’application GASEL afin de déclencher son paiement.
Synchronisation des données
Synchroniser les données avec le module de gestion d’emploi du temps pour garantir la répartition et la cohérence des heures d’enseignement.
Suivi des charges horaires
Suivre la charge horaire de chaque enseignant pour assurer une répartition des heures équitable et identifier les manques ou surcharges potentielles.
III.7.E - Scénarios
Diagramme de séquence modélisant les échanges lors de l’affectation d’un enseignant :


rajoute a la suitede ce rapport en reprennant le style rédactionnel une nouvelle partie intitulé : Evolution réalisé pendant le S6

Voici les réalisation que je tu veux que tu parle: 

- J'ai rajouté des barres de recherche pour filtrer les modules affiché, j'ai aussi limité le nombre de modules affiché pour augmenter les performances
- J'ai amélioré la page d'affectaction de professeur à un module (rajout de barre de recherche pour rechercher les modules et les professeurs)
- J'ai rajouté une nouvelle page pour permettre au chef de département de pouvoir administrer les élèves. Edition de l'étudiant, changement de semestre, changement d'année, suppression d'un étudiant de la base de donnée...
- J'ai rajouté une nouvelle page pour permettre de visualiser l'ensemble des modules ainsi que le nombre d'heure dans chaque matière et le prof. Le but a terme de cette page est de répondre parfaitement aux besoin exprimé par les professeur pour pouvoir visualiser les cours ou il n'y a pas de prof, voir si des profs ne font pas assez d'heure...