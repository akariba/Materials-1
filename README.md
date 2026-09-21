CCR RELATIONSHIP CORRELATION — PHASE 4A
WINDOWS LOCAL WORKING POC

You are working inside the CURRENT CCR repository in VSCode on Windows.

The immediate objective is:

GET THE CCR RELATIONSHIP CORRELATION TOOL WORKING LOCALLY ON WINDOWS.

Do NOT work on Unix / Market Dev in this phase.

Do NOT spend more time fixing external DNS.

Do NOT require SEC, GLEIF or Web connectivity for the application to start
and operate locally.

External providers currently have connectivity problems in this Windows
environment. The application must handle that gracefully.

==================================================
1. OBJECTIVE
==================================================

Create a usable local CCR Relationship Intelligence POC using the REAL
currently available CCR data.

The user must be able to:

1. open the application;
2. understand the CCR population;
3. search clients;
4. open a client;
5. see its exposure/reference information;
6. open the relationship network;
7. see available evidence-backed structural relationships where they really
   exist;
8. optionally display local research-candidate signals separately;
9. configure AI relationship analyses;
10. inspect SEC/GLEIF/Web provider status;
11. run external research explicitly when connectivity is available;
12. see a clean failure state when external connectivity is unavailable.

No fake CCR relationships.

==================================================
2. CURRENT FOUNDATION
==================================================

Use the existing:

backend/data/ccr_relationship_intelligence.sqlite3

Current validated foundation includes approximately:

- 16,755 canonical CCR clients
- 25,000 exposure rows
- 24,984 linked exposure rows
- 14 unresolved source identities
- 16 unresolved exposure rows
- 8,009 valid local LEIs
- Phase-3 external research schema
- source policy
- research runs
- external identity tables
- evidence tables
- provider cache
- GLEIF / SEC provider infrastructure

Recompute counts from database.

Do not hardcode them.

==================================================
3. IMPORTANT WINDOWS RULE
==================================================

External connectivity is OPTIONAL for local UI operation.

Application startup must NOT:

- call SEC
- call GLEIF
- call Web
- fail because DNS is unavailable
- automatically perform external research

External provider state may show:

AVAILABLE
UNAVAILABLE
NOT_CONFIGURED
DNS_ERROR
CACHE_ONLY

The rest of the application must continue working.

==================================================
4. PRESERVE EXISTING DATA
==================================================

Do not modify:

Customer_latest.parquet
thousandClients.csv
backend/data/ccr_clients.sqlite3

Do not alter Phase-2 canonical identity.

Do not fabricate:

relationships
parents
suppliers
customers
investors
materiality
confidence
evidence

==================================================
5. FIRST — AUDIT THE CURRENT FRONTEND
==================================================

Inspect the existing frontend.

Determine:

framework
routes
components
API client
theme/design system
current pages
current broken states

Do not rewrite everything if usable structure exists.

Reuse working components.

==================================================
6. LOCAL BACKEND CONTRACT
==================================================

Create or complete read-only/local endpoints required by the UI.

Use existing FastAPI conventions.

At minimum provide:

GET /api/ccr/status

GET /api/ccr/overview

GET /api/ccr/clients

GET /api/ccr/clients/{ccr_client_key}

GET /api/ccr/clients/{ccr_client_key}/exposure

GET /api/ccr/clients/{ccr_client_key}/identifiers

GET /api/ccr/clients/{ccr_client_key}/hierarchy

GET /api/ccr/clients/{ccr_client_key}/relationships

GET /api/ccr/clients/{ccr_client_key}/candidates

GET /api/ccr/network/{ccr_client_key}

GET /api/ccr/research/status

GET /api/ccr/relationship-config

POST /api/ccr/relationship-config

Existing compatible Phase-3 routes may be reused.

Do not duplicate routes unnecessarily.

==================================================
7. OVERVIEW PAGE
==================================================

Build a clean CCR Relationship Intelligence landing page.

The user should understand the tool within seconds.

Show real calculated values:

CCR Clients
Exposure Records
Resolved Clients
Unresolved Clients
Clients with LEI
Research-ready Clients
Relationship Observations
Research Runs
Evidence Records

Do not invent monetary totals because exposure units are still UNKNOWN.

If amount units are unresolved display:

Exposure values available
Units not confirmed

rather than a fake USD number.

==================================================
8. GLOBAL RELATIONSHIP FOOTPRINT
==================================================

Include the world-map component in the Overview.

This is important.

Use actual country fields from canonical CCR clients.

Show:

number of CCR clients by country
percentage of population
selected client location

If available, show relationship connection arcs ONLY for real
evidence-backed relationships.

Do NOT draw fake relationship arcs just to make the map attractive.

When there are no real edges:

show client distribution points / country bubbles.

Label clearly:

CCR Client Footprint

and separately:

Evidence-backed Relationship Connections

==================================================
9. CLIENTS PAGE
==================================================

Create a scalable searchable client table.

Columns should use actual available fields such as:

Legal Name
GFCID
CAGID
Country
Industry / Sector
LEI
Identity Quality
Exposure Record Count
Research Readiness

Support:

search by legal name
GFCID
CAGID
LEI

Filters:

Country
Sector / industry where available
Identity quality
Has LEI
SEC readiness
GLEIF readiness
Web readiness

Use backend pagination.

Do not send all 16k records to browser if unnecessary.

==================================================
10. CLIENT DETAIL PAGE
==================================================

When a client is selected show:

legal/display name

GFCID
CAGID
LEI
country
industry
sector
identity quality

Exposure section:
number of exposure/facility records

Do NOT present unknown-unit exposure amounts as USD.

Identifiers section

Research readiness:

GLEIF
SEC
Web

Provider status

Relationships

Research Candidates

Evidence

==================================================
11. RELATIONSHIP TYPES
==================================================

Create the canonical CCR relationship taxonomy/configuration catalogue.

Initial configurable types:

SUPPLIER
CRITICAL_SUPPLIER
CUSTOMER
KEY_CUSTOMER

PARENT
SUBSIDIARY
ULTIMATE_PARENT

INVESTOR
SPONSOR

LENDER
FINANCING_RELATIONSHIP

STRATEGIC_PARTNER
JOINT_VENTURE

TECHNOLOGY_PROVIDER
TECHNOLOGY_DEPENDENCY

CLOUD_PROVIDER
INFRASTRUCTURE_PROVIDER
INFRASTRUCTURE_DEPENDENCY

SERVICE_PROVIDER

MANUFACTURING_PARTNER
DISTRIBUTOR
SOURCE_OF_INPUTS

OTHER_EVIDENCE_BACKED_RELATIONSHIP

These are allowed taxonomy values.

Their existence in the taxonomy does NOT mean a relationship exists.

==================================================
12. RELATIONSHIP DATA STATES
==================================================

Keep states explicit.

CONFIRMED_EXTERNAL
EXTERNAL_PROPOSAL_PENDING_REVIEW
REVIEW_REQUIRED
INSUFFICIENT_EVIDENCE
CONFLICT
HISTORICAL

Candidate/similarity signals must NOT use these states.

They belong to a separate layer:

RESEARCH_CANDIDATE

==================================================
13. NETWORK VIEW
==================================================

Build the relationship network.

This is a core page.

Default behavior:

user searches/selects ONE CCR client

center node:
selected CCR client

Then display bounded connected data only.

Never load the entire 16k universe.

Provide layers:

[✓] Evidence-backed relationships
[ ] Research candidates
[ ] External structural observations
[ ] Indirect paths

If no real relationship exists:

show the selected node plus an honest empty state:

"No evidence-backed relationships currently stored."

Then optionally:

"Show research candidates"

==================================================
14. RESEARCH CANDIDATES
==================================================

Use the existing Phase-2:

candidate_signal_registry

Candidate signals may include only locally supported dimensions.

Examples:

same industry
same sector
same geography
existing structural identifier signal
shared classification

These are for RESEARCH SEEDING ONLY.

Render candidate edges as:

dashed
light
clearly labelled

RESEARCH CANDIDATE

Never:

SUPPLIER
CUSTOMER
PARTNER

unless actual evidence exists.

==================================================
15. NETWORK NODE VISUALS
==================================================

Distinguish:

Selected CCR Client
CCR Client
External Entity
Research Candidate

When a selected node has exposure context, node size may use:

exposure record count

for now.

Do NOT use unknown-unit exposure amount.

Legend must explicitly say:

Node size = Exposure Record Count

if that sizing is used.

==================================================
16. NETWORK EDGE VISUALS
==================================================

Real evidence-backed:
solid

GLEIF structural observation:
solid but separate color/style

Pending review:
dashed

Research candidate:
thin dotted/dashed

Indirect:
multi-hop style

Do not visually make candidates look confirmed.

==================================================
17. EDGE INSPECTOR
==================================================

Clicking a real edge must show:

Subject
Related Entity
Relationship Type
Direction
State
Source Channel
Source Tier
Evidence Count
Research Run
Review State

Button:

View Evidence

Clicking a candidate edge must instead show:

Candidate Signal
Why this entity was proposed for research
Source local fields
NOT EVIDENCE
No confirmed relationship

==================================================
18. AI CREATE RELATIONSHIP
==================================================

Build this now.

This is configuration first.

Create a page/panel:

AI Create Relationship

The user can define analysis presets.

Seed with:

1. Supply Chain Dependency
2. Technology Dependency
3. Customer Relationship
4. Parent / Subsidiary
5. Investor / Sponsor
6. Lender / Financing
7. Strategic Partner
8. Infrastructure Dependency
9. Service Provider
10. Joint Venture
11. Custom Analysis

==================================================
19. AI CONFIG STRUCTURE
==================================================

Each preset should support:

Analysis Name

Active:
ON / OFF

Objective

Detailed Instructions

Relationship Scope

Source Channels:
[ ] SEC
[ ] GLEIF
[ ] High-quality Web

Allowed Relationship Types

Source Tier Minimum

Require Primary Source:
YES / NO

Require Multiple Sources:
YES / NO

Minimum Evidence Count

Allow Historical Evidence:
YES / NO

Maximum Evidence Age

Direction Rules

Entity Resolution Requirements

Review Requirement

==================================================
20. EXAMPLE PRESET — SUPPLY CHAIN
==================================================

Seed:

Analysis Name:
Supply Chain Dependency

Objective:

Identify entities whose goods, services, components, technology or other
inputs are materially required for the subject company's operations.

Detailed instructions:

- Look for explicit supplier/customer disclosures.
- Determine what is supplied.
- Determine relationship direction.
- Distinguish ordinary supplier from dependency.
- Do not infer a supplier relationship from shared sector.
- Do not infer dependency from simple vendor mention.
- Prefer explicit SEC filing or primary-source evidence.
- Use high-quality secondary sources only when permitted.
- Preserve evidence excerpt and citation.
- Return insufficient evidence rather than guessing.

Sources:

SEC = enabled
GLEIF = disabled for supplier relationship evidence
Web = enabled when provider becomes available

Allowed relationship types:

SUPPLIER
CRITICAL_SUPPLIER
SOURCE_OF_INPUTS
MANUFACTURING_PARTNER

==================================================
21. PARENT / SUBSIDIARY PRESET
==================================================

Objective:

Identify defensible legal/corporate hierarchy.

Primary source:

GLEIF Level 2
SEC where applicable

Allowed:

PARENT
SUBSIDIARY
ULTIMATE_PARENT

Do NOT treat:

beneficial owner
investor
sponsor

as equivalent to accounting-consolidating parent.

==================================================
22. CONFIG PERSISTENCE
==================================================

Persist the AI relationship configurations.

Add additive tables if needed such as:

relationship_analysis_configs
relationship_analysis_config_versions

Fields should support:

config_id
name
description
active
objective
instructions
sources
allowed_relationship_types
source_policy
evidence_rules
direction_rules
review_rules
created_at
updated_at
version

Do not store config only in frontend localStorage.

==================================================
23. CONFIG VERSIONING
==================================================

Every edit creates a new version or maintains an auditable version value.

The user should be able to see:

Current Version
Last Updated

No need for complex approval workflow yet.

==================================================
24. EXTERNAL RESEARCH PAGE
==================================================

Create the page even though Windows connectivity is currently unavailable.

Show provider cards:

GLEIF
SEC
Web

Each shows:

Configured
Connectivity
Cache
Last Successful Run
Last Error

For current Windows state it is valid to show:

GLEIF
Configured: Yes
Connectivity: DNS Error

SEC
Configured: Yes
Connectivity: DNS Error

Web
Configured: No

This must NOT break the rest of the product.

==================================================
25. RUN EXTERNAL RESEARCH
==================================================

The control may exist.

But execution must remain explicit.

Button:

Run External Research

Never call external research on:

page load
client click
network click
tab change
refresh

If Windows DNS fails:

display:

Research could not run
Provider connectivity unavailable

with diagnostic status.

Do not crash.

==================================================
26. RELATIONSHIP EXPLORER
==================================================

Create a table with:

Subject
Related Entity
Relationship Type
Direction
Status
Source
Confidence / Quality
Evidence Count
Review State

If no relationships exist:

show proper empty state.

Do not fill it with candidate signals.

Provide a separate tab:

Research Candidates

==================================================
27. EVIDENCE VIEW
==================================================

For real evidence:

Publisher
Source
Source Tier
Document / Filing Type
Published Date
Retrieved Date
Evidence Excerpt
Source Reference
Admissibility
Research Run

Do not expose raw JSON by default.

Technical Details may be expandable.

==================================================
28. LOCAL PROVIDER STATUS
==================================================

Application must start even if:

socket.getaddrinfo(api.gleif.org) fails

or

socket.getaddrinfo(data.sec.gov) fails.

Provider status checks must:

timeout quickly
be bounded
not block UI startup

Prefer backend cached status rather than repeated browser polling.

==================================================
29. WINDOWS STARTUP
==================================================

Make local startup straightforward.

Do not permanently hardcode the user's C:\ path.

Use project-relative paths.

Backend:

python -m uvicorn app.main:app --host 127.0.0.1 --port 8000

Frontend:

use the existing frontend toolchain.

Likely:

npm install
npm run dev

Use the actual repo scripts/package.json.

Do not guess if different.

==================================================
30. FRONTEND API CONFIG
==================================================

For local development:

frontend should communicate with backend reliably.

Prefer:

Vite proxy / same-origin development proxy

or configurable:

VITE_API_BASE_URL

Do not scatter:

http://127.0.0.1:8000

through components.

This will help later Unix migration.

==================================================
31. UI VISUAL LANGUAGE
==================================================

Reuse the established clean Relationship Intelligence visual language.

Do not redesign the Stylus preset.

Visual priorities:

large relationship network
clear client context
world map
evidence panel
configuration panel

Avoid:

giant technical status dashboard
raw JSON everywhere
giant unbounded graph
fake relationship counts

==================================================
32. MAIN NAVIGATION
==================================================

Preferred navigation:

Overview

Clients

Network

Relationship Explorer

AI Create Relationship

External Research

Review

Use existing navigation if already close.

==================================================
33. LOCAL WORKING ACCEPTANCE SCENARIO
==================================================

Use REAL CCR data.

Select a deterministic actual client with:

resolved identity
legal name
country
LEI if possible

Do not hardcode a famous company merely for appearance.

Acceptance flow:

1. Overview opens.
2. Counts reconcile to backend.
3. World map loads.
4. Search client.
5. Open client detail.
6. Exposure record count displays.
7. LEI displays where available.
8. Open Network.
9. Selected client is center node.
10. Evidence-backed relationships display if any.
11. Otherwise honest empty state displays.
12. Toggle Research Candidates.
13. Candidate nodes appear separately.
14. Click candidate and see "NOT EVIDENCE".
15. Open AI Create Relationship.
16. Edit Supply Chain Dependency preset.
17. Save.
18. Reload page.
19. Configuration persists.
20. Open External Research.
21. Provider DNS error does not crash UI.

==================================================
34. TESTS
==================================================

Add tests for:

Overview API

client pagination

client search

client detail

network boundedness

candidate != relationship

candidate cannot appear as confirmed edge

AI config CRUD

AI config persistence

AI config versioning

external provider failure does not break local APIs

GET pages do not trigger external calls

network page does not trigger external calls

world-map country aggregation

empty relationship state

evidence endpoint

Phase-2 regression

Phase-3 regression

==================================================
35. RUN THE APPLICATION
==================================================

After implementation:

start backend

start frontend

exercise the local acceptance flow.

Use localhost/127.0.0.1 only for this Windows POC.

If browser automation/playwright already exists, use it.

Otherwise perform API tests plus frontend build/typecheck.

==================================================
36. SCREENSHOTS
==================================================

If browser tooling is available, capture screenshots of:

Overview
Clients
Client Detail
Network
AI Create Relationship
External Research

Save under an appropriate local test/output directory.

Do not embed mock business values.

==================================================
37. REPORT
==================================================

Create:

backend/data/CCR_PHASE4A_WINDOWS_LOCAL_POC_REPORT.md

Include:

ROUTES
API STATUS
UI PAGES
OVERVIEW COUNTS
CLIENT SEARCH
NETWORK
WORLD MAP
RESEARCH CANDIDATES
RELATIONSHIP CONFIG
EXTERNAL PROVIDER STATUS
TEST RESULTS
KNOWN LIMITATIONS
FILES CHANGED

==================================================
38. FINAL RESPONSE
==================================================

Return exactly:

CCR WINDOWS LOCAL POC: PASS / FAIL

BACKEND
Running:
URL:
Health:

FRONTEND
Running:
URL:
Build/typecheck:

OVERVIEW
CCR clients:
Exposure rows:
Resolved:
Unresolved:
LEI clients:
World map: PASS / FAIL

CLIENTS
Search: PASS / FAIL
Pagination: PASS / FAIL
Client detail: PASS / FAIL

NETWORK
Selected-client graph: PASS / FAIL
Evidence-backed edges:
Research candidate layer: PASS / FAIL
Candidate/evidence separation: PASS / FAIL
No full-universe graph: PASS / FAIL

AI CREATE RELATIONSHIP
Page: PASS / FAIL
Default presets:
Edit: PASS / FAIL
Save: PASS / FAIL
Persistence: PASS / FAIL
Versioning: PASS / FAIL

EXTERNAL RESEARCH
GLEIF status:
SEC status:
Web status:
DNS failure handled gracefully: PASS / FAIL
Automatic external calls: 0 / FAIL

RELATIONSHIPS
Confirmed external:
Pending review:
GLEIF observations:
Research candidates:
Synthetic relationships: 0 / FAIL

TESTS
Passed:
Failed:

SCREENSHOTS
Overview:
Clients:
Client Detail:
Network:
AI Create Relationship:
External Research:

REPORT:
backend/data/CCR_PHASE4A_WINDOWS_LOCAL_POC_REPORT.md

WINDOWS LOCAL POC READY:
YES / NO

STOP.
