Dans un premier temps, j'initialise ma scène avec une camera une scene et je défini la potition de cette camera

![[Pasted image 20250220105603.png]]

par la suite j'importe mes texture avec mon loader

![[Pasted image 20250220105638.png]]

Je crée un cylindre pour initialiser la base du moulin
![[Pasted image 20250220105713.png]]

Je crée les 4 pales de mon moulin avec les texures, je les positionnes au bon endroit
![[Pasted image 20250220105814.png]]

Donc a ce point la rien ne bouge et c'est moche mais ne vous en faites pas ca arrive :)
![[Pasted image 20250220105935.png]]

Je met les pales en animation pour qu'elles tournes
![[Pasted image 20250220110009.png]]

Je rajoute deux boutons pour le fun pour faire accélérer ou décélérer les pales
![[Pasted image 20250220110052.png]]

Maintenant mes pales tournes.

J'ajoute maintenant un sol pour que ma scène soit réaliste
Je met une texture d'eau
![[Pasted image 20250220110152.png]]

Je me suis aussi permis de rajouter de l'herbe et du ciel sur ma scène 

![[Pasted image 20250220110952.png]]

pour un rendu magnifique
![[Pasted image 20250220111015.png]]

je rajoute un petit toit a mon moulin :)
![[Pasted image 20250220111452.png]]
![[Pasted image 20250220111436.png]]

j'ai rajouté un petit easter egg, quand la vitesse des pales  est trop rapide alors la vitesse est telle que le moulin s'envole, je vous invite a essayer

![[Pasted image 20250220112507.png]]
![[Pasted image 20250220112527.png]]
vous pouvez bien sur cliquer sur reset pour revenir a l'était initial

j'ai rajouté des event listener sur les fleches du clavier pour pouvoir déplacer le moulin par ce que c'est cool en vrai
![[Pasted image 20250220114550.png]]
![[Pasted image 20250220114612.png]]

Pour résumer, voici les fonctionnalités que j'ai

- Objet / model : un moulin avec des pales
- Textures : un beau ciel, une belle herbe, une belle mer et des belles textures de moulin (on s'y croirait)
- Lumière : il y en a mais je n'arrive pas a les mettre en avant sur la scene pour qu'elle soit vraiment visible
- Animation : boutons pour accélérer les pales et pour décélérer, un bouton pour reset, si on accélère trop alors le moulin s'envole, si on utilise les flèches du clavier alors le moulin se déplace sur la scène.