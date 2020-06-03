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
