---
status: Approved
date: 2026-03-24
owner: nic
version: 1.0.0
---

# Share Repo Design

## Goal

Prepare the pm-doc-framework repo for sharing with PM colleagues who have
moderate AI/Claude maturity. The repo serves as a reference — people read it
and copy what they want.

## Audience

PMs who use AI coding agents but haven't thought deeply about structured specs
as agent input. They need the "why" pitched briefly and the "what" laid out
clearly enough to navigate on their own.

## Deliverables

### 1. README.md

Concise (~100-150 lines) README structured as:

- **One-liner** — what this is
- **The problem** — why ad-hoc prompts produce bad results, structured specs fix it
- **What's in the box** — file layout tree with one-line descriptions
- **Key concepts** — EARS notation (pattern table), document taxonomy, ADR/RFC flow, review rules (existence + severity levels, not full list), ID conventions
- **Getting started** — distilled adoption order
- **Workflow cheat sheets** — greenfield / brownfield / bugfix (reuse from CLAUDE.md)
- **License** — MIT

Tone: direct, scannable, no fluff. Assumes reader knows what AI agents are.

### 2. LICENSE

MIT license.

### 3. Branch protection

- Require PR before merging to `main`
- No required approvals (self-merge allowed)
- No required status checks
- Collaborators control who can merge

### 4. Repo visibility

- Flip from private to public

## Out of scope

- GitHub template repo setup
- CI/CD or automated checks
- Contributing guide (premature for reference repo)
- Changelog
