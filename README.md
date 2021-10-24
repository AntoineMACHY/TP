# TP1-linux

## TP1 : Are you dead yet ?

Nous allons voir différentes manières pour détruire une machine Linux/GNU.

1. ```sudo rm -r --no-preserve-root /``` Cette commande permet de supprimer tout les fichiers depuis la racine de façons récursives.

2. ```sudo dd if=/dev/zero of=/dev/sda``` Cette commande permet de remplacer tout les bits du disque dur par des 0, cela a pour effet de formater petit a petit le disque dur. Il est possible de stopper le processus avec ```Control + c```. Neanmoins si une partie importante est "touché" la machine devient completement inutilisable.

3. ```sudo chmod -R 000 /``` Cette commande retire absolument tout les droit à tout le monde. Sans droit la machine est totalement inutile.

4. Ceci n'est pas une commande. Mais reste efficace, cela consiste a télécharger une images, lourde de préférence et de la copier plusieurs milliers de fois. La machine ralentira et au redemmarage ne sera plus du tout fonctionelle. 

5. ```sudo cp -R / /*``` Cette commande créee un second dossier racine et par la meme occasion des incohérence dans les fichiers système.

6. ```sudo mv / /*``` Renomme le fichier racine et cause des problèmes dans l'adresse des fichiers.

