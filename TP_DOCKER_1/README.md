# TP1 Docker
### 1 . Installation de docker
### 2 . Créer dossier TP_DOCKER_1
### 3 . Executer un serveur web dans un container 
   - Pour récuperer l'image httpd
   ```bash
   docker pull httpd:latest 
   ```

   -  Pour connaitre la version
   ```bash 
   docker -v  
   ```

   - creer le dossier html avec : mkdir et dedans créer le fichier index.html

   - Démarrer le conteneur et servir la page html créer précedemment à l'aide d'une référence absolue:
   ```bash 
   docker run -d -p 8080:80 -v /home/saitamadubled/Documents/devops_TP2_DOCKER_ynov/TP_DOCKER_1/html/index html:/usr/local/apache2/htdocs/index.html  httpd:latest
   ```

   - Stopper et arreter 
   ```bash 
   docker ps                   // voir les conteneur en marche
   docker stop [CONTENEUR]     // stopper
   docker rm [CONTENEUR]       // supprimer
   ```