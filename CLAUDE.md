# PM Documentation Framework

## Repo structure

```
specs/_templates/     # Copy a template to create a new doc
specs/_rules/         # Review rules per doc type (check after authoring)
specs/_reference/     # EARS notation, doc taxonomy, cross-doc relationships
specs/constitution.md # Non-negotiable engineering principles (read first, always)
specs/glossary.md     # Shared vocabulary
specs/interfaces/     # One file per component boundary
decisions/adrs/       # Immutable decision records (MADR 4.0)
decisions/rfcs/       # Pre-decision exploration
```

## Before writing code

Read these files in order — skip any that don't exist yet:

1. `specs/constitution.md` — overrides everything
2. `specs/requirements.md` — EARS requirements with FR/NFR IDs
3. `decisions/adrs/` — accepted ADRs constrain tech choices
4. `specs/architecture.md` — system structure, patterns, components
5. `specs/interfaces/` — contracts at boundaries you're touching

## Creating a new document

1. Copy the template from `specs/_templates/{doc-type}-template.md`
2. Fill in YAML frontmatter (status, date, owner, version)
3. Follow the template structure — don't skip sections, mark empty ones TBD with owner
4. Assign unique IDs: FR-NNN, NFR-NNN, ADR-NNN, RFC-NNN, CONST-{CAT}-NN
5. IDs are sequential and never reused

## Reviewing a document

Check against `specs/_rules/{doc-type}-rules.md`. Error-severity rules must be fixed before the document is usable. Warning-severity rules should be fixed.

Cross-document consistency rules are in `specs/_rules/cross-doc-rules.md` — check these when a document references other documents.

## Requirements change governance (REQ-R07)

**No behavioral requirement change without an ADR.** If a change to requirements.md would cause an agent to generate different code, it needs an ADR first. Clarifications, typo fixes, and added failure modes do not.

## EARS quick reference

| Pattern | Keyword | Template |
|---------|---------|----------|
| Ubiquitous | (none) | The \<system\> shall \<response\>. |
| Event-driven | **When** | When \<trigger\>, the \<system\> shall \<response\>. |
| State-driven | **While** | While \<precondition\>, the \<system\> shall \<response\>. |
| Optional | **Where** | Where \<feature\>, the \<system\> shall \<response\>. |
| Unwanted | **If/then** | If \<condition\>, then the \<system\> shall \<response\>. |
| Complex | Combined | While \<pre\>, when \<trigger\>, the \<system\> shall \<response\>. |

Full notation guide with examples: `specs/_reference/ears-notation.md`

## Key references

- Cross-doc relationships and traceability: `specs/_reference/cross-doc-relationships.md`
- When to write an RFC vs ADR: `specs/_reference/greenfield-rfc-vs-adr.md`
- Document taxonomy (all doc types): `specs/_reference/doc-taxonomy.md`
- Agent optimization (what makes docs agent-consumable): `specs/_reference/agent-optimization.md`
