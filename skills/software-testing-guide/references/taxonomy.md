# Software Verification Taxonomy

Testing terms describe different dimensions. Combine the dimensions that clarify the evidence being produced.

## 1. Mechanism: how evidence is produced

- **Static analysis:** evaluates source and other artifacts through inspection and analysis: parsing, formatting, linting, type checking, compiler diagnostics, schema and configuration validation, dependency and license analysis, SAST, data-flow and control-flow analysis, abstract interpretation, and symbolic execution.
- **Formal verification:** proves properties over a model or implementation: theorem proving, proof assistants, model checking, refinement and dependent types, verified compilation, contracts, and deductive verification. Pair proofs with execution against relevant integrations and environments.
- **Dynamic automated testing:** executes software with selected inputs and checks outcomes.
- **Runtime analysis:** observes execution for hidden faults: assertions, sanitizers, race and deadlock detectors, leak detectors, profilers, invariant monitors, tracing, and runtime verification.
- **Human evaluation:** code and test review, exploratory testing, manual acceptance, usability research, accessibility review, alpha and beta testing, dogfooding, and domain-expert judgment.
- **Online experimentation:** compares live alternatives statistically: A/B and multivariate tests, holdouts, interleaving, and bandits.
- **Production verification:** synthetic transactions, canaries, shadow traffic, replay, continuous verification, observability checks, and SLO or error-budget evaluation.
- **Meta-testing:** evaluates the verification system: mutation testing, seeded faults, coverage, flake detection, test-impact analysis, and suite performance or maintainability analysis.

## 2. Scope: how much collaborating software executes

- **Symbol:** one expression, rule, function, method, or type-level property.
- **Unit:** a small cohesive behavior isolated from slow or uncontrolled collaborators.
- **Component:** a deployable or substantial module through its public interface, with dependencies controlled or replaced.
- **Contract:** compatibility at an API, protocol, event, ABI, file-format, schema, or consumer/provider boundary.
- **Integration:** interaction between real implementations, such as code plus database, services, filesystem, queue, browser engine, or external SDK.
- **Subsystem:** a coherent slice containing several integrated components.
- **System:** the assembled product in a representative environment.
- **End-to-end (E2E):** a complete user or business journey across all relevant boundaries from an external entry point to an externally meaningful result.
- **System-of-systems:** behavior across independently operated products or organizations.
- **Production:** verification against a live deployment.

State which dependencies are real, simulated, replaced, or omitted. A browser, API, or database test may occupy any compatible scope.

## 3. Target: what is exercised

Common targets include algorithms, domain rules, modules, libraries and SDKs, processes, services, APIs, protocols, contracts, databases, caches, queues, filesystems, CLIs, browsers, UI components, desktop and mobile apps, operating systems, networks, infrastructure and configuration, deployment pipelines, data pipelines, ML models, LLM and agent systems, embedded firmware, hardware, and third-party dependencies.

Pair target names such as UI, API, CLI, and database with a scope when useful.

## 4. Purpose: which quality or risk is assessed

- **Functional correctness:** examples, rules, state transitions, workflows, error handling, and invariants.
- **Contract and conformance:** schemas, protocols, standards, serialization, migrations, compatibility, and consumer/provider behavior.
- **Security and privacy:** authentication, authorization, isolation, input handling, secrets, dependency risk, abuse cases, cryptography, data minimization, retention, and leakage. Techniques include SAST, DAST, IAST, software-composition analysis, penetration testing, and red teaming.
- **Performance and efficiency:** latency, throughput, resource use, cost, capacity, scalability, load, stress, spike, soak, endurance, volume, and benchmark regression.
- **Reliability, resilience, and recovery:** retries, timeouts, idempotency, degradation, failover, backup and restore, disaster recovery, fault injection, and chaos experiments.
- **Compatibility and portability:** versions, platforms, devices, browsers, locales, networks, upgrades, interoperability, and installation.
- **Usability and accessibility:** task success, comprehension, workflow friction, keyboard and screen-reader behavior, contrast, semantics, and assistive-technology compatibility.
- **Presentation:** visual correctness, layout, rendering, media, and visual regression.
- **Data quality:** completeness, validity, consistency, uniqueness, lineage, drift, reconciliation, and statistical properties.
- **Operability and observability:** deployment, configuration, diagnostics, logs, metrics, traces, alerts, rollback, and support workflows.
- **Maintainability and testability:** modularity, analyzability, change safety, harness quality, and architectural constraints.
- **Safety, compliance, and certification:** hazards, regulatory controls, auditability, and required evidence.
- **AI and ML quality:** predictive quality, calibration, robustness, fairness, drift, hallucination, harmful output, prompt injection, tool use, retrieval quality, and agent task completion.

## 5. Input and stimulation technique

- **Example-based:** selected cases, table-driven or parameterized tests, equivalence partitions, boundary values, decision tables, state transitions, scenarios, use cases, and error guessing.
- **Combinatorial:** pairwise and covering-array selection across interacting factors.
- **Random or generative:** inputs sampled from distributions or generators.
- **Property-based:** invariants checked across generated inputs.
- **Stateful or model-based:** generated command sequences compared with a state model.
- **Fuzzing:** malformed, random, evolutionary, coverage-guided, grammar-aware, protocol-aware, structure-aware, or differential input generation, often paired with runtime detectors.
- **Metamorphic:** relations checked between transformed inputs and outputs.
- **Differential:** implementations, versions, configurations, or old and new systems compared.
- **Fault injection and chaos:** dependencies, resources, clocks, networks, hosts, or processes perturbed.
- **Replay and mirroring:** captured traffic replayed or copied to another implementation.
- **Search-based:** inputs optimized toward failures, states, or coverage.
- **Exploratory:** a human adapts investigation from observations.

## 6. Oracle: how success is judged

Oracles include exact values or states, predicates and invariants, reference models, differential comparisons, metamorphic relations, schemas and contracts, snapshots and golden masters, visual diffs, approval review, statistical thresholds and confidence intervals, runtime assertions and sanitizers, human judgment, and production signals or SLOs.

Snapshots provide a stored-output oracle. Visual regression combines a visual target with an image-based oracle. Traffic mirroring gains equivalence evidence through differential, invariant, or statistical oracles.

## 7. Perspective

- **Black-box:** derives checks from observable specifications.
- **White-box:** uses implementation structure, paths, state, or instrumentation.
- **Grey-box:** combines public behavior with partial internal knowledge.

Each perspective can apply at any scope.

## 8. Intent, lifecycle, and environment

**Intent:** regression, characterization or golden-master, smoke, sanity, acceptance, conformance, certification, release qualification, diagnosis, and monitoring.

**Lifecycle:** editor or pre-commit, pull-request CI, merge, scheduled or nightly, pre-release, deployment, post-deploy, continuous production, alpha, beta, and dogfood.

**Environment:** in-process, hermetic, simulated, emulated, virtualized, containerized, local real dependencies, shared integration, staging, hardware-in-loop, production-like, and production. Record relevant datasets, versions, topology, and dependency substitutions.

## Common term relationships

- Regression describes intent and can occur at every scope.
- Acceptance identifies stakeholder criteria and may use automation or human evaluation.
- Smoke and sanity describe breadth and intent.
- Property testing and fuzzing share input generation while differing in generator structure, exploration strategy, and oracle style.
- Mutation testing measures suite sensitivity by changing the program.
- Linting belongs to static analysis; formatting is a deterministic source transformation or check.
- User testing evaluates representative users; human testing also includes expert review and exploratory work.
- Performance, security, accessibility, reliability, and compatibility apply across scopes and mechanisms.
