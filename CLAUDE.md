# Project context for Claude

## What this repo is
A **public portfolio of AI/automation solutions Lara De Rosa has delivered**, built as
personal advertisement — aimed at forward-deployed engineer / solutions architect / AI
engineer roles that look for **end-to-end ownership**: finding the problem, not just
building the ticket.

A **case-study portfolio, not a code repo**. Prose + diagrams + sanitized evidence, with
redacted code excerpts where they prove something.

## Standing decisions (do not re-litigate)
- **Clients are anonymized.** No client names, firm names, people, product codenames,
  vendor case-management-system names, or identifiable case data in **any committed file —
  including this one.** Use role descriptors ("a 400-person plaintiff-side PI firm").
  Specificity comes from detail, not names. Third-party tech vendors (Retell, Microsoft,
  Power Platform) are fine to name.
- **This repo is public.** Assume every commit is world-readable immediately. Run the
  identifier scan below before every commit.
- **Code: illustrative excerpts only.** Redacted snippets of the interesting parts (a
  prompt, a schema, a scoring rule). No client source, no credentials, no PHI/PII, no real
  schema prefixes or table names.
- **Depth is tiered.** 3 flagship deep dives + 4 short entries.
- Every case study follows `_template/README.md` section-for-section.
- **Diagnosis is a first-class section** — how the problem was found (audit, process
  mapping, interviews, data) is the differentiator for forward-deployed roles.
- Diagrams are **Mermaid**. Open questions are `<!-- OPEN: ... -->` HTML comments so they
  don't render publicly but stay greppable.

### Pre-commit scan
```bash
grep -rniE "<client names>|<cms vendor>|<employer prefix>" --include="*.md" .
```
Lara knows the actual terms to substitute; do not write them into this file.

## The seven solutions

| Slug | Tier | Status |
|---|---|---|
| `fnol-voice-agent` | **Flagship** | **Drafted** — awaiting Lara on the `OPEN` items |
| `marketing-engine` | TBD | Not started |
| `medical-lien-calculator` | TBD | Not started |
| `liability-dispute-agent` | TBD | Not started |
| `medical-provider-agent` | TBD | Not started |
| `firm-ops-dashboard` | TBD | Not started |
| `document-generation` | TBD | Not started |

Slugs are provisional except `fnol-voice-agent`. Rename once each project is understood
(the original slug `fnol-intake-agent` was wrong — "intake" means client signup in PI, not
claim opening).

## Working method (per project, one at a time)
1. Claude states what it already knows. **Claude has no cross-session memory** — the only
   knowledge is this file and the committed case studies. Read them, don't guess.
2. Lara gives a raw description + documentation.
3. Claude asks the remaining questions needed for a solid case study.
4. Claude drafts, Lara corrects, commit.

Drafting before all answers are in works well: draft what's known, mark gaps as `OPEN`
comments, commit so progress survives the session.

## Reusable findings
- The FNOL client is a **~400-person, ~$50M-revenue** plaintiff-side PI firm; its **claims
  department is ~30 people** (~1,200 hrs/wk capacity — the denominator that makes the
  125–200 hrs/wk finding land). **Four of the
  seven projects (`fnol-voice-agent`, `liability-dispute-agent`, `medical-provider-agent`,
  `document-generation`) plausibly come from the same ~10-solution engagement** at that
  firm — confirm with Lara. If so, the root README should say so: one audit producing ten
  solutions is a stronger story than four unrelated builds.
- Her environment has Fireflies (meeting transcripts — good source for diagnosis
  sections), Gmail, Supabase, Figma connected. GitHub is scoped to this repo only; other
  repos need `add_repo` and may not be authorized.

## Progress log
One line per session, newest last.
- **2026-08-13** — Repo scaffolded (root README, `_template/`, 7 folders). Decisions
  locked: anonymized, illustrative excerpts, tiered depth. `fnol-voice-agent` deep dive
  drafted from three handover docs + Lara's verbal account; before-state economics
  quantified (~250–310 calls/wk, ~125–200 staff-hrs/wk). Open: her role, timeline,
  measured after-state, what was ruled out.

## Conventions
- Branch: `claude/portfolio-repo-setup-hxm78l`. Commit as work completes.
- Per-project assets in `<slug>/assets/`.
- Never commit a screenshot without checking for firm/party names, claim or policy
  numbers, dollar figures tied to a real matter, adjuster names, dates of loss, or PHI.
