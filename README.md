LENDING UI RECONSTRUCTION — U2
FULL NETWORK INTELLIGENCE

THIS IS AN IMPLEMENTATION TASK.

DO NOT WRITE ANOTHER DESIGN BLUEPRINT.
DO NOT WRITE ANOTHER ARCHITECTURE AUDIT.
DO NOT STOP AFTER ANALYSIS.

YOU MUST MODIFY THE RUNNING FRONTEND AND, ONLY WHERE REQUIRED FOR BOUNDED READS,
THE LENDING BACKEND.

THE RESULT MUST BE VISIBLY RUNNABLE IN THE BROWSER.

============================================================
READ FIRST
============================================================

Read:

backend/data/LENDING_UI_RECONSTRUCTION_BLUEPRINT.md
backend/data/LENDING_UI_U1_IMPLEMENTATION_REPORT.md
backend/data/LENDING_CURRENT_PRODUCT_ARCHITECTURE_AUDIT.md

Current source overrides older reports.

This is LENDING ONLY.

Never use CCR data, CCR relationship truth, Customer_latest.parquet, or
customer-master values.

============================================================
MISSION
============================================================

Completely reconstruct Network Intelligence into a premium institutional
relationship-intelligence workspace.

The current Network page is only a transitional implementation.

U2 must create the real Network Intelligence product.

This is NOT a cosmetic reskin.

The finished surface should feel comparable to a premium capital-markets,
cyber-intelligence, investigative-graph, or institutional research product,
while retaining the LIGHT visual language already selected for Lending.

The experience must be:

- visually sophisticated;
- spatially clear;
- fast;
- bounded;
- evidence-first;
- relationship-centric;
- usable by a senior credit professional;
- highly interactive;
- readable without training;
- deterministic;
- source-aware.

============================================================
MANDATORY VISUAL OUTCOME
============================================================

The Network experience must occupy the available workspace.

Do NOT render:

- a small graph floating in a generic card;
- a giant blank white page;
- a basic SVG demo;
- disconnected decorative nodes;
- a dashboard containing many equal-weight boxes.

The network is the primary visual surface.

Target approximate layout:

┌─────────────────────────────────────────────────────────────────────┐
│ Global Lending command bar                             ASK LENDING │
├─────────────────────────────────────────────────────────────────────┤
│ Context / source lanes / current focus / bounds                    │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│   NETWORK CANVAS                                      INSPECTOR     │
│                                                     ┌────────────┐ │
│         related entity                              │ Selected   │ │
│              ○                                      │ entity /   │ │
│             / CAM                                   │ relation   │ │
│            /                                        │ evidence   │ │
│      ○────●────○ SEC                                │ provenance │ │
│          focus                                      │ actions    │ │
│            \                                        └────────────┘ │
│             \ CAM REVIEW                                            │
│              ○                                                      │
│                                                                     │
│   [ + ] [ - ] [ fit ] [center] [layout] [filters] [map] [table]   │
├─────────────────────────────────────────────────────────────────────┤
│ visible count · returned count · truncated · degree · source lanes │
└─────────────────────────────────────────────────────────────────────┘

The inspector may collapse so the canvas can become wider.

============================================================
FULLSCREEN / EXPANDED NETWORK
============================================================

MANDATORY.

The compact network shown elsewhere in Lending must have:

EXPAND NETWORK

When selected, it opens the full Network Intelligence workspace.

Inside Network Intelligence provide:

FULLSCREEN / FOCUS MODE

When activated:

- collapse/minimize the Lending navigation rail;
- collapse secondary descriptive text;
- maximize the graph canvas;
- keep graph controls;
- preserve Ask Lending;
- preserve source legend;
- preserve inspector access;
- preserve exit/back control.

The user must be able to comfortably investigate the graph across nearly the
entire screen.

============================================================
NETWORK IS FOCUS-BASED
============================================================

Do not draw the full universe by default.

Require an explicit focus entity.

Default degree = 1.

The focus entity appears centrally.

First-degree connected entities appear around it.

Expansion is explicit.

Never render arbitrary disconnected entities.

If there are no governed first-degree connections, show:

NO GOVERNED CONNECTION CURRENTLY ESTABLISHED

and provide explicit investigation/research actions.

Do not manufacture a graph to fill empty space.

============================================================
GRAPH TECHNOLOGY
============================================================

The current audit confirmed that the active graph is hand-authored SVG and
multiple SVG graph implementations now coexist.

For U2, consolidate Network around ONE reusable graph implementation.

Evaluate whether a focused graph library already exists in the dependency tree.

If none does, it is acceptable in U2 to add ONE justified graph dependency,
preferably:

@xyflow/react

IF it materially improves:

- viewport controls;
- custom nodes;
- custom edges;
- label placement;
- accessibility;
- interaction;
- future maintainability.

Do not add an entire visualization framework merely for decoration.

If a dependency is added, document why.

============================================================
GRAPH QUALITY
============================================================

The graph must be extremely legible.

Every visible node must have:

- identity;
- readable label;
- node type;
- relationship attachment;
- source-supported state.

Every visible node other than the focus must be connected by a visible edge.

No arbitrary floating nodes.

No hidden inferred paths.

No fake relationship strength.

No force-layout motion after initial placement.

Use a deterministic radial/layered structure.

For degree 1:

             Entity
                ○
             CAM│
                │
     Entity ○───●───○ Entity
             SEC focus CAM REVIEW
                │
                ○
             Entity

For expanded branches, preserve visual ancestry and avoid overlapping labels.

============================================================
NODE DESIGN
============================================================

Nodes should be designed objects, not plain dots.

FOCUS NODE:

- visually strongest;
- entity/client name;
- compact type indicator;
- optional reported OSUC if it is a portfolio client;
- clear CAM availability state;
- subtle glow/halo is allowed.

PORTFOLIO CLIENT:

- distinct outline;
- CAGID available in inspector;
- exposure may affect limited node size ONLY when explicitly labelled
  EXPOSURE CONTEXT;
- node size must never imply risk.

RELATED ENTITY:

- neutral institutional treatment;
- name visible;
- entity type if known.

REVIEW node/relationship:

- amber workflow treatment.

External:

- separate supplementary styling.

AI:

- separate governed AI styling.

V2:

- clearly fallback/history.

============================================================
EDGE DESIGN — CRITICAL
============================================================

Every relationship edge must expose provenance.

This is mandatory.

If the relationship is CAM/V3:

       CAM

must appear on or immediately next to the edge.

If CAM review-required:

       CAM · REVIEW

If external SEC evidence:

       SEC

If external Web:

       WEB

If governed AI:

       AI

If V2 fallback:

       V2

If multiple retained assertions independently support a displayed connection:

       CAM + SEC

may be displayed ONLY as an inventory shorthand.

It does NOT mean SEC has become CAM.

The inspector must show the assertions independently.

Also show relationship type where space permits.

Example:

 NVIDIA ───────────── TSMC
          SUPPLIER
             CAM

or

 COMPANY A ───────── COMPANY B
          CUSTOMER
         CAM · REVIEW

Direction arrows appear ONLY when direction is actually source-supported.

Unknown direction = undirected edge.

============================================================
EDGE INTERACTION
============================================================

Hover:

- visually emphasize edge;
- emphasize both endpoints;
- show compact tooltip:
    relationship type
    source
    direction
    state
    evidence count

Click:

open the Relationship Inspector.

Inspector should contain:

Relationship
Subject
Related entity
Exact relationship type
Family
Direction
Connectivity
State
Authority
Source lane
Review state
Evidence count
Source references
Exact excerpts where available
Lineage status
Limitations

Provide:

OPEN RELATIONSHIP INTELLIGENCE

OPEN EVIDENCE

RESEARCH CONNECTION

when appropriate.

============================================================
NODE INSPECTOR
============================================================

Clicking a node opens a sophisticated right-side drawer.

For portfolio clients include:

name
CAGID
sector
country label
reported OSUC
portfolio share if available
CAM availability
relationship count
review-required count

Actions:

OPEN CLIENT 360
CENTER NETWORK
EXPAND FIRST DEGREE
VIEW RELATIONSHIPS
VIEW EVIDENCE
RESEARCH CONNECTION

For non-client entities show only fields actually available.

Do not invent missing data.

============================================================
SOURCE LANE CONTROLS
============================================================

At the top of Network provide visible source-lane controls.

Default:

CAM/V3 ON

Review CAM may be visible with CAM but visually distinct.

External OFF
AI OFF
V2 OFF

Controls:

[ CAM ]
[ REVIEW ]
[ SEC / WEB ]
[ AI ]
[ V2 HISTORY ]

Turning a lane on may fetch/show that lane only if supported.

It must never silently call a provider.

External means persisted/cached external results.

It does NOT mean execute external research.

============================================================
MISSING CONNECTION WORKFLOW
============================================================

This is a major product capability.

If the user selects or searches two entities for which no governed connection
is currently established:

show clearly:

NO GOVERNED CONNECTION CURRENTLY ESTABLISHED
IN THE SELECTED SCOPE

Then explain:

CAM relationship:
Not established / unavailable / unresolved as appropriate

Cached external evidence:
present / none

SEC research:
not performed / cached / unavailable

Web research:
not performed / cached / unavailable

Stylus:
status only

R2D2:
status only

DO NOT automatically call any provider.

Provide button:

RESEARCH CONNECTION →

This navigates to Research with prepared context.

============================================================
PREPARED RESEARCH CONTEXT
============================================================

Carry:

subject identity
counterparty identity
CAGIDs where applicable
known aliases
relationship hypothesis
CAM status
known relationship IDs
source excerpts
missing evidence fields
country/sector context
selected scope
requested channel options

Do not execute research merely through navigation.

============================================================
GEOGRAPHY MODE
============================================================

Network must include:

GRAPH
MAP
TABLE

as first-class views.

MAP should use the existing local geography assets and current source labels.

The map should be much more visually refined than the current version.

LIGHT APPLICATION SHELL
+
DARK CARTOGRAPHIC CANVAS

is acceptable and preferred.

The map should look luminous/shiny but still analytical.

Use restrained:

- teal/cyan;
- gold/amber;
- subtle glows;
- highlighted geography;
- point halos.

No neon game aesthetic.

============================================================
GEOGRAPHIC NETWORK
============================================================

Where BOTH endpoints have reliable mapped geography AND an actual relationship
record supports the connection, allow relationship arcs on the map.

Do not fabricate geography.

Do not infer HQ.

Do not infer domicile.

Do not render arcs for unresolved locations.

Arc provenance must remain inspectable.

CAM arc:
CAM

SEC arc:
SEC

etc.

============================================================
SHINY MAP TREATMENT
============================================================

Implement a premium geographic canvas:

- dark navy/cartographic background;
- muted continents;
- subtle borders;
- restrained luminous active countries;
- haloed mapped entity points;
- selected country focus;
- animated hover transition only;
- no continuous decorative particle flow;
- source-aware relationship arcs;
- selected-client marker;
- tooltips;
- zoom/pan;
- fit-to-visible selection.

The surrounding application remains light.

This contrast is intentional.

============================================================
TABLE VIEW
============================================================

Provide a synchronized relationship table below or instead of the graph.

Columns where available:

Subject
Related Entity
Relationship Type
Family
Direction
State
Connectivity
Source
Evidence
Review
Action

Clicking a row selects the corresponding graph edge.

Clicking a graph edge selects the corresponding row.

============================================================
NETWORK SEARCH
============================================================

Provide focus search.

It must search only what the backend actually supports.

At minimum support portfolio client name and CAGID.

If entity/relationship search is not yet supported by a bounded backend
contract, DO NOT fake it.

Instead state the limitation and implement the smallest bounded read adapter
needed if justified.

Never query the full 2.855 GB normalized artifact merely to perform a search.

============================================================
BOUNDS
============================================================

Initial focused graph:

maximum approximately:
50 nodes
100 edges

Expansion:

maximum approximately:
+50 nodes
+100 edges per explicit request

Hard browser-rendering ceiling:

250 nodes
500 edges

If actual current bounded backend capabilities require a smaller practical
limit, use the safer bound.

Server response should expose if feasible:

returned
available
has_more
truncated
truncation_reason

UI must surface truncation.

Never pretend the displayed graph is complete when it is bounded.

============================================================
PERFORMANCE — HARD RULE
============================================================

U2 MUST NOT make the browser load:

backend/data/lending_relationship_database.json

or any equivalent ~2.855 GB / 32,957-row artifact.

It must not materialize that entire universe before applying a limit.

Do not use the broad legacy group endpoint as initial Network loading.

Network must be based on bounded CAM/V3-first reads.

Any backend work performed for U2 must be:

Lending-only
read-only
source-lane aware
bounded before expensive processing
paginated/limited
deterministic
tested

============================================================
CURRENT V3 AUTHORITY
============================================================

Preserve:

41 CAM/V3 relationship rows
13 canonical
28 review-required

Do not inflate the visible authoritative network using V2 or normalized history.

Review-required remains source/workflow state.

It is NOT a risk rating.

============================================================
AI ACCESS WINDOW
============================================================

Preserve and visually improve:

ASK LENDING INTELLIGENCE

as a persistent upper-right entry point.

During U2 it may remain provider-free if the current implementation is not yet
model-backed.

But redesign its UI architecture so it is context-aware.

Opening it from Network should show:

Current focus
Selected node
Selected relationship
Current degree
Visible source lanes
Filters
Graph bounds
Current view

Suggested questions may include:

"What relationships are visible for this client?"
"Why is this connection review-required?"
"What evidence supports this edge?"
"Which visible relationships are CAM authoritative?"
"Show me the relationship between NVIDIA and TSMC."

IMPORTANT:

Until U4 implements model-backed orchestration, DO NOT pretend this is an LLM.

If the requested answer cannot be resolved from current bounded reads, provide
a navigation/research action instead.

============================================================
FUTURE AI-CONTROL COMPATIBILITY
============================================================

Structure Network actions so U4 can later call typed UI commands such as:

focusEntity(id)
selectRelationship(id)
expandNode(id)
setDegree(1|2)
setView(graph|map|table)
toggleLane(CAM|REVIEW|EXTERNAL|AI|V2)
openEvidence(id)
prepareResearch(subject, counterparty)

Do NOT implement uncontrolled natural-language mutation.

============================================================
VISUAL QUALITY
============================================================

This cannot look like the current generic React dashboard.

Required qualities:

- premium financial/institutional product;
- refined typography;
- strong information hierarchy;
- generous canvas;
- deliberate whitespace;
- compact utility chrome;
- smooth drawer transitions;
- subtle depth;
- clear selected states;
- crisp graph typography;
- custom icons where useful;
- restrained source colors;
- excellent hover/focus states.

Avoid:

- endless identical cards;
- Bootstrap-like boxes;
- giant bordered rectangles;
- default HTML-looking buttons;
- primitive tabs;
- weak typography;
- oversized empty areas;
- admin-console styling.

============================================================
RESPONSIVE BEHAVIOR
============================================================

Desktop:
full canvas + inspector.

Medium width:
canvas + overlay inspector.

Small width:
graph remains usable;
inspector becomes bottom sheet;
rail collapses.

============================================================
ACCESSIBILITY
============================================================

Support:

keyboard focus
visible focus states
node selection by keyboard where practical
edge selection where practical
semantic controls
tooltips not hover-only
reduced-motion preference
adequate contrast

============================================================
BACKEND CHANGES
============================================================

Backend changes are permitted ONLY if necessary for the bounded U2 contract.

Possible justified additions:

- focused network endpoint;
- bounded entity search;
- bounded expansion endpoint;
- returned/available/truncation metadata.

Do NOT:

- create another relationship store;
- change authority semantics;
- migrate CAM;
- merge V2 into V3;
- alter research providers;
- alter AI publication;
- alter review semantics.

============================================================
TESTS
============================================================

Add focused tests for:

- CAM/V3-first graph;
- explicit focus;
- first-degree loading;
- review styling;
- source provenance;
- direction handling;
- unresolved direction;
- node/edge bounds;
- truncation;
- source-lane toggles;
- no disconnected nodes;
- no automatic external/provider call;
- no AI/provider invocation;
- no full normalized artifact read;
- focus change;
- expansion;
- empty relationship state.

Frontend:

npm run build
npm run lint

Do not claim visual validation unless actually performed.

============================================================
MANUAL VISUAL CASES
============================================================

Verify if environment permits:

1. default Network with no focus;
2. focus client with CAM relationship;
3. focus client with review-required relationship;
4. client with no governed connection;
5. edge selected;
6. node selected;
7. expanded graph;
8. MAP view;
9. TABLE view;
10. source toggle;
11. fullscreen Network;
12. narrow screen;
13. Ask Lending opened from a selected relationship.

============================================================
OUTPUT REPORT
============================================================

Create:

backend/data/LENDING_UI_U2_FULL_NETWORK_REPORT.md

Document:

- changed files;
- graph architecture;
- map architecture;
- APIs;
- bounds;
- authority handling;
- source labels;
- edge provenance;
- inspector behavior;
- missing-connection workflow;
- Ask integration;
- tests;
- build/lint;
- performance;
- limitations;
- screenshots/manual validation if available.

State explicitly:

DOES ORDINARY NETWORK LOAD OR MATERIALIZE THE FULL 32,957-ROW /
2.855-GB NORMALIZED ARTIFACT?

The answer must be NO for U2 to pass.

============================================================
STOP CONDITION
============================================================

Do not start Relationship Intelligence U3.

Do not start model-backed Ask Lending U4.

Do not repair Stylus or activate R2D2.

Do not redesign Research.

Stop after U2 implementation and validation.

Final line must be exactly:

READY FOR LENDING UI RECONSTRUCTION U3
