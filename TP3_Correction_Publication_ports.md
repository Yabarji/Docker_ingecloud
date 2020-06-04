# TP3 Publication de ports réseaux

#### Correction de l'exercice 1
1. La commande suivante permet de lancer le container basé sur nginx et d'exposer le port 80 de ce container sur le port 8080 de la machine hôte :

```$ docker container run -d -p 8080:80 nginx```

2. La page index.html servie par défaut par nginx est accessible sur le port 8080
> http://localhost:8080

3. Si nous lançons un autre container en utilisant le même port de la machine hôte, nous obtenons une erreur car ce port ne peut pas être utilisé pour les 2 containers.

```
$ docker container run -d -p 8080:80 nginx
c9dc92128bd8871d1c75678fd41dc09c5afcf02857c7c64bd89f560cb2b6aec7
docker: Error response from daemon: driver failed programming external
connectivity on endpoint objective_leakey
(25ea6fe30398e51b5ad3dbd55a56cded518370c81a41d4013d58ca399647718a): Bind for
0.0.0.0:8080 failed: port is already allocated.
```

#### Correction de l'exercice 2
1. La commande permettant de lancer le container en question est la suivante

```$ docker container run -d -p 3000:80 nginx:1.14```

Vous devriez obtenir un résultat proche de celui ci-dessous:
```
Unable to find image 'nginx:1.14' locally
1.14: Pulling from library/nginx
177e7ef0df69: Pull complete
132d4353ecd5: Pull complete
9482632c8a8f: Pull complete
Digest: sha256:98f78a1dde1ba9c9fbb10671b14a74fcff97f0cc85c182e217618397fcaf63fa
Status: Downloaded newer image for nginx:1.14
6eea1906d21fa26c6bd8695c317e29f99e651657063df1964a18906091bd1ed5
```

2. L'inspection d'un container se fait à l'aide de la commande :

```$ docker inspect CONTAINER_ID```
>Note: il est possible de n'utiliser que les permiers caractères de l'identifiant, ou bien le nom du
container si celui-ci à été précisé avec l'option --name lors de la création.

```$ docker inspect 6ee```

Le résultat de la commande ci-dessus a été volontairement tronqué pour améliorer la lisibilité.
```
[
{
"Id": "6eea1906d21fa26c6bd8695...1964a18906091bd1ed5",
"Created": "2019-01-07T12:43:38.035470972Z",
"Path": "nginx",
"Args": [
"-g",
"daemon off;"
],
"State": {
"Status": "running",
"Running": true,
"Paused": false,
"Restarting": false,
"OOMKilled": false,
"Dead": false,
"Pid": 6880,
"ExitCode": 0,
"Error": "",
"StartedAt": "2019-01-07T12:43:39.051210644Z",
"FinishedAt": "0001-01-01T00:00:00Z"
},
"Image": "sha256:3f55d5bb33f3ae6e7f232c82...69324c95ac1cb9d7ae",
"ResolvConfPath":
"/var/lib/docker/containers/6eea1906d21fa26c6bd8695...906091bd1ed5/resolv.conf",
"HostnamePath":
"/var/lib/docker/containers/6eea1906d21fa26c6bd8695...906091bd1ed5/hostname",
"HostsPath":
"/var/lib/docker/containers/6eea1906d21fa26c6bd8695...906091bd1ed5/hosts",
"LogPath": "/var/lib/docker/containers/6eea...1bd1ed5/6eea...1bd1ed5-
json.log",
"Name": "/loving_proskuriakova",
"RestartCount": 0,
"Driver": "overlay2",
"Platform": "linux",
"MountLabel": "",
"ProcessLabel": "",
"AppArmorProfile": "docker-default",
"ExecIDs": null,
"HostConfig": {
...
},
"HostPort": "3000"
}
...
...
...
"bridge": {
"IPAMConfig": null,
"Links": null,
"Aliases": null,
"NetworkID": "445eea139d71bcffcb...1788775b00a7791ab",
"EndpointID": "85d94006c9daee54a...aad4529dc92905",
"Gateway": "172.17.0.1",
"IPAddress": "172.17.0.3",
"IPPrefixLen": 16,
"IPv6Gateway": "",
"GlobalIPv6Address": "",
"GlobalIPv6PrefixLen": 0,
"MacAddress": "02:42:ac:11:00:03",
"DriverOpts": null
```

3. Les format de templating "Go template" permet de récupérer seulement les informations
dont on a besoin dans cette imposante structure json.
La commande utilisée pour récupérer le nom du container:

```
$ docker inspect --format "{{ .Name }}" efc940
/elated_mclean
```

La commande pour récupérer l'adresse IP du container:

```
$ docker inspect -f '{{ .NetworkSettings.IPAddress }}' efc940
172.17.0.5
```
4. Le templating Go est très riche, vous trouverez quelques exemples supplémentaires à
l'adresse suivante Go template :
> https://docs.docker.com/config/formatting/
https://docs.docker.com/engine/reference/commandline/inspect/
