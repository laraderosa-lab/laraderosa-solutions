# Lara De Rosa: Solutions

> AI and automation systems delivered inside real operating businesses, from finding the
> problem to running it in production.

Seven case studies. Each one covers what was broken, **how I worked out that it was the thing
worth fixing**, what I built, and what changed as a result.

## The work

| Solution | What it does | Problem it solved | Stack |
|---|---|---|---|
| ★ **[FNOL voice agent](./fnol-voice-agent)** | Voice AI agent phones insurance carriers to open claims, navigating IVRs, holding, and answering the carrier's interview, with a human approval gate and post-call accuracy verification | A 400-person PI firm was spending **~125–200 staff-hours a week** opening claims by phone, a tenth to a sixth of the claims department's whole capacity, one call at a time. Calls now run concurrently. | Retell AI, Copilot Studio, Power Automate, Dataverse, React/TS |
| ★ **[Medical provider selection](./medical-provider-selection)** | Ranks an ~18,000-provider directory by driving distance from the client's home, sends voice AI agents to phone the shortlist for their earliest appointment, and drafts the booking email | Choosing providers cost the 65-person treatment team at a 400-person PI firm **~350–440 staff-hours a week**, split between scrolling a specialty-filtered directory with Google Maps open in a second tab and phoning offices one at a time. Ranking is now one search, and the calls run concurrently with nobody on the line. | Power Platform Code App (React/TS), Dataverse, Power Automate, Azure Maps, Retell AI, Copilot Studio |
| ★ **[Liability dispute agent](./liability-dispute-agent)** | A chat agent that helps claims staff answer an insurance carrier's liability denial and drafts the reply into the adjuster's email thread, reasoning only from the firm's own reviewed playbooks and verified Vehicle Code sections | Getting liability accepted is **the biggest single measure of a claims rep's performance**, and the firm had no reliable way to make reps better at it. The knowledge was scattered across contradictory documents, the people who could apply it kept leaving, and juniors were filling the gap with public consumer AI. | Copilot Studio, Claude Opus 4.1, SharePoint knowledge set, Power Automate, MS Graph, MCP |
| ★ **[Marketing attribution](./marketing-attribution)** | Rebuilds a law firm's marketing attribution from ad-account structure through lead capture to settled case value, surfacing ROI per source, campaign and ad group in Power BI | A small criminal-defense and PI firm was spending **well over $500k a year** buying cases and could not attribute a paid search lead at all, because its agency ran one landing page across many ad groups. Its only ROI reporting came from that same agency. | Lawmatics, Clio Manage, Make, Skyvia, BigQuery, Power BI, CallRail, Google Ads |
| [Dashboards](./dashboards) | How I decide what a firm's reporting carries, in two layers. A strategic layer on where cases come from, which sources and referral partners produce signed cases worth having, and what each costs against the case value it returns. An operations layer on team load, stage bottlenecks, and cases at risk from an approaching statute of limitations or from sitting longer than the firm's median for their stage. Both over one warehouse-backed model. Includes the two builds it came from, at two different firms | A firm's data is complete and unreadable. A case management system answers single-object questions, so every question spanning two of them becomes a manual export and the weekly ones stop being asked. Both engagements arrived asking about AI and got the data layer first, on the argument that a firm cannot evaluate AI against a process it cannot see | Power BI, Azure SQL, BigQuery, Skyvia, Clio Manage/Grow, Lawmatics |
| **[Document automation](./document-generation)** | A framework for automating any document that is mostly the same every time. Assess each block for the least powerful technique that will fill it, then assemble from five levels: boilerplate, merge fields, conditional logic, AI classification, AI narrative. Includes a working demand letter, block by block | Firms want long documents drafted automatically. Merge-field tooling cannot finish the document, and whole-document AI generation costs more, breaks Word formatting, and puts a review burden on every line. Deciding **per block** is what lets a reviewer know which parts of the page could not have come out wrong. Applied at ~a dozen US PI firms, four directly. | Power Automate, Make.com, SharePoint / Drive, Word field logic, system-of-record APIs, LLM nodes |
| [Lien reduction letters](./lien-reduction-letters) | Turns one settlement form submission into a letter per lienholder, checking whether the lien pool covers the claims and running the statutory 50/50 pro-rata split when it doesn't, so every letter on the matter reconciles | A Missouri PI firm's case management system couldn't compute the lien split, so settlement figures lived in Excel, the pro-rata math was done on a calculator, and totals were hand-typed into a Word template **once per medical provider** | Fillout, Make, Microsoft 365 Word merge, OneDrive |

★ = flagship deep dive.

**Two of these are frameworks rather than single builds.** Document automation is the approach
used whenever one of the other solutions has to produce a document, so it appears inside several
of the entries above. It has its own page because the reusable part is the assessment. Every
application of it so far has been at legal firms, though nothing in the framework is specific to
legal documents.

Dashboards is the same shape. The page sets out the two layers I scope reporting in and the
data work both of them need underneath, and it carries the two builds it came from as separate
pages, at two different firms on two different stacks. The marketing ROI dashboard sits there
too, since the [marketing attribution](./marketing-attribution) work is what made the numbers on
it true.

Four of these came out of a **single engagement at the same firm**, where one audit produced
roughly ten solutions and I delivered them as a program rather than as separate briefs. Each of
those entries carries its own diagnosis, so they can be read in any order.

## Capabilities, by project

Filled in as case studies land, so a reader can see breadth without opening seven files.

| | Discovery / audit | LLM agents | Data modelling | Integrations | Front-end / dashboards | Deployed & handed off |
|---|---|---|---|---|---|---|
| FNOL voice agent | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Medical provider selection | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Liability dispute agent | ✅ | ✅ | | ✅ | | |
| Marketing attribution | ✅ | | ✅ | ✅ | ✅ | ✅ |
| Dashboards | | | ✅ | ✅ | ✅ | ✅ |
| Document automation | ✅ | ✅ | | ✅ | | ✅ |
| Lien reduction letters | | | | ✅ | | ✅ |

## How to read these

Every case study follows the same eight sections, so they're comparable: context, diagnosis,
problem, solution, architecture, my involvement, impact, what I'd do differently. The two
framework pages, document automation and dashboards, are the exceptions, since a
diagnosis-to-impact arc does not fit a method applied across clients. The builds linked from the
dashboards page follow the sections as usual.

The diagnosis section comes second on purpose. In most of this work the brief I was handed
wasn't the problem that needed solving, and the reasoning that got from one to the other is
the part that transfers to the next client.

## A note on confidentiality

These were delivered for real clients, so **clients are anonymized throughout** and no client
source code, credentials, or case data appears here. Code samples are redacted excerpts
included to show approach, not to be reused. Where a number is quoted it was measured. Where
it wasn't, the case study says so.

---

**Lara De Rosa** · [lara.d@swans.co](mailto:lara.d@swans.co)
