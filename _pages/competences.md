---
title: "Compétences"
permalink: /competences/
layout: single
classes: wide
author_profile: false
---

<style>
body {
  font-family: 'Inter', 'Segoe UI', Tahoma, sans-serif;
  color: #333;
  line-height: 1.6;
}

.accordion {
  margin-bottom: 1rem;
  border-radius: 12px;
  border: 1px solid #ddd;
  overflow: hidden;
  box-shadow: 0 2px 6px rgba(0,0,0,0.05);
}

.accordion input {
  display: none;
}

.accordion-label {
  display: block;
  padding: 1rem;
  background: #f9f9f9;
  font-weight: 600;
  cursor: pointer;
  position: relative;
  transition: background 0.3s ease;
}

.accordion-label:hover {
  background: #eef6ff;
}

.accordion-label::after {
  content: '➕';
  position: absolute;
  right: 1rem;
  transition: transform 0.3s ease;
}

.accordion input:checked + .accordion-label::after {
  content: '➖';
}

.accordion-content {
  max-height: 0;
  overflow: hidden;
  background: #fff;
  transition: max-height 0.5s ease, padding 0.3s ease;
  padding: 0 1rem;
}

.accordion input:checked ~ .accordion-content {
  max-height: 1000px; /* assez grand pour le contenu */
  padding: 1rem;
}

.skill {
  margin-bottom: 1rem;
}

.skill-name {
  display: flex;
  justify-content: space-between;
  font-size: 0.9rem;
  margin-bottom: 0.3rem;
  color: #444;
}

.skill-bar {
  height: 8px;
  background: #eee;
  border-radius: 6px;
  overflow: hidden;
  position: relative;
}

.skill-bar span {
  display: block;
  height: 100%;
  background: linear-gradient(90deg, #0078d4, #00b4d8);
  width: 0;
  border-radius: 6px;
  animation: fill-bar 2s forwards;
}

@keyframes fill-bar {
  from { width: 0; }
  to { width: var(--level); }
}
</style>

<div class="accordion">
  <input type="checkbox" id="cloud">
  <label class="accordion-label" for="cloud">☁️ Cloud & Infrastructure</label>
  <div class="accordion-content">
    <div class="skill">
      <div class="skill-name"><span>Azure</span><span>85%</span></div>
      <div class="skill-bar"><span style="--level:85%"></span></div>
    </div>
    <div class="skill">
      <div class="skill-name"><span>AWS</span><span>70%</span></div>
      <div class="skill-bar"><span style="--level:70%"></span></div>
    </div>
    <div class="skill">
      <div class="skill-name"><span>Terraform</span><span>80%</span></div>
      <div class="skill-bar"><span style="--level:80%"></span></div>
    </div>
  </div>
</div>

<div class="accordion">
  <input type="checkbox" id="devops">
  <label class="accordion-label" for="devops">⚙️ DevOps & Automatisation</label>
  <div class="accordion-content">
    <div class="skill">
      <div class="skill-name"><span>Docker</span><span>75%</span></div>
      <div class="skill-bar"><span style="--level:75%"></span></div>
    </div>
    <div class="skill">
      <div class="skill-name"><span>Kubernetes</span><span>65%</span></div>
      <div class="skill-bar"><span style="--level:65%"></span></div>
    </div>
    <div class="skill">
      <div class="skill-name"><span>CI/CD (Azure DevOps, Jenkins)</span><span>80%</span></div>
      <div class="skill-bar"><span style="--level:80%"></span></div>
    </div>
  </div>
</div>

<div class="accordion">
  <input type="checkbox" id="security">
  <label class="accordion-label" for="security">🔒 Sécurité & Observabilité</label>
  <div class="accordion-content">
    <div class="skill">
      <div class="skill-name"><span>IAM & RBAC</span><span>85%</span></div>
      <div class="skill-bar"><span style="--level:85%"></span></div>
    </div>
    <div class="skill">
      <div class="skill-name"><span>Monitoring (App Insights, Log Analytics)</span><span>75%</span></div>
      <div class="skill-bar"><span style="--level:75%"></span></div>
    </div>
  </div>
</div>
