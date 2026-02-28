# Lite LLM

Lite LLM is a deterministic, tiered-parameter, hierarchical sparse expert (HSER) language model runtime designed to scale from **1B → 1T parameters** and beyond (up to quadrillion-scale parameter universes) while keeping **active compute bounded** per token.

This GitHub organization hosts the **specification corpus**, **reference implementations**, and **operational tooling** for building and deploying Lite LLM as an enterprise / reference-grade system.

---

## What makes Lite LLM different

### Deterministic by design
Lite LLM treats determinism as a first-class requirement:
- Stable top‑k routing with seeded tie‑breaking
- Deterministic collectives and reproducible distributed execution
- Deterministic audit logs and replayable training runs

### Tiered Parameter Architecture (TPA)
Parameters are partitioned across storage tiers:
- **Hot** (HBM / GPU)
- **Warm** (DRAM)
- **Cold** (NVMe)
- **Archive** (Object Store)

Only the TierSet for a request is eligible for routing; everything else has **zero activation probability**.

### Hierarchical Sparse Expert Routing (HSER)
Routing is hierarchical:
**Tier → Group → Expert**
with bounded activation:
`k_tier × k_group × k_expert` experts per token per layer.

This enables extreme parameter scaling while keeping per-token compute predictable.

### Enterprise runtime focus
Lite LLM is not only a model architecture—it is a runtime system:
- Distributed execution protocols
- Storage hierarchy and prefetching
- Secure loading and integrity verification
- Multi-tenant isolation, quotas, and compliance readiness

---

## Repositories (recommended layout)

### Specifications (authoritative)
- `lite-llm-specs` — Enterprise Runtime Engineering Specification Corpus (SPEC‑001…SPEC‑060)
- `lite-llm-schemas` — JSON/YAML schemas for manifests, telemetry, policies
- `lite-llm-rfcs` — Design proposals and evolution process (RFCs)

### Reference implementations
- `lite-llm-runtime` — Rust runtime (routing, caches, dispatch, TierSet engine)
- `lite-llm-train` — Training orchestration, checkpointing, determinism harness
- `lite-llm-kernels` — Device kernels + safe wrappers (CUDA/HIP/Metal/CPU)
- `lite-llm-comm` — Transport abstraction (RDMA / NCCL / QUIC), collectives
- `lite-llm-storage` — Shards, manifests, tier placement, streaming + prefetch

### Tooling
- `lite-llm-cli` — Operator CLI (inspect checkpoints, tier policies, telemetry)
- `lite-llm-observability` — Metrics exporters, dashboards, tracing
- `lite-llm-deploy` — Helm charts, Terraform modules, bare‑metal playbooks

> The organization may not yet contain all repositories listed above; this is the intended long-term structure.

---

## Getting started

### 1) Read the specs
Start with:
- **SPEC‑001** Runtime Architecture Overview
- **SPEC‑003** Deterministic Routing Engine
- **SPEC‑004** Tiered Parameter Architecture (TPA)
- **SPEC‑005** Hierarchical Sparse Expert Routing (HSER)
- **SPEC‑006** Active Compute Bounding Model
- **SPEC‑021…030** Storage hierarchy (hot/warm/cold/archive)
- **SPEC‑041…050** Inference runtime (TierSet selection, dispatch, KV cache)

### 2) Implement the contracts
The specs are written to be directly implementable:
- Deterministic routing + stable sorting
- Tier placement policies and shard formats
- All‑to‑all dispatch and imbalance handling
- Audit logging and integrity verification

### 3) Validate determinism
Before performance optimization:
- Ensure cross-node routing reproducibility
- Validate deterministic collectives
- Use the replay engine during training

---

## Contribution

We welcome contributions in:
- Spec clarifications and testable invariants
- Rust runtime modules (memory model, routing, dispatch, caching)
- Deterministic training harness and replay tooling
- Storage tier orchestration and prefetch algorithms
- Security hardening and audit improvements

Please read:
- `CONTRIBUTING.md` for workflow and standards
- `CODE_OF_CONDUCT.md` for community expectations
- `SECURITY.md` for vulnerability reporting

---

## Security

Lite LLM emphasizes:
- Memory-safe runtime design in Rust
- Secure checkpoint loading and integrity verification
- Encryption at rest for tier storage
- Key management and auditability
- Sandboxing and capability isolation for extensions

See `SECURITY.md` to report vulnerabilities responsibly.

---

## Governance

The specification corpus is the **normative authority**.  
Changes to the corpus should go through the RFC process:
1. Open an RFC in `lite-llm-rfcs`
2. Discuss and iterate
3. Land a spec patch with tests, invariants, and migration notes

---

## License

Each repository specifies its own license. If unspecified, consider it **all rights reserved** until a license is added.

---

## Contact

- Security: see `SECURITY.md`
- General: open an issue in the relevant repository

