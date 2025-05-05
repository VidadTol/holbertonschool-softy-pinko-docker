# Utilisation d'Ubuntu le plus récent
FROM ubuntu:latest

# Mise à jour des paquets et installation de Python3 & pip3
RUN apt-get update && apt-get upgrade -y
RUN apt-get install -y python3 python3-pip

# Correction du problème "externally managed"
# Evite l erreur pip3: This environment is externally managed
RUN rm -f /usr/lib/python*/EXTERNALLY-MANAGED

# Installation de Flask avec pip3
RUN pip3 install flask

# Installation de Flask-CORS pour gérer les requêtes CORS
RUN pip3 install flask flask-cors

# Création du répertoire de l'application
WORKDIR /app

# Copie du fichier api.py dans le conteneur
COPY ./api.py /app/api.py

# Commande de démarrage du serveur Flask
CMD ["python3", "/app/api.py"]