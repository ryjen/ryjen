# Engineering work — evidence-led case studies

These examples provide a short entry point for reviewers. Authoritative implementation details, status, and tests remain in each project's own repository. Independent work is identified as such; source and CI evidence does **not** imply commercial adoption, production deployment, customer scale, or independent security certification.

## Platform / backend: Config Drift Guard

**Origin:** independent assessment-oriented project. **Maturity:** evaluator-ready vertical slice, not an operated enterprise control plane.

- **Problem:** configuration changes can diverge from intended state, and blind remediation creates additional operational risk.
- **Design:** canonical and observed inputs flow through validation, deterministic comparison, classification, an immutable remediation plan, explicit operator approval, reconciliation, and post-write verification. Fastify and SQLite hold workflow authority; the Next.js console and SSE provide observation.
- **Failure semantics:** stale observations reject application; malformed input, interrupted workflows, failed writes, and contradictory decisions have documented tests/scenarios.
- **Reproduce:** [README five-minute demo](https://github.com/ryjen/config-drift-guard#five-minute-demo), [operator walkthrough](https://github.com/ryjen/config-drift-guard/blob/main/docs/DEMO.md), [CI](https://github.com/ryjen/config-drift-guard/actions/workflows/ci.yml).
- **Boundary:** adapters currently cover synthetic service configuration and structured documentation, not live Kubernetes or Terraform state.

**Engineering signal:** declarative control planes, consistency and concurrency, durable workflows, tests around failure, and usable operator interfaces.

## Mobile / Kotlin Multiplatform: Eyespie (Wayfinder)

**Origin:** independent mobile application. **Maturity:** backendless closed-alpha implementation with physical release acceptance outstanding.

- **Problem:** share an on-device image-clue game across Android and iOS without requiring a hosted account or surrendering core game authority to a backend.
- **Design:** Kotlin Multiplatform, SQLDelight local-authoritative game/clue/progress state, CameraX/AVFoundation behind bounded capture interfaces, native MediaPipe embedding adapters, platform-backed local P-256 identities, and versioned signed `.eyespie` interchange.
- **Security/quality:** hostile imports are validated before persistence; release candidate identity, pinned model checks, CI, and native handoff runbooks explicitly distinguish automated proof from device acceptance.
- **Reproduce/inspect:** [Wayfinder implementation and build commands](https://github.com/ryjen/eyespie#closed-alpha-implementation-status), [release-readiness evidence and gaps](https://github.com/ryjen/eyespie#release-readiness), [Android runtime verification](https://github.com/ryjen/eyespie/blob/main/docs/development/android-runtime.md).
- **Boundary:** iOS signing, physical Android/iOS inference parity, real-device sharing and cross-device delivery remain candidate-bound validation work. Supabase belongs to a preserved pre-reboot history, not the current app runtime.

**Engineering signal:** mobile architecture across native and shared code, offline authority, serialization/protocol design, privacy, and exact-candidate releases.

## Rust / safety engineering: tidyfs

**Origin:** independent open-source CLI. **Maturity:** working reversible cleanup system; destructive deletion is intentionally unsupported.

- **Problem:** disk-space tools can accidentally destroy important data, especially when automation or model-generated recommendations are treated as commands.
- **Design:** parallel read-only scanning and SQLite aggregation feed deterministic policy, non-overlapping cleanup plans, explicit preview, interactive approval, reversible quarantine, durable execution state, and recovery.
- **Authority:** optional local inference is advisory. It cannot create eligible candidates, lower risk, override protections, determine bytes authoritatively, or directly mutate files; observations are revalidated after inference.
- **Reproduce/inspect:** [CLI commands and current capabilities](https://github.com/ryjen/tidyfs#current-capabilities), [AI architecture](https://github.com/ryjen/tidyfs/blob/main/docs/ai-architecture.md), [threat model](https://github.com/ryjen/tidyfs/blob/main/docs/threat-model.md), [CI](https://github.com/ryjen/tidyfs/actions).
- **Boundary:** no permanent deletion, unrestricted shell execution, or claim of live-model quality scores absent recorded evidence.

**Engineering signal:** Rust systems programming, resource safety, adversarial validation, and robust recovery semantics.

## Go / developer infrastructure: Repora

**Origin:** independent project. **Maturity:** pre-alpha repository-control CLI.

- **Problem:** mirror drift between Git canonical sources and other hosting providers creates risky ad hoc ref repair.
- **Design:** topology and identity validation, observed mirror states, explicit plans, stale-head preflight, reviewed destructive intent, force-with-lease where authorized, and durable per-target results.
- **Failure semantics:** independent mirror operations can have partial outcomes; evidence records intent, before/after states and remaining divergence rather than pretending cross-provider atomicity.
- **Reproduce/inspect:** [current scope and implemented features](https://github.com/hackelia-micrantha/repora#implemented-today), [managed-README example](https://github.com/hackelia-micrantha/repora/tree/main/examples/managed-readme), [CI](https://github.com/hackelia-micrantha/repora/actions).
- **Boundary:** no claim of hosted orchestration, automatic provider provisioning, full ref coverage, or rollback of independently completed remote actions.

**Engineering signal:** Git internals, explicit consistency models, Go CLI architecture, defensive repository mutation, and honest partial failure.

## Professional collaboration: OpenArchive Save for Android

**Origin:** collaborative open-source work associated with professional experience, **not** an independently owned product.

- **Problem area:** privacy-sensitive Android networking and application maintenance.
- **Attributable code:** [internal Tor daemon integration](https://github.com/OpenArchive/Save-app-android/commit/07ce958285e814634b53d63a699de6a7b2d7a059), [Orbot proxy enhancements](https://github.com/OpenArchive/Save-app-android/commit/14e9afda120612244d17b1d62aca64d0b549928a), and [Orbot callback initialization](https://github.com/OpenArchive/Save-app-android/commit/a330ffed779d6fbf95a7c29d3b309a93b1139b75). These commits were verified as ancestors of the upstream `next` branch on October 15, 2026.
- **Evidence:** inspect those commits and the [upstream Android project](https://github.com/OpenArchive/Save-app-android).
- **Boundary:** authored code is not proof that every feature reached users, received production qualification, or alone represents the broader team's work.

**Engineering signal:** collaborative native Android delivery, security-sensitive networking integration and maintainability.

## How to use these examples

For a technical interview, pick the **two most relevant** examples, then discuss the constraint that forced the architecture, the rejected alternative, the most consequential failure mode, and evidence that the protection works. For a resume, project-origin and maturity labels remain mandatory. Do not infer operational outcomes from CI badges, public contracts, simulated trials, or private-core repository descriptions.
