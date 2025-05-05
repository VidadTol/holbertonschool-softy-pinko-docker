# Utilisation de la dernière version de Nginx
FROM nginx:latest

# Création du dossier pour les fichiers front-end
RUN mkdir -p /var/www/html/softy-pinko-front-end

# Copie des fichiers du front-end vers le serveur Nginx
COPY softy-pinko-front-end /var/www/html/softy-pinko-front-end

# Copie du fichier de configuration Nginx
COPY softy-pinko-front-end.conf /etc/nginx/conf.d/default.conf
