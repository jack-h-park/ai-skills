# ai-skills

Reusable AI playbooks and canonical skills for use across multiple repositories.

## What this repo is

This repo holds the shared layer of a 3-layer AI skill system:

```text
jackhpark-ai-skills/              <- this repo (shared layer)
  playbooks/                      <- reusable methods, checklists, failure taxonomies
  skills/
    dev/                          <- engineering skills
    pm/                           <- product / strategy skills
    hybrid/                       <- cross-functional skills

project-repo/                     <- consuming project
  ai/skill-wrappers/<skill>/SKILL.md
                                  <- local binding to the canonical skill
  docs/...-local-adapter.md       <- repo-specific mapping
```

## Layer roles

| Layer | Location | Purpose |
|---|---|---|
| Canonical playbook | `playbooks/` | Generic reusable method with no repo-specific names |
| Canonical skill | `skills/<domain>/<skill>/SKILL.md` | Reusable execution contract with no repo-local paths |
| Local adapter | `project/docs/...-local-adapter.md` | Repo-specific vocabulary, endpoints, invariants |
| Skill wrapper | `project/ai/skill-wrappers/<skill>/SKILL.md` | Local routing layer that binds canonical skill to adapter |

## How to use this in a project

1. Read the canonical playbook in `playbooks/`.
2. Read the canonical skill in `skills/`.
3. Create a repo-local adapter in `docs/<domain>/<skill-name>-local-adapter.md`.
4. Create a repo-local wrapper in `ai/skill-wrappers/<skill-name>/SKILL.md`.

## Canonical playbooks available

| File | Domain | What it covers |
|---|---|---|
| `api-smoke-patterns.md` | dev | Repeatable smoke-test method for API endpoints |
| `retrieval-trace-review.md` | dev | Retrieval trace analysis method |
| `telemetry-contract-audit.md` | dev | Telemetry contract verification method |
| `telemetry-operational-verification.md` | dev | Reusable operational verification checklist for telemetry semantics |
| `admin-surface-hierarchy-audit.md` | dev | Admin UI structural depth audit method |
| `settings-ownership-audit.md` | hybrid | Settings ownership classification and precedence audit |

## Authoring principles

- One playbook = one reusable engineering job.
- One canonical skill = one reusable execution contract.
- Canonical assets must work across repositories with only a local adapter and local wrapper added on top.
- No repo-specific names, paths, events, trace names, or UI primitive names in canonical assets.
- Local adapters supply concrete mappings and remain in the consuming project.
- Local wrappers stay thin and only bind canonical skill to the consuming project.
- A checklist can be promoted if another repo could reuse the sequence with only adapter substitutions.
- Audit results, postmortems, rollout notes, and one-off investigations do not belong in canonical assets.

## What belongs here vs in a project

Belongs here:
- reusable playbooks, checklists, failure taxonomies, output formats
- reusable canonical skills that define routing boundaries and output contracts

Stays in a project:
- local adapters
- local skill wrappers
- repo-specific docs, postmortems, and audit results

## Adding a new canonical asset

1. Identify a repeated engineering job that applies across projects.
2. Write the playbook in `playbooks/` with no repo-specific names.
3. Write the canonical skill in `skills/` with no repo-local paths.
4. Verify another repository could consume both using only a thin wrapper and local adapter.
