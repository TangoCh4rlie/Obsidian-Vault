`:%s/(truc a remplacer)/(par quoi))/` d pour toute la ligne

| Option          | Description                                            |
| --------------- | ------------------------------------------------------ |
| **G**           | Saut au début de la dernière ligne du fichier          |
| **gg**          | Passer au début du fichier                             |
| **]]**          | Déplace le curseur à la fin du fichier                 |
| **[[**          | Déplace le curseur au début du fichier                 |
| **G + A**       | Se rend à la fin du fichier et passe en mode insertion |
| **gg+A**        | Se rend au début du fichier et passe en mode insertion |
| **Ctrl + Home** | Affiche le haut du texte                               |
| **Ctrl+End**    | Affiche la fin du texte                                |
| **`:2`**        | Passe à la première ligne                              |
| **`:$`**        | Déplace le curseur à la fin du fichier                 |
| **2+G**         | Sauter au début du fichier                             |

`"+[number]+p` permet de coller un truc du regitre
`:reg` pour avoir la liste des éléments copiés
`q+[lettre]` enregistre les entrées clavier, pour pouvoir rejouter `[number]+@+[lettre]`
`v+%` pour aller d'un [ a un autre ]
`[relative_line_number]+j|k` pour aller a la ligne correspondante
`c|v+i|a+(|[|{` pour sélectionner ou modifier tout ce qu'il y a dans les parentèses ou ...
