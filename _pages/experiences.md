---
title: "Expériences"
permalink: /experiences/
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
.exp-wrap{max-width:1100px;margin:40px auto;padding:0 20px;font-family:var(--font-sans);color:#222;line-height:1.65}
.exp-header{margin-bottom:28px}
.exp-header h1{font-size:34px;letter-spacing:.02em;margin:0 0 6px;color:var(--blue-strong)}
.exp-header p{margin:0;color:var(--muted);font-size:15px}

.experiences-accordion{display:grid;gap:var(--gap);margin-top:18px}
.experiences-accordion details{border-radius:var(--radius);overflow:hidden;background:transparent}
.experiences-accordion details summary{
  list-style:none;cursor:pointer;background:var(--blue);color:#fff;
  padding:16px 22px;font-weight:700;font-size:16px;letter-spacing:.02em;
  display:flex;align-items:center;justify-content:space-between;
  transition:background .18s ease,transform .08s ease;
  border:1px solid rgba(0,0,0,0.03)
}
.experiences-accordion details summary::-webkit-details-marker{display:none}
.experiences-accordion details summary:hover,
.experiences-accordion details summary:focus{
  background:linear-gradient(180deg,var(--blue) 0%,var(--blue-strong) 100%);
  transform:translateY(-1px);outline:none
}
.summary-arrow{display:inline-block;width:20px;height:20px;transform:rotate(0deg);transition:transform .35s ease;opacity:.95}
.experiences-accordion details[open] summary .summary-arrow{transform:rotate(180deg)}
.experiences-accordion details .panel{
  background:var(--panel);border:1px solid rgba(0,0,0,0.06);border-top:none;
  padding:0 22px;border-radius:0 0 var(--radius) var(--radius);
  box-shadow:0 8px 26px rgba(10,20,30,0.05);
  color:#333;overflow:hidden;max-height:0;opacity:0;
  transition:max-height 1s cubic-bezier(.2,.9,.2,1),opacity .95s ease
}
.experiences-accordion details[open] .panel{padding:18px 22px 22px;max-height:1400px;opacity:1}
.panel h3{margin:0 0 8px;color:#12263b;font-size:15px;font-weight:700}
.panel p,.panel li{margin:6px 0;font-size:14px}
.panel ul{margin:6px 0 0 18px;padding:0}
.panel li{margin-bottom:8px}

/* Search bar */
.exp-header-row{display:flex;align-items:center;justify-content:space-between;gap:12px;flex-wrap:wrap}
.searchbar{position:relative;min-width:280px}
#expSearch{appearance:none;width:320px;max-width:100%;padding:10px 36px 10px 12px;border:1px solid rgba(0,0,0,.15);border-radius:8px;font-size:14px}
#expSearch:focus{outline:none;box-shadow:0 0 0 3px rgba(23,76,123,.15);border-color:var(--blue)}
#clearExpSearch{position:absolute;right:8px;top:50%;transform:translateY(-50%);background:transparent;border:0;font-size:16px;color:#999;cursor:pointer;display:none}
#expSearch{background:#d9ebff;border:1px solid #a8c9f0;color:#123d63;font-weight:500}
#expSearch::placeholder{color:#5b87aa;opacity:.9}
#expMeta{margin-top:6px;color:var(--muted);font-size:13px}
.is-hidden{display:none!important}

/* highlight */
mark.hl{background:#ffeb3b66;color:#111;padding:0 .15em;border-radius:3px;box-shadow:inset 0 0 0 1px #f0d00080}
</style>

<div class="exp-wrap">
  <div class="exp-header">
    <div class="exp-header-row">
      <p style="margin:0">Expériences professionnelles et projets personnels.</p>
      <div class="searchbar">
        <input type="search" id="expSearch" placeholder="Rechercher (Azure, DevOps, Support…)" aria-label="Rechercher une expérience">
        <button type="button" id="clearExpSearch" aria-label="Effacer">✕</button>
      </div>
    </div>
    <div id="expMeta"></div>
  </div>

  <div class="experiences-accordion" id="experiencesAccordion">

    <!-- Projets Cloud & DevOps -->
    <details>
      <summary>
        <span>🚀 Projets Cloud & DevOps | Perso - Autonomie | Décembre 2024 - En cours</span>
        <span class="summary-arrow">▾</span>
      </summary>
      <div class="panel">
        <p><strong>Lieu :</strong> LAB Personnel<br>
        <strong>Période :</strong> Décembre 2024 – En cours<br>
        <strong>Poste :</strong> DevOps & Cloud Projects (autodidacte)</p>
        <ul>
          <li>Déploiement d’une application Laravel (PHP + MySQL + Redis) sur Azure App Service avec pipeline CI/CD GitHub Actions, Private Endpoints, Key Vault, SSH et logs.</li>
          <li>Pipeline CI/CD complet avec Jenkins, Docker, Terraform et Azure pour build & déploiement d’une app JavaScript.</li>
          <li>Migration de VM on-premises vers Azure avec Azure Migrate (discovery, réplication, test de connectivité).</li>
          <li>Configuration de VPN site-to-site & point-to-site (S2S/P2S) avec certificats et routage.</li>
          <li>Application des pratiques DevOps (~6h/j), documentation régulière sur GitHub.</li>
        </ul>
      </div>
    </details>

    <!-- Ministère Justice -->
    <details>
      <summary>
        <span>💼 Technicien Informatique de Proximité | Ministère de la Justice | Décembre 2023 - Juillet 2024</span>
        <span class="summary-arrow">▾</span>
      </summary>
      <div class="panel">
        <p><strong>Lieu :</strong> Bobigny, France<br>
        <strong>Période :</strong> Décembre 2023 – Juillet 2024<br>
        <strong>Poste :</strong>Technicien Informatique de Proximité</p>
        <ul>
          <li>Gestion des incidents et demandes (N1/N2) via GLPI selon les normes ITIL.</li>
          <li>Support utilisateurs VIP sur site et à distance (RDP, TeamViewer, AnyDesk).</li>
          <li>Administration des identités : Active Directory, gestion des accès, groupes, MFA.</li>
          <li>Installation, masterisation, maintenance des postes Windows 10/11, imprimantes.</li>
          <li>Administration Microsoft 365 (Exchange, Outlook, Teams, OneDrive), scripts PowerShell.</li>
          <li>Dépannage réseau local (Wi-Fi, switchs, routeurs, téléphonie IP, brassage).</li>
          <li>Suivi du parc informatique, inventaire et reporting via Power BI Report Server.</li>
          <li>Application des politiques de sécurité, conformité RGPD, contrôle des droits.</li>
          <li>Collaboration avec équipes DSI, documentation technique simplifiée.</li>
        </ul>
      </div>
    </details>

    <!-- BNP -->
    <details>
      <summary>
        <span>💼 Technicien Support (Akkodis) | BNP Paribas | Septembre 2023 - Septembre 2023</span>
        <span class="summary-arrow">▾</span>
      </summary>
      <div class="panel">
        <p><strong>Lieu :</strong> Nanterre, France<br>
        <strong>Période :</strong> Septembre 2023 – Septembre 2023<br>
        <strong>Poste :</strong> Technicien Support IT (Mission intérim)</p>
        <ul>
          <li>Installation et configuration de postes (PC, imprimantes, copieurs) avec suivi en équipe.</li>
          <li>Support N1/N2 sur Windows, MacOS, iOS et Android (à distance via TeamViewer et sur site).</li>
          <li>Gestion des tickets (GLPI) et mise à jour des inventaires IT (Excel).</li>
          <li>Paramétrage et dépannage systèmes et logiciels.</li>
        </ul>
      </div>
    </details>

    <!-- Cojean -->
    <details>
      <summary>
        <span>💼 Employé polyvalent et gestion de stock | Labo de Cojean | Avril 2022 - Juin 2023</span>
        <span class="summary-arrow">▾</span>
      </summary>
      <div class="panel">
        <p><strong>Lieu :</strong> Saint-Ouen, France<br>
        <strong>Période :</strong> Avril 2022 – Juin 2023<br>
        <strong>Poste :</strong>Employé polyvalent et gestion de stock</p>
        <ul>
          <li>Suivi de production et gestion d’équipe avec Office 365 (Excel, Teams, SharePoint).</li>
          <li>Facturation électronique, gestion des commandes et des stocks via ERP interne.</li>
        </ul>
      </div>
    </details>

    <!-- Alternance -->
    <details>
      <summary>
        <span>💻 IT Technician & Full Stack Developer en Alternance | CFM France | Septembre 2020 - Octobre 2021</span>
        <span class="summary-arrow">▾</span>
      </summary>
      <div class="panel">
        <p><strong>Lieu :</strong> Bobigny, France<br>
        <strong>Période :</strong> Septembre 2020 – Octobre 2021<br>
        <strong>Poste :</strong> Technicien Informatique & Développeur Full Stack (alternance)</p>
        <ul>
          <li>Conception & gestion de 5 projets web (PHP, JS, WP), déploiement cloud (OVH).</li>
          <li>Formation utilisateurs (M365, Zoom, WordPress) & support N1/N2.</li>
          <li>Installation/imaging postes (Windows, Android, iOS).</li>
          <li>Gestion serveurs cloud (Azure), SSH/Putty, automatisation PowerShell.</li>
          <li>Sécurité & optimisation réseau/systèmes, documentation IT.</li>
        </ul>
      </div>
    </details>

  </div>
</div>

<script>
document.addEventListener("DOMContentLoaded", () => {
  const acc = document.getElementById("experiencesAccordion");
  const input = document.getElementById("expSearch");
  const clearBtn = document.getElementById("clearExpSearch");
  const meta = document.getElementById("expMeta");
  const items = [...acc.querySelectorAll("details")];

  function norm(s){return (s||"").toLowerCase().normalize("NFD").replace(/[\u0300-\u036f]/g,"");}
  function removeHighlights(el){el.querySelectorAll("mark.hl").forEach(m=>m.replaceWith(document.createTextNode(m.textContent)));}

  function highlight(el, query){
    if(!query) return;
    removeHighlights(el);
    const nq=norm(query);
    function walk(n){
      if(n.nodeType===3){
        let text=n.nodeValue;
        let normText=norm(text);
        let idx=normText.indexOf(nq);
        if(idx!==-1){
          const frag=document.createDocumentFragment();
          let last=0;
          while(idx!==-1){
            frag.appendChild(document.createTextNode(text.slice(last,idx)));
            const mark=document.createElement("mark");
            mark.className="hl";
            mark.textContent=text.slice(idx,idx+query.length);
            frag.appendChild(mark);
            last=idx+query.length;
            idx=norm(text.slice(last)).indexOf(nq);
            if(idx!==-1) idx+=last;
          }
          frag.appendChild(document.createTextNode(text.slice(last)));
          n.replaceWith(frag);
        }
      } else if(n.nodeType===1 && n.childNodes && !["SCRIPT","STYLE","MARK"].includes(n.tagName)){
        [...n.childNodes].forEach(walk);
      }
    }
    walk(el);
  }

  function reset(){
    items.forEach(d=>{d.classList.remove("is-hidden");d.removeAttribute("open");removeHighlights(d);});
    clearBtn.style.display="none";meta.textContent="";
    window.__expSearchActive=false;
  }

  function search(q){
    const query=norm(q.trim());
    if(!query){reset();return;}
    window.__expSearchActive=true;
    let matches=0;
    items.forEach(d=>{
      const text=norm(d.textContent||"");
      if(text.includes(query)){
        d.classList.remove("is-hidden");d.setAttribute("open","");
        highlight(d,q);matches++;
      } else {d.classList.add("is-hidden");d.removeAttribute("open");removeHighlights(d);}
    });
    clearBtn.style.display="inline";
    meta.textContent=(matches>0)?matches+" expérience(s) trouvée(s) pour « "+q+" »":"Aucun résultat pour « "+q+" »";
  }

  input.addEventListener("input",e=>search(e.target.value));
  clearBtn.addEventListener("click",()=>{input.value="";reset();input.focus();});
});
</script>
