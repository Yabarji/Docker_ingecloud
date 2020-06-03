# Correction TP Docker : Les commandes de base

### Exercice 1 : Hello from Alpine
Le but de ce premier exercice est de lancer des containers basés sur l'image alpine
1. Lancez un container basé sur alpine en lui fournissant la command echo hello
2. Quelles sont les étapes effectuées par le docker daemon ?
3. Lancez un container basé sur alpine sans lui spécifier de commande. Qu’observez-vous ?
#### Correction de l'exercice 1
1. La commande à lancer est :
```docker container run alpine echo hello```

2. Le résultat de la commande précédente montre les différentes étapes qui sont effectuées:

```
Unable to find image 'alpine:3.8' locally
latest: Pulling from library/alpine
88286f41530e: Pull complete
Digest: sha256:1072e499f3f655a032e88542330cf75b02e7bdf673278f701d7ba61629ee3ebe
Status: Downloaded newer image for alpine:latest
hello
L'image alpine n'étant pas disponible localement, elle est téléchargée depuis le Docker Hub.
Un container est alors lancé à partir de cette image avec la commande spécifiée (echo
"hello"). Le résultat de cette commande est affiché sur la sortie standard. Une fois la
commande terminée, le container est supprimé.
```

3. La commande à lancer est :
```docker container run alpine```

L'image alpine étant déjà présente localement (téléchargée lors de l'étape précédente), elle est
ré-utilisée. La commande exécutée par défaut lors du lancement d'un container basé suralpine est "/bin/sh". Cette commande ne produit pas de résultat sur la sortie standard. Le
container est supprimé une fois la commande lancée.

### Exercice 2 : shell intéractif
Le but de cet exercice est lancer des containers en mode intéractif
1. Lancez un container basé sur alpine en mode interactif sans lui spécifier de commande
2. Que s’est-il passé ?
3. Quelle est la commande par défaut d’un container basé sur alpine ?
4. Naviguez dans le système de fichiers
5. Utilisez le gestionnaire de package d’alpine (apk) pour ajouter un package
```
$ apk update
$ apk add curl
```

#### Correction de l'exercice 2
1. La commande permettant de lancer un container en mode "interactif" est la suivante:
```docker container run -ti alpine```
2. Nous obtenons un shell sh dans le container.
3. Par défaut, la commande par défaut utilisée dans l'image alpine est /bin/sh
Note: nous y reviendrons plus tard mais il est intéressant de voir que cette information est
présente dans le fichier Dockerfile qui est utilisé pour créer l'image
(https://github.com/gliderlabs/docker-
alpine/blob/2127169e2d9dcbb7ae8c7eca599affd2d61b49a7/versions/library-
3.6/x86_64/Dockerfile)
4. Nous pouvons naviguer dans le système de fichiers de la même façon que nous le faisonsdans une autre distribution Linux plus "traditionnelle" en utilisant les commandes cd, ls,
pwd, cat, less, ...
5. Le gestionnaire de package d'une distribution alpine est apk
Pour mettre à jour la liste des packages, nous pouvons utiliser la commande apk update .
Pour installer un package, comme curl , nous utilisons la commande suivante apk add curl

### Exercice 3 : foreground / background
Le but de cet exercice est de créer des containers en foreground et en background
1. Lancez un container basé sur alpine en lui spécifiant la commande ping 8.8.8.8
2. Arrêter le container avec CTRL-C
Le container est t-il toujours en cours d’exécution ?
Note: vous pouvez utiliser la command docker ps que nous détaillerons dans l'une des
prochaines lectures), et qui permet de lister les containers qui tournent sur la machine.
3. Lancez un container en mode interactif en lui spécifiant la command ping 8.8.8.8
4. Arrêter le container avec CTRL-P CTRL-Q
Le container est t-il toujours en cours d’exécution ?
5. Lancez un container en background, toujours en lui spécifiant la command ping 8.8.8.8
Le container est t-il toujours en cours d’exécution ?

#### Correction de l'exercice 3
1. Le container peut être lancé avec la commande suivante :

```docker container run alpine ping 8.8.8.8```
2. La commande docker ps ne liste pas le container car le processus a été arrêté par la commande CTRL-C
3. La commande suivante permet de lancer le container en mode "interactif" :

```docker container run -ti alpine ping 8.8.8.8```
4. La commande CTRL-P CTRL-Q permet de se détacher du speudo terminal (alloué avec
les options -t -i, ou -ti).
Le container continue à tourner. Il est listé avec la commande docker ps
5. La commande suivante permet de lancer le container en background : 

```docker container run -d alpine ping 8.8.8.8```
La commande docker ps permet de voir que le container tourne, il n'est simplement pas
attaché au terminal depuis lequel il a été lancé.

### Exercice 4 : liste des containers
Le but de cet exercice est de montrer les différentes options pour lister les containers du
système
1. Listez les containers en cours d’exécution. Est ce que tous les containers que vous avez créés sont listés ?
2. Utilisez l’option -a pour voir également les containers qui ont été stoppés
3. Utilisez l’option -q pour ne lister que les IDs des containers (en cours d’exécution ou
stoppés)
#### Correction de l'exercice 4
1. Pour lister les containers en cours d'execution sur le système, les 2 commandes suivantes sont équivalentes
```
docker container ls
docker ps
```
Note: la seconde commande est historique et date de l'époque ou la plateforme Docker était
principalement utilisée pour la gestion des containers et des images. Par la suite, d'autres
primitives que nous verrons dans les prochains chapitres ont été ajoutées (volume, network,
node, ...), ce qui a conduit à une refactorisation de l'api disponible en ligne de commande.

2. Seuls les containers en cours d'execution sont listés. Les containers qui ont été créés
puis arrêtés ne sont pas visible dans la sortie de cette commande.

3. Les commandes suivantes permettent de lister les containers en cours d'execution ainsi
que ceux qui sont stoppés.
```
docker container ls -a
docker ps -a
```

4. Les commandes suivantes permettent de lister les identifiants de l'ensemble des
containers tournant sur la machine hôte, ceux en cours d'execution et également ceux qui
ont été stoppés.
```
docker container ls -aq
docker ps -aq
```
Note: on verra que ces commandes sont très utiles, notamment lorsque l'on souhaitera faire
une action sur un ensemble de containers.

### Exercice 5 : exec dans un container
Le but de cet exercice est de montrer comment lancer un processus dans un container
existant
1. Lancez un container en background, basé sur l’image alpine. Spécifiez la commande
ping 8.8.8.8 et le nom ping avec l’option --name
2. Observez les logs du container en utilisant l’ID retourné par la commande précédente ou
bien le nom du container. Quittez la commande de logs avec CTRL-C
3. Lancez un shell sh, en mode interactif, dans le container précédent
4. Listez les processus du container
Qu'observez vous par rapport aux identifiants des processus ?

#### Correction de l'exercice 5
1. La commande suivante permet de lancer le container en question
```
$ docker container run -d --name ping alpine ping 8.8.8.8
172c401915f56e3fb10391259fac77bc2d3c194a1b27fa5072335e04656e57bb
```
2. La commande suivante permet de suivre les logs en continue (option -f) à partir de l'identifiant :
```
$ docker container logs -f 172
PING 8.8.8.8 (8.8.8.8): 56 data bytes
64 bytes from 8.8.8.8: seq=0 ttl=37 time=20.713
64 bytes from 8.8.8.8: seq=1 ttl=37 time=19.747
64 bytes from 8.8.8.8: seq=2 ttl=37 time=19.730
64 bytes from 8.8.8.8: seq=3 ttl=37 time=20.345
64 bytes from 8.8.8.8: seq=4 ttl=37 time=24.476
ms
ms
ms
ms
ms
```
Le nom du container peut également être utilisé
```
$ docker container logs -f ping
...
64 bytes
64 bytes
64 bytes
64 bytes
64 bytes
```
La commande CTRL-C permet de quitter la sortie de logs, mais elle ne stoppe pas le container
car elle n'est pas envoyé au processus tournant dans celui-ci.

3. La commande suivante permet de lancer un shell sh dans le container
```
$ docker exec -ti ping sh
/ #
```
4. La commande suivante permet de lister les processus qui tournent dans le container
```
/ # ps aux
```

### Exercice 6 : cleanup
Le but de cet exercice est de stopper et de supprimer les containers existants
1. Listez tous les containers (actifs et inactifs)
2. Stoppez tous les containers encore actifs en fournissant la liste des IDs à la commande
stop
3. Vérifiez qu’il n’y a plus de containers actifs
4. Listez les containers arrêtés
5. Supprimez tous les containers
6. Vérifiez qu’il n’y a plus de containers


#### Correction de l'exercice 6
1. Afin de lister les containers qui tournent ainsi que ceux qui ont été arrêtés, il faut utiliser
l'option -a , les commandes suivantes sont équivalentes:
```
docker ps -a
docker container ls -a
```
2. Pour stopper, en une seule ligne de commande, l'ensemble des containers qui tournent,
on peut donner la liste des identifiants à la commande stop . On utilise pour cela l'option -q lorsque l'on liste les containers.

```docker container stop $(docker container ls -q)```

3. La commande suivante ne devrait plus renvoyer de containers

```docker container ls```

Note: cette commande est équivalente à docker ps

4. Si on ajoute l'option -a , on obtient les containers qui sont arrêtés.

```docker container ls -a```

5. Suppression des containers

```docker container prune```