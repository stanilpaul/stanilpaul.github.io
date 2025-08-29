---
title: "CI/CD Azure DevOps Pipelines — Application C# sur Azure App Service"
excerpt: "Pipeline YAML Azure DevOps : build C#, publication et déploiement continus vers Azure App Service, déclenché depuis GitHub via Service Principal."
permalink: /projects/azure-devops-pipelines-csharp-appservice/
header:
  overlay_image: /assets/images/azuredevopscicd_hero.png
  overlay_filter: 0.35
  teaser: /assets/images/azuredevopscicd_teaser.png
image: /assets/images/azuredevopscicd_teaser.png
tags:
  - Azure
  - Azure DevOps
  - Pipelines
  - CI/CD
  - YAML
  - App Service
  - C#
  - Service Principal
  - GitHub
toc: true
toc_sticky: true
classes: wide
read_time: true
author_profile: true
breadcrumbs: true
---

## Introduction

<video autoplay muted loop playsinline preload="metadata" width="100%">
  <source src="{{ '/assets/videos/azuredevopspipelinegithubrepo.mp4' | relative_url }}" type="video/mp4">
</video>

### Contexte

Après avoir complété ma formation Azure DevOps, j’ai décidé de mettre en pratique mes connaissances avec un projet concret.
L’objectif était de déployer une application web hébergée sur GitHub vers Azure App Service, en utilisant un pipeline entièrement automatisé avec Azure DevOps Pipelines.

Ce projet m’a permis d’explorer les fonctionnalités principales d’Azure DevOps (Repos, Pipelines, Service connections, App Registrations, Boards, etc.) tout en développant une approche pratique du CI/CD dans un environnement cloud Microsoft.


### Objectif

- Héberger une application existante sur Azure App Service
- Mettre en place un pipeline CI/CD avec Azure DevOps
- Connecter GitHub à Azure DevOps via OAuth/App Registration
- Automatiser la compilation et le déploiement via YAML pipelines
- Comprendre les limites du compte gratuit (parallélisme) et les solutions

### Environnement utilisé

- Cloud : Microsoft Azure
- Outils CI/CD : Azure DevOps Pipelines
- Code source : GitHub (fork de [online-calculator-app]())
- Application : C# (95.1%), HTML, CSS, JavaScript
- Déploiement cible : Azure App Service + App Service Plan
- Sécurité & identité : Azure App Registration (Service Principal)
- Pipeline : YAML (CI/CD automatisé)

## Architecture globale

### Description

- L’application (un calculateur simple) est stockée sur GitHub
- Un pipeline YAML défini dans Azure DevOps automatise les étapes suivantes :
  - Build du code en mode Release
  - Publication de l’application
  - Déploiement automatique vers Azure App Service
- L’authentification entre Azure DevOps et Azure est réalisée via une App Registration (Service Principal)
- Le déclenchement du pipeline est lié aux push sur la branche main de GitHub
  
### Schéma d’architecture (vue simplifiée)

<div style="overflow-x:auto;">
  <a href="{{ '/assets/images/diagram-project3.svg' | relative_url }}" target="_blank">
    <img src="{{ '/assets/images/diagram-project3.svg' | relative_url }}" 
         style="width:100%; height:auto;" 
         alt="Diagramme Infra Azure">
  </a>
</div>

## Prérequis

### Techniques

- Abonnement Azure actif
- Compte GitHub (pour forker le repo de l’application)
- Compte Azure DevOps avec accès aux Pipelines
- Droits de création : App Service, Service Principal, Resource Group

### Étapes préparatoires

- Création d’un App Service Plan + App Service
- Création d’une App Registration (client ID/secret) pour authentifier Azure DevOps vers Azure
- Demande de parallélisme (obligatoire pour exécuter les pipelines avec un compte gratuit → délai 4 à 5 jours)

## Déploiement Infrastructure & Application

### CI/CD avec GitHub Actions

1. Cloner l’application depuis GitHub Fork de [online-calculator-app](https://github.com/huzefaMD/online-calculator-app)
 vers mon GitHub : 👉 [Mon repo](https://github.com/stanilpaul/AZURE-DEVOPS-PROJ_online-calculator-app)
2. Créer un App Service et un App Plan dans Azure
3. Créer une App Registration (Service Principal)
   - Génération du client ID + secret
   - Attribution des rôles nécessaires au niveau du resource group
4. Configurer le pipeline YAML dans Azure DevOps :
   
```yml
variables:
  buildConfiguration: 'Release'

steps:
- script: dotnet build --configuration $(buildConfiguration)
  displayName: 'dotnet build $(buildConfiguration)'

- task: DotNetCoreCLI@2
  inputs:
    command: 'publish'
    publishWebProjects: true

- task: AzureWebApp@1
  inputs:
    azureSubscription: 'azuredevops-serviceendpoint'
    appType: 'webApp'
    appName: 'mywebapp25'
    package: '$(System.DefaultWorkingDirectory)/**/*.zip'

```

5. Configurer la connexion GitHub ↔ Azure DevOps
   - Nouveau pipeline → GitHub → connexion au repo → sélection du YAML
   - Ajustement des valeurs (subscription, appName, etc.)
   - Commit + push → déclenchement automatique
6. Activer le Continuous Integration (CI)
   - Dans le pipeline : “Triggers” → override YAML → activer “CI” sur la branche main

## CI/CD avec Azure DevOps Pipelines

### Fonctionnement

- CI : Chaque modification poussée sur `main` déclenche automatiquement le build et la publication
- CD : L’application est déployée automatiquement sur Azure App Service
- Logs & monitoring : disponibles dans l’interface Azure DevOps et App Service Logs

## Application

- Type : Web App (calculatrice en ligne)
- Langages : C# (95%), HTML, CSS, JS
- Déploiement cible : Azure App Service (Linux)
- Résultat : modification dans GitHub → pipeline → déploiement → mise en production immédiate  
👉 Démo : Un push sur GitHub met à jour la calculatrice en ligne en quelques minutes.

## Sécurité

- Service Principal utilisé pour sécuriser la communication Azure DevOps ↔ Azure
- App Registration configurée avec droits minimaux nécessaires
- Secrets gérés dans Azure DevOps Library (secure files/variables)
- Application hébergée uniquement en HTTPS via App Service

## Procédures opérationnelles

- Déploiement : push sur GitHub → pipeline → déploiement automatisé
- Rollback : revert sur GitHub → pipeline → retour à la version précédente
- Supervision : monitoring via Azure DevOps + App Service logs

## Résultats

- ✅ Premier projet complet avec Azure DevOps Pipelines
- ✅ Intégration GitHub ↔ Azure DevOps réussie
- ✅ Déploiement automatisé fonctionnel
- ✅ Mise en pratique des concepts vus en formation Azure DevOps
- ✅ Gain de confiance pour industrialiser le CI/CD dans un contexte professionnel

## Annexes

- [Repo de l’application utilisée](https://github.com/huzefaMD/online-calculator-app)
- [Mon fork GitHub](https://github.com/stanilpaul/AZURE-DEVOPS-PROJ_online-calculator-app)
- [Demande de parallélisme Azure DevOps](https://forms.office.com/pages/responsepage.aspx?id=v4j5cvGGr0GRqy180BHbR5zsR558741CrNi6q8iTpANURUhKMVA3WE4wMFhHRExTVlpET1BEMlZSTCQlQCN0PWcu&route=shorturl)
- [Azure Devops](https://aex.dev.azure.com/)