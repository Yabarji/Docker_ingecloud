**Exercice 1 : publication de port**
Le but de cet exercice est de créer un container en exposant un port sur la machine hôte
1. Lancez un container basé sur nginx et publiez le port 80 du container sur le port 8080 de
l’hôte
2. Vérifiez depuis votre navigateur que la page par défaut de nginx est servie sur
http://localhost:8080
3. Lancez un second container en publiant le même port
Qu’observez-vous ?


**Exercice 2 : inspection d'un containerLe but de cet exercice est l'inspection d’un container**
1. Lancez, en background, un nouveau container basé sur nginx:1.14 en publiant le port 80
du container sur le port 3000 de la machine host.
Notez l'identifiant du container retourné par la commande précédente.
2. Inspectez le container en utilisant son identifiant
3. En utilisant le format Go template, récupérez le nom et l’IP du container
4. Manipuler les Go template pour récupérer d'autres information

