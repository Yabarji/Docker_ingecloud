# TP Docker Commit : Création d’une image à partir d’un container
**Enoncé**
1. Lancez une container basé sur une image alpine:3.8, en mode interactif, et en lui donnant
le nom c1
2. Lancez la commande curl google.com
Qu'observez-vous ?
3. Installez curl à l’aide du gestionnaire de package apk
4. Quittez le container avec CTRL-P CTRL-Q (pour ne pas killer le processus de PID 1)
5. Créez une image, nommée myping, à partir du container c1
Utilisez pour cela la commande commit (docker commit --help pour voir le fonctionnment de
cette commande)
6. Lancez un shell intéractif dans un container basée sur l’image myping et vérifiez que curl
est présent
