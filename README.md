CCR ADVANCED UI RECONSTRUCTION — STAGE 2
PORTFOLIO + GLOBAL MAP + ENTITY INTELLIGENCE

Continue in the CURRENT CCR repository.

Stage 1 is the visual/workspace foundation.

Do not revert it.

This is an IMPLEMENTATION task.
Do not stop after describing the design.

Keep working until the screens below are implemented and validated.

No fabricated data.

==================================================
1. PORTFOLIO PAGE
==================================================

Completely reconstruct Portfolio.

It must become the main command center.

Top area:

PORTFOLIO INTELLIGENCE

Compact snapshot line:
snapshot date / data freshness / provider posture

KPI row:

CCR SUBJECTS
CANONICAL ENTITIES
EXPOSURE RECORDS
RESEARCH CANDIDATES
EVIDENCE DOCUMENTS
RELATIONSHIP OBSERVATIONS

Use actual values.

Zero must display as zero.

Do not make zero disappear.

==================================================
2. WORLD MAP AS PRIMARY VISUAL
==================================================

The existing world map must become the dominant analytical visualization.

Use:
frontend/public/countries.geojson

Make it visually rich.

Dark basemap.

Country borders subtle.

Data layer colors should glow slightly but remain professional.

Layers:

POPULATION
IDENTITY
RESEARCH
EVIDENCE

If later supported:
RELATIONSHIPS
EVENTS
STRESS

but keep disabled when data unavailable.

==================================================
3. MAP INTERACTIONS
==================================================

Hover:

country
CCR entity count
share of CCR population
LEI coverage
research-ready count
evidence-document count if available

Click:

select country.

Country selection must:

highlight country
filter lower analytical panels
update inspector

Double click or button:
zoom to country

Controls:

Reset
Fit Data
Zoom +
Zoom -
Layer selector
Legend

==================================================
4. MAP VISUALIZATION
==================================================

Do not make every country the same pale color.

Use proper quantitative intensity.

Use CCR population as default.

When Identity selected:
visualize identifier/LEI coverage where defensible.

When Research selected:
visualize research readiness/count.

When Evidence selected:
visualize source-backed evidence count where available.

No fabricated relationship arcs.

==================================================
5. PORTFOLIO ANALYTICS BELOW MAP
==================================================

Use compact 2x2 / 3x2 analytical panels.

A. COUNTRY CONCENTRATION

bar chart:
top 10 countries

B. ENTITY CLASS

MASTER_BACKED
DETERMINISTIC_MASTER_MATCH
CCR_ONLY_ENTITY
REVIEW_REQUIRED
EXTERNAL_ENTITY if present

C. IDENTIFIER COVERAGE

LEI
CIK
Ticker
Domain

D. RESEARCH POSTURE

candidates
plans
claims
evidence
unresolved

E. INDUSTRY / CLASSIFICATION

Use actual available values only.

F. SOURCE / PROVIDER POSTURE

SEC
GLEIF
Web
AI

==================================================
6. ENTITIES PAGE
==================================================

Current table is functional but visually weak.

Rebuild it as dense institutional entity search.

Header:

ENTITIES

Subhead:
Universal canonical entity registry.

Filter bar:

Search
Entity class
Country
Identity quality
CCR membership
Research state

Add clear filters button.

Table:

ENTITY
CLASS
COUNTRY
IDENTIFIERS
CCR
EXPOSURE ROWS
RESEARCH
EVIDENCE
RELATIONSHIPS

Use pagination/server query.

Use compact status indicators.

Clicking row:
select entity + navigate to intelligence.

==================================================
7. ENTITY INTELLIGENCE PAGE
==================================================

Create a dedicated entity intelligence route/page.

Do not rely only on the right inspector.

Suggested route:

/entity/:entityKey

Header:

LEGAL NAME
Ticker if available
Country
Entity class
CCR membership
Identity quality

Actions:

Research Entity
Open Network
Open Evidence
AI Analyst

==================================================
8. ENTITY INTELLIGENCE HEADER METRICS
==================================================

Compact metrics:

Exposure Records
Research Candidates
Research Plans
Evidence Documents
Relationship Observations
Events

Actual values only.

==================================================
9. ENTITY INTELLIGENCE TABS
==================================================

INTELLIGENCE
EXPOSURE
RELATIONSHIPS
EVIDENCE
RESEARCH
TIMELINE

==================================================
10. INTELLIGENCE TAB
==================================================

Build a serious summary surface.

LEFT:

ENTITY PROFILE

legal name
country
industry/RMI
entity class
CCR membership
identity quality
research eligibility

Identifiers:

GFCID
CAGID
LEI
CIK
Ticker
Domain

CENTER:

RELATIONSHIP RADAR SUMMARY

Corporate
Supply
Customer
Finance
Technology
Infrastructure
Services
Strategic

For each:
EVIDENCED
PROPOSAL
RESEARCHING
CANDIDATE
NO DATA

No percentages.

RIGHT:

RESEARCH POSTURE

provider readiness
latest run
plans
claims
evidence
unresolved questions
review requirements

==================================================
11. EXPOSURE TAB
==================================================

Make source rows useful.

Summary:

record count
distinct facility IDs
facility types
direct-exposure rows
contingent-exposure rows

Table:

facility ID
facility type
facility description
direct exposure
contingent exposure
OSUC
outstanding
total exposure

Do not aggregate monetary values.

Banner:

"Source amount units, currency and additive semantics are not governed."

==================================================
12. RESPONSIVE BEHAVIOR
==================================================

At 1920:
map + side analytics can coexist.

At 1440:
map remains dominant.

At laptop widths:
inspector may overlay rather than permanently consume width.

==================================================
13. ACCEPTANCE
==================================================

Validate:

Portfolio loads.
World map renders.
Country hover works.
Country click filters.
Country selection updates inspector.
Entity search works.
Entity filters work.
Entity page opens.
Entity tabs work.
Exposure rows load.
No fake relationship/event/risk data.
Build passes.
Backend regression remains green.

Create:

backend/data/CCR_ADVANCED_FRONTEND_UI2_STAGE2_REPORT.md

FINAL RESPONSE:

CCR UI2 STAGE 2: PASS / FAIL
PORTFOLIO: PASS / FAIL
WORLD MAP: PASS / FAIL
COUNTRY INTERACTION: PASS / FAIL
ENTITY REGISTRY: PASS / FAIL
ENTITY INTELLIGENCE: PASS / FAIL
EXPOSURE: PASS / FAIL
REAL DATA ONLY: PASS / FAIL
