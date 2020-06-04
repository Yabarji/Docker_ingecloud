# Formation Docker

## Commandes hote :
```
docker version
docker info
```
## Commandes docker client :
```
docker --help
docker search
```

# Telecharger une image docker depuis le HUB
```
docker pull [IMAGE:VERSION]
docker pull debian:jessie
```

# Lister les images disponibles sur l'hote:
```
docker images
```

# Creer et demarrer un container sans options 
```docker run debian:jessie```

# Creer et demarrer un container en mode interactif
### -t : tty
### -i : interactif
```docker run -it debian:jessie /bin/bash```

# Creer et demarrer un container en lui specifiant une commande (date) 
```docker run debian:jessie date```

# Lister les containers actif 
```docker ps```

# Lister touts les containers (actif et arrêtés)
```docker ps -a```

# Démarrer un container
```docker start [ID|NOM]```

# Stopper un container
```docker stop [ID|NOM]```

### Visualiser les Logs d'un container à l'état RUNNING :
```
$ docker logs ID
$ docker logs -f ID
```

### Demarrer un container en background : detaché
```$ docker run -d -it debian:jessie```

### Utilisation des ID pour stop & remove 
```$ docker stop $(docker ps -q) && docker rm $(docker ps -aq)```

### Prune 
```$ docker container prune```

### Sortir d'un conteneur sans tuer son processus
> Sinon on stoppe le conteneur

```CTRL+P+Q```
