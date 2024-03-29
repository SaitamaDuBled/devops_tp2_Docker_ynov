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
docker build -t [MY_IMAGE] .
```
- Exécuter cette image
```bash 
docker run --name [MY_CONTAINER] -d -p 8080:80 [MY_IMAGE]
```
- Vérifier ensuite sur le [localhost](http://localhost:8080/) sur le port 8080.

### Avantages et inconvénients des 2 méthodes

- **Docker Run Only** :

| Avantages  | Inconvénients   | 
|-------------------------|-----------------------------|
| Rapidité de mise en place | Reproductibilité compliquée |
| Pratique pour des tâches simples | Commandes longues et complexes |
| | Limité en termes de travail d'équipe |

- **Dockerfile** :

| Avantages  | Inconvénients   | 
|-------------------------|-----------------------------|
| Reproductibilité | Temps de construction de l'image |
| Facilite la configuration | Taille de l'image peut être volumineuse |
| Favorise le travail en équipe |  ||

### 5 . Utiliser une base de données dans un container docker

   - Récupérer les images de mysql et de phpmyadmin:
```bash 
docker pull mysql:latest
docker pull phpmyadmin/phpmyadmin:latest
```
   - Executer 2 containers à partir des images

```bash 
docker run -d --name mysql_container -e MYSQL_ROOT_PASSWORD=password mysql:latest
docker run -d --name phpmyadmin_container --link mysql_container:db -p 8080:80 phpmyadmin/phpmyadmin:latest
```

  - Accéder à la plateforme phpmyadmin sur votre [localhost:8080](http://localhost:8080/):

![Phpmyadmin](./image.png)

### 6 . Utilisation de docker-compose.yml

   - docker-compose comparé à docker run:
   
| **Docker Compose**  | **Docker Run**   | 
|-------------------------|-----------------------------|
| Utilisé pour définir et gérer des applications multi-conteneurs | Utilisé pour lancer des conteneurs Docker individuels. |
| Facilite la configuration | Principalement utilisé pour des cas simples ou des tests rapides.|
| Permet de définir plusieurs services, leurs dépendances et leurs configurations dans un fichier unique| fastidieux pour la gestion d'applications complexes ou multi-conteneurs. ||

   - Commande permettant de lancer tous les containers :
```bash 
   docker-compose up 
```
   - Commande permettant de les stopper :
```bash 
   docker-compose down
```
   - docker-compose.yml permettant d'utiliser phpmyadmin :

```docker-compose.yml 

# version de docker-compose
version: '3.8'

services:
  # container pour mysql
  mysql_container:
    image: mysql:latest
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: password

  # container pour phpmyadmin
  phpmyadmin_container:
    image: phpmyadmin/phpmyadmin:latest
    restart: always
    environment:
      PMA_HOST: mysql_server
    # port EXPOSE
    ports:
      - "8080:80"
```
