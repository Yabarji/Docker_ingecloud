# Presentation des volumes

# Création d'un projet sous forme répertoire sur le docker hôte

```
$ mkdir TP5_Volume
$ cd TP5_Volume
$ mkdir www
$ cd www
$ vi index.html (recopier le fichier index.html en exemple sur github)
```

# Création d'un conteneur nginx en lui attribuant un volume ${PWD}/www (ou le chemin complet pour aller jusqu'à www)

```$ docker container run -d -v ${PWD}/www/:/usr/share/nginx/html/ -p 89:80 --name web01 nginx:1.18```

# Test du site 
http://localhost:89


# On peut maintenant modifier le fichier index.html SUR LE DOCKER HOTE
> La modif se visible instantanement dans le conteneur via le partage du volume
