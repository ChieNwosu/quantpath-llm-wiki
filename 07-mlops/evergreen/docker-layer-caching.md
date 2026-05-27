---
title: Docker Layer Caching
type: evergreen
domain: mlops
status: seed
visibility: PORTFOLIO_SAFE
rag_ready: true
created: 2026-05-27
last_updated: 2026-05-27
tags:
  - mlops
  - docker
  - ci-cd
  - infrastructure
  - reproducibility
  - aws
  - quantpath
aliases:
  - DLC
  - Docker build cache
  - container layer caching
---

# Docker Layer Caching

**Summary**: A build optimization strategy that reuses unchanged intermediate layers from previous Docker builds, dramatically reducing CI/CD pipeline execution time for ML workloads where dependency installation dominates build duration.

**Type**: Evergreen note
**Domain**: MLOps / Infrastructure / CI-CD
**Status**: Seed
**Visibility**: PORTFOLIO_SAFE
**Last updated**: 2026-05-27

---

## Core Concept

Docker images are built as ordered stacks of read-only layers. Each `RUN`, `COPY`, or `ADD` instruction produces a layer. If the instruction and its inputs haven't changed since the last build, Docker reuses the cached layer instead of re-executing the instruction.

For ML workloads, this is transformative:
- Installing `torch`, `tensorflow`, or `transformers` can take 5-15 minutes
- Model dependencies change infrequently compared to application code
- Without caching, every commit triggers a full rebuild
- With caching, only changed layers rebuild — seconds instead of minutes

---

## How Layer Caching Works

```
Dockerfile execution order:
┌────────────────────────────────────────┐
│ FROM python:3.11-slim                  │ ← Base image (rarely changes)
├────────────────────────────────────────┤
│ COPY requirements.txt .                │ ← Cache key: file hash
├────────────────────────────────────────┤
│ RUN pip install -r requirements.txt    │ ← EXPENSIVE: reuses if requirements unchanged
├────────────────────────────────────────┤
│ COPY src/ ./src/                       │ ← Changes frequently (invalidates below)
├────────────────────────────────────────┤
│ RUN python -m pytest tests/            │ ← Rebuilds when src changes
├────────────────────────────────────────┤
│ ENTRYPOINT ["python", "serve.py"]      │ ← Thin layer
└────────────────────────────────────────┘
```

**Cache invalidation rule**: When any layer's cache is invalidated, all subsequent layers must also rebuild. This is why instruction ordering matters enormously.

---

## Why This Matters in Production

1. **CI/CD velocity**: ML pipelines with 10-minute builds become 30-second builds when only code changes.
2. **Developer iteration speed**: Local development cycles tighten from minutes to seconds.
3. **Cost reduction**: Shorter CI/CD runs = fewer compute-minutes billed.
4. **Deployment frequency**: Faster builds enable more frequent, smaller deployments — reducing risk.
5. **Resource efficiency**: Shared base layers across services reduce storage and transfer overhead.

---

## Optimization Strategies

### 1. Multi-Stage Builds
Separate build-time dependencies from runtime:
```dockerfile
# Stage 1: Build
FROM python:3.11 AS builder
COPY requirements.txt .
RUN pip install --user -r requirements.txt

# Stage 2: Runtime (smaller image)
FROM python:3.11-slim
COPY --from=builder /root/.local /root/.local
COPY src/ ./src/
```

### 2. Dependency Layer Isolation
Copy dependency manifests before source code:
```dockerfile
# Good: requirements cached independently of source changes
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .

# Bad: any file change invalidates pip install
COPY . .
RUN pip install -r requirements.txt
```

### 3. BuildKit Cache Mounts
Persist package manager caches across builds:
```dockerfile
RUN --mount=type=cache,target=/root/.cache/pip \
    pip install -r requirements.txt
```

### 4. Pinned Base Images
Use digest-pinned images for deterministic builds:
```dockerfile
FROM python:3.11-slim@sha256:abc123...
```

---

## CI/CD Cache Backends

| Platform | Cache Mechanism | Scope |
|---|---|---|
| GitHub Actions | `docker/build-push-action` with `cache-from`/`cache-to` | Repo-level |
| AWS CodeBuild | Local caching or ECR cache | Project-level |
| GitLab CI | Registry-based caching | Project-level |
| Databricks | Pre-built cluster images | Workspace-level |
| BuildKit | Registry, local, S3, GHA backends | Flexible |

---

## Failure Modes and Risks

| Failure Mode | Impact | Mitigation |
|---|---|---|
| Stale cache poisoning | Old dependencies served despite updates | Hash-based cache keys, not timestamps |
| Layer ordering mistakes | Every build invalidates expensive layers | Lint Dockerfiles, enforce COPY-before-RUN pattern |
| Unbounded cache growth | CI storage exhaustion | TTL policies, cache size limits |
| Platform-specific caches | Works locally, fails in CI | Use registry-backed caching for portability |
| Security vulnerabilities in cached layers | Known CVEs persist | Scheduled full rebuilds, vulnerability scanning |
| Non-deterministic installs | Cache hides version drift | Pin all dependencies, use lock files |

---

## Governance Considerations

- **Supply chain security**: Cached layers may contain outdated packages with known vulnerabilities. Implement periodic full rebuilds.
- **Reproducibility**: Ensure cache keys are deterministic. Avoid relying on external state (network fetches, timestamps).
- **Audit trail**: Tag images with build metadata (commit SHA, pipeline ID, timestamp) for traceability.
- **Base image policy**: Define organizational standards for approved base images and update cadences.
- **Scanning requirements**: All cached layers should pass vulnerability scanning before deployment.

---

## AWS Relevance

- **ECR (Elastic Container Registry)**: Native cache backend for Docker BuildKit
- **CodeBuild**: Supports local caching modes (Docker layer cache, source cache, custom cache)
- **SageMaker**: Pre-built containers for common frameworks; custom containers benefit from DLC
- **ECS/EKS**: Layer caching reduces deployment time for containerized ML services
- **Lambda containers**: 10GB image limit makes layer optimization critical

## Databricks Relevance

- **Custom cluster images**: Pre-baked Docker images for Databricks Runtime reduce cluster startup
- **Init scripts vs. containers**: Containers with cached layers replace slow init scripts
- **MLflow Projects**: Dockerfile-based project definitions benefit from layer caching in CI
- **Unity Catalog containers**: Governed container registries for approved ML environments

---

## ML-Specific Patterns

### Model Weight Caching
```dockerfile
# Cache large model downloads separately from code
COPY model_manifest.json .
RUN python download_models.py  # Only re-downloads if manifest changes

COPY src/ ./src/              # Code changes don't trigger re-download
```

### GPU Layer Separation
```dockerfile
FROM nvidia/cuda:12.1-runtime AS base
# CUDA layer rarely changes

COPY requirements-gpu.txt .
RUN pip install -r requirements-gpu.txt
# Framework layer changes occasionally

COPY src/ ./src/
# Application layer changes frequently
```

---

## Portfolio / Project Integration Opportunities

- **QuantPath containerized pipelines**: Optimize R/Python analysis containers for fast iteration
- **Bedrock RAG deployment**: Container images for embedding services with cached model weights
- **CI/CD for ML**: Docker caching is a prerequisite for fast ML pipeline CI
- **Databricks custom images**: Pre-built containers for specialized QuantPath workloads

---

## Related Notes

- [[ci-cd-for-ml]] — Docker caching as CI/CD acceleration strategy
- [[kubeflow-pipelines]] — containerized pipeline steps benefit from DLC
- [[observability-for-ml-systems]] — container metrics and image provenance
- [[moc-mlops]] — MLOps knowledge map

---

## Sources and Further Reading

- Docker Documentation: Build Cache
- BuildKit: Cache Backends
- AWS: ECR Pull-Through Cache
- Google: Best Practices for Building Containers
