---
title: "Pipeline CI/CD Azure + Terraform"
excerpt: "Provisionnement Azure via Terraform et déploiements GitHub Actions — de dev à prod."
header:
  teaser: /assets/images/p1_teaser.jpg    # miniature de la grille
  overlay_image: /assets/images/p1_hero.jpg
tags: [Azure, Terraform, GitHub Actions, IaC, DevOps]
---

## Objectif
Mettre en place une chaîne CI/CD pour provisionner une infra Azure (RG, VNet, Subnets, Storage, Key Vault...) avec Terraform, puis déployer une app.

## Architecture
![Diagramme]({{ "/assets/images/p1_diagram.png" | relative_url }})

## Étapes
1. Repository mono (infra/ + app/). Modules Terraform + variables par environnement.
2. Workflows GitHub Actions: plan/apply, protections de branches, secrets/OIDC.
3. Déploiement applicatif (App Service/Container) + config (Key Vault refs).
4. Observabilité: App Insights + Log Analytics + alertes.

## Démo (YouTube)
<div class="ratio ratio-16x9">
  <iframe src="https://www.youtube.com/embed/ID_DE_TA_VIDEO" title="Démo" allowfullscreen></iframe>
</div>

## Code source
[Voir le repo](https://github.com/stanilpaul/TON-REPO){: .btn .btn--primary target="_blank" rel="noopener" }