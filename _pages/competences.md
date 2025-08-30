---
title: "Compétences"
permalink: /competences/
layout: single
classes: wide
author_profile: false
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

/* Rotate when parent details open */
.skills-accordion details[open] summary .summary-arrow {
  transform: rotate(180deg);
}

/* Panel - animated open/close */
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

/* When open - allow content to show with a slide + fade */
.skills-accordion details[open] .panel {
  padding: 18px 22px 22px 22px;
  max-height: 1400px; /* suffisamment grand */
  opacity: 1;
}

/* Inner layout */
.panel .section {
  transform: translateY(6px);
  opacity: 0;
  transition: opacity 1s ease, transform 1s ease;
}
.panel h3 {
  margin: 0 0 8px 0;
  color: #12263b;
  font-size: 15px;
  font-weight: 700;
}
.panel p, .panel .line {
  margin: 6px 0;
  color: #333;
  font-size: 14px;
}
.panel ul {
  margin: 6px 0 0 18px;
  padding: 0;
}
.panel li {
  margin-bottom: 8px;
  font-size: 14px;
  color: #333;
}

/* subtle highlight on open */
.skills-accordion details[open] summary {
  box-shadow: 0 6px 18px rgba(10,20,30,0.06);
}

/* small transition for list items appearance */
.panel .section { transform: translateY(0); transition: transform 0.28s ease; }
.skills-accordion details[open] .panel .section { transform: translateY(0); }

/* Responsive */
@media (max-width: 800px){
  .comp-wrap{ padding: 0 14px; }
  .skills-accordion details summary { font-size: 15px; padding: 14px; }
  .panel { padding: 16px; }
}

/* Accessibility focus */
.skills-accordion details summary:focus {
  box-shadow: 0 0 0 3px rgba(23,76,123,0.14);
  outline: none;
}

/* Search bar à droite du sous-titre */
.comp-header-row{display:flex;align-items:center;justify-content:space-between;gap:12px;flex-wrap:wrap}
.searchbar{position:relative;min-width:280px}
#skillSearch{appearance:none;width:320px;max-width:100%;padding:10px 36px 10px 12px;border:1px solid rgba(0,0,0,.15);border-radius:8px;font-size:14px}
#skillSearch:focus{outline:none;box-shadow:0 0 0 3px rgba(23,76,123,.15);border-color:var(--blue)}
#clearSearch{position:absolute;right:8px;top:50%;transform:translateY(-50%);background:transparent;border:0;font-size:16px;color:#999;cursor:pointer;display:none}
#searchMeta{margin-top:6px;color:var(--muted);font-size:13px}
.is-hidden{display:none !important}

#skillSearch {
  background: #d9ebff; /* bleu plus clair */
  border: 1px solid #a8c9f0;
  color: #123d63;
  font-weight: 500;
}
#skillSearch::placeholder {
  color: #5b87aa;
  opacity: 0.9;
}


/* Surlignage des occurrences */
mark.hl{
background:#ffeb3b66; /* jaune doux */
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
            <li>Bicep / ARM Templates, Terraform (intégration Azure), Azure CLI, azd, PowerShell.</li>
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
            <li>Azure CLI, azd, PowerShell : automatisation et scripts de déploiement.</li>
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
document.addEventListener('DOMContentLoaded', function() {
  const detailsList = Array.from(document.querySelectorAll('.skills-accordion details'));

  // Ensure all closed on load
  detailsList.forEach(d => d.removeAttribute('open'));

  // Exclusive accordion: when one opens, close others
  detailsList.forEach(d => {
    d.addEventListener('toggle', function() {
      if (d.open && !window.__skillSearchActive) {
        detailsList.forEach(other => {
          if (other !== d) other.removeAttribute('open');
        });
        // accessibility focus
        const panel = d.querySelector('.panel');
        if (panel) {
          panel.setAttribute('tabindex', '-1');
          panel.focus({preventScroll: true});
        }
      }
    });
  });

  // Staggered reveal with ~1s transitions
  detailsList.forEach(d => {
    d.addEventListener('toggle', function() {
      const sections = Array.from(d.querySelectorAll('.panel .section'));
      if (d.open) {
        // reset then animate with stagger
        sections.forEach((s) => {
          s.style.opacity = 0;
          s.style.transform = 'translateY(8px)';
          // ensure transition properties are applied (matching CSS)
          s.style.transition = 'opacity 1000ms ease, transform 1000ms ease';
        });
        sections.forEach((s, i) => {
          // stagger: 120ms * index (keeps total pleasant)
          setTimeout(() => {
            s.style.opacity = 1;
            s.style.transform = 'translateY(0)';
          }, 120 * i);
        });
      } else {
        // close: remove inline styles to reset to CSS defaults
        sections.forEach((s) => {
          s.style.opacity = '';
          s.style.transform = '';
          s.style.transition = '';
        });
      }
    });
  });
});


</script>

<script>
(function () {
  document.addEventListener('DOMContentLoaded', function () {
    var input = document.getElementById('skillSearch');
    var clearBtn = document.getElementById('clearSearch');
    var meta = document.getElementById('searchMeta');
    var acc = document.getElementById('skillsAccordion');
    if (!input || !acc) return;
    var items = Array.prototype.slice.call(acc.querySelectorAll('details'));

    function norm(s) {
      return (s || '').toLowerCase().normalize('NFD').replace(/[\u0300-\u036f]/g, '');
    }

    // Fonction qui enlève les <mark>
    function removeHighlights(el) {
      el.querySelectorAll('mark.hl').forEach(mark => {
        mark.replaceWith(document.createTextNode(mark.textContent));
      });
    }

function highlight(el, query) {
  if (!query) return;
  removeHighlights(el);

  let normQuery = norm(query);

  function walk(node) {
    if (node.nodeType === 3) { // texte pur
      let original = node.nodeValue;
      let normalized = norm(original);

      let frag = document.createDocumentFragment();
      let lastIndex = 0;
      let start;

      while ((start = normalized.indexOf(normQuery, lastIndex)) !== -1) {
        let end = start + normQuery.length;

        // retrouver les indices dans le texte original
        let before = original.slice(lastIndex, start);
        let match = original.slice(start, end);
        let after = original.slice(end);

        if (before) frag.appendChild(document.createTextNode(before));

        let mark = document.createElement("mark");
        mark.className = "hl";
        mark.textContent = match;
        frag.appendChild(mark);

        // avancer
        original = after;
        normalized = norm(original);
        lastIndex = 0; // on repart du début de la sous-chaîne
      }

      if (original) {
        frag.appendChild(document.createTextNode(original));
      }

      if (frag.childNodes.length) {
        node.replaceWith(frag);
      }
    } 
    else if (node.nodeType === 1 && node.childNodes && !["SCRIPT","STYLE","MARK"].includes(node.tagName)) {
      [...node.childNodes].forEach(walk);
    }
  }
  walk(el);
}




    // Reset complet
    function reset() {
      items.forEach(function (d) {
        d.classList.remove('is-hidden');
        d.removeAttribute('open');
        var panel = d.querySelector('.panel');
        if (panel) removeHighlights(panel);
      });
      if (clearBtn) clearBtn.style.display = 'none';
      if (meta) meta.textContent = '';
      window.__skillSearchActive = false;
    }

    // Recherche
    function search(q) {
      var query = norm(q.trim());
      if (!query) {
        reset();
        return;
      }
      window.__skillSearchActive = true;
      var matches = 0;
      items.forEach(function (d) {
        var text = norm(d.textContent || '');
        var panel = d.querySelector('.panel');
        if (text.indexOf(query) !== -1) {
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
      if (clearBtn) clearBtn.style.display = 'inline';
      if (meta) meta.textContent = (matches > 0)
        ? matches + ' catégorie(s) trouvée(s) pour « ' + q + ' »'
        : 'Aucun résultat pour « ' + q + ' »';
    }

    // Events
    input.addEventListener('input', e => search(e.target.value));
    input.addEventListener('keyup', e => search(e.target.value));
    if (clearBtn) clearBtn.addEventListener('click', function () {
      input.value = '';
      reset();
      input.focus();
    });
  });
})();
</script>