<h1 align="center">Hi 👋, I'm Tharuka Threemavithana</h1>

<p align="center">
  <strong>Computer Engineering Undergraduate @ University of Ruhuna</strong><br>
  Backend Engineering · Security Engineering · Full-Stack Development
</p>

<p align="center">
  <a href="https://www.linkedin.com/in/tharuka-madhuwantha/">LinkedIn</a>
  &nbsp;·&nbsp;
  <a href="mailto:tharukamaduwantha62@gmail.com">Email</a>
  &nbsp;·&nbsp;
  <a href="https://github.com/TM-threemavithana">GitHub</a>
</p>

---

## About

I build backend and security-focused systems, with particular interest in authorization, failure modes, testing, deployment, and operational constraints.

Recent work includes SQL policy enforcement for LLM agents, client-side encrypted file transfer, retrieval systems, multi-tenant applications, and cloud deployment pipelines.

I prefer **evidence over adjectives** — code, tests, architecture, security notes, CI, and reproducible examples.

---

## 🚀 Featured Work

### 🔒 [AgentIAM](https://github.com/TM-threemavithana/agentiam)

A SQL policy-enforcement proxy for controlling what LLM-powered agents are allowed to execute against PostgreSQL and MySQL.

A parameterized query prevents untrusted **values** from becoming executable SQL syntax. It does not prevent an agent from intentionally generating syntactically valid but unauthorized SQL such as:

```sql
DELETE FROM users;
```

AgentIAM parses generated SQL and evaluates its AST against agent-specific rules before execution.

```yaml
allowed_statements:
  - SELECT

allowed_tables:
  - users
  - orders

select_limit: 100
```

#### Where it fits

AgentIAM complements existing database controls rather than replacing them.

**PostgreSQL RLS**  
Controls which rows a database role can access.

**Hasura Permissions**  
Controls row and column access through Hasura's API authorization layer.

**Teleport Database Access**  
Controls authenticated database access using identity, RBAC, short-lived credentials, access requests, and auditing.

**AgentIAM**  
Controls the semantic structure of SQL an autonomous agent attempts to execute after database connectivity has already been granted.

These layers can be used together.

#### Architecture

<p align="center">
  <img
    src="https://raw.githubusercontent.com/TM-threemavithana/agentiam/main/assets/architecture.svg"
    alt="AgentIAM architecture"
    width="760"
  />
</p>

<p align="center">
  <img
    src="https://raw.githubusercontent.com/TM-threemavithana/agentiam/main/assets/client_terminal.png"
    alt="AgentIAM client terminal showing policy enforcement"
    width="48%"
  />
  <img
    src="https://raw.githubusercontent.com/TM-threemavithana/agentiam/main/assets/gateway_logs.png"
    alt="AgentIAM gateway policy logs"
    width="48%"
  />
</p>

The project also documents its own boundaries, including resource-exhaustion risks, view/masking edge cases, protocol/dependency risks, and deployment/topology assumptions.

**Evidence:**  
[Security](https://github.com/TM-threemavithana/agentiam/blob/main/SECURITY.md)
·
[Policy Schema](https://github.com/TM-threemavithana/agentiam/blob/main/policies.schema.json)
·
[Tests](https://github.com/TM-threemavithana/agentiam/tree/main/tests)
·
[Examples](https://github.com/TM-threemavithana/agentiam/tree/main/examples)
·
[CI](https://github.com/TM-threemavithana/agentiam/actions)
·
[Apache-2.0 License](https://github.com/TM-threemavithana/agentiam/blob/main/LICENSE)

`Go` · `PostgreSQL` · `MySQL` · `Docker` · `Kubernetes`

> **Performance:** I don't publish proxy-overhead numbers yet because I haven't published a reproducible benchmark covering workload, concurrency, environment, latency distribution, throughput, and sample size.

---

### 🔐 [SecXfer](https://github.com/TM-threemavithana/secxfer)

A client-side encrypted file-transfer security project exploring how plaintext and private keys can remain outside the central storage/API server.

It uses established cryptographic primitives through PyNaCl/libsodium, including X25519-based key agreement, XChaCha20-Poly1305 authenticated encryption, Ed25519 signatures, and HKDF-SHA256.

The surrounding protocol composition, session-establishment logic, replay handling, key-management workflow, and application integration are project-designed and **have not undergone an independent cryptographic audit or formal verification**.

The optional PSK mechanism is best understood as additional secret-key hardening; I do **not** treat it as independently verified general post-quantum security.

**Evidence:**  
[Source](https://github.com/TM-threemavithana/secxfer/tree/master/src)
·
[Tests](https://github.com/TM-threemavithana/secxfer/tree/master/tests)
·
[Security Policy](https://github.com/TM-threemavithana/secxfer/blob/master/SECURITY.md)
·
[Repository](https://github.com/TM-threemavithana/secxfer)

`Python` · `PyNaCl/libsodium` · `Django` · `FastAPI` · `Next.js`

---

### ☁️ [Smart Inventory](https://github.com/TM-threemavithana/smart-inventory)

An inventory and order-processing system combining a React/TypeScript frontend, Node.js API, Azure SQL, Storage Queues, Python Azure Functions, Container Apps, observability, Infrastructure as Code, and CI/CD.

The backend includes **8 passing Jest tests**, while the deployment repository contains infrastructure definitions and deployment documentation.

**Evidence:**  
[CI/CD](https://github.com/TM-threemavithana/smart-inventory/tree/main/.github/workflows)
·
[Backend](https://github.com/TM-threemavithana/smart-inventory/tree/main/backend)
·
[Infrastructure](https://github.com/TM-threemavithana/smart-inventory/tree/main/infra)
·
[Deployment](https://github.com/TM-threemavithana/smart-inventory/blob/main/DEPLOYMENT.md)

`TypeScript` · `React` · `Node.js` · `Python` · `Azure` · `Docker`

> **Performance:** I don't quote end-to-end latency or throughput until there is a reproducible benchmark defining workload, concurrency, environment, and measurement methodology.

---

## 📂 More Projects

### 🧠 [IntelliDocs](https://github.com/TM-threemavithana/intellidocs)

Retrieval-augmented document question answering with document ingestion, vector retrieval, local LLM execution, PostgreSQL, Redis, MinIO, and Docker.

[Tests](https://github.com/TM-threemavithana/intellidocs/tree/main/tests)
·
[Backend](https://github.com/TM-threemavithana/intellidocs/tree/main/backend)
·
[Docker Compose](https://github.com/TM-threemavithana/intellidocs/blob/main/docker-compose.yml)

---

### 🏢 [Multi-Tenant ATS SaaS](https://github.com/TM-threemavithana/laravel-saas)

Laravel applicant-tracking system with tenant isolation, RBAC, Redis queues, Meilisearch, MinIO, Docker, and GitHub Actions.

Includes a **47-test PHPUnit suite** covering tenant isolation, authentication, background jobs, and storage workflows.

[Tests](https://github.com/TM-threemavithana/laravel-saas/tree/main/tests)
·
[CI](https://github.com/TM-threemavithana/laravel-saas/actions)

---

## 🤝 Selected Contributions

### 🎫 [EventNet Microservices](https://github.com/MadhawaRathnayake/EventNet-micro)

Contributed payment functionality, reservation handling, and Kubernetes configuration.

- [`6293424`](https://github.com/MadhawaRathnayake/EventNet-micro/commit/6293424) — Added payment-service functionality
- [`6ec2baf`](https://github.com/MadhawaRathnayake/EventNet-micro/commit/6ec2baf) — Added UUID support to reservation handling
- [`c53774d`](https://github.com/MadhawaRathnayake/EventNet-micro/commit/c53774d) — Updated payment-service Kubernetes configuration
- [Contribution history](https://github.com/MadhawaRathnayake/EventNet-micro/commits/main/?author=TM-threemavithana)

---

### 🔍 [Sri Lankan Currency Authentication](https://github.com/Asitha0012/Counterfeit-Currency-Detection-using-Image-Processing)

Contributed classical computer-vision work for Sri Lankan banknote analysis.

- [`778e931`](https://github.com/Asitha0012/Counterfeit-Currency-Detection-using-Image-Processing/commit/778e931) — Improved security-thread detection
- [`ff11b2c`](https://github.com/Asitha0012/Counterfeit-Currency-Detection-using-Image-Processing/commit/ff11b2c) — Added automatic background segmentation
- [`bb525bd`](https://github.com/Asitha0012/Counterfeit-Currency-Detection-using-Image-Processing/commit/bb525bd) — Added Sri Lankan banknote-specific support
- [Contribution history](https://github.com/Asitha0012/Counterfeit-Currency-Detection-using-Image-Processing/commits/main/?author=TM-threemavithana)

---

## 🛠️ Technical Toolkit

**Languages**  
`Go` · `TypeScript` · `Python` · `Java` · `PHP` · `JavaScript`

**Backend & Data**  
`Node.js` · `Django` · `FastAPI` · `Laravel` · `PostgreSQL` · `MySQL` · `Redis`

**Infrastructure**  
`Docker` · `Kubernetes` · `GitHub Actions` · `AWS` · `Microsoft Azure`

**Security / Systems**  
`SQL AST Parsing` · `mTLS` · `HMAC-SHA256` · `Authenticated Encryption` · `RBAC` · `Policy Enforcement`

---

## 📫 What I'm Looking For

I'm interested in **internship and graduate engineering opportunities** involving backend engineering, security engineering, application security, cloud infrastructure, or AI/LLM security.

I'm also open to research and open-source collaboration around secure software systems.

<p align="center">
  <a href="https://www.linkedin.com/in/tharuka-madhuwantha/">
    <img
      src="https://img.shields.io/badge/LinkedIn-Connect-0077B5?style=for-the-badge&logo=linkedin&logoColor=white"
      alt="LinkedIn profile"
    />
  </a>
  <a href="mailto:tharukamaduwantha62@gmail.com">
    <img
      src="https://img.shields.io/badge/Email-Contact_Me-D14836?style=for-the-badge&logo=gmail&logoColor=white"
      alt="Email me"
    />
  </a>
</p>

---

<p align="center">
  <sub>Prefer evidence over adjectives.</sub>
</p>
