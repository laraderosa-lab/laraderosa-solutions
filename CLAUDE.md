# Project context for Claude

## What this repo is
A **public portfolio of AI/automation solutions Lara De Rosa has delivered**, as personal
advertisement. Target readers are hiring managers for forward-deployed engineer / solutions
architect / AI engineer roles, who look for **end-to-end ownership**: finding the problem, not
just building the ticket.

A **case-study portfolio, not a code repo**. Prose, diagrams and sanitized evidence, with
redacted code excerpts where they prove something.

## Standing decisions (do not re-litigate)
- **Clients are anonymized.** No client names, firm names, people, product codenames, vendor
  case-management-system names, or identifiable case data in **any committed file, including
  this one.** Use role descriptors ("a 400-person plaintiff-side PI firm"). Specificity comes
  from detail, not names. Third-party tech vendors (Retell, Microsoft, Power Platform) are
  fine to name.
- **This repo is public.** Assume every commit is world-readable the moment it lands.
- **Code: illustrative excerpts only.** Redacted snippets of the interesting parts (a prompt,
  a schema, a scoring rule). No client source, no credentials, no PHI/PII, no real schema
  prefixes, table names or flow names.
- **Depth is tiered.** 3 flagship deep dives, 4 short entries.
- Every case study follows `_template/README.md` section for section.
- **Diagnosis is a first-class section.** How the problem was found (audit, process mapping,
  interviews, data) is the differentiator for forward-deployed roles.
- Diagrams are **Mermaid**. Open questions are `<!-- OPEN: ... -->` HTML comments, so they
  don't render publicly but stay greppable.
- **No em dashes**, and no AI-slop patterns (colon reveals, "not X but Y" contrasts, asides
  telling the reader what matters). Use the `no-ai-slop` skill, and write this way in the
  first draft rather than fixing it afterwards.

## Per-project workflow
One project at a time. Lara's method:
1. Claude states what it already knows. **Claude has no cross-session memory.** The only
   knowledge is this file and the committed case studies. Read them, don't guess. Say plainly
   when the answer is nothing.
2. Lara gives a raw description. **Ask whether handover, architecture or user docs exist.**
   For `fnol-voice-agent` those docs were by far the highest-value input.
3. Claude asks the questions still needed for a solid case study.
4. Claude drafts, Lara corrects, commit.

Drafting before all answers are in works well: draft what's known, mark gaps as `OPEN`
comments, commit so progress survives the session.

### Definition of done, per project
- [ ] `<slug>/README.md` follows all eight template sections
- [ ] Root `README.md`: the project's row filled in, plus its row in the capability matrix
- [ ] `★` added to the row if it's a flagship
- [ ] Identifier scan passed (below), and every image checked
- [ ] No em dashes; slop pass done
- [ ] `CLAUDE.md` progress log and solutions table updated
- [ ] Committed and pushed

### Pre-commit scan
```bash
grep -rn "—" --include="*.md" .          # em dashes, expect 0
grep -rn "OPEN:" --include="*.md" .      # outstanding questions
```
**The identifier blocklist is deliberately not in this file**, because this file is public.
**Ask Lara for the current list of client names, firm names, people and vendor system names at
the start of any session that will commit prose**, hold it in session only, and grep for it
before committing. Do not run a scan with placeholder terms and treat a clean result as a
pass.

## The seven solutions

Seven total. Six are unwritten.

| Slug | Where the slug came from | Tier | Status |
|---|---|---|---|
| `fnol-voice-agent` | **Accurate.** Project is understood | **Flagship** | Drafted. Refinement continues in its own dedicated session |
| `marketing-engine` | **Guess.** Invented from the single word "marketing" | TBD | Not started |
| `medical-lien-calculator` | **Guess.** Inferred from a two-word shorthand | TBD | Not started |
| `firm-ops-dashboard` | **Guess.** Only that it was a dashboard for a firm | TBD | Not started |
| `liability-dispute-agent` | Lara's own words | TBD | Not started |
| `medical-provider-agent` | Lara's own words | TBD | Not started |
| `document-generation` | Lara's own words | TBD | Not started |

**Do not infer what a project is from its slug.** The three marked *Guess* are placeholders
Claude invented in the first session with no knowledge of the work, and they will read as
established fact if you let them. Ask Lara what each project actually was, then rename the
folder. `fnol-intake-agent` was renamed to `fnol-voice-agent` for exactly this reason, because
"intake" means client signup in personal injury, not claim opening.

Lara refers to these projects by client name, which is not recorded here (public repo). Expect
shorthand that matches no slug, and ask which one she means rather than guessing.

## Reusable findings
- The FNOL client is a **~400-person, ~$50M-revenue** plaintiff-side PI firm; its **claims
  department is ~30 people** (~1,200 hrs/wk capacity, the denominator that makes the
  125–200 hrs/wk finding land). **Four of the seven projects (`fnol-voice-agent`,
  `liability-dispute-agent`, `medical-provider-agent`, `document-generation`) plausibly come
  from the same ~10-solution engagement** at that firm. `medical-provider-agent` is
  **confirmed** by Lara as part of that engagement (2026-08-13); the other two are still
  assumptions. The root README should say so once enough of them are written, because one
  audit producing ten solutions is a stronger story than four unrelated builds, and the
  shared diagnosis stops being repeated four times.
- Her environment has Fireflies (meeting transcripts, a good source for diagnosis sections),
  Gmail, Supabase and Figma connected. GitHub is scoped to this repo only; other repos need
  `add_repo` and may not be authorized. Uploaded files do **not** survive into a new session.

## Progress log
One line per session, newest last.
- **2026-08-13.** Repo scaffolded (root README, `_template/`, 7 folders). Decisions locked:
  anonymized, illustrative excerpts, tiered depth. `fnol-voice-agent` deep dive drafted from
  three handover docs and Lara's verbal account; before-state economics quantified (~250–310
  calls/wk, ~125–200 staff-hrs/wk; the reframe is that the bottleneck was serialization, since
  one person can hold one phone line). Prose passed through `no-ai-slop`. Still open on FNOL:
  Lara's role, timeline, measured after-state, alternatives ruled out, how much to say about
  the CMS API workaround.

## Conventions
- **Branch:** `claude/portfolio-repo-setup-hxm78l`. Commit and push as work completes. If two
  sessions run at once, the second will hit push conflicts, so `git pull --rebase` before
  pushing, or work on a per-project branch.
- Per-project assets in `<slug>/assets/`.
- Never commit a screenshot without checking for firm or party names, claim or policy numbers,
  dollar figures tied to a real matter, adjuster names, dates of loss, or PHI.
