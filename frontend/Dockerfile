# Utiliser l'image Node.js version 20 pour React
FROM node:20

# Définir le répertoire de travail
WORKDIR /app

# Copier les fichiers package.json et package-lock.json
COPY package*.json ./

# Installer les dépendances
RUN npm install

# Copier le reste des fichiers de l'application
COPY . .

# Exposer le port 3000 pour React
EXPOSE 3000

# Commande pour démarrer le serveur de développement React
CMD ["npm", "start"]
