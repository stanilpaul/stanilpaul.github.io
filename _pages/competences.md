---
title: "Compétences"
permalink: /competences/
layout: single
classes: wide
author_profile: true
---

<style>
:root{
  --blue:#174c7b;
  --blue-strong:#123d63;
  --muted:#555;
  --panel:#fff;
  --radius:6px;
  --gap:18px;
  --font-sans: "Inter", "Segoe UI", Tahoma, sans-serif;
}

/* Container */
.comp-wrap{
  max-width: 1100px;
  margin: 40px auto;
  padding: 0 20px;
  font-family: var(--font-sans);
  color: #222;
  line-height: 1.65;
}

/* Header */
.comp-header{
  margin-bottom: 28px;
}
.comp-header h1{
  font-size: 34px;
  letter-spacing: 0.02em;
  margin: 0 0 6px;
  color: var(--blue-strong);
}
.comp-header p{
  margin: 0;
  color: var(--muted);
  font-size: 15px;
}

/* Accordion grid */
.skills-accordion {
  display: grid;
  gap: var(--gap);
  margin-top: 18px;
}

/* Each details */
.skills-accordion details {
  border-radius: var(--radius);
  overflow: hidden;
  background: transparent;
}

/* Summary bar */
.skills-accordion details summary {
  list-style: none;
  cursor: pointer;
  background: var(--blue);
  color: #fff;
  padding: 16px 22px;
  font-weight: 700;
  font-size: 16px;
  letter-spacing: 0.02em;
  display: flex;
  align-items: center;
  justify-content: space-between;
  transition: background 0.18s ease, transform 0.08s ease;
  border: 1px solid rgba(0,0,0,0.03);
}

/* Remove default marker */
.skills-accordion details summary::-webkit-details-marker { display: none; }

/* Hover & focus */
.skills-accordion details summary:hover,
.skills-accordion details summary:focus {
  background: linear-gradient(180deg, var(--blue) 0%, var(--blue-strong) 100%);
  transform: translateY(-1px);
  outline: none;
}

/* Arrow indicator */
.summary-arrow {
  display:inline-block;
  width:20px;
  height:20px;
  transform: rotate(0deg);
  transition: transform 0.35s ease;
  opacity: 0.95;
}
.skills-accordion details[open] summary .summary-arrow {
  transform: rotate(180deg);
}

/* Panel */
.skills-accordion details .panel {
  background: var(--panel);
  border: 1px solid rgba(0,0,0,0.06);
  border-top: none;
  padding: 0 22px;
  border-radius: 0 0 var(--radius) var(--radius);
  box-shadow: 0 8px 26px rgba(10,20,30,0.05);
  color: var(--muted);
  overflow: hidden;
  max-height: 0;
  opacity: 0;
  transition: max-height 1s cubic-bezier(.2,.9,.2,1), opacity 0.95s ease;
}
.skills-accordion details[open] .panel {
  padding: 18px 22px 22px 22px;
  max-height: 1400px;
  opacity: 1;
}

/* Inner layout */
.panel .section {
  margin-bottom: 14px;
}
.panel h3 {
  margin: 0 0 6px 0;
  color: #12263b;
  font-size: 15px;
  font-weight: 700;
}
.panel ul {
  margin: 0 0 6px 18px;
  padding: 0;
}
.panel li {
  margin-bottom: 6px;
  font-size: 14px;
  color: #333;
}

/* subtle highlight */
.skills-accordion details[open] summary {
  box-shadow: 0 6px 18px rgba(10,20,30,0.06);
}

/* Responsive */
@media (max-width: 800px){
  .comp-wrap{ padding: 0 14px; }
  .skills-accordion details summary { font-size: 15px; padding: 14px; }
  .panel { padding: 16px; }
}

/* Search bar */
.comp-header-row{display:flex;align-items:center;justify-content:space-between;gap:12px;flex-wrap:wrap}
.searchbar{position:relative;min-width:280px}
#skillSearch{appearance:none;width:320px;max-width:100%;padding:10px 36px 10px 12px;border:1px solid rgba(0,0,0,.15);border-radius:8px;font-size:14px;background:#d9ebff;border:1px solid #a8c9f0;color:#123d63;font-weight:500}
#skillSearch::placeholder{color:#5b87aa;opacity:0.9}
#skillSearch:focus{outline:none;box-shadow:0 0 0 3px rgba(23,76,123,.15);border-color:var(--blue)}
#clearSearch{position:absolute;right:8px;top:50%;transform:translateY(-50%);background:transparent;border:0;font-size:16px;color:#999;cursor:pointer;display:none}
#searchMeta{margin-top:6px;color:var(--muted);font-size:13px}
.is-hidden{display:none !important}

/* Highlight */
mark.hl{
  background:#ffeb3b66;
  color:#111;
  padding:0 .15em;
  border-radius:3px;
  box-shadow: inset 0 0 0 1px #f0d00080;
}
</style>

<div class="comp-wrap">
  <div class="comp-header">
    <!-- <h1>Compétences</h1> -->
<div class="comp-header-row"> <p style="margin:0">Spécialisation Azure (niveau ingénieur).</p> <div class="searchbar"> <input type="search" id="skillSearch" placeholder="Rechercher (AKS, Terraform, Key Vault…)" aria-label="Rechercher une compétence"> <button type="button" id="clearSearch" aria-label="Effacer">✕</button> </div> </div> <div id="searchMeta"></div>
    
  </div>

    <div class="skills-accordion" id="skillsAccordion">
      <!-- Certifications -->
      <details data-key="certs">
        <summary>
          <span>Certifications & formation</span>
          <span class="summary-arrow">▾</span>
        </summary>
        <div class="panel">
          <div class="section">
            <ul>
              <li><strong>AZ-104</strong> — Microsoft Azure Administrator (certifié).</li>
              <li><strong>Terraform Associate</strong> — en cours de préparation (exam 003).</li>
              <li>Formation continue : Azure + Terraform (projets hands-on).</li>
            </ul>
          </div>
        </div>
      </details>
    <!-- Azure -->
    <details data-key="azure">
      <summary>
        <span>Azure Cloud— Expertise (niveau ingénieur)</span>
        <span class="summary-arrow">▾</span>
      </summary>
      <div class="panel">
        <div class="section">
          <h3>Administration & Architecture</h3>
          <ul>
            <li>Conception et déploiement d'infrastructures résilientes : Resource Groups, App Service, VM, VM Scale Sets, Availability Sets, Functions.</li>
            <li>Planification de capacity, HA, autoscaling et stratégies de failover.</li>
          </ul>
        </div>

        <div class="section">
          <h3>Réseau & Connectivité</h3>
          <ul>
            <li>VNet, Subnets, NSG, UDR, Route Tables, VNet Peering.</li>
            <li>Private Endpoints / Private Link, Private DNS zones pour PaaS (MySQL, Redis, Key Vault).</li>
            <li>Load Balancer, Application Gateway, WAF, Traffic Manager, Bastion.</li>
            <li>VPN (P2S, S2S) et diagnostics réseau (Network Watcher).</li>
          </ul>
        </div>

        <div class="section">
          <h3>Sécurité & Identity</h3>
          <ul>
            <li>Azure AD, Managed Identities, App Registrations / Service Principal, RBAC avancé.</li>
            <li>Key Vault, gestion des secrets, Service Connector, policies de rotation et accès.</li>
            <li>Azure Policy, Blueprints et gouvernance (Management Groups, tagging).</li>
          </ul>
        </div>

        <div class="section">
          <h3>Stockage & Data</h3>
          <ul>
            <li>Storage Accounts (Blob, File, Disk) : configuration, redondance, snapshots, lifecycle.</li>
            <li>Azure Database for MySQL, Azure SQL, Azure Cache for Redis — configuration sécurisée et optimisation des connexions.</li>
          </ul>
        </div>

        <div class="section">
          <h3>IaC & Automatisation</h3>
          <ul>
            <li>Bicep / ARM Templates, Terraform (intégration Azure), Azure CLI, PowerShell.</li>
            <li>Gestion du state (Azure Storage backend), modules réutilisables, pipelines IaC.</li>
          </ul>
        </div>

        <div class="section">
          <h3>DevOps & Observabilité</h3>
          <ul>
            <li>CI/CD : GitHub Actions, Azure DevOps Pipelines (YAML), déploiements slots, blue/green, approbations.</li>
            <li>Azure Monitor, Log Analytics, Application Insights, alerting, dashboards et runbooks.</li>
          </ul>
        </div>

        <div class="section">
          <h3>Notes</h3>
          <ul>
            <li>Projets notables : App Service + MySQL + Redis avec Private Endpoints et pipelines automatisés (CI/CD).</li>
            <li>Orientation SRE : runbooks, SLIs/SLOs, remédiation automatisée et optimisation coûts.</li>
          </ul>
        </div>
      </div>
    </details>

    <!-- Multi-cloud -->
    <details data-key="multicloud">
      <summary>
        <span>Multi-cloud (AWS, Oracle Cloud, GCP)</span>
        <span class="summary-arrow">▾</span>
      </summary>
      <div class="panel">
        <div class="section">
          <h3>Vue d'ensemble</h3>
          <ul>
            <li>Compétences multi-cloud : Azure (spécialité), AWS (niveau administrateur), Oracle Cloud (OCI) et GCP (usage pratique).</li>
            <li>Approche commune : patterns d'intégration, réseaux hybrides, migrations et uniformisation via Terraform.</li>
          </ul>
        </div>

        <div class="section">
          <h3>AWS (niveau administrateur)</h3>
          <ul>
            <li>Compute (EC2), S3, VPC, IAM, RDS concepts, intégration avec services applicatifs.</li>
          </ul>
        </div>

        <div class="section">
          <h3>Oracle Cloud (OCI) & GCP</h3>
          <ul>
            <li>Déploiements de base et intégrations, utilisation des consoles natives et scripts Terraform.</li>
          </ul>
        </div>
      </div>
    </details>

    <!-- IaC & Provisioning -->
    <details data-key="iac">
      <summary>
        <span>Infrastructure as Code & Provisioning</span>
        <span class="summary-arrow">▾</span>
      </summary>
      <div class="panel">
        <div class="section">
          <ul>
            <li>Terraform : modules, workspaces, backends Azure Storage, stratégies de verrouillage et sécurité du state.</li>
            <li>Bicep / ARM Templates : déploiements natifs Azure et intégration CI.</li>
            <li>Azure CLI, PowerShell : automatisation et scripts de déploiement.</li>
          </ul>
        </div>
      </div>
    </details>

    <!-- Réseau & Sécurité -->
    <details data-key="network-sec">
      <summary>
        <span>Réseau & Sécurité</span>
        <span class="summary-arrow">▾</span>
      </summary>
      <div class="panel">
        <div class="section">
          <ul>
            <li>NSG, Firewalls, WAF, Application Gateway, Load Balancer, Traffic Manager.</li>
            <li>VPN (S2S, P2S), ExpressRoute (concepts), bastion, segmentation réseau et durcissement.</li>
            <li>IAM, RBAC, identity management, gestion des secrets et policies de conformité.</li>
          </ul>
        </div>
      </div>
    </details>

    <!-- DevOps & CI/CD -->
    <details data-key="devops">
      <summary>
        <span>DevOps & CI/CD</span>
        <span class="summary-arrow">▾</span>
      </summary>
      <div class="panel">
        <div class="section">
          <ul>
            <li>Azure DevOps (Pipelines YAML, Repos, Boards, Artifacts) et GitHub Actions.</li>
            <li>Jenkins pour cas legacy, stratégies de release (canary, blue/green), triggers et approbations.</li>
            <li>Gestion de code : Git, branching strategies, PR reviews, GitOps.</li>
          </ul>
        </div>
      </div>
    </details>

    <!-- Conteneurs -->
    <details data-key="containers">
      <summary>
        <span>Conteneurs & Orchestration</span>
        <span class="summary-arrow">▾</span>
      </summary>
      <div class="panel">
        <div class="section">
          <ul>
            <li>Docker : images, optimisation, registries.</li>
            <li>Kubernetes / AKS : déploiements, autoscaling et troubleshooting.</li>
            <li>ACI & Ansible pour déploiements légers et automatisation de configuration.</li>
          </ul>
        </div>
      </div>
    </details>

    <!-- Systèmes & Virtualisation -->
    <details data-key="systems">
      <summary>
        <span>Systèmes & Virtualisation</span>
        <span class="summary-arrow">▾</span>
      </summary>
      <div class="panel">
        <div class="section">
          <ul>
            <li>Windows Server 2019 / 2022, Windows 10/11, Linux (Debian), macOS, Android.</li>
            <li>Virtualisation : VMware, Hyper-V, VirtualBox — conception d'infrastructures virtuelles et optimisation.</li>
          </ul>
        </div>
      </div>
    </details>

    <!-- Bases de données -->
    <details data-key="db">
      <summary>
        <span>Bases de données & Stockage</span>
        <span class="summary-arrow">▾</span>
      </summary>
      <div class="panel">
        <div class="section">
          <ul>
            <li>MySQL (incl. Azure Database for MySQL) : administration, migrations, sauvegardes.</li>
            <li>Microsoft SQL Server : administration et optimisation basique.</li>
            <li>Storage Accounts (Blob, Files, Disk) : lifecycle, redondance, snapshots.</li>
          </ul>
        </div>
      </div>
    </details>

    <!-- Observabilité -->
    <details data-key="observ">
      <summary>
        <span>Observabilité & Supervision</span>
        <span class="summary-arrow">▾</span>
      </summary>
      <div class="panel">
        <div class="section">
          <ul>
            <li>Azure Monitor, Log Analytics, Application Insights, Network Watcher.</li>
            <li>KQL, dashboards, alerting, playbooks et runbooks pour gestion d'incidents.</li>
            <li>GLPI (ITSM) et Power BI</li>
          </ul>
        </div>
      </div>
    </details>

    <!-- Automatisation & Scripting - UPDATED CONTENT -->
    <details data-key="automation">
      <summary>
        <span>Automatisation & Scripting</span>
        <span class="summary-arrow">▾</span>
      </summary>
        <div class="panel">
        <div class="section">
          <ul>
            <li>PowerShell, Bash / Shell, Python — scripts d'administration, déploiement, intégration et outils d'automatisation opérationnelle.</li>
            <li>Terraform (avec Azure) et Ansible — IaC et provisioning : modules réutilisables, backends, gestion du state, playbooks et intégration dans des pipelines CI/CD.</li>
          </ul>
        </div>
      </div>
    </details>

    <!-- Développement Web & Mobile -->
    <details data-key="dev">
      <summary>
        <span>Développement Web & Mobile (support DevOps)</span>
        <span class="summary-arrow">▾</span>
      </summary>
      <div class="panel">
        <div class="section">
          <ul>
            <li>Python, Java, C#, PHP, JavaScript, WordPress</li>
            <li>Mobile : Flutter, Android (Java/Kotlin), iOS (Swift) — build & déploiement.</li>
          </ul>
        </div>
      </div>
    </details>

    <!-- SRE & méthodes -->
    <details data-key="sre">
      <summary>
        <span>Outils & Méthodes SRE</span>
        <span class="summary-arrow">▾</span>
      </summary>
      <div class="panel">
        <div class="section">
          <ul>
            <li>Monitoring continu, alerting, playbooks.</li>
            <li>Runbooks, procédures de rollback, tests de résilience basiques.</li>
            <li>Optimisation coûts, tagging, gouvernance cloud.</li>
          </ul>
        </div>
      </div>
    </details>

  </div>
</div>

<script>
(function () {
  document.addEventListener('DOMContentLoaded', function () {
    const input = document.getElementById('skillSearch');
    const clearBtn = document.getElementById('clearSearch');
    const meta = document.getElementById('searchMeta');
    const acc = document.getElementById('skillsAccordion');
    if (!input || !acc) return;
    const items = Array.from(acc.querySelectorAll('details'));

    const norm = s => (s || '').toLowerCase().normalize('NFD').replace(/[\u0300-\u036f]/g, '');

    function removeHighlights(el) {
      el.querySelectorAll('mark.hl').forEach(mark => mark.replaceWith(document.createTextNode(mark.textContent)));
    }

    function highlight(el, query) {
      if (!query) return;
      removeHighlights(el);
      const normQuery = norm(query);

      function walk(node) {
        if (node.nodeType === 3) {
          let original = node.nodeValue;
          let normalized = norm(original);
          let frag = document.createDocumentFragment();
          let lastIndex = 0, start;

          while ((start = normalized.indexOf(normQuery, lastIndex)) !== -1) {
            let end = start + normQuery.length;
            frag.appendChild(document.createTextNode(original.slice(lastIndex, start)));

            let mark = document.createElement("mark");
            mark.className = "hl";
            mark.textContent = original.slice(start, end);
            frag.appendChild(mark);

            lastIndex = end;
          }
          frag.appendChild(document.createTextNode(original.slice(lastIndex)));
          if (frag.childNodes.length) node.replaceWith(frag);
        } else if (node.nodeType === 1 && node.childNodes && !["SCRIPT","STYLE","MARK"].includes(node.tagName)) {
          [...node.childNodes].forEach(walk);
        }
      }
      walk(el);
    }

    function reset() {
      items.forEach(d => {
        d.classList.remove('is-hidden');
        d.removeAttribute('open');
        const panel = d.querySelector('.panel');
        if (panel) removeHighlights(panel);
      });
      clearBtn.style.display = 'none';
      meta.textContent = '';
      window.__skillSearchActive = false;
    }

    function search(q) {
      const query = norm(q.trim());
      if (!query) return reset();

      window.__skillSearchActive = true;
      let matches = 0;
      items.forEach(d => {
        const text = norm(d.textContent || '');
        const panel = d.querySelector('.panel');
        if (text.includes(query)) {
          d.classList.remove('is-hidden');
          d.setAttribute('open', '');
          matches++;
          if (panel) highlight(panel, q);
        } else {
          d.classList.add('is-hidden');
          d.removeAttribute('open');
          if (panel) removeHighlights(panel);
        }
      });
      clearBtn.style.display = 'inline';
      meta.textContent = matches > 0
        ? matches + ' catégorie(s) trouvée(s) pour « ' + q + ' »'
        : 'Aucun résultat pour « ' + q + ' »';
    }

    input.addEventListener('input', e => search(e.target.value));
    clearBtn.addEventListener('click', () => { input.value = ''; reset(); input.focus(); });
  });
})();
</script>