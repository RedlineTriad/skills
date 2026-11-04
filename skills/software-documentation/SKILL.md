---
name: software-documentation
description: Design or improve compact, durable software-project documentation. Use when creating READMEs, CONTRIBUTING guides, architecture docs, intent/principles docs, ADRs, or larger developer-doc sets.
---

# Software Documentation

Create the **smallest useful documentation system**.

## Core rule

Every document needs:
- one audience;
- one job;
- one canonical source of truth.

**Do**
- Optimize for reader decisions and tasks.
- Repeat framing; link mutable facts.
- Prefer examples over claims.
- Mark unknowns instead of inventing intent.
- Keep durable rationale separate from volatile mechanics.

**Don't**
- Create files because a template says so.
- Duplicate config, versions, commands, or API facts.
- Turn implementation accidents into principles.
- Put every audience in the README.
- Write generic advice already enforced by tooling.

## Choose documents

### `README.md`

**Use when:** always.

**Audience:** evaluator + first-time user.

**Contain**
1. What it is.
2. Who it is for.
3. Why it exists.
4. One canonical example.
5. Quick start.
6. Main scope / non-goals.
7. Important caveats.
8. Alternatives: when to choose each.
9. Links deeper.

**Do**
- Make the first screen enough to judge relevance.
- Show a realistic input/output or command quickly.
- Route readers elsewhere.

**Don't**
- Explain the whole architecture.
- Dump the full tech stack.
- Include contributor setup unless users need it.

**Examples**
- uv: https://docs.astral.sh/uv/
- ripgrep: https://github.com/BurntSushi/ripgrep
- Niquests: https://github.com/jawah/niquests

---

### `CONTRIBUTING.md`

**Use when:** outside contributors or multiple developers may change the project.

**Audience:** someone proposing a change.

**Contain**
1. What work is welcome.
2. What needs discussion first.
3. What is out of scope.
4. Dev setup.
5. Test / lint / validation commands.
6. Review expectations.
7. Links to intent + architecture.

**Do**
- Start with contribution policy.
- Explain project-specific review rules.
- Separate:
  - mechanically enforced rules;
  - human-review guidelines;
  - architecture invariants.

**Don't**
- Start with compiler installation.
- Restate formatter rules in prose.
- Say only “PRs welcome”.

**Example**
- uv: https://github.com/astral-sh/uv/blob/main/CONTRIBUTING.md

---

### `docs/INTENT.md` / `PHILOSOPHY.md` / `PRINCIPLES.md`

**Use when:** future contributors could build something technically valid but product-wrong.

**Do not use when:** README goals/non-goals are enough.

**Audience:** maintainers + future design decisions.

**Contain**
- Human problem.
- Primary user / job.
- Goals.
- Non-goals.
- Priority order.
- Product invariants.
- Trust / privacy / failure principles.
- Good and bad example decisions.

**Do**
- Write tradeoffs that settle arguments.
- Prefer: `X > Y when they conflict because ...`
- Document what must remain true across redesigns.

**Don't**
- Write slogans: “simple, scalable, robust”.
- Record current directory structure.
- Use it as a decision diary.

**Examples**
- SQLite “Appropriate Uses”: https://www.sqlite.org/whentouse.html
- TigerStyle: https://tigerstyle.dev/

---

### `docs/ARCHITECTURE.md`

**Use when:** a newcomer cannot answer “where should this change go?”

**Do not use when:** the whole codebase is obvious from a short tree.

**Audience:** codebase newcomers + maintainers.

**Contain**
1. Bird’s-eye view.
2. Inputs / outputs.
3. Main data flow.
4. Coarse code map.
5. Component ownership.
6. Dependency direction.
7. Boundaries + invariants.
8. Important forbidden dependencies.
9. Cross-cutting concerns.
10. Where common changes belong.

**Do**
- Document stable structure.
- Document absences and forbidden coupling.
- Explain *where* and *why*.

**Don't**
- Walk every file.
- Mirror the source tree mechanically.
- Store historical decisions here.

**Examples**
- rust-analyzer: https://rust-analyzer.github.io/book/contributing/architecture.html
- matklad on `ARCHITECTURE.md`: https://matklad.github.io/2021/02/06/ARCHITECTURE.md.html
- C4 diagrams: https://c4model.com/

---

### ADRs: `docs/decisions/NNNN-*.md`

**Use when:** a consequential, non-obvious decision deserves historical rationale.

**Do not use when:** the choice is trivial or obvious from code.

```md
# Decision

Status: accepted

## Context
What forces made this a decision?

## Decision
What did we choose?

## Consequences
What improves? What gets worse?
```

**Do**
- Keep one decision per file.
- Preserve rejected alternatives when useful.

**Don't**
- Rewrite ADRs to match the present.
- Create one for every library choice.

**Example**
- Nygard ADRs: https://www.cognitect.com/blog/2011/11/15/documenting-architecture-decisions

---

## Larger user docs

Use [Diátaxis](https://diataxis.fr/) as a diagnostic model:

- **Tutorial** — teach through a successful first experience.
- **How-to** — achieve a concrete goal.
- **Reference** — precise lookup facts.
- **Explanation** — build understanding.

**Do**
- Organize around reader tasks.
- Cross-link heavily.
- Add categories only as volume requires.

**Don't**
- Force four top-level folders into a tiny project.
- Mix a tutorial with exhaustive reference.
- Lead task-focused readers through architecture theory.

Good corpus: https://docs.djangoproject.com/

## Coding guidelines

Use only for **project-specific judgment**.

Pattern:

```text
Value
→ engineering consequence
→ rule
→ example
→ enforcement
```

Example:

```text
Value: results must be inspectable.
Consequence: ranking must be deterministic.
Rule: no hidden network access inside ranking.
Enforcement: boundary tests.
```

**Do**
- Explain why rules exist.
- Automate mechanical rules.
- State when a strict rule applies.

**Don't**
- Write “use descriptive names”, “follow SOLID”, “write clean code”.
- Universalize context-specific rules.

Examples:
- TigerStyle: https://tigerstyle.dev/
- Effective Go: https://go.dev/doc/effective_go
- Google Go decisions: https://google.github.io/styleguide/go/decisions.html

## Writing style

**Do**
- Use direct language.
- Prefer active voice.
- Use descriptive headings.
- Put examples near claims.
- Recommend a default path.
- Say when an alternative is better.
- Surface caveats where they affect decisions.

**Don't**
- Use marketing filler.
- Say “powerful”, “robust”, “seamless” without evidence.
- Hide limitations in an FAQ.
- Explain internals before value.
- Make readers infer prerequisites.

Style reference:
https://developers.google.com/style

## Information ownership

Before writing, map facts to owners:

```text
project identity        → README
quick start             → README
product goals           → INTENT
product invariants      → INTENT
code map                → ARCHITECTURE
architecture invariants → ARCHITECTURE
test commands           → CONTRIBUTING
testing philosophy      → ARCHITECTURE
historical rationale    → ADR
exact config/API facts  → generated/reference source
```

If two documents own the same mutable fact, fix the design.

## Default setups

### Tiny project

```text
README.md
```

Add `CONTRIBUTING.md` only if others contribute.

### Small serious project

```text
README.md
CONTRIBUTING.md
docs/
  INTENT.md        # only if product invariants matter
  ARCHITECTURE.md  # only if code placement is non-obvious
```

### Growing project

```text
README.md
CONTRIBUTING.md
docs/
  INTENT.md
  ARCHITECTURE.md
  decisions/
  guides/
  reference/
  concepts/
```

Add tutorials/how-to/reference/explanation according to reader need, not symmetry.

## Final check

Ask:

- Can a stranger explain the project after one README screen?
- Can they reach one useful result quickly?
- Can they tell when **not** to use it?
- Does each mutable fact have one owner?
- Can a contributor tell whether their change is welcome?
- Can a newcomer tell where a change belongs?
- Can maintainers identify product and architecture invariants?
- Are claims demonstrated or scoped?
- Are unknowns marked?
- Is any document cheaper to delete than maintain?

If yes to the last question: delete or merge it.
