CCR RELATIONSHIP & EVENT INTELLIGENCE
FULL WINDOWS ANALYTICAL PLATFORM REBUILD
WORLD MAP + HELIX AI + STYLUS + EVENT INTELLIGENCE
END-TO-END IMPLEMENTATION

You are working inside the CURRENT CCR repository opened in VSCode on Windows.

Proceed autonomously through the complete scope.

Do not stop for intermediate approval.

The objective is to turn the currently working CCR correlation POC into a
coherent analytical intelligence product.

This is NOT a cosmetic patch.

Reconstruct the frontend and connect it end-to-end to the existing CCR data,
local correlation engine, approved Helix AI runtime, relationship research,
event analysis and evidence architecture.

The application must run locally on Windows first.

Unix deployment comes later.

==================================================
0. NON-NEGOTIABLE RULES
==================================================

CCR ONLY.

Do not modify or depend directly on unrelated repositories.

Do not change source datasets:

Customer_latest.parquet
thousandClients.csv
backend/data/ccr_clients.sqlite3

Preserve:

backend/data/ccr_relationship_intelligence.sqlite3

and all validated canonical Phase-2 business data.

Do not fabricate:

relationships
evidence
exposure units
financial amounts
parents
suppliers
customers
event impacts
theme scores
news
AI results

A research candidate is NOT a relationship.

An AI inference is NOT evidence.

External evidence and AI analysis must always retain provenance.

Do not use a public OpenAI/Anthropic/Google credential.

Use the approved internal Helix / enterprise AI mechanism available on this
workstation.

Never print, log, persist, return to frontend, write to JSON, write to SQLite,
or write to disk any bearer token.

Do not disable TLS verification.

Do not bypass corporate certificate policy.

==================================================
1. READ THE CURRENT IMPLEMENTATION FIRST
==================================================

Before modifying code inspect:

backend/
backend/app/
backend/app/core/
backend/app/routers/
backend/config/
backend/data/
backend/scripts/
backend/tests/

frontend/
frontend/src/
frontend/public/
frontend/package.json
frontend/vite.config.*

Read current Phase reports:

CCR_RELATIONSHIP_PHASE2_FOUNDATION_REPORT.md
CCR_RELATIONSHIP_PHASE3_EXTERNAL_RESEARCH_REPORT.md
CCR_PHASE4A_WINDOWS_LOCAL_POC_REPORT.md
CCR_PHASE4B_LOCAL_CORRELATION_REPORT.md
and any Phase 4B.1 report if present.

Inspect actual code rather than relying only on reports.

Run the current tests before changing anything.

Record baseline counts and Phase-2 fingerprint.

==================================================
2. IMPORTANT MAP ASSET
==================================================

A geographic map file already exists:

frontend/public/countries.geojson

USE THIS FILE.

Do not fetch a world map from the internet.

Do not use online map tiles.

Load the asset at runtime from:

/countries.geojson

Inspect its feature properties and determine which property contains:

ISO alpha-2
ISO alpha-3
country name

Build a deterministic country-code mapping between canonical CCR country data
and the GeoJSON.

Do not guess mappings silently.

Persist a small explicit alias map only for defensible exceptions.

==================================================
3. PRODUCT TO BUILD
==================================================

Product name:

CCR RELATIONSHIP INTELLIGENCE

Subtitle:

Clients · Relationships · Events · Themes · Impact

Primary business question:

"What could affect our CCR clients, through which entities and relationships,
and what evidence supports that conclusion?"

The application must support six interchangeable starting points:

CLIENT
RELATIONSHIP
EVENT
NEWS
THEME
COUNTRY

A selection in one analytical surface should update the others.

==================================================
4. NEW INFORMATION ARCHITECTURE
==================================================

Replace the current primary navigation.

Use:

INTELLIGENCE

01 Command Center
02 World Map
03 Events & News
04 Theme Radar
05 Client 360
06 Relationship Graph
07 Impact Matrix

ANALYSIS

08 AI Analyst
09 Analysis Studio
10 Review & Evidence

SYSTEM

11 Data & Sources

Old local routes may redirect to the appropriate new route.

Never render raw:

404 {"detail":"Not Found"}

in the product.

==================================================
5. STYLUS
==================================================

Use the approved existing Stylus design system/preset available to the current
environment/project.

FIRST inspect the current repository/environment for the established Stylus
preset, tokens, CSS variables, theme package, component wrappers or generated
styles.

Do not invent a second competing theme framework.

Do not alter the approved Stylus base preset itself.

Create CCR-specific composition/layout styles ON TOP of the existing Stylus
tokens.

If the repository contains a Stylus preset/config:

reuse it.

If Stylus is provided through an installed internal UI package:

use that package.

If the exact Stylus implementation cannot be found:

report:

STYLUS_RUNTIME_NOT_FOUND

and preserve current design tokens rather than inventing a fake internal
package.

The UI design should be:

dark navy / graphite analytical canvas
compact
high information density
clear hierarchy
professional financial intelligence software

Status semantics:

selected entity:
cyan

evidence-backed relationship:
blue / teal + solid

external proposal:
violet + solid/dashed

research candidate:
muted gray + dotted

event propagation:
amber/orange + dashed

high impact:
red

medium impact:
amber

lower impact / mitigating:
green

Do not use color as the only status indicator.

==================================================
6. GLOBAL APPLICATION SHELL
==================================================

Top bar:

CCR logo / title

CCR RELATIONSHIP INTELLIGENCE

Global search bar:

"Search client, entity, event, country, theme or paste news..."

Suggestions:

AI Bubble
Taiwan
NVIDIA
interest rates
data centers

These are EXAMPLE search hints only.

Do not hardcode analytical results.

Right side:

As-of date
active context/lens
local/backend state
AI Analyst toggle

Left navigation:

new navigation described above.

Right side:

persistent collapsible AI Analyst drawer.

==================================================
7. COMMAND CENTER
==================================================

The Command Center is the default application route.

Do NOT create giant hero marketing text.

Use a compact analytical layout.

TOP:
KPI ribbon

CENTER LEFT:
large World Map

CENTER RIGHT:
Active Events & Themes

RIGHT DRAWER:
AI Analyst

LOWER LEFT:
Theme Radar

LOWER CENTER:
Relationship Network preview

LOWER RIGHT:
Event Impact Summary

BOTTOM:
Top Impacted CCR Clients

Use REAL backend counts.

Initial KPI examples:

CCR Clients
Exposure Records
Clients with LEI
Research Ready
Evidence-backed Relationships
Research Candidates
Evidence Records

Do not display fake event counts before event data exists.

==================================================
8. WORLD MAP — CORE VISUAL
==================================================

Build a proper interactive SVG/GeoJSON world map using:

frontend/public/countries.geojson

Recommended implementation:

React + d3-geo

or the current visualization library if already present and suitable.

Do not add a huge GIS dependency unnecessarily.

Projection:

geoNaturalEarth1 or another recognizable global projection.

Map modes:

CLIENTS
EVENT IMPACT
THEME EXPOSURE
RELATIONSHIP CONNECTIONS
RESEARCH CANDIDATES

Default:

CLIENTS

Client mode:

country fill = relative CCR population
bubble size = CCR client count

Tooltip:

Country
CCR clients
% of CCR population
top sectors where available
clients with LEI
research-ready clients

Do not show monetary exposure until units are confirmed.

==================================================
9. MAP INTERACTION
==================================================

Clicking a country must create a global analytical context:

selectedCountry

and update:

Client table
Theme Radar
Event Impact
Relationship preview
AI Analyst context

The URL should preserve selection.

Example:

/world-map?country=US

No reload required.

==================================================
10. MAP CONNECTIONS
==================================================

Draw bounded arcs only.

Never draw all relationships globally.

Connection semantics:

solid teal:
evidence-backed relationship

violet:
external proposal

gray dotted:
research candidate

amber dashed:
event transmission

On hover:

source entity
destination entity
connection class
relationship/event type
evidence state

Never make research candidates look confirmed.

==================================================
11. ANALYTICAL CONTEXT STORE
==================================================

Create a central frontend context/store.

It should track:

selectedClient
selectedEntity
selectedRelationship
selectedCandidate
selectedEvent
selectedTheme
selectedCountry
selectedSector
dateWindow
activeLens

Use existing state library if already installed.

Otherwise lightweight React Context/Zustand is acceptable.

Do not introduce Redux unless already present.

All major views consume this shared context.

==================================================
12. CLIENT 360
==================================================

Rebuild client detail as analytical Client 360.

Header:

Legal Name
GFCID
CAGID
Country
Sector
Industry
LEI
Identity Quality

Analytical metrics:

Evidence-backed Relationships
Research Candidates
Relevant Events
Relevant Themes
Evidence Records
Exposure Record Count

Panels:

Relationship Graph
Event Sensitivity
Theme Exposure
Geographic Context
Identifiers / External Identity
Evidence Timeline

Actions:

Run Relationship Analysis
Assess Event
Research Relationship
Ask AI

==================================================
13. RELATIONSHIP GRAPH
==================================================

Make this a primary analytical canvas.

Layout:

LEFT
filters/layers

CENTER
large graph

RIGHT
entity/edge inspector

LEFT controls:

Lens:
Relationship
Event
Theme
Geography
Industry

Layers:

Evidence-backed
External proposals
Research candidates
Event propagation
Indirect paths

Relationship type filters use only actual supported relationship taxonomy.

Graph must be bounded.

No entire 16k-node graph.

==================================================
14. GRAPH SEMANTICS
==================================================

Selected CCR client:
largest cyan node

CCR client:
blue

External entity:
green

Theme:
purple

Event:
amber

Research candidate:
muted gray

Edges:

evidence-backed:
solid

candidate:
dotted

event propagation:
amber dashed

external proposal:
violet

Indirect path:
thin segmented

==================================================
15. GRAPH INSPECTOR
==================================================

For an evidence-backed edge show:

Subject
Related Entity
Relationship Type
Direction
Current/Historical
Source Channel
Source Tier
Evidence Count
Quality
Research Run
Last Updated

Buttons:

View Evidence
Ask AI
Analyze Event Exposure

For a candidate edge show:

RESEARCH CANDIDATE

Candidate Score
Analysis Preset
Top Signal Reasons

Evidence:
NONE

Relationship:
NOT ESTABLISHED

Button:

Research This Pair

==================================================
16. THEME RADAR
==================================================

Create a real analytical scatter plot.

X:
CCR Client Coverage

Y:
Theme Velocity / Change

Bubble size:
related clients / relationship coverage

Bubble outline:
evidence quality

Theme examples that may become supported once evidence exists:

AI Bubble
AI Capital Spending
Data Centers
Semiconductors
Interest Rates
Taiwan
Energy
China
Defense

DO NOT fabricate current scores.

If no theme observations exist yet:

display an empty analytical chart shell with:

NO_THEME_OBSERVATIONS

and allow:

Discover Themes

through AI.

==================================================
17. EVENTS & NEWS
==================================================

Build Event Intelligence as a first-class page.

Top input:

Paste a news headline, event narrative, or scenario.

Examples:

"AI capex spending declines sharply"

"Rates remain higher for longer"

"Earthquake disrupts Taiwan semiconductor production"

"Oil prices rise sharply after geopolitical escalation"

Examples are prompt helpers only.

Workflow:

TEXT
↓
HELIX AI EVENT PARSER
↓
STRUCTURED EVENT
↓
LOCAL CCR MATCHING
↓
RELATIONSHIP TRANSMISSION
↓
CLIENT IMPACT
↓
EVIDENCE / EXPLANATION

==================================================
18. EVENT DATA CONTRACT
==================================================

Create persistent event objects.

Tables such as:

events
event_entities
event_themes
event_countries
event_sectors
event_client_impacts
event_transmission_paths
event_evidence

An event should include:

event_id
title
event_type
event_summary
event_date
as_of_date
horizon
direction
status
created_by
created_at

AI extraction output:

themes
countries
industries
sectors
named_entities
possible transmission_channels

Every extracted item needs:

source:
AI
RULE
USER
EVIDENCE

and confidence/quality metadata where applicable.

==================================================
19. EVENT TYPES
==================================================

Provide configurable event taxonomy:

MACRO_RATES
MACRO_INFLATION
MACRO_GROWTH
AI_CAPEX
AI_VALUATION
TECHNOLOGY
SUPPLY_CHAIN
GEOPOLITICAL
NATURAL_DISASTER
ENERGY
REGULATORY
TRADE_POLICY
FUNDING_LIQUIDITY
CREDIT_EVENT
COMPANY_SPECIFIC
CUSTOM

Taxonomy availability does not assert an event exists.

==================================================
20. EVENT IMPACT ENGINE
==================================================

Do not let AI arbitrarily assign HIGH/MEDIUM/LOW.

Use a two-stage model.

STAGE A — candidate relevance

Use local deterministic information:

country
sector
industry
relationship candidates
evidence-backed relationships
named entity match
theme match

STAGE B — AI explanation

Helix explains the transmission hypothesis using the structured context.

Store separately:

event_relevance_score

and:

ai_assessment

Do not label the numeric relevance score as probability.

==================================================
21. TRANSMISSION PATHS
==================================================

Represent impact paths explicitly.

Example shape:

EVENT
→ Theme
→ Entity
→ Relationship
→ CCR Client

or:

EVENT
→ Country
→ Industry
→ CCR Client

Store each hop.

Never say:

A affects C because A relates to B and B relates to C

unless the underlying hops actually exist.

Display paths visually in:

Map
Graph
Client 360
Impact Matrix
AI Analyst

==================================================
22. IMPACT MATRIX
==================================================

Build a full page.

Rows:
CCR clients

Columns:
selected events/themes

Cells:

HIGH
MEDIUM
LOW
NOT ASSESSED
INSUFFICIENT EVIDENCE

Click a cell to open an Impact Detail drawer.

Drawer:

Client
Event
Impact state
Local relevance score
Transmission channels
Paths
Evidence
AI explanation
Research gaps

Do not populate a state until an assessment has run.

==================================================
23. NEWS ANALYSIS
==================================================

News is not a generic feed.

News should be an event trigger.

Card contract:

Headline
Publisher
Date
Source Tier
Detected Entities
Detected Themes
Countries
Potential CCR Clients
Existing Relationship Paths

Action:

Analyze Impact

Only use approved high-quality Web/news sources when the provider is
configured.

Search snippets alone are not evidence.

==================================================
24. ANALYSIS STUDIO
==================================================

Rename the current AI Create Relationship experience:

ANALYSIS STUDIO

Top-level cards:

Supply Chain Dependency
Technology Dependency
Customer Relationship
Parent / Subsidiary
Investor / Sponsor
Lender / Financing
Strategic Partner
Infrastructure Dependency
Service Provider
Joint Venture
Macro Event
Theme Exposure
News / Event Driven
Custom Analysis

Card shows:

Active status
Source channels
Allowed output types
Last run
Run Analysis
Configure

Configuration is a drawer/modal rather than the main page.

==================================================
25. AI ANALYST
==================================================

Create a persistent right-side AI Analyst.

It must understand current context.

Examples:

"Why is this client exposed?"

"Show me the transmission path."

"Which CCR clients could be affected by higher rates?"

"Explain the relationship between these entities."

"What evidence supports this supplier relationship?"

"Which clients are exposed to the AI bubble?"

"Compare these two clients."

"Summarize latest evidence."

The frontend sends structured context, not just free text.

Context request should include where applicable:

selected client
selected event
selected theme
selected relationship
selected candidate
selected country
selected date window
current filters

==================================================
26. HELIX — APPROVED INTERNAL AI ONLY
==================================================

Use the approved Helix runtime already available on this workstation.

FIRST detect:

helix CLI availability

Run safe/version/help commands.

Do not print tokens while diagnosing.

Inspect current project/environment for:

llm_gateway
R2D2
Helix helpers
approved certificate configuration
approved model environment variables

Reuse the approved enterprise authentication mechanism.

The previously proven token acquisition pattern is:

helix auth access-token print -a

BUT:

verify the installed CLI contract before depending on it.

Do not assume undocumented flags.

Do not persist its output.

Do not print it.

Do not place tokens in .env.

Do not send tokens to frontend.

==================================================
27. HELIX TOKEN MANAGER
==================================================

Create one centralized backend token manager.

Preferred module concept:

backend/app/core/helix_auth.py

Responsibilities:

acquire approved Helix access token

hold token ONLY in process memory

track acquisition timestamp

serialize refresh under a lock

refresh proactively

force refresh after auth failure

never log token

never persist token

never return token to API

Required functions conceptually:

get_token()

refresh_token(force=False)

invalidate_token()

get_safe_status()

The token manager must be safe under concurrent AI requests.

==================================================
28. 20-MINUTE TOKEN REFRESH
==================================================

The requested proactive refresh interval is:

20 minutes = 1200 seconds.

Implement configuration:

CCR_HELIX_REFRESH_SECONDS=1200

However:

do not blindly refresh a still-valid token if the installed Helix/runtime
already manages lifecycle differently.

The backend must:

1. inspect actual Helix token behavior;
2. use the approved acquisition mechanism;
3. reacquire at or before configured refresh interval where appropriate;
4. always force reacquisition after 401/403 authentication failure;
5. retry the AI request at most once after auth refresh.

Never enter an infinite auth retry loop.

==================================================
29. WINDOWS BATCH STARTER
==================================================

Create:

run_ccr_windows.bat

It should:

- locate repository root relative to the BAT file
- activate current project .venv if present
- set only NON-SECRET runtime configuration
- set CCR_HELIX_REFRESH_SECONDS=1200
- start the backend
- start the frontend
- start the optional safe Helix session keepalive if needed
- never contain a token
- never echo a token
- never redirect token output to a file

No user-specific absolute C:\ path.

Use project-relative paths.

==================================================
30. OPTIONAL HELIX KEEPALIVE BATCH
==================================================

If and ONLY IF live workstation testing proves that Helix CLI session refresh
is required independently of backend in-memory refresh, create:

scripts/helix_keepalive.bat

Use a loop:

REFRESH
→ wait 1200 seconds
→ REFRESH
→ repeat

But the refresh operation MUST use an approved Helix command.

Do NOT invent a scope/auth command.

Determine the valid command from:

helix --help
helix auth --help
existing approved internal code/configuration

If the safe approved command is confirmed to be equivalent to:

helix auth access-token print -a

its output MUST be discarded, never logged:

> NUL

The purpose is session maintenance only.

The backend still owns application token caching.

If Helix itself already performs refresh automatically:

DO NOT create unnecessary keepalive logic.

Report:

KEEPALIVE_NOT_REQUIRED

==================================================
31. HELIX HEALTH STATUS
==================================================

Expose safe backend endpoint:

GET /api/ai/status

Return only:

configured
helix_cli_available
authenticated
token_age_seconds
refresh_interval_seconds
model_provider
model_name
last_success
last_error_category

Never return:

token
authorization header
secret path
certificate content

==================================================
32. AI GATEWAY
==================================================

Create one CCR AI gateway abstraction.

Example:

CCRHelixAI

Methods:

parse_event()
analyze_event()
explain_client()
explain_relationship()
explain_candidate()
discover_themes()
summarize_evidence()
answer_context_question()

Use structured JSON/Pydantic contracts.

Do not pass around untyped model text when structured state is required.

==================================================
33. AI FAILURE BEHAVIOR
==================================================

AI unavailable must NOT break the rest of the platform.

States:

AI_READY
AUTH_REQUIRED
AUTH_REFRESHING
AI_UNAVAILABLE
TIMEOUT
MODEL_ERROR
INVALID_RESPONSE

Local CCR:

Map
Client 360
correlation
network
candidate generation

must continue to work without AI.

No silent fake fallback.

==================================================
34. AI EVENT PARSER CONTRACT
==================================================

Use structured output.

Input:

event text
as-of date
optional horizon

Output:

title
summary
event_type
direction
horizon
themes[]
countries[]
sectors[]
industries[]
named_entities[]
transmission_channels[]
uncertainties[]

AI must be instructed:

return UNKNOWN rather than inventing facts.

Entity extraction must subsequently resolve against canonical CCR identities.

==================================================
35. AI ANALYST RESPONSE CONTRACT
==================================================

Output:

answer
key_findings[]
transmission_paths[]
supporting_evidence_ids[]
research_gaps[]
assumptions[]
quality
model_metadata

AI must not cite evidence IDs that were not provided in its context.

==================================================
36. RELATIONSHIP RESEARCH
==================================================

From any:

candidate edge
client
entity pair
event path

user can click:

Research Relationship

Research drawer:

Subject
Related Entity
Question
Analysis preset
Source channels
As-of date
Instructions

Explicit button:

RUN RESEARCH

No execution before that click.

==================================================
37. EXTERNAL SOURCES
==================================================

Preserve existing source-policy hierarchy.

Use:

GLEIF
SEC
approved high-quality Web/news

Do not make providers required for application startup.

Provider state appears in:

Data & Sources

not as a dominant feature of Command Center.

==================================================
38. DATA & SOURCES PAGE
==================================================

Display:

CCR Master
CCR Exposure Extract
Canonical CCR database
GLEIF
SEC
Web / News
Helix AI

For each:

configured
coverage
connectivity
cache
last success
last error

Technical diagnostics belong here.

==================================================
39. REVIEW & EVIDENCE
==================================================

Tabs:

Confirmed Relationships
External Proposals
Research Candidates
Conflicts
Event Assessments
Evidence

Evidence detail:

publisher
channel
title
filing type
date
excerpt
source tier
admissibility
retrieved at
research run

No raw token or sensitive headers.

==================================================
40. COMMAND CENTER AI PANEL
==================================================

Persistent AI Analyst on right.

Default when no selection:

"Ask about clients, relationships, events, themes or countries."

Suggested actions:

Which clients could be affected by higher rates?

Show clients exposed to AI infrastructure.

Explain current relationship candidates.

Analyze a news headline.

When context selected:

suggest context-specific questions.

==================================================
41. COMMAND CENTER ACTIVE EVENTS PANEL
==================================================

Once event assessments exist show:

event title
impact state
affected client count
trend / recency
themes

Do not hardcode:

AI Bubble
Rates Higher for Longer
Taiwan

unless the user created/analyzed those events.

Before events exist show:

"No events assessed yet"

button:

Analyze Event

==================================================
42. EVENT IMPACT MAP
==================================================

When an event is selected:

map changes from Client mode to Event Impact.

Country fill/bubble derived from assessed CCR clients.

Side summary:

potentially relevant clients
high
medium
lower
insufficient evidence

Map arcs:

only actual stored transmission paths

No fake routes.

==================================================
43. PERFORMANCE
==================================================

Target:

initial Command Center < 2 seconds locally after backend ready

client searches < 500ms typical

local candidate run < 2 seconds typical

map rendering should aggregate countries

graph defaults <= 50 nodes

AI calls are asynchronous.

Do not block the browser while AI runs.

==================================================
44. AI JOB EXECUTION
==================================================

For potentially long Helix calls create background jobs.

Pattern:

POST
→ job id

GET job
→ status/result

Frontend polls safely.

Statuses:

QUEUED
RUNNING
COMPLETED
FAILED
CANCELLED

Do not create uncontrolled concurrency.

Provide configurable global semaphore.

==================================================
45. AI OBSERVABILITY
==================================================

Log safely:

request id
job id
AI operation
model
start
end
duration
status
input character count
output character count
token-refresh event BOOLEAN
retry count

Never log:

bearer token
Authorization header
certificate
confidential full prompts by default

==================================================
46. CACHE
==================================================

Separate caches:

AI result cache
provider cache
token cache

AI explanation cache key should include:

operation
entity/event identity
as-of date
relevant evidence version
prompt/config version

Do not return stale result when underlying evidence changed.

==================================================
47. GLOBAL SEARCH
==================================================

Global input classification:

CLIENT
COUNTRY
THEME
EVENT
NEWS_TEXT
RELATIONSHIP_QUESTION

Simple identifiers/names can route deterministically.

Long narrative text can route to Helix Event Parser.

Do not call AI for obvious exact client lookup.

==================================================
48. ROUTING RECONSTRUCTION
==================================================

Implement robust frontend routes.

Suggested:

/
→ /command-center

/command-center
/world-map
/events
/themes
/client/:clientKey
/graph
/impact
/ai
/analysis
/review
/data-sources

Use a proper router.

Do not continue fragile handwritten hash routing if that is the cause of the
current raw 404 behavior.

Preserve deep linking.

Client keys must be URL encoded safely.

==================================================
49. ERROR BOUNDARIES
==================================================

Every page requires:

loading
empty
error
ready

No raw backend response as screen body.

404:

"Page or analytical object not found"

500:

"Analysis service error"

AI error:

"AI analysis unavailable — local analytics remain available"

==================================================
50. MAP ACCEPTANCE TEST
==================================================

Using countries.geojson prove:

GeoJSON loads locally

no internet map request

all renderable canonical country codes reconcile or are reported

world geography visibly recognizable

US / UK / JP / etc positions correct

country client counts reconcile

click filtering works

selected country updates AI context

event mode works after a test event

==================================================
51. HELIX ACCEPTANCE TEST
==================================================

Test the LIVE approved Helix runtime.

Required:

helix CLI detected

authentication available

one small structured AI call succeeds

token is not printed

token is not stored in database

token is not written to .env

token is not visible in frontend/network payload

safe status endpoint works

Then simulate/invalidate auth and prove:

cache invalidates
token reacquired
request retries once
request succeeds or returns governed auth failure

==================================================
52. 20-MINUTE REFRESH ACCEPTANCE
==================================================

Do not wait 20 real minutes for unit tests.

Parameterize refresh interval.

Test mode:

CCR_HELIX_REFRESH_SECONDS=5

Prove:

initial acquisition
refresh after interval
concurrent calls cause only one refresh
token never logged

Production/local default:

1200 seconds.

Also verify:

401 causes immediate forced refresh independent of interval.

==================================================
53. BATCH ACCEPTANCE
==================================================

Double-click/run:

run_ccr_windows.bat

Expected:

backend starts
frontend starts
non-secret environment configured
Helix integration initializes
browser can load application

If a keepalive script was proven necessary:

it starts minimized/separately

and does not expose credentials.

Closing application should not leave uncontrolled infinite child processes.

Provide:

stop_ccr_windows.bat

if needed.

==================================================
54. STYLUS ACCEPTANCE
==================================================

Report:

Stylus source/preset found at:
<actual path/package>

Stylus base modified:
NO

CCR components using Stylus:
<count/components>

If unavailable:

STYLUS_RUNTIME_NOT_FOUND

Do not falsely claim Stylus integration.

==================================================
55. END-TO-END ANALYTICAL DEMO
==================================================

Use REAL CCR client data.

Do not hardcode famous companies merely to create attractive output.

Demonstrate:

FLOW A — CLIENT

Search actual client
→ Client 360
→ Generate local relationship candidates
→ open graph
→ inspect candidate
→ Ask AI to explain why candidate was returned

FLOW B — EVENT

Enter:

"Interest rates remain materially higher for longer."

→ Helix parses event
→ local candidate impact engine selects relevant clients from available
country/sector/industry/context
→ AI explains plausible transmission channels
→ results appear on world map
→ Impact Matrix populated

Important:

if available local data is insufficient to claim true impact:

mark:

RESEARCH_REQUIRED
or
INSUFFICIENT_EVIDENCE

Do not pretend model output is fact.

FLOW C — RELATIONSHIP

Select a research candidate
→ Research Relationship drawer
→ run only if provider available
→ evidence appears
→ relationship remains proposal/review until governance requirements pass

FLOW D — AI ANALYST

Ask:

"Which CCR clients appear most relevant to the selected event and why?"

AI answer must use the current context and cite internal result/evidence IDs.

==================================================
56. TESTS
==================================================

Preserve all existing tests.

Add tests for:

GeoJSON loading

country aggregation

country-code normalization

map cross-filtering

new router/deep links

encoded client keys

Client 360

graph boundedness

event persistence

event parsing schema

impact candidate logic

transmission paths

Impact Matrix

Helix token manager

token locking

token refresh

401 refresh

no token logging

AI structured response validation

AI timeout

AI invalid JSON

AI context propagation

Analysis Studio

Review & Evidence

no automatic external research

no fake relationship promotion

Phase-2 fingerprint unchanged

source files unchanged

==================================================
57. PLAYWRIGHT / BROWSER ACCEPTANCE
==================================================

If Playwright is available, automate real browser workflow.

Viewport:

1600x1000 or similar analyst workstation.

Capture:

01_command_center.png
02_world_map.png
03_events_news.png
04_event_impact_map.png
05_theme_radar.png
06_client_360.png
07_relationship_graph.png
08_impact_matrix.png
09_ai_analyst.png
10_analysis_studio.png
11_review_evidence.png
12_data_sources.png

Console errors:

0

Unhandled 404:

0

HTTP 500:

0

==================================================
58. REPORT
==================================================

Create:

backend/data/CCR_FULL_ANALYTICAL_PLATFORM_REPORT.md

Include:

Architecture
Stylus integration
World map
Countries GeoJSON
CCR data reconciliation
Routes
Client 360
Relationship Graph
Event engine
Theme Radar
Impact Matrix
AI Analyst
Helix integration
Helix authentication
20-minute refresh
Windows batch startup
External research
Tests
Browser acceptance
Performance
Known limitations

Never put tokens or sensitive authentication values in report.

==================================================
59. FINAL RESPONSE FORMAT
==================================================

Return exactly:

CCR FULL ANALYTICAL PLATFORM: PASS / FAIL

APPLICATION
Frontend:
Backend:
Windows starter:

STYLUS
Found:
Source:
Base preset modified: NO / FAIL

WORLD MAP
countries.geojson loaded:
Offline:
Countries rendered:
CCR countries reconciled:
Cross-filtering:
Event impact mode:
Relationship arcs:

CLIENT 360
PASS / FAIL

RELATIONSHIP GRAPH
PASS / FAIL

EVENT INTELLIGENCE
Event parser:
Event persistence:
Impact candidate engine:
Transmission paths:
Impact map:
Impact Matrix:

THEME RADAR
PASS / FAIL

AI ANALYST
Helix connected:
Model:
Structured output:
Context aware:
Failure handling:

HELIX AUTH
CLI detected:
Approved auth reused:
Token persisted to disk: 0 / FAIL
Token exposed to frontend: 0 / FAIL
Token printed/logged: 0 / FAIL
Refresh interval:
401 forced refresh:
Concurrent refresh lock:

WINDOWS BATCH
run_ccr_windows.bat:
20-minute refresh:
stop script:
Secrets embedded: 0 / FAIL

EXTERNAL RESEARCH
GLEIF:
SEC:
Web/News:
Explicit execution only:
Automatic external research: 0 / FAIL

SAFETY
Synthetic relationships: 0 / FAIL
Synthetic evidence: 0 / FAIL
Candidate promoted without evidence: 0 / FAIL
Canonical Phase-2 mutations: 0 / FAIL
Source file mutations: 0 / FAIL
Exposure currency invented: 0 / FAIL

BROWSER
Unhandled 404:
HTTP 500:
JS errors:

TESTS
Passed:
Failed:

SCREENSHOTS:
<paths>

REPORT:
backend/data/CCR_FULL_ANALYTICAL_PLATFORM_REPORT.md

WINDOWS ANALYTICAL POC READY:
YES / NO

If NO:
list only genuine blockers.

STOP.
