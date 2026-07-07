# Xzcolp-AGI-Core

**Level 5 Autonomous AGI System | GIQNexusV3 Architecture**

[![Status](https://img.shields.io/badge/Status-Operational-brightgreen?style=flat-square)](system_blueprint.yaml)
[![Mode](https://img.shields.io/badge/Mode-Level%205%20Autonomous-blue?style=flat-square)](docs/operational_modes.md)
[![Architecture](https://img.shields.io/badge/Architecture-GIQNexusV3-orange?style=flat-square)](docs/architecture.md)
[![License](https://img.shields.io/badge/License-MIT-blueviolet?style=flat-square)](LICENSE)

---

## Overview

**Xzcolp-AGI-Core** is a production-grade autonomous AI system designed for Level 5 operational autonomy. The system implements **GIQNexusV3**, a triple-slice logic engine that orchestrates three concurrent processing pipelines:

- **Alpha Slice**: Historical batch processing (0–500ms latency budget)
- **Beta Slice**: Real-time streaming processing (10–100ms latency budget)  
- **Gamma Slice**: Predictive simulation and anomaly detection (100–2000ms latency budget)

All slices operate in parallel under the **Quantum-Sieve** middleware, which provides adaptive load balancing, dynamic thresholds, and probabilistic request acceptance. Security is enforced through the **Proactive Sentinel** layer with pre-commit validation, runtime redaction, and KMS-backed secret management.

---

## Architecture at a Glance

```
┌─────────────────────────────────────────────────────────────┐
│                    Sovereign Interface                      │
│              (REST + gRPC | mTLS + JWT Auth)               │
└────────────────────┬────────────────────────────────────────┘
                     │
┌────────────────────▼────────────────────────────────────────┐
│                  Quantum-Sieve Middleware                   │
│    (Adaptive Routing, QoS Scoring, Probabilistic Accept)    │
└──┬──────────────────────────────┬─────────────────────┬────┘
   │                              │                     │
┌──▼──────┐              ┌────────▼──────┐      ┌──────▼──┐
│  Alpha  │              │     Beta      │      │ Gamma   │
│  Slice  │              │     Slice     │      │  Slice  │
│         │              │               │      │         │
│Batch    │              │Real-time      │      │Predict. │
│0-500ms  │              │10-100ms       │      │100-2000m│
└─────────┘              └───────────────┘      └─────────┘
         │                      │                      │
         └──────────┬───────────┴──────────┬───────────┘
                    │                      │
        ┌───────────▼──────────────────────▼───────┐
        │    XNeo_Memory_Vault (BigQuery)          │
        │  • request_log (audit trail)             │
        │  • vector_store (embeddings)             │
        │  • system_metrics (time-series)          │
        └──────────────────────────────────────────┘
        
        ┌──────────────────────────────────────────┐
        │    Proactive Sentinel Security Layer     │
        │  • Pre-commit SAST validation            │
        │  • Runtime token redaction               │
        │  • KMS envelope encryption               │
        └──────────────────────────────────────────┘
```

---

## Key Features

### 🔄 **Absolute Symmetry**
Every component enforces symmetrical constraints and interfaces, enabling frictionless orchestration without tight coupling.

### ⚡ **Zero-Latency Internal Communication**
gRPC bidirectional streams + async queues ensure sub-100ms request routing across slices.

### 🧠 **Quantum-Sieve Middleware**
- Per-request scoring based on priority, metadata, and system state
- Dynamic acceptance thresholds that adapt to CPU load and queue depth
- Probabilistic filtering with sigmoid decay and temperature tuning
- Starvation prevention (minimum accept rate per slice)

### 🛡️ **Proactive Sentinel**
- Pre-commit static analysis (ruff, bandit, git-secrets, trivy)
- Runtime token/PII redaction before logging
- KMS-wrapped encryption for secrets and JWTs
- Binary authorization for container deployments

### 📊 **Unified Data Architecture**
- **BigQuery** (XNeo_Memory_Vault): Request audit logs, vector embeddings, system metrics
- **Firestore**: Ephemeral in-flight state and session tokens (3600s TTL)
- **Cloud Logging**: Structured, redacted request/error trails
- **Cloud Trace**: Distributed tracing with per-slice latency attribution

### 🚀 **GCP-Native Deployment**
- **Cloud Run**: Serverless, auto-scaling, managed infrastructure
- **VPC Integration**: Private networking, egress control
- **Cloud Monitoring**: Real-time alerting on error budgets, latency SLOs

---

## Directory Structure

```
Xzcolp-AGI-Core/
├── system_blueprint.yaml           # Master configuration (GIQNexusV3, Quantum-Sieve, Sentinel)
├── README.md                        # This file
├── LICENSE                          # MIT License
├── CONTRIBUTING.md                  # Contribution guidelines
│
├── .github/
│   └── workflows/
│       ├── test.yml                 # Unit + integration tests, static analysis, coverage
│       ├── build-and-deploy.yml     # Docker build, image scan, Cloud Run deploy
│       ├── terraform-plan.yml       # Terraform init/plan on PR
│       └── terraform-apply.yml      # Terraform apply on manual approval
│
├── docs/
│   ├── architecture.md              # Detailed GIQNexusV3 design
│   ├── quantum_sieve_spec.md        # Quantum-Sieve algorithm & tuning guide
│   ├── security.md                  # Proactive Sentinel, KMS, secrets
│   ├── operational_modes.md         # Level 5 degradation modes & runbooks
│   ├── api_protocol.md              # Sovereign Interface (REST + gRPC)
│   └── data_schema.md               # BigQuery & Firestore schemas
│
├── terraform/
│   ├── main.tf                      # GCP resources (SA, KMS, Secret Manager, BigQuery)
│   ├── variables.tf                 # Input variables (project_id, region, etc.)
│   ├── outputs.tf                   # Output values
│   └── backend.tf                   # Remote state config (optional: Cloud Storage)
│
├── docker/
│   ├── Dockerfile                   # Multi-stage build for xneo-backend
│   ├── .dockerignore                # Build context exclusions
│   └── entrypoint.sh                # Container startup script
│
├── deployment/
│   └── cloudrun/
│       ├── build_and_push.sh        # Docker build & push to GCR
│       └── deploy.sh                # Cloud Run service deployment
│
├── src/
│   ├── __init__.py
│   ├── api/
│   │   ├── __init__.py
│   │   ├── app.py                   # FastAPI entrypoint
│   │   ├── routes.py                # REST routes (/sovereign/execute, /status, /metrics)
│   │   └── grpc_service.py          # gRPC service handlers
│   │
│   ├── giqnexus/
│   │   ├── __init__.py
│   │   ├── engine.py                # GIQNexusV3 orchestrator (slice coordination)
│   │   ├── alpha.py                 # Alpha slice (batch / historical)
│   │   ├── beta.py                  # Beta slice (real-time streaming)
│   │   ├── gamma.py                 # Gamma slice (predictive simulation)
│   │   └── middleware.py            # Quantum-Sieve implementation
│   │
│   ├── security/
│   │   ├── __init__.py
│   │   ├── sentinel.py              # Proactive Sentinel: redaction, validation
│   │   ├── kms_adapter.py           # KMS client wrapper
│   │   ├── secret_manager.py        # Secret Manager client wrapper
│   │   ├── jwt_handler.py           # JWT signing/verification
│   │   └── validators.py            # Request envelope validation
│   │
│   ├── data/
│   │   ├── __init__.py
│   │   ├── bigquery_client.py       # BigQuery connection & queries
│   │   ├── firestore_client.py      # Firestore ephemeral state
│   │   ├── schemas/
│   │   │   ├── request_log.json     # BigQuery table schema
│   │   │   ├── vector_store.json    # Vector embeddings schema
│   │   │   └── system_metrics.json  # Time-series metrics schema
│   │   └── migrations.py            # Schema versioning
│   │
│   └── config/
│       ├── __init__.py
│       ├── settings.py              # Pydantic BaseSettings (env-based config)
│       └── constants.py             # System constants (thresholds, timeouts)
│
├── tests/
│   ├── __init__.py
│   ├── conftest.py                  # pytest fixtures (mocked GCP clients)
│   ├── unit/
│   │   ├── test_giqnexus_engine.py   # Engine orchestration logic
│   │   ├── test_quantum_sieve.py     # Middleware filtering & scoring
│   │   ├── test_sentinel.py          # Security validation & redaction
│   │   └── test_validators.py        # Envelope contract validation
│   │
│   └── integration/
│       ├── test_api_endpoints.py     # REST + gRPC endpoint tests
│       ├── test_bigquery.py          # BigQuery read/write operations
│       └── test_end_to_end.py        # Full request flow (Alpha → Beta → Gamma)
│
├── requirements.txt                 # Python dependencies
├── pyproject.toml                   # Poetry / build config
├── .pre-commit-config.yaml          # Pre-commit hooks (ruff, bandit, git-secrets)
└── .gitignore                       # Git exclusions
```

---

## Quick Start

### Prerequisites

- **Python 3.11+**
- **Docker** (for containerization)
- **gcloud CLI** (for GCP authentication)
- **terraform** (for infrastructure provisioning)
- **gh** (GitHub CLI, for PR automation)

### Local Setup

```bash
# Clone the repository
git clone https://github.com/Xscript-Fixed-Admin/Xzcolp-AGI-Core.git
cd Xzcolp-AGI-Core

# Install Python dependencies
pip install -r requirements.txt

# Install pre-commit hooks
pre-commit install

# Run tests locally
pytest tests/ -v --cov=src

# Start local dev server (FastAPI)
uvicorn src.api.app:app --reload --host 0.0.0.0 --port 8080
```

### Deployment to GCP

```bash
# 1. Authenticate to GCP
gcloud auth application-default login
export GCP_PROJECT=$(gcloud config get-value project)

# 2. Deploy infrastructure (Terraform)
cd terraform
terraform init
terraform plan -var="project_id=${GCP_PROJECT}"
terraform apply -var="project_id=${GCP_PROJECT}"

# 3. Build and push container image
bash deployment/cloudrun/build_and_push.sh gcr.io/${GCP_PROJECT}/xneo-backend:latest

# 4. Deploy to Cloud Run
bash deployment/cloudrun/deploy.sh gcr.io/${GCP_PROJECT}/xneo-backend:latest
```

---

## Sovereign Interface API

### REST Endpoints

#### `POST /v1/sovereign/execute`
Submit a request to the GIQNexusV3 engine.

**Request:**
```json
{
  "id": "uuid-v4",
  "timestamp": "2026-07-07T10:00:00Z",
  "slice_hint": "beta",
  "metadata": {
    "user_id": "user-123",
    "session_id": "sess-456"
  },
  "vector": [0.1, 0.2, ..., 0.9],
  "vector_dim": 1024,
  "priority": 75
}
```

**Response:**
```json
{
  "status": "ok",
  "result": {
    "alpha_output": {...},
    "beta_output": {...},
    "gamma_output": {...}
  },
  "latency_ms": 87,
  "routed_slice": "beta",
  "8888-SYMMETRY-8888": "kms-signed-verification-token"
}
```

#### `GET /v1/sovereign/status`
Health check and operational metrics.

**Response:**
```json
{
  "operational_mode": "LEVEL_5_AUTONOMOUS",
  "uptime_s": 123456,
  "slices_status": {
    "alpha": { "healthy": true, "queue_depth": 42, "avg_latency_ms": 250 },
    "beta": { "healthy": true, "queue_depth": 123, "avg_latency_ms": 65 },
    "gamma": { "healthy": true, "queue_depth": 8, "avg_latency_ms": 800 }
  },
  "system_metrics": {
    "cpu_load_avg": 0.45,
    "memory_usage_pct": 62,
    "request_rate_per_s": 450
  }
}
```

#### `GET /v1/sovereign/metrics`
Prometheus metrics export (requires authentication).

---

## Security & Compliance

### Secret Management
- All secrets stored in **Google Secret Manager** with automatic 90-day rotation.
- KMS-backed envelope encryption for sensitive payloads.
- Service accounts use least-privilege IAM roles.

### Pre-Deployment Checks
- **Ruff**: Python linting and formatting
- **Bandit**: Static security analysis
- **git-secrets**: Detect hardcoded credentials
- **Trivy**: Container image vulnerability scanning

### Monitoring & Alerting
- **Cloud Logging**: All requests redacted before storage
- **Cloud Trace**: Distributed tracing for latency analysis
- **Cloud Monitoring**: Error budget alerts, SLO tracking, anomaly detection

---

## Contributing

Please see [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on:
- Branch naming conventions
- Commit message format
- PR requirements (tests, security checks)
- Code review process

---

## Operational Runbooks

Detailed runbooks for operational modes, failure scenarios, and degradation are available in:
- [`docs/operational_modes.md`](docs/operational_modes.md) — Level 5 autonomy, failover logic
- [`docs/security.md`](docs/security.md) — Key rotation, secret audits
- [`docs/quantum_sieve_spec.md`](docs/quantum_sieve_spec.md) — Tuning guide for middleware

---

## System Status

| Component | Version | Status | Last Updated |
|-----------|---------|--------|--------------|
| GIQNexusV3 | 3.0.0 | ✅ Operational | 2026-07-07 |
| Quantum-Sieve | 1.1.0 | ✅ Operational | 2026-07-07 |
| Proactive Sentinel | 1.0.0 | ✅ Operational | 2026-07-07 |
| Sovereign Interface | 1.0.0 | ✅ Operational | 2026-07-07 |

---

## License

This project is licensed under the **MIT License**. See [LICENSE](LICENSE) for details.

---

## Support & Contact

For issues, questions, or feature requests:
- **GitHub Issues**: [Create an issue](https://github.com/Xscript-Fixed-Admin/Xzcolp-AGI-Core/issues)
- **Documentation**: See [`docs/`](docs/) directory
- **Security**: Report vulnerabilities via [GitHub Security Advisory](https://github.com/Xscript-Fixed-Admin/Xzcolp-AGI-Core/security/advisories) (responsible disclosure)

---

**Operational Mode**: Level 5 Autonomous | **Architecture**: GIQNexusV3 | **Status**: ✅ Active
