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

# Directive CMD : commande par défaut executee à la fin (donc une fois un conteneur RUNNING)
CMD ["python","app.py"]  
