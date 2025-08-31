---
title: "Formations & Certifications"
permalink: /formations/
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
.form-wrap{max-width:1100px;margin:40px auto;padding:0 20px;font-family:var(--font-sans);color:#222;line-height:1.65}
.form-header{margin-bottom:28px}
.form-header h1{font-size:34px;letter-spacing:.02em;margin:0 0 6px;color:var(--blue-strong)}
.form-header p{margin:0;color:var(--muted);font-size:15px}

.form-accordion{display:grid;gap:var(--gap);margin-top:18px}
.form-accordion details{border-radius:var(--radius);overflow:hidden;background:transparent}
.form-accordion details summary{
  list-style:none;cursor:pointer;background:var(--blue);color:#fff;
  padding:16px 22px;font-weight:700;font-size:16px;letter-spacing:.02em;
  display:flex;align-items:center;justify-content:space-between;
  transition:background .18s ease,transform .08s ease;
}
.form-accordion details summary::-webkit-details-marker{display:none}
.form-accordion details summary:hover,
.form-accordion details summary:focus{
  background:linear-gradient(180deg,var(--blue) 0%,var(--blue-strong) 100%);
  transform:translateY(-1px);outline:none
}
.summary-arrow{display:inline-block;width:20px;height:20px;transform:rotate(0deg);transition:transform .35s ease;opacity:.95}
.form-accordion details[open] summary .summary-arrow{transform:rotate(180deg)}
.form-accordion details .panel{
  background:var(--panel);border:1px solid rgba(0,0,0,0.06);border-top:none;
  padding:0 22px;border-radius:0 0 var(--radius) var(--radius);
  box-shadow:0 8px 26px rgba(10,20,30,0.05);
  color:#333;overflow:hidden;max-height:0;opacity:0;
  transition:max-height 1s cubic-bezier(.2,.9,.2,1),opacity .95s ease
}
.form-accordion details[open] .panel{padding:18px 22px 22px;max-height:1400px;opacity:1}
.panel h3{margin:0 0 8px;color:#12263b;font-size:15px;font-weight:700}
.panel p,.panel li{margin:6px 0;font-size:14px}
.panel ul{margin:6px 0 0 18px;padding:0}
.panel li{margin-bottom:8px}

/* Search bar */
.form-header-row{display:flex;align-items:center;justify-content:space-between;gap:12px;flex-wrap:wrap}
.searchbar{position:relative;min-width:280px}
#formSearch{appearance:none;width:320px;max-width:100%;padding:10px 36px 10px 12px;border:1px solid rgba(0,0,0,.15);border-radius:8px;font-size:14px}
#formSearch:focus{outline:none;box-shadow:0 0 0 3px rgba(23,76,123,.15);border-color:var(--blue)}
#clearFormSearch{position:absolute;right:8px;top:50%;transform:translateY(-50%);background:transparent;border:0;font-size:16px;color:#999;cursor:pointer;display:none}
#formSearch{background:#d9ebff;border:1px solid #a8c9f0;color:#123d63;font-weight:500}
#formSearch::placeholder{color:#5b87aa;opacity:.9}
#formMeta{margin-top:6px;color:var(--muted);font-size:13px}
.is-hidden{display:none!important}

/* highlight */
mark.hl{background:#ffeb3b66;color:#111;padding:0 .15em;border-radius:3px;box-shadow:inset 0 0 0 1px #f0d00080}
</style>

<div class="form-wrap">
  <div class="form-header">
    <div class="form-header-row">
      <p style="margin:0">Formations académiques, certifications et autoformations Cloud & DevOps.</p>
      <div class="searchbar">
        <input type="search" id="formSearch" placeholder="Rechercher (Azure, DevOps, Terraform…)" aria-label="Rechercher une formation">
        <button type="button" id="clearFormSearch" aria-label="Effacer">✕</button>
      </div>
    </div>
    <div id="formMeta"></div>
  </div>

  <div class="form-accordion" id="formAccordion">

    <!-- Autoformation -->
    <details>
      <summary>
        <span>Autoformation continue — Cloud & DevOps | Mai 2025 – En cours</span>
        <span class="summary-arrow">▾</span>
      </summary>
      <div class="panel">
        <ul>
          <li>Azure Cloud & Terraform (niveau ingénieur Cloud).</li>
          <li>Projets pratiques CI/CD avec GitHub Actions.</li>
          <li>Publication progressive de projets sur GitHub (hands-on).</li>
          <li>Préparation certification <strong>HashiCorp Terraform Associate</strong>.</li>
          <li>Approfondissement Microsoft 365 & culture DevOps.</li>
        </ul>
      </div>
    </details>

    <!-- Formation privée -->
    <details>
      <summary>
        <span>Formation privée — DevOps & Cloud (Huzefai, Inde) | Fév. 2025 – Août 2025</span>
        <span class="summary-arrow">▾</span>
      </summary>
      <div class="panel">
        <ul>
          <li>DevOps & Azure DevOps (CI/CD : Jenkins, GitHub Actions, Azure Pipelines).</li>
          <li>Conteneurs & orchestration : Docker, Swarm, Kubernetes (AKS, Minikube, YAML).</li>
          <li>Cloud multi-provider : Azure (admin), AWS (EC2, S3, VPC), GCP (initiation).</li>
          <li>Infrastructure as Code : Terraform, Ansible, YAML.</li>
          <li>Linux systèmes : gestion utilisateurs, sécurité, scripts Bash.</li>
        </ul>
        <p><em>80% pratique — axée projets réels DevOps & Cloud.</em></p>
      </div>
    </details>

    <!-- Certification -->
    <details>
      <summary>
        <span>Certification Microsoft Azure Administrator (AZ-104) | Fév. 2025</span>
        <span class="summary-arrow">▾</span>
      </summary>
      <div class="panel">
        <p>Réussie avec succès (<strong>Score 853/1000</strong>).</p>
        <ul>
          <li>+500h labs, 60 scénarios réels (cloud hybride & entreprise).</li>
          <li>Azure Infra : VMs, Disks, Load Balancer, Availability, Bastion.</li>
          <li>Réseau & Sécurité : VNet, NSG, VPN Gateway, Firewall, App Gateway.</li>
          <li>Stockage & DB : Blob, File Share, Azure SQL/MySQL.</li>
          <li>Identité & Gouvernance : Azure AD, RBAC, Policies, Management Groups.</li>
          <li>DevOps & automatisation : PowerShell, Azure CLI, ARM, IaC.</li>
        </ul>
        <p>
          🔗 <a href="https://learn.microsoft.com/api/credentials/share/fr-fr/PaulPaul-2197/637D25067696EBC3?sharingId=D25051DD12D1109C" target="_blank">Certification officielle AZ-104</a><br>
          🔗 <a href="/assets/pdf/Mes_compétences_Azure_cloud.pdf" target="_blank">Télécharger le sommaire détaillé (PDF)</a>
        </p>
      </div>
    </details>

    <!-- IUT -->
    <details>
      <summary>
        <span>Licence Professionnelle Informatique — IUT de Bobigny | 2020 – 2021</span>
        <span class="summary-arrow">▾</span>
      </summary>
      <div class="panel">
        <ul>
          <li>Développement Web & Mobile (Android, iOS, Flutter, PHP, JS, SQL, CMS).</li>
          <li>Réseaux & systèmes : Linux, Wireshark, Kali.</li>
          <li>Design & multimédia : Photoshop, Illustrator, After Effects, Canva.</li>
        </ul>
      </div>
    </details>

    <!-- BTS -->
    <details>
      <summary>
        <span>BTS SIO SLAM — Lycée Louise Michel, Bobigny | 2018 – 2020</span>
        <span class="summary-arrow">▾</span>
      </summary>
      <div class="panel">
        <ul>
          <li>Développement logiciel & Web (Java, C#, PHP, SQL, WordPress).</li>
          <li>Réalisation de projets dynamiques en Java et PHP.</li>
        </ul>
      </div>
    </details>

  </div>
</div>

<script>
document.addEventListener("DOMContentLoaded", () => {
  const acc = document.getElementById("formAccordion");
  const input = document.getElementById("formSearch");
  const clearBtn = document.getElementById("clearFormSearch");
  const meta = document.getElementById("formMeta");
  const items = [...acc.querySelectorAll("details")];

  function norm(s){return (s||"").toLowerCase().normalize("NFD").replace(/[\u0300-\u036f]/g,"");}
  function removeHighlights(el){el.querySelectorAll("mark.hl").forEach(m=>m.replaceWith(document.createTextNode(m.textContent)));}

  function highlight(el, query){
    if(!query) return;
    removeHighlights(el);
    const nq=norm(query);
    function walk(n){
      if(n.nodeType===3){
        let o=n.nodeValue, frag=document.createDocumentFragment();
        let regex=new RegExp("("+query+")","gi");
        let parts=o.split(regex);
        parts.forEach(p=>{
          if(norm(p)===nq){
            let mark=document.createElement("mark");
            mark.className="hl";mark.textContent=p;frag.appendChild(mark);
          }else frag.appendChild(document.createTextNode(p));
        });
        n.replaceWith(frag);
      } else if(n.nodeType===1 && n.childNodes && !["SCRIPT","STYLE","MARK"].includes(n.tagName)){
        [...n.childNodes].forEach(walk);
      }
    }
    walk(el);
  }

  function reset(){
    items.forEach(d=>{d.classList.remove("is-hidden");d.removeAttribute("open");removeHighlights(d);});
    clearBtn.style.display="none";meta.textContent="";
    window.__formSearchActive=false;
  }

  function search(q){
    const query=norm(q.trim());
    if(!query){reset();return;}
    window.__formSearchActive=true;
    let matches=0;
    items.forEach(d=>{
      const text=norm(d.textContent||"");
      if(text.includes(query)){
        d.classList.remove("is-hidden");d.setAttribute("open","");
        highlight(d,q);matches++;
      } else {d.classList.add("is-hidden");d.removeAttribute("open");removeHighlights(d);}
    });
    clearBtn.style.display="inline";
    meta.textContent=(matches>0)?matches+" formation(s) trouvée(s) pour « "+q+" »":"Aucun résultat pour « "+q+" »";
  }

  input.addEventListener("input",e=>search(e.target.value));
  clearBtn.addEventListener("click",()=>{input.value="";reset();input.focus();});
});
</script>
