CCR ADVANCED FRONTEND — ANALYST INTELLIGENCE WORKSPACE / PHASE UI-1

Work ONLY in the CURRENT CCR repository.

This task replaces the current CCR frontend visual architecture.

Do NOT modify:
- canonical CCR business data
- relationship semantics
- evidence thresholds
- research-orchestrator logic
- source-policy rules
- protected Phase-2 data
- production relationship states

Do NOT invent:
- relationships
- exposure totals
- active/inactive client states
- AI insights
- events
- risk scores

Use real CCR data only.

Minimal read-only backend/API additions are allowed ONLY when required to expose
already-existing CCR database information to the frontend.

Do not create new business facts.

==================================================
READ FIRST
==================================================

Read these reports if present:

backend/data/CCR_CANONICAL_DATA_MODEL_REPORT.md
backend/data/CCR_RELATIONSHIP_UNIVERSE_MODEL_REPORT.md
backend/data/CCR_RELATIONSHIP_EVIDENCE_PATH_POLICY.md
backend/data/CCR_RESEARCH_ORCHESTRATOR_REPORT.md
backend/data/CCR_EXTERNAL_PROVIDER_READINESS_REPORT.md
backend/data/CCR_RELATIONSHIP_PILOT_SEMANTICS_REPORT.md
backend/data/CCR_3M_RELATIONSHIP_PILOT_REPORT.md

Inspect:

frontend/
backend/app/
existing CCR APIs
existing CSS/design system
countries.geojson
current client/network/research/review pages

Preserve working routes and backend functionality where practical.

==================================================
OBJECTIVE
==================================================

Transform the existing CCR application into an advanced institutional
relationship-intelligence workspace.

The product should visually feel like:

credit intelligence
+
entity intelligence
+
relationship graph
+
global exposure monitor
+
research workstation

NOT:

a collection of simple form pages.

The selected CCR entity should become the persistent analytical context across
the application.

==================================================
1. GLOBAL APPLICATION SHELL
==================================================

Replace the current page-centric shell with:

LEFT NAVIGATION
+
TOP COMMAND BAR
+
MAIN ANALYTICAL CANVAS
+
RIGHT INTELLIGENCE INSPECTOR
+
OPTIONAL BOTTOM DETAIL DRAWER

Desktop-first.

Target primary desktop widths:

1440px
1600px
1920px

Still remain usable on smaller laptop screens.

Layout concept:

┌────────────────────────────────────────────────────────────────────────┐
│ CCR RELATIONSHIP INTELLIGENCE        Search / Command       AI Analyst │
├────────────┬───────────────────────────────────────┬───────────────────┤
│ NAVIGATION │                                       │                   │
│            │          ANALYTICAL CANVAS            │    INSPECTOR      │
│ Portfolio  │                                       │                   │
│ Entities   │                                       │ Evidence / Entity │
│ Network    │                                       │ Research / Event  │
│ Radar      │                                       │                   │
│ Events     │                                       │                   │
│ Research   │                                       │                   │
│ Evidence   │                                       │                   │
│ Review     │                                       │                   │
├────────────┴───────────────────────────────────────┴───────────────────┤
│ Contextual bottom drawer: exposure / evidence / history / research     │
└────────────────────────────────────────────────────────────────────────┘

==================================================
2. VISUAL LANGUAGE
==================================================

Build a sophisticated analytical visual system.

Use:

clean institutional typography
dense but readable information hierarchy
thin separators
subtle card elevation
controlled use of color
compact badges
micro-labels
high information density

Avoid:

giant empty cards
marketing-style landing pages
oversized slogans
decorative gradients
cartoon icons
excessive rounded cards
large unused white space

The workspace should resemble a serious professional analytical platform.

Use a neutral light analytical theme initially.

Prepare CSS tokens for future dark mode.

Create shared design tokens for:

background
surface
surface-elevated
border
text-primary
text-secondary
muted
positive
warning
negative
information
selected
evidence-backed
proposal
candidate
external-entity

==================================================
3. LEFT NAVIGATION
==================================================

Replace current navigation with:

01 Portfolio
02 Entities
03 Network
04 Radar
05 Events
06 Research
07 Evidence
08 Review

At bottom:

Provider Status
System Status

Provider status should display current actual CCR state:

GLEIF
SEC
Web
AI

Never fabricate READY states.

Read existing provider-status API/data.

==================================================
4. TOP COMMAND BAR
==================================================

Create a persistent top bar containing:

CCR logo/title

global entity search

current selected entity chip

country filter if applicable

research status indicator

provider health indicator

AI Analyst button

command palette trigger

Example:

[ CCR INTELLIGENCE ]

Search entity / GFCID / CAGID / LEI / CIK / ticker...

[ 3M CO × ]

Providers  ● GLEIF  ● SEC  ○ WEB

[ AI Analyst ]

Keyboard shortcut:

Ctrl/Cmd + K

for command/entity search.

==================================================
5. GLOBAL ENTITY CONTEXT
==================================================

Create a central SelectedEntityContext.

When a user chooses a client/entity:

entity remains selected while navigating between:

Portfolio
Entity
Network
Radar
Events
Research
Evidence
Review

Persist entity key in URL.

Example:

?entity=MASTER:0000426083

Reloading the browser should preserve selected entity.

Do not use GFCID alone as universal entity identity if the canonical entity_key
is available.

==================================================
6. PORTFOLIO PAGE
==================================================

Rebuild Overview into:

PORTFOLIO INTELLIGENCE

Top KPI strip should use real values.

Possible cards:

CCR Subjects
Canonical Entities
Exposure Records
Research-Ready
Entities with LEI
Relationship Proposals
Evidence Documents
Open Research Gaps

Do not display monetary totals because exposure amount semantics remain unknown.

Display:

Exposure Records

not:

Total Exposure $

unless semantics become governed later.

==================================================
7. GLOBAL WORLD MAP
==================================================

Use the existing countries.geojson.

Build a proper recognizable interactive world map.

Do NOT use abstract polygon approximations.

Map must support analytical layer switching.

Initial available layers:

CCR Population
Identity Coverage
Research Readiness
Evidence Coverage

Future disabled layers:

Relationships
Events
Stress

If a layer has no populated production data, show it disabled or with a
clear zero-data state.

Country representation:

fill intensity or bubbles based on CCR subject count.

Hover:

country
CCR subjects
canonical entities if available
LEI coverage
research-ready count

Click:

select country and filter the rest of the page.

Map controls:

[ Population ]
[ Identity ]
[ Research ]
[ Evidence ]

Add:

Reset view
Fit data
Legend

==================================================
8. PORTFOLIO ANALYTICS PANELS
==================================================

Below the map create compact analytical panels.

A. COUNTRY CONCENTRATION

Top countries by CCR subject count.

Horizontal bars.

B. INDUSTRY / RMI MIX

Use real available classification.

Do not infer taxonomy equivalence where it is unresolved.

C. IDENTITY COVERAGE

Breakdown:

master-backed
deterministic match
CCR-only
review required

D. IDENTIFIER COVERAGE

LEI
CIK
ticker
domain where verified

E. RESEARCH READINESS

ready
discovery required
review blocked
unknown

Use actual CCR data.

==================================================
9. ENTITY PAGE
==================================================

Selecting an entity opens a rich analytical entity workspace.

Header:

3M CO

badges:

CCR SUBJECT
MASTER BACKED
HIGH IDENTITY
RESEARCH ELIGIBLE

Identifiers:

GFCID
CAGID
LEI
CIK
Ticker
Country

Use compact copy buttons.

Do not overload header.

==================================================
10. ENTITY SUMMARY STRIP
==================================================

Create cards:

Exposure Records
Identifiers
Relationship Observations
Research Claims
Evidence Documents
Research Runs
Events

Use actual counts.

Zero is valid.

Example:

RELATIONSHIP OBSERVATIONS
0
No evidence-backed production observations

Do not hide zeros.

==================================================
11. ENTITY TABS
==================================================

Entity workspace tabs:

Intelligence
Exposure
Relationships
Evidence
Research
Timeline

INTELLIGENCE should be default.

==================================================
12. INTELLIGENCE VIEW
==================================================

Create a three-column analytical composition.

LEFT:

Entity profile
identity
country
industry
CCR membership

CENTER:

Relationship Radar placeholder/data visualization

RIGHT:

Research & evidence state

Relationship Radar dimensions:

Corporate Structure
Supply
Customer
Finance
Technology
Infrastructure
Services
Strategic

Important:

Radar does NOT mean numeric risk score.

Each dimension should show states such as:

EVIDENCED
PROPOSAL
RESEARCHING
CANDIDATE
NO DATA

Never fabricate percentages.

==================================================
13. EXPOSURE VIEW
==================================================

Display actual source exposure/facility rows.

Show:

facility ID
facility type
facility description
direct exposure field
contingent exposure field
other raw amount fields

BUT clearly label:

Units / currency / additivity not governed

Do not aggregate these fields into misleading totals.

Provide:

row count
facility count
facility-type distribution
raw exposure distribution only where technically safe

==================================================
14. RELATIONSHIPS VIEW
==================================================

Prepare the full relationship interface now even if production relationship
count is zero.

Show three separate layers:

EVIDENCE-BACKED
PROPOSALS
RESEARCH CANDIDATES

Never merge them.

Relationship row/card:

related entity
relationship type
direction
state
source tier
evidence count
freshness
review state

If none exist:

"No evidence-backed relationships currently stored."

Do NOT create demo edges.

==================================================
15. RIGHT INTELLIGENCE INSPECTOR
==================================================

Create a persistent contextual inspector.

Default tabs:

ENTITY
EVIDENCE
RESEARCH
SOURCE

When entity selected:

identity details

When relationship selected:

relationship type
direction
status
counterparty
evidence documents
evidence snippets
source tier
research run

When map country selected:

country analytics

When research run selected:

run status
plan
providers
outcome

Inspector width:

approximately 330–400px desktop.

Resizable if practical.

==================================================
16. RESEARCH STATUS EXPERIENCE
==================================================

Build a compact reusable research-status component.

Statuses:

READY
RUNNING
PROPOSAL_PENDING_REVIEW
INSUFFICIENT_EVIDENCE
NOT_FOUND
PROVIDER_UNAVAILABLE
IDENTITY_UNRESOLVED
RELATED_ENTITY_UNRESOLVED
DIRECTION_UNRESOLVED
CONFLICT_REVIEW_REQUIRED

Each should have:

consistent badge
tooltip
plain-language description

Do not use generic red "error" for governed research outcomes such as
NOT_FOUND.

==================================================
17. EMPTY STATES
==================================================

Empty states must be analytical.

BAD:

"No data."

GOOD:

"No evidence-backed relationships currently stored.
145 correlation candidates exist in the separate research-candidate layer."

Use actual counts when available.

Never imply candidate = relationship.

==================================================
18. AI ANALYST SURFACE
==================================================

Create the visual shell for an AI Analyst.

Do NOT yet make autonomous calls.

Button:

AI Analyst

opens right-side expandable panel.

Suggested future prompts:

Explain this entity
Summarize available evidence
What relationship gaps remain?
Which research questions are unresolved?
Explain this network
Assess this event against this entity

For now:

wire only to existing safe AI endpoint if already present.

If no production AI endpoint exists:

show controlled "AI integration not configured" state.

Do not fake responses.

==================================================
19. RESEARCH ACTION
==================================================

Entity header should contain:

[ Research Entity ]

Click opens modal/drawer with:

relationship type
research scope
source strategy
minimum tier
research instructions

This should use the existing Research Orchestrator API if available.

Do not create a second research system.

No automatic research on page load.

==================================================
20. PERFORMANCE
==================================================

Do not load all 16k+ entities into the browser.

Use backend pagination/search.

Entity search should debounce.

Tables should paginate or virtualize.

Map country aggregation should come from compact aggregate API data.

Avoid expensive full-graph fetches.

==================================================
21. API CONTRACT
==================================================

Inspect existing APIs first.

Reuse them.

If needed, add ONLY read-oriented endpoints such as:

GET /api/portfolio/summary

GET /api/portfolio/geography

GET /api/entities/search

GET /api/entities/{entity_key}

GET /api/entities/{entity_key}/exposure

GET /api/entities/{entity_key}/relationships

GET /api/entities/{entity_key}/research

GET /api/entities/{entity_key}/evidence

GET /api/providers/status

Do not duplicate existing routes.

Do not change database schema in this task unless absolutely unavoidable.

==================================================
22. FRONTEND ARCHITECTURE
==================================================

Refactor into reusable components.

Suggested structure:

frontend/src/
  app/
  components/
    shell/
    navigation/
    command/
    map/
    charts/
    entity/
    relationship/
    research/
    evidence/
    inspector/
    tables/
    badges/
  pages/
    PortfolioPage
    EntityPage
    NetworkPage
    RadarPage
    EventsPage
    ResearchPage
    EvidencePage
    ReviewPage
  state/
  api/
  styles/

Follow current project framework conventions if structure differs.

Do not rewrite the entire frontend framework unnecessarily.

==================================================
23. UX DETAILS
==================================================

Add:

loading skeletons
error boundaries
tooltips
keyboard focus states
sticky table headers
sortable tables
copy identifier action
breadcrumbs
URL-preserved filters
responsive inspector behavior

Use subtle motion only for:

drawer open/close
selection
map zoom
panel transitions

No flashy animation.

==================================================
24. DATA TRUTH BANNER
==================================================

Add a small non-intrusive data-governance banner where relevant:

"Relationship candidates are research leads, not evidence."

On exposure view:

"Exposure amount units and additive semantics are not yet governed."

On research:

"External research runs only after explicit user action."

These should be compact, not giant warnings.

==================================================
25. REMOVE CURRENT WEAK DESIGN
==================================================

Replace:

large marketing headers
excess blank white space
simple stacked cards
form-like main pages
decorative placeholder network pages

with analytical layouts.

Keep only reusable useful components.

Do not preserve poor layout merely for visual backward compatibility.

==================================================
26. FIRST-PASS ROUTES
==================================================

Fully implement in this phase:

Portfolio
Entities / Entity Intelligence

Build functional shell/placeholders connected to actual state for:

Network
Radar
Events
Research
Evidence
Review

Do not attempt the advanced graph/event engines in this task.

Those come in UI-2.

==================================================
27. VALIDATION
==================================================

Run:

frontend TypeScript validation
frontend production build
backend regression
API smoke tests

Test:

portfolio loads
map renders
country click works
entity search works
entity selection persists
entity page loads
tabs work
exposure loads
relationship zero-state is correct
research state loads
provider pulse loads
inspector works

No fake relationship data.

==================================================
28. REPORT
==================================================

Create:

backend/data/CCR_ADVANCED_FRONTEND_UI1_REPORT.md

Include:

UI architecture
routes
components
API reuse/additions
screens implemented
data sources
performance approach
known limitations
validation results

==================================================
FINAL RESPONSE
==================================================

CCR ADVANCED FRONTEND UI-1: PASS / FAIL

PORTFOLIO:
PASS / FAIL

WORLD MAP:
PASS / FAIL

ENTITY SEARCH:
PASS / FAIL

ENTITY INTELLIGENCE:
PASS / FAIL

EXPOSURE VIEW:
PASS / FAIL

RELATIONSHIP LAYERS:
PASS / FAIL

INTELLIGENCE INSPECTOR:
PASS / FAIL

RESEARCH ACTION:
PASS / FAIL

AI ANALYST SHELL:
PASS / FAIL

REAL CCR DATA ONLY:
PASS / FAIL

FAKE RELATIONSHIPS:
0 / FAIL

FRONTEND BUILD:
PASS / FAIL

BACKEND REGRESSION:
passed:
failed:
errors:

REPORT:
backend/data/CCR_ADVANCED_FRONTEND_UI1_REPORT.md

Also provide the local URL to open the redesigned CCR application.

STOP.
