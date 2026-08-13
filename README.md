# Lara De Rosa: Solutions

> AI and automation systems delivered inside real operating businesses, from finding the
> problem to running it in production.

Seven case studies. Each one covers what was broken, **how I worked out that it was the thing
worth fixing**, what I built, and what changed as a result.

## The work

| Solution | What it does | Problem it solved | Stack |
|---|---|---|---|
| ★ **[FNOL voice agent](./fnol-voice-agent)** | Voice AI agent phones insurance carriers to open claims, navigating IVRs, holding, and answering the carrier's interview, with a human approval gate and post-call accuracy verification | A 400-person PI firm was spending **~125–200 staff-hours a week** opening claims by phone, a tenth to a sixth of the claims department's whole capacity, one call at a time. Calls now run concurrently. | Retell AI, Copilot Studio, Power Automate, Dataverse, React/TS |
| ★ **[Medical provider selection](./medical-provider-selection)** | Ranks an ~18,000-provider directory by driving distance from the client's home, sends voice AI agents to phone the shortlist for their earliest appointment, and drafts the booking email | The same firm's 65-person treatment team was spending **~200–250 staff-hours a week** on hold to provider offices, a twelfth to a tenth of its capacity, and picked providers by scrolling a specialty-filtered directory and copy-pasting two addresses into Google Maps once per candidate. Selection is now one search, and the calls run concurrently with nobody on the line. | Power Platform Code App (React/TS), Dataverse, Power Automate, Azure Maps, Retell AI, Copilot Studio |
| [Marketing engine](./marketing-engine) | | | |
| [Medical lien calculator](./medical-lien-calculator) | | | |
| [Liability dispute agent](./liability-dispute-agent) | | | |
| [Firm operations dashboard](./firm-ops-dashboard) | | | |
| [Document generation](./document-generation) | | | |

★ = flagship deep dive.

The first two came out of **one engagement at one firm**, an audit of two departments that
produced around ten solutions. They share a data platform, a run-status vocabulary and the same
batching pattern, so the case studies cross-reference the shared diagnosis instead of repeating
it.

## Capabilities, by project

Filled in as case studies land, so a reader can see breadth without opening seven files.

| | Discovery / audit | LLM agents | Data modelling | Integrations | Front-end / dashboards | Deployed & handed off |
|---|---|---|---|---|---|---|
| FNOL voice agent | ✅ | ✅ | ✅ | ✅ | ✅ | |
| Medical provider selection | ✅ | ✅ | ✅ | ✅ | ✅ | |
| Marketing engine | | | | | | |
| Medical lien calculator | | | | | | |
| Liability dispute agent | | | | | | |
| Firm operations dashboard | | | | | | |
| Document generation | | | | | | |

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
