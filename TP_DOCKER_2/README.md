# TP2 Docker
### 1 . Récupérer code source tp_docker_2_devops.zip ur moodle
### 2 . Créer un Dockerfile qui permet de lancer une application NodeJS

### 3 . Executer un serveur web dans un container 

- Ecrire un Dockerfile pour utiliser nodejs :
```Dockerfile
FROM node:20-alpine
WORKDIR /app

COPY ./src ./
RUN npm install

CMD ["node","server.js"]
EXPOSE 3000
```
- Construire l'image et lancer un container avec l'image :

```Dockerfile
docker build -t [my_image] . 
docker run --name [my_container] -p 3000:3000 [my_image]
```
### 4 . Adapter le fichiers models/index.js