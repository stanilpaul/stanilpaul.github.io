<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CI/CD Jenkins sur Azure avec Terraform | Stanil Paul</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://cdn.jsdelivr.net/npm/mermaid@10.3.0/dist/mermaid.min.js"></script>
    <style>
        :root {
            --primary: #0078d4;
            --secondary: #505a64;
            --accent: #ffb900;
            --light-bg: #f8f9fa;
            --dark-bg: #212529;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            color: #333;
            line-height: 1.6;
        }
        
        .hero-section {
            background: linear-gradient(135deg, #0078d4 0%, #106ebe 100%);
            color: white;
            padding: 4rem 0;
            margin-bottom: 3rem;
        }
        
        .tech-icon {
            font-size: 2.5rem;
            margin: 0 10px;
            color: var(--primary);
        }
        
        .section-title {
            border-left: 5px solid var(--primary);
            padding-left: 15px;
            margin: 2rem 0 1.5rem;
        }
        
        .card {
            border: none;
            border-radius: 8px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.1);
            transition: transform 0.3s ease;
            margin-bottom: 20px;
        }
        
        .card:hover {
            transform: translateY(-5px);
        }
        
        .card-header {
            background-color: var(--primary);
            color: white;
            border-radius: 8px 8px 0 0 !important;
        }
        
        .architecture-diagram {
            background-color: #f8f9fa;
            padding: 20px;
            border-radius: 8px;
            margin: 20px 0;
        }
        
        .learning-box {
            background-color: #e8f4ff;
            border-left: 4px solid var(--primary);
            padding: 20px;
            margin: 30px 0;
            border-radius: 0 8px 8px 0;
        }
        
        .code-block {
            background-color: #2d2d2d;
            color: #f8f9fa;
            padding: 15px;
            border-radius: 5px;
            overflow-x: auto;
            margin: 15px 0;
        }
        
        .tag {
            display: inline-block;
            background-color: #e8f4ff;
            color: var(--primary);
            padding: 5px 10px;
            border-radius: 20px;
            font-size: 0.85rem;
            margin: 0 5px 5px 0;
        }
        
        .nav-pills .nav-link.active {
            background-color: var(--primary);
        }
        
        .step-number {
            display: inline-block;
            width: 40px;
            height: 40px;
            background-color: var(--primary);
            color: white;
            text-align: center;
            line-height: 40px;
            border-radius: 50%;
            margin-right: 10px;
        }
        
        footer {
            background-color: var(--dark-bg);
            color: white;
            padding: 3rem 0;
            margin-top: 4rem;
        }
        
        @media (max-width: 768px) {
            .tech-icon {
                font-size: 2rem;
                margin: 0 5px;
            }
        }
    </style>
</head>
<body>
    <!-- Hero Section -->
    <section class="hero-section">
        <div class="container">
            <div class="row align-items-center">
                <div class="col-md-8">
                    <h1 class="display-4 fw-bold">CI/CD Jenkins sur Azure avec Terraform</h1>
                    <p class="lead">Pipeline DevOps automatisé de bout en bout avec infrastructure as code</p>
                    <div class="mt-4">
                        <span class="tag bg-white text-primary me-2">Azure</span>
                        <span class="tag bg-white text-primary me-2">Terraform</span>
                        <span class="tag bg-white text-primary me-2">Jenkins</span>
                        <span class="tag bg-white text-primary me-2">Docker</span>
                        <span class="tag bg-white text-primary me-2">CI/CD</span>
                    </div>
                </div>
                <div class="col-md-4 text-center">
                    <i class="fas fa-cloud-upload-alt fa-10x text-white-50"></i>
                </div>
            </div>
        </div>
    </section>

    <div class="container">
        <!-- Learning Outcomes -->
        <div class="learning-box">
            <h3><i class="fas fa-graduation-cap me-2"></i>Ce que vous apprendrez avec ce projet</h3>
            <div class="row mt-4">
                <div class="col-md-6">
                    <ul>
                        <li>Déployer une infrastructure éphémère et économique sur Azure (Spot VM) via Terraform</li>
                        <li>Installer et sécuriser Jenkins pour automatiser le cycle build → test → déploiement</li>
                    </ul>
                </div>
                <div class="col-md-6">
                    <ul>
                        <li>Mettre en place un pipeline CI/CD déclenché par webhook GitHub</li>
                        <li>Produire une documentation technique claire "niveau consultant/architecte"</li>
                    </ul>
                </div>
            </div>
        </div>

        <!-- Context & Objectives -->
        <section>
            <h2 class="section-title">Contexte et Objectifs du Projet</h2>
            <div class="row">
                <div class="col-md-6">
                    <div class="card h-100">
                        <div class="card-header">
                            <h5 class="mb-0"><i class="fas fa-bullseye me-2"></i>Objectifs</h5>
                        </div>
                        <div class="card-body">
                            <ul>
                                <li>Automatiser la chaîne CI/CD complète (commit → build/test → déploiement)</li>
                                <li>Minimiser les coûts avec des VM Spot et réduire les opérations manuelles</li>
                                <li>Créer un cadre reproductible avec l'Infrastructure as Code (IaC)</li>
                                <li>Documenter le processus comme le ferait un architecte cloud Azure</li>
                            </ul>
                        </div>
                    </div>
                </div>
                <div class="col-md-6">
                    <div class="card h-100">
                        <div class="card-header">
                            <h5 class="mb-0"><i class="fas fa-project-diagram me-2"></i>Application</h5>
                        </div>
                        <div class="card-body">
                            <p>Application JavaScript complète avec :</p>
                            <ul>
                                <li>Frontend en JavaScript/Node.js</li>
                                <li>Backend API</li>
                                <li>Base de données MySQL conteneurisée</li>
                                <li>Déploiement via Docker Compose</li>
                            </ul>
                            <p>Basée sur <a href="https://github.com/docker/getting-started-app" target="_blank">docker/getting-started-app</a></p>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- Technical Stack -->
        <section>
            <h2 class="section-title">Stack Technique</h2>
            <div class="text-center my-4">
                <i class="fab fa-microsoft tech-icon" title="Azure"></i>
                <i class="fab fa-jenkins tech-icon" title="Jenkins"></i>
                <i class="fab fa-docker tech-icon" title="Docker"></i>
                <i class="fas fa-server tech-icon" title="Terraform"></i>
                <i class="fab fa-github tech-icon" title="GitHub"></i>
                <i class="fas fa-database tech-icon" title="MySQL"></i>
            </div>
            
            <div class="row">
                <div class="col-md-4 mb-4">
                    <div class="card h-100">
                        <div class="card-body text-center">
                            <i class="fab fa-microsoft fa-3x mb-3 text-primary"></i>
                            <h5>Cloud Azure</h5>
                            <p>VM Spot, Disques Managés, Réseau Virtuel</p>
                        </div>
                    </div>
                </div>
                <div class="col-md-4 mb-4">
                    <div class="card h-100">
                        <div class="card-body text-center">
                            <i class="fas fa-server fa-3x mb-3 text-primary"></i>
                            <h5>Infrastructure as Code</h5>
                            <p>Terraform pour le déploiement de l'infrastructure</p>
                        </div>
                    </div>
                </div>
                <div class="col-md-4 mb-4">
                    <div class="card h-100">
                        <div class="card-body text-center">
                            <i class="fab fa-jenkins fa-3x mb-3 text-primary"></i>
                            <h5>CI/CD</h5>
                            <p>Jenkins avec pipelines déclaratifs et webhooks GitHub</p>
                        </div>
                    </div>
                </div>
                <div class="col-md-4 mb-4">
                    <div class="card h-100">
                        <div class="card-body text-center">
                            <i class="fab fa-docker fa-3x mb-3 text-primary"></i>
                            <h5>Conteneurisation</h5>
                            <p>Docker et Docker Compose pour l'application</p>
                        </div>
                    </div>
                </div>
                <div class="col-md-4 mb-4">
                    <div class="card h-100">
                        <div class="card-body text-center">
                            <i class="fas fa-database fa-3x mb-3 text-primary"></i>
                            <h5>Base de Données</h5>
                            <p>MySQL avec stockage persistant</p>
                        </div>
                    </div>
                </div>
                <div class="col-md-4 mb-4">
                    <div class="card h-100">
                        <div class="card-body text-center">
                            <i class="fas fa-shield-alt fa-3x mb-3 text-primary"></i>
                            <h5>Sécurité</h5>
                            <p>Apache comme reverse proxy, gestion des accès</p>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- Architecture -->
        <section>
            <h2 class="section-title">Architecture du Projet</h2>
            
            <ul class="nav nav-pills mb-3" id="architectureTab" role="tablist">
                <li class="nav-item" role="presentation">
                    <button class="nav-link active" id="cloud-tab" data-bs-toggle="pill" data-bs-target="#cloud" type="button" role="tab">Vue Ingénieur Cloud</button>
                </li>
                <li class="nav-item" role="presentation">
                    <button class="nav-link" id="dev-tab" data-bs-toggle="pill" data-bs-target="#dev" type="button" role="tab">Vue Développeur</button>
                </li>
            </ul>
            
            <div class="tab-content" id="architectureTabContent">
                <div class="tab-pane fade show active" id="cloud" role="tabpanel">
                    <div class="architecture-diagram">
                        <div class="mermaid">
                            graph TB
                                subgraph AzureCloud[Cloud Azure]
                                    subgraph ResourceGroup[Groupe de Ressources]
                                        subgraph VNet[Réseau Virtuel]
                                            subgraph Subnet[Sous-réseau]
                                                VM[VM Ubuntu Spot]
                                            end
                                        end
                                        NSG[Groupe de Sécurité Réseau]
                                        Disk[Disque Azure pour données]
                                        PIP[IP Publique]
                                    end
                                end
                                
                                Dev[Developer] -->|Push du code| GitHub[GitHub]
                                GitHub -->|Webhook| Jenkins[Jenkins sur VM]
                                Terraform[Terraform] -->|Provisionnement| AzureCloud
                                Jenkins -->|Déploiement| Docker[Docker Engine]
                                Docker --> App[Container: Application]
                                Docker --> MySQL[Container: MySQL]
                                MySQL -->|Stockage persistant| Disk
                                PIP -->|Accès HTTP| App
                                Users[Utilisateurs Internet] -->|Application| PIP
                                
                                classDef azure fill:#008AD7,color:white;
                                classDef process fill:#6B3B87,color:white;
                                classDef data fill:#107C10,color:white;
                                
                                class AzureCloud,ResourceGroup,VNet,Subnet,NSG,PIP azure;
                                class VM,Jenkins,Docker,App,MySQL process;
                                class GitHub,Disk data;
                        </div>
                    </div>
                    
                    <div class="mt-4">
                        <h4>Points clés de l'architecture cloud :</h4>
                        <ul>
                            <li><strong>VM Spot Azure</strong> pour une réduction de coût significative (jusqu'à 90%)</li>
                            <li><strong>Infrastructure as Code</strong> avec Terraform pour la reproductibilité</li>
                            <li><strong>Groupe de sécurité réseau</strong> configuré pour limiter l'accès aux ports nécessaires</li>
                            <li><strong>Disque Azure attaché</strong> pour la persistance des données MySQL</li>
                            <li><strong>Jenkins</strong> installé sur la VM avec accès sécurisé via Apache</li>
                        </ul>
                    </div>
                </div>
                
                <div class="tab-pane fade" id="dev" role="tabpanel">
                    <div class="architecture-diagram">
                        <div class="mermaid">
                            graph LR
                                A[Développeur] -->|git push| B[GitHub]
                                B -->|Webhook| C[Jenkins]
                                C --> D[Pipeline CI/CD]
                                D --> E[Checkout Code]
                                D --> F[Build Application]
                                D --> G[Run Tests]
                                D --> H[Build Docker Images]
                                D --> I[Deploy Containers]
                                I --> J[Frontend Container]
                                I --> K[Backend Container]
                                I --> L[MySQL Container]
                                L --> M[(Volume Docker)]
                                
                                style A fill:#6B3B87,color:white
                                style B fill:#107C10,color:white
                                style C fill:#D83B01,color:white
                                style J,K,L fill:#008AD7,color:white
                        </div>
                    </div>
                    
                    <div class="mt-4">
                        <h4>Processus de développement :</h4>
                        <ul>
                            <li><strong>Intégration continue</strong> : À chaque push, le code est testé et validé</li>
                            <li><strong>Déploiement continu</strong> : Après validation, déploiement automatique en production</li>
                            <li><strong>Environnement reproductible</strong> : Docker garantit la cohérence entre dev et prod</li>
                            <li><strong>Tests automatisés</strong> : Exécution de tests à chaque modification</li>
                            <li><strong>Feedback immédiat</strong> : Le développeur est notifié du résultat du pipeline</li>
                        </ul>
                    </div>
                </div>
            </div>
        </section>

        <!-- Implementation Steps -->
        <section>
            <h2 class="section-title">Mise en Œuvre Pas à Pas</h2>
            
            <div class="card mb-4">
                <div class="card-header">
                    <h5 class="mb-0"><span class="step-number">1</span> Provisionnement de l'infrastructure avec Terraform</h5>
                </div>
                <div class="card-body">
                    <p>Définition des ressources Azure dans des fichiers Terraform :</p>
                    <ul>
                        <li>Configuration du provider Azure</li>
                        <li>Création d'un groupe de ressources</li>
                        <li>Déploiement d'une machine virtuelle Ubuntu Spot</li>
                        <li>Configuration du réseau et des règles de sécurité</li>
                        <li>Attribution d'une IP publique</li>
                    </ul>
                    
                    <div class="code-block">
                        <pre><code class="language-hcl">
# Exemple de configuration Terraform pour une VM Azure
resource "azurerm_linux_virtual_machine" "jenkins_vm" {
  name                = "jenkins-vm"
  resource_group_name = azurerm_resource_group.example.name
  location            = azurerm_resource_group.example.location
  size                = "Standard_B2s"
  admin_username      = "adminuser"
  
  # Configuration de la VM Spot
  priority        = "Spot"
  eviction_policy = "Deallocate"
  
  network_interface_ids = [azurerm_network_interface.example.id]
  
  os_disk {
    caching              = "ReadWrite"
    storage_account_type = "Standard_LRS"
  }
  
  source_image_reference {
    publisher = "Canonical"
    offer     = "UbuntuServer"
    sku       = "18.04-LTS"
    version   = "latest"
  }
}
                        </code></pre>
                    </div>
                </div>
            </div>
            
            <div class="card mb-4">
                <div class="card-header">
                    <h5 class="mb-0"><span class="step-number">2</span> Installation et configuration de Jenkins</h5>
                </div>
                <div class="card-body">
                    <p>Script d'installation et de configuration automatique :</p>
                    <ul>
                        <li>Installation de Java, Docker et Jenkins</li>
                        <li>Configuration des plugins Jenkins nécessaires</li>
                        <li>Mise en place de la sécurité et des utilisateurs</li>
                        <li>Configuration d'Apache comme reverse proxy</li>
                        <li>Ouverture des ports nécessaires (8080 pour Jenkins, 3000 pour l'application)</li>
                    </ul>
                </div>
            </div>
            
            <div class="card mb-4">
                <div class="card-header">
                    <h5 class="mb-0"><span class="step-number">3</span> Pipeline CI/CD Jenkins</h5>
                </div>
                <div class="card-body">
                    <p>Définition du pipeline déclaratif dans un Jenkinsfile :</p>
                    
                    <div class="code-block">
                        <pre><code class="language-groovy">
pipeline {
    agent any
    environment {
        APP_PORT = "3000"
        VM_IP = "20.121.15.142"  // Votre IP publique
    }
    stages {
        stage('1. Checkout & Setup') {
            steps {
                echo "🔁 Récupération du code"
                git branch: 'main', 
                url: 'https://github.com/stanilpaul/docker-getting-started-devops-enhanced.git'
                sh 'docker volume create todo-mysql-data || true'
            }
        }
        stage('2. Build & Test') {
            steps {
                echo "🔨 Construction et tests"
                sh '''
                    docker-compose up -d
                    sleep 15
                    docker-compose exec app yarn test || true
                    docker-compose down
                '''
            }
        }
        stage('3. Deploy Production') {
            steps {
                echo "🚀 Déploiement final"
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
            echo "✅ SUCCÈS: Application en production!"
            echo "🌐 Accédez à: http://${VM_IP}:${APP_PORT}"
            sh 'docker ps'
        }
        failure {
            echo "❌ ÉCHEC: Vérifiez les logs"
            sh 'docker-compose logs || true'
        }
    }
}
                        </code></pre>
                    </div>
                </div>
            </div>
            
            <div class="card mb-4">
                <div class="card-header">
                    <h5 class="mb-0"><span class="step-number">4</span> Configuration des Webhooks GitHub</h5>
                </div>
                <div class="card-body">
                    <p>Mise en place de l'intégration entre GitHub et Jenkins :</p>
                    <ul>
                        <li>Configuration du webhook dans le repository GitHub</li>
                        <li>Configuration de Jenkins pour accepter les webhooks GitHub</li>
                        <li>Test de l'intégration avec un push de code</li>
                    </ul>
                </div>
            </div>
        </section>

        <!-- Results & Analysis -->
        <section>
            <h2 class="section-title">Résultats et Analyse</h2>
            
            <div class="row">
                <div class="col-md-6">
                    <div class="card h-100">
                        <div class="card-header">
                            <h5 class="mb-0"><i class="fas fa-chart-line me-2"></i>Avantages Obtenus</h5>
                        </div>
                        <div class="card-body">
                            <ul>
                                <li><strong>Réduction des coûts</strong> : Utilisation de VM Spot pour une économie jusqu'à 90%</li>
                                <li><strong>Automatisation complète</strong> : Déploiement en un click après configuration initiale</li>
                                <li><strong>Reproductibilité</strong> : L'infrastructure peut être recréée identiquement à tout moment</li>
                                <li><strong>Feedback rapide</strong> : Les développeurs voient immédiatement l'impact de leurs changes</li>
                            </ul>
                        </div>
                    </div>
                </div>
                <div class="col-md-6">
                    <div class="card h-100">
                        <div class="card-header">
                            <h5 class="mb-0"><i class="fas fa-balance-scale me-2"></i>Analyse Coûts/Bénéfices</h5>
                        </div>
                        <div class="card-body">
                            <ul>
                                <li><strong>Coût estimé</strong> : ~15-20€/mois (VM Spot B2s + stockage)</li>
                                <li><strong>Économie</strong> : ~100€/mois comparé à une VM standard</li>
                                <li><strong>Temps de déploiement</strong> : Infrastructure ~10min, Pipeline ~5min</li>
                                <li><strong>Maintenance</strong> : Réduite grâce à l'automatisation</li>
                            </ul>
                        </div>
                    </div>
                </div>
            </div>
            
            <div class="card mt-4">
                <div class="card-header">
                    <h5 class="mb-0"><i class="fas fa-vial me-2"></i>Tests et Validation</h5>
                </div>
                <div class="card-body">
                    <p>Le pipeline inclut plusieurs niveaux de validation :</p>
                    <ul>
                        <li><strong>Tests unitaires</strong> : Exécution des tests JavaScript avec Yarn</li>
                        <li><strong>Tests d'intégration</strong> : Validation du bon fonctionnement des containers</li>
                        <li><strong>Tests de disponibilité</strong> : Vérification que l'application répond sur le port configuré</li>
                        <li><strong>Validation du déploiement</strong> : Confirmation du succès du déploiement</li>
                    </ul>
                </div>
            </div>
        </section>

        <!-- Improvements -->
        <section>
            <h2 class="section-title">Améliorations Possibles</h2>
            
            <div class="row">
                <div class="col-md-6">
                    <div class="card h-100">
                        <div class="card-header">
                            <h5 class="mb-0"><i class="fas fa-shield-alt me-2"></i>Sécurité</h5>
                        </div>
                        <div class="card-body">
                            <ul>
                                <li>Utilisation d'Azure Key Vault pour la gestion des secrets</li>
                                <li>Mise en place d'un reverse proxy avec TLS/SSL</li>
                                <li>Configuration de l'intégration OIDC entre GitHub et Jenkins</li>
                                <li>Restriction des acc réseau avec NSG plus stricts</li>
                            </ul>
                        </div>
                    </div>
                </div>
                <div class="col-md-6">
                    <div class="card h-100">
                        <div class="card-header">
                            <h5 class="mb-0"><i class="fas fa-tachometer-alt me-2"></i>Performance & Monitoring</h5>
                        </div>
                        <div class="card-body">
                            <ul>
                                <li>Implémentation d'Azure Monitor pour la surveillance</li>
                                <li>Configuration d'alertes sur les métriques importantes</li>
                                <li>Mise en place de logs centralisés avec Log Analytics</li>
                                <li>Autoscaling selon la charge (avec des VM standard)</li>
                            </ul>
                        </div>
                    </div>
                </div>
            </div>
            
            <div class="card mt-4">
                <div class="card-header">
                    <h5 class="mb-0"><i class="fas fa-expand-arrows-alt me-2"></i>Évolutivité</h5>
                </div>
                <div class="card-body">
                    <ul>
                        <li>Migration vers Azure Kubernetes Service (AKS) pour une meilleure orchestration</li>
                        <li>Déploiement multi-région pour la haute disponibilité</li>
                        <li>Implémentation de blue-green deployments</li>
                        <li>Ajout d'un staging environment avant la production</li>
                    </ul>
                </div>
            </div>
        </section>

        <!-- Conclusion -->
        <section>
            <h2 class="section-title">Conclusion</h2>
            <div class="card">
                <div class="card-body">
                    <p>Ce projet démontre la mise en place d'un pipeline CI/CD complet utilisant des technologies et pratiques standard dans le domaine DevOps. L'utilisation combinée de Terraform pour l'infrastructure as code, Jenkins pour l'automatisation, et Docker pour la conteneurisation, permet de créer une solution robuste, reproductible et économique.</p>
                    
                    <p>L'architecture proposée, bien que conçue pour un coût minimal, intègre les principes fondamentaux du cloud et peut servir de base à des implémentations plus complexes et robustes. La documentation technique détaillée montre une compréhension approfondie des enjeux techniques et opérationnels, telle qu'attendue d'un architecte cloud Azure.</p>
                    
                    <div class="text-center mt-4">
                        <a href="https://github.com/stanilpaul/docker-getting-started-devops-enhanced" class="btn btn-primary btn-lg me-3" target="_blank">
                            <i class="fab fa-github me-2"></i>Voir le code source
                        </a>
                        <a href="/assets/docs/devops-ci-cd-documentation.pdf" class="btn btn-outline-primary btn-lg" target="_blank">
                            <i class="fas fa-file-pdf me-2"></i>Documentation complète
                        </a>
                    </div>
                </div>
            </div>
        </section>
    </div>

    <footer>
        <div class="container">
            <div class="row">
                <div class="col-md-6">
                    <h5>Stanil Paul</h5>
                    <p>Ingénieur Cloud Azure | DevOps</p>
                    <p>Spécialisé dans la conception et l'implémentation de solutions cloud sur Microsoft Azure.</p>
                </div>
                <div class="col-md-6 text-md-end">
                    <a href="#" class="text-white me-3"><i class="fab fa-linkedin fa-2x"></i></a>
                    <a href="#" class="text-white me-3"><i class="fab fa-github fa-2x"></i></a>
                    <a href="#" class="text-white"><i class="fas fa-envelope fa-2x"></i></a>
                </div>
            </div>
            <div class="row mt-3">
                <div class="col-12 text-center">
                    <p class="mb-0">&copy; 2023 Stanil Paul. Tous droits réservés.</p>
                </div>
            </div>
        </div>
    </footer>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
    <script>
        // Initialize Mermaid
        mermaid.initialize({
            startOnLoad: true,
            theme: 'default',
            flowchart: {
                useMaxWidth: false,
                htmlLabels: true
            }
        });
        
        // Activate tooltips
        var tooltipTriggerList = [].slice.call(document.querySelectorAll('[data-bs-toggle="tooltip"]'))
        var tooltipList = tooltipTriggerList.map(function (tooltipTriggerEl) {
            return new bootstrap.Tooltip(tooltipTriggerEl)
        });
    </script>
</body>
</html>