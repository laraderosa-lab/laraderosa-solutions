# The Marketing ROI Dashboard

Companion to [Marketing Attribution](./README.md). That case study covers the five layers that
had to be rebuilt before any number was true. This one covers the surface built on top of them.

## Why this piece carries the project

Everything upstream of the dashboard is invisible. A rebuilt taxonomy, an ad account
restructured under protest, remapped history, a cost model, settled value flowing back from the
case management system: none of it changes a decision on its own. It changes decisions when the
owner opens one screen and sees which spend earns.

It is also where half-fixed attribution would have shown. The people reading this dashboard know
their own channels, so a per-campaign number that contradicts what they already believe gets
noticed in the first week. Once one number is wrong the whole thing stops being opened, and the
firm goes back to the agency's monthly report on impressions and clicks.

## The five pages

Power BI over an hourly BigQuery warehouse fed from both Lawmatics and Clio Manage. Once the
warehouse exists the marginal cost of the next question is a query rather than a project, which
is why it runs to five pages rather than the one the project was scoped around.

- **Intake overview**, from Lawmatics. The funnel from total leads through qualified to hired,
  with conversion and qualification rates, split by practice area, plus lead volume by month
  and by day of week.
- **Source performance**, the page the attribution work exists to make true. Leads, hires,
  conversion rate and case value by source, by campaign and by ad group, with referral
  partners broken out individually.
- **Intake detail.** Consultations booked, attended, missed and paid, and a full breakdown of
  **why** rejected leads were rejected, separating leads the firm turned down from leads that
  turned the firm down.
- **Matters overview**, from Clio. Open cases by practice area, pipeline funnels per practice
  area, median days to close, and an aging list of the oldest open files, each deep-linking
  back into Clio so the dashboard is a way into the work rather than a read-only artifact.
- **Financials.** Estimated against actual case value, accrued and cash positions by month,
  and average settlement value by lead source, which is the join that turns attribution into a
  buying decision.

Three of the findings these pages produced in the first pass are in
[§7 of the main case study](./README.md#7-impact): the pre-signed case vendor whose cases are
mostly dropped after signing, the 40% of rejections caused by leads for services the firm does
not offer, and the roughly one lead in ten that is invalid.

<!-- OPEN: the Clio pages. The V1 walkthrough covered the Lawmatics pages and the financials,
and Clio was still hypothetical at that point ("same thing if we ever did a dashboard for
Clio"). Were the two Clio-fed pages yours, or did they land after the account moved to a
colleague? Section 6 of the main case study currently claims the whole dashboard. -->

## What the numbers had to mean

A report over a CRM inherits the CRM's definitions unless someone decides otherwise. Two of
those decisions changed what the client saw.

**Conversion rate excludes anything still in intake.** A lead that has not resolved yet is not a
lead the firm failed to sign. Counting it as one, which is what the native report did, understates
conversion by however many cases happen to be in flight on the day you look. Excluding intake
means the dashboard's headline conversion rate deliberately disagrees with the number the same
people had been reading in the CRM, so the first walkthrough spent time on why.

**Qualification rate depends on what counts as a lead at all.** Wrong numbers, current clients
calling about an open case, and enquiries for work the firm does not do all sit in the
denominator and hold the rate down. The owner had a benchmark in mind that the firm's own rate
came nowhere near, and part of that gap was definitional rather than performance.

**A target only means something next to what the source costs.** The client wanted goal lines on
the dashboard, per channel. Word of mouth converts on its own and costs nothing to run, so
holding it to the same conversion target as paid search says nothing about either. Rather than
ship goal lines against numbers nobody had seen yet, targets were left until the client had used
the real data for a while and could set ones that meant something.

## Design decisions

- **Everything cross-filters, and every aggregate drills to the matters underneath it.** Click a
  rejection reason and the sources that produced it appear. Click again and the individual
  matters are listed, each linking straight into its record in the CRM. The alternative is
  finding a number you distrust and then going to search for the cases by hand.
- **Show the practice areas the firm does not take.** Lead volume is split by practice area
  including the ones the firm rejects on sight, because that view is the only place unmet demand
  shows up. Another firm looked at the same page and found a steady stream of medical
  malpractice enquiries it had been turning away without ever counting.
- **Scheduled extracts, not just a screen.** Weekly and monthly cuts go out to the people who
  need them on a schedule. The report they replace was a staff member exporting from the CRM and
  doing the arithmetic in a spreadsheet every week.
- **Fold the financial reporting in rather than leaving it where it was.** The firm's financial
  report already existed in Looker Studio, and moving it onto the same model made settlement
  value joinable to lead source, which is what makes ROI per source a real number instead of two
  reports side by side. Gross and net sit on one page here rather than on two.
- **Ship V1 with a known hole.** Personal injury case value was missing at launch, because the
  settled-value backflow from Clio was not finished. Waiting would have delayed everything else
  the client could already use, and the gap was named out loud rather than left to be discovered.
- **Power BI Pro per viewer.** Every person who opens the dashboard needs a licence. For a firm
  of this size that is a real line item, and it is the kind of thing that has to be said before
  launch rather than after.
- **No AI layer, for now.** The owner asked for an assistant he could ask for trends and
  recommendations. It was deferred on the grounds that an AI has nothing to flag until the
  targets exist, since without them it can only report that a number moved.

<!-- OPEN: still needed for this page.
  - The screenshots. You mentioned a PDF with altered pictures. It did not survive into this
    session, since uploads never do, so please re-attach it and I will build an evidence
    section around it: one redacted image per page above, each captioned with the question that
    page answers.
    Redaction check before anything is committed: firm name, staff names in slicers, client
    names and contact details, referral partner and vendor names, campaign names containing the
    city or state, tracking phone numbers, real spend and settlement figures.
    Note from the firm-ops dashboard work: blur in a client-supplied export is not redaction.
    Previous "pre-anonymized" PDFs still carried legible names under partial blur. Substitute at
    source or crop to aggregates.
  - How ROI is defined when a PI case settles months or years after the spend that bought it.
  - Whether the default view opens at source or at campaign level.
  - The refresh cadence the client sees, and whether that is a Skyvia scheduling constraint.
  - The Clio half: custom connector too, or does Skyvia ship one for Clio?
  - The marketing dashboard you had already built natively in Lawmatics and shown the team.
    Did this replace it outright, or do both still run? Worth a sentence either way, since
    "I built the cheap version first and then outgrew it" is a better story than not
    mentioning it. -->

<!-- OPEN: sourced from the V1 walkthrough call of 2026-03-23 (Fireflies), verified against the
transcript rather than the AI summary. Everything in "What the numbers had to mean" and "Design
decisions" is from that call. Nothing here comes from the later biweeklies, which a colleague
ran after the account transitioned. -->

## Evidence

<!-- Redacted screenshots from the PDF, once re-attached. Assets belong in ./assets/. -->

Not yet added.
