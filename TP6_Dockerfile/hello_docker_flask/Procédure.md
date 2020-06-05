# Création d'un image docker_flask

## Le projet 
IL contient un script app.py, un fichier requirement.txt et le Dockerfile

## Le BUILD
On build une image à partir de ce projet
```
$ docker image build -t docker_flask:1.0 .
```

## Le Conteneur associé
On instancie un conteneur à partir de cette image
```
$ docker container run -p 5000:5000 docker_flask:1.0
```
