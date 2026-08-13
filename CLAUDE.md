# Project context for Claude

## What this repo is
A **public portfolio of AI/automation solutions Lara De Rosa has delivered**, built as
personal advertisement — primarily aimed at forward-deployed engineer / solutions
architect / AI engineer roles that look for **end-to-end ownership**: finding the
problem, not just building the ticket.

It is a **case-study portfolio, not a code repo**. Prose + diagrams + sanitized
evidence, with redacted code excerpts where they prove something.

## Standing decisions (do not re-litigate)
- **Clients are anonymized.** No real client names, firm names, people, or
  identifiable case data anywhere in committed files. Use role descriptors
  ("a 40-attorney PI firm in the Southeast"). Specificity comes from detail, not names.
- **Code: illustrative excerpts only.** Redacted snippets of the interesting parts
  (a prompt, a schema, a scoring rule). No client source, no credentials, no PHI/PII.
- **Depth is tiered.** 3 flagship deep dives + 4 short entries. Tier assignment TBD.
- Every case study follows `_template/README.md` section-for-section so a reader can
  compare across projects.
- **Diagnosis is a first-class section**, not an afterthought — how the problem was
  found (audit, process mapping, interviews, data) is the differentiator for
  forward-deployed roles.
- Diagrams are **Mermaid** (renders natively on GitHub, stays diffable).

## The seven solutions
Slugs are **provisional** — rename once each project is understood.

| Slug | Working title | Tier | Status |
|---|---|---|---|
| `marketing-engine` | Marketing Citrine | TBD | Not started |
| `medical-lien-calculator` | Northland lien calculator | TBD | Not started |
| `fnol-intake-agent` | DK Law FNOL agent | TBD | Not started |
| `liability-dispute-agent` | Liability dispute agent | TBD | Not started |
| `medical-provider-agent` | Medical provider agent | TBD | Not started |
| `firm-ops-dashboard` | Dashboard (Bob Simon) | TBD | Not started |
| `document-generation` | Document generation | TBD | Not started |

## Working method (per project, one at a time)
1. Claude states what it already knows. **Claude has no cross-session memory** — the
   only knowledge is this file and the committed case studies. Read them, don't guess.
2. Lara gives a raw description + any documentation.
3. Claude asks the remaining questions needed to write a solid case study.
4. Claude drafts the case study, Lara corrects, commit.

## Progress log
Keep to one line per session. Newest last.
- **2026-08-13** — Repo scaffolded: root README, `_template/`, seven stub folders.
  Decisions above locked. No project content gathered yet.

## Conventions
- Branch: `claude/portfolio-repo-setup-hxm78l`. Commit as work completes.
- Per-project assets in `<slug>/assets/`.
- Never commit a screenshot without checking it for client names, party names, dollar
  figures tied to a real matter, or PHI.
