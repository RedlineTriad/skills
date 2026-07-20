---
name: software-testing-guide
license: MIT
description: "Select, classify, audit, and implement proportionate software tests and verification. Use for test strategy, test portfolio design, gap analysis, terminology, CI quality gates, and choosing among unit, integration, E2E, property, fuzz, mutation, formal, performance, security, production, and human evaluation."
---

# Software Testing Guide

Treat testing as evidence against concrete risks.

## Method

1. Inspect the change or system, public behavior, boundaries, existing tests, CI, and repository conventions.
2. Identify consequential failure modes and stable observable seams.
3. Choose the smallest credible portfolio: narrow deterministic checks for local behavior, real boundary checks for integration assumptions, and broad journeys for assembly risks.
4. Implement proportionately, reuse existing tools, run relevant checks, and distinguish observed results from recommendations.

Load [references/taxonomy.md](references/taxonomy.md) for broad strategy or terminology. Load [references/selection.md](references/selection.md) for portfolio selection, audits, and implementation planning.

## Classification

Describe verification using the coordinates that add useful information:

`mechanism × scope × target × purpose × technique × oracle × perspective × lifecycle × environment`

Key distinctions:

- unit/component/integration/system/E2E describe scope;
- UI/API/CLI/database/protocol describe targets;
- property/fuzz/snapshot/visual/differential/fault injection describe techniques or oracles;
- security/performance/accessibility/reliability/compatibility describe purposes;
- regression/smoke/acceptance/characterization describe intent;
- black/white/grey box describe perspective;
- static analysis, formal verification, human evaluation, online experiments, production verification, and mutation analysis describe mechanisms.

Preserve understandable repository terminology. Add qualifiers where they clarify evidence, such as `integration/API contract`, `E2E/browser smoke`, or `unit/property`.

Prefer checks with meaningful behavioral sensitivity, independent oracles, controlled nondeterminism, fast diagnosis, and complementary evidence. Use coverage, mutation results, failure history, and production signals to refine the portfolio.

Routine local and hermetic verification can proceed directly. Use a guided plan for production traffic, destructive recovery, expensive shared load, real-user research, penetration or red-team work, certification, and public contract changes.
