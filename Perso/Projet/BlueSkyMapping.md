---

excalidraw-plugin: parsed
tags: [excalidraw]

---
==⚠  Switch to EXCALIDRAW VIEW in the MORE OPTIONS menu of this document. ⚠== You can decompress Drawing data with the command palette: 'Decompress current Excalidraw file'. For more info check in plugin settings under 'Saving'


# Excalidraw Data
## Text Elements
taille en fonction du nombre de lien qui partent du node ^UTrUmyZW

Node = user
Edge = relation (follow) ^ZGCt9NQZ

Dans un premier temps pas de différentiation entre follow et followers ^inReSodS

couleur en fonction du topic traité par le compte 
(je sais pas encore comment faire pour déterminer ca) ^jWbWgGKq

Liste de nodes ^1jCmka3B

Id
user 1
user 2
user 3
user 4
user 5
user 6 ^SV1uAk5h

Liste de follow ^XTaBXaxk

Source,Target
user 1,user 2
user 1,user 3 ^HSzAC4mC

Liste de followers ^BohWuOWb

Source,Target
user 3,user 2
user 4,user 3 ^CxeyGUUG

hashMap followers
hashMap follow
liste userTraité

tant que queue est pas vide    
    fait un appel
    récupère la liste des follow
    les mets dans un queue
    prend le premier de la liste
    vérifie qu'il a pas été checké
    récupère follow et followers dans une hash map follow et follwers
    rajoute le user dans la liste des utilisateur traités
    
format les données de sommet (liste des user traité) en .csv
format les données d'arete (follower) en .csv
format les données d'arete (follow) en .csv

     ^Pyx1WI41

pour n utilisateur ^jESJ9gTu

Pourquoi pas trier la liste 
pour faciliter la recherche ^Er43vqVN

100 000 / 100 = 1 000 ^37QyHsUS

%%
## Drawing
```compressed-json
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

4jfagqM6rzBAA===
```
%%