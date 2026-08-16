# FNOL Voice Agent

> A voice AI agent that phones insurance carriers to open first-notice-of-loss claims for a
> 400-person personal injury firm. It navigates the IVR, sits on hold, answers the carrier's
> interview, and writes the claim number back into the case file. Software can hold five
> phone lines at once and a person can't, so a case that took **2.5 hours of sequential
> calling now takes one ~30-minute step.**

## At a glance

| | |
|---|---|
| **Client** | Plaintiff-side personal injury firm, ~400 staff, ~$50M annual revenue (US) |
| **Domain** | Claims operations, a ~30-person department, opening FNOL claims with carriers |
| **My role** | Co-diagnosed the problem and co-decided the approach. Built the voice agent and the system around it |
| **Timeline** | 6 weeks from the first client conversation to rollout, alongside nine other solutions from the same audit |
| **Stack** | Retell AI (voice), Microsoft Copilot Studio, Power Automate, Dataverse, AI Builder, React/TypeScript Code App, Teams, Chromium extension |
| **Status** | Completed and rolled out |

---

## 1. Context

The firm runs plaintiff-side personal injury cases across a ~400-person operation, of which
the claims department is about **30 people**. When a new case arrives, that department has to
open a claim with **every insurance carrier attached to the accident**: the client's own
insurer (first-party) and each defendant's insurer (third-party). None of the substantive
work on the file can begin until those claim numbers exist.

Most carriers still only accept a new claim **over the phone**.

## 2. Diagnosis: how I knew this was the problem to solve

This project came out of an audit. Nobody asked for a voice agent.

**Stage one. The firm's own data pointed at a department.** Management had measured time on
desk per department. Claims consumed **more man-hours than any other** without being the
slowest, so what stood out was the volume of work per file rather than how long a file
waited.

That points at a department rather than a workflow, so there was nothing to build yet.

**Stage two. Interviews down the whole ladder.** We audited the claims department by talking
to it end to end: department management, case builders, and the people doing the day-to-day
work. Management describes the process as designed. The people doing it describe what
actually happens. The gap between those two accounts is where the finding was.

The heaviest workflow turned out to be the most mundane one, *opening the claim*. Each call
ran **30–40 minutes**, and almost none of that time went on skilled work. It went on:

- navigating the carrier's IVR menu tree,
- waiting on hold,
- then answering a long, repetitive interview about the accident: facts of loss, vehicles,
  drivability, airbags, seatbelts, policy details.

Every answer already existed in the case management system. A person was reading a screen
down a phone line for half an hour.

**Why it added up to real money.**

| | |
|---|---|
| New cases per week (department) | ~100–125 |
| Claims to open per case (avg) | ~2.5 (client's carrier, defendant's carrier, usually at least one more) |
| Carrier calls per week | **~250–310** |
| Duration each | 30–40 min |
| **Weekly staff time** | **~125–200 hours** |

The department has about 30 people, so its total weekly capacity is roughly 1,200 hours.
Claim-opening calls were consuming 125–200 of them. That is **between a tenth and a sixth of
the entire department's capacity**, or three to five people doing nothing but working menus
and waiting on hold.

It is also why the audit landed here rather than on a more interesting workflow. This was the
department's largest problem rather than its hardest, and it was made entirely of work nobody
needed a person for.

**The reframe.** The obvious framing is that the calls take too long, so make them shorter.
That caps out fast, because you can't compress a carrier's interview much below its question
list. The actual constraint is that a human can only be on one call at a time. A case with
five carriers means five sequential calls, roughly 2.5 hours of wall clock, and no one call
is slow. They cannot overlap. The bottleneck was **serialization**. That makes the target
concurrent calls, and the only way to get concurrency is to take the human off the line.

This FNOL agent was **one of roughly ten solutions** the audit produced for this client. It
was prioritized early because the cost was large, measurable, and concentrated in a single
repetitive workflow, which is what you want from a first target while a program still has to
prove itself.

## 3. Problem

Opening claims consumed **125–200 staff-hours a week**, a tenth to a sixth of the claims
department's entire capacity, in unskilled telephone time. Because calls could only run one
at a time, each new case sat for hours before substantive work could start. The cost scaled
linearly with caseload, so growth made it worse. The work was too repetitive to justify
skilled staff and too consequential to do carelessly. These are recorded calls with an
opposing insurer at the start of a legal matter.

## 4. Solution

A voice AI agent places the carrier calls, and a human approves what it's going to say before
it dials.

From the case file open in front of them, a staff member clicks a browser extension and picks
**FNOL**. Everything after that is automated up to a single review step:

1. **Intake.** The system reads the case, works out every party on the accident and every
   carrier attached to them, and builds **one reviewable row per carrier**. Multi-defendant
   and multi-policy cases fan out correctly, so two defendants with two policies each is four
   claims to open.
2. **Human review.** The reviewer gets a card in Teams, opens the claim, checks the
   pre-filled details, fixes anything wrong, and **selects which carriers to call.** Nothing
   dials until they hit submit. If a carrier is missing, they add it in the case management
   system first, because the app deliberately won't let them create one.
3. **Parallel calling.** Every selected carrier is called **simultaneously**. The voice agent
   works through the IVR, holds, reaches a human, and answers the carrier's interview from
   the approved case data, while staying inside limits on what it will *not* disclose.
4. **Automatic retry when no human is reached.** Carrier lines fail in ordinary ways. The IVR
   changes, the menu path dead-ends, nobody picks up. When a call ends without reaching a
   person, the system calls that carrier again, up to **three attempts** in total, before it
   tells the staff member no human was reached and to try later.
5. **One-click retry.** If all three attempts fail, the staff member retries from the app
   itself. One button re-launches the same approved call, or set of calls, without going back
   to the case file, re-opening the extension, or re-reviewing data they already approved.
6. **Write-back.** Each call returns the **claim number, whether the claim was opened, the
   assigned adjuster and their contact details**, plus a transcript, recording and summary.
   These go back into the case management system and the case file.
7. **Accuracy check.** A second AI pass compares **what the agent actually said on the call**
   against **what the reviewer approved**, field by field, and flags mismatches. Nobody has
   to read a transcript to check the agent. If nothing is flagged, nothing went wrong.

The staff member's involvement drops from ~2.5 hours of talking to a few minutes of
reviewing.

## 5. Architecture

```mermaid
flowchart TB
  staff(["Claims staff"])

  subgraph client["In the tools staff already use"]
    ext["Browser extension<br/>on the case file"]
    agent["Conversational agent<br/>(Copilot Studio)"]
    app["Review app<br/>(React, in Teams)"]
  end

  subgraph orch["Orchestration (cloud flows)"]
    f1["1 · Intake<br/>read case → resolve parties → one row per carrier"]
    f2["2 · Place calls<br/>one outbound call per selected carrier"]
    f3["3 · Post-call<br/>write-back + accuracy evaluation"]
  end

  subgraph data["System of record"]
    t[("Review table<br/>1 row per claim per attempt")]
    cms[["Case management system"]]
  end

  voice["Voice AI agent<br/>(Retell)"]
  carrier["Insurance carriers<br/>(by phone)"]
  llm["LLM prompt steps<br/>party extraction · accuracy scoring"]

  staff --> ext --> agent --> f1
  f1 --> cms
  f1 --> llm
  f1 --> t
  f1 -->|"ready to review"| staff

  staff --> app
  app <-->|"read / correct"| t
  app -->|"approve + select carriers<br/>· one-click retry"| f2
  f2 --> t
  f2 ==>|"N calls, concurrently"| voice
  voice <-->|"IVR → hold → interview"| carrier

  voice -->|"webhook"| f3
  f3 --> llm
  f3 --> t
  f3 -.->|"no human reached<br/>auto-retry, 3 attempts max"| f2
  f3 -->|"claim no. + adjuster"| cms
  f3 -->|"outcome / accuracy alert"| staff
```

### Key decisions and tradeoffs

| Decision | Why | What I gave up |
|---|---|---|
| **Human review sits between automated intake and automated calling** | Review costs minutes. The call costs 30–40 and cannot be taken back, since you cannot un-say something to an opposing carrier on a recorded line. Gate the unrecoverable step, not the cheap one. | Not fully autonomous. A person is in the loop on every case. |
| **One adaptable agent for every carrier**, rather than a scripted agent per carrier | Hardcoding the big carriers (press 2, then 4, then read these answers) is cheaper per call and more predictable. It also covers only the carriers you built for, breaks the day one reorders its IVR or changes its questions, and has nowhere to go when a call leaves the script. An agent that can work an unfamiliar menu and answer an unfamiliar interview handles every carrier the firm might call, and survives them changing their process. | Higher cost per call, and much more iteration on the call design. |
| **No direct carrier API integrations, ruled out by the deadline** | Submitting a claim straight into a carrier's system is faster, cheaper and less error-prone than phoning it, and we have built those integrations on other work. Every carrier would need its own custom integration, built one at a time. Speed was the priority here, so it stayed out of scope for this build. | The highest-volume carriers get dialed when they could be sent a request. First thing I would revisit (§8). |
| **Post-call accuracy evaluation on top of prevention** | Prevention does most of the work and holds misstatement under 3% of calls. Some hallucination is inherent to any AI build. The evaluation catches the rest, and it is also what makes the system usable. Without it, staff would read every transcript to be sure, which costs about what the call did. Because the system reports its own errors loudly, no alert means the call was accurate. | A second LLM pass per call, and the last few percent are fixed after the fact rather than prevented. |
| **Two tiers of severity on that check** (essential and minor) | Some answers have to be right for the claim to be right, like date of loss, client name, passenger count. Others carry no urgency if they come out wrong, like airbag deployment or the weather. Both kinds are reported and visible after the call. Only an essential mismatch raises an urgent alert, which is what keeps the alert worth reacting to. | Which fields are essential is a judgement call, and the list needs maintaining. |
| **Carriers can only be added in the case management system, never in the app** | Adding a missing carrier from inside the app is the obvious convenience, and it would save a reviewer about two minutes. It would also undermine the need to keep the case management system updated, and risk fragmenting data away from the source of truth. I designed for the best user experience that did not cut against the bigger client purpose. | A slower path when a carrier really is missing, and a feature that reads as an omission until someone asks why. |
| **Automatic retry, then a one-click retry** | Not reaching a human is the common failure and usually transient, so three attempts absorb most of it unnoticed. When it does need a person, the expensive part (reading the case, checking the data, approving it) is already done and should not be repeated. | A genuinely unreachable carrier takes three attempts to surface instead of one. |
| **Built entirely inside the firm's existing Microsoft estate** | The firm was already on Teams, Entra and Power Platform. A standalone app meant new logins, a new access model, and IT owning something unfamiliar. Access comes from existing group membership. | Platform ceilings. Per-service capacity and throttling limits, and the solution is bounded by what the platform exposes. |
| **Triggered from a browser extension on the case file** | Staff live in the case management system all day. Making them navigate elsewhere and paste a case ID is where adoption dies. One click, in place. | An extension to distribute and maintain per-user. |
| **No credentials in the client app** | All carrier calling, case-system access and messaging happen server-side in the flows. The browser app holds no secrets. | Slightly more indirection, since the UI can't call third parties directly. |

### Constraints I built inside

- **Non-technical end users.** Claims staff, not analysts. The whole surface is one click in
  the browser and one card in Teams.
- **Recorded, adversarial calls.** The counterparty is the opposing insurer, and the call
  becomes part of the record on a legal matter. That drove both the pre-call human gate and
  the post-call verification.
- **The agent had to withhold as well as answer.** A plaintiff firm should not volunteer
  everything to a defendant's carrier, so scope of disclosure was a design requirement.

### Illustrative excerpt: the accuracy evaluator's contract

*Redacted and simplified. The model scores each field, and severity is derived in code, so
the model never grades its own homework.*

```jsonc
// Post-call: the transcript is compared against the values the reviewer approved.
// The model returns per-field verdicts only. It does not decide how bad the miss is.
{
  "fields": [
    { "key": "date_of_loss",  "approved": "2026-03-14", "heard": "2026-03-14", "status": "correct" },
    { "key": "policy_number", "approved": "<redacted>",  "heard": "<redacted>", "status": "correct" },
    { "key": "airbags",       "approved": "Did not deploy", "heard": null,      "status": "not_disclosed" },
    { "key": "client_name",   "approved": "<redacted>",  "heard": "<redacted>", "status": "incorrect" }
  ]
}
```

```js
// Severity is computed deterministically, outside the model.
// A model that both makes the error and rates its seriousness is not a control.
const ESSENTIAL = ['date_of_loss', 'client_name', 'policy_number', 'vehicle', /* … */];

const scored    = fields.filter(f => f.status !== 'not_provided_by_user');
const incorrect = scored.filter(f => f.status === 'incorrect');

const severity =
  incorrect.length === 0                                   ? 'perfect'   : // green
  incorrect.some(f => ESSENTIAL.includes(f.key))           ? 'essential' : // red  → alert + pin open
                                                             'minor';     // yellow → visible, no alert

const score = Math.round(
  (scored.filter(f => f.status === 'correct').length / scored.length) * 100
);
```

Three deliberate choices there. Fields the reviewer never supplied are excluded from the
denominator, so the score isn't punished for absent data. `not_disclosed` (the agent didn't
say it) is tracked separately from `incorrect` (the agent said it wrong), because they are
different failures. And only `essential` interrupts a human. A `minor` mismatch is still
reported and still visible after the call, but it raises no alarm, which keeps the alarm
worth reacting to.

## 6. My involvement

I co-ran the diagnosis and co-decided what to build. The project came out of the department
audit in §2 rather than a client request.

I then built the voice agent and the system around it:

- **The voice agent in Retell AI.** The call design, the prompting, how it handles a carrier's
  interview, and the limits on what it will not disclose to an opposing insurer.
- **The Power App.** The review surface where staff check the pre-filled claim, correct it,
  choose which carriers to call, and retry.
- **The Power Automate flows.** Intake and party resolution, placing the concurrent calls,
  the retry logic, write-back into the case management system, and the post-call accuracy
  evaluation.
- **The Copilot Studio agent.** The conversational entry point staff talk to.

Six weeks from the first client conversation to rollout, running alongside the nine other
solutions the same audit produced.

## 7. Impact

**The before state, measured in the audit:**

| Metric | Before |
|---|---|
| Carrier calls per week | ~250–310 |
| Duration per call | 30–40 min (IVR + hold + interview) |
| Weekly staff time on claim opening | **~125–200 hours**, or 10–17% of the 30-person department's capacity |
| A five-carrier case | ~2.5 hours of sequential calling |
| Staff time per case (avg 2.5 carriers) | ~90 minutes |

**What the design changes, mechanically.** Calls stop being sequential. A five-carrier case
goes from ~2.5 hours of one-at-a-time calling to a single review step plus five concurrent
calls. The wall clock becomes the length of the *longest* call rather than the *sum* of them,
and the staff member isn't on any of them. Per-case human involvement drops from ~90 minutes
of talking to a few minutes of reviewing.

<!-- OPEN: this section deliberately stops at "mechanically" because I only have the
before-state numbers. To make it land I need whatever was actually measured after
deployment:
  - claims opened through the agent (count, over what period)
  - measured hours saved / change in time on desk, if tracked
  - how often the agent successfully opened the claim (success rate)
  - how often the accuracy check caught a real error, even "we found N in M calls"
  - adoption: how many staff use it, is it the default path now
If none of it was measured, say so and I'll write it as an honest qualitative outcome. An
unverifiable percentage in a public portfolio is worse than no percentage. -->

## 8. What I'd do differently

- **Re-evaluate the voice platform.** Retell was a good choice at the time. Voice AI is moving
  fast enough that the right answer has a short shelf life, so I would benchmark the
  alternatives again rather than assume the original pick still wins.
- **Go to the largest carriers directly and try to skip the call.** A handful of carriers
  account for most of the volume. For those I would open a conversation about an API
  integration that submits the claim straight into their system, which is faster, cheaper and
  less error-prone than dialing, and would leave the voice agent to cover the long tail. We
  have built that kind of integration successfully on other work. Here it lost to the six-week
  timeline. That was the right call then, and it is the first thing I would pick up next.
- **Let the app write back into the case management system.** A carrier can only be added in
  the case management system, never in the app. I chose that to keep one source of truth, and
  it costs a reviewer the slower path on the day a carrier really is missing. It had to be a
  rule because the integration only runs one way. This case management system's API is limited
  enough that writing back was not on the table. Given one that accepts writes, I would let a
  reviewer add the carrier where they are already working and push it back, which keeps the
  source of truth intact without sending someone into another system first.

---

<details>
<summary>Evidence</summary>

<!-- Candidates, all needing a redaction pass before they go in:
     - Review app screenshot with the carrier list (client/party names blurred)
     - Accuracy check: field-by-field comparison view, green/yellow/red
     - A Teams outcome card
     - A sanitized call transcript excerpt (best single artifact, since it shows the agent
       handling a real carrier interview; needs heavy redaction: no party names, no policy
       or claim numbers, no carrier name)
     Check every image for: firm name, party names, claim/policy numbers, dollar figures,
     dates of loss, adjuster names, PHI. -->

Not yet added.

</details>
