1) Configuration des adresses IP de chaque machine, 
   ```sudo ifconfig eth0 <ip>``` puis ```sudo service network-manager stop``` pour faire en sorte que les ip ne changent pas toutes seules
2) Execution du programme pour établir une connexion entre les deux machines, ```./tp-TCP```
3) Capture de trames avec WireShark