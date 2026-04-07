# Lite LLM Rust Skeleton (Specs 1-6)

This repository contains six independent Rust crate skeletons aligned to the first six implementation tracks from `lite-llm-spec`:

1. Core Runtime Architecture
2. Distributed Systems Layer
3. Storage and Memory Hierarchy
4. Training Runtime
5. Inference Runtime
6. Security and Enterprise Controls

The root directory is not a Rust project. Each crate under `crates/` is standalone and can be built independently.

## Repository Layout

```text
lite-llm/
  .gitignore
  LICENSE
  README.md
  crates/
    lite-llm-core-runtime/
    lite-llm-distributed/
    lite-llm-storage/
    lite-llm-training/
    lite-llm-inference/
    lite-llm-security/
  lite-llm-spec/
```

## Crate Map

### 1) `lite-llm-core-runtime`
Specification scope: core runtime architecture and deterministic execution contracts.

Includes skeletons for:
- Runtime configuration types (`TierId`, `TierSet`, routing limits)
- Runtime lifecycle (`boot`, `model load`, `TierSet activation`, `shutdown`)
- Deterministic router trait and baseline implementation scaffold
- Runtime state machine and transition checks

### 2) `lite-llm-distributed`
Specification scope: distributed execution, parallelism, transport, deterministic collectives.

Includes skeletons for:
- Parallelism dimensions (`dp`, `tp`, `pp`, `ep`)
- Communication traits for collectives and all-to-all
- Transport abstraction (`RDMA`, `NCCL`, `QUIC` placeholders)
- Fault handling and recovery policy shape

### 3) `lite-llm-storage`
Specification scope: hot/warm/cold/archive placement, lazy loading, checkpointing.

Includes skeletons for:
- Tier placement policy enums and interfaces
- Hot cache APIs and eviction hook points
- Checkpoint manifest and shard metadata models
- Snapshot and restore entry points

### 4) `lite-llm-training`
Specification scope: curriculum tier expansion, load balancing, deterministic replay.

Includes skeletons for:
- Tier expansion phase machine
- Load-balancing loss config and calculation interface
- Training replay metadata model and validation hooks
- Training engine entry trait

### 5) `lite-llm-inference`
Specification scope: TierSet selection, token routing pipeline, telemetry.

Includes skeletons for:
- TierSet selection policy (`fast`, `balanced`, `deep`, `max`)
- Inference pipeline stages and execution contract
- Telemetry event types and collector interface
- Budget-aware selection context

### 6) `lite-llm-security`
Specification scope: memory safety policy mapping, integrity, access control, auditability.

Includes skeletons for:
- Artifact integrity verification contract
- Access control and tier authorization model
- Deterministic audit log event model
- Key management and policy placeholders

## Build and Check

Run commands from each crate directory.

### Example

```bash
cd crates/lite-llm-core-runtime
cargo check
```

Repeat for:
- `crates/lite-llm-distributed`
- `crates/lite-llm-storage`
- `crates/lite-llm-training`
- `crates/lite-llm-inference`
- `crates/lite-llm-security`

## Design Notes

- This is a skeleton, not a runtime implementation.
- Public APIs are intentionally small and explicit so behavior can be filled in from the spec in controlled increments.
- Crates are intentionally independent to allow separate iteration and packaging.

## Suggested Next Implementation Order

1. Finalize deterministic route selection in `core-runtime`.
2. Implement deterministic all-to-all protocol in `distributed`.
3. Add concrete cache and lazy loading behavior in `storage`.
4. Implement curriculum scheduler and replay metadata persistence in `training`.
5. Wire an end-to-end inference request through `inference` pipeline stages.
6. Enforce authz and audit hooks at crate boundaries via `security`.

## Source Specifications

Primary spec corpus is in:
- `lite-llm-spec/`

The code skeleton is intended to align with:
- `lite-llm-spec/README.md`
- `lite-llm-spec/001-runtime-architecture.md` through `060-threat-model-and-security-hardening-guide.md`

## License

The root `LICENSE` file is copied from:
- `lite-llm-spec/LICENSE`
