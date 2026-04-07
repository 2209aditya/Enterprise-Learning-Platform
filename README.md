<div align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:0F2027,50:203A43,100:2C5364&height=200&section=header&text=SkillForge&fontSize=80&fontColor=FFFFFF&fontAlignY=38&desc=Enterprise%20Learning%20Platform%20%E2%80%94%20DevOps%20Driven&descAlignY=62&descColor=A8D8EA&animation=fadeIn" width="100%"/>
</div>

<br/>

<div align="center">

[![Azure DevOps](https://img.shields.io/badge/Azure_DevOps-CI%2FCD-0078D7?style=for-the-badge&logo=azure-devops&logoColor=white)](https://dev.azure.com)
[![Spring Boot](https://img.shields.io/badge/Spring_Boot-3.x-6DB33F?style=for-the-badge&logo=spring-boot&logoColor=white)](https://spring.io)
[![Angular](https://img.shields.io/badge/Angular-17-DD0031?style=for-the-badge&logo=angular&logoColor=white)](https://angular.io)
[![Kubernetes](https://img.shields.io/badge/AKS-Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)](https://kubernetes.io)
[![Terraform](https://img.shields.io/badge/Terraform-IaC-7B42BC?style=for-the-badge&logo=terraform&logoColor=white)](https://terraform.io)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Database-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)](https://postgresql.org)

<br/>

[![Build](https://img.shields.io/badge/Build-Passing-brightgreen?style=flat-square)](https://dev.azure.com)
[![Coverage](https://img.shields.io/badge/Coverage-87%25-green?style=flat-square)](https://sonarqube.io)
[![Security](https://img.shields.io/badge/Trivy-0%20Critical-success?style=flat-square)](https://github.com/aquasecurity/trivy)
[![License](https://img.shields.io/badge/License-MIT-yellow?style=flat-square)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-Welcome-brightgreen?style=flat-square)](CONTRIBUTING.md)

<br/>

> **SkillForge** is a production-grade enterprise learning platform that helps organizations upskill employees in DevOps, Cloud, Java, and more — deployed on **Azure AKS** using fully automated multi-environment **CI/CD pipelines**, **Terraform IaC**, and a **Blue-Green deployment** strategy.

<br/>

**[🚀 Live Demo](https://skillforge.yourdomain.com)** &nbsp;·&nbsp; **[📖 Docs](docs/)** &nbsp;·&nbsp; **[🏗️ Architecture](#-system-architecture)** &nbsp;·&nbsp; **[🚦 Pipeline](#-cicd-pipeline)** &nbsp;·&nbsp; **[⚡ Quick Start](#-quick-start)**

</div>

---

## 📌 Table of Contents

- [✨ What is SkillForge?](#-what-is-skillforge)
- [🏗️ System Architecture](#-system-architecture)
- [🔬 Microservices](#-microservices)
- [⚙️ Tech Stack](#️-tech-stack)
- [☁️ Azure Infrastructure](#️-azure-infrastructure)
- [🔁 CI/CD Pipeline](#-cicd-pipeline)
- [🌍 Multi-Environment Strategy](#-multi-environment-strategy)
- [🔐 Security](#-security)
- [📚 Platform Features](#-platform-features)
- [🧠 Roadmap Engine](#-roadmap-engine)
- [🏆 Gamification](#-gamification)
- [📊 Monitoring & Observability](#-monitoring--observability)
- [🔁 Disaster Recovery](#-disaster-recovery)
- [📂 Repo Structure](#-repo-structure)
- [⚡ Quick Start](#-quick-start)
- [💼 Interview & Resume](#-interview--resume)
- [🤝 Contributing](#-contributing)

---

## ✨ What is SkillForge?

SkillForge solves a real enterprise problem — **structured, trackable employee upskilling at scale** — backed by the kind of DevOps infrastructure you'd find at top-tier product companies.

<table>
<tr>
<td width="50%">

**🎓 For Employees**
- Personalized learning roadmaps
- Course progress & quiz tracking
- Certifications & achievement badges
- Team leaderboard & points system

</td>
<td width="50%">

**🏢 For Organizations**
- Multi-environment AKS deployment
- Zero-downtime Blue-Green rollouts
- Full DR strategy (RTO < 10 min)
- Enterprise RBAC & Key Vault security

</td>
</tr>
</table>

---

## 🏗️ System Architecture

```
                    ┌──────────────────────────────────────────────────┐
                    │            Azure Front Door (Global CDN)          │
                    └─────────────────────┬────────────────────────────┘
                                          │ HTTPS
                    ┌─────────────────────▼────────────────────────────┐
                    │        API Gateway / Nginx Ingress Controller      │
                    │             (Rate Limiting · Auth · TLS)           │
                    └───┬───────────┬──────────┬──────────┬────────────┘
                        │           │           │          │
         ┌──────────────▼──┐  ┌─────▼──────┐ ┌─▼──────┐ ┌▼─────────────────┐
         │  User Service   │  │Course Svc  │ │Progress│ │Notification Svc  │
         │  :8081 (Auth)   │  │  :8082     │ │  :8083 │ │     :8085        │
         └──────┬──────────┘  └─────┬──────┘ └───┬────┘ └──────────────────┘
                │                   │             │
         ┌──────▼───────────────────▼─────────────▼──────────────────────────┐
         │                   Azure Service Bus (Async Messaging)              │
         └──────────────────────────┬────────────────────────────────────────┘
                                    │
         ┌──────────────────────────▼────────────────────────────────────────┐
         │   Azure PostgreSQL Flexible Server  │  Azure Cache for Redis       │
         └───────────────────────────────────────────────────────────────────┘
                                    │
         ┌──────────────────────────▼────────────────────────────────────────┐
         │                   Azure Key Vault (All Secrets)                    │
         └───────────────────────────────────────────────────────────────────┘
```

> All services run inside **Azure Kubernetes Service (AKS)** pods, managed via **Helm charts**. Each environment (DEV / UAT / PRE-PROD / PROD / DR) has its own isolated resource group and configuration.

---

## 🔬 Microservices

| Service | Responsibility | Port |
|:---|:---|:---|
| 🔐 **User Service** | Auth, JWT, roles (Employee / Manager / Admin) | `8081` |
| 📚 **Course Service** | Courses, modules, content, external links | `8082` |
| 📊 **Progress Service** | Completion %, quiz scores, points, certifications | `8083` |
| 🧠 **Recommendation Service** | AI-driven personalized roadmap generation | `8084` |
| 🔔 **Notification Service** | Email + Slack alerts on milestones | `8085` |

---

## ⚙️ Tech Stack

<table>
<tr><th>Layer</th><th>Technology</th></tr>
<tr>
<td><b>Backend</b></td>
<td>

![Java](https://img.shields.io/badge/Java_17-ED8B00?style=flat-square&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot_3-6DB33F?style=flat-square&logo=spring&logoColor=white)
![Spring Security](https://img.shields.io/badge/Spring_Security-6DB33F?style=flat-square&logo=spring-security&logoColor=white)

</td>
</tr>
<tr>
<td><b>Frontend</b></td>
<td>

![Angular](https://img.shields.io/badge/Angular_17-DD0031?style=flat-square&logo=angular&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![TailwindCSS](https://img.shields.io/badge/Tailwind_CSS-06B6D4?style=flat-square&logo=tailwindcss&logoColor=white)

</td>
</tr>
<tr>
<td><b>Database & Cache</b></td>
<td>

![PostgreSQL](https://img.shields.io/badge/Azure_PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![Redis](https://img.shields.io/badge/Azure_Redis-DC382D?style=flat-square&logo=redis&logoColor=white)

</td>
</tr>
<tr>
<td><b>Messaging</b></td>
<td>

![Azure Service Bus](https://img.shields.io/badge/Azure_Service_Bus-0078D4?style=flat-square&logo=microsoft-azure&logoColor=white)

</td>
</tr>
<tr>
<td><b>DevOps</b></td>
<td>

![Azure DevOps](https://img.shields.io/badge/Azure_DevOps-0078D7?style=flat-square&logo=azure-devops&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![Kubernetes](https://img.shields.io/badge/AKS-326CE5?style=flat-square&logo=kubernetes&logoColor=white)
![Helm](https://img.shields.io/badge/Helm-0F1689?style=flat-square&logo=helm&logoColor=white)

</td>
</tr>
<tr>
<td><b>IaC & Security</b></td>
<td>

![Terraform](https://img.shields.io/badge/Terraform-7B42BC?style=flat-square&logo=terraform&logoColor=white)
![Key Vault](https://img.shields.io/badge/Azure_Key_Vault-0078D4?style=flat-square&logo=microsoft-azure&logoColor=white)
![SonarQube](https://img.shields.io/badge/SonarQube-4E9BCD?style=flat-square&logo=sonarqube&logoColor=white)
![Trivy](https://img.shields.io/badge/Trivy-1904DA?style=flat-square&logo=aqua-security&logoColor=white)

</td>
</tr>
</table>

---

## ☁️ Azure Infrastructure

```
Azure Subscription
│
├── 🔵 skillforge-dev          (Developer testing)
│   ├── AKS Cluster            (1 node pool, Standard_D2s_v3)
│   ├── PostgreSQL Flexible    (Burstable tier)
│   ├── Redis Cache            (Basic C0)
│   └── Key Vault
│
├── 🟡 skillforge-uat          (QA & stakeholder validation)
│
├── 🟠 skillforge-preprod      (Production-like testing)
│
├── 🔴 skillforge-prod         (Live users — High Availability)
│   ├── AKS Cluster            (3 node pools, zone redundant)
│   ├── PostgreSQL Flexible    (General Purpose, zone redundant)
│   ├── Redis Cache            (Premium P1, clustered)
│   ├── Azure Front Door       (Global routing + WAF)
│   └── Application Gateway
│
└── ⚫ skillforge-dr            (Disaster Recovery — secondary region)
    ├── AKS Cluster            (Standby, scaled to 0)
    ├── PostgreSQL Replica      (Real-time streaming from PROD)
    └── Front Door Failover     (Auto-triggered on health check fail)
```

---

## 🔁 CI/CD Pipeline

### 🧪 CI — Triggered on Every Push / PR

```
  ✅  Checkout & Version Tagging
  ☕  Maven Build + Unit Tests       (JUnit 5)
  📊  SonarQube Quality Gate         (Coverage ≥ 80%, 0 Blocker issues)
  🔒  Trivy Container Scan           (0 CRITICAL vulnerabilities to pass)
  🐳  Docker Build & Push            → Azure Container Registry (ACR)
  📦  Helm Chart Package & Publish   → Azure Artifact Feed
  💬  Slack Notification             → #deployments channel
```

### 🚀 CD — Multi-Environment Promotion

```
  Push to develop
        │
        ▼
  ┌─────────────┐  Auto  ┌─────────────┐  Auto  ┌──────────────────┐
  │   🔵 DEV    │───────▶│   🟡 UAT    │───────▶│  🟠 PRE-PROD    │
  │  (No gate)  │        │  (No gate)  │        │  ✅ 1 Approval   │
  └─────────────┘        └─────────────┘        └────────┬─────────┘
                                                          │ Manual
                                                          ▼
                                                ┌─────────────────────┐
                                                │     🔴 PROD         │
                                                │  ✅ 2 Approvals     │
                                                │  Blue-Green Deploy  │
                                                └──────────┬──────────┘
                                                           │ Manual (SRE)
                                                           ▼
                                                ┌─────────────────────┐
                                                │      ⚫ DR           │
                                                │  ✅ SRE Approval    │
                                                └─────────────────────┘
```

### 🔵🟢 Blue-Green Deployment (PROD)

```
  Step 1  →  Deploy new version to GREEN slot (zero live traffic)
  Step 2  →  Run automated smoke tests on GREEN
  Step 3  →  Shift 100% traffic: Front Door → GREEN  (instant, zero downtime)
  Step 4  →  Monitor for 15 min (error rate + latency alerts)
  Step 5a →  ✅ Success: decommission BLUE
  Step 5b →  ❌ Issue:   1-click rollback → BLUE restored in < 2 min
```

---

## 🌍 Multi-Environment Strategy

| Env | Purpose | Deploy Trigger | Approvals |
|:---:|:---|:---|:---:|
| 🔵 **DEV** | Developer testing | Auto on `develop` push | ❌ |
| 🟡 **UAT** | QA & stakeholder validation | Auto after DEV | ❌ |
| 🟠 **PRE-PROD** | Production parity testing | Manual | ✅ 1 |
| 🔴 **PROD** | Live users | Manual | ✅ 2 |
| ⚫ **DR** | Disaster Recovery | Manual (SRE) | ✅ SRE |

---

## 🔐 Security

```
🔑  Azure Key Vault           All secrets — DB passwords, JWT keys, API tokens
🛡️  Azure RBAC                Least-privilege roles across all Azure resources
👤  Kubernetes RBAC            Pod-level access control per namespace
🔐  Azure AD SSO              Employee single sign-on
🎫  JWT Tokens                Stateless API auth (15-min access + refresh)
🌐  HTTPS Everywhere          TLS enforced via Front Door + Cert Manager
🚪  API Gateway               Rate limiting (500 req/min), IP allowlisting
📦  Trivy Scanning            Blocks deploys on ANY critical CVE
🔒  Network Policies           Zero-trust service-to-service traffic in AKS
🧱  Pod Security Standards     Restricted pod policies — no root containers
```

---

## 📚 Platform Features

### 🎓 Learning Tracks

| Track | Topics | Duration |
|:---|:---|:---:|
| ☸️ **DevOps Engineer** | Linux · Git · Docker · K8s · CI/CD · Azure | 12 weeks |
| ☁️ **Cloud Architect** | Azure Fundamentals · Solutions Arch · AKS · DR | 10 weeks |
| ☕ **Java Developer** | Core Java · Spring Boot · Microservices · REST | 8 weeks |
| 🗃️ **DSA & System Design** | Arrays · Trees · Graphs · LLD · HLD | 6 weeks |

### 👨‍💻 Employee Dashboard Features

| Feature | Description |
|:---|:---|
| 📈 **Progress Tracker** | Module-by-module completion with visual % bar |
| 🏆 **Leaderboard** | Live team + org rankings updated in real-time |
| 🎓 **Certifications** | Auto-issued on course completion |
| 🔥 **Streaks** | Daily learning streak with streak-freeze option |
| 🔔 **Smart Notifications** | Slack + email alerts on milestones & reminders |
| 🔗 **External Courses** | Integrated Udemy & Coursera links |

---

## 🧠 Roadmap Engine

```
  ╔══════════════════════════════════════════════════════╗
  ║       Your DevOps Learning Roadmap                   ║
  ╠══════════════════════════════════════════════════════╣
  ║  ✅  Step 1 · Linux Fundamentals        [Completed]  ║
  ║  ✅  Step 2 · Git & Version Control     [Completed]  ║
  ║  🔄  Step 3 · Docker & Containers      [In Progress] ║
  ║  ⏳  Step 4 · Kubernetes (AKS)         [Locked]      ║
  ║  ⏳  Step 5 · CI/CD with Azure DevOps  [Locked]      ║
  ║  ⏳  Step 6 · Cloud Architecture       [Locked]      ║
  ║  ⏳  Step 7 · SRE & Observability      [Locked]      ║
  ╠══════════════════════════════════════════════════════╣
  ║  Progress: ████████░░░░░░░░  42%   🔥 Streak: 7d    ║
  ╚══════════════════════════════════════════════════════╝
```

Auto-generated based on **employee role + current skill level** — no manual configuration needed.

---

## 🏆 Gamification

### Points System

| Action | Points |
|:---|:---:|
| ✅ Complete a Course | `+100` |
| 📝 Pass a Quiz (≥ 70%) | `+50` |
| 🎓 Earn a Certification | `+200` |
| 🔥 7-Day Learning Streak | `+75` |
| ⭐ #1 on Team Leaderboard | `+150` |
| 🗓️ Complete a Daily Goal | `+25` |

### Skill Levels

```
  🥉 Beginner        0  –   499 pts
  🥈 Intermediate   500 –  1499 pts
  🥇 Advanced      1500 –  3999 pts
  🏆 Expert        4000+       pts
```

---

## 📊 Monitoring & Observability

```
  Azure Monitor            →  CPU, memory, disk, network metrics
  Application Insights     →  API latency (p50/p95/p99), error rates
  Log Analytics Workspace  →  Centralized logs from all 5 microservices
  Azure Alerts             →  Slack + PagerDuty for:
                                 • Deployment failure
                                 • API p95 latency > 500ms
                                 • Pod crash loops (> 3 restarts/hour)
                                 • DB connections > 80% pool utilization
```

**SLOs tracked:**

| Metric | Target |
|:---|:---:|
| API P99 latency | `< 300ms` |
| Service uptime | `≥ 99.9%` |
| Deployment success rate | `≥ 99.5%` |
| Pod restart rate | `< 0.1 / hour` |

---

## 🔁 Disaster Recovery

```
  PROD (Primary — East US)               DR (Secondary — West Europe)
  ──────────────────────                  ──────────────────────────
  PostgreSQL  [Primary]  ──streaming──▶  PostgreSQL  [Replica]
  AKS Cluster [Active]                   AKS Cluster [Standby — scaled 0]
  Front Door  [Healthy]  ──failover───▶  Front Door  [DR endpoint]
```

| DR Metric | Target | Method |
|:---|:---:|:---|
| **RTO** | `< 10 min` | Automated Front Door failover |
| **RPO** | `< 5 min` | PostgreSQL streaming replication |
| Backup Frequency | Every 6 hours | Azure Backup + geo-redundant storage |
| DR Drill | Quarterly | Runbook in `docs/DR.md` |

---

## 📂 Repo Structure

```
skillforge/
│
├── 📁 frontend/                     # Angular 17 SPA
│   ├── src/app/
│   │   ├── dashboard/
│   │   ├── courses/
│   │   ├── leaderboard/
│   │   └── auth/
│   └── Dockerfile
│
├── 📁 backend/                      # Spring Boot Microservices
│   ├── user-service/
│   ├── course-service/
│   ├── progress-service/
│   ├── recommendation-service/
│   └── notification-service/
│
├── 📁 infra/                        # Terraform IaC
│   ├── modules/
│   │   ├── aks/
│   │   ├── db/
│   │   ├── network/
│   │   └── keyvault/
│   ├── dev/    uat/    preprod/
│   ├── prod/   dr/
│   └── variables.tf
│
├── 📁 pipelines/                    # Azure DevOps YAML
│   ├── ci-pipeline.yml
│   ├── cd-dev.yml
│   ├── cd-uat.yml
│   ├── cd-preprod.yml
│   ├── cd-prod.yml                  # Blue-Green deploy
│   └── cd-dr.yml
│
├── 📁 helm/                         # Helm charts
│   └── skillforge/
│       ├── Chart.yaml
│       ├── values.yaml
│       ├── values-dev.yaml
│       ├── values-prod.yaml
│       └── templates/
│
└── 📁 docs/
    ├── HLD.md
    ├── LLD.md
    ├── DR.md
    └── ARCHITECTURE.md
```

---

## ⚡ Quick Start

### Prerequisites

```bash
java --version     # 17+
node --version     # 18+
docker --version   # 24+
kubectl version    # 1.28+
helm version       # 3+
terraform version  # 1.6+
az --version       # Azure CLI 2.50+
```

### 1. Clone

```bash
git clone https://github.com/your-username/skillforge.git
cd skillforge
```

### 2. Run Locally

```bash
cd backend
docker-compose up -d       # Starts PostgreSQL + Redis + all 5 services
```

### 3. Start Frontend

```bash
cd frontend
npm install && npm start   # → http://localhost:4200
```

### 4. Deploy Infra (DEV)

```bash
cd infra/dev
terraform init
terraform plan -out=plan.tfplan
terraform apply plan.tfplan
```

### 5. Trigger CI/CD

```bash
# Push to develop → auto-deploys to DEV then UAT
git checkout develop
git push origin develop
# Pipeline: Build → SonarQube → Trivy → Docker Push → Helm → AKS
```

---

## 💼 Interview & Resume

### 🎯 Resume Line

> *Architected and delivered **SkillForge** — a production-grade enterprise learning platform on Azure with 5 Spring Boot microservices on AKS, a 5-environment Azure DevOps CI/CD pipeline (DEV → UAT → PRE-PROD → PROD → DR) with Blue-Green deployment, Terraform IaC, SonarQube + Trivy security gates, and a DR strategy achieving RTO < 10 min and RPO < 5 min.*

### 🧠 Interview Topics This Project Covers

| Topic | How It's Demonstrated |
|:---|:---|
| **Microservices** | 5 independent services, async via Azure Service Bus |
| **CI/CD** | Multi-stage Azure DevOps, 5 environments with gates |
| **Blue-Green Deploy** | Front Door traffic switching, 1-click rollback |
| **IaC** | Full Terraform modules for AKS, DB, networking |
| **Kubernetes** | Helm charts, HPA, pod security, namespaces |
| **Security** | Key Vault, RBAC, Trivy scan, JWT, Azure AD |
| **Disaster Recovery** | Streaming replication, standby cluster, failover |
| **Observability** | Azure Monitor, App Insights, Log Analytics, alerts |

### 🏷️ ATS Keywords

`Azure DevOps` · `AKS` · `Kubernetes` · `Terraform` · `CI/CD` · `Spring Boot` · `Microservices` · `Helm` · `Docker` · `Blue-Green Deployment` · `SonarQube` · `Trivy` · `Azure Key Vault` · `Disaster Recovery` · `Infrastructure as Code` · `Redis` · `PostgreSQL` · `Azure Service Bus` · `RBAC` · `API Gateway`

---

## 🤝 Contributing

```bash
# 1. Fork this repo and create your branch
git checkout -b feature/my-awesome-feature

# 2. Commit with conventional commits
git commit -m "feat(progress): add streak freeze mechanism"

# 3. Push — CI pipeline auto-triggers on your PR
git push origin feature/my-awesome-feature
```

See [CONTRIBUTING.md](CONTRIBUTING.md) for full guidelines.

---

## 📜 License

Licensed under **MIT** — see [LICENSE](LICENSE) for details.

---

<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:2C5364,50:203A43,100:0F2027&height=120&section=footer" width="100%"/>

**Built with ❤️ to stand out in DevOps interviews**

⭐ **Star this repo if it helped you — it keeps me motivated!** ⭐

[![GitHub stars](https://img.shields.io/github/stars/your-username/skillforge?style=social)](https://github.com/your-username/skillforge)
[![GitHub forks](https://img.shields.io/github/forks/your-username/skillforge?style=social)](https://github.com/your-username/skillforge)

</div>
