# ssh
`ssh-keygen -t <methode>`
ajouter la clef ssh à la liste
`eval "$(ssh-agent -s)"`
`ssh-add ~/.ssh/<nom_fichier>`
copier la clef publique sur un ordinateur distant
`ssh-copy-id <username>@<ip address>`

Si un host à la meme adresse ip mais que c'est pas la meme machine alors 
`ssh-keygen -f "/home/tangocharlie/.ssh/known_hosts" -R "<ip>"`
# scp
copier de manière sécuriser un fichier sur un ordinateur distant, il faut que ce dernier ai openssh
`scp myfile.txt pi@192.168.1.3:project/`