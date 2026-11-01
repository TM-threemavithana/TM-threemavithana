<h1 align="center">Hi, I’m Tharuka Threemavithana 👋</h1>

<p align="center">
  <strong>Computer Engineering Undergraduate @ University of Ruhuna</strong>
</p>

<p align="center">
  Backend & Distributed Systems · Cloud-Native Platform Engineering · AI Security
</p>

<p align="center">
  <a href="https://www.linkedin.com/in/tharuka-madhuwantha/">
    <img
      src="https://img.shields.io/badge/LinkedIn-0077B5?style=flat-square&logo=linkedin&logoColor=white"
      alt="LinkedIn"
    />
  </a>
</p>

## 👨‍💻 About me

I am a Computer Engineering undergraduate focused on building reliable, observable, and secure software systems. My work covers cloud-native platform engineering, high-throughput distributed streaming, backend services, and application security for AI-driven workflows.

- 🔒 **Current Focus**: [AgentIAM](https://github.com/TM-threemavithana/agentiam) (an AST-level SQL firewall proxy for LLM agents) and [ForgeOps](https://github.com/TM-threemavithana/ForgeOps) (a self-hosted platform engineering and observability lab).
- ⚙️ **Core Technical Interests**: Go systems programming, Java (Spring Boot), Kubernetes GitOps, correlated observability (OTel, Alloy, Tempo, Loki, Prometheus), and stream processing with Apache Kafka.
- 🤝 **Collaboration**: Open to backend engineering, platform/SRE, and AI security projects.

---

## 🏛️ Engineering Pillars & Flagship Projects

### 🛠️ Platform Engineering, DevOps & SRE

#### [ForgeOps](https://github.com/TM-threemavithana/ForgeOps) — Self-Hosted Platform Engineering & DevOps Lab
A local cloud-native software delivery platform built on a local Kubernetes cluster (Kind on WSL2 / Linux) modeling production platform patterns without paid cloud dependencies.
- **GitOps Delivery:** Argo CD continuously reconciles Helm chart releases from desired-state Git manifests.
- **Correlated Observability:** Unified three-pillar observability pipeline (OpenTelemetry Java agent $\rightarrow$ Grafana Alloy $\rightarrow$ Tempo traces, Loki logs, Prometheus metrics) with trace-to-log correlation in Grafana.
- **Policy-as-Code & Secrets:** 10 Kyverno policies validate container hardening in CI; Mozilla SOPS + age encrypts Kubernetes secret values in Git manifests while preserving metadata for linting, with decryption keys managed offline by operators rather than cloud KMS.
- **Documented Load & DR Tests:** Local k6 load generation test results (2,275 requests at 0.00% error rate in test environment), five failure-injection experiments, and automated PostgreSQL backup/restore drills with measured recovery times.
- **Core stack:** `Kubernetes (Kind)` · `Argo CD` · `Grafana Alloy/Tempo/Loki` · `Prometheus` · `Kyverno` · `SOPS` · `Helm`
- **Evidence:** [Verification & Rehearsal Evidence](https://github.com/TM-threemavithana/ForgeOps/tree/master/docs/evidence) · [CI Pipeline](https://github.com/TM-threemavithana/ForgeOps/actions/workflows/ci.yml)

#### [Faultline](https://github.com/TM-threemavithana/faultline) — Linux Infrastructure Diagnostics & Incident Reporting CLI
A focused Python CLI utility for diagnosing Linux host infrastructure health and generating structured incident reports.
- **System Diagnostics:** Evaluates disk utilization per mount, sampled CPU, memory/swap, systemd service units (with container fallback), DNS resolution, and TCP socket connectivity with strict timeouts.
- **Structured Reporting:** Generates machine-readable JSON or human-readable terminal reports with severity classification, evidence, and standardized exit codes (0: OK, 1: WARN, 2: CRIT, 3: ERROR).
- **Core stack:** `Python 3.11+` · `Linux / systemd` · `Socket Diagnostics` · `Pytest` · `CLI`
- **Evidence:** [Architecture & Trade-offs](https://github.com/TM-threemavithana/faultline/blob/main/docs/architecture.md) · [CI Pipeline](https://github.com/TM-threemavithana/faultline/actions/workflows/ci.yml)

---

### ⚡ Backend Engineering & Distributed Systems

#### [StreamForge](https://github.com/TM-threemavithana/streamforge) — Distributed Mobility Pipeline & Real-Time Anomaly Engine
A distributed streaming mobility platform engineered to ingest, normalize, and evaluate historical NYC Taxi & Limousine Commission datasets.
- **Polyglot Pipeline:** Vectorized Parquet scanning using PyArrow $\rightarrow$ low-latency Go ingestion gateway $\rightarrow$ Apache Kafka 3.8 KRaft (6 partitions) $\rightarrow$ Go analytics consumer & Java 17 Spring Boot anomaly rules engine.
- **Data Invariants:** Deterministic SHA-256 event hashing, integer-based accounting (zero floating-point drift), and physical database boundary segregation between trip telemetry and alert storage.
- **Documented Benchmark Measurements:** In documented local benchmark runs using a 10,000-event dataset, achieved 9,792.9 events/sec sustained ingestion throughput via pipelined Kafka batching (117.1x speedup over unpipelined baseline), with 36.0 ms p95 ack latency and peak worker memory under 75 MB.
- **Core stack:** `Go 1.24` · `Java 17 (Spring Boot)` · `Apache Kafka (KRaft)` · `PyArrow` · `PostgreSQL` · `React 19`
- **Evidence:** [Benchmark Results & Reproducibility Documentation](https://github.com/TM-threemavithana/streamforge/tree/main/docs/verification) · [CI Pipeline](https://github.com/TM-threemavithana/streamforge/actions/workflows/ci.yml)

#### [TaskFlow](https://github.com/TM-threemavithana/TaskFlow) — Task Management REST API
A task and project management REST API built with Spring Boot 3 and Java 17.
- **Design Patterns in Practice:** Spring Data JPA Specifications (Strategy pattern for composable criteria queries), Adapter pattern for DTO mapping, and Observer pattern via Spring `@EventListener`.
- **Security & Authorization:** Role-based access control, resource ownership verification, and stateless Spring Security 6 authentication with JWTs.
- **Automated Testing:** 92 tests across 11 test classes covering unit tests, Mockito service tests, and real PostgreSQL integration tests orchestrated via Testcontainers.
- **Core stack:** `Java 17` · `Spring Boot 3` · `Spring Data JPA` · `Spring Security 6 (JWT)` · `PostgreSQL` · `Testcontainers`
- **Evidence:** [Integration Test Suite](https://github.com/TM-threemavithana/TaskFlow/tree/main/src/test/java/com/taskflow/integration)

---

### 🛡️ AI Security & Application Security

#### [AgentIAM](https://github.com/TM-threemavithana/agentiam) — AST-Level SQL Firewall Proxy for AI Agents
A PostgreSQL and MySQL wire-protocol proxy in Go designed to inspect and filter database traffic from LLM agents (LangChain / LlamaIndex).
- **Semantic AST Evaluation:** Intercepts raw wire packets and parses SQL into Abstract Syntax Trees using `pg_query_go` and PingCAP TiDB parser to evaluate and block destructive statements (such as prompt-injected `DELETE` queries or unconstrained table scans) according to configured policy.
- **Security Controls:** Injects row-level security (RLS) constraints into queries dynamically, enforces query row caps, and supports mTLS alongside an HMAC-authenticated control plane.
- **Ecosystem:** Ships with Kubernetes Helm deployment manifests and a native Python SDK for LLM agent integration.
- **Core stack:** `Go` · `PostgreSQL Wire Protocol` · `AST Parsing` · `mTLS` · `Kubernetes Helm` · `Python SDK`
- **Evidence:** [Integration Tests](https://github.com/TM-threemavithana/agentiam/tree/main/tests/integration/asyncpg) · [CI Pipeline](https://github.com/TM-threemavithana/agentiam/actions/workflows/ci.yml)

#### [Sentinel Edge](https://github.com/TM-threemavithana/sentinel-edge) — Edge AI & API Security Gateway
A Cloudflare edge AI security gateway combining an operations console with a dedicated request inspection worker.
- **Edge Data Plane:** Hono gateway Worker performing request inspection, SSRF mitigations (validating public HTTPS origins and resolving A/AAAA records via DoH, combined with manual redirect handling and strict upstream routing), PBKDF2 authentication, and tenant-aware rate limits coordinated by Durable Objects.
- **AI Threat Analysis:** Asynchronous threat classification using Workers AI backed by Cloudflare Queues with retry and dead-letter queue policies.
- **Core stack:** `Cloudflare Workers` · `Hono` · `Next.js 16` · `Durable Objects` · `Workers AI` · `D1 & KV`
- **Evidence:** [Live Product Showcase](https://sentinel-edge-console.tharukamaduwantha62.workers.dev/showcase) · [Threat Model](https://github.com/TM-threemavithana/sentinel-edge/blob/main/docs/THREAT_MODEL.md) · [CI Pipeline](https://github.com/TM-threemavithana/sentinel-edge/actions/workflows/ci.yml)

#### [SecXfer](https://github.com/TM-threemavithana/secxfer) — Zero-Trust Encrypted File Transfer
An end-to-end encrypted file-transfer system exploring client-side hybrid encryption with a ciphertext-only central relay.
- **Cryptographic Primitives:** Implements Extended Triple Diffie-Hellman (X3DH) one-time prekeys, XChaCha20-Poly1305 AEAD via libsodium, and optional HMAC-SHA256 pre-shared key (PSK) mixing.
- **Architecture & Integrity:** Local client services handle cryptographic operations while a central Django server transports ciphertext. Includes an explicit threat model and qualified security claims.
- **Core stack:** `Python` · `Django` · `FastAPI` · `Next.js` · `X3DH` · `XChaCha20-Poly1305`
- **Evidence:** [Security Properties & Threat Model](https://github.com/TM-threemavithana/secxfer/blob/master/README.md) · [Automated Tests](https://github.com/TM-threemavithana/secxfer/tree/master/tests)

---

## 🤝 Collaborative & Team Engineering

- **[EventNet Microservices](https://github.com/MadhawaRathnayake/EventNet-micro)**: Contributed to the payment service within a team-managed microservices deployment on Azure Kubernetes Service (AKS), working with Node.js, Express, PostgreSQL, RabbitMQ, and automated container deployment workflows.
- **[Counterfeit Currency Detection](https://github.com/Asitha0012/Counterfeit-Currency-Detection-using-Image-Processing)**: Contributed to a team-developed computer vision pipeline using OpenCV to authenticate Sri Lankan Rupee banknotes by verifying physical and visual security features.

---

## 🛠️ Core Technologies & Tools

| Category | Technologies |
|:---|:---|
| **Languages** | `Go` · `Java (17 / 21 LTS)` · `Python 3.11+` · `TypeScript` · `SQL` · `Bash` |
| **Cloud & Orchestration** | `Kubernetes (Kind / Local; AKS via team project)` · `Docker` · `Helm` · `Argo CD (GitOps)` · `Terraform` · `Cloudflare Workers` |
| **Observability & SRE** | `Grafana Alloy` · `OpenTelemetry` · `Grafana Tempo` · `Grafana Loki` · `Prometheus` · `Alertmanager` |
| **Testing & Reliability** | `Testcontainers` · `Grafana k6` · `Pytest` · `JUnit 5 / Mockito` |
| **Security & Systems** | `Kyverno (Policy-as-Code)` · `Mozilla SOPS + age` · `AST SQL Parsing` · `mTLS` · `X3DH / AEAD` |
| **Databases & Streaming** | `PostgreSQL` · `Apache Kafka (KRaft)` · `Redis` · `MySQL` · `Flyway` |

---

## 📬 Contact & Links

- **LinkedIn**: [linkedin.com/in/tharuka-madhuwantha](https://www.linkedin.com/in/tharuka-madhuwantha/)
- **GitHub**: [github.com/TM-threemavithana](https://github.com/TM-threemavithana)
