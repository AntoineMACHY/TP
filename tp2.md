# Tp2-linux

# TP2 : Manipulation de services

Le but de ce TP est de faire notre propre service, c'est pourquoi il se compose en 3 partie.  Nous allons d'abord apprendre a se servir d'un service dans les deux premieres parties puis en faire un en troisième partie.

Avant tout on change le nom de la machine avec la commande ```sudo hostname node1.tp2.linux```

<img src="Images/node.png" alt="photo"/>

On change le nom de la machine quand elle s'allume ```cd /etc``` et ```sudo nano hostname``` puis on écrit node1.tp2.linux

Enfin on vérifie le réseau (l'envoie et la réception de donnée) de notre VM :

```ping 1.1.1.1``` sur VM

<img src="Images/ping 1.1.1.1.png" alt="photo"/>

```ping ynov.com``` sur VM

<img src="Images/ping ynov.com.png" alt="photo"/>

```ping 192.168.56.140``` sur notre PC

<img src="Images/pingVM.png" alt="photo"/>

## Partie 1 : Installation et configuration d'un service SSH

1. On installe le pack "ssh" avec la commande```sudo apt install openssh-server```

2. On lance le serveur avec la commande ```sudo systemctl start sshd``` 

3. On vérifie qu'il soit bien actif avec la commande ```sudo systemctl status sshd```

<img src="Images/sudo systemctl status sshd.png" alt="photo"/>

On affiche le processus lié au service ssh avec la commande ```ps -e```

<img src="Images/ps -e.png" alt="photo"/>

On affiche le port utilisé par le service ssh avec ```sudo ss -lanpt```

<img src="Images/sudo ss -l -anpt.png" alt="photo"/>

On affiche les logs du service ssh avec la commande ```sudo journalctl -u ssh```

Pour se connecter au serveur ssh depuis notre PC, il faut taper la commande ```ssh toto@192.168.56.140```

4. On va modifier le fichier sshd_config pour cela on va faire ```cd /etc/ssh``` puis ```sudo nano sshd_config```. Ensuite on modifie son port d'écoute qui est abituellement 22 en 1060.

On vérifie que la modification a bien été sauvegardée avec la commande ```sudo cat sshd_config``` 

<img src="Images/cat du port.png" alt="photo"/>

On vérifie ensuite que la modification a bien été prise en compte avec la commande ```sudo ss -lanpt```

<img src="Images/sudo ss -l -anpt2.png" alt="photo"/>

On peut désormais redémarrer le service avec la commande ```sudo systemctl restart sshd```

Maitenant qu'on veut se connecter au nouveau port on doit faire : ```ssh -p 1060 192.168.56.168```

## Partie 2 : FTP

1. On installe le pack "vsftpd" avec la commande```sudo apt install vsftpd```

2. On lance le serveur avec la commande ```sudo systemctl start vsftpd``` 

3. On vérifie qu'il soit bien actif avec la commande ```sudo systemctl status vsftpd```

<img src="Images/staue de vsftpd.png" alt="photo"/>

On affiche le processus liés au service ssh avec la commande ```ps -e```

<img src="Images/ps -e de vsftpd.png" alt="photo"/>

On affiche le port utilisé par le service ssh avec ```sudo ss -lanpt```

<img src="Images/port 21.png" alt="photo"/>

On affiche les logs du service ssh avec la commande ```sudo journalctl -u vsftpd```

Pour ce connecter au serveur ftp on va dans le gestionnaire de fichier ---> On rentre ```ftp://192.168.56.140```

Pour uploader et telecharger un fichier de notre PC à la VM, on fait simplement un copier coller d'un fichier de notre PC au gestionnaire de fichier connecté à la VM et inversement.

Pour vérifier que cela a marché on fait ```ls``` dans le dossier où on a copier le fichier.

<img src="Images/ls -a de la photo.png" alt="photo"/>

Pour mettre en évidence les lignes de log du download et de l'upload il faut se rendre dans le dossier log avec ```cd /var/log``` puis afficher le fichier "vsftpd.log" ```sudo cat vsftpd.log```.

<img src="Images/copiecolle.png" alt="photo"/>

4. On va modifier le comportement du service. Il faut donc faire ```cd /etc``` puis ```sudo nano vsftp.conf``` pour rentrer dans le fichier. Ainsi on peut changer le port d'écoute de vsftpd qui est de base 22 en 1060 en ajoutant ```listen_port=1060```. Puis pour vérifier qu'il soit bien sauvegardé on fait ```sudo cat vsftpd.conf```

<img src="Images/listen_port-1060.png" alt="photo"/>

Ainsi on voit si ces modifications ont pris effet grâce à la commande ```sudo ss -lanpt```.

<img src="Images/portvsftpd1060.png" alt="photo"/>

On peut désormé redémarrer le service à l'aide de la commande ```sudo systemctl restart vsftpd```.

Pour se connecter au serveur ftp on va dans le gestionnaire de fichier ---> On rentre ```ftp://192.168.56.140:1060/```.

On peut donc réutiliser la même méthode dit prècedemment pour upload et download un fichier. (copier coller dans le gestionnaire de fichier)

## Parti 3 : Création de votre propre service

1. On installe le pack "netcat" avec la commande```sudo apt-get install netcat```.

Les deux commandes pour faire un chat avec "netcat" sont : ```nc -l -p 2000``` et ```nc 192.168.56.142 2000```.

<img src="Images/nc.png" alt="photo"/>

Suite à cela, on essaie de stocker notre discussion dans un fichier texte appellé "test.txt". A l'aide de la commande ```touch test.txt``` on crée le fichier. Puis pour lui faire stocker les données échangées on fait ```nc -l -p 2000 >> test.txt``` et ```nc 192.168.56.142 2000 >> test.txt```. Pour vérifier cela suite à un échange on va afficher les données stockées par le fichier texte ```cat test.txt```.

<img src="Images/test.png" alt="photo"/>

2. On va créer un fichier appelé "chat_tp2.service" dans /etc/systemd/system avec les commandes ```cd /etc/systemd/system``` puis ```sudo touch chat_tp2.service```.

<img src="Images/sudo touch service.png" alt="photo"/>

Ensuite on lui donne les mêmes permissions que les autres services, c'est à dire le droit d'y écrire, de le lire et de l'exécuter avec la commande ```sudo chmod 777 chat_tp2.service```.

Puis on y dépose le contenu suivant : 

<img src="Images/danservice.png" alt="photo"/>

Ainsi on peut exécuter la commande ```sudo systemctl daemon-reload```

3. A présent nous devons tester le service que nous avons créé. 

On démarre le service avec la commande ```sudo systemctl start chat_tp2``` puis on vérifie qu'il soit correctement lancé avec la commande ```sudo systemctl status chat_tp2```.

<img src="Images/statuschat.png" alt="photo"/>

On vérifie le port via la commande ```sudo ss -lanpt```

<img src="Images/sschat.png" alt="photo"/>

Ainsi on se connecte avec la commande ```nc 192.168.56.142 2000```depuis un terminal qu'on nomme "terminal B". Puis pour voir les données envoyées en temps réel par le "terminal B", on va voir nos logs grâce à la commande ```journalctl -xe -u chat_tp2 -f```

<img src="Images/lognc.png" alt="photo"/>