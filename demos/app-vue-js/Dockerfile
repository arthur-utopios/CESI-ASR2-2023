# On choisit une image de base
FROM node:20-bullseye-slim

# On modifie le répertoire de travail, par convention /app
WORKDIR /app

# On copie des fichiers du répertoire courant vers l'image
COPY . .

# Exécution d'une commande bash
RUN npm install

# Exposition d'un port de l'image
EXPOSE 5173

# Commande qui sera exécutée lorsqu'on lancera le container
CMD npm run dev