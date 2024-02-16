# Installation de docker
1. Récuperation de httpd
   - docker pull httpd:latest // pour récuperer l'image httpd
   -  // Pour connaitre la version
   ```bash 
   docker -v  
   ```
   - creer le dossier html avec : mkdir html et dedans le fichier index.html
   - Démarrer le conteneur et servir la page html créer précedemment à l'aide d'une référence absolue:
   ```bash 
   docker run -d -p 8080:80 -v /home/saitamadubled/Documents/devops_TP2_DOCKER_ynov/TP_DOCKER_1/html/index html:/usr/local/apache2/htdocs/index.html  httpd:latest
   ```