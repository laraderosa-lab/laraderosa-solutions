# Medical Provider Selection and Booking

> A provider search and booking app for the treatment team at a 400-person personal injury
> firm. It ranks an ~18,000-provider directory by driving distance from the client's home,
> sends voice AI agents to phone the shortlist for their earliest appointment, and drafts the
> booking email. Choosing providers was costing the 65-person team **~350–440 staff-hours a
> week**, around a seventh of its capacity, none of it needing clinical or legal judgment.
> **Ranking is now one search, and the calls run concurrently with nobody on the line.**

## At a glance

| | |
|---|---|
| **Client** | Plaintiff-side personal injury firm, ~400 staff, ~$50M annual revenue (US). Same firm and same engagement as the [FNOL voice agent](../fnol-voice-agent), different department |
| **Domain** | Treatment coordination. Following a client's post-accident care and booking the appointments a doctor recommends |
| **My role** | Sole engineer. Ideation, diagnosis, design and build, end to end. Change management was the client's, by agreement |
| **Timeline** | <!-- OPEN: dates + duration --> |
| **Stack** | React/TypeScript Code App on Microsoft Power Platform, Dataverse, Power Automate, Azure Maps (custom connector), Retell AI (voice), Copilot Studio, Leaflet/MapLibre, Outlook, Teams |
| **Status** | <!-- OPEN: in production since when? how many users? --> |

---

## 1. Context

The same audit that produced the FNOL voice agent covered a second department at this firm. The
claims department opens claims with carriers. The **treatment team**, about **65 people**,
handles what happens next: tracking a client's medical care after the accident, and when a
doctor recommends a procedure or a specialist, finding a provider and booking the appointment.

Booking appointments is the bulk of that team's day. Two things make provider choice
consequential rather than clerical. The firm cares how fast a case moves through the pipeline,
so the provider with the earliest opening is usually the right one. And these providers treat
on a lien, meaning they get paid out of the eventual settlement, so how much a provider
historically reduces its bill affects what the client actually keeps.

## 2. Diagnosis: how I knew this was the problem to solve

**The method here was shadowing, not interviewing.** For the claims department the finding came
out of interviews down the management ladder, because the gap between the process as designed
and the process as run was where the waste hid. The treatment team's problem was visible in a
way that interviews would have flattened, so we sat with them and watched them book
appointments.

**What the screen actually required.** The case management system holds a contact directory of
roughly **18,000 providers**, filterable by specialty. There are twenty to thirty specialties,
so filtering leaves a shorter list, and still a list to be read. The directory has no
coordinates, no map, and no distance sort.

So to answer "who is near this client", a coordinator:

1. filtered the directory to the specialty the doctor recommended,
2. scrolled the resulting list,
3. copied the client's address into Google Maps,
4. copied a candidate provider's address in after it,
5. read off the distance, and repeated from step 4 for the next candidate.

Then, having picked candidates, they phoned each office to ask its earliest availability,
because the earliest opening moves the case fastest. Sequential calls, each one through an IVR
and a hold queue.

**The list itself could not be trusted.** Two findings came out of watching people use it:

- Notes on provider records were **outdated**, so what the record said and what staff knew
  disagreed.
- The directory has a **"do not use" checkbox**, and it was not used to mark do-not-use
  providers. Which providers to avoid lived in individual coordinators' heads.

That second finding reads as staff carelessness and it is not. The field was not missing.
Ticking it had no consequence anywhere in anyone's workflow, so nobody ticked it. That makes it
a governance problem, and adding a second exclusion flag inside a new app would have reproduced
it exactly.

**The reframe.** A request like this arrives as "make the provider directory easier to search",
and better search does not help. A directory answers "what do we know about this provider". The
coordinator's question is "which of these 18,000 is the best choice for *this* client, today",
which resolves against four things at once:
driving distance from the client's home, whether the provider is excluded, how much the
provider tends to reduce its bill, and how much of the firm's existing caseload already sits
with it. Ranking against a specific client is a different job from storage, and the system of
record was never built to do it.

**The second half of the reframe** is the same finding as FNOL, arrived at independently. Once
you have a shortlist you still have to phone every office, and a person holds one line at a
time. Three ten-minute calls is thirty minutes of wall clock because they cannot overlap.

**What I ruled out.** The one worth recording: **letting the voice agent book the appointment on
the call.** Firm policy requires appointment requests in writing, so a phone booking would not
have counted. The agent confirms availability and a human sends the email, which is why the
workflow ends in a draft rather than a sent message.

The design alternatives I weighed inside the build are in §5 rather than here, since each one is
easier to follow next to the decision it lost to.

<!-- Asked Lara 2026-08-13 for other alternatives evaluated and rejected; nothing further to add
for now. Leave this as-is rather than padding it with plausible-sounding options. -->

## 3. Problem

Choosing a provider took a manual pass over a specialty slice of an 18,000-row directory,
followed by copy-pasting two addresses into Google Maps once per candidate, on a team whose
main job is booking appointments. The list carried outdated notes and an exclusion flag nobody
filled in, so selection quality depended on which coordinator happened to be doing it.
Confirming availability then meant a sequential phone call per office, through an IVR and a
hold queue each time. Every one of those steps sat between an injured client and the treatment
that both their recovery and the case value depend on.

**What it cost, on deliberately conservative numbers.** A personal injury client's treatment
runs for months, so one case is not one appointment. Across the life of a case the team picks a
provider and phones around roughly **6 times**, and drafts around **30 booking emails**, most of
them repeat appointments with a provider already chosen. The firm takes in **~100–125 new cases
a week**, and in steady state a department finishes about as many cases as it starts, so weekly
volume is per-case volume times intake:

| | |
|---|---|
| New cases per week (firm) | ~100–125 |
| Provider selections per case | ~6 |
| **Provider selections per week** | **~600–750** |
| Searching the directory, per selection | ~15 min |
| **Weekly staff time on provider search** | **~150–190 hours** |
| Availability calls per selection | ~2, at ~10 min each |
| Availability calls per week | ~1,200–1,500 |
| **Weekly staff time on availability calls** | **~200–250 hours** |
| **Combined, search plus calls** | **~350–440 hours a week** |
| Booking emails drafted per week | ~3,000–3,750 |

One provider selection cost about **35 minutes**: a quarter of an hour finding candidates, then
two ten-minute calls to find out when they could actually be seen. Six of those per case is
around **3.5 hours per case** before a single appointment is booked.

The treatment team is about 65 people, so its weekly capacity is roughly 2,600 hours. Provider
selection was consuming 350 to 440 of them, **13% to 17% of the department's capacity**, or the
equivalent of nine to eleven people doing nothing but scrolling a directory, copy-pasting
addresses into Google Maps, working through phone trees and sitting on hold. None of it required
clinical or legal judgment.

Three things make those numbers conservative rather than favourable. Six selections and two
calls each are the low end of what shadowing showed, against the three-call selections the team
described as typical. The 15 minutes is search only, and has to be, because two calls alone
account for 20. And treatment coordination is not a workflow the firm could decide to do less
of, because the volume is set by how many people were injured and what their doctors
recommended.

<!-- Units confirmed with Lara 2026-08-13: ~6 selection episodes per case, ~2 calls per
selection episode, ~30 booking emails per case. Her "per case" in conversation sometimes meant
"per provider selection", which is what made the calls figure ambiguous; it is settled now, so
do not re-derive these.

The ~15 min per search is also Lara's estimate (2026-08-13), not a stopwatch figure, which is
why the prose says "about".

OPEN, still: the ~100-125 new cases/week is the claims department's measured intake, reused on
Lara's confirmed assumption that treaters pick up the same cases. Every weekly figure above
scales off it, so it is the one to re-check if anything ever looks off. -->

## 4. Solution

An app that ranks providers against the client's address, phones the shortlist with voice AI
agents to get their earliest availability, and drafts the booking email into the coordinator's
own outbox. It lives in Teams, where the team already works.

**Kept fresh in the background, every weekday morning:**

1. **Catalog sync.** A scheduled pull from the case management system refreshes the provider
   catalog: contact details, the do-not-use flag, open and total case counts with that
   provider, and average bill reduction.
2. **Geocoding.** A second scheduled pass turns new or changed addresses into coordinates. A
   provider appears on the map once it has them.

**What a coordinator does:**

3. **Search.** Pick the specialty, enter the client's address. The app returns the **three
   closest providers by driving distance**, plus every provider of that specialty on a map.
   Gold pins for the top picks, blue for other active providers, black for do-not-use.
4. **Compare.** Each provider shows driving distance, average bill reduction, and the firm's
   open and total caseload with it, so the choice is made against the variables the team
   actually weighs.
5. **Check availability.** Select one provider or several. Optionally add a provider that is
   not in the catalog. Optionally ask the agent to confirm the office performs the procedure
   before asking about dates, and attach constraints such as nothing before next Monday or no
   morning slots.
6. **Parallel calls.** Every selected office is phoned **at the same time**. The voice agent
   works the IVR, holds, and asks for the earliest opening for that procedure. **One request
   returns one answer**, once every call in it has finished, however many calls that was.
7. **Book.** Pick the provider from the returned results and enter the matter ID. A flow pulls
   the client and case details from the case management system, an LLM step composes the
   request, and the email lands in the coordinator's **own Outlook drafts**. They review and
   send it. Nothing goes out automatically.

**Two escape hatches.** If the coordinator already knows which provider they want, they can
skip the calls and draft the email straight away. If
the provider they need is not in the catalog, they can add it ad hoc and mix it into a batch
with catalog providers.

**How the do-not-use problem got fixed.** The flag stays in the case management system, so
there is one source of truth and the team keeps managing it where they already manage provider
records. What changed is that ticking it now does something: a do-not-use provider is **never
recommended**, drops to the bottom of the results in its own group, and turns black on the map.
It stays visible on purpose. Hiding it would look tidier and would tell a coordinator nothing
when they went looking for a provider they know exists.

## 5. Architecture

**How the catalog stays fresh and searchable.** Two scheduled jobs mirror and enrich the
provider list, and search combines a cheap coordinate filter with a paid routing call.

```mermaid
flowchart LR
  cms[["Case management system<br/>(system of record)"]]
  treater(["Treatment<br/>coordinator"])

  subgraph sched["Scheduled, weekday mornings"]
    sync["Catalog sync<br/>contacts · do-not-use<br/>caseload · bill reduction"]
    geo["Geocoding<br/>via Azure Maps"]
  end

  cat[("Provider catalog<br/>~18k rows")]
  maps["Azure Maps<br/>driving distance"]
  search["Search app"]

  cms -.->|"scheduled pull"| sync
  sync -->|"upsert"| cat
  geo -->|"lat/long"| cat
  cat -->|"specialty filter"| search
  treater --> search
  search -->|"25 nearest by coords"| maps
  maps -->|"driving distance"| search
  search -->|"3 closest + full map"| treater
```

**What one request does.** Steps 1, 7 and 10 are the human ones. Step 5 is the gate that turns
an unbounded number of phone calls into a single answer.

```mermaid
flowchart TB
  s1(["1 · Coordinator selects<br/>providers + constraints"])
  f1["2 · Start availability batch<br/>one call row per provider"]
  v["3 · Voice AI agents (Retell)<br/>N calls placed at once"]
  o(["Provider offices<br/>IVR · hold · earliest opening"])
  f2["4 · Post-call webhook<br/>fires once per call"]
  g{"5 · Every call in<br/>the batch done?"}
  w(["No notification yet.<br/>A retry keeps the batch open"])
  n["6 · One notification,<br/>results ranked in the app"]
  s2(["7 · Coordinator picks a<br/>provider + enters matter ID"])
  f3["8 · Booking email drafter<br/>lookup, compose, draft"]
  out["9 · Draft lands in the<br/>requester's Outlook"]
  s3(["10 · Coordinator reviews<br/>and sends it"])

  calls[("Availability calls<br/>1 row per call, grouped by batch ID")]
  cms[["Case management system"]]

  s1 --> f1
  f1 ==> v
  v <--> o
  v -->|"webhook"| f2
  f2 --> g
  g -->|"no, one is still on hold"| w
  g -->|"yes"| n
  n --> s2 --> f3 --> out --> s3
  f1 -.->|"create"| calls
  f2 -.->|"write outcome"| calls
  f3 -.->|"client + case lookup"| cms
```

### Key decisions and tradeoffs

| Decision | Why | What I gave up |
|---|---|---|
| **Driving distance, not straight-line** | Straight-line distance is free and ranks wrong. A provider two miles away across a river or with no crossing for six miles is not the nearest provider, and the coordinator would have caught the error and stopped trusting the tool. | A paid routing call per candidate, and latency in the search. |
| **Shortlist the 25 nearest by coordinates, then ask the routing API for driving distance on those** | Routing every one of ~18,000 providers per search is unaffordable and pointless. Coordinate proximity is a cheap, good-enough filter, and driving distance decides the actual ranking. | An edge case where the true best drive sits outside the 25 nearest as the crow flies. |
| **The do-not-use flag stays in the case management system and is shown, not hidden** | One source of truth, managed where the team already manages providers. Showing excluded providers at the bottom in black makes the exclusion legible instead of making a provider mysteriously absent. | The app cannot fix a bad flag in place, and a correction waits for the next morning's sync. |
| **One row per call, grouped by a batch ID, and nothing notifies until every row in the batch is terminal** | A four-provider request that sends four notifications makes the coordinator do the collation. The point of the batch is a single comparison. One request, one answer, however many calls. | A completion gate to get right, and per-call results are invisible until the slowest office is done. |
| **Confirm by phone, book by email** | Firm policy requires the appointment request in writing. Automating the booking call would have produced a step the firm could not use. | Not end-to-end. A human still sends the email. |
| **The draft lands in the requester's own Outlook drafts and is never sent** | The email goes to a treating provider from a named person at the firm, and it commits the client to an appointment. Review costs seconds. | A step that could have been automated stays manual by choice. |
| **Confirmed availability expires after six hours** | Appointment slots go. Booking against a slot that was free this morning produces a wrong email and a call from the provider's office. Expired results have to be reconfirmed. | Coordinators who leave a request overnight have to rerun the calls. |
| **Ad-hoc providers create a call row but never a catalog row** | Staff can reach any provider immediately without anyone typing into the permanent catalog, so the synced catalog stays a faithful mirror of the system of record. | Ad-hoc providers are not reusable. Using one twice means adding it twice. |

### Constraints I built inside

- **The case management system is the system of record and its API is limited.** The provider
  catalog is pulled on a schedule and mirrored, rather than queried live. That is why the app
  is a day-fresh copy and why a do-not-use correction takes effect the next business day.
- **The exclusion problem was organisational.** The design had to make an existing, ignored
  field consequential rather than replace it, or the same drift would have started again in a
  new column.
- **Appointments must be requested in writing.** Shaped the whole back half: confirm by voice,
  commit by email.
- **Non-technical users.** Treatment coordinators, not analysts. The surface is a search box,
  a map, and two buttons.
- **Built inside the firm's existing Microsoft estate**, with access granted by membership of
  an existing security group, the same pattern as the other solutions in this engagement. No
  new logins, no new access model for IT to learn.

### Illustrative excerpt: the batch completion gate

*Redacted, with table and column names replaced. This is the piece worth showing, because it
is what makes an unbounded number of phone calls behave like one request.*

```js
// Post-call webhook. Fires once per completed call, so N times for an N-provider request.
// The coordinator gets exactly one notification, after the last call lands.

const call = await findCallByVoiceCallId(payload.call_id);

if (!reachedAHuman(payload)) {
  // Offices are busy, and a hold queue that times out is not a failed provider.
  if (call.attempts < MAX_ATTEMPTS) {          // MAX_ATTEMPTS = 3
    return placeCallAgain(call);               // row stays pending, no notification
  }
  return markTerminal(call, 'no_human_reached');
}

await markTerminal(call, 'success', {
  earliestAvailability: payload.extracted.earliest_date,
  procedureOffered:     payload.extracted.performs_procedure,
  details:              payload.extracted.notes,
});

// The gate. Every call started together shares a batch ID, so completion is a
// question about siblings, not about this call.
const siblings = await findCallsInBatch(call.batchId);
if (siblings.some(isStillPending)) return;     // someone is still on hold

await notifyRequester(call.batchId, siblings); // one card, all providers, ranked
```

Three things that gate buys. A slow office cannot trigger a premature "here are your results".
A retry is invisible to the coordinator, because a pending row keeps the batch open rather than
reporting a failure. And because the unit of completion is the batch rather than the call, the
same code path serves a one-provider request and a nine-provider one.

The shape is deliberately the same as the FNOL agent's one-row-per-carrier-per-attempt model,
and both share a status option set across the engagement. Ten solutions built by the same team
against the same data platform should not each invent their own vocabulary for "this thing
finished".

### Illustrative excerpt: shortlisting before routing

```js
// Search: specialty is a hard gate, distance is the ranking.
const candidates = await providers.where({
  specialty: chosenSpecialty,
  isActive:  true,
  geocoded:  true,                    // no coordinates, no ranking, no map pin
});

// Cheap first pass. Coordinate distance to pick who is worth a routing call.
const nearest25 = candidates
  .map(p => ({ ...p, crowFlies: haversine(clientCoords, p.coords) }))
  .sort((a, b) => a.crowFlies - b.crowFlies)
  .slice(0, 25);

// Paid second pass, on 25 rows rather than ~18,000.
const routed = await azureMaps.driveTimes(clientCoords, nearest25);

const ranked = [
  ...routed.filter(p => !p.doNotUse).sort(byDrivingDistance),
  ...routed.filter(p =>  p.doNotUse).sort(byDrivingDistance),   // last, always, in black
];
```

## 6. My involvement

**I owned this one end to end.** Nobody asked for it. It came out of shadowing a department to
find out where its time went, and I took it from that observation through to a deployed app:

- the diagnosis, including the shadowing sessions and the finding that an existing unused field
  was the real fix for provider exclusion,
- the data model, the two scheduled jobs that mirror and geocode the provider catalog, and the
  ranking approach that shortlists on coordinates before paying for driving distance,
- the React app, the map, and the search and comparison interface,
- the voice agent and its prompt, the per-call row model, and the batch completion gate that
  turns an unbounded number of calls into one answer,
- the booking-email flow and the decision to stop at a draft rather than send.

**What I did not own: change management.** Training the coordinators and driving adoption were
the client's responsibility by agreement, not an oversight. That boundary matters more than it
sounds, because the one design choice here that depended on human behaviour rather than code was
the do-not-use flag, and making it work required staff to be trained to use it. That training was
somebody else's to deliver, and it happened (see §7).

It also explains the gap in §7. Adoption and measurement sit naturally with whoever runs change
management, so no after-state numbers came back to me. I would negotiate that differently now
(see §8).

<!-- OPEN: minor, worth claiming if true. Did you write the three handover docs this case study
was drawn from (user guide, maintenance runbook, architecture)? The runbook is better than most
internal documentation and it belongs in the list above. I have not asserted it because I do not
know. -->

## 7. Impact

**The before state, from the shadowing sessions:**

| Metric | Before |
|---|---|
| Team size | ~65 people, ~2,600 staff-hours a week of capacity |
| Provider directory size | ~18,000 records, filterable by specialty only |
| Distance information available in the system of record | None. No coordinates, no map, no distance sort |
| How distance was determined | Two addresses copied into Google Maps, once per candidate provider |
| Which providers to avoid | An unused checkbox, plus individual staff memory |
| Provider selections per week | ~600–750, at ~35 min each |
| Weekly staff time on provider search | ~150–190 hours (~15 min per selection) |
| Weekly staff time on availability calls | ~200–250 hours (~1,200–1,500 calls at ~10 min) |
| **Combined weekly cost of choosing providers** | **~350–440 hours, 13% to 17% of the department's capacity** |
| Booking emails drafted per week | ~3,000–3,750 |
| Confirming availability for three providers | Three sequential calls, ~10 min each, ~30 min of wall clock |

**What the design changes, mechanically.** Two separate effects, worth keeping apart.

*The human comes off the phone.* The 200 to 250 weekly hours of availability calling were spent
on hold and in phone trees, and the agent absorbs essentially all of it. What replaces it is
reading a results card, which is seconds rather than minutes. This is the larger effect and it
does not depend on concurrency at all.

*The wall clock stops being a sum.* Calls in a request are placed at once, so two ten-minute
calls become one ten-minute wait and three become one, because the wall clock is the slowest
call rather than the total. Since concurrency has no practical ceiling here, checking six
providers costs about what checking one costs, which changes what a coordinator will bother to
do. Phoning six offices to find the earliest opening was previously an hour, so nobody did it.
Now it is the same ten minutes as phoning two, and a wider search is free.

*Ranking replaces looking.* The 150 to 190 weekly hours of search were spent reading a list and
operating a second browser tab to answer a question the data could answer directly. A specialty
and an address now return the three closest providers by driving distance, with the rest on a
map. Fifteen minutes becomes the time it takes to type an address.

**The one outcome I can report, and it is the one I care most about.** The do-not-use checkbox
is now **the only way to mark a provider as do-not-use, staff were trained on it, and it has
become the single source of truth.** Before, the field existed and was ignored, and which
providers to avoid lived in individual coordinators' heads.

That is the test of the design choice in §2. The tempting fix was a new exclusion flag inside
the new app, which would have been faster to build and would have failed the same way, because
the original field was not ignored for lack of a better field. It was ignored because ticking it
changed nothing. Making it consequential, and leaving it where the team already managed provider
records, is why it is now maintained. A design that depends on people doing something they were
not doing before is a risk, and this is the version of that risk that paid off.

**What was not measured, stated plainly.** Nothing was measured after rollout. There is no
count of appointments booked through the app, no agent reach rate, no change in
time-to-first-appointment, and no adoption figure. The before-state numbers above come from
shadowing and from the estimates in §3; everything after that is mechanical, meaning it follows
from how the system works rather than from an observation of it working. Adoption tracking sits
with change management, which was the client's by agreement, so those numbers were never mine to
collect.

I would rather publish that gap than fill it. A portfolio with an invented percentage in it is
worth less than one with an honest hole, because the reader cannot tell which of your numbers
are real once they catch a single one that is not.

## 8. What I'd do differently

- **The deploy can silently ship the previous build.** The build script type-checks and then
  bundles, so a type error leaves the output directory untouched, and the push step still
  reports success and uploads the stale bundle. The runbook tells the operator to read the
  build output for errors before pushing, which is a documented workaround for something the
  pipeline should refuse to do. The push should fail on a failed type-check.
- **Search is specialty-gated, so a provider with no specialty is unreachable.** The row exists,
  it syncs, it geocodes, and no search can return it. That is a silent data trap rather than a
  visible error, and it should surface as a data-quality warning instead of living in a
  troubleshooting table.
- **The "draft ready" notification depends on the user having installed the bot.** The card
  cannot reach a coordinator who has not added the agent's Teams app, and the fix is an
  install policy. The draft is in Outlook either way, so nothing is lost, but a coordinator
  waiting for a card that will never arrive has no way to know that.
- **The specialty mapping refresh is manual.** It runs on demand rather than on a schedule,
  which means the lookup that gates all search depends on someone remembering. It should be on
  the same weekday recurrence as the other two jobs.
- **I built the thing and then could not tell you what it did.** Change management was the
  client's by agreement, and I treated measurement as part of that, so no after-state numbers
  came back. Quantifying the before state was the whole basis for building this, and I did not
  arrange to quantify the after state. Next time the instrumentation goes in the build, not the
  handover: log every search, call and draft with a timestamp, so the usage data exists whether
  or not anyone is assigned to look at it. Owning the diagnosis and not the verification is
  half a job.
- <!-- OPEN: yours, on the technical side. Anything that actually frustrated you, or that you
  would rebuild? The Azure Maps cost model, the map component, the 25-provider cap, the
  six-hour expiry window, the scheduled-mirror approach to the provider catalog? -->

---

<details>
<summary>Evidence</summary>

<!-- Candidates, all needing a redaction pass first:
     - The search screen: ranked provider list beside the map, gold/blue/black pins. Best
       single artifact, since the whole diagnosis is "they could not see this". Blur provider
       names and the client address, and use a demo address rather than a real client's.
     - A do-not-use provider sitting at the bottom of the results in black.
     - The availability results view for a multi-provider batch, showing one request with
       several returned dates.
     - A drafted booking email with everything identifying redacted.
     Check every image for: firm name, provider names, client names and addresses, matter IDs,
     dates of loss, dollar figures, PHI. Provider names are the new risk here that FNOL did
     not have, since a real clinic name is identifying even though it is not the client. -->

Not yet added.

</details>
