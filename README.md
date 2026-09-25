LENDING INTELLIGENCE — CURRENT PRODUCT DESIGN + SYSTEM ARCHITECTURE AUDIT

THIS IS LENDING ONLY.

DO NOT inspect, use, merge, import, infer from, or redesign CCR data or CCR
business logic.

Do not use:
- Customer_latest.parquet
- CCR customer-master values
- CCR relationship truth
- CCR population counts

CCR/shared legacy code may be mentioned ONLY where it physically coexists in
the repository and creates a technical boundary or contamination risk.

============================================================
MISSION
============================================================

Perform a comprehensive CURRENT-STATE forensic audit of the Lending Intelligence
application as it exists NOW after the UI reconstruction work.

I need a detailed document describing:

1. Current frontend product design
2. Current information architecture
3. Current page/route architecture
4. Current frontend component architecture
5. Current backend architecture
6. Current API architecture
7. Current data architecture
8. Current relationship authority model
9. Current network architecture
10. Current geography/map architecture
11. Current evidence and lineage model
12. Current research architecture
13. Current AI architecture
14. Stylus integration
15. R2D2 integration
16. Other external/provider integrations
17. Current Ask Lending Intelligence implementation
18. Current state-management / investigation-context architecture
19. Performance/bounded-read architecture
20. Security/governance/action boundaries
21. Current deployment/runtime architecture
22. Current technical debt
23. Current gaps between intended product and actual implementation
24. What must be preserved during the next reconstruction stages

THIS IS AN AUDIT.

Do NOT redesign the product.
Do NOT implement U2.
Do NOT change code.
Do NOT change APIs.
Do NOT change source data.
Do NOT change provider configuration.

Read and trace the existing implementation.

============================================================
READ FIRST
============================================================

At minimum inspect:

backend/data/LENDING_UI_RECONSTRUCTION_BLUEPRINT.md
backend/data/LENDING_UI_U1_IMPLEMENTATION_REPORT.md

and any subsequent U1.5 report if present.

Also inspect all relevant current source files under:

frontend/src/
backend/app/
backend/data/
scripts/
tests/

Inspect package.json / dependency configuration.

Inspect environment/configuration references relevant to:

- AI
- Stylus
- R2D2
- SEC
- Web
- provider adapters
- research
- caches
- model/provider routing

Do not expose secrets.

============================================================
1. CURRENT PRODUCT / UX ARCHITECTURE
============================================================

Document what the current user sees.

Include the actual active Lending shell and its hierarchy.

From the running implementation identify:

- institutional left rail;
- global command/search;
- authority indicator;
- Ask Lending Intelligence;
- context strip;
- Executive page;
- Portfolio;
- Geography;
- Network;
- Relationships;
- Attention;
- Research;
- Studio;
- Client Detail / Client 360;
- inspectors/drawers;
- map;
- graph;
- tables;
- filters;
- handoffs.

For each surface document:

- route;
- owning React component;
- child components;
- APIs called;
- initial load behavior;
- user interactions;
- URL parameters;
- context preserved across navigation;
- read/write behavior;
- empty/error/loading states;
- source lanes displayed;
- current visual maturity;
- legacy implementation dependencies.

Include an actual route table.

============================================================
2. CURRENT FRONTEND ARCHITECTURE
============================================================

Produce a component/module map.

Show actual paths such as:

App
  ProductShell
    PrimaryRail
    CommandBar
    ContextStrip
    AskLending
  Executive
    ...
  Portfolio
    ...
  Geography
    ...
  Network
    ...
  Client
    ...

Use actual names from the repository.

Identify:

- new reconstructed components;
- legacy components still active;
- duplicated implementations;
- monolithic components;
- shared utilities;
- API client modules;
- data adapters;
- types/contracts;
- styling architecture;
- map modules;
- graph modules;
- inspector modules;
- AI/assistant modules.

State what is active versus retained/unused.

============================================================
3. PAGE-BY-PAGE CURRENT DESIGN
============================================================

Document the CURRENT rendered design in detail.

Especially inspect:

A. Executive Intelligence

Current visible elements include things such as:

- 2,484 portfolio clients;
- reported OSUC;
- CAM coverage;
- review-required;
- attention items;
- geographic intelligence map;
- compact relationship ecosystem;
- exposure ranking;
- CAM availability;
- sector concentration.

Confirm actual implementation and source.

B. Portfolio / Client Analytics

Document:

- metrics;
- attention cards;
- search;
- sector/country/CAM filters;
- relationship filters;
- tables;
- sorting;
- pagination/loading;
- client handoff.

C. Geographic Intelligence

Document:

- map implementation;
- geometry source;
- country mapping;
- markers;
- aggregation;
- map metrics;
- mapped/unmapped behavior;
- URL state;
- relation to Network.

D. Network Intelligence

Document current:

- focus-selection behavior;
- degree 1 / degree 2 controls;
- graph/geography/table modes;
- source-lane toggles;
- CAM / review / external / AI controls;
- node bounds;
- edge bounds;
- expansion;
- inspectors;
- empty-network behavior;
- relationship evidence handoff.

E. Client Detail / Client 360

Document:

- identity;
- exposure;
- CAM count;
- relationship count;
- tabs;
- relationship grouping;
- source lanes;
- unresolved endpoints;
- V2 fallback/history;
- evidence;
- review handoffs;
- Network handoff;
- Research handoff;
- Intelligence handoff.

============================================================
4. DATA ARCHITECTURE
============================================================

Create a detailed source-to-UI data architecture.

For every current Lending data source identify:

- file/store/database;
- physical format;
- purpose;
- approximate population;
- authority;
- lifecycle;
- owning loader;
- APIs consuming it;
- UI surfaces consuming it;
- whether currently active;
- whether fallback/history/supplemental/internal.

At minimum reconcile the known Lending universes:

CAM/V3
V2 candidate/fallback
Normalized operational projection
External research/overlay
Published/governed AI
Portfolio workbook/source population

Do not collapse them into one denominator.

Explicitly state:

CAM/V3 = authoritative Lending relationship truth.

V2 = fallback/history only where supported.

Normalized operational projection = separate governed/internal projection.

External = supplemental.

Governed AI = separate generated/published lane.

Reported OSUC = source-reported/supplemental exposure context.

Review-required = workflow state, not risk.

============================================================
5. SOURCE → API → UI LINEAGE
============================================================

For every major visible metric or object, trace:

SOURCE
    ↓
LOADER / STORE
    ↓
BACKEND SERVICE
    ↓
API
    ↓
FRONTEND ADAPTER
    ↓
COMPONENT
    ↓
DISPLAY

Examples:

Portfolio client count
Reported OSUC
CAM coverage
Review-required count
Top exposures
Sector concentration
Country distribution
Relationship rows
Network nodes
Network edges
Evidence counts
Attention items

Do not assume lineage.

Trace actual code.

============================================================
6. RELATIONSHIP ARCHITECTURE
============================================================

Document exactly how a relationship is represented.

Include actual fields where present:

- relationship ID;
- semantic/group ID;
- subject;
- related entity;
- endpoint IDs;
- relationship type;
- family;
- direction;
- state;
- connectivity;
- source lane;
- source system;
- evidence;
- source references;
- review state;
- publication state;
- completeness;
- lineage;
- authority;
- confidence if source-defined;
- taxonomy/reason codes.

Explain differences between:

- source assertion;
- semantic/group display;
- evidence record;
- review item;
- external proposal;
- governed AI instance.

============================================================
7. NETWORK ARCHITECTURE
============================================================

Trace current Network end-to-end.

Document:

- graph data source;
- API;
- graph adapter;
- node construction;
- edge construction;
- node identity;
- edge identity;
- source labels;
- direction;
- deterministic layout;
- degree expansion;
- first-degree behavior;
- caps;
- truncation;
- source toggles;
- inspectors;
- table synchronization;
- geography view.

Confirm whether the browser ever loads:

- normalized 32,957-row artifact;
- ~2.8 GB normalized history;
- broad group materialization.

Identify any route that still risks doing so.

Network provenance rules must be documented:

CAM
CAM · REVIEW
SEC
WEB
AI
V2

If multiple assertions support a semantic connection explain how the current
implementation represents that.

============================================================
8. GEOGRAPHY / MAP ARCHITECTURE
============================================================

Document:

- map technology;
- geometry file/source;
- rendering technology;
- country-key reconciliation;
- mapped country count;
- unmapped labels;
- map metrics;
- client count;
- relationship count;
- reported OSUC;
- markers;
- fills;
- interaction;
- focus;
- URL state;
- graph/map relationship.

State explicitly what geography represents and what it does NOT represent.

No country-risk interpretation unless actually source-supported.

============================================================
9. EXTERNAL RESEARCH ARCHITECTURE
============================================================

Trace the current external research workflow.

Document the complete lifecycle:

REQUEST
→ cache lookup
→ provider readiness
→ provider call
→ retrieval
→ extraction
→ identity resolution
→ claim/candidate
→ evidence
→ classification
→ proposal/conflict/insufficient
→ review
→ optional governed action

Identify exact current providers and adapters.

Separate:

SEC
Web
Stylus
R2D2
other providers

Do not imply a provider exists unless code/config proves it.

============================================================
10. STYLUS INTEGRATION
============================================================

Perform a specific Stylus audit.

Search the repository for:

Stylus
stylus
provider names
environment variables
client classes
HTTP endpoints
research adapters
provider registries
feature flags
configuration
tests
cached results

Document:

A. Is Stylus currently implemented?

Use one classification:

ACTIVE
PARTIALLY IMPLEMENTED
CONFIGURED BUT UNUSED
STUBBED
PLANNED ONLY
NOT FOUND

B. If implemented, show actual architecture:

UI
↓
API
↓
research orchestrator
↓
Stylus adapter/client
↓
external service
↓
normalized result
↓
evidence/proposal/store
↓
UI

C. Document:

- request fields;
- response schema;
- authentication mechanism conceptually;
- timeout behavior;
- retry behavior;
- caching;
- fail-closed behavior;
- provenance;
- audit logging;
- review boundary;
- whether ordinary page load can call Stylus;
- whether Ask Lending can invoke it;
- whether explicit user confirmation is required.

DO NOT display credentials or secrets.

============================================================
11. R2D2 INTEGRATION
============================================================

Perform the same audit for R2D2.

Search all code/config/tests/reports.

Classify it:

ACTIVE
PARTIALLY IMPLEMENTED
CONFIGURED BUT UNUSED
STUBBED
PLANNED ONLY
NOT FOUND

Explain what R2D2 actually does in THIS repository.

Do not infer from its name.

Trace:

UI
↓
API
↓
orchestrator
↓
R2D2 adapter/client
↓
service
↓
response
↓
normalization
↓
evidence/result
↓
user-facing surface

Document its relationship, if any, to:

- external research;
- SEC;
- Web;
- document retrieval;
- AI extraction;
- relationship discovery;
- relationship validation;
- CAM;
- proposals;
- review;
- Ask Lending Intelligence.

============================================================
12. AI ARCHITECTURE
============================================================

Perform a complete AI architecture audit.

Identify every current AI-related component.

Separate:

A. Ask Lending Intelligence

B. Governed AI Relationship Studio

C. AI used inside research/extraction, if any

D. provider/model infrastructure

E. future/stubbed AI components

For Ask Lending Intelligence document:

- frontend component;
- context payload;
- active route;
- focused client/entity;
- selected relationship;
- filters;
- source lanes;
- graph state;
- geography state;
- bounded metadata;
- question payload;
- backend endpoint;
- model/provider call;
- tool/action system;
- response rendering.

State whether the current Ask surface is:

LIVE MODEL-BACKED
READ-ONLY RULE/CONTEXT ASSISTANT
PARTIAL
UI ONLY

Do not infer.

============================================================
13. AI UI-CONTROL ARCHITECTURE
============================================================

Determine whether AI can currently control the Lending UI.

Audit support for actions such as:

navigate
search
focus client
focus entity
filter
show map
show network
select relationship
open evidence
open inspector
expand network
prepare research

Separate:

SUPPORTED NOW
PARTIALLY SUPPORTED
NOT IMPLEMENTED

Also distinguish:

SAFE READ/NAVIGATION ACTIONS

from:

EXPLICIT CONFIRMATION ACTIONS

such as:

run SEC research
run Web research
run Stylus
run R2D2
create proposal
approve
publish
modify review state

============================================================
14. MODEL / PROVIDER MATRIX
============================================================

Produce a provider matrix.

Columns:

Provider
Purpose
Current status
Invocation path
Automatic or explicit
Cache
Persistence
Evidence provenance
Can alter CAM?
Failure behavior
Tests
Configuration source

Include if found:

OpenAI
Anthropic
Grok/xAI
Stylus
R2D2
SEC
Web provider(s)
GLEIF
other external systems

Do not include hypothetical providers.

============================================================
15. AI GOVERNANCE
============================================================

Document current AI governance.

Trace the existing lifecycle if implemented:

Describe
→ Configure
→ Draft
→ Preview
→ Approval
→ Publish

Explain:

- definition;
- version;
- instance;
- publication;
- audit;
- provenance;
- human approval;
- separation from CAM.

State clearly whether published AI can ever mutate CAM automatically.

============================================================
16. SEC / WEB RESEARCH FALLBACK
============================================================

Document the intended and actual missing-connection behavior.

For:

NO GOVERNED CONNECTION CURRENTLY ESTABLISHED

trace what currently happens.

Explain:

- CAM check;
- cached external check;
- SEC state;
- Web state;
- research-not-performed state;
- Research Connection handoff;
- provider execution;
- result classification;
- proposal/review.

Confirm no research provider is automatically invoked merely because a CAM
relationship is missing.

============================================================
17. ATTENTION / REVIEW ARCHITECTURE
============================================================

Document all current attention/review concepts.

Separate:

CAM review-required
normalized review
external proposal review
external conflict
insufficient evidence
identity unresolved
data readiness issue
AI governance approval

Do not combine them into a fake universal risk queue.

Trace current UI routes and mutation behavior.

============================================================
18. CURRENT SEARCH ARCHITECTURE
============================================================

Audit the global search.

Identify what it actually searches:

clients
CAGID
entities
relationship IDs
relationship groups
counterparties
other fields

Document:

- frontend debounce;
- endpoint;
- pagination;
- bounds;
- result ranking;
- current limitations.

The current placeholder may say:

Search client, CAGID, entity, relationship

Verify whether the backend actually supports each class.

Do not describe placeholder text as implemented functionality.

============================================================
19. URL / INVESTIGATION CONTEXT
============================================================

Document current URL-backed context.

Include actual parameters such as:

focus
view
scope
lane
type
family
state
connectivity
country
sector
degree
selected
page
cursor
research

Classify each:

IMPLEMENTED
PARTIAL
PLANNED

Explain whether investigation context survives handoffs between:

Executive
Portfolio
Client 360
Geography
Network
Relationships
Attention
Research
Studio.

============================================================
20. PERFORMANCE ARCHITECTURE
============================================================

Audit boundedness and performance.

For every major initial page load identify:

- endpoints;
- limits;
- pagination;
- rows returned;
- expensive adapters;
- caching;
- frontend rendering limits.

Explicitly audit the known large normalized universe:

approximately 32,957 rows
approximately 2.8 GB artifact

Identify any code path that materializes it before applying a limit.

Identify risks in:

relationship groups
relationship details
search
Network
Relationships
workbench
Ask Lending

============================================================
21. CURRENT FRONTEND TECHNOLOGY
============================================================

Document actual frontend stack:

React
TypeScript
Vite
routing
CSS architecture
state management
query/cache library
map renderer
graph renderer
table library
animation library
icons
testing
linting

For each:

CURRENTLY INSTALLED
CURRENTLY USED
LEGACY/UNUSED

Do not recommend replacements in this section.

============================================================
22. CURRENT BACKEND TECHNOLOGY
============================================================

Document:

framework
routers
services
stores
SQLite
JSON
Parquet if Lending actually uses it
file artifacts
cache directories
provider clients
test architecture
runtime server
configuration model

Include a directory/module diagram.

============================================================
23. SECURITY / CONFIGURATION
============================================================

Document safely:

- environment variable categories;
- provider credentials architecture;
- secret-handling approach;
- client/server boundaries;
- browser-exposed configuration;
- provider call location;
- authentication assumptions;
- explicit-action boundaries.

DO NOT print secret values.

============================================================
24. CURRENT DEPLOYMENT / RUNTIME
============================================================

Document:

- local frontend runtime;
- backend runtime;
- proxying;
- ports;
- build output;
- deployment evidence in repository;
- remote/local parity status;
- known deployment gaps.

Do not infer deployment status where evidence is absent.

============================================================
25. ARCHITECTURE DIAGRAMS
============================================================

Include ASCII/Mermaid-style diagrams.

A. Entire Lending architecture

USER
 ↓
REACT UI
 ↓
LENDING API CLIENT
 ↓
FASTAPI ROUTERS
 ↓
SERVICES / STORES
 ↓
CAM / V2 / NORMALIZED / EXTERNAL / AI
 ↓
PROVIDERS

B. Relationship truth architecture

CAM/V3
     ↓
authoritative relationship read

V2
     ↓
fallback/history

External SEC/Web/Stylus/R2D2
     ↓
supplemental evidence/proposal

Governed AI
     ↓
separate governed generated lane

C. Ask Lending architecture

UI CONTEXT
   ↓
ASK LENDING
   ↓
READ/SEARCH/ACTION ROUTER
   ↓
LENDING DATA / RESEARCH HANDOFF / UI ACTIONS

D. Network architecture

FOCUS
 ↓
BOUNDED RELATIONSHIP READ
 ↓
NODE/EDGE ADAPTER
 ↓
DETERMINISTIC GRAPH
 ↓
INSPECTOR / EVIDENCE / EXPANSION

============================================================
26. CURRENT PRODUCT GAPS
============================================================

After documenting the system, identify gaps.

Do not redesign them yet.

Classify each gap as:

VISUAL
UX
FRONTEND ARCHITECTURE
BACKEND API
DATA
AI
RESEARCH
PROVIDER
PERFORMANCE
GOVERNANCE
DEPLOYMENT
TESTING

Examples to verify rather than assume:

- full Network not yet visually mature;
- relationship search limitations;
- Ask Lending may not yet be model-backed;
- Stylus integration may be incomplete;
- R2D2 may be incomplete;
- deep routes may still use legacy layouts;
- relationship-group endpoint may still be expensive;
- graph may require explicit focus;
- provider calls may only exist in Research;
- browser visual regression tests may be absent.

============================================================
27. PRESERVATION CONTRACT FOR NEXT UI STAGES
============================================================

End with an explicit preservation list for U2+.

Separate:

MUST PRESERVE

MAY REFACTOR

MUST NOT CHANGE WITHOUT GOVERNANCE APPROVAL

This list should protect:

- CAM/V3 authority;
- source-lane distinctions;
- read/write boundaries;
- explicit research invocation;
- bounded loading;
- relationship evidence;
- lineage;
- review semantics;
- OSUC semantics;
- V2 fallback semantics;
- external supplemental semantics;
- AI separation.

============================================================
OUTPUT
============================================================

Create:

backend/data/LENDING_CURRENT_PRODUCT_ARCHITECTURE_AUDIT.md

This should be a detailed engineering/product architecture document.

Do not make code changes except creating this report.

At the beginning include:

CURRENT STATE SNAPSHOT

with:

- active pages;
- active routes;
- current Lending population;
- current CAM/V3 relationship count;
- current review-required count;
- current external production count;
- current AI production count;
- active research providers;
- Stylus status;
- R2D2 status;
- Ask Lending status;
- current map technology;
- current graph technology;
- current major performance constraint.

At the end include:

NEXT RECONSTRUCTION READINESS

with exactly three classifications:

READY
READY WITH PREREQUISITES
NOT READY

Evaluate separately:

U2 Full Network Intelligence
U3 Relationship Intelligence
U4 Ask Lending / AI interaction
U5 Research + Stylus/R2D2
U6 Attention / Review
U7 final visual hardening

For every classification state the concrete prerequisite, not a vague opinion.

============================================================
HARD RULE
============================================================

Do not rely on prior reports where current source contradicts them.

CURRENT SOURCE > OLD REPORT.

Do not call external providers during this audit.

Do not run Stylus.
Do not run R2D2.
Do not run SEC.
Do not run Web.
Do not run AI generation.

Inspect configuration and code only.

Do not expose secrets.

Do not modify application behavior.

STOP after the report.

Final response must end exactly:

LENDING CURRENT ARCHITECTURE AUDIT COMPLETE
