# Utiliser l'image Alpine Linux comme base
FROM node:alpine

# Définir le répertoire de travail de l'application dans le conteneur
WORKDIR /app

# Copier le package.json et package-lock.json dans le conteneur
COPY ./src/package*.json .

# Installer les dépendances de l'application
RUN npm install

# Copier le reste des fichiers de l'application dans le conteneur
COPY . .

# port EXPOSE
EXPOSE 3000

# Commande par défaut pour démarrer l'application Node.js
CMD ["node", "app.js"]
