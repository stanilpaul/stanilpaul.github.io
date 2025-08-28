---
title: "CI/CD Jenkins sur Azure (Terraform, Docker)"
excerpt: "Pipeline de bout en bout: Azure Spot VM via Terraform + Jenkins + Docker Compose. Build, tests et déploiement d'une app conteneurisée."
header:
  overlay_image: /assets/images/devops-ci-cd-jenkins-azure-terraform_hero.png
  teaser: /assets/images/devops-ci-cd-jenkins-azure-terraform_teaser.png
tags: [Azure, Terraform, Jenkins, Docker, CI/CD, DevOps, IaC, Linux, SRE]
toc: true
toc_sticky: true
classes: wide
---

<!-- Init Mermaid (liens cliquables = securityLevel 'loose') --><script src="https://cdn.jsdelivr.net/npm/mermaid@10/dist/mermaid.min.js"></script><script> mermaid.initialize({ startOnLoad: true, theme: "neutral", securityLevel: "loose" }); </script><div class="notice--info"> <strong>On apprend quoi avec ce projet ?</strong><br/> - Déployer une <em>infrastructure économique</em> sur Azure (Spot VM) via <strong>Terraform</strong> (IaC).<br/> - Installer et orchestrer <strong>Jenkins</strong> pour automatiser <strong>build → test → déploiement</strong>.<br/> - Conteneuriser l’app (frontend + MySQL) via <strong>Docker Compose</strong> et l’exposer publiquement.<br/> - Produire une documentation <strong>niveau consultant/architecte</strong> (enjeux, choix, coûts, sécurité, SRE). </div>
1) Contexte et objectifs
Application de départ: “docker/getting-started-app” (JS + MySQL).
Mon apport: transformation en projet DevOps complet (IaC + CI/CD + containers).
Objectifs:
Automatiser le pipeline: commit → build/test → déploiement via webhook GitHub.
Réduire les coûts et l’ops manuel (Spot VM, éviter SSH côté équipe).
Documenter clairement pour revue d’architecture et transfert de connaissance.
2) Architecture — Vue Ingénieur Cloud (Azure)
<div class="mermaid"> flowchart LR subgraph Azure_Subscription[Azure Subscription] subgraph RG[Resource Group] TF[(Terraform)] VM[Ubuntu Spot VM] NSG[Network Security Group] PIP[(Public IP)] JV[Jenkins (service)] DK[Docker Engine] APP[App Container] DB[(MySQL Container)] VOL[(Azure Disk - Volume)] AP[Apache (init Jenkins - démo)] GH[GitHub Repo]
  TF --> VM
  VM <-->|attached| PIP
  VM --- NSG
  VM --> DK
  DK --> APP
  DK --> DB
  DB --> VOL
  VM --> JV
  JV -->|webhook| GH
  AP -. expose init pass .- JV
end
end

USER[Utilisateur Internet] -->|HTTP| APP

%% Styles
classDef az fill:#e6f3ff,stroke:#0078d4,color:#000,stroke-width:1px;
class VM,NSG,PIP,JV,DK,APP,DB,VOL,AP az;

%% Lien cliquable vers le repo
click GH "https://github.com/stanilpaul/docker-getting-started-devops-enhanced" "Repo GitHub" _blank

</div>
3) Pipeline — Vue Développeur (CI/CD)
<div class="mermaid"> sequenceDiagram participant Dev as Développeur participant GH as GitHub participant JK as Jenkins participant VM as Azure VM participant DC as Docker Compose
Dev->>GH: git push (branche main)
GH-->>JK: Webhook (Push event)
JK->>VM: Checkout repo (Jenkinsfile)
JK->>VM: docker volume create (si besoin)
JK->>DC: docker-compose up -d (environnement de test)
JK->>VM: Attente MySQL (3306) + tests (yarn test)
JK->>DC: docker-compose down (préserve volumes)
JK->>DC: docker-compose up -d (déploiement prod)
JK-->>Dev: URL app (http://<IP_publique>:3000)

</div>
4) Implémentation (résumé)
Terraform (IaC):
azurerm_* pour RG, réseau, sécurité, IP, NIC, Linux VM (Spot).
NSG: ports minimaux (80/443/3000 pour la démo; SSH restreint si besoin).
cloud‑init / script d’init: Docker, Compose, Jenkins, Apache.
Jenkins:
Webhook GitHub → pipeline déclaratif (Jenkinsfile au repo).
Plugins: Git, Pipeline, Docker (minimal).
Docker Compose:
Services: app, mysql + volume todo-mysql-data (persistance).
5) Jenkinsfile (extrait utilisé)
pipeline {
  agent any
  environment {
    APP_PORT = "3000"
    VM_IP    = "addressPublic"   // IP/DNS public
  }
  stages {
    stage('1. Checkout & Setup') {
      steps {
        git branch: 'main', url: 'https://github.com/stanilpaul/docker-getting-started-devops-enhanced.git'
        sh 'docker volume create todo-mysql-data || true'
      }
    }
    stage('2. Build & Test') {
      steps {
        sh '''
          docker-compose up -d
          for i in {1..30}; do nc -z localhost 3306 && break || sleep 2; done
          docker-compose exec -T app yarn test || true
          docker-compose down
        '''
      }
    }
    stage('3. Deploy Production') {
      steps {
        sh '''
          docker-compose up -d
          sleep 5
          curl -I http://localhost:${APP_PORT} || true
        '''
      }
    }
  }
  post {
    success {
      echo "✅ http://${VM_IP}:${APP_PORT}"
      sh 'docker ps --format "table {{.Names}}\\t{{.Image}}\\t{{.Status}}"'
    }
    failure {
      sh 'docker-compose logs --tail=100 || true'
    }
  }
}

6) Procédure — pas à pas
Provisionner l'infra : terraform init && terraform apply -auto-approve → RG + réseau + VM Spot + NSG + IP publique.
Bootstrap VM (cloud‑init): installe Docker, Compose, Jenkins, Apache.
Configurer Jenkins:
Récupérer le mot de passe initial (via Apache – démo).
Créer l'admin et installer les plugins.
Créer un job “Pipeline from SCM” (branche main, Jenkinsfile à la racine).
Ajouter le webhook GitHub (push → job).
Exécuter le Pipeline: compose up (tests) → tests → down → compose up -d (prod).
Accéder à l'application: http://<IP_PUBLIQUE>:3000
7) Sécurité, SRE, coûts — regard consultant
Sécurité: Key Vault pour secrets; SSH restreint/fermé; reverse proxy TLS; NSG minimal; OIDC GitHub→Jenkins (SSO).
SRE: Spot = préemptible (ok démo). Prod: VMSS ou AKS (Ingress, PV). Healthchecks, logs/metrics (Monitor + Log Analytics).
Coûts: Spot B‑series: -70 à -90% vs on‑demand; disques Standard SSD.
8) Améliorations & roadmap
AKS + Helm + Ingress + Cert‑Manager (TLS auto).
Sauvegardes Jenkins & MySQL (volumes/PV, snapshots).
Environnements dev/stage/prod + approbations.
Terraform: modules, backend distant (Storage + SAS), workspaces.
9) Démo vidéo et code
<div class="ratio ratio-16x9"> <iframe src="https://www.youtube.com/embed/ID_DE_TA_VIDEO" title="Démo CI/CD Jenkins + Terraform + Docker" allowfullscreen></iframe> </div>
Repo: docker-getting-started-devops-enhanced{: .btn .btn--primary target="_blank" rel="noopener" }
