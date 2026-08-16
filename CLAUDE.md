# Project context for Claude

## What this repo is
A **public portfolio of AI/automation solutions Lara De Rosa has delivered**, as personal
advertisement. Target readers are hiring managers for forward-deployed engineer / solutions
architect / AI engineer roles, who look for **end-to-end ownership**: finding the problem, not
just building the ticket.

A **case-study portfolio, not a code repo**. Prose, diagrams and sanitized evidence, with
redacted code excerpts where they prove something.

## Standing decisions (do not re-litigate)
- **Clients are anonymized.** No client names, firm names, people, product codenames, or
  identifiable case data in **any committed file, including this one.** Use role descriptors
  ("a 400-person plaintiff-side PI firm"). Specificity comes from detail, not names.
- **Software vendors are fine to name**, including the CRM and the case management system
  (2026-08-15, Lara). Retell, Microsoft, Power Platform, Lawmatics, Clio, CallRail, Skyvia,
  BigQuery, and whatever CMS a firm runs on. Thousands of firms use each of these, so naming one
  identifies nobody, and the constraints they impose are half of why the architecture looks the
  way it does. Only the client is anonymous. This settles the "naming Clio needs a ruling" open
  question below. **`fnol-voice-agent` still says "the case management system" throughout and
  that stays**, which is a deliberate choice on that entry rather than a leftover of the older
  rule, so do not offer to name it.
- **This repo is public.** Assume every commit is world-readable the moment it lands.
- **Code: illustrative excerpts only.** Redacted snippets of the interesting parts (a prompt,
  a schema, a scoring rule). No client source, no credentials, no PHI/PII, no real schema
  prefixes, table names or flow names.
- **Label an excerpt for what it is** (2026-08-16, Lara). Most of this work is built in Power
  Automate, Make and similar, so an excerpt is usually **the logic of a flow written out as
  code**, not source lifted from a repo. Rendering it as code is fine and beats a screenshot of
  a designer canvas. **Calling it "redacted" is not**, because that word tells the reader it is
  the real artifact with identifiers swapped, and it invites an interview question Lara would
  have to correct mid-answer. `medical-provider-selection`'s batch-gate excerpt was caught this
  way: it was written from the handover docs plus Lara's verbal account, the underlying thing is
  a cloud flow, and the label claimed otherwise. It now opens "Not source code."
  **The other entries' excerpts have not been audited.** Sessions after this one wrote them and
  their provenance is unknown, so before treating the repo as publication-ready, check each
  against its real artifact and relabel any that are reconstructions. Ask Lara rather than
  inferring, since only she knows which excerpts came from something she pasted.
- **Depth is tiered.** 3 flagship deep dives, 4 short entries.
- **Length follows the project. The rule is concision, not a word count** (2026-08-15, Lara).
  A bigger project earns a longer entry. `marketing-attribution` rebuilt five layers across
  three months and runs proportionally long, which is correct for what it covers. Judge a draft
  by whether every paragraph is carrying something, and never against a target.
  **Do not write a word count into this file.** A "~3,000 to 3,400 words" rule used to live
  here, generalised from a single entry's edit, and it bound every session after it until Lara
  asked where the number came from. Replacing it with a different number repeats the mistake.
  What still holds: when something genuinely is bloated, the fix is a **structural cut** (a
  table that restates an earlier section, a second diagram, a third code excerpt) rather than
  word-level tightening, which does not move the total.
- Every case study follows `_template/README.md` section for section.
- **Every case study stands alone.** A reader may open any entry first, so shared context
  (the client, the audit, a constraint two projects hit) is restated in that entry's own words
  rather than delegated to a sibling. "The same audit as the FNOL agent" is not allowed as
  load-bearing prose. Links to sibling entries are fine as see-also, and never as a prerequisite.
- **Diagnosis is a first-class section.** How the problem was found (audit, process mapping,
  interviews, data) is the differentiator for forward-deployed roles.
- Diagrams are **Mermaid**. Open questions are `<!-- OPEN: ... -->` HTML comments, so they
  don't render publicly but stay greppable.
- **No em dashes**, and no AI-slop patterns (colon reveals, "not X but Y" contrasts, asides
  telling the reader what matters). Write this way in the first draft rather than fixing it
  afterwards.
- **The canonical style guide is `petergyang/no-ai-slop` on GitHub, `main` branch.** Always
  read it before drafting or editing prose here, and do not rely on a local skill of the same
  name or on memory of what it says. Two files matter:
  ```bash
  git clone --depth 1 https://github.com/petergyang/no-ai-slop.git
  # skills/no-ai-slop/SKILL.md   the rules: words to cut, patterns to cut, editing principles
  # skills/no-ai-slop/eval.md    the checklist to run against the draft afterwards
  ```
  Run the `eval.md` checks against what you wrote before committing. The patterns that actually
  catch things in this repo are interpretive metadiscourse (a sentence telling the reader what
  the previous sentence means), aphoristic kicker lines, restating a point the prose already
  showed, and generic sentences that fail the portability test.
- **No swagger** (2026-08-15, Lara). Cut "I would say so in an interview", "the decision I would
  defend hardest", "the part worth noticing", "the row that matters". State what was done and
  why it mattered, then stop. Nobody asked.

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
- [ ] `<slug>/README.md` follows all eight template sections. **§8 is the exception: it only
      exists if Lara supplied it.** An entry ships with seven sections rather than an invented
      "what I'd do differently". This has already been got wrong twice.
- [ ] Root `README.md`: the project's row filled in, plus its row in the capability matrix
- [ ] `★` added to the row if it's a flagship
- [ ] No client, firm or person names anywhere, and every image checked
- [ ] No em dashes; slop pass done
- [ ] `CLAUDE.md` progress log and solutions table updated
- [ ] Committed and pushed

### Pre-commit scan
```bash
grep -rn "—" --include="*.md" .          # em dashes, expect 0
grep -rn "OPEN:" --include="*.md" .      # outstanding questions
```
Client names, firm names and the names of people at a client must never reach a commit. They
are not listed here, because this file is public. **The blocklist ritual is retired**
(2026-08-15, Lara): do not ask for a list of banned terms at the start of a session. The guard
is that a name should never enter a draft in the first place. Write role descriptors from the
start rather than typing a name and scrubbing it later, and when a name arrives in source
material (a handover doc, a transcript, a screenshot) it stays in the session and does not get
typed into a file. Software vendor names are not covered by any of this, see the standing
decisions.

## The seven solutions

Seven total. **All seven now have a draft**, at varying depth. Every slug is confirmed or
corrected, so none of the original guesses survive.

| Slug | Where the slug came from | Tier | Status |
|---|---|---|---|
| `fnol-voice-agent` | **Accurate.** Project is understood | **Flagship** | Drafted, iteration 1 done, plus a third §8 item added 2026-08-16 (two-way write-back). One `OPEN` left (measured after-state) |
| `marketing-attribution` | **Accurate.** Renamed from `marketing-engine` once the work was understood | **Flagship** | **Iterations 1, 1b and 2 done.** §8 exists with one item, Lara's, and may gain more. See the 2026-08-15 log entries for what was corrected; do not re-litigate any of it. Six `OPEN`s left in `README.md` and two in `dashboard.md`, and they are the whole to-do list: the dashboard PDF (re-upload needed, it never survives a session), what the ~50 sources collapsed into (N sources / M campaigns), client headcount, the ~$30k/mo lead vendor and ~$20k/mo PPC figures, the dashboard's own design decisions, and a **business outcome for §7**, which is the weakest part of the entry |
| `firm-ops-dashboard` | **Close enough.** Confirmed as the dashboard project, though it covers intake/marketing and finance too, so consider a rename | Short | Drafted, gaps open |
| `medical-provider-selection` | **Accurate.** Renamed from `medical-provider-agent` 2026-08-13, because the work is provider *selection* (search, ranking, booking), and the internal app path says so too | **Flagship** | **Iterations 1 to 4 done**, and the most finished entry in the repo. **§8 now exists with one item, Lara's** (two-way write-back), and may gain more. Outstanding: in-production-since date and user count, handover-doc authorship, and the evidence screenshots |
| `document-generation` | Lara's own words. **Accurate**, but it is a *method*, not one build. Entry retitled "Document automation" 2026-08-16, folder not yet renamed | TBD, leaning flagship | **Restructured 2026-08-16 as a framework page**, off the eight-section template. Carries a synthetic demand-letter demo. Awaiting: the demand-letter assessment table checked, impact numbers, role detail, video clearance |
| `liability-dispute-agent` | Lara's own words. **Accurate**, project is understood | **Flagship** (proposed, confirm) | Drafted. OPEN on role, timeline, ruled-out alternatives, measured impact |
| `lien-reduction-letters` | **Accurate.** Renamed from the guessed `medical-lien-calculator` once the handover doc arrived | Short entry | **Complete except for one `OPEN`** (what Lara's rework covered). **§2 and §6 deliberately removed 2026-08-16**, so it runs six sections. ~2 weeks, completed and delivered |

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
  **Its source material is gone from every session but recoverable.** The entry was built from a
  90-minute client-handover transcript, a client walkthrough PDF, and a connector definition and
  replication config Lara pasted. Uploads never survive, so to go deeper than the committed
  entry, search **Fireflies** for the handover call rather than asking Lara to re-explain the
  system. The dashboard PDF has to come from her.
- **Naming Clio is settled: yes** (2026-08-15). Software vendors including the CRM and the CMS
  can be named, see the standing decisions. `firm-ops-dashboard` keeps Clio Manage and Clio Grow.
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
  unreadable, see above). Different, much smaller client than FNOL. The story (**both halves of
  this sentence were corrected on 2026-08-15: the client asked for the work rather than Lara
  pitching it unasked, and the source count was about 50, not a thousand**): junk marketing
  sources, a whole capture channel arriving
  with no attribution because the agency set no UTM parameters, PI revenue never reaching the
  reporting system, and conversion rates inflated by dropped cases that stayed marked hired.
  The strongest beat is non-technical, getting a hostile vendor onto one-landing-page-per-ad-
  group (**corrected 2026-08-15: Lara negotiated this with the agency herself. The "escalated
  to the firm's owner" version was invented and is wrong**). Lawmatics and Clio Manage cleared
  for naming. Still
  open: the Skyvia-to-Power BI layer (Lara built a custom Lawmatics connector, vibe coded, and
  the transcript predates it), the timeline, Lara's role split, and every after-state number.
  The client walkthrough doc arrived later as a PDF and confirmed the workstream structure,
  added the accounting-system and referral-fee cost mapping, and showed that each workstream was
  designed in Figma and walked through with the client before being built. (**Partly wrong,
  corrected 2026-08-16: the dashboard was not designed in Figma at all.** The claim came from
  that PDF, which is unrecoverable, so "each workstream" cannot be trusted. §6 now narrows it to
  the taxonomy rework and carries an `OPEN` asking whether even that is right. Do not restate
  the every-workstream version.) It does not mention
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
  branch until she flips it in repo settings. (**Done 2026-08-16: Lara switched the default to
  `main`.**) Second, **two remote branch names carry client
  identifiers** (`claude/citrine-marketing-mme404` and `claude/clio-manage-life-dashboard-e1rdm5`)
  and branch names are public, so they should be deleted; both are fully merged, so nothing is
  lost. All nine `claude/*` branches are now redundant.
  **Deletion cannot be done from a session.** `git push --delete` returns 403 from the git host
  for every branch, while ordinary pushes succeed, so the session's credentials allow creating
  and updating refs but not removing them. The proxy logs no relay failure, so this is not the
  egress policy. There is no branch-deletion tool on the GitHub MCP server either. Do not retry
  it, and do not try to route around it. Lara deletes branches at
  <https://github.com/laraderosa-lab/laraderosa-solutions/branches>, and
  `claude/portfolio-repo-setup-hxm78l` can only go after the default is moved to `main`.
- **2026-08-15 (provider selection, iteration 1).** Straight onto `main`. Four corrections from
  Lara. **Role is the same shape as FNOL**: co-owner of the idea and the diagnosis, sole owner
  of the end-to-end implementation. The old "sole engineer, ideation through build" was wrong on
  the front half. **Timeline is FNOL's**: 6 weeks, first conversation to rollout, alongside the
  nine other solutions, and status is completed and rolled out. **The treaters' role was written
  too narrowly.** They book appointments (the largest single piece), *and* follow up and check in
  on clients through treatment, *and* chase bills and records back from the offices afterwards.
  §1, the Domain row and §3 all said or implied booking-only. **New standing style rule: every
  case study must stand alone.** Do not write "the same audit as FNOL" or "the same firm as FNOL"
  as load-bearing prose, because a reader may open any entry first. Cross-links are fine as
  see-also, and shared context gets restated in the entry's own words. §1, §2 and the §5 excerpt
  note were rewritten on that basis, plus the root README line saying the diagnosis is "described
  once, in the FNOL case study". Two clarity fixes: the pre-state availability calls went to
  **the offices of the best few matches**, not to every office in the specialty; and the booking
  email is **composed by the system**, with the human only reviewing and clicking send, so §2 no
  longer reads as though a person writes it.
  **A session handed a `claude/*` branch may be looking at a stale clone.** This one started on
  a branch cut before `main` existed, so the checkout showed a three-line stub and CLAUDE.md's
  old seven-projects table, and the first answer was "there is no draft". `git fetch origin main`
  and check `origin/main` before telling Lara something is missing.
- **2026-08-15 (provider selection, iteration 2).** Slop pass plus a substantial cut, on Lara's
  instruction that *this* doc was too long. Structural cuts, not just tightening:
  the two architecture diagrams merged into one, the shortlisting code excerpt dropped (the
  trade-off row already carries it), §7's before-state table cut from eleven rows to four since
  it duplicated §3, and the constraints list cut from five bullets to three. Slop removed: the
  "matters more than it sounds" and "the one I care most about" metadiscourse, the "I would
  rather publish that gap than fill it" kicker, the "half a job" kicker, and several colon
  reveals. (This entry's "aim for ~3,200 words on future entries" instruction was **superseded
  on 2026-08-15**, see the length standing decision. The cut was right for provider selection
  and wrong as a general rule.)
  Four corrections from Lara, all of which changed content rather than wording:
  1. **The §2 reframe was wrong.** It said the ask was "make the directory easier to search" and
     that better search does not help. False dichotomy. The client did want easier search *and*
     the directory kept centralised in the case management system, and both were delivered. The
     ranking layer is a third thing on top, not a replacement.
  2. **The do-not-use story is misinformation, not an unused field.** Staff were never instructed
     to use the checkbox, so they typed free-text "DNU" notes onto provider records instead. A
     note has no date anyone trusts, and the few records actually ticked were stale, so nobody
     knew whether an old tick still applied. The data was contradictory rather than absent. The
     fix was making the checkbox the only way to mark a provider, plus documentation and training,
     so the field gets cleaned in the CMS and then in the app's mirror.
  3. **Booking by email has practical reasons, not just policy.** The request usually carries the
     client's previous records as attachments, and the email thread is what the coordinator
     follows up on weeks later. Also: the draft is unsent because **that is the chosen human
     review point**. The alternative was a review screen in the app followed by an automatic
     send, and reviewing a draft in your own outbox is a thing coordinators already do all day.
  4. **The ad-hoc provider option is not a contradiction of FNOL's "carriers only in the CMS"
     rule.** The difference is sync latency. FNOL reads the CMS live, so a carrier added upstream
     appears on the next run and an in-app shortcut would only fragment the source of truth. This
     catalog is a daily mirror, so the same rule would make a coordinator wait a day to place a
     call. Hence ad-hoc for today, with training to add it upstream so it syncs overnight. The
     §5 table now carries this contrast explicitly.
  (This entry's "the CMS vendor stays out of every committed file" note was **superseded on
  2026-08-15**, see the software-vendors standing decision. The entry still says "the case
  management system" throughout, which is now a choice rather than a rule, and Lara has not
  asked for it to be named.)
- **2026-08-15 (provider selection, iteration 3).** Three deletions, all Lara's.
  1. **§8 "What I'd do differently" is gone entirely**, because Claude wrote it. Four of the five
     bullets were defects lifted out of the handover docs (the type-check deploy gap, the
     specialty-gated search trap, the Teams bot install dependency, the manual specialty refresh)
     and the fifth was an invented reflection about instrumentation. **This is the second time an
     invented §8 has had to be deleted**, after FNOL. Do not write that section from documents or
     from inference. It only exists if Lara says it. An `OPEN` comment now sits where the section
     was, so the gap is greppable without rendering. **The entry therefore has seven of the eight
     template sections on purpose**, which is a deliberate exception to the definition of done.
  2. **§7's "What was not measured" paragraph is gone.** The single reportable outcome (the
     do-not-use flag is now maintained) stays. Do not restore a paragraph enumerating what was
     never measured.
  3. **§6 was overclaiming.** Lara did **not** implement the scheduled job that refreshes the
     provider table daily. Rewritten to FNOL's shape: a co-owned idea and diagnosis paragraph,
     then a bulleted list of what she did build (the ranking, the React app, the Retell voice
     agent, the Power Automate flows), then the timeline. The "what I did not own: change
     management" paragraph went too. **New rule: §6 lists what Lara did, not what she did not**,
     and the change-management boundary lives in the At a glance role row instead. When a
     handover doc describes a component, that is not evidence she built it. Ask.
- **2026-08-15 (provider selection, iteration 3b).** §6 corrected again, this time upward. The
  **geocoding is hers** and it is the best pure-engineering detail in the repo: ~18,000 provider
  addresses to Azure Maps via an Azure Function, coordinates back into Dataverse, **batched 100
  rows at a time on both ends and calling the Dataverse API directly rather than the prebuilt
  actions**. That is 180 calls per side instead of 18,000, **~90% off the geocoding cost and a
  full run from a few hours to ~15 minutes**. What she did *not* build is the **daily catalog
  sync that refreshes the provider table from the case management system**, which is the job the
  previous draft wrongly attributed to her. The two are easy to confuse because §4 describes them
  as a pair of scheduled jobs. §6's list is now in her own order: geocoding, React app, the
  call-running flow, the booking-email flow, the Retell agent. Azure Functions added to the stack
  row. **Lesson: when a correction removes a component, ask what the adjacent ones actually were
  rather than dropping the whole area.** The first pass deleted the geocoding along with the sync
  and lost a measured 90% cost win.

- **2026-08-15 (marketing, iteration 1).** On `main`. Lara's corrections, all of which changed
  content: **timeline is ~3 months**, roughly a month each on attribution, cost mapping and
  dashboard design, replacing the "20 to 30 hours across 2 to 3 weeks" scoping figure.
  **Status is finalised and handed over.** **The ~1,000 sources figure was wrong: it was about
  50**, a flat list mixing genuine sources, entries that should have been campaigns under a
  grouped source, duplicates and stale spend. The count was wrong in four places including the
  impact table and the Figma line. **The "pitched unasked for months" story is wrong and is
  gone**: the client asked for the work and Lara was told they wanted it, then owned everything
  from scoping to handover. §2's "why it had stayed unfixed" paragraph and §6's "months of
  pitching a project nobody had asked for" both went with it.
  **§4 restructured into the six-step chain Lara described**, each step a prerequisite for the
  next: taxonomy (source vs campaign, defined) → route both capture channels into it (longest
  phase: the ad account restructure, CallRail number pools, the ClickFunnels form path, the
  agency negotiation) → remap history → cost → revenue → warehouse and dashboard. The through
  line she wanted stated plainly: the client is spending money it cannot attribute.
  **`"crim is the one does doesn't need the retroactivity"` is resolved.** Criminal defense is
  priced at intake so its value is already correct in the CRM, and only personal injury needs
  the settled value carried back from Clio. §4 step 5 says so.
  **Five passages deleted at Lara's instruction**, plus their restatements elsewhere: the
  archive-junk-matters-to-a-sheet trade-off, the custom-fields-as-JSON trade-off, the
  Lawmatics-fires-once-per-matter and CallRail-cannot-filter-by-number constraints, and the
  API-returns-duplicate-records constraint. Knock-on trims: the daily-sync code excerpt (whose
  comment restated the once-per-matter fact), the "API produces duplicates anyway" clauses, and
  §8's "whether the phone line should have been routed through call tracking at all".
  **Dashboard split into `marketing-attribution/dashboard.md`**, referenced at the end, because
  the doc was too long. The five pages moved there. It still needs the PDF, which did not
  survive the session.
  **Iteration 1b, same day.** More corrections, several of which killed invented content.
  **Lara negotiated the agency changes herself. She did not escalate to the firm's owner**, and
  that claim was in both §4 and §6. **Status is finalised and rolled out**, not handed to a
  colleague. **The "we could fake the numbers in the dashboard" blockquote is gone**, since
  Lara did not recognise it. **The cost mechanism was wrong**: everything lands in the Google
  Sheet automatically, and the manual fifteen minutes is the **intake manager** transcribing
  from the sheet into Lawmatics, which also answers where costs live. **The conversion-rate
  mechanism is specific**: a lead is marked hired in Lawmatics, migrates to Clio, gets dropped
  in Clio, and nothing communicates back, so it stays hired and inflates the rate. That is the
  flow she built, and §4 step 5 now covers only that one, since the did-not-hire and
  junk-matter jobs matter less to this solution. **The forms path was written so only its
  author could follow it** and is rewritten: the agency posted ClickFunnels submissions
  straight into the CRM with no source or campaign, because their forms never captured that
  information, so Lara negotiated the webhook to her own Make scenario, which derives ad group
  from landing page and campaign from ad group. Submitting a Lawmatics form is just how a lead
  gets created, not a design choice, and the old text claimed otherwise.
  **New: preempt the gclid objection.** A reader who knows Google Ads will ask why gclid was
  not used. It resolves only inside Google's stack, Lawmatics cannot read or exchange it, and
  the agency fed click data to their own systems, which is why only they could report. §2 now
  says so. Also: call it **the Google Ads account**, never "the ad account".
  **Length rule corrected**: concision, not a word count. The entry was briefly cut against the
  old target and then restored in full, since the project is a large one and the cuts were
  serving a number rather than the reader. Also ported into this file: the
  `petergyang/no-ai-slop` pin, the loosened anonymization rule, the retirement of the blocklist
  ritual, and a no-swagger rule.
  **Process failure worth recording.** This session was handed `claude/marketing-attribution-
  iteration-nca1jd`, worked on it for four commits, and only discovered `origin/main` existed
  when a push was rejected. The clone had two branches in it, so `git branch -a` looked like the
  whole repo, and the session told Lara the marketing draft "was never committed and was lost"
  when it was sitting on `main` the whole time. **Run `git fetch origin` and look at
  `origin/main` before concluding anything about what does or does not exist.**

- **2026-08-16 (marketing, iteration 2).** Corrections from Lara, on `main`.
  **Two decision rows were factually wrong and are rewritten.** The cost row said Lawmatics'
  native cost entry is daily; it is **per campaign and per period, daily, weekly or monthly,
  and Lara set it to monthly**, so the "divide by thirty and type it thirty times" line was
  invented arithmetic. The Power BI row said native reporting "cannot reach Clio or the sheet";
  wrong, and it contradicts the whole document. **The ROI data is unified in Lawmatics, and the
  dashboard needs neither Clio nor the sheet to answer the ROI question.** Power BI was chosen
  for **cross-filtering**: which source converts best, which sources and campaigns produce the
  most rejected leads, which lost cases the firm caused against which it turned away and why,
  with sub-categories under each reason. Clio data alongside it is a **bonus, not a dependency**.
  The same wrong reasoning was in §4 step 6 and in `dashboard.md`, and was fixed in all three.
  **"The API is paginated at 100 records a page and rate limited to ten requests a second" was
  a fabrication** built by reading Lara's own connector config back as though it described the
  API. Those are values *she set*, and the config's own comment says the throttle is a guess.
  Lawmatics publishes **150 requests a minute**, so the configured 10/sec is likely four times
  over. The claim is gone from `README.md` and `dashboard.md`. **Rule: a value in a config is a
  choice, not a documented property of the thing it points at.**
  **The incremental-overlap row claimed duplicate rows.** It upserts on record id, so the
  overlap costs a re-read, not a duplicate. Fixed in the row, the code comment and the note
  under the excerpt.
  **§8 deleted, Claude's again, third time across the repo** (after FNOL and provider
  selection). Lara will write it. An `OPEN` marker sits where it was.
  Other cuts, all Lara's: the custom-field-cleanup and Lawmatics-to-Clio-mapping sentence out
  of §6 (not part of this project), the "not mine, a colleague set up Clio" paragraph, and the
  "finding outside the brief" paragraph about the Clio task backlog. **The agency had a
  negative incentive, not a neutral one**: the reporting being built measures its performance
  and can contradict its own reports. **The pre-signed vendor finding was wrong.** It is not
  that average settlement came in under $3k; it is that **most of those cases are dropped after
  signing** (wrong matter type, client at fault, client goes MIA), which only became visible
  once drops flowed back from Clio. Lawmatics alone had it as the best-converting source.
  §7's reporting row now links `dashboard.md`.
  **Process, again.** This session repeated the exact failure logged on 2026-08-15: it was
  handed a stale clone with two branches, ran `git branch -a`, and told Lara the marketing
  draft did not exist. `git fetch origin` **first**, then look at `origin/main`.
  **§8 then written, from Lara, two items.** First, embed Lawmatics forms on the firm's own
  website and **set the UTM parameters on the landing pages herself, which the agency does
  not**, so source and campaign arrive filled in and the ClickFunnels to webhook to Make to
  landing-page-derivation chain disappears. Her reason for calling the shipped design weaker is
  the external dependency, not the complexity. Second, **the cost ingestion is over-engineered
  for a task a person does in two minutes**, which is her phrasing.
  **Five candidates were put to her and four were rejected. Do not re-propose them:**
  1. "I should have built the dashboard first." **Rejected, and the premise was false.** She
     could not have built a dashboard on data that bad. **The §2 paragraph claiming two of the
     four problems were discovered by modelling data for the dashboard is deleted, because it
     is not true.** Do not reintroduce a discovered-it-from-the-dashboard story anywhere.
     **The real provenance**, and §2 now says so: findings 3 and 4 (PI revenue reading zero,
     cases dropped in Clio still marked hired in Lawmatics) came out of Lara's own analysis
     while she was building the revenue side of the ROI, not out of the initial audit and not
     out of any reporting layer.
  2. A companion report for the unticked final-value checkbox. Rejected: the checkbox is still
     the best approach, so a known disadvantage of a design she would keep does not belong in a
     "what I'd do differently".
  3. The connector replicating SSN, driver licence and date of birth into the warehouse.
     Rejected, she would not say that is true.
  4. The throttle configured above the API's published ceiling. Rejected.
  **`dashboard.md` filled out from Fireflies**, which worked and should be the first move next
  time a gap needs source material. The **V1 dashboard walkthrough is `01KKXZYVJSF7XZVY53CE7BEE5R`,
  2026-03-23, organised by Lara**, and she demos the dashboard herself from ~10:40 to ~32:00.
  **Read the transcript, not the AI summary**: the summary garbles "Lawmatics" as "Nomadics" and
  "Clio" as "Kio", and a summary is not a source. What it yielded, all verified against her own
  words: conversion rate **excludes anything still in intake** (an unresolved lead is not a lost
  one, so the dashboard deliberately disagrees with the CRM's native figure); qualification rate
  is hostage to invalid leads in the denominator; **targets have to be per source and weighed
  against source cost**, so goal lines were deferred until the client had used real data;
  cross-filter to drill from a rejection reason to sources to the individual matters, each
  deep-linked into the CRM; a **practice-area view including the work the firm rejects**, to
  expose unmet demand; scheduled extracts replacing a staff member's weekly spreadsheet;
  the **financial report migrated in from Looker Studio**, which is what makes settlement value
  joinable to lead source; **V1 shipped with PI case value missing** because the backflow was not
  finished; **Power BI Pro per viewer**; and an **AI query layer asked for by the owner and
  deferred**, because there is nothing to flag before targets exist.
  **Two things to check with Lara.** The Clio-fed pages were still hypothetical on 2026-03-23
  ("same thing if we ever did a dashboard for Clio") and **the account transitioned to a
  colleague over the following month**, so §6's claim to the whole dashboard may be overclaiming
  the same way provider selection did. And she had **already built a marketing dashboard natively
  in Lawmatics** before this one.
  **Then the five dashboard screenshots arrived** (2026-08-16) and `dashboard.md` was rebuilt
  around them: what it is (five tabs, page by page), **how the pages relate** (source is a shared
  dimension, lead to matter to settled value and back onto the lead, with a Mermaid diagram),
  what it exists to do, the measure definitions, and the design decisions. Verified from the
  images: **conversion rate = hired / (hired + did not hire)**, with intake excluded, which
  matches her explanation exactly; loss reasons are ~20 codes prefixed to say who ended it,
  rolled into three categories (firm rejected, did not hire, invalid); **median case value is
  shown next to total, not average**; the financial page separates cash received, revenue earned
  but unpaid, and outstanding balance, with a gross/net toggle. **The deployed tab names are
  "Lawmatics: Intake Overview", "Clio: Matters Overview", "Financial Dashboard", "Task Tracker"
  and "Lawmatics Monthly"**, which does not match the five-page list the entry had, and two of
  those tabs have never been seen. An `OPEN` asks her to map them.
  **The screenshots are not publishable and Lara said so herself.** Firm name and logo on every
  page, client names, emails and phone numbers, case numbers built from client surnames,
  attorney and staff names, referral partners by name, both marketing vendors by name with one
  of them inside a source name, area codes that place the firm, and real settlement figures.
  **Do not commit them without a substitute-at-source or crop-to-aggregates pass.**
  **One number to check with her**: §7 says "around one lead in ten is invalid". The lost-lead
  summary makes invalid ~10.7% of *lost* leads, which is ~6.5% of all leads, though the
  practice-area view has several invalid-ish buckets that together run higher. Not changed,
  because the definition varies by page and she knows which one the claim came from.
  **Later biweeklies are a colleague's, not hers.** The 2026-07-13 sync shows the dashboard in
  use and the owner winding down the marketing agency on the back of ad-spend-versus-hires
  analysis, which is the business outcome §7 is missing, but it happened post-handover. Do not
  put it in §6 or §7 without her ruling.
  Also cut this round, all Lara's: the ROI-data-is-unified opening of the Power BI decision row
  (it survives once in §4 step 6, and the row now argues cross-filtering only), "and had already
  declined to help" from the landing-page row, **the whole "On the connector" paragraph in §6**
  (the vibe-coded explanation, which she found unclear even after a plain-language rewrite), and
  "That took several meetings, which I did myself" from the unglamorous-parts paragraph.

- **2026-08-16 (§8 write-back, two entries).** Lara's own item, and it lands in **both**
  `medical-provider-selection` and `fnol-voice-agent`: the integration with the case management
  system runs one way, so she would make the systems write back into it. In provider selection
  that means adding a provider or ticking do-not-use from the app and having it land upstream,
  which is what the ad-hoc-provider and flag-stays-upstream trade-off rows are working around.
  In FNOL it means adding a carrier from the app. Her stated reason is that **this case
  management system's API is very limited**, so write-back was not available, and she would
  build it two-way on a system that accepts writes. `medical-provider-selection` therefore has
  §8 for the first time, and its "deliberately absent" `OPEN` is replaced by one saying more
  items may come. **This is the first §8 content that did not have to be deleted, because it
  is hers.**
  **Note the tension to watch:** the 2026-08-15 FNOL rule was "do not mention the CMS API at
  all, assume it has one". The new item names the API's limits as the reason on both pages.
  Lara gave it in one breath covering both projects, so it is written that way, and she has
  been asked to confirm. If she vetoes, the FNOL item can stand on "the integration only runs
  one way" without naming the cause.
  Process: this session opened on a **stale clone again**, the third time. `git branch -a`
  showed two `claude/*` branches and no `main`, the working tree was the 2026-08-13 scaffold,
  and the first answer to Lara was that the medical entry was an unwritten stub. It is on
  `main` and has been since 2026-08-15. `git fetch origin main` **before** answering anything
  about what exists.
- **2026-08-16 (liability dispute, §7 and §8 pass).** On `main`. Two deletions and a rewrite,
  all Lara's. Deleted from §7: the closing paragraph saying the liability acceptance rate was
  never instrumented. Deleted from §8: the case-reading tool being named for a smaller job than
  it does. **She keeps the three remaining §8 items but not the way they were written.** They
  read as running down the work. **New standing rule for §8: write the rebuild, not the
  regret.** Each item is now "I'd do X" and argues for what the change would give the firm,
  rather than naming the shipped build's weakness and then offering a fix. Two things she
  called out specifically: **"for very little work" is Claude's opinion and had to go**, since
  a session has no basis for estimating effort on a system it did not build, and **"I never
  instrumented X" becomes "I'd instrument X"**. Cut on the same grounds: "the weakest part of
  the build", "the honest gap in this case study", "the strongest claim in this case study",
  and "the thing I would go back and change first". The §5 no-gate trade-off row still points
  at §8 and still resolves.
  **Then, same day.** The §8 usage-reporting item deleted too, so §8 is down to two: the
  regression set behind the playbooks, and measuring the outcome. **Timeline and status are
  FNOL's**: 6 weeks from the first client conversation to rollout, alongside nine other
  solutions from the same firm-wide audit, completed and rolled out. Both `OPEN`s in At a
  glance are closed. Written **without naming FNOL**, per the stand-alone rule, and §2's
  opening sentence ("the same firm-wide audit that produced the FNOL voice agent") was
  rewritten for the same reason. When Lara says two projects share a fact, write the fact into
  the entry, never the sibling's name.
- **2026-08-16 (FNOL, §5 architecture).** On `main`. Lara said the diagram misportrayed the
  runtime, and gave the real chain. It is now drawn as: extension → **Copilot agent** → flow 1
  (reads the case, resolves parties and carriers) → **one row per party per carrier** in
  Dataverse, which feeds the review app. Submit fires flow 2, which sends **one HTTP request
  per selected carrier to Retell** and writes **only request status** to the row. Retell posts
  back to **flow 3, the webhook**, which **branches**: no human reached **re-dials Retell
  directly** (not via flow 2), **3 attempts in total**, with the **attempt count updated on the
  same row and no new row created**; human reached runs the accuracy evaluation, updates the
  row, and writes the claim number and adjuster into the case management system **by API call**.
  **Flows notify through the Copilot agent in Teams**, so notification edges go flow → agent →
  staff rather than flow → staff. The review app is **also the results surface**: outcome,
  accuracy evaluation and full transcript are read there. §4 step 1's "one row per carrier"
  corrected to per party per carrier.
  **Open tension, flagged not resolved.** §8 says the integration only runs one way and that
  this CMS's API is too limited for write-back, but flow 3 writes the claim number and adjuster
  in through the API. So writes work for some things and not others. An `OPEN` sits in §8
  asking Lara which it is; her words were left untouched.
  Mermaid can be validated in-session: `npx -y @mermaid-js/mermaid-cli@11 -p pc.json -i x.mmd
  -o x.svg` with `pc.json` containing `{"args":["--no-sandbox","--disable-setuid-sandbox"]}`.
  Without the puppeteer config it dies as root; the config takes an **array**, not an object.
- **2026-08-16 (lien letters, shorter shape plus the no-reduction path).** On `main`. Two
  changes from Lara. **The scenario branches**: it computes the pool, tests it against the
  total claimed, and if the pool covers the claims it drafts the letters with each lienholder
  paid in full, skipping the pro-rata split entirely. Only a shortfall triggers the
  calculation. The point is that the firm can use the tool on any settlement rather than only
  the ones needing a reduction, and before this those letters were still typed one at a time.
  Written into §1 (a closing paragraph), §2, §3 (step 2 is now the branch), the diagram (a
  decision node), a new decisions row, the code excerpt (`needsReduction`), and the §5 table.
  Root README row updated too. **The no-reduction letter is close to the same template**, per
  Lara, stating the amount that will be paid rather than asking the lienholder to accept less.
  **§2 (Diagnosis) and §6 (My involvement) deleted at Lara's instruction, because this is a
  short entry, and the remaining sections renumbered 1 to 6.** Nothing load-bearing was lost:
  the no-API and no-math-in-the-CMS facts moved into §2 Problem, the scoping decision already
  lived in the first §4 decisions row, and the co-built role is in the At a glance row, where
  the "which parts did the rework touch" `OPEN` now sits. **A short entry can drop template
  sections beyond §8.** Provider selection dropped §8 only; this one drops two from the
  middle. Do not restore them.
  **The code excerpt was relabelled.** It said "Redacted and simplified", which claims it is
  the real artifact with identifiers swapped. It is a Make scenario written out as code from a
  colleague's handover doc, so it now opens "Not source code", matching the fix made to
  `medical-provider-selection`. **Two `Redacted and…` labels remain in `marketing-attribution`
  and still need Lara's ruling** on whether they are real pasted artifacts.
  **§8, now §6, was Claude's and is gone. Fourth time across the repo** (after FNOL, provider
  selection and marketing). The rounding remainder, the placeholder contract and the manual
  log-back were all inference from the handover doc. **Replaced with Lara's own, one item**:
  she'd read settlement amounts out of the case management system and write the calculated
  reductions back, and the reason she did not is that the system's API could not support it.
  One paragraph rather than a bullet list. The §4 excerpt note's "See §6" pointer and its
  independent-rounding clause went with the deleted bullet.
  Then two more deletions, both Lara's. **§5's "Nothing here was measured" opening paragraph
  is gone**, the same cut she made to provider selection's §7, so Impact starts on the
  before/after table. And **§6 does not get framed as a small build**: "a build this small
  does not carry a long list" went, because the section should read as an ordinary change
  rather than an apology for having one item. **General rule: do not preface a section with
  a note about its own size or completeness.**
  **At a glance closed**: timeline **~2 weeks**, status **completed and delivered**. Lara's
  note that this is a simpler solution than the others is the reason the entry stays short,
  and it is not written into the entry itself. The only `OPEN` left on this project is which
  parts her rework covered, which sits on the role row.
  **Slop pass run against the pinned `petergyang/no-ai-slop` repo.** Vocabulary was clean. Seven
  pattern fixes, all cuts or clarity: three pieces of metadiscourse ("which is exactly the
  direction it should not scale", "What earns the excerpt is…", "Every downstream decision
  follows from that"), an abstract topic sentence ahead of the fact it introduced ("The pattern
  also generalises"), an inanimate subject doing a human verb ("so the case file still knows
  the letters exist"), a dangling quantifier ("Every lienholder cannot be paid in full" to "Not
  every lienholder can be paid in full"), and a fragment in a code comment. Bold-inside-prose
  was left alone, since it is house style across all seven entries.

- **2026-08-16 (document automation, restructured as a framework page).** On `main`. Lara said
  the eight-section template does not fit a framework, and that the approach is not legal-only.
  Both are right, and the entry is rebuilt around it.
  **What the misfit was.** §2 Diagnosis was not a diagnosis, it was the argument for why
  whole-document AI and merge-fields-only both fail. §3 Problem restated it. §7 Impact had no
  number and its table described a property of the method rather than a measured outcome. The
  five-level table, the strongest thing on the page, sat two thirds down.
  **New shape, eight sections but not the template's**: 1 the framework (levels table first
  screen), 2 why the two obvious approaches fail, 3 how to assess a document (a five-step
  procedure, previously two sentences, and the most transferable part), 4 worked example, 5
  where the work runs, 6 the two levels that need care, 7 trade-offs and constraints, 8 my
  involvement and what changed. **At a glance rows changed too**: Client / Timeline / Status do
  not apply to a framework, so it is What it is / Applies to / Where it has been used / My role
  / Provenance / Stack / Status.
  **Generalization rule, confirmed by Lara**: she has not applied it outside legal but sees no
  reason it would differ. So the framework is written generally ("document", "system of
  record"), with one line saying every application so far has been US plaintiff-side PI firms,
  and no claim it has been proven elsewhere. "The CMS" survives only inside the worked example.
  **The worked example is a demand letter**, Lara's choice. It carries a section-by-section
  assessment table (section, what varied between past letters, level, why not a level higher).
  **That table is Claude's reconstruction and is flagged `OPEN` as the first thing to check.**
  The two findings it produces: most of a demand letter is Levels 1 to 3, and the treatment
  summary and damages blocks, which clients assume need AI, are the most mechanical on the page.
  **A demo shipped**: `assets/demand-letter-levels.html`, self-contained, synthetic throughout,
  every block shaded by level with a click-through panel giving what fills it, what it may read,
  and how it can be wrong. Lara chose static-and-portfolio-facing over a runnable version with
  real model calls, so **do not build the runnable one without asking**. Screenshots committed
  in both themes because GitHub renders committed HTML as source, not as a page.
  Colors are an **ordinal** ramp (levels are ordered), single blue hue, validated in both modes
  with the dataviz skill's script. Text stays in text tokens; the rail and an L1..L5 badge carry
  identity, so the letter stays readable and identity is never colour-alone.
  **Structural cut**: the level-tagged `jsonc` template excerpt is gone, because the demo page
  does that job better. The Level 4 contract excerpt stays and was **relabelled from "Redacted
  and simplified" to "Not source code"**, matching the lien and provider fixes.
  **`Redacted and…` labels: there are five in the repo, not the two this file recorded.**
  `liability-dispute-agent`, `fnol-voice-agent`, and `marketing-attribution` twice, plus the one
  fixed here. All still need Lara's ruling on which are real pasted artifacts.
  **No "what I'd do differently" section**, per the standing rule. An `OPEN` sits where it would
  go. Root README updated: row renamed to Document automation, the method paragraph rewritten,
  the eight-sections line given an exception clause, capability row renamed.
  **Open naming question**: the folder is still `document-generation` while the entry is titled
  document automation.

## Conventions
- **Branch names are public too.** Never put a client name, or the shorthand Lara uses for a
  client, in a branch name. If a session is handed one that does, say so before pushing and
  work on `main` instead. **Two such branches exist right now and still need deleting**, see the
  2026-08-15 log entry.
- **Work on `main`. It is the only branch.** Commit and push straight to `main` as work
  completes. Do not create a feature branch unless Lara asks for one.
  Sessions are handed a branch name automatically (`claude/<something>-<id>`). **Ignore it**,
  `git checkout main` and work there. If a session has already committed to a handed branch,
  merge it into `main` before the session ends.
  This is a standing correction, not a preference. Until 2026-08-15 every session worked on its
  own branch and none merged back, so seven drafts existed and the repo's landing page showed
  none of them. Lara saw an empty-looking portfolio and reasonably concluded nothing had been
  pushed.
  `git pull --rebase` before pushing, since another session may be running.
  **`main` is the GitHub default as of 2026-08-16**, so a fresh clone lands on it and the
  landing page is correct. Before that it was not, and sessions were handed branches cut from a
  stale 2026-08-13 default, which is how one session read a three-line stub and told Lara the
  provider case study did not exist. If a checkout ever looks impossibly old again, run
  `git remote show origin` and `git fetch origin main` before concluding anything is missing.
  Repo-settings writes are blocked by the sandbox proxy, so only Lara can change the default, at
  <https://github.com/laraderosa-lab/laraderosa-solutions/settings>. Nothing is broken if it is
  wrong, so do not "fix" it by re-pushing or re-branching, just say so.
- Per-project assets in `<slug>/assets/`.
- Never commit a screenshot without checking for firm or party names, claim or policy numbers,
  dollar figures tied to a real matter, adjuster names, dates of loss, or PHI.
