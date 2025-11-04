---
title: "Multi-Région Azure avec Peering VNet & DNS Privé : Automatisation Terraform Complète"
excerpt: "Déploiement automatisé de 3 réseaux virtuels Azure dans 3 régions (France, US, Inde), connectés via peering full-mesh, avec résolution DNS interne, VMs Linux/Windows, NSG dynamiques, et gestion de coûts via Spot Instances. Infrastructure as Code avancée avec Terraform."
header:
  overlay_image: /assets/images/project2-terraform-peering-hero.png
  teaser: /assets/images/project2-terraform-peering-teaser.png
tags: [Azure, Terraform, IaC, Virtual Network Peering, Private DNS Zone, Multi-Region, Cloud Engineer, DevOps, NSG, Bastion Alternative, Spot VM, Cloud-init, DNS Resolution]
toc: true
toc_sticky: true
classes: wide
completion_date: 2025-11-04
github_repo: https://github.com/stanilpaul/terraform_azure_labs/tree/main/1.Virtual_Network_Peering_Three_Different_regions%2BPrivate_DNS_Zone
---

<video autoplay muted loop playsinline controls preload="metadata" width="100%">
  <source src="{{ '/assets/videos/demo-pro2-terra-peering.mp4' | relative_url }}" type="video/mp4">
  Votre navigateur ne supporte pas la vidéo.
</video>

> 📅 **Date de réalisation** : {{ page.completion_date | date: "%d %B %Y" }}

---

## 🎯 Problématique & Contexte métier

> *Comment connecter des infrastructures cloud déployées dans plusieurs régions géographiques, tout en permettant une résolution de noms interne transparente, sécurisée, et gérée via Infrastructure as Code ?*

### Le défi

Dans un scénario multi-région (ex: filiales internationales, DRP, compliance géo), on doit :
- Déployer des **réseaux isolés mais interconnectés**
- Permettre aux services de **communiquer entre régions sans passer par Internet**
- Offrir une **résolution DNS interne cohérente** (`service-us.paul.lab`, `db-india.paul.lab`)
- Gérer les **accès sécurisés** (NSG par subnet, pas de ports ouverts inutilement)
- Optimiser les **coûts** (Spot VMs, sizing adapté)
- Automatiser **tout le cycle de vie** → reproductibilité, audit, rollback

👉 Ce projet répond à tous ces besoins avec une seule commande `terraform apply`.

---

## 📸 Galerie de captures d’écran

<div class="screenshots-grid">
  <a href="{{ '/assets/images/pro2-terra-peering/architecture.png' | relative_url }}" target="_blank" title="Architecture Globale">
    <img src="{{ '/assets/images/pro2-terra-peering/architecture.png' | relative_url }}" alt="Architecture Globale" loading="lazy" />
    <span>Architecture Globale</span>
  </a>
  <a href="{{ '/assets/images/pro2-terra-peering/peering-links.png' | relative_url }}" target="_blank" title="Peering Full Mesh">
    <img src="{{ '/assets/images/pro2-terra-peering/peering-links.png' | relative_url }}" alt="Peering Full Mesh" loading="lazy" />
    <span>Peering Full Mesh</span>
  </a>
  <a href="{{ '/assets/images/pro2-terra-peering/dns-zone.png' | relative_url }}" target="_blank" title="Private DNS Zone">
    <img src="{{ '/assets/images/pro2-terra-peering/dns-zone.png' | relative_url }}" alt="Private DNS Zone" loading="lazy" />
    <span>Private DNS Zone</span>
  </a>
  <a href="{{ '/assets/images/pro2-terra-peering/linux-web.png' | relative_url }}" target="_blank" title="Apache2 Linux VM">
    <img src="{{ '/assets/images/pro2-terra-peering/linux-web.png' | relative_url }}" alt="Apache2 Linux VM" loading="lazy" />
    <span>Apache2 Linux VM</span>
  </a>
  <a href="{{ '/assets/images/pro2-terra-peering/windows-iis.png' | relative_url }}" target="_blank" title="IIS Windows VM">
    <img src="{{ '/assets/images/pro2-terra-peering/windows-iis.png' | relative_url }}" alt="IIS Windows VM" loading="lazy" />
    <span>IIS Windows VM</span>
  </a>
  <a href="{{ '/assets/images/pro2-terra-peering/nsg-rules.png' | relative_url }}" target="_blank" title="NSG Rules">
    <img src="{{ '/assets/images/pro2-terra-peering/nsg-rules.png' | relative_url }}" alt="NSG Rules" loading="lazy" />
    <span>NSG Rules</span>
  </a>
  <a href="{{ '/assets/images/pro2-terra-peering/plan-output.png' | relative_url }}" target="_blank" title="Terraform Plan">
    <img src="{{ '/assets/images/pro2-terra-peering/plan-output.png' | relative_url }}" alt="Terraform Plan" loading="lazy" />
    <span>Terraform Plan</span>
  </a>
  <a href="{{ '/assets/images/pro2-terra-peering/apply-success.png' | relative_url }}" target="_blank" title="Apply Success">
    <img src="{{ '/assets/images/pro2-terra-peering/apply-success.png' | relative_url }}" alt="Apply Success" loading="lazy" />
    <span>Apply Success</span>
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

✅ Déployer **3 VNets dans 3 régions Azure** (France Central, East US, Central India)  
✅ Créer un **peering full-mesh** (tous les VNets interconnectés) avec `setproduct()`  
✅ Configurer des **subnets public/private** avec NSG adaptés (RDP/HTTP uniquement en public)  
✅ Déployer **VMs Linux (Ubuntu) dans les subnets privés** → Apache2 via `cloud-init`  
✅ Déployer **VMs Windows (Server 2022) dans les subnets publics** → IIS via Custom Script Extension  
✅ Utiliser des **Spot Instances** pour réduire les coûts de test  
✅ Mettre en place une **zone DNS privée** (`paul.lab`) hébergée en France, liée à tous les VNets  
✅ Créer des **enregistrements A dynamiques** pour toutes les VMs → résolution par nom  
✅ Appliquer des **naming conventions** et **tags** cohérents  
✅ Utiliser **des variables dynamiques (maps)** → extensible à N régions/subnets  
✅ Éviter `count` → privilégier `for_each` partout  
✅ Sécuriser les secrets avec `sensitive = true`

---

## 🏗️ Architecture globale

### Schéma d’architecture

<div style="overflow-x:auto; text-align:center;">
  <a href="{{ '/assets/images/3VnetPeering.svg' | relative_url }}" target="_blank">
    <img src="{{ '/assets/images/3vnetpeering.svg' | relative_url }}" 
         style="width:100%; max-width: 1400px; height:auto; border: 1px solid #eee; border-radius: 8px;" 
         alt="Architecture Terraform Azure Multi-Région Peering + DNS">
  </a>
  <p><em>Cliquez pour agrandir</em></p>
</div>

<div style="overflow-x:auto; text-align:center;">
  <a href="{{ '/assets/images/diagram-projec1.svg' | relative_url }}" target="_blank">
    <img src="{{ '/assets/images/diagram-projec1.svg' | relative_url }}" 
         style="width:100%; max-width: 1200px; height:auto; border: 1px solid #eee; border-radius: 8px;" 
         alt="Architecture Terraform Azure Multi-Région Peering + DNS">
  </a>
  <p><em>Cliquez pour agrandir</em></p>
</div>
---

## 🧩 Découpage logique du code Terraform

Le code est entièrement modulaire via des **blocs dynamiques** pilotés par une seule variable map :

```hcl
vnets = {
  france = {
    region    = "francecentral"
    vnet_cidr = "10.0.0.0/16"
    subnets = {
      "public"  = "10.0.0.0/24"
      "private" = "10.0.1.0/24"
    }
  },
  india = { ... },
  us = { ... }
}
```

### 1. Resource Groups & VNets

```hcl
resource "azurerm_resource_group" "this" { for_each = var.vnets ... }
resource "azurerm_virtual_network" "this" { for_each = var.vnets ... }
```

→ Un RG + un VNet par région, nommés automatiquement (rg-france, vnet-france, etc.)

### 2. Subnets & NSG

```hcl
resource "azurerm_subnet" "this" { 
      for_each = merge([
    for key, value in var.vnets : {
      for x, y in value.subnets :
      "${key}-${x}" => {
        vnet_key    = key # ex: france, us, india
        subnet_name = x   # ex: private/public
        cidr        = y   # "10.0.0.0/24"
      }
    }
  ]...)
  ...
 }
resource "azurerm_network_security_group" "nsg" {
  dynamic "security_rule" {
    for_each = each.value.is_public ? ["rdp_rule"] : []
    ...
  }
}
```

→ Les NSG sont créés conditionnellement : règles RDP/HTTP uniquement sur les subnets publics.

### 3. Peering Full-Mesh

```hcl
resource "azurerm_virtual_network_peering" "this" {
  for_each = {
    for pair in setproduct(keys(var.vnets), keys(var.vnets)) :
    "${pair[0]}-to-${pair[1]}" => { ... }
    if pair[0] != pair[1]
  }
  ...
}
```

→ Tous les VNets sont peerés entre eux → communication cross-région directe et sécurisée.

### VMs Linux (Apache2)

```hcl
resource "azurerm_linux_virtual_machine" "ubuntu" {
  custom_data = base64encode(templatefile("web-server-cloud-init.txt", { ... }))
}
```

→ Script `cloud-init` injecté pour installer Apache2 et afficher un message personnalisé par région.

### 5. VMs Windows (IIS) + Spot Instance

```hcl
resource "azurerm_windows_virtual_machine" "windows" {
  priority        = "Spot"
  eviction_policy = "Deallocate"
  ...
}
resource "azurerm_virtual_machine_extension" "windows_iis" {
  settings = jsonencode({
    commandToExecute = "powershell -Command \"Install-WindowsFeature Web-Server...\""
  })
}
```

→ Coût réduit grâce au mode Spot + installation automatisée d’IIS.

### 6. Private DNS Zone + Records

```hcl
resource "azurerm_private_dns_zone" "internal" { name = var.domainename ... }
resource "azurerm_private_dns_a_record" "ubuntu" {
  records = [ azurerm_linux_virtual_machine.ubuntu[each.key].private_ip_address ]
}
```

→ Résolution DNS interne fonctionnelle : `ping apache2-us.paul.lab` depuis n’importe quelle VM.

---

## 🔄 Workflow de déploiement

```bash
git clone https://github.com/stanilpaul/terraform_azure_labs.git
cd terraform_azure_labs/1.Virtual_Network_Peering_Three_Different_regions+Private_DNS_Zone

az login
terraform init
terraform validate
terraform plan
terraform apply -auto-approve

# 5. Test manuel :
#   - RDP vers la VM Windows publique via son IP publique
#   - Depuis cette VM, accède aux sites Apache via leurs noms DNS :
#     → http://apache2-france.paul.lab
#     → http://apache2-us.paul.lab
#     → http://apache2-india.paul.lab
```

**⏱️ Temps de déploiement total : ~10 minutes**
**⏱️ Temps manuel équivalent : 1h20 (comme documenté dans les étapes manuelles)**

---

## 🛠️ Technologies & Outils utilisés

| **Catégorie** | **Outils & Technologies** |
|----------------|---------------------------|
| **Cloud** | Microsoft Azure (Multi-Region) |
| **IaC** | Terraform v1.3+, for_each, setproduct, merge, templatefile |
| **Langage** | HCL (HashiCorp Language) |
| **OS** | Ubuntu 22.04 LTS, Windows Server 2022 |
| **Init Scripts** | Cloud-init (Linux), CustomScriptExtension (Windows) |
| **Réseau** | VNet Peering, NSG, Private DNS Zone, Public IPs |
| **Coûts** | Spot Instances pour Windows VM |
| **Sécurité** | NSG conditionnels, pas de SSH/RDP exposé sauf besoin |
| **Validation** | terraform validate, tests manuels post-déploiement |

---

## ✅ Résultat fonctionnel

- ☑️ 3 VNets déployés dans 3 régions, totalement interconnectés via peering
- ☑️ Communication cross-région sans passer par Internet (latence optimale, sécurité accrue)
- ☑️ Résolution DNS interne fonctionnelle entre toutes les VMs
- ☑️ Sites web accessibles :
  - Via IP publique (Windows IIS)
  - Via nom DNS interne (Linux Apache2, depuis la VM Windows)
- ☑️ NSG appliqués correctement : seul le trafic nécessaire est autorisé
- ☑️ Coûts optimisés grâce aux Spot Instances
- ☑️ Infrastructure 100% reproductible, versionnable, et documentée

### Démonstration vidéo (2 min)

Dans la vidéo :

- Je lance le terraform apply complet
- Je montre les ressources créées dans le portail Azure
- Je fais un RDP vers la VM Windows
- Depuis celle-ci, je ping les VMs Linux par leur nom DNS
- J’ouvre les sites Apache via Edge en utilisant les URLs DNS
- Je valide que tout est interconnecté et fonctionnel

➡️ Preuve que l’automatisation Terraform remplace avantageusement les déploiements manuels.

---

## 📈 Bonnes pratiques mises en œuvre

| **Pratique** | **Implémentation dans le projet** |
|---------------|-----------------------------------|
| **Infrastructure as Code** | ☑️ 100% Terraform |
| **Dynamisme & Extensibilité** | ☑️ Ajouter une région ? Juste modifier la map `vnets` |
| **Sécurité réseau** | ☑️ NSG conditionnels, pas de ports inutiles ouverts |
| **Gestion des coûts** | ☑️ Spot VM pour les environnements non prod |
| **Naming convention** | ☑️ `rg-{region}`, `vnet-{region}`, `vm-{os}-{region}` |
| **Résolution de noms** | ☑️ Private DNS Zone + enregistrements A dynamiques |
| **Évitement de count** | ☑️ `for_each` utilisé partout |
| **Documentation implicite** | ☑️ Variables bien typées + descriptions |
| **Sécurité des secrets** | ☑️ `admin_password` marqué comme sensitive |
| **Reproductibilité** | ☑️ `terraform destroy` puis `apply` → même résultat |

---

## 🚧 Limites & Axes d’amélioration

| **Ce que j’ai fait** | **Ce qu’on ferait en production** |
|------------------------|-----------------------------------|
| Mot de passe en clair dans `tfvars` | ➤ Azure Key Vault + `azurerm_key_vault_secret` |
| Accès RDP depuis Internet | ➤ Azure Bastion ou P2S VPN |
| Pas de CI/CD | ➤ Pipeline GitHub Actions pour apply auto sur PR merge |
| Pas de monitoring | ➤ Azure Monitor + alertes sur uptime VM |
| Pas de backup | ➤ Azure Backup pour les disques OS/data |
| Script IIS basique | ➤ DSC ou Ansible pour une configuration plus robuste |
| Pas de tests automatisés | ➤ Terratest pour valider la connectivité cross-région |

---

## 📚 Sources & Inspirations

- [Microsoft Learn - VNet Peering](https://learn.microsoft.com/en-us/azure/virtual-network/virtual-network-peering-overview)
- [Microsoft Learn - Private DNS Zones](https://learn.microsoft.com/en-us/azure/dns/private-dns-overview)
- [HashiCorp Learn - Dynamic Blocks](https://developer.hashicorp.com/terraform/language/expressions/dynamic-blocks)
- [Azure Spot VMs Documentation](https://learn.microsoft.com/en-us/azure/virtual-machines/spot-vms)

🧑‍💻 Pourquoi ce projet compte pour mon profil d’ingénieur cloud

> “Ce projet n’est pas juste un lab technique. C’est une démonstration concrète de ma capacité à :”

- ☑️ Concevoir des architectures multi-région complexes avec Terraform
- ☑️ Maîtriser les fonctions avancées de HCL (setproduct, merge, templatefile)
- ☑️ Automatiser des scénarios réalistes d’entreprise (interconnexion, DNS, sécurité)
- ☑️ Optimiser les coûts sans sacrifier la fonctionnalité (Spot VMs)
- ☑️ Produire du code propre, maintenable, et extensible
- ☑️ Documenter rigoureusement mes choix techniques → valeur ajoutée pour les équipes

---

## 📎 Annexes

- [Ce projet](https://github.com/stanilpaul/terraform_azure_labs/tree/master/1.Virtual_Network_Peering_Three_Different_regions%2BPrivate_DNS_Zone)

---

## 🧠 Ce que j’ai appris grâce à ce projet

> “L’automatisation révèle les failles invisibles en manuel.”

-  Maîtriser setproduct() pour générer des combinaisons (ici, peerings full-mesh)
-  Comprendre les limites des for_each imbriqués → solution avec merge([...])
-  Gérer les dépendances implicites (ex: DNS records après création des VMs → depends_on)
-  Utiliser try() pour éviter les erreurs si une ressource n’existe pas encore
-  La puissance du templatefile() pour injecter du contexte dans les scripts
-  L’importance de la convention de nommage des clés ("${region}-${subnet}") pour référencer facilement les ressources

➡️ Ce projet confirme ma transition vers un ingénieur cloud capable de concevoir, automatiser, et industrialiser des architectures multi-région sécurisées.