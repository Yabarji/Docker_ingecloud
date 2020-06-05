# Image application python flask

# Directive FROM pour partir d'une image de référence
FROM python:3.7-slim

LABEL maintainer="Pierre <psable@dawan.fr>"

# Directive COPY : pour intégrer des fichiers dans l'image
COPY . /app

# Directive WORKDIR : permet de me positionner dans un répertoire
WORKDIR /app

# Directive RUN : executer des commandes de type shell
RUN pip install -r requirements.txt

# Directive ENTRYPOINT : permet de definir la commande a executer au demarrage du conteneur /!\ Celle-ci ne pourra pas être surchage
ENTRYPOINT ["python"]

# Directive CMD : commande par défaut executee à la fin (donc une fois un conteneur RUNNING) ou argument de ENTRYPOINT
# CMD peut être surchargée au démarrage d'un conteneur
CMD ["app.py"]  
