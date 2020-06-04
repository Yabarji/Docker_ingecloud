# TP Network : présentation réseau bridge

## Création d'un réseau dédié de type bridge
> Un réseau de type bridge créé permet d'implementer le mecanisme DNS (résolution de nom)
Ainsi les conteneurs pourront communiquer entre eux via l'IP ou leur non de conteneur

```$ docker network create tp4_net```

## Création de conteneur utilisant ce réseau et en leur précisant un nom :

```
$ docker container run -d --network tp4_net --name centos01 centos
$ docker container run -d --network tp4_net --name centos02 centos
```

## Connexion dans un des deux conteneurs pour tester le réseau

```
$ docker container exec -it centos01 /bin/bash
root@id# ping centos02
```
