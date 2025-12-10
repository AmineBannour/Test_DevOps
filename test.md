# Livrables - Projet DevOps

## Étapes réalisées

### 1. Création du Dockerfile
- Utilisation de l'image de base `node:18-alpine`
- Définition du WORKDIR `/app`
- Copie de `package.json` et `package-lock.json`
- Installation des dépendances avec `npm install`
- Copie du reste du code
- Exposition du port 3000
- Commande de démarrage : `CMD ["npm", "start"]`
- Ajout du script `"start"` dans `package.json` : `"start": "node src/index.js"`

### 2. Création du docker-compose.yml
- Version "3" (supprimée car obsolète dans les versions récentes)
- Service `app` :
  - `build: ./exam`
  - `container_name: todo-app`
  - `ports: "3000:3000"`
  - `restart: always`
- Service `mongodb` :
  - `image: mongo`
  - `ports: "27017:27017"`

### 3. Création du Jenkinsfile
- Stage 1 : Checkout - Récupération du code du dépôt Git
- Stage 2 : Install dépendances Node - `npm install`
- Stage 3 : Tests - `npm test`
- Stage 4 : Build Docker - `docker build -t todo-app .`

## Commandes utilisées

### Docker
```bash
# Construction de l'image
docker build -t todo-app .

# Exécution du conteneur
docker run -p 3000:3000 todo-app

# Arrêt d'un conteneur utilisant le port 3000
docker stop <container_id>
```

### Docker Compose
```bash
# Démarrer les services
docker compose up --build

# Démarrer en arrière-plan
docker compose up -d --build

# Arrêter les services
docker compose down
```

### Jenkins
Le pipeline Jenkins exécute automatiquement les 4 étapes définies dans le Jenkinsfile.

## Captures d'écran requises

1. **App en local** : Application accessible sur http://localhost:3000
2. **Build Docker réussi** : Sortie de la commande `docker build -t todo-app .`
3. **Conteneur en cours d'exécution** : Sortie de `docker ps` montrant le conteneur `todo-app`
4. **docker-compose up** : Sortie de la commande `docker compose up`
5. **Frontend ouvert via compose** : Application accessible via docker-compose
6. **Pipeline Jenkins exécuté (toutes les étapes green)** : Interface Jenkins montrant tous les stages en succès

