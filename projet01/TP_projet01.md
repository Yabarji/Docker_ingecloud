# TP projet01 : création de 3 conteneur liés

## Creation d'un réseau docker de type dédié

```$ docker network create dockerweb```

## Structure du projet
> Les repertoire conf et www sont créés et les fichiers index.php et nginx.conf déposés

## Lancement des conteneurs 
> /!\ Bien se repositionner à la racine du projet : dans projet01
> SI recreéation des conteneurs, bien nettoyer avant :
$ docker container stop app_web app_php && docker container rm app_web app_php

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

## Modification du fichier index.php pour interroger la base du conteneur nommé "app_bdd"

