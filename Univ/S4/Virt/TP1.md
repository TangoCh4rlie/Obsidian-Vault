commandes utiles

- créer un nouveau name space avec seulement le mount de différent:
`sudo unshare --fork --mount bash`

de base si on ajoute pas de params les 8 namespace sont les mêmes

- monter le dossier folder dans toto
`sudo mount --bind folder toto`

Résultat de la commande (dans le namespace actuel) le contenu de folder est visible dans le dossier toto mais ce n'est pas le cas pour le namespace "père" qui n'est pas affecté par les modifications

- Spécification de --mount-proc
si ya pas ce param le dossier /proc est le meme pour les deux name space donc ps affichera les memes numéro que le shell de base
en revanche si ya le param le dossier /proc n'est plus le même que le name space de base et donc il n'y aura que les numéro des process du nouveau name space avec les "bon" numéro (1, 8...) (avec les numéro théorique des process du nouveau namespace)


### exo3

- créer un dossier
- créer 3 sous-dosser (bin, lib, lib64)
- mettre /bin/bash /bin/ls /bin/pwd /bin/ps dans notre fichier bin/
(ldd bin/bash) pour avoir les différentes librairies
- copier les lib dans le dossier lib/
- sudo chroot ./ bash
