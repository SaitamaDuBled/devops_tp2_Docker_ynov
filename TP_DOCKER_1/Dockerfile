# Utilisation de l'image Apache officielle
FROM httpd:latest

# Copier le fichier index.html vers le répertoire /usr/local/apache2/htdocs/ du conteneur
COPY ./html/index.html /usr/local/apache2/htdocs/

# mettre le dossier sur lequel index.html est
WORKDIR /usr/local/apache2/htdocs/

# Ouvre le lien entre docker et la machine en ouvrant le port 80
EXPOSE 80
