# Lara De Rosa: Solutions

> AI and automation systems delivered inside real operating businesses, from finding the
> problem to running it in production.

Seven case studies. Each one covers what was broken, **how I worked out that it was the thing
worth fixing**, what I built, and what changed as a result.

## The work

| Solution | What it does | Problem it solved | Stack |
|---|---|---|---|
| ★ **[FNOL voice agent](./fnol-voice-agent)** | Voice AI agent phones insurance carriers to open claims, navigating IVRs, holding, and answering the carrier's interview, with a human approval gate and post-call accuracy verification | A 400-person PI firm was spending **~125–200 staff-hours a week** opening claims by phone, a tenth to a sixth of the claims department's whole capacity, one call at a time. Calls now run concurrently. | Retell AI, Copilot Studio, Power Automate, Dataverse, React/TS |
| ★ **[Medical provider selection](./medical-provider-selection)** | Ranks an ~18,000-provider directory by driving distance from the client's home, sends voice AI agents to phone the shortlist for their earliest appointment, and drafts the booking email | Choosing providers cost the same firm's 65-person treatment team **~350–440 staff-hours a week**, around a seventh of its capacity, split between scrolling a specialty-filtered directory with Google Maps open in a second tab and phoning offices one at a time. Ranking is now one search, and the calls run concurrently with nobody on the line. | Power Platform Code App (React/TS), Dataverse, Power Automate, Azure Maps, Retell AI, Copilot Studio |
| ★ **[Marketing attribution](./marketing-attribution)** | Rebuilds a law firm's marketing attribution from ad-account structure through lead capture to settled case value, surfacing ROI per source, campaign and ad group in Power BI | A small criminal-defense and PI firm was spending **well over $500k a year** buying cases and could not attribute a paid search lead at all, because its agency ran one landing page across many ad groups. Its only ROI reporting came from that same agency. | Lawmatics, Clio Manage, Make, Skyvia, BigQuery, Power BI, CallRail, Google Ads |
| [Medical lien calculator](./medical-lien-calculator) | | | |
| [Firm operating dashboards](./firm-ops-dashboard) | Replicates a $50M PI firm's case management and intake systems into a warehouse hourly, and serves leadership, per-team, intake/marketing and financial reports off one shared model | The firm's data was complete and unreadable. Every question spanning two objects was a manual export, so questions that needed asking weekly stopped being asked. Teams could not see progress toward the bonus they were working for. Shipped as a data-first pilot in place of the AI project the client came in asking about. | Clio Manage/Grow, Skyvia, Azure SQL, Power BI |
| **[Document generation](./document-generation)** | Assesses each section of a legal template for the least powerful technique that will fill it, then assembles the document from five levels: boilerplate, merge fields, conditional logic, AI classification, AI narrative | Firms want long documents drafted automatically. Merge-field tooling cannot finish the document, and whole-document AI generation costs more, breaks Word formatting, and puts a review burden on every line. Deciding **per section** is what lets a reviewer know which parts of the page could not have come out wrong. Applied at ~a dozen US PI firms, four directly. | Power Automate, Make.com, SharePoint / Drive, Word field logic, CMS APIs, LLM nodes |
| ★ **[Liability dispute agent](./liability-dispute-agent)** | A chat agent that helps claims staff answer an insurance carrier's liability denial and drafts the reply into the adjuster's email thread, reasoning only from the firm's own reviewed playbooks and verified Vehicle Code sections | Getting liability accepted is **the biggest single measure of a claims rep's performance**, and the firm had no reliable way to make reps better at it. The knowledge was scattered across contradictory documents, the people who could apply it kept leaving, and juniors were filling the gap with public consumer AI. | Copilot Studio, Claude Opus 4.1, SharePoint knowledge set, Power Automate, MS Graph, MCP |

★ = flagship deep dive.
<!-- OPEN: is document generation a flagship? It has the strongest reusable idea of the seven
and the weakest measured impact. Add ★ and bold the row if yes. -->

**Document generation is a method, not a build.** It is the approach used whenever one of the
other solutions has to produce a document, so it appears inside several of the entries above.
It has its own page because the reusable part is the assessment.

The first two came out of **one engagement at one firm**, an audit of two departments that
produced around ten solutions. They share a data platform, a run-status vocabulary and the same
batching pattern, so the case studies cross-reference the shared diagnosis instead of repeating
it.

Four of these came out of a **single engagement at the same firm**, where one audit produced
roughly ten solutions and I delivered them as a program rather than as separate briefs. The
diagnosis that found them is described once, in the FNOL case study.

<!-- OPEN: confirm the exact list of four and that "roughly ten" is the number you want to
     use publicly. Evidence says: FNOL, liability dispute, medical provider, document
     generation. Also confirm whether the firm-ops dashboard is the same client's operations
     console, which would make it five. -->


## Capabilities, by project

Filled in as case studies land, so a reader can see breadth without opening seven files.

| | Discovery / audit | LLM agents | Data modelling | Integrations | Front-end / dashboards | Deployed & handed off |
|---|---|---|---|---|---|---|
| FNOL voice agent | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Medical provider selection | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Marketing attribution | ✅ | | ✅ | ✅ | ✅ | ✅ |
| Medical lien calculator | | | | | | |
| Firm operating dashboards | | | ✅ | ✅ | ✅ | ✅ |
| Document generation | ✅ | ✅ | | ✅ | | ✅ |

<!-- OPEN: two things to check on the document generation row.
  (a) "LLM agents" is the wrong column name for it. That work is prompt orchestration
      (classification nodes, scoped drafting nodes), not agents. Consider renaming the column
      to "LLM systems" so the row is honest, or tell me to blank the tick.
  (b) "Deployed & handed off" is ticked on the strength of "a lot of things were shipped".
      Confirm the client owns and maintains them now, or I will split deployed from handed off. -->

| Liability dispute agent | ✅ | ✅ | | ✅ | | |

## How to read these

Every case study follows the same eight sections, so they're comparable: context, diagnosis,
problem, solution, architecture, my involvement, impact, what I'd do differently.

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
