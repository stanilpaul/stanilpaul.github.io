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

<script type="module">
  import mermaid from "https://cdn.jsdelivr.net/npm/mermaid@10/dist/mermaid.esm.min.mjs";
  mermaid.initialize({ startOnLoad: true, theme: "neutral" });
</script>

<div class="notice--info">
<strong>On apprend quoi avec ce projet ?</strong><br/>
- Déployer une <em>infrastructure économique</em> sur Azure (Spot VM) via <strong>Terraform</strong> (IaC).<br/>
- Installer et orchestrer <strong>Jenkins</strong> pour automatiser <strong>build → test → déploiement</strong>.<br/>
- Conteneuriser l’app (frontend + MySQL) via <strong>Docker Compose</strong> et l’exposer publiquement.<br/>
- Rédiger une documentation <strong>niveau consultant/architecte</strong> (enjeux, choix, coûts, sécurité, SRE).
</div>

## 1) Contexte et objectifs
- Application de départ: “docker/getting-started-app” (JS + MySQL).
- Mon apport: transformation en projet DevOps complet (IaC + CI/CD + containers).
- Objectifs:
  - Automatiser le pipeline: commit → build/test → déploiement depuis GitHub (webhook).
  - Réduire les coûts et l’ops manuel (Spot VM, éviter SSH côté équipe).
  - Documenter clairement pour revue d’architecture et transfert de connaissance.

## 2) Architecture — Vue Ingénieur Cloud (Azure)
```mermaid
flowchart LR
  subgraph Azure_Subscription[Azure Subscription]
    subgraph RG[Resource Group]
      TF[(Terraform)]
      VM[Ubuntu Spot VM]
      NSG[Network Security Group]
      PIP[(Public IP)]
      JV[Jenkins (service)]
      DK[Docker Engine]
      APP[App Container]
      DB[(MySQL Container)]
      VOL[(Azure Disk - Volume)]
      AP[Apache (init Jenkins - démo)]
      GH[GitHub Repo]
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

  classDef az fill:#e6f3ff,stroke:#0078d4,color:#000,stroke-width:1px;
  class VM,NSG,PIP,JV,DK,APP,DB,VOL,AP az;

  click GH "https://github.com/stanilpaul/docker-getting-started-devops-enhanced" "Repo GitHub" _blank

  sequenceDiagram
  participant Dev as Développeur
  participant GH as GitHub
  participant JK as Jenkins
  participant VM as Azure VM
  participant DC as Docker Compose

  Dev->>GH: git push (branche main)
  GH-->>JK: Webhook (Push event)
  JK->>VM: Checkout repo (Jenkinsfile)
  JK->>VM: docker volume create (si besoin)
  JK->>DC: docker-compose up -d (environnement de test)
  JK->>VM: Attente MySQL (3306) + tests (yarn test)
  JK->>DC: docker-compose down (préserve volumes)
  JK->>DC: docker-compose up -d (déploiement prod)
  JK-->>Dev: URL app (http://<IP_publique>:3000)