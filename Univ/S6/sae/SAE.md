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
