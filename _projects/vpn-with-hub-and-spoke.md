---
title: "Architecture Hub & Spoke avec S2S et P2S VPN sur Azure"
excerpt: "Implémentation complète d’un réseau sécurisé Azure : connexion Site-to-Site (avec simulation On-Prem) + Point-to-Site via certificat auto-signé. Architecture Hub & Spoke avec peering VNet, NSG granulaires, et démonstration de connectivité bout-en-bout."
header:
  overlay_image: /assets/images/vpn-hub-spoke-hero.png
  teaser: /assets/images/vpn-hub-spoke-teaser.png
tags: [Azure, Networking, VPN, Hub and Spoke, S2S, P2S, Virtual Network, NSG, Infrastructure, Cloud Engineer]
toc: true
toc_sticky: true
classes: wide
completion_date: 2025-09-16
---

<video autoplay muted loop playsinline preload="metadata" width="100%">
  <source src="{{ '/assets/videos/vpn-final.mp4' | relative_url }}" type="video/mp4">
</video>

> 📅 **Date de réalisation** : {{ page.completion_date | date: "%d %B %Y" }}

## Objectif du projet
 
> *Simuler une infrastructure d’entreprise réelle en combinant les meilleures pratiques Azure Networking :*
> - Connecter un environnement **“On-Premises” simulé** à Azure via **Site-to-Site VPN**
> - Permettre aux utilisateurs distants de se connecter via **Point-to-Site VPN**
> - Structurer le réseau Azure selon le modèle **Hub & Spoke**
> - Appliquer des règles de sécurité réseau (**NSG**) strictes
> - Valider la connectivité entre tous les segments (on-prem → hub → spokes)

Ce projet a été réalisé dans un but d’apprentissage approfondi des architectures réseau Azure, en s’appuyant sur la documentation officielle Microsoft Learn et des tutoriels YouTube. Il reflète les compétences attendues d’un **ingénieur infrastructure cloud Azure**.

---

## 🧭 Architecture globale

### Architecture diagram

<div style="overflow-x:auto;">
  <a href="{{ '/assets/images/vpn-d.svg' | relative_url }}" target="_blank">
    <img src="{{ '/assets/images/vpn-d.svg' | relative_url }}" 
         style="width:100%; height:auto;" 
         alt="Diagramme Infra Azure">
  </a>
</div>


### Vue d’ensemble

<br>
<div style="overflow-x:auto;">
  <a href="{{ '/assets/images/vpn-3.svg' | relative_url }}" target="_blank">
    <img src="{{ '/assets/images/vpn-3.svg' | relative_url }}" 
         style="width:100%; height:auto;" 
         alt="Diagramme Infra Azure">
  </a>
</div>



### Environnements

| Environnement       | Resource Group     | Address Space   | Subnets                     |
|---------------------|--------------------|-----------------|-----------------------------|
| **On-Prem Simulé**  | `OnPremRG`         | `172.0.0.0/16`  | `workload-subnet (172.0.0.0/24)`, `GatewaySubnet (172.0.1.0/27)` |
| **Azure Hub**       | `AzureRG`          | `10.100.0.0/16` | `workload-subnet (10.100.0.0/24)`, `GatewaySubnet (10.100.1.0/27)` |
| **Spoke 1**         | `AzureRG`          | `10.200.0.0/24` | `workload-subnet (10.200.0.0/24)` |
| **Spoke 2**         | `AzureRG`          | `10.222.0.0/24` | `workload-subnet (10.222.0.0/27)` |

> ⚠️ **Note** : Le “On-Prem” est entièrement simulé dans Azure pour des raisons pratiques. En production, il s’agirait d’un réseau physique ou d’un autre cloud.

---

## 🔌 Connexions réseau

### Peering VNet (Azure interne)
- Hub ↔ Spoke 1
- Hub ↔ Spoke 2
- Spoke 1 ↔ Spoke 2 *(pour simplification — en prod, transit par Hub uniquement)*

### Site-to-Site VPN
- Entre **Virtual Network Gateway (Azure Hub)** et **Local Network Gateway (On-Prem simulé)**
- Protocole : IKEv2
- Clé partagée : configurée manuellement

### Point-to-Site VPN
- Basé sur **certificat auto-signé** (self-signed)
- Téléchargement du client VPN depuis le portail Azure
- Testé depuis une VM VMware totalement externe au réseau Azure

---

## 🔐 Sécurité réseau (NSG)

Tous les **NIC** disposent d’un NSG dédié (pas de NSG au niveau subnet pour plus de granularité).

### Règles appliquées :
- **Trafic interne uniquement** autorisé entre les sous-réseaux Azure (ports ICMP, HTTP 80, etc.)
- **Exception** : VM Windows dans Spoke 2 → Port **RDP 3389** ouvert pour administration
- Aucun accès Internet direct vers les workloads (sauf via Jumpbox)

> 💡 *En production, on utiliserait un firewall centralisé (ex: Azure Firewall) dans le Hub pour forcer tout le trafic transitant entre Spokes à passer par le Hub.*

---

## 🛠️ Étapes de mise en œuvre

### 1. Planification IP
- Attribution des plages CIDR sans chevauchement
- Réservation du `/27` pour chaque `GatewaySubnet` (recommandation Microsoft)

### 2. Déploiement des VNet & Subnets
- Création via portail Azure (pour apprentissage visuel)
- Validation des plages et noms cohérents

### 3. Configuration des Gateways
#### ➤ Virtual Network Gateway (Azure Hub)
- SKU : `VpnGw2AZ`
- Type : Route-based
- IP publique associée

#### ➤ Local Network Gateway (On-Prem simulé)
- Adresse IP publique de la gateway On-Prem
- Espaces d’adressage On-Prem (`172.0.0.0/16`)
- Clé partagée

#### ➤ Connection (S2S)
- Type : Site-to-site (IPsec)
- Association des deux gateways
- Validation de l’état “Connected”

### 4. Point-to-Site (P2S)
- Génération de certificat racine auto-signé (via PowerShell/OpenSSL)
- Upload du certificat public dans la configuration P2S du VNG
- Téléchargement et installation du client VPN sur machine cliente
- Connexion et validation de la route ajoutée

### 5. Tests de connectivité
Depuis la **VM Windows (Spoke 2)** :
- ✅ Ping vers serveurs web dans Hub, Spoke 1, et On-Prem
- ✅ Accès HTTP (port 80) à toutes les pages web

Depuis le **client P2S (VMware)** :
- ✅ Connexion établie au réseau Azure
- ✅ Accès aux serveurs web dans Hub, Spoke 1, Spoke 2
- ❌ Pas d’accès à On-Prem (non configuré pour P2S — normal)

---

## 📺 Démonstration vidéo (4 min)

Dans la vidéo, je montre :
- La topologie finale dans le portail Azure
- La connectivité depuis la Jumpbox Windows vers tous les segments
- L’installation et la connexion du client P2S depuis une machine externe
- La navigation sur les sites web hébergés dans chaque VNet

➡️ **Preuve fonctionnelle que l’architecture est opérationnelle et sécurisée.**

---

## ⚙️ Outils & Technologies utilisés

- **Cloud** : Microsoft Azure
- **Réseau** : VNet, Peering, NSG, Virtual Network Gateway, Local Network Gateway
- **VPN** : Site-to-Site (IPsec/IKEv2), Point-to-Site (certificat)
- **Sécurité** : NSG par NIC, segmentation réseau
- **Validation** : Ping, curl, navigateur web, logs Azure
- **Client P2S** : Généré via portail Azure + certificat auto-signé

---

## 🧩 Limites & améliorations possibles

| Ce que j’ai fait                          | Ce qu’on ferait en production               |
|------------------------------------------|---------------------------------------------|
| Peering direct entre Spokes              | Forcer le transit par le Hub (UDR + Firewall) |
| Certificat auto-signé pour P2S           | PKI d’entreprise ou Azure AD auth            |
| NSG sur NIC seulement                    | NSG + Azure Firewall + Monitoring            |
| Pas de monitoring/logs                   | Azure Monitor + Network Watcher              |
| Pas de HA pour les gateways              | Activer la redondance (active-active)        |
| Simulation On-Prem dans Azure            | Vraie appliance/firewall on-prem (Cisco, Palo Alto, etc.) |

---

## 📚 Sources & Références

- [Microsoft Learn – S2S VPN](https://learn.microsoft.com/fr-fr/azure/vpn-gateway/tutorial-site-to-site-portal)
- [Microsoft Learn – P2S avec certificats](https://learn.microsoft.com/fr-fr/azure/vpn-gateway/point-to-site-certificate-gateway)
- [Génération certificat P2S](https://learn.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-certificates-point-to-site)
- Tutoriels YouTube :
  - [Hub & Spoke Deep Dive](https://www.youtube.com/watch?v=0WgvDeObn8I)
  - [Azure Networking Masterclass](https://www.youtube.com/watch?v=S0j3mOHpuIE&t=3795s)

---

## 🧑‍💻 Pourquoi ce projet compte pour mon profil

> En tant que candidat à un poste d’**ingénieur cloud infrastructure Azure**, ce projet démontre :
> - Ma capacité à concevoir une **architecture réseau complexe et sécurisée**
> - Ma compréhension des **concepts avancés de connectivité hybride (S2S/P2S)**
> - Mon autonomie dans la **mise en œuvre via le portail Azure** (et bientôt via Terraform/Bicep 😊)
> - Mon souci du **détail technique et de la documentation professionnelle**

---

## 📎 Annexes

- [Lien vers la vidéo de démo](#) *(à remplacer par ton lien)*
- [Diagramme d’architecture (PNG/SVG)](/assets/images/diagram-vpn-hub-spoke.png)
- [Fichiers de configuration (optionnel)](lien-vers-github)

---

✅ **Prochaine étape** : Automatiser tout ça avec **Terraform** pour rendre le déploiement reproductible et versionnable !

---