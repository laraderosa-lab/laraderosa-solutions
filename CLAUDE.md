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

Seven total. **All seven now have a draft**, at varying depth. Every slug is confirmed or
corrected, so none of the original guesses survive.

| Slug | Where the slug came from | Tier | Status |
|---|---|---|---|
| `fnol-voice-agent` | **Accurate.** Project is understood | **Flagship** | Drafted, iteration 1 done. One `OPEN` left (measured after-state) |
| `marketing-attribution` | **Accurate.** Renamed from `marketing-engine` once the work was understood | **Flagship** | Drafted. OPEN on the Skyvia/Power BI layer, timeline, and every after-state number |
| `firm-ops-dashboard` | **Close enough.** Confirmed as the dashboard project, though it covers intake/marketing and finance too, so consider a rename | Short | Drafted, gaps open |
| `medical-provider-selection` | **Accurate.** Renamed from `medical-provider-agent` 2026-08-13, because the work is provider *selection* (search, ranking, booking), and the internal app path says so too | **Flagship** | **Materially complete.** All eight sections written, before-state quantified, role and outcome filled in. Outstanding: timeline, status/in-production-since, handover-doc authorship, one technical "what I'd rebuild", and the identifier scan against Lara's real blocklist |
| `document-generation` | Lara's own words. **Accurate**, but it is a *method*, not one build | TBD, leaning flagship | Drafted. Awaiting impact numbers, role detail, video clearance |
| `liability-dispute-agent` | Lara's own words. **Accurate**, project is understood | **Flagship** (proposed, confirm) | Drafted. OPEN on role, timeline, ruled-out alternatives, measured impact |
| `lien-reduction-letters` | **Accurate.** Renamed from the guessed `medical-lien-calculator` once the handover doc arrived | Short entry | Drafted and confirmed. Only `OPEN`s left are timeline, status, and what the rework covered |

**Do not infer what a project is from its slug.** Four of the seven started as placeholders
Claude invented in the first session with no knowledge of the work, and every one of them was
wrong. `fnol-intake-agent` became `fnol-voice-agent` ("intake" means client signup in personal
injury rather than claim opening), `marketing-engine` became `marketing-attribution` (the work
produces no marketing, it measures it), `medical-lien-calculator` became `lien-reduction-letters`
(the calculation is one step, the letters are the deliverable), and `medical-provider-agent`
became `medical-provider-selection`. Ask Lara what a project actually was before naming anything
after it.

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
- **The shared-engagement question is answered: yes.** The client's private documentation repo
  contains one numbered set of ~10 solutions for one firm, covering FNOL, letter of
  representation, loss of use, DMV filings, police report retrieval, policy limit search,
  preservation of evidence, medical provider search and booking, liability dispute, and a
  read-only operations console. `firm-ops-dashboard` is very likely that console, which would
  make it **five** portfolio entries from one engagement, not four. Confirm with Lara.
- **Private client repos are available in-session** on the same GitHub account: documentation
  (three-doc handover set per solution, plus one-page overviews), the Power Platform React
  apps, and the Azure functions. They are **by far the highest-value input** and they are
  private, so read them freely and commit nothing from them verbatim. They are not in the
  session by default, they have to be added and cloned.
- **Identifiers seen in those repos**, all of which must stay out of this repo: the client's
  name and initials, the case-management vendor's name, the Dataverse schema prefix, the
  `fl-<id>-*` flow naming convention, solution package names, the environment host and id, bot
  ids, SharePoint knowledge-folder names, pod names, and Entra group names.
- **Headcount needs reconciling.** The committed FNOL page says ~400 staff and ~30 in claims.
  The client's own ROI model says 99 heads firm-wide and 34 in claims, and their pod directory
  lists 151 people. Those may be different populations (total staff vs. licensed users vs.
  case-carrying pods), but the 400 is load-bearing in the FNOL headline. Ask Lara.
- The firm's ROI model is the source of the modeled per-solution savings. Benchmark is ~125
  new cases a week across 5 pods. Liability disputes arise on ~half of cases.
- **`lien-reduction-letters` is a different client from the FNOL firm.** A Missouri
  plaintiff-side PI firm, on Fillout/Make/Microsoft 365 rather than the FNOL client's Power
  Platform estate, with a different case management system that has **no API at all**. So the
  seven projects span at least two clients, and the root README should not imply one
  engagement produced all seven. Confirm the split with Lara.
- **Handover docs for these projects may be authored by colleagues.** The lien one was, and
  it says "we" throughout. Never write §6 (My involvement) from a doc Lara did not write; ask.
  On the lien project the answer was **co-built**: a colleague wrote the first version, Lara
  reworked it substantially. She asked that the write-up not characterise the earlier version
  as weak, so it says whose it was and stops there. Expect this shape again.
- **Not every project has a diagnosis story or measured impact.** The lien one arrived as a
  defined request and nothing was measured before or after. Lara said so plainly. The right
  move is a short §2 explaining the scoping judgment that was actually made, and a §7 that
  states up front that nothing was measured. Do not pad either section, and never manufacture
  a discovery narrative to fill the template.
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
- **2026-08-13 (second session).** `liability-dispute-agent` drafted on its own branch, from the
  client's private handover docs plus Lara's account. The reframe that makes this one work: it
  is a **knowledge-retention** project that happens to draft emails. High churn was taking the
  firm's liability expertise out of the building, and juniors were filling the gap with public
  consumer AI (confidentiality exposure, hallucinated Vehicle Code citations, arguments with no
  relationship to the firm's own positions). The first deliverable was consolidating scattered
  expert knowledge into one reviewed 15-file set, and only then the agent. Two things sharpened
  it after Lara's answers: the diagnosis **starts with management naming the KPI** (how often a
  rep gets liability accepted is the biggest measure of their performance, and they said they
  wished the team were better at it), and the before-state is a **quality** story, not a time
  one, anchored on a rep sending the carrier a police report that hurt the client's own case.
  The knowledge consolidation was done **from documents, not interviews**, and Lara did all of
  it. Still open: timeline, status, ruled-out alternatives, whether the handover docs are hers.
  Modeled impact is in the draft and labelled as such; the KPI itself was never instrumented,
  which is now §8's first entry.
- **2026-08-14.** `medical-lien-calculator` renamed to `lien-reduction-letters` and drafted
  as a short entry from one handover doc (a colleague's, not Lara's). The domain content is
  solid: the statutory net-recovery split, the pro-rata pool, and why a per-lienholder letter
  set has to reconcile against a shared derivation. Scrubbed from the source before drafting:
  client firm name, doc author's name, case management vendor name, and a client wiki URL
  containing the firm name. Lara then confirmed: co-built with a colleague, no diagnosis
  story, no metrics. Rewritten to say all three plainly instead of carrying `OPEN` blocks, so
  the entry reads as finished. Left open: timeline, current status, and which parts her
  rework covered.

- **2026-08-15 (consolidation).** Seven parallel session branches were merged into `main`,
  which is now the trunk and the only branch holding the whole portfolio. Sessions had been
  branching off the old default and never merging back, so Lara opened the repo and saw session
  one. Root README reconciled by hand: both tables carry all seven projects, flagships grouped
  first, the superseded "the first two came out of one engagement" paragraph dropped in favour
  of the four-project version, and duplicate stale rows removed. CLAUDE.md is the union of all
  seven branches' findings, with the progress log put back in date order. **Two things need
  Lara.** First, `main` still is not the GitHub default, so the landing page shows the old
  branch until she flips it in repo settings. Second, **two remote branch names carry client
  identifiers** (`claude/citrine-marketing-mme404` and `claude/clio-manage-life-dashboard-e1rdm5`)
  and branch names are public, so they should be deleted; both are fully merged, so nothing is
  lost. Nine branches are now redundant and can go.

## Conventions
- **Branch names are public too.** Never put a client name, or the shorthand Lara uses for a
  client, in a branch name. If a session is handed one that does, say so before pushing and ask
  to move the work.
- **Branches.** `main` is the trunk and holds the whole portfolio. On 2026-08-15 all seven
  session branches were merged into it, so it is the only branch that carries every case study.
  Branch per project off `main` (`claude/<slug>-<id>`), commit and push as work completes, then
  **merge back into `main` before the session ends**, or the landing page will not show the
  work. If two sessions run at once the second will hit push conflicts, so `git pull --rebase`
  first.
  **Check whether `main` is actually the repo default before trusting the landing page.**
  Repo-settings writes are blocked by the sandbox proxy, so only Lara can set it, at
  <https://github.com/laraderosa-lab/laraderosa-solutions/settings>. Nothing is broken if it is
  wrong, so do not "fix" it by re-pushing or re-branching, just say so.
- Per-project assets in `<slug>/assets/`.
- Never commit a screenshot without checking for firm or party names, claim or policy numbers,
  dollar figures tied to a real matter, adjuster names, dates of loss, or PHI.
