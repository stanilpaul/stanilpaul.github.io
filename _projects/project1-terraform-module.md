---
title: "Architecture modulaire Azure avec Terraform : Networking, Compute, Load Balancing & Bastion"
excerpt: "Projet complet d'infrastructure as code (IaC) sur Azure avec Terraform. Découpage en modules indépendants (Networking, Compute, LB, Bastion), gestion de state files séparés, respect des bonnes pratiques DevOps et sécurité. Simule une collaboration entre équipes IT dans un environnement de production."
header:
  overlay_image: /assets/images/terraform-azure-hero.jpg
  teaser: /assets/images/terraform-azure-teaser.png
tags: [Azure, Terraform, IaC, Infrastructure as Code, Cloud Engineer, DevOps, Modular Architecture, Remote State, Load Balancer, Bastion, NSG, Cloud-init]
toc: true
toc_sticky: true
classes: wide
completion_date: 2025-09-30
github_repo: https://github.com/stanilpaul/project1_terraform_module
tf_registry: https://registry.terraform.io/search/modules?q=stanilpaul
---

<video autoplay muted loop playsinline controls preload="metadata" width="100%">
  <source src="{{ '/assets/videos/demo-pro1-terra-module.mp4' | relative_url }}" type="video/mp4">
  Votre navigateur ne supporte pas la vidéo.
</video>

> 📅 **Date de réalisation** : {{ page.completion_date | date: "%d %B %Y" }}

---

## 🎯 Problématique & Contexte métier

> *Comment concevoir une infrastructure cloud sécurisée, reproductible, et maintenable par plusieurs équipes métiers, tout en respectant les bonnes pratiques DevOps et les standards de production ?*

### Le défi

En entreprise, les infrastructures cloud ne sont pas gérées par une seule personne. Elles impliquent :
- Une **équipe réseau** (VNet, NSG, NAT, IPs)
- Une **équipe compute** (VMs, disques, scripts d’initialisation)
- Une **équipe SRE/Infra** (Load Balancers, monitoring, scalabilité)
- Une **équipe support/sécurité** (accès bastion, audit)

Souvent, ces équipes doivent :
- Travailler **indépendamment**
- Partager des **outputs sans se bloquer**
- Garantir la **sécurité des états et secrets**
- Pouvoir **ajouter/supprimer des ressources dynamiquement**

👉 Ce projet simule exactement ce scénario avec Terraform, en créant **4 modules indépendants**, chacun avec son propre **remote state file**, comme dans un vrai environnement de production.

---

## 📸 Galerie de captures d’écran

<div class="screenshots-grid">
  <a href="{{ '/assets/images/pro1-terra-module/public_module.png' | relative_url }}" target="_blank" title="Public Terraform Module">
    <img src="{{ '/assets/images/pro1-terra-module/public_module.png' | relative_url }}" alt="Public Terraform Module" loading="lazy" />
    <span>Public Terraform Module</span>
  </a>
  <a href="{{ '/assets/images/pro1-terra-module/private_module.png' | relative_url }}" target="_blank" title="Private Terraform Module">
    <img src="{{ '/assets/images/pro1-terra-module/private_module.png' | relative_url }}" alt="Private Terraform Module" loading="lazy" />
    <span>Private Terraform Module</span>
  </a>
  <a href="{{ '/assets/images/pro1-terra-module/github.png' | relative_url }}" target="_blank" title="GitHub Repos">
    <img src="{{ '/assets/images/pro1-terra-module/github.png' | relative_url }}" alt="GitHub" loading="lazy" />
    <span>GitHub Repos</span>
  </a>
  <a href="{{ '/assets/images/pro1-terra-module/networking.png' | relative_url }}" target="_blank" title="Networking Module">
    <img src="{{ '/assets/images/pro1-terra-module/networking.png' | relative_url }}" alt="Networking" loading="lazy" />
    <span>Networking</span>
  </a>
  <a href="{{ '/assets/images/pro1-terra-module/compute.png' | relative_url }}" target="_blank" title="Compute Module">
    <img src="{{ '/assets/images/pro1-terra-module/compute.png' | relative_url }}" alt="Compute" loading="lazy" />
    <span>Compute</span>
  </a>
  <a href="{{ '/assets/images/pro1-terra-module/lb.png' | relative_url }}" target="_blank" title="Load Balancing Module">
    <img src="{{ '/assets/images/pro1-terra-module/lb.png' | relative_url }}" alt="Load balancing" loading="lazy" />
    <span>Load Balancing</span>
  </a>
  <a href="{{ '/assets/images/pro1-terra-module/bastion.png' | relative_url }}" target="_blank" title="Bastion Module">
    <img src="{{ '/assets/images/pro1-terra-module/bastion.png' | relative_url }}" alt="Bastion" loading="lazy" />
    <span>Bastion</span>
  </a>
  <a href="{{ '/assets/images/pro1-terra-module/backend_github.png' | relative_url }}" target="_blank" title="Backend GitHub">
    <img src="{{ '/assets/images/pro1-terra-module/backend_github.png' | relative_url }}" alt="Backend Github" loading="lazy" />
    <span>Backend GitHub</span>
  </a>
  <a href="{{ '/assets/images/pro1-terra-module/network_apply.png' | relative_url }}" target="_blank" title="Network Apply">
    <img src="{{ '/assets/images/pro1-terra-module/network_apply.png' | relative_url }}" alt="Network Apply" loading="lazy" />
    <span>Network Apply</span>
  </a>
  <a href="{{ '/assets/images/pro1-terra-module/4containers.png' | relative_url }}" target="_blank" title="4 State Containers">
    <img src="{{ '/assets/images/pro1-terra-module/4containers.png' | relative_url }}" alt="4 Containers" loading="lazy" />
    <span>4 Containers</span>
  </a>
  <a href="{{ '/assets/images/pro1-terra-module/remote-state.png' | relative_url }}" target="_blank" title="Remote State Files">
    <img src="{{ '/assets/images/pro1-terra-module/remote-state.png' | relative_url }}" alt="Remote state" loading="lazy" />
    <span>Remote State</span>
  </a>
  <a href="{{ '/assets/images/pro1-terra-module/web1.png' | relative_url }}" target="_blank" title="Web Site 1 (External LB)">
    <img src="{{ '/assets/images/pro1-terra-module/web1.png' | relative_url }}" alt="Web 1" loading="lazy" />
    <span>Web 1 (External)</span>
  </a>
  <a href="{{ '/assets/images/pro1-terra-module/web2.png' | relative_url }}" target="_blank" title="Web Site 2 (Internal LB)">
    <img src="{{ '/assets/images/pro1-terra-module/web2.png' | relative_url }}" alt="Web 2" loading="lazy" />
    <span>Web 2 (Internal)</span>
  </a>
</div>

<style>
.screenshots-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 20px;
  padding: 20px 0;
  margin: 32px 0;
}

.screenshots-grid a {
  display: flex;
  flex-direction: column;
  text-decoration: none;
  color: #333;
  transition: transform 0.2s ease;
}

.screenshots-grid a:hover {
  transform: translateY(-4px);
}

.screenshots-grid img {
  width: 100%;
  height: 200px;
  object-fit: cover;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0,0,0,0.1);
  transition: box-shadow 0.2s ease;
}

.screenshots-grid a:hover img {
  box-shadow: 0 8px 16px rgba(0,0,0,0.15);
}

.screenshots-grid span {
  margin-top: 8px;
  font-size: 0.9em;
  text-align: center;
  font-weight: 500;
  color: #555;
}

@media (max-width: 768px) {
  .screenshots-grid {
    grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
    gap: 16px;
  }
  .screenshots-grid img {
    height: 160px;
  }
  .screenshots-grid span {
    font-size: 0.85em;
  }
}
</style>

---

## 💡 Objectifs techniques

✅ Concevoir une architecture modulaire avec **Terraform**  
✅ Utiliser **des state files séparés** stockés dans Azure Blob Storage  
✅ Appliquer le principe de **responsabilité unique par module**  
✅ Automatiser le déploiement de VMs avec **cloud-init** (Apache2)  
✅ Mettre en place **2 load balancers** (externe + interne)  
✅ Gérer les accès via **NSG + Bastion + NAT Gateway**  
✅ Standardiser les noms, tags, et plages IP  
✅ Valider le code avec **TF Lint**  
✅ Générer automatiquement la **documentation (README.md)** avec `terraform-docs`  
✅ Publier les modules sur **Terraform Registry + GitHub**  
✅ Éviter `count`, privilégier les **map objects dynamiques**  
✅ Rendre l’infrastructure **extensible** (n VMs, n subnets, etc.)

---

## 🏗️ Architecture globale

### Schéma d’architecture

<div style="overflow-x:auto; text-align:center;">
  <a href="{{ '/assets/images/terraform-module-pro1.svg' | relative_url }}" target="_blank">
    <img src="{{ '/assets/images/terraform-module-pro1.svg' | relative_url }}" 
         style="width:100%; max-width: 1200px; height:auto; border: 1px solid #eee; border-radius: 8px;" 
         alt="Architecture Terraform Azure Modulaire">
  </a>
  <p><em>Cliquez pour agrandir</em></p>
</div>

---

## 🧩 Modules détaillés

Chaque module représente une équipe métier, avec son propre cycle de vie, ses permissions, et son state file.


### 1. Module `networking-project1` → Équipe Réseau

🔗 [GitHub](https://github.com/stanilpaul/terraform-azurerm-networking-project1)

#### Responsabilités :
- Création du **Resource Group**
- Déploiement du **VNet + 4 subnets** (auto-calculés via `cidrsubnet`)
- Attribution d’un **NSG par subnet** (règles standardisées via map)
- Création de **Public IPs** (pour LB externe + NAT Gateway)
- Mise en place de la **NAT Gateway** (accès sortant pour VMs internes)
- Application de **tags** sur toutes les ressources

#### Inputs requis:
* location
* nat_name
* nsg_rules_simple
* nsg_rules_simple
* rg_name
* subnets
* vnet_address_space
* vnet_name

#### Outputs exposés :
```hcl
resource_group, vnet_details, subnets_details, public_ip_details, nsg_details, nat_details
```

### 2. Module `compute-web-tier-project1` → Équipe Infrastructure / VMs

🔗 [GitHub](https://github.com/stanilpaul/terraform-azurerm-compute-web-tier-project1)

#### Responsabilités :
- Création de **VMs Linux (Ubuntu 22.04 LTS)** via map dynamique
- Association à **un subnet spécifique**
- Ajout de **disques de données** persistants
- Installation d’**Apache2 via cloud-init**
- Génération de **NICs** avec NSG attaché
- Tags + noms standardisés

#### Inputs requis:
* instances
* location
* rg_name
* tags

#### Outputs exposés :
```hcl
disk_details, nic_details, vm_details
```

### 3. Module `load-balancing-project1` → Équipe SRE / Infra

🔗 [GitHub](https://github.com/stanilpaul/terraform-azurerm-load-balancing-project1)

#### Responsabilités :
- Création d’un **Load Balancer externe** (accès public sur port 80 → VM1)
- Création d’un **Load Balancer interne** (accès interne → VM2)
- Configuration des **rules, probes, backend pools**
- Sécurisation via **NSG implicite** (seulement port 80 autorisé)

#### Inputs requis:
* internal_lb_name
* internal_subnet_id
* internal_vm_nics
* location
* name_external_lb
* public_ip_id
* public_vm_nics
* rg_name
* tags

#### Outputs exposés :
```hcl
external_lb_details, internal_lb_details
```

### 4. Module `bastion-project1` →  Équipe Support / Sécurité

🔗 [GitHub](https://github.com/stanilpaul/terraform-azurerm-bastion-project1)

#### Responsabilités :
- Création d’un **subnet dédié Bastion**
- Déploiement du service **Azure Bastion**
- Attribution d’une **IP publique dédiée**
- Accès sécurisé aux VMs **sans exposer de ports RDP/SSH**

#### Inputs requis:
* bastion_ip_name
* bastion_name
* bastion_subnet_cidr
* location
* rg_name
* vnet_name
* tags

#### Outputs exposés :
```hcl
bastion_details
```

---

## 🔄 Workflow de déploiement (Remote State Files)

Chaque module lit uniquement les states dont il a besoin → **dépendances explicites et contrôlées**.

### 4 containers Azure distincts :
- `network-terraform-state`
- `vm-terraform-state`
- `loadbalancing-terraform-state`
- `bastion-terraform-state`

### Sécurité : 

Les tokens et secrets ne sont jamais commités (`.tfvars` local, `.gitignore` strict).

---

## 🛠️ Technologies & Outils utilisés


| Catégorie      | Outils & Technologies                                     |
|----------------|-----------------------------------------------------------|
| **Cloud**      | Microsoft Azure                                           |
| **IaC**        | Terraform v1.3+, Modules, Remote State                    |
| **Langage**    | HCL (HashiCorp Language)                                  |
| **Validation** | TF Lint, `terraform validate`                             |
| **Documentation** | terraform-docs, README.md auto-généré                  |
| **Versioning** | Git, GitHub, Tags SemVer                                  |
| **Publication**| Terraform Registry (Public & Private)                     |
| **OS**         | Ubuntu 22.04 LTS (remplacement de 18.04 EOL)              |
| **Init Scripts** | Cloud-init (Apache2 install)                            |
| **Réseau**     | VNet, Subnets, NSG, NAT Gateway, Public IPs, Load Balancers |
| **Sécurité**   | Bastion Host, Tags, RBAC implicite via modules            |


--- 

## ✅ Résultat fonctionnel

* ✅ Accès public via Load Balancer externe → VM1 (site web Apache)
* ✅ Accès interne via Load Balancer interne → VM2 (site web privé)
* ✅ VM2 peut faire apt update grâce à la NAT Gateway
* ✅ Accès sécurisé aux VMs via Azure Bastion (pas de ports ouverts)
* ✅ Toutes les ressources taggées → traçabilité et coûts
* ✅ Ajout/suppression de VMs ou subnets → modification simple de la map d’entrée


---

### Démonstration vidéo (3 min)


Dans la vidéo :
- Je montre le **workflow de déploiement module par module**
- La **connexion au site web public** via LB externe
- L’accès **interne au site privé** via LB interne
- La connexion **sécurisée via Bastion**
- Le contenu des **state files dans Azure Storage Explorer**
  
➡️ Preuve que l’architecture est opérationnelle, modulaire, et sécurisée.


---

## 📈 Bonnes pratiques mises en œuvre


| Pratique                     | Implémentation dans le projet                          |
|-------------------------------|-------------------------------------------------------|
| **Infrastructure as Code**    | ✅ 100% Terraform                                      |
| **Modularité**                | ✅ 4 modules indépendants                              |
| **Remote State**              | ✅ Backend Azure, 4 state files                        |
| **Sécurité des secrets**      | ✅ .tfvars non versionné, sensitive outputs            |
| **Extensibilité**             | ✅ Maps dynamiques (n VMs, n subnets)                  |
| **Documentation automatique** | ✅ terraform-docs → README.md                          |
| **Validation syntaxique**     | ✅ TF Lint + `terraform validate`                      |
| **Naming convention**         | ✅ Standard RG-VNET-VM-LB-BASTION                      |
| **Tagging**                   | ✅ Environnement, Owner, Project sur toutes ressources |
| **Évitement de count**        | ✅ Utilisation exclusive de `for_each` + maps          |
| **Versioning des modules**    | ✅ Tags SemVer sur GitHub + Registry                   |
| **Collaboration multi-équipes** | ✅ Simulée via découpage modules/state                |


---

## 🚧 Limites & Axes d’amélioration


| Ce que j’ai fait                        | Ce qu’on ferait en production                               |
|-----------------------------------------|-------------------------------------------------------------|
| **Mot de passe en clair dans tfvars**   | ➤ Azure Key Vault + `azurerm_key_vault_secret`             |
| **Cloud-init basique**                  | ➤ Ansible / Packer pour images custom                      |
| **Pas de CI/CD**                        | ➤ Azure DevOps / GitHub Actions pour `terraform apply` auto |
| **Monitoring absent**                   | ➤ Azure Monitor + Alertes sur métriques VM/LB               |
| **Pas de tests automatisés**            | ➤ Terratest pour valider connectivité / règles NSG          |
| **Modules publiés manuellement**        | ➤ Release automatisée via GitHub Actions                    |

---

## 📚 Sources & Inspirations

- [Chief Architect @ Microsoft](https://www.youtube.com/watch?v=esvtvKB8LSQ&list=PLk-ELTMns8FZc9FuzeMv-Xg0UaMS6_6jq)
- [Microsoft Learn](https://learn.microsoft.com/en-us/azure/developer/terraform/)
- [HashiCorp Learn](https://learn.microsoft.com/en-us/azure/developer/terraform/)
- [Mes labs personnels](https://github.com/stanilpaul/learning_terraform_2nd_time)

🧑‍💻 Pourquoi ce projet compte pour mon profil d’ingénieur cloud

> *“Ce projet n’est pas juste un **lab**.  
> C’est une simulation de production réelle qui démontre :”*


* Ma maîtrise de Terraform avancé (modules, remote state, variables dynamiques)
* Ma capacité à structurer une infrastructure complexe pour des équipes multiples
* Mon attention aux bonnes pratiques DevOps (sécurité, validation, documentation)
* Ma rigueur dans la gestion des dépendances et des états
* Mon autonomie pour résoudre des erreurs complexes (ex: image Ubuntu EOL, outputs sensibles, etc.)
* Mon souci de qualité et professionnalisme (lint, docs auto, tags, naming)


---

## 📎 Annexes

- [📁 Code source complet du projet](https://github.com/stanilpaul/project1_terraform_module)
- [📁 Code source Module Networking](https://github.com/stanilpaul/terraform-azurerm-networking-project1)
- [📁 Code source Module Compute](https://github.com/stanilpaul/terraform-azurerm-compute-web-tier-project1)
- [📁 Code source Module Load Balancing](https://github.com/stanilpaul/terraform-azurerm-load-balancing-project1)
- [📁 Code source Module Bastion](https://github.com/stanilpaul/terraform-azurerm-bastion-project1)
- [📁 Code Source Préparation pour ce projet](https://github.com/stanilpaul/learning_terraform_2nd_time)
- [📦 Modules Terraform](https://registry.terraform.io/namespaces/stanilpaul)

---

## 🚀 Prochaines étapes

- Intégrer Azure Key Vault pour les secrets
- Ajouter du CI/CD avec GitHub Actions
- Écrire des tests d’intégration avec Terratest
- Containeriser les apps avec Docker + Azure Container Instances
- Ajouter du monitoring avec Azure Monitor + Grafana

---

## 🧠 Ce que j’ai appris grâce à ce projet

> *“Les erreurs ont été mes meilleurs professeurs.”*

- ✅ Gérer les dépendances entre modules sans créer de spaghetti
- ✅ Comprendre pourquoi Ubuntu 18.04 disparaît soudainement 😅 → gestion du cycle de vie des images
- ✅ Maîtriser `sensitive = true` et ne jamais exposer un mot de passe par accident
- ✅ Automatiser la doc avec `terraform-docs` → gagner 2h/semaine en maintenance
- ✅ Travailler avec des state files séparés → éviter les conflits en équipe
- ✅ Simuler un workflow multi-équipes → penser comme un architecte, pas juste un dev

➡️ Ce projet m’a transformé d’un utilisateur de Terraform à un **concepteur d’infrastructures modulaires**.