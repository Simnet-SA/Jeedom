Largement basé sur le repository Jeedom/core

Déploiment d'un conteneur Jeedom complet (serveur Apache, php5, mysql). 

# Jeedom  #

Website (English): [https://jeedom.com/site/en/](https://jeedom.com/site/en/)

Website (French):  [https://jeedom.com/site/](https://jeedom.com/site/)

# Installation #

## Pre-requis ##

Une machine host avec Docker installé (testé uniquement sur Debian pour le moment)

## Procédure ##

Accéder à la machine host en SSH et naviguer vers un répertoire dédié à l'installation.
Télécharger les fichiers d'installation avec git clone.
Se déplacer dans le répertoire récupéré :
<code>cd core</code>

S'assurer que le démon Docker tourne.

Construire l'image avec la commande : 
<code>docker build -t $IMG_NAME .</code>

Remplacer $IMG_NAME par le nom que vous voulez donner à l'image. Ne pas oublier le "." à la fin de la commande pour que Docker charge le Dockerfile

Démarrer le conteneur :
<code>Docker run --name $CONT_NAME -d -p 80:80 -p 80:80 $IMG_NAME</code>

Remplacer $CONT_NAME par le nom que vous voulez donner à votre conteneur.

Entrer dans un navigateur l'IP de la machine hôte. Un écran vous demande le mot de passe root de la BDD. une fois renseigné, cliquer sur "proceed", puis accéder à l'écran de login Jeedom.

## Logins ##

Jeedom : admin/admin
SSH : root/Mjeedom96 (à modifier dans core/install/OS_specific/Docker/init.sh avant le build)
BDD : root/Mjeedom96 (à modifier dans core/install/mysqlinstall.sh avant le build)

## Différences avec le repository jeedom officiel ##

- core/install/OS_specific/Docker/init.sh : pas de mot de passe SSH aléatoire
- core/install/install.sh : correction de bugs avec le cron
- core/install/OS_specific/Docker/supervisord.conf : ajout du service mysql
- ajout d'un script d'installation de mysql dans core/install
- modification du Dockerfile pour prendre en compte les changements et installer Jeedom lors du build de l'image
