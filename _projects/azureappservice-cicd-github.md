---
title: "CI/CD avec GitHub Actions et Azure App Service"
excerpt: "Mise en place d’un pipeline CI/CD pour une application PHP (Laravel) déployée sur Azure App Service, avec base MySQL et cache Redis."
header:
  overlay_image: /assets/images/devops-github-actions-azure-php-laravel_hero.png
  teaser: /assets/images/devops-github-actions-azure-php-laravel_teaser.png
tags: [Azure, GitHub Actions, CI/CD, DevOps, PHP, Laravel, MySQL, Redis, Cloud, Automation]
toc: true
toc_sticky: true
classes: wide
---


## Introduction

<video autoplay muted loop playsinline preload="metadata" width="100%">
  <source src="{{ '/assets/videos/azureappserviceproject1.mp4' | relative_url }}" type="video/mp4">
</video>

### Contexte

Ce projet a été réalisé dans le cadre de mon apprentissage sur Azure App Service Environments et les intégrations avec GitHub. L’objectif était de mettre en pratique les concepts appris (via Microsoft Learn et des vidéos YouTube) en déployant une application Laravel connectée à une base MySQL et à un cache Redis, le tout hébergé sur Azure.


### Objectif

- Héberger une application PHP (Laravel) sur Azure App Service
- Connecter l’application à Azure Database for MySQL Flexible Server
- Ajouter un cache avec Azure Cache for Redis
- Mettre en place une automatisation CI/CD avec GitHub Actions
- Sécuriser les connexions via Private Endpoints et Azure Key Vault

### Environnement utilisé

- Cloud : Microsoft Azure
- Web hosting : Azure App Service (Linux)
- Base de données : Azure Database for MySQL Flexible Server
- Cache : Azure Cache for Redis
- CI/CD : GitHub Actions
- Framework : Laravel (PHP 8.4)
- Versioning : Git & GitHub
- Outils complémentaires : Azure CLI, Visual Studio Code Codespaces

  
## Architecture globale

### Description

- Application Laravel déployée sur Azure App Service Linux
- Base MySQL et Redis Cache créés dans Azure, accessibles uniquement via private endpoints
- Connexions sécurisées avec Azure Key Vault (stockage des secrets)
- Déploiement continu configuré avec GitHub Actions : chaque push sur GitHub déclenche un build + déploiement automatique
- Tests et migrations exécutés directement dans le conteneur App Service


### Schéma d’architecture (vue simplifiée)

<div style="overflow-x:auto;">
  <a href="{{ '/assets/images/diagram-project2.svg' | relative_url }}" target="_blank">
    <img src="{{ '/assets/images/diagram-project2.svg' | relative_url }}" 
         style="width:100%; height:auto;" 
         alt="Diagramme Infra Azure">
  </a>
</div>


## Prérequis

### Techniques

- Azure Subscription
- GitHub account (fork du repo Laravel Tasks)
- Connaissances de base : PHP, Laravel, Git
- Azure CLI installé en local

### Accès

- Rôle Contributor/Owner sur Azure
- Droits d’accès au repo GitHub forké

## Déploiement Infrastructure & Application

### Étapes principales

1. Création de l’App Service (Linux, PHP 8.4, plan Basic)
2. Création d’une Azure Database for MySQL Flexible Server
3. Création d’un Azure Cache for Redis
4. Configuration des Private Endpoints pour MySQL et Redis
5. Stockage des secrets dans Azure Key Vault
6. Configuration des Service Connectors (App Service ↔ MySQL & Redis via Key Vault)
7. Paramétrage des variables d’environnement Laravel (APP_KEY, DB, Redis, SSL, etc.)
8. Configuration de l’intégration continue avec GitHub Actions
9. Tests : migration de la base (`php artisan migrate`) et vérification via navigateur

### CI/CD avec GitHub Actions

  
### Workflow

Chaque commit/push déclenche un pipeline qui :
1. Build le code Laravel
2. Déploie sur Azure App Service
3. Exécute les migrations si nécessaire
4. Met à jour automatiquement l’application en ligne

Exemple simplifié du workflow GitHub Actions généré automatiquement :
```yaml
name: Build and deploy PHP app to Azure Web App

on:
  push:
    branches:
      - main

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Setup PHP
        uses: shivammathur/setup-php@v2
        with:
          php-version: '8.4'
      - name: Run composer install
        run: composer install --no-dev --optimize-autoloader
      - name: Deploy to Azure Web App
        uses: azure/webapps-deploy@v2
        with:
          app-name: "laravel-mysql-demo"
          publish-profile: ${{ secrets.AZURE_WEBAPP_PUBLISH_PROFILE }}
          package: .
```

## Application

- Repo source : [Azure-Samples/laravel-tasks](https://github.com/Azure-Samples/laravel-tasks)
- Langage : PHP (Laravel)
- Base de données : Azure MySQL Flexible Server
- Cache : Azure Redis
- Fonctionnement :
  - Ajout de tâches dans l’UI Laravel
  - Les données sont stockées dans MySQL
  - Redis assure le cache et améliore la vitesse de réponse

## Sécurité

- Utilisation de Private Endpoints (pas d’accès public à MySQL et Redis)
- Secrets déplacés dans Azure Key Vault via Service Connectors
- App Service configuré en HTTPS (SSL activé)
- Logging activé via App Service Log Stream

## Procédures opérationnelles

- Déploiement : GitHub → push → pipeline → Azure
- Migration DB : via `php artisan migrate --force` dans l’App Service (SSH intégré)
- Rollback : revert sur GitHub → redéploiement automatique
- Supervision : App Service Logs, Azure Monitor

## Résultats

- ✅ Déploiement complet en moins de 6h (avec résolution de bugs Laravel & compatibilité PHP)
- ✅ Mise en place réussie de GitHub Actions → déploiement automatique dès modification du code
- ✅ Application en ligne, fonctionnelle avec DB + Redis
- ✅ Vidéo de démonstration (2 minutes) montrant la mise à jour automatique du frontend après un push GitHub

## Annexes

- [Tutoriel officiel Microsoft](https://learn.microsoft.com/en-us/azure/app-service/tutorial-php-mysql-app?pivots=azure-developer-cli)
- [Repo Laravel Tasks](https://github.com/Azure-Samples/laravel-tasks)
- [Mon Repo](https://github.com/stanilpaul/AppServiceProject-Php-SQL-laravel-tasks)
- [Azure App Service](https://azure.microsoft.com/fr-fr/products/app-service)
- [Azure Database for MySQL](https://azure.microsoft.com/fr-fr/products/mysql)
- [Azure Cache for Redis](https://azure.microsoft.com/fr-fr/products/cache/)