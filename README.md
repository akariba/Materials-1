LENDING — COMPLETE FRONTEND REPLACEMENT + WORKING ANALYTICS POC

The current Lending UI is rejected.

DO NOT refine it.
DO NOT preserve its visual design.
DO NOT continue incrementally from its page layout.

Replace the Lending frontend with a new analytics-first Lending Relationship
Intelligence POC using the already validated backend.

Proceed autonomously through the complete scope.
Do not stop for intermediate approval.
Stop only for a genuine external blocker.

==================================================
1. PRIMARY OBJECTIVE
==================================================

Deliver ONE working final Lending application at:

/lending

It must combine:

1. Portfolio analytics
2. Exposure/materiality analytics
3. CAM coverage analytics
4. Sector concentration
5. Geographic portfolio analytics
6. Client ranking and drilldown
7. Relationship network analytics
8. Relationship/evidence explorer
9. External SEC/R2D2 intelligence
10. Review queue

The UI must use REAL backend data.

No mock business data.

==================================================
2. CURRENT UI IS NOT A BASELINE
==================================================

The existing Lending screens are NOT visually approved.

Current examples include:

- old /lending relationship dashboard
- current /portfolio/lending shell
- cards saying NOT AVAILABLE
- old senior-management layout
- old filter layout
- old visual hierarchy

Do not preserve those layouts.

You may reuse useful technical components, hooks, API clients or graph
libraries, but redesign the actual Lending UX.

==================================================
3. FIX THE 502 FIRST
==================================================

Before rebuilding the UI, identify and resolve the current:

Portfolio analytics unavailable
502 Bad Gateway

Check:

- actual running backend URL/port
- frontend API base URL
- Vite proxy
- backend router mounting
- frontend route path
- old/legacy API client usage
- startup/import errors
- whether frontend is calling the same backend application where the
  Portfolio API passed validation

Test the Portfolio API directly before touching presentation.

The running API must reconcile to:

Portfolio clients = 2,484
CAM-covered = 1,698
Without CAM = 786
Exactly 1 CAM = 928
Exactly 2 CAMs = 770
Reported OSUC ≈ $349.27B
CAM-covered OSUC ≈ $259.93B
Canonical CAM relationships = 13
Review-required relationships = 28

If those values do not reconcile:

STOP.
Do not compensate in frontend.
Report the backend mismatch.

If they reconcile:
continue immediately into the full frontend replacement.

==================================================
4. HARD DATA BOUNDARIES
==================================================

DO NOT:

- change V1
- change V2
- change V3
- rerun CAM extraction
- change the 13 canonical CAM relationships
- change the 28 review-required relationships
- modify CAM/PDF/DOCX source files
- modify source workbooks
- modify Portfolio API calculations
- modify external-overlay governance
- modify Stylus preset
- modify SEC/R2D2 configuration
- trigger external research automatically
- modify CCR
- modify RPR

Small read-only API compatibility fixes are permitted only if genuinely
necessary to make the existing validated backend reachable.

==================================================
5. FINAL ROUTE OWNERSHIP
==================================================

The final application must live at:

/lending

Do not leave the user choosing between:

/lending
and
/portfolio/lending

After the new UI passes:

- /lending = final Lending Relationship Intelligence application
- /portfolio/lending may redirect to /lending if useful
- remove legacy Lending UI from active route ownership

Do not affect CCR routes.

==================================================
6. PRODUCT DESIGN
==================================================

This is an ANALYTICS WORKBENCH.

It must not look like:

- a collection of empty cards
- a technical admin page
- a developer tool
- a static report
- a giant table
- a giant graph
- a mockup

Visual style:

- white/light background
- subtle pale-blue accents
- dark navy/charcoal text
- restrained borders
- clean institutional look
- compact analytical density
- generous enough whitespace
- professional senior-management / credit-risk quality
- no logos for companies
- no decorative images
- no unnecessary gradients
- no oversized cards

==================================================
7. NAVIGATION
==================================================

Use a compact left navigation.

Pages:

Overview
Clients
Network
Relationship Explorer
External Research
Review Queue

Keep navigation simple.

Do not put entities/companies in sidebar navigation.

==================================================
8. OVERVIEW — ANALYTICS FIRST
==================================================

This page must answer within seconds:

What portfolio am I looking at?
How large is it?
How much CAM coverage do we have?
Where is exposure concentrated?
Which clients matter most?
Where are the relationships?
What requires attention?

Build the page in this analytical flow:

PORTFOLIO SCALE
↓
CAM COVERAGE
↓
EXPOSURE CONCENTRATION
↓
SECTOR DISTRIBUTION
↓
GEOGRAPHIC DISTRIBUTION
↓
CLIENT RANKING
↓
RELATIONSHIP NETWORK PREVIEW
↓
REVIEW / ATTENTION

--------------------------------------------------
8A. TOP METRICS
--------------------------------------------------

Use real backend values.

Show compact metrics:

Portfolio in Scope
Reported OSUC
CAM Coverage
CAM-Covered OSUC
Canonical CAM Relationships
Review Required

Do not hardcode values.

Do not call the 2,484 population the full Lending universe.

Use:

CAM Priority Portfolio
or
Current Portfolio Scope

==================================================
9. CAM COVERAGE ANALYTICS
==================================================

Required visual analytics:

With CAM vs Without CAM

1 CAM vs 2 CAMs

Client coverage %

OSUC coverage %

Use a clean stacked bar, donut, or equivalent.

Clicking a segment should drill/filter Clients.

==================================================
10. EXPOSURE ANALYTICS
==================================================

Create exposure/materiality analytics based on:

Reported OSUC
Portfolio Share
Exposure Rank
Percentile if deterministically calculable
Cumulative portfolio share if deterministically calculable

Do NOT invent a risk score.

Show:

Top clients by Reported OSUC

Columns:

Rank
Client
CAGID
Reported OSUC
Portfolio %
Sector
CAM Status
Relationship Count / Coverage

Click client -> Client Detail.

Add useful deterministic concentration statistics such as:

Top 10 share
Top 20 share

only if calculable from API data.

==================================================
11. SECTOR ANALYTICS
==================================================

Required:

ranked horizontal bar chart.

Toggle:

Reported OSUC
Client Count

Sort descending.

Click sector -> Clients page with that sector filter.

If CAM coverage by sector is available, provide a secondary view:

CAM Coverage by Sector

Do not invent sectors.

==================================================
12. GEOGRAPHIC ANALYTICS
==================================================

Build a geographic portfolio view if validated country data exists.

Required analytics where supported:

Client count by country
Reported OSUC by country

Provide toggle:

Exposure
Client Count

Click a country -> filtered Clients list.

Use an interactive geographic map or an equivalent meaningful geographic
visualization.

Do not invent coordinates.

Do not infer countries from company names.

If only country names are available, use a library/data representation that
can map countries deterministically.

If geography is genuinely unavailable:
show a small controlled empty state, not a giant empty card.

==================================================
13. CLIENTS PAGE
==================================================

Provide full searchable portfolio population.

Search:

Client Name
CAGID

Filters where real data supports:

Sector
Country
CAM Yes/No
CAM Count
Risk Rating
Credit Classification
Relationship Coverage

Default sort:

Reported OSUC descending

Columns:

Client
CAGID
Sector
Country
Reported OSUC
Portfolio %
CAM
CAM Count
Risk Rating
Credit Classification
Relationships

Use pagination or virtualization.

Do not render all 2,484 rows simultaneously.

==================================================
14. CLIENT DETAIL
==================================================

Click a client and open a proper analytical profile.

Header:

Client Name
CAGID
Sector
Country
Risk Rating
Credit Classification

Materiality row:

Reported OSUC
Portfolio Share
Exposure Rank
CAM Status
CAM Count

Then sections/tabs:

Overview
Relationships
External Intelligence
Evidence

Overview should summarize:

- exposure
- portfolio rank
- CAM status
- canonical relationships
- review-required relationships
- external proposals/corroborations

==================================================
15. RELATIONSHIP NETWORK PREVIEW
==================================================

Overview must include a small network preview.

Do NOT render hundreds of nodes.

Default:
maximum approximately 8–12 useful evidence-backed nodes.

Show only real relationships.

Button:

Open Full Network

==================================================
16. FULL NETWORK PAGE
==================================================

This is a major analytical page.

Layout:

LEFT:
filters and lenses

CENTER:
large relationship graph

RIGHT:
selected node/edge inspector

BOTTOM:
relationship records table if useful

Required graph capabilities:

pan
zoom
fit
search
node selection
edge selection
evidence drilldown

Do not render full 2,484-client universe automatically.

==================================================
17. NETWORK LENSES
==================================================

One primary lens active at a time.

Working lenses:

CAM
Exposure
Hidden / Indirect
External SEC/Web

CAM:
authoritative canonical V3 relationships.

Exposure:
node size can represent Reported OSUC.

Hidden / Indirect:
only backend-supported evidence-backed paths.

External:
show supplemental external intelligence over CAM.

Prepare disabled future lenses:

Market & News
AI Ecosystem
Potential Impact

Label them:

Future capability

Do NOT fake those datasets.

==================================================
18. GRAPH SEMANTICS
==================================================

CAM canonical:
solid line

CAM review required:
dashed line

External proposal:
visibly supplemental dashed/dotted line

Conflict:
clear review styling

Historical:
dotted when backend supports it

Do not rely only on color.

Show legend.

==================================================
19. NETWORK ENTITY INSPECTOR
==================================================

Node selection should show:

Entity name
CAGID
Sector
Country
Reported OSUC
Portfolio Share
CAM status
Relationship counts

Edge selection should show:

Subject
Related Entity
Relationship Type
Direction
Connectivity
State
CAM / External source layer
Confidence
Evidence Count
Review State

Button:

View Evidence

==================================================
20. RELATIONSHIP EXPLORER
==================================================

Create a serious searchable/filterable relationship table.

Columns:

Subject
Related Entity
Relationship Type
Direction
Connectivity
State
Source Layer
Confidence
Evidence Count
Review State

Clearly distinguish:

CAM
CAM Review
External
CAM + External Corroboration

Do not expose old 32,957 extraction candidates as relationships.

==================================================
21. RELATIONSHIP DETAIL
==================================================

Present:

Subject
→ relationship type →
Related Entity

Then:

Direction
Connectivity
State
Confidence
Source layer
Review status

Evidence must be separated:

CAM Evidence

External Evidence

CAM evidence should show where available:

document
page/location
excerpt

External evidence should show:

SEC / Web
publisher
title
date
filing type
source reference
excerpt
source tier
admissibility
backend normalized confidence

==================================================
22. EXTERNAL RESEARCH PAGE
==================================================

Use exactly six runtime inputs:

SubjectEntity
RelatedEntity
RelationshipScope
SourceChannels
ResearchInstruction
AsOfDate

Convenience modes:

Web Research
= R2D2_WEB

SEC Research
= SEC_FILING

Deep Validation
= both

Execution is ONLY from:

Run External Research

Never auto-run on:

page load
client selection
network selection
refresh
reconnect
route change
cache miss
browser reload

==================================================
23. EXTERNAL RESULT EXPERIENCE
==================================================

Do not make JSON the primary interface.

Show:

Relationship
Classification
Backend Confidence
CAM Comparison
Evidence Count
Review Requirement

Governed states:

CAM_CORROBORATION
EXTERNAL_PROPOSAL_PENDING_REVIEW
CONFLICT_REVIEW_REQUIRED
NO_EXTERNAL_CORROBORATION
MENTION_ONLY
INSUFFICIENT_EVIDENCE

Raw JSON may be under:

Technical Details

==================================================
24. REVIEW QUEUE
==================================================

Tabs:

CAM Review
External Proposals
Conflicts

CAM Review:
existing 28 review-required relationships.

External:
external proposals pending review.

Conflicts:
external/CAM conflicts.

Columns:

Entity Pair
Relationship
Source
Reason
Confidence
Evidence Count
Reported OSUC context where applicable
Review State

Do not allow accidental CAM canonical mutation.

==================================================
25. DATA QUALITY / EMPTY STATES
==================================================

Do not build large blank cards saying NOT AVAILABLE.

If a feature has no data:

- hide it when appropriate
or
- show a compact inline empty state.

The page must still look finished.

Do not create dead sections purely because they were mentioned in an old UI.

==================================================
26. ANALYTICS DRILLDOWN
==================================================

Every important visualization should do something:

CAM segment -> filtered Clients
Sector bar -> filtered Clients
Country map -> filtered Clients
Exposure ranking -> Client Detail
Network node -> Client Detail / Entity Detail
Network edge -> Relationship Detail
Review count -> Review Queue

Avoid decorative charts.

==================================================
27. DATA SOURCE RULES
==================================================

All business numbers must come from backend APIs.

NO hardcoded:

2484
1698
786
928
770
349.27B
259.93B
13
28

Those may appear in tests/expected validations,
but never as frontend business constants.

==================================================
28. OSUC LABELING
==================================================

Use:

Reported OSUC

Do not use:

OSUC Net of Hedges

unless backend explicitly provides governed proof.

Do not invent an as-of date.

==================================================
29. PERFORMANCE
==================================================

Desktop POC target:

1366x768
1440x900
1920x1080

Use pagination / virtualization for portfolio tables.

Limit network size.

Avoid rendering thousands of elements.

No browser freezing.

==================================================
30. ROUTE TRANSITION
==================================================

After new UI works:

/lending
must become the final new application.

/portfolio/lending
may redirect to /lending.

Legacy Lending UI must no longer be the active user-facing Lending screen.

Do not delete code recklessly if dependencies remain.
Just remove it from route ownership.

==================================================
31. TEST EVERYTHING
==================================================

Verify:

/lending opens new application

No 502

Overview values reconcile to API

CAM coverage visualization works

Sector analytics works

Geographic analytics works if data available

Client ranking works

Client search works

Client filters work

Client detail works

Network works

Network node click works

Network edge click works

Relationship Explorer works

Evidence drilldown works

External cached result works

External explicit Run button is wired

No external call occurs automatically

Review Queue works

No mock data

==================================================
32. REGRESSION PROTECTION
==================================================

At end verify:

V1 unchanged
V2 unchanged
V3 unchanged

V3 canonical = 13
V3 review-required = 28
V3 unresolved subjects = 0

Portfolio API unchanged

External overlay backend unchanged

Stylus preset unchanged

CCR unchanged

RPR unchanged

==================================================
33. VALIDATION REPORT
==================================================

Create:

backend/data/LENDING_FINAL_POC_UI_VALIDATION_REPORT.md

Report:

API CONNECTION
direct portfolio API PASS/FAIL
frontend connection PASS/FAIL
502 resolved YES/NO

ROUTES
/lending PASS/FAIL
legacy route replaced YES/NO
/portfolio/lending redirect/status

OVERVIEW
portfolio count
reported OSUC
CAM count
CAM coverage
sector analytics PASS/FAIL
geography PASS/FAIL
exposure ranking PASS/FAIL
network preview PASS/FAIL

CLIENTS
search
filters
sorting
pagination
detail drilldown

NETWORK
CAM
Exposure
Hidden
External
node selection
edge selection
evidence drilldown

RELATIONSHIPS
canonical count
review count
external count
explorer PASS/FAIL

EXTERNAL
cache read
explicit run control
automatic calls = 0

REVIEW
CAM review
external proposal
conflict views

REGRESSION
V1 unchanged
V2 unchanged
V3 unchanged
Portfolio API unchanged
External Overlay unchanged
Stylus unchanged
CCR untouched
RPR untouched

==================================================
34. FINAL RESPONSE
==================================================

Return:

LENDING FINAL POC UI: PASS / FAIL

502 RESOLVED:
YES / NO

Final Lending route:
/lending

Portfolio clients:
X

Reported OSUC:
X

CAM-covered clients:
X

Canonical CAM relationships:
X

Review-required CAM relationships:
X

Overview analytics:
PASS / FAIL

CAM coverage analytics:
PASS / FAIL

Sector analytics:
PASS / FAIL

Geographic analytics:
PASS / FAIL / NOT AVAILABLE

Exposure ranking:
PASS / FAIL

Clients:
PASS / FAIL

Client Detail:
PASS / FAIL

Network:
PASS / FAIL

Relationship Explorer:
PASS / FAIL

External Research:
PASS / FAIL

Review Queue:
PASS / FAIL

Automatic external executions:
X

No mock business data:
PASS / FAIL

V1 unchanged:
PASS / FAIL

V2 unchanged:
PASS / FAIL

V3 unchanged:
PASS / FAIL

Portfolio API unchanged:
PASS / FAIL

External Overlay unchanged:
PASS / FAIL

Stylus preset unchanged:
PASS / FAIL

CCR untouched:
PASS / FAIL

RPR untouched:
PASS / FAIL

Validation report:
<path>

READY FOR USER POC TEST:
YES / NO

If NO, list only genuine blockers.

Then STOP.

START NOW.
