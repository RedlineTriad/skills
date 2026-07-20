# Selecting a Proportionate Test Portfolio

## Start from risk

For each important behavior, ask:

1. Which failure matters, and to whom?
2. What are its likelihood, impact, detectability, and recovery cost?
3. At which stable seam is the failure observable?
4. Which economical mechanism and oracle would detect it reliably?
5. Which integration, assembly, environment, or human assumption needs separate evidence?

Build complementary evidence with suitable feedback time, reliability, maintenance cost, and diagnostic value.

## Useful baseline

Many projects benefit from:

- compiler, type, lint, schema, and configuration checks suited to the stack;
- focused unit or component checks for deterministic domain behavior and edge cases;
- integration or contract checks for important boundaries and dependency assumptions;
- a small set of system or E2E checks for critical journeys and assembly risks;
- production observability plus safe rollout and rollback mechanisms.

Adapt the portfolio to the product. Libraries, distributed services, data pipelines, user interfaces, embedded systems, and ML products expose different risks.

## Match techniques to risk

- **Property-based:** algebraic rules, parsers, serializers, transformations, state machines, broad structured domains, and dense edge-case spaces.
- **Fuzzing:** untrusted or complex inputs, parsers, protocols, native code, security boundaries, crashes, hangs, and runtime corruption. Pair with strong runtime detectors.
- **Model-based or stateful:** workflows, protocols, caches, distributed state, and APIs with numerous valid action sequences.
- **Differential or metamorphic:** rewrites, migrations, compilers, numerical code, ML systems, and domains with difficult exact oracles.
- **Mutation:** important deterministic suites where assertion strength and case selection deserve measurement.
- **Snapshot or golden:** stable structured output, generated code, rendering trees, and legacy characterization. Keep review surfaces compact and meaningful.
- **Visual regression:** visual contracts and cross-browser or cross-device rendering. Calibrate tolerances and review intended changes.
- **Performance:** user-visible latency, throughput, resource or cost limits, capacity, and regression risk. Define workload, environment, warmup, variance, and thresholds.
- **Security and privacy:** assets, trust boundaries, attackers, abuse cases, and data flows. Combine static, dynamic, dependency, configuration, and authorized human assessment.
- **Resilience and recovery:** distributed dependencies, retries, failover, backups, queues, and partial failure. Progress from controlled local fault injection to representative environments.
- **Formal methods:** tractable cores, protocols, concurrency, cryptography, safety-critical logic, and high-consequence properties.
- **Human, usability, and accessibility:** comprehension, desirability, workflow, assistive technology, and domain judgment.
- **A/B and online experiments:** causal product questions supported by statistical design and operational safeguards.
- **Canary, shadow, replay, and synthetic monitoring:** deployment, scale, compatibility, and production-specific assumptions, supported by data controls, observability, and rollback.

## New projects

Establish fast static checks and testable seams early. Add representative checks at important boundaries. Encode critical contracts and invariants near their source. Introduce specialized techniques as their corresponding risks appear.

## Existing projects and changes

Use nearby conventions as a starting point. Inspect the change, callers, boundaries, prior incidents, flaky suites, and current gaps. Place regression evidence at the narrowest stable seam, then cover integration and assembly assumptions separately. Characterization tests can preserve legacy behavior while intent is recovered.

## Evidence quality

Favor portfolios with:

- broad behavioral sensitivity and precise failure localization;
- public-interface assertions and realistic boundary checks;
- compact, reviewable snapshots and visual baselines;
- coverage interpreted alongside oracle strength and risk;
- mutation or seeded-fault sampling for critical deterministic suites;
- explicit workload and statistical treatment for performance and experiments;
- production verification backed by isolation, observability, ownership, and rollback;
- active flake ownership, repair, and quarantine policies.

## Naming and reporting

Use repository conventions. Add the dominant scope or mechanism and meaningful qualifier where useful: `unit/property`, `integration/database`, `contract/API`, `system/performance`, `E2E/browser smoke`, `production/synthetic`, `human/usability`, `meta/mutation`.

When completing work, report the risks addressed, checks added or recommended, commands run and observed results, remaining assumptions, and operational boundaries.

Use a guided plan for production traffic, destructive recovery or migration, expensive shared load, real-user research, penetration or red-team work, certification, and organization-wide policy changes.
