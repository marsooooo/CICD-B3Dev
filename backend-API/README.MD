# Fullstack Deployment Workflow

## Description

Ce projet utilise un workflow GitHub Actions (`deploy-fullstack.yml`) pour déployer automatiquement le frontend et le backend de l’application.  

### Fonctionnement du workflow

1. **Frontend**  
   - Build du projet React situé dans `admin-dashboard`.  
   - Transfert des fichiers build vers le VPS via `rsync`.  
   - Redémarrage du service PM2 `update-build-CICD-daily` pour mettre à jour le frontend.

2. **Backend**  
   - Installation des dépendances Node.js dans `backend-API`.  
   - Déploiement sur Render via l’API Render, en déclenchant un nouveau déploiement et en vidant le cache si nécessaire.  
   - Les secrets GitHub (`RENDER_API_KEY`, `RENDER_SERVICE_ID`, `MONGO_URI`, `JWT_SECRET`) sont utilisés pour sécuriser l’accès au backend et à la base de données.

---

## Utilisation de l’application

1. Accéder à l’application frontend :  
   - https://cicd.marceau-tison.com

2. **Inscription et connexion**  
- Pour utiliser l’application, l’utilisateur doit se **register** puis se **login**.  
- Après connexion, accéder au dashboard :  
  ```
  https://cicd.marceau-tison.com/dashboard
  ```

3. **Comptes admin**  
- Par défaut, tout nouvel utilisateur est créé avec le rôle `user`.  
- Pour créer un compte avec le rôle `admin`, la requête de création doit inclure explicitement `"role": "admin"` et être effectuée depuis l’extérieur de l’application (ex. via API ou base de données).  

---

## Remarques

- Les variables d’environnement (MongoDB, JWT, API Render) doivent être correctement configurées dans GitHub Actions et Render pour que le déploiement fonctionne.  
- Toute modification du frontend ou du backend sur la branche `main` déclenchera automatiquement le workflow de déploiement.
