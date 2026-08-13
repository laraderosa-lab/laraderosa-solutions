# Lara De Rosa: Solutions

> AI and automation systems delivered inside real operating businesses, from finding the
> problem to running it in production.

Seven case studies. Each one covers what was broken, **how I worked out that it was the thing
worth fixing**, what I built, and what changed as a result.

## The work

| Solution | What it does | Problem it solved | Stack |
|---|---|---|---|
| ★ **[FNOL voice agent](./fnol-voice-agent)** | Voice AI agent phones insurance carriers to open claims, navigating IVRs, holding, and answering the carrier's interview, with a human approval gate and post-call accuracy verification | A 400-person PI firm was spending **~125–200 staff-hours a week** opening claims by phone, a tenth to a sixth of the claims department's whole capacity, one call at a time. Calls now run concurrently. | Retell AI, Copilot Studio, Power Automate, Dataverse, React/TS |
| [Marketing engine](./marketing-engine) | | | |
| [Medical lien calculator](./medical-lien-calculator) | | | |
| ★ **[Liability dispute agent](./liability-dispute-agent)** | A chat agent that helps claims staff answer an insurance carrier's liability denial and drafts the reply into the adjuster's email thread, reasoning only from the firm's own reviewed playbooks and verified Vehicle Code sections | Getting liability accepted is **the biggest single measure of a claims rep's performance**, and the firm had no reliable way to make reps better at it. The knowledge was scattered across contradictory documents, the people who could apply it kept leaving, and juniors were filling the gap with public consumer AI. | Copilot Studio, Claude Opus 4.1, SharePoint knowledge set, Power Automate, MS Graph, MCP |
| [Medical provider agent](./medical-provider-agent) | | | |
| [Firm operations dashboard](./firm-ops-dashboard) | | | |
| [Document generation](./document-generation) | | | |

★ = flagship deep dive.

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
| FNOL voice agent | ✅ | ✅ | ✅ | ✅ | ✅ | |
| Marketing engine | | | | | | |
| Medical lien calculator | | | | | | |
| Liability dispute agent | ✅ | ✅ | | ✅ | | |
| Medical provider agent | | | | | | |
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
