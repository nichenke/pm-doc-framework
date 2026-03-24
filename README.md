# PM Documentation Framework

A structured documentation framework for spec-driven development with AI agents.

## The problem

AI coding agents produce better results when given structured, unambiguous
specifications. Without a consistent framework, each project re-invents its own
format, requirements drift without traceability, and agents make assumptions
that diverge from intent. This framework gives you a standard set of planning
and design documents that serve as shared source of truth between humans and AI
agents.

## What's in the box

```
specs/
  _templates/          # Copy a template to start a new doc
  _rules/              # Machine-checkable review rules per doc type
  _reference/          # EARS notation, doc taxonomy, cross-doc relationships
  constitution.md      # Non-negotiable engineering principles
  glossary.md          # Shared vocabulary
  requirements.md      # (per project) What + why
  architecture.md      # (per project) How
  test-strategy.md     # (per project) How we verify
  interfaces/          # One file per component boundary
decisions/
  rfcs/                # Pre-decision exploration
  adrs/                # Immutable decision records (MADR 4.0)
```

## Key concepts

### Document types

| Document | Purpose | When |
|----------|---------|------|
| **Requirements Spec** | What to build and why — outcomes, user journeys, success measures | Before any design work |
| **Architecture Doc** | How to build it — system structure, patterns, technology choices | After requirements stabilize |
| **ADR** | Why a specific choice was made — rationale, alternatives, consequences | At each decision point |
| **RFC** | Pre-decision exploration — weigh options, get feedback | Before an ADR exists |
| **Interface Contract** | API/event/data boundaries between components | During architecture phase |
| **Test Strategy** | How we verify — levels, frameworks, coverage targets | Parallel to architecture |
| **Constitution** | Invariant rules that apply everywhere, always | Day zero, rarely changes |
| **Glossary** | Shared vocabulary and entity relationships | Day one, maintained always |

### EARS requirements notation

Requirements use [EARS](https://alistairmavin.com/ears/) (Easy Approach to Requirements Syntax) patterns:

| Pattern | Keyword | Template |
|---------|---------|----------|
| Ubiquitous | *(none)* | The \<system\> shall \<response\>. |
| Event-driven | **When** | When \<trigger\>, the \<system\> shall \<response\>. |
| State-driven | **While** | While \<precondition\>, the \<system\> shall \<response\>. |
| Optional | **Where** | Where \<feature\>, the \<system\> shall \<response\>. |
| Unwanted | **If/then** | If \<condition\>, then the \<system\> shall \<response\>. |
| Complex | Combined | While \<pre\>, when \<trigger\>, the \<system\> shall \<response\>. |

### Decision records

**RFCs** explore options before committing. Once resolved, each RFC produces one or more **ADRs** — immutable records of what was decided and why. ADRs use [MADR 4.0](https://github.com/adr/madr) format. They're never edited after acceptance; if a decision changes, a new ADR supersedes the old one.

### Review rules

Every doc type has machine-checkable review rules in `specs/_rules/`. Rules are
tagged by severity:

- **Error** — must fix before the doc is usable (e.g., missing frontmatter, missing requirement IDs, behavioral changes without an ADR)
- **Warning** — should fix (e.g., vague adjectives, missing tradeoffs, missing failure modes)

### ID conventions

| Doc type | Pattern | Example |
|----------|---------|---------|
| Functional Requirement | FR-NNN | FR-001 |
| Non-Functional Requirement | NFR-NNN | NFR-001 |
| ADR | ADR-NNN | ADR-001 |
| RFC | RFC-NNN | RFC-001 |
| Constitution Principle | CONST-{CAT}-NN | CONST-CS-01 |

IDs are sequential and never reused. Superseded documents keep their IDs.

## Getting started

1. **Start with Requirements + ADRs** — highest leverage. Requirements tell agents what to build; ADRs prevent them from relitigating decisions.
2. **Add Architecture Doc** once you have enough ADRs to reference.
3. **Add Interface Contracts** when you have multi-component systems.
4. **Add RFCs** when decisions need deliberation before commitment.
5. **Add Test Strategy** to close the verification gap.
6. **Maintain the Glossary** from day one — low effort, prevents the most insidious bugs.

## Workflows

### Greenfield (new project)

1. Write Requirements Spec (problem statement + user journeys + EARS requirements)
2. Write RFCs for foundational technical decisions
3. Resolve each RFC → produce corresponding ADR(s)
4. Write Architecture Doc (synthesize ADRs into coherent design)
5. Write Interface Contracts (one per component boundary)
6. Decompose into tasks → execute

### Brownfield (adding features)

1. Write change specification (delta against existing requirements)
2. Maybe 0-1 RFCs if new technical territory
3. ADRs for any new decisions
4. Update Architecture Doc
5. Decompose into tasks → execute

### Bug fix

1. Identify which requirement (FR-xxx) is violated
2. Read constitution, architecture, and relevant interface contracts
3. Fix the code to match the spec
4. If the spec was wrong, write an ADR first, then update the requirement

## Standards referenced

- [EARS](https://alistairmavin.com/ears/) — Easy Approach to Requirements Syntax (Rolls-Royce, used by AWS Kiro)
- [MADR 4.0](https://github.com/adr/madr) — Markdown Any Decision Records
- [arc42](https://arc42.org) — Architecture documentation template
- [C4 Model](https://c4model.com) — Software architecture visualization

## License

[MIT](LICENSE)
