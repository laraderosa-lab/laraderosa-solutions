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
[§7 of the main case study](./README.md#7-impact): the pre-signed case vendor whose settlement
values came out below what the firm pays per lead, the 40% of rejections caused by leads for
services the firm does not offer, and the roughly one lead in ten that is invalid.

<!-- OPEN: the screenshots. You mentioned a PDF with altered pictures. It did not survive into
this session, since uploads never do, so please re-attach it and I will build this section
around it: one redacted image per page above, each captioned with the question that page
answers.
Redaction check before anything is committed: firm name, staff names in slicers, client names
and contact details, referral partner and vendor names, campaign names containing the city or
state, tracking phone numbers, real spend and settlement figures.
Note from the firm-ops dashboard work: blur in a client-supplied export is not redaction.
Previous "pre-anonymized" PDFs still carried legible names under partial blur. Substitute at
source or crop to aggregates. -->

## Design decisions

The two that shaped the whole reporting layer sit in the main case study, along with the
Skyvia connector definition that feeds the warehouse: Power BI over Lawmatics' native
dashboards, because ROI per source is a joined question and native reporting can only see its
own system, and replicating into a warehouse rather than pointing the BI tool at the API,
which is paginated at 100 records a page and rate limited to ten requests a second.

<!-- OPEN: the decisions specific to the dashboard itself, which I do not have:
     - how ROI is defined when a PI case settles months or years after the spend that bought it
     - whether dropped cases sit in the denominator
     - whether the default view opens at source or at campaign level
     - the refresh cadence the client sees, and whether that is a Skyvia scheduling constraint
     - did this fully replace the V1 Lawmatics-native dashboard, or do both still run?
     - the Clio half: custom connector too, or does Skyvia ship one for Clio? -->

## Evidence

<!-- Redacted screenshots from the PDF, once re-attached. Assets belong in ./assets/. -->

Not yet added.
