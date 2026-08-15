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

> **Not yet done.** As of 2026-08-13 the blocklist has been requested twice and never supplied,
> so **neither written case study has been scanned against Lara's real list.** What was run
> instead: a scan for identifiers lifted from the handover documents themselves (the CMS vendor
> product, the client firm name embedded in the batch-ID convention, the internal repo name, the
> Dataverse column prefix, the security group names, the flow-name convention, the raw
> option-set integers). All clean. That is stronger than placeholders and still not the
> authoritative check. **Get the list and re-scan both case studies before treating the repo as
> publication-ready.**

## The seven solutions

Seven total. Five are unwritten.

| Slug | Where the slug came from | Tier | Status |
|---|---|---|---|
| `fnol-voice-agent` | **Accurate.** Project is understood | **Flagship** | Drafted, iteration 1 done. One `OPEN` left (measured after-state) |
| `marketing-attribution` | **Accurate.** Renamed from `marketing-engine` once the work was understood | **Flagship** | Drafted. OPEN on the Skyvia/Power BI layer, timeline, and every after-state number |
| `medical-lien-calculator` | **Guess.** Inferred from a two-word shorthand | TBD | Not started |
| `firm-ops-dashboard` | **Close enough.** Confirmed as the dashboard project, though it covers intake/marketing and finance too, so consider a rename | Short | Drafted, gaps open |
| `liability-dispute-agent` | Lara's own words | TBD | Not started |
| `medical-provider-selection` | **Accurate.** Renamed from `medical-provider-agent` 2026-08-13, because the work is provider *selection* (search, ranking, booking), and the internal app path says so too | **Flagship** | **Materially complete.** All eight sections written, before-state quantified, role and outcome filled in. Outstanding: timeline, status/in-production-since, handover-doc authorship, one technical "what I'd rebuild", and the identifier scan against Lara's real blocklist |
| `document-generation` | Lara's own words. **Accurate**, but it is a *method*, not one build | TBD, leaning flagship | Drafted. Awaiting impact numbers, role detail, video clearance |

**Do not infer what a project is from its slug.** The two still marked *Guess* are placeholders
Claude invented in the first session with no knowledge of the work, and they will read as
established fact if you let them. Ask Lara what each project actually was, then rename the
folder. `fnol-intake-agent` became `fnol-voice-agent` and `marketing-engine` became
`marketing-attribution` for exactly this reason: "intake" means client signup in personal
injury rather than claim opening, and the marketing work produces no marketing, it measures it.

`firm-ops-dashboard` is **confirmed by Lara as a different client** from the Power BI dashboard
inside `marketing-attribution`. Two dashboards, two engagements. Do not merge them.

Lara refers to these projects by client name, which is not recorded here (public repo). Expect
shorthand that matches no slug, and ask which one she means rather than guessing.

## Reusable findings
- The FNOL client is a **~400-person, ~$50M-revenue** plaintiff-side PI firm; its **claims
  department is ~30 people** (~1,200 hrs/wk capacity, the denominator that makes the
  125–200 hrs/wk finding land). **Four of the seven projects (`fnol-voice-agent`,
  `liability-dispute-agent`, `medical-provider-agent`, `document-generation`) plausibly come
  from the same ~10-solution engagement** at that firm. `medical-provider-selection` is
  **confirmed** by Lara as part of that engagement (2026-08-13); the other two are still
  assumptions. The root README now states this for the two written projects.
- **The engagement covered two departments**: the **claims department** (~30 people, FNOL) and
  the **treaters / treatment team** (**~65 people, ~2,600 hrs/wk capacity**), who track a
  client's post-accident care and book the appointments doctors recommend. Ask which department
  a new project belongs to, since the before-state economics differ per department.
- **The firm's intake is ~100–125 new cases/wk** (measured for claims). Both written case
  studies scale their weekly arithmetic off it, treaters on the stated assumption that the same
  cases flow through. **Per-case volumes for treaters** (Lara's conservative estimates,
  2026-08-13): ~6 provider selections, ~2 availability calls per selection at ~10 min, ~30
  booking emails, and ~15 min of directory searching per selection. That yields ~600–750
  selections/wk at ~35 min each: ~150–190 hrs/wk searching plus ~200–250 hrs/wk on calls,
  **~350–440 hrs/wk combined, 13–17% of the 2,600-hr capacity**, and ~3,000–3,750 booking
  emails/wk. All of these are Lara's conservative estimates, not stopwatch figures, and the case
  study says so.
- **Watch the unit when Lara quotes per-case figures.** She sometimes says "per case" meaning
  "per provider selection", which made the calls figure ambiguous for two rounds. The units
  above were explicitly confirmed on 2026-08-13 and should not be re-derived. When a new
  project needs volume arithmetic, ask which unit each number is in before computing.
- **Shared platform conventions across the engagement's solutions**: Dataverse as the data
  layer, Power Automate flows for orchestration, Retell for voice, Copilot Studio agents for
  notification and composition, access by Entra group membership, and **one shared 8-value
  run-status choice set** reused by every solution. Two solutions also share a batch-ID +
  one-row-per-call pattern with a fan-in completion gate. Name the pattern once and
  cross-reference it rather than re-explaining it per case study.
- **The case management system is a named commercial product and must never be committed.** The
  handover docs name it constantly. Same for the client firm name, the real Dataverse column
  prefix, the real flow-name convention, the internal repo name, Entra group names and the raw
  option-set integers. None of those appear in this file either, deliberately. Redact by
  substitution, the way the two drafted case studies do: descriptive table names, flows
  described by function, and "the case management system" for the vendor product.
- The `marketing-attribution` client is a **different, much smaller firm**: single office, US,
  criminal defense (the larger book) plus personal injury (the growth bet), roughly six people
  known by role. It runs **Lawmatics** for intake and **Clio Manage** for case management, and
  Lara has confirmed both may be named. Do not conflate it with the FNOL firm.
- **Naming Clio needs a ruling.** The standing decision bans "vendor case-management-system
  names", but Lara named Clio Manage and Clio Grow throughout the dashboard session and named
  the branch after it. The draft names Clio. Either narrow the rule to the FNOL client's CMS,
  or scrub Clio from `firm-ops-dashboard` and call it "the firm's case management system".
- **Raw source material from Lara arrives unredacted, including material she describes as
  already modified.** The dashboard-session transcripts named a real referral-partner firm, a
  first name, a referral marketplace and a city. Sanitize on the way in, quote only after
  redacting, and never copy an identifier into this file while checking it.
- **"Pre-anonymized" client exports still need a full check.** The five dashboard PDFs Lara
  supplied as already-modified still carried client emails and phone numbers, legible client
  names under partial blur, a staff name in a slicer, and referral-partner lists that read as
  real firms. Blur in an export is not redaction. Substitute at source or crop to aggregates.
- **`document-generation` is not a project, it is the house method** for any solution that has
  to emit a document, used across a big chunk of them. Confirmed 2026-08-14: the five-level
  framework (boilerplate → merge fields → conditional logic → AI classification → AI narrative)
  was **co-developed by Lara in a group session and written up by someone else**, so do not
  claim sole authorship. Applied at **~a dozen** US plaintiff-side PI firms practice-wide,
  **four by Lara directly**, several documents each. Design rule: lowest level that will do the
  job. Level 4 classifies only, and the prose it selects was written by a human. Template
  assessment is still **manual**.
- All document work is **US plaintiff-side PI firms**. The walkthrough video Lara uses is an
  **Ontario** statement of claim, so any reference to it must say the sample is Ontario while
  the clients were US.
- Her environment has Fireflies (meeting transcripts, a good source for diagnosis sections),
  Gmail, Supabase and Figma connected. GitHub is scoped to this repo only; other repos need
  `add_repo` and may not be authorized. Uploaded files do **not** survive into a new session.
- **Google Docs cannot be read in this environment.** `docs.google.com` is blocked by the
  network egress proxy, and the Google Drive connector exposes only `share_file`, `trash_file`
  and `update_file`, with no content fetch. Ask Lara to paste or upload doc contents instead of
  sharing a link, and do not burn a turn discovering this again.

## Progress log
One line per session, newest last.
- **2026-08-13.** Repo scaffolded (root README, `_template/`, 7 folders). Decisions locked:
  anonymized, illustrative excerpts, tiered depth. `fnol-voice-agent` deep dive drafted from
  three handover docs and Lara's verbal account; before-state economics quantified (~250–310
  calls/wk, ~125–200 staff-hrs/wk; the reframe is that the bottleneck was serialization, since
  one person can hold one phone line). Prose passed through `no-ai-slop`. Still open on FNOL:
  Lara's role, timeline, measured after-state, alternatives ruled out, how much to say about
  the CMS API workaround.
- **2026-08-13 (second session).** `medical-provider-agent` renamed to
  `medical-provider-selection` and drafted as the second flagship, from three handover docs
  (user guide, maintenance runbook, architecture) plus Lara's verbal account. Confirmed it is
  the **treaters** department, same engagement as FNOL. Diagnosis method was **shadowing**,
  which contrasts usefully with FNOL's interview ladder. Strongest findings: the ~18k-provider
  directory had no coordinates so staff copy-pasted addresses into Google Maps per candidate;
  the "do not use" checkbox existed but ticking it had no consequence, so nobody ticked it, and
  the fix was to make the existing field consequential rather than add a new one. Root README
  now states that the first two case studies come from one engagement. Still open: the
  treatment team's size and appointment volume (the missing denominator, the equivalent of
  FNOL's 125-200 hrs/wk), how long one selection took, Lara's role, timeline, status, measured
  after-state, what was ruled out.
- **2026-08-13 (second session).** `firm-ops-dashboard` drafted from Lara's verbal account plus
  five dashboard PDF exports. Clio Manage/Grow to Skyvia to Azure SQL to Power BI, hourly at
  both hops, five reports on one semantic model, team goals fed from a management spreadsheet.
  Open on this one: Lara's timeline, her own "what I'd do differently", and who framed the
  data-before-AI argument. **Screenshots deliberately not committed**, see below.
- **2026-08-13 (third session).** Created `main` and made it the repo default, because the
  default had been a session-scoped feature branch, so pushed work never showed on the landing
  page (Lara reported seeing nothing pushed; the commits were fine, the default branch was
  wrong). Repo-settings writes are blocked by the sandbox proxy, so Lara flipped the default
  herself. Quantified the treaters' before-state from Lara's estimates: **~200–250 staff-hrs/wk
  on availability calls against a ~2,600 hr capacity**, which gives provider selection the
  fundable-arithmetic paragraph FNOL already had. Still open on provider selection: Lara's
  role, timeline, status, measured after-state, what was ruled out, minutes per provider
  search, and whether the do-not-use flag is now actually maintained (the real test of that
  design choice).
- **2026-08-13 (third session, later).** Provider selection is now materially complete. Filled
  in: **Lara's role** (sole engineer, ideation through build; **change management was the
  client's by agreement**), **~15 min per provider search** (giving the ~350–440 hrs/wk
  headline), and **the do-not-use flag is now maintained**, trained on, and the single source of
  truth, which is the payoff of the "make the existing field consequential" decision and the
  only reportable after-state. **Nothing else was measured after rollout**, so §7 says so
  plainly instead of estimating; §8 gained the honest reflection that instrumentation should
  have gone in the build rather than the handover. Alternatives-ruled-out stays thin at Lara's
  direction. **Still open on this project: timeline, status/in-production-since, whether Lara
  wrote the three handover docs, and one technical "what I'd rebuild".**
- **2026-08-14.** `marketing-engine` renamed to `marketing-attribution` and drafted as the
  second flagship, from a 90-minute client-handover transcript (the walkthrough Google Doc was
  unreadable, see above). Different, much smaller client than FNOL. The story is a project Lara
  pitched unasked for months: ~1,000 junk marketing sources, a whole capture channel arriving
  with no attribution because the agency set no UTM parameters, PI revenue never reaching the
  reporting system, and conversion rates inflated by dropped cases that stayed marked hired.
  The strongest beat is non-technical, forcing a hostile vendor onto one-landing-page-per-ad-
  group by escalating to the firm's owner. Lawmatics and Clio Manage cleared for naming. Still
  open: the Skyvia-to-Power BI layer (Lara built a custom Lawmatics connector, vibe coded, and
  the transcript predates it), the timeline, Lara's role split, and every after-state number.
  The client walkthrough doc arrived later as a PDF and confirmed the workstream structure,
  added the accounting-system and referral-fee cost mapping, and showed that each workstream was
  designed in Figma and walked through with the client before being built. It does not mention
  Skyvia either. Extract PDFs with `pip install pypdf` then repair the broken backend with
  `pip install --force-reinstall cffi cryptography`; `pdftotext` and `pdftoppm` are unavailable
  and poppler-utils will not install. The reporting layer was then filled in from the connector
  definition and replication config Lara pasted: custom REST connector against the Lawmatics
  API, replicated into BigQuery, read by Power BI. Blocklist confirmed as **any names of people
  or clients**. Branch moved off the client-named one it was handed.

- **2026-08-14.** `firm-ops-dashboard` corrected and filled out from Lara's answers plus three
  client-call transcript excerpts. Key corrections: **the dashboard client is a different firm
  from the FNOL client** (~$50M revenue, under 400 people), **Lara did not diagnose this one**
  (pilot engagement, the client arrived with the pain point stated), and the strongest idea in
  the project, ranking referral partners by hired rather than by volume, **was the client's,
  asked for live in the pilot review**. Section 2 rewritten to say so. Impact section now
  carries redacted client quotes instead of invented metrics. Sequencing recorded: Clio Grow
  intake shipped alone as the pilot, Clio Manage reports followed.
- **2026-08-15.** FNOL iteration 1, on branch `claude/fnol-solution-iteration-b1buz6`. Filled
  in role (co-diagnosed, co-decided; built the Retell agent, Power App, Power Automate flows
  and Copilot agent), timeline (**6 weeks, first conversation to rollout, alongside the other
  nine solutions**, which confirms the one-audit-ten-solutions story) and status (completed).
  Added the **auto-retry (3 attempts when no human is reached) and one-click retry from the
  app**, which had been missed. Rewrote §8 in Lara's words (re-benchmark voice platforms;
  pursue direct carrier API integrations for the highest-volume carriers, done elsewhere, out
  of scope here). Dropped the invented "what I ruled out" subsection and the invented §8.
  Reframed accuracy evaluation as **detection on top of prevention** (<3% misstatement) with
  the trust argument: staff would otherwise read every transcript, so surfacing our own errors
  loudly is what makes silence informative. **Lesson: do not invent a section and present it
  as fact.** §8 and the ruled-out list were both Claude's inventions and both had to go.
  Iteration 1b: **do not mention the CMS API at all**, assume it has one (that constraint
  bullet is deleted, and the `OPEN` with it). Four real trade-offs added to §5, all Lara's:
  one adaptable agent vs. a scripted agent per carrier (cheaper and more predictable, but
  covers only the carriers you build for and breaks when they change their IVR or questions);
  no direct carrier API integrations, ruled out by the six-week timeline, which is also the
  §8 item; **two-tier severity restored** with the correct framing (both tiers are reported
  and visible, only essential raises an *urgent* alert, examples: essential = date of loss,
  client name, passenger count; minor = airbag deployment, weather); and **carriers can only
  be added in the CMS, never in the app**, to stop the source of truth fragmenting.
- **2026-08-14.** `document-generation` drafted on branch
  `claude/document-generation-automation-67eozm`, framed as a **method entry** rather than a
  single build, since Lara confirmed it is the approach used inside other solutions. Root
  README row and capability matrix filled. Content came from Lara's verbal account in one
  session: the five levels, the three deployment shapes (in-CMS with Word field formulas /
  hybrid export to a flow / flow-only), and the two Level 5 wiring patterns (node per section
  vs prompts bracketed inside the template). Still open: measured impact (none quoted yet, the
  weakest part of the entry), Lara's per-client role split, flagship or not, whether the
  walkthrough video link is public and its sample document clean, and confirmation that the
  node-vs-in-template tradeoff is written the right way round. Lara will build the demand-letter
  demo later; the entry deliberately does not describe it as existing.

## Conventions
- **Branch names are public too.** Never put a client name, or the shorthand Lara uses for a
  client, in a branch name. If a session is handed one that does, say so before pushing and ask
  to move the work.
- **Branches.** `main` holds the current state of the portfolio and is where work belongs.
  **Check whether `main` is actually the repo default before trusting the landing page.** As of
  2026-08-13 it was not: the default was still `claude/portfolio-repo-setup-hxm78l`, and only
  Lara can change it, because repo-settings writes are blocked by the sandbox proxy. If it is
  still wrong, the landing page shows session-one work and *nothing is broken*, so do not
  "fix" it by re-pushing or re-branching. Ask Lara to flip it at
  <https://github.com/laraderosa-lab/laraderosa-solutions/settings>. Once flipped, the two
  `claude/*` branches are redundant and can be deleted.
  Branch per project off `main` (`claude/<slug>-<id>`), commit and push as work completes, then
  merge into `main` so the repo's landing page always shows the real portfolio. Before
  2026-08-13 the default branch was a session-scoped feature branch, which meant pushed work
  was invisible on the landing page. If two sessions run at once the second will hit push
  conflicts, so `git pull --rebase` first.
- Per-project assets in `<slug>/assets/`.
- Never commit a screenshot without checking for firm or party names, claim or policy numbers,
  dollar figures tied to a real matter, adjuster names, dates of loss, or PHI.
