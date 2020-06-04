# TP projet01 : création de 3 conteneur liés

## Creation d'un réseau docker de type dédié

```$ docker network create dockerweb```

## Structure du projet
> Les repertoire conf et www sont créés et les fichiers index.php et nginx.conf déposés

## Lancement des conteneurs 
> /!\ Bien se repositionner à la racine du projet : dans projet01
> SI recreéation des conteneurs, bien nettoyer avant :

```
$ docker container stop app_web app_php && docker container rm app_web app_php
```

```
$ sudo docker container run -d -v ${PWD}/www/:/srv/http/ --network dockerweb --name app_php phpdockerio/php73-fpm

$ sudo docker container run -d --name app_web -v ${PWD}/www/:/usr/share/nginx/html/ -v ${PWD}/conf/:/etc/nginx/conf.d/ -p 8082:80 --network dockerweb nginx:1.18
```

## Test URL
> http://dockerweb:8082


## Démarrage d'un troisieme conteneur mariadb

```
$ sudo docker container run -d --network dockerweb --name app_bdd -e MYSQL_ROOT_PASSWORD=roottoor44 mariadb:10.4
```

## Lien entre php et mariadb
> On modifie le fichier index.php en ajoutant une connexion vers app_bdd

| Problème : il manque une driver php-mysql dans le conteneur app_php

## Ajout package et commit
On se connecte au conteneur app_php : 

```
$ sudo docker container exec -it app_php /bin/bash
root@id# apt update && apt install php7.3-mysql
root@id# exit
```

On redémarre le conteneur app_php pour valider la modif :

```
$ sudo docker container restart app_php
```

On valide via l'URL

Si OK, on réalise un commit pour générer une nouvelle image qui reflète notre besoin
```
$ sudo docker commit -a "Auteur" -m "Ajout du module php7.3-mysql" app_php php-mysql:1.0
```

| Ainsi on pourra détruire le conteneur app_php et le reconstruire à partir de cette nouvelle image :

```
$ sudo docker container stop app_php && sudo docker container rm app_php
$ sudo docker container run -d -v ${PWD}/www/:/srv/http/ --network dockerweb --name app_php php-mysql:1.0
```
