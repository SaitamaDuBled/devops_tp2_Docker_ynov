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

   - Démarrer le conteneur et servir la page html créer précedemment à l'aide d'une référence absolue (chemin à partir de la racine ):
   ```bash 
   docker run -d -p 8080:80 -v /home/saitamadubled/Documents/devops_TP2_DOCKER_ynov/TP_DOCKER_1/html/index.html:/usr/local/apache2/htdocs/index.html  httpd:latest
   ```

   - Stopper et arreter 
   ```bash 
   docker ps                   // voir les conteneur en marche
   docker stop [CONTENEUR]     // stopper
   docker  rm  [CONTENEUR]       // supprimer
   ```

### 4 . Builder une image
   
- à l'aide d'un dockerfile, créer une image qui permet d'exécuter un serveur web (apache dans mon cas)

```Dockerfile 
# Utilisation de l'image Apache officielle
FROM httpd:latest

# Copier le fichier index.html vers le répertoire /usr/local/apache2/htdocs/ du conteneur
COPY ./html/index.html /usr/local/apache2/htdocs/

# Définit le dossier de travail actuel
WORKDIR /usr/local/apache2/htdocs/

# Ouvre le lien entre docker et la machine en ouvrant le port 80
EXPOSE 80
```
- Construire l'image avec :
```bash 
docker build -t [NOM_DIMAGE] .
```
- Exécuter cette image
```bash 
docker run --name [NOM_DOCKER] -d -p 8080:80 [NOM_DIMAGE]
```
- Vérifier ensuite sur le [localhost](http://localhost:8080/) sur le port 8080.