# Contributing to Lite LLM

Thanks for helping build Lite LLM.

## How to contribute

1. **Pick a target**
   - Spec corrections or clarifications
   - Reference implementation modules
   - Tests for determinism, routing, storage, and dispatch
   - Tooling improvements

2. **Open an issue first (recommended)**
   - Describe the change
   - Identify impacted specs and invariants
   - Include a test plan

3. **Create a pull request**
   - Keep PRs focused and small
   - Include tests when adding behavior
   - Update docs/specs if behavior changes

## Engineering standards

- Determinism is non-negotiable for routing, collectives, and replay paths.
- Unsafe code must be isolated, justified, and reviewed.
- Prefer explicit invariants, measurable bounds, and testable contracts.

## Commit / PR conventions

- Use descriptive titles: `runtime: add stable_topk with seeded tiebreak`
- Reference issues/spec IDs: `SPEC-003`, `SPEC-044`, etc.
- Include benchmarking notes when relevant.

## Code of conduct

By participating, you agree to the Code of Conduct.

