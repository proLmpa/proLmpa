# Hi, I'm proLmpa
## Tech Stack & Proficiency

Proficiency is expressed as **number of distinct projects shipped** using each technology.
*(A "project" = a deployed service or platform that reached production or a working demo stage.)*


### Languages & Runtimes

| Technology | Projects | Notes |
|---|:---:|---|
| **Kotlin** | 1 platform · 6 services | Primary language; Spring Boot 4 on JDK 25 |
| **Java** | — | *(fill in)* |
| **Python / Go / etc.** | — | *(fill in)* |

### Frameworks & Libraries

| Technology | Projects | Notes |
|---|:---:|---|
| **Spring Boot 4** | 1 platform · 6 services | Including pre-release Spring Boot 4 + BOM workarounds |
| **Spring Security** | 1 platform · 5 services | JWT auth, HMAC signing, per-service SecurityFilterChain |
| **Spring Data JPA + QueryDSL 5.1** | 1 platform · 4 services | `ddl-auto: validate`, custom Q-class queries |
| **Resilience4j 2.3** | 1 platform | Circuit breaker (COUNT_BASED), async fire-and-forget |
| **Micrometer + Actuator** | 1 platform · 6 services | Metrics export, health probes |

### Data & Caching

| Technology | Projects | Notes |
|---|:---:|---|
| **PostgreSQL** | 1 platform · 4 isolated DBs | Schema-first, one DB per service |
| **Redis** | 1 platform | Distributed cache; `@Cacheable` / `@CacheEvict` |
| **Caffeine** | 1 platform | L1 in-process cache; two-level caching (Caffeine → Redis → DB) |

### Infrastructure & DevOps

| Technology | Projects | Notes |
|---|:---:|---|
| **Kubernetes (minikube)** | 1 platform · 8 workloads | NodePort exposure, per-service Deployments |
| **Helm** | 1 chart | Multi-service umbrella chart (`helm/baemin/`) |
| **ArgoCD** | 1 platform | GitOps auto-sync on `main`; CI bumps `images.tag` |
| **Docker** | 1 platform | Container images built in CI pipeline |

### Observability

| Technology | Projects | Notes |
|---|:---:|---|
| **ELK Stack** | 1 platform | Elasticsearch + Logstash + Kibana for log aggregation |
| **Micrometer** | 1 platform | Metrics instrumentation across all services |

### Security

| Technology | Projects | Notes |
|---|:---:|---|
| **JWT (jjwt 0.12)** | 1 platform | Stateless auth; `JwtAuthenticationFilter` across all services |
| **HMAC Request Signing** | 1 platform | `X-Bff-Signature` + `X-Bff-Timestamp` for internal BFF→service trust |
| **RBAC** | 1 platform | `CUSTOMER / OWNER / ADMIN` roles; enforced at service layer |


## Business Value I Deliver

### Backend & Platform Engineering

- **Microservice decomposition** — split a monolith into independently deployable services, each owning its own database, with well-defined API boundaries and no shared schema coupling
- **Resilient inter-service communication** — circuit breakers, async fire-and-forget calls, and graceful degradation so a downstream failure never takes down the entire platform
- **Multi-level caching design** — Caffeine (L1) → Redis (L2) → DB reduces read latency and database load for high-frequency endpoints; atomic dual-layer eviction keeps consistency on writes
- **Consistent API contract** — domain-separated DTOs, RFC 7807 `ProblemDetail` error responses, and a zero-path-variable REST convention that keeps clients predictable
- **Schema-safe database management** — `ddl-auto: validate` with manual DDL migrations means schema and code are always in sync; no surprise table drops in production

### Security Engineering

- **Zero-trust internal perimeter** — HMAC-signed headers between gateway and backend services reject any request not originating from the trusted BFF, even inside a private cluster network
- **Stateless JWT auth with RBAC** — token-based authentication eliminates server-side session state; role checks are enforced at the service layer, not just at the gateway
- **Layered Spring Security configuration** — each service gets its own `SecurityFilterChain`, scoped to its access model (public endpoints, internal-only paths, JWT-gated routes) — no one-size-fits-all security policy
- **Least-privilege ownership enforcement** — resource ownership is validated at the service layer on every mutation (`store.userId != currentUser().id`), not delegated to the client

### Cloud / DevOps / SRE

- **GitOps delivery pipeline** — ArgoCD watches the `main` branch; merging a PR is the only deployment action; no manual `kubectl apply` in production
- **Declarative multi-service Helm charts** — all runtime configuration (replica counts, JVM flags, image tags) lives in version-controlled `values.yaml`; environment differences are diffs, not tribal knowledge
- **Observable from day one** — structured logging shipped to ELK, Micrometer metrics, and Actuator health/liveness/readiness probes are built into every service at project inception, not bolted on later
- **Compute isolation without data isolation** — Kubernetes workloads share a cluster; databases remain on dedicated VMs with separate credentials per service, trading network simplicity for data boundary integrity


## Featured Projects

| Project | Stack | What it demonstrates |
|---|---|---|
| **Baemin (food delivery platform)** | Kotlin · Spring Boot 4 · K8s · ArgoCD · ELK | Full microservice platform: 6 services, GitOps deployment, multi-level cache, JWT + HMAC security |
| *(add more)* | | |


## 📬 Contact
[![Email](https://img.shields.io/badge/Email-kheeyeoul%40gmail.com-blue?logo=gmail)](mailto:kheeyeoul@gmail.com)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Profile-blue?logo=linkedin)](https://www.linkedin.com/in/heeyeoul-kim-ab0619264/)
