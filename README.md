LENDING TOTAL UI RECONSTRUCTION
PHASE U0 — MASTER PRODUCT + UX + FRONTEND ARCHITECTURE BLUEPRINT

Work only in the CURRENT Lending repository.

THIS IS LENDING ONLY.

CCR IS OUT OF SCOPE.

Do not inspect, import, depend on, reference, or use CCR data, CCR customer master,
CCR routes, CCR relationship logic, or CCR product semantics for this work.

==================================================
MISSION
==================================================

Design the complete replacement user experience for Lending Relationship Intelligence.

This is NOT a restyling exercise.

The existing Lending frontend is a FUNCTIONAL REFERENCE ONLY for:

- working routes;
- existing capabilities;
- backend APIs;
- authority semantics;
- data contracts;
- governance rules;
- validated workflows.

It is NOT the design baseline.

Do NOT preserve the current:

- navigation structure;
- card layouts;
- page compositions;
- map design;
- network layout;
- table-first interaction model;
- filter placement;
- visual hierarchy;
- spacing system;
- component organization;
- old dashboard appearance;

unless the new product architecture independently justifies it.

The goal is a completely reconstructed institutional-grade Lending intelligence
application that is substantially more advanced, visually sophisticated,
interactive, clear, explainable and usable by senior lending professionals.

DO NOT IMPLEMENT THE NEW UI IN THIS TASK.

Produce the master architecture and reconstruction blueprint first.

==================================================
READ FIRST
==================================================

Inspect all currently available Lending implementation reports, especially where present:

backend/data/LENDING_IMPLEMENTATION_REBASELINE.md
backend/data/LENDING_PROMPT4A_EXECUTIVE_HOME_REPORT.md
backend/data/LENDING_PROMPT4B_PORTFOLIO_CLIENT_REPORT.md
backend/data/LENDING_PROMPT4C_NETWORK_REPORT.md
backend/data/LENDING_CCR_ISOLATION_REPORT.md

Also inspect the actual current code.

At minimum inspect:

frontend/package.json
frontend/src/App*
frontend/src/main*
frontend/src/components/
frontend/src/pages/
frontend/src/services/
frontend/src/hooks/
frontend/src/styles/
frontend/src/index.css

and relevant Lending backend routers/services/contracts under:

backend/app/

Do not rely only on reports.
Verify repository truth.

==================================================
NON-NEGOTIABLE DATA / GOVERNANCE CONTRACT
==================================================

The reconstruction must preserve validated Lending semantics.

CAM/V3
= authoritative Lending relationship truth.

V2
= fallback/history only.

Normalized operational/workbench data
= separate governed projection.

External research
= supplemental.

SEC / Web / Stylus evidence
= supplemental unless explicitly governed through the existing process.

Governed AI
= separate governed lane.

Review-required
= workflow state, NOT risk.

Reported OSUC
= source-reported exposure metric.

Do not invent:

- risk scores;
- materiality scores;
- systemic-risk scores;
- relationship-strength scores;
- probabilities;
- loss estimates;
- causal flows;
- exposure flows;
- unsupported relationship direction;
- unsupported entity geography;
- unsupported relationship completeness.

Zero, Unknown, Unavailable, Not Loaded, Filtered Out and Truncated must remain
distinct states.

Ordinary page loading must NOT automatically invoke:

- AI generation;
- SEC research;
- Web research;
- Stylus/provider execution;
- external proposals;
- expensive full-history relationship adaptation.

Research must be an explicit user action.

==================================================
PRODUCT DESIGN TARGET
==================================================

The new application should feel like a modern institutional intelligence system,
not a collection of admin pages.

Target characteristics:

- light, premium institutional design;
- high information density without clutter;
- strong typography and hierarchy;
- large analytical canvases;
- minimal unnecessary borders;
- sophisticated map and network interaction;
- smooth but restrained motion;
- advanced drill-down;
- strong search;
- contextual inspectors;
- evidence-first explainability;
- persistent investigation context;
- minimal configuration burden for senior users.

The experience should help a senior Lending user answer:

1. Where is our exposure?
2. Which clients matter most?
3. How are clients connected?
4. What relationships are governed by CAM?
5. Which relationships require review?
6. What external evidence exists?
7. What is missing?
8. What changed?
9. Why am I seeing this?
10. What should I investigate next?
11. What evidence supports the relationship?
12. Where did that evidence come from?

==================================================
PROPOSE THE NEW INFORMATION ARCHITECTURE
==================================================

Design the entire Lending product from scratch.

Evaluate and propose a coherent architecture that may include surfaces such as:

- Executive Intelligence
- Portfolio
- Geographic Intelligence
- Client 360
- Network Intelligence
- Relationship Intelligence
- Evidence / Lineage
- Events / Developments
- Attention / Review
- External Research
- Governed AI / Relationship Studio

Do not mechanically use those names if better product names exist.

Determine:

- global navigation;
- secondary navigation;
- contextual navigation;
- breadcrumb model;
- global search;
- persistent investigation context;
- client/entity switching;
- cross-page handoff behavior;
- URL-backed state.

The user should never feel that each page is a disconnected application.

==================================================
EXECUTIVE HOME
==================================================

Design a completely new executive opening experience.

The first screen should immediately communicate:

- portfolio exposure;
- client population;
- CAM coverage;
- relationship coverage;
- attention/review workload;
- meaningful deterministic signals;
- geographic context;
- relationship ecosystem context;
- recent developments where supported.

Do not simply recreate the current dashboard with prettier cards.

Propose a strong command-center composition with:

- executive indicators;
- major geographic visualization;
- small relationship-network preview;
- investigation signals;
- exposure concentration;
- coverage gaps;
- attention items;
- recent relationship/evidence changes if supported;
- clear next actions.

Every signal must state its deterministic basis.

==================================================
ADVANCED GEOGRAPHIC INTELLIGENCE
==================================================

The geographic map should become a major Lending analytical surface.

Evaluate the current frontend/backend and recommend an appropriate implementation,
potentially using technologies such as:

- MapLibre GL;
- deck.gl;
- WebGL overlays;
- clustering;
- aggregation;
- arc layers;
- density layers;

but only introduce technologies justified by the repository and desired capability.

The map architecture should support, where reliable data exists:

- portfolio exposure;
- client geography;
- related entity geography;
- country aggregation;
- sector filtering;
- relationship arcs;
- ecosystem highlighting;
- selected-client focus;
- selected-entity focus;
- event highlighting;
- geographic drill-down.

NEVER infer coordinates, domicile or headquarters where source data does not support them.

Define what happens when geography is unavailable.

Design interactions between:

MAP
NETWORK
CLIENT 360
RELATIONSHIP DETAIL

A selection on one surface should be capable of constraining/focusing the others.

==================================================
NETWORK EXPERIENCE — SIGNATURE PRODUCT FEATURE
==================================================

The Lending network must become one of the signature experiences.

Create TWO network experiences:

1. COMPACT NETWORK PREVIEW
2. FULL NETWORK INTELLIGENCE

--------------------------------------------------
COMPACT NETWORK PREVIEW
--------------------------------------------------

Use on surfaces such as:

- Executive Home;
- Client 360;
- relevant investigation views.

It should normally show only a small understandable ecosystem.

For example:

selected entity
+ most relevant first-degree relationships
+ limited important second-order context where justified.

It must NOT become a hairball.

Provide a clear:

EXPAND NETWORK

action.

--------------------------------------------------
FULL NETWORK INTELLIGENCE
--------------------------------------------------

Design a dedicated large network workspace.

Required capabilities should include:

- pan;
- zoom;
- fit;
- reset;
- semantic zoom;
- search;
- focus;
- node selection;
- edge selection;
- neighborhood expansion;
- branch collapse;
- controlled first-degree expansion;
- optional second-degree expansion;
- relationship-family filtering;
- source-layer filtering;
- review filtering;
- exposure filtering;
- sector filtering;
- geography filtering;
- path investigation where supported;
- graph/table synchronization;
- entity inspector;
- relationship inspector;
- evidence drill-down.

The network must NEVER default to rendering the entire relationship universe.

Use progressive disclosure.

Investigate suitable graph technologies already installed or potentially appropriate,
for example:

- Sigma.js;
- Cytoscape.js;
- WebGL-based graph layers;
- another justified high-performance React-compatible graph engine.

Do not recommend a library merely because it is fashionable.

Explain why the chosen architecture fits Lending.

==================================================
NETWORK CLARITY — HARD ACCEPTANCE RULE
==================================================

The graph must remain understandable.

Design for:

- collision avoidance;
- stable selection;
- deterministic grouping;
- intelligent label visibility;
- semantic zoom;
- edge aggregation where justified;
- node clustering where justified;
- progressive expansion;
- bounded graph size;
- visible truncation;
- relationship-family grouping;
- clear center/focus entity;
- explicit current investigation scope.

Do NOT scatter disconnected entities around the canvas.

Every primary-canvas node must have a visible reason for participating in the
current investigation.

If an entity is not connected under the current governed scope, do not show it as
an arbitrary floating node.

Instead expose the state:

NO GOVERNED CONNECTION CURRENTLY ESTABLISHED

and distinguish the reason:

- no CAM relationship;
- identity unresolved;
- relationship evidence unavailable;
- direction unresolved;
- state unresolved;
- filtered out;
- supplemental layer disabled;
- research not performed;
- graph bounded/truncated.

==================================================
NETWORK EDGE PROVENANCE — HARD RULE
==================================================

EVERY VISIBLE RELATIONSHIP EDGE MUST IDENTIFY ITS SOURCE DIRECTLY ON THE EDGE.

Examples:

CAM

SEC

WEB

AI

V2

CAM + SEC

CAM + WEB

SEC + WEB

CAM + SEC + WEB

The user must not need to open a tooltip just to know where a relationship came from.

Example:

COREWEAVE
      |
Supplier · CAM
      |
NVIDIA

or:

ENTITY A
      |
Customer · SEC
      |
ENTITY B

or:

ENTITY A
      |
Strategic Partner · CAM + SEC
      |
ENTITY B

The exact source semantics must remain correct.

SEC-only must not look like CAM.

Web-only must not look like CAM.

AI must not look like CAM.

V2 history must not look like CAM.

If CAM is corroborated by SEC:

CAM + SEC

may be displayed.

If several source classes support the same governed relationship, define an
unambiguous compact provenance label.

For dense zoom levels, define shorter edge-label behavior while preserving direct
source visibility.

==================================================
NETWORK EDGE MEANING
==================================================

Every relationship edge must expose:

- exact relationship type;
- optional UI relationship family;
- direction;
- relationship state;
- connectivity;
- authority/source lane;
- evidence count;
- source count;
- review state;
- provenance;
- why this edge is visible.

Where appropriate, direction should be visible with arrowheads.

Do not infer direction.

If direction is unresolved, render it explicitly as unresolved.

Do not use animated particles to imply money flow, operational flow or causality
unless the data genuinely supports such meaning.

==================================================
NODE MEANING
==================================================

Define distinct visual semantics for:

- portfolio client;
- governed related entity;
- review-related entity;
- external supplemental entity;
- governed AI/proposed entity;
- historical/fallback entity.

For portfolio clients:

node size MAY reflect reported exposure.

If so, explicitly state:

SIZE = REPORTED EXPOSURE

and never imply that size means risk.

Non-client entities should not be sized by invented importance.

Design badges/halos/borders for:

- CAM;
- review;
- external;
- AI;
- V2 history;

without creating excessive visual noise.

==================================================
NO CONNECTION → RESEARCH CONNECTION
==================================================

A missing governed connection must not become a dead end.

Design a first-class:

RESEARCH CONNECTION

workflow.

Example:

COREWEAVE ↔ ENTITY X

No governed connection currently established.

Current state:

CAM: no relationship available
SEC: not researched
WEB: not researched

Actions:

SEARCH SEC
SEARCH WEB
RUN EXTERNAL RESEARCH

The application should automatically carry:

- subject entity;
- counterparty;
- known identities;
- current relationship hypothesis if one exists;
- current CAM context;
- missing evidence;
- relevant dates;
- current investigation state.

Do NOT require the senior user to re-enter all this information.

Research is still an EXPLICIT user action.

Do not automatically run SEC/Web/provider requests merely because an edge is missing.

==================================================
EXTERNAL RESEARCH LIFECYCLE
==================================================

Design the lifecycle visually:

No governed connection
        ↓
Research connection
        ↓
SEC / Web / Stylus
        ↓
Evidence discovered
        ↓
Entity validation
        ↓
Relationship-semantic validation
        ↓
Supplemental relationship / proposal
        ↓
Review where required
        ↓
Governed state

External evidence must not silently mutate CAM.

Define how a newly discovered supplemental relationship appears in the graph.

It should be immediately distinguishable from CAM.

==================================================
CLIENT 360 — COMPLETE RECONSTRUCTION
==================================================

The existing Client Detail page is NOT the design baseline.

Design a completely new Client 360.

It should tell the story of the client.

Consider:

- client identity;
- reported exposure;
- share/rank;
- sector;
- geography;
- CAM coverage;
- relationship ecosystem;
- attention signals;
- major counterparties;
- relationship families;
- recent developments;
- evidence coverage;
- external research;
- review state.

A compact client network should be a major visual section.

Provide EXPAND NETWORK.

Design how the user moves from:

Client
→ Relationship
→ Evidence
→ Research
→ Review

without losing context.

==================================================
RELATIONSHIP INTELLIGENCE WORKSPACE
==================================================

Do not rebuild the existing Relationship Explorer as another table-heavy page.

Design a forensic relationship investigation workspace.

Consider a composition such as:

LEFT
relationship/entity navigator

CENTER
relationship visualization / evidence / lineage

RIGHT
contextual inspector

The workspace should make it easy to answer:

- what is the relationship?
- who are the endpoints?
- which direction?
- what state?
- what source?
- why was it classified this way?
- what evidence supports it?
- what evidence conflicts?
- what is under review?
- what changed?
- why not another taxonomy?
- which source document supports it?

Design explicit assertion/evidence lineage.

==================================================
WHY AM I SEEING THIS?
==================================================

Create a reusable explainability pattern throughout the product.

Important objects should have:

WHY AM I SEEING THIS?

This should explain deterministic factors such as:

- source;
- scope;
- authority lane;
- relationship type;
- endpoint identity;
- direction;
- review state;
- evidence count;
- filters;
- graph truncation;
- external inclusion.

Do not use generic AI prose when deterministic explanation is available.

==================================================
EVIDENCE EXPERIENCE
==================================================

Design evidence as a first-class object.

Users should be able to move:

relationship
→ assertion
→ evidence
→ source document
→ exact source location/excerpt

without leaving the investigation.

Design:

- source cards;
- source badges;
- evidence timeline where appropriate;
- exact excerpts;
- document identifiers;
- publication/as-of dates;
- conflicting evidence;
- corroborating evidence;
- unavailable evidence states.

==================================================
ATTENTION / REVIEW
==================================================

Reconstruct Review into a more useful ATTENTION CENTER.

Do not present 28 repetitive cards with equal visual importance.

Design deterministic categories such as:

- relationship review;
- evidence gaps;
- identity questions;
- direction/state questions;
- external conflicts;
- external proposals;
- governed AI approval.

Only use categories genuinely supported by data.

Do not classify something as high risk merely because it requires review.

Every item should explain:

WHY THIS REQUIRES ATTENTION

and provide immediate access to evidence.

==================================================
AI EXPERIENCE
==================================================

AI should become an integrated assistant, not another difficult configuration page.

Design a persistent:

ASK LENDING INTELLIGENCE

experience.

Examples:

Show me what connects NVIDIA to my largest exposures.

Show relationships under review for my largest technology clients.

Which portfolio clients have no CAM relationship intelligence?

Find external evidence for this relationship.

The UI response should preferably manipulate the product:

- focus map;
- focus network;
- set filters;
- open relevant clients;
- highlight relationships;
- show evidence;

rather than return only prose.

AI must respect governance.

Normal AI interaction must not silently create governed relationship truth.

==================================================
AI CREATE RELATIONSHIP
==================================================

Simplify relationship definition for senior users.

Primary experience:

DESCRIBE THE RELATIONSHIP YOU WANT TO IDENTIFY

Example:

Companies materially dependent on the same GPU supplier.

The system may propose:

relationship name;
relationship family;
endpoint semantics;
evidence requirements;
direction;
qualification logic;
review behavior.

Then show:

PREVIEW

before:

APPROVE / PUBLISH

Keep advanced configuration available behind:

ADVANCED CONFIGURATION

Do not force senior users to understand every low-level schema field.

==================================================
EVENTS / DEVELOPMENTS
==================================================

Design an Events / Developments concept that can eventually support, where governed
data exists:

- refinancing;
- acquisitions;
- major contracts;
- supplier disruption;
- ratings actions;
- regulatory developments;
- earnings developments;
- interest-rate context;
- bankruptcy;
- operational disruption;
- geopolitical events.

Do not fabricate event capability if the backend does not currently support it.

Explicitly classify this part of the blueprint as one of:

READY NOW
PARTIALLY READY
FUTURE DATA/ENGINE REQUIRED

Design how an event could highlight affected clients and relationship paths without
claiming guaranteed credit impact.

==================================================
FRONTEND TECHNOLOGY REVIEW
==================================================

Audit the current frontend stack first.

Then make a justified recommendation for the reconstruction.

Evaluate technologies such as, only where appropriate:

React + TypeScript
TanStack Query
TanStack Table
React Virtual
Zustand
MapLibre GL
deck.gl
Sigma.js
Cytoscape.js
Apache ECharts
Framer Motion
Web Workers

Do NOT add dependencies in this task.

For each recommended technology explain:

- capability;
- why Lending needs it;
- whether something already installed can provide it;
- bundle/performance implications;
- implementation risk;
- whether adoption is necessary or optional.

Prefer the smallest high-quality stack that achieves the design.

==================================================
DESIGN SYSTEM
==================================================

Specify a new design system.

Direction:

LIGHT
PREMIUM
INSTITUTIONAL
INTELLIGENCE-ORIENTED
CLEAR
HIGH-END ENTERPRISE ANALYTICS

Avoid generic Bootstrap/admin-dashboard appearance.

Define:

- typography;
- spacing;
- page grid;
- shell;
- navigation;
- command bar;
- surfaces;
- borders;
- elevation;
- drawers;
- inspectors;
- tooltips;
- badges;
- tables;
- charts;
- map controls;
- graph controls;
- empty states;
- loading states;
- error states;
- source labels;
- review labels.

Color semantics must be restrained and meaningful.

For example, conceptually:

neutral/navy
= primary institutional UI

blue/teal
= analytical emphasis

amber
= review/attention

red
= explicit conflict/error only

Do not assign colors that imply risk where no risk classification exists.

==================================================
MOTION
==================================================

Define restrained purposeful motion for:

- map transitions;
- graph focus;
- neighborhood expansion;
- panel transitions;
- investigation handoffs;
- loading skeletons.

Do not use decorative continuous animation that suggests live data or economic flow
when none exists.

Support reduced-motion preferences.

==================================================
PERFORMANCE ARCHITECTURE
==================================================

The new experience must remain fast with growing data.

Design:

- code splitting;
- lazy loading;
- bounded APIs;
- pagination;
- virtualization;
- graph edge/node caps;
- progressive graph fetch;
- first-degree neighborhood loading;
- controlled expansion;
- server-side aggregation;
- caching;
- stale-time strategy;
- cancelable requests;
- Web Workers where justified.

The browser must never load multi-gigabyte normalized artifacts.

Do not design the UI around unbounded 32,957-row relationship adaptation.

If a desired experience needs a new bounded read API, identify it explicitly.

Do not implement it yet.

==================================================
STATE MODEL
==================================================

Design explicit visual treatment for:

0

Unknown

Unavailable

Not Applicable

Not Loaded

Filtered Out

Truncated

No CAM Relationship

Review Required

Supplemental Only

Identity Unresolved

Direction Unresolved

State Unresolved

Evidence Unavailable

API Failure

Never collapse these into one generic empty state.

==================================================
RESPONSIVE + ACCESSIBILITY
==================================================

The primary environment is a professional desktop / large monitor.

Design for that first.

Also specify behavior for:

- laptop;
- narrower desktop;
- tablet-width where practical.

Ensure:

- keyboard navigation;
- visible focus;
- accessible map/graph alternatives;
- screen-reader labels;
- contrast;
- reduced motion;
- non-color-only status communication.

==================================================
RECONSTRUCTION STRATEGY
==================================================

Do NOT recommend destroying the working frontend and replacing it in one uncontrolled change.

Design a staged reconstruction.

Prefer a parallel/new shell or feature-flagged approach so the existing application remains
available until replacement surfaces pass validation.

Propose implementation phases.

A possible sequence to evaluate:

U1 — Design system + new shell
U2 — Executive Intelligence
U3 — Geographic Intelligence
U4 — Client 360
U5 — Network Intelligence
U6 — Relationship Intelligence
U7 — Attention / Review
U8 — Research + AI integration
U9 — Events / advanced analytics
U10 — performance/accessibility/release hardening

You may propose a better sequence after inspecting dependencies.

Each phase must have clear acceptance criteria.

==================================================
BACKEND GAP ANALYSIS
==================================================

For every major new UX capability classify backend readiness:

READY NOW

NEEDS SMALL BOUNDED READ API

NEEDS BACKEND ENHANCEMENT

FUTURE CAPABILITY

Examples to analyze:

executive metrics;
map aggregation;
country/sector drill-down;
network preview;
first-degree graph expansion;
graph counts;
source provenance;
CAM + SEC combinations;
evidence excerpts;
relationship lineage;
entity search;
path exploration;
events;
external research handoff;
AI interaction;
attention/review categories.

Do not invent APIs that already exist.

Inspect current repository first.

==================================================
VISUAL WIREFRAME SPECIFICATION
==================================================

For each major surface, provide a textual/ASCII wireframe showing:

- page hierarchy;
- major regions;
- map/network placement;
- command controls;
- inspectors;
- indicators;
- evidence areas;
- interactions.

At minimum:

Executive Intelligence
Portfolio
Geographic Intelligence
Client 360
Network Intelligence
Relationship Intelligence
Attention Center
External Research
AI Relationship Studio

These are architecture wireframes, not final pixel-perfect designs.

==================================================
FINAL REPORT
==================================================

Create:

backend/data/LENDING_UI_RECONSTRUCTION_BLUEPRINT.md

The report must include:

1. Executive product vision
2. Existing frontend diagnosis
3. Capabilities worth preserving
4. Components/layouts that should be replaced
5. Proposed information architecture
6. Navigation model
7. Design system
8. Executive Home architecture
9. Geographic Intelligence architecture
10. Network Preview architecture
11. Full Network Intelligence architecture
12. Network anti-hairball strategy
13. Node semantics
14. Edge semantics
15. DIRECT EDGE PROVENANCE LABEL rules
16. CAM / SEC / WEB / AI / V2 visual semantics
17. No-connection / Research Connection workflow
18. Client 360 architecture
19. Relationship Intelligence architecture
20. Evidence / lineage experience
21. Attention Center
22. External Research experience
23. AI assistant
24. AI relationship creation
25. Events / future intelligence
26. frontend technology recommendation
27. performance architecture
28. accessibility
29. responsive behavior
30. backend readiness matrix
31. required bounded API enhancements
32. staged reconstruction plan
33. acceptance criteria per implementation phase
34. known limitations
35. explicit deferred capabilities

Also include visual ASCII wireframes for all principal surfaces.

==================================================
MANDATORY QUESTIONS TO ANSWER
==================================================

The report must explicitly answer:

1. What should the completely reconstructed Lending product look and feel like?

2. Which existing frontend concepts should be discarded?

3. Which existing functional capabilities should be preserved?

4. What technology should power the geographic map and why?

5. What technology should power the relationship network and why?

6. How will the graph prevent a hairball?

7. What is the maximum/default network scope before progressive expansion?

8. How will a small Network Preview differ from Full Network Intelligence?

9. How will edge labels visibly show:
   CAM
   SEC
   WEB
   AI
   V2
   combinations such as CAM + SEC?

10. What happens visually when there is NO governed connection?

11. How does the user launch SEC/Web/Stylus research from that missing connection?

12. How are supplemental research results shown without pretending they are CAM?

13. How does a user move from:
    Map
    → Network
    → Client
    → Relationship
    → Evidence
    → Source
    → Research
    → Review
    without losing context?

14. Which capabilities are ready using today's APIs?

15. Which require small bounded backend APIs?

16. Which should be deferred?

17. How should the reconstruction be implemented without destabilizing the
    currently working Lending application?

==================================================
STRICT NON-GOALS
==================================================

DO NOT:

- implement the reconstruction yet;
- modify backend business logic;
- modify source data;
- change CAM/V3 authority;
- change relationship truth;
- create synthetic relationships;
- create synthetic metrics;
- create risk scores;
- add external relationships;
- run SEC;
- run Web research;
- run Stylus;
- run AI generation;
- modify CCR;
- read CCR as a Lending source;
- introduce dependencies in package.json;
- start page-by-page coding.

This task is the architecture/design blueprint only.

==================================================
STOP CONDITION
==================================================

Stop after the report.

Do not start U1.

The final line of the report must be exactly:

READY FOR LENDING UI RECONSTRUCTION U1
