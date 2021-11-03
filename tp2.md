# Tp2-linux

# TP2 : Manipulation de services

Le but de ce TP est de faire notre propre service, c'est pourquoi il ce compose en 3 partie. C'est a dire qu'on va d'abord apprendre a se servir d'un service dans les deux premieres parties puis en faire un en troisième partie.

Avant tous on change le nom de la machine avec la commande ```sudo hostname node1.tp2.linux```

<img src="Images/node.png" alt="photo"/>

On change le nom de la machine quand elle s'allume ```cd /etc``` et ```sudo nano hostname``` puis on écrit node1.tp2.linux

Enfin on vérifie le réseau (l'envoie et la réception de donnée) de notre VM :

```ping 1.1.1.1``` sur VM

<img src="Images/ping 1.1.1.1.png" alt="photo"/>

```ping ynov.com``` sur VM

<img src="Images/ping ynov.com.png" alt="photo"/>

```ping 192.168.56.140``` Sur notre PC

<img src="Images/pingVM.png" alt="photo"/>

Partie 1 : Installation et configuration d'un service SSH

1. On installe le paquet avec la commande```sudo apt install openssh-server```

2. On lance le serveur avec la commande ```sudo systemctl start sshd``` 

3. On vérifie qu'il soit bien actif avec la commande ```sudo systemctl status sshd```

<img src="Images/sudo systemctl status sshd.png" alt="photo"/>
