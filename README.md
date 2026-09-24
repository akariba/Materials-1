LENDING TOTAL UI RECONSTRUCTION — U1
BUILD THE NEW PRODUCT NOW

Work only in the CURRENT Lending repository.

READ FIRST:

backend/data/LENDING_UI_RECONSTRUCTION_BLUEPRINT.md

The U0 blueprint is APPROVED.

THIS IS NOT A PLANNING TASK.
THIS IS NOT A REPORT-ONLY TASK.
START WRITING FRONTEND CODE.

==================================================
MISSION
==================================================

Begin the TOTAL reconstruction of the Lending frontend.

The existing Lending UI is only a functional reference for:

- working APIs;
- routes;
- data contracts;
- authority rules;
- validated functionality.

It is NOT the visual baseline.

The finished U1 must visibly look like a NEW premium institutional
Lending Intelligence product.

Do not merely improve CSS on the existing pages.

==================================================
U1 MUST BUILD
==================================================

Build and mount:

1. NEW Lending Intelligence application shell
2. NEW institutional left navigation rail
3. NEW global search / command bar
4. NEW persistent context strip
5. NEW Executive Intelligence landing page
6. NEW metric/exposure/coverage presentation
7. NEW Attention / Investigation area
8. NEW shiny Geographic Intelligence preview
9. NEW compact Relationship Network preview
10. NEW contextual inspector drawer
11. NEW source-lane / authority visual system
12. NEW persistent "Ask Lending Intelligence" access point
13. Responsive desktop/laptop layouts
14. Explicit loading / unavailable / zero / truncated states

The implementation must be mounted on the active Lending route.

==================================================
ROUTES
==================================================

Make:

/lending

the NEW Executive Intelligence landing experience.

Also support:

/lending/intelligence

for the same Executive Intelligence experience if compatible with the
existing router.

Preserve existing working routes during migration.

New primary navigation should represent:

EXECUTIVE
PORTFOLIO
GEOGRAPHY
NETWORK
RELATIONSHIPS
ATTENTION
RESEARCH
STUDIO

Do not expose Events as an active capability unless supported by actual data.

==================================================
VISUAL DIRECTION
==================================================

Use a LIGHT premium institutional design.

The application should feel closer to a modern intelligence terminal than
an admin dashboard.

Visual character:

- warm near-white background;
- white analytical surfaces;
- deep ink/navy typography;
- sophisticated blue/teal accents;
- generous whitespace;
- very clean separators;
- restrained shadows;
- large analytical canvases;
- editorial hierarchy;
- compact high-information controls;
- minimal unnecessary cards.

Authority/source colors:

CAM/V3        = petrol / teal
Review        = amber
SEC           = blue
WEB           = ochre / gold
Governed AI   = violet
V2/history    = slate
Error/conflict = red only when actually supported

Do NOT use red for exposure.
Do NOT imply risk through color.

==================================================
NEW PRODUCT SHELL
==================================================

Build a completely new shell.

LEFT RAIL

Include:

Lending Intelligence

Executive
Portfolio
Geography
Network
Relationships
Attention
Research
Studio

Requirements:

- polished active state;
- collapsible behavior;
- keyboard accessible;
- strong premium visual hierarchy;
- no recreation of the old horizontal menu.

TOP COMMAND BAR

Include:

- global Lending search;
- current scope;
- CAM/V3 authority status;
- attention indicator;
- ASK LENDING INTELLIGENCE access.

CONTEXT STRIP

Show compactly:

- current population/scope;
- selected focus where applicable;
- active source lanes;
- filters;
- bounded/truncated state;
- as-of information where actually available;
- read-only/explicit-action state.

==================================================
EXECUTIVE INTELLIGENCE
==================================================

Rebuild the Landing page entirely.

Do not preserve the old dashboard layout.

Create a strong top-level Executive Intelligence experience.

Use real existing Lending API values.

Present a concise metric band using meaningful existing values such as:

- portfolio clients;
- reported OSUC;
- clients with CAM;
- clients without CAM;
- canonical CAM/V3 relationships;
- review-required CAM/V3 relationships.

Do NOT fabricate values.

Reported OSUC must visibly state:

SOURCE-REPORTED / SUPPLEMENTAL

Review-required must state:

WORKFLOW STATE — NOT RISK

CAM coverage must not imply CAM freshness.

==================================================
ATTENTION / INVESTIGATION
==================================================

Create a premium editorial attention surface.

Use only deterministic existing conditions such as:

- review-required CAM/V3 relationships;
- large reported exposure without CAM;
- missing relationship information;
- unresolved context;
- evidence limitations.

Do not invent:

HIGH RISK
MEDIUM RISK
LOW RISK

Every attention item should answer:

WHY AM I SEEING THIS?

and provide a relevant action.

==================================================
SHINY GEOGRAPHIC INTELLIGENCE PREVIEW
==================================================

This is a major visual requirement.

Create an attractive, modern geographic intelligence preview on the
Executive page.

It should visually approach a premium global intelligence map:

- polished world geometry;
- soft luminous points/markers where actual data supports locations;
- restrained glow;
- cluster/aggregation behavior where useful;
- elegant hover/focus states;
- region/country context;
- reported exposure and/or client counts;
- clean controls;
- high-quality zoom/focus behavior.

The surrounding UI remains LIGHT.

The map itself MAY use a darker high-contrast visualization surface if that
produces the premium luminous global-map treatment requested.

Do not create fake cities or coordinates.

Do not infer headquarters.

Do not infer country risk.

Do not draw relationship arcs unless both endpoint geography and relationship
data actually support the arc.

If current geography only supports country-level data, use country-level
mapping honestly.

Add:

OPEN GEOGRAPHIC INTELLIGENCE →

Full Geography reconstruction will be a later phase.

==================================================
COMPACT NETWORK PREVIEW
==================================================

Build a beautiful compact network preview.

This is NOT the final full-screen Network workspace.

The compact graph should show:

- one selected/focus entity;
- first-degree governed relationships;
- at most 13 visible nodes including focus;
- at most 24 visible edges;
- no disconnected nodes;
- clean deterministic positioning;
- no graph hairball;
- no continuous force-layout motion.

If no safe focus exists:

show:

SELECT A CLIENT TO EXPLORE ITS RELATIONSHIP ECOSYSTEM

with bounded client search.

==================================================
NETWORK SOURCE LABELS — HARD REQUIREMENT
==================================================

EVERY visible relationship line must display provenance directly on the edge.

Examples:

Supplier · CAM

Parent · CAM

Customer · SEC

Strategic Partner · WEB

Relationship · AI

Historical · V2

Supplier · CAM + SEC

Do not rely on colors alone.

If actual production data currently contains only CAM relationships, show CAM.

Do NOT create fake SEC, Web, AI, or V2 examples merely to demonstrate styling.

==================================================
NETWORK INTERACTION
==================================================

Click node:

- focus/highlight node;
- open useful client/entity context.

Click relationship edge:

open InspectorDrawer.

Inspector should show available real fields:

- subject;
- related entity;
- relationship type;
- direction;
- state;
- connectivity;
- source;
- review state;
- evidence count;
- source references;
- WHY AM I SEEING THIS?

==================================================
EXPAND NETWORK
==================================================

The compact network must have a prominent:

EXPAND NETWORK →

control.

Navigate to:

/lending/network?focus=<safe-focus-id>

Preserve investigation context.

The full-screen advanced Network Intelligence canvas will be built in the
NEXT reconstruction phase.

Do not implement a fake full network in U1.

==================================================
NO CONNECTION
==================================================

Do NOT show random isolated graph nodes.

If a selected client has no governed connection:

display:

NO GOVERNED CONNECTION CURRENTLY ESTABLISHED

Then show the actual known reason, where supported:

- no CAM relationship;
- review-only state;
- identity unresolved;
- evidence unavailable;
- supplemental lane disabled;
- filtered out;
- graph truncated;
- research not performed.

Provide:

RESEARCH CONNECTION →

Do not automatically invoke a provider.

==================================================
ASK LENDING INTELLIGENCE
==================================================

Build a persistent AI entry point in the shell:

ASK LENDING INTELLIGENCE

It should appear in the command bar and be available from the new
Executive experience.

Clicking it opens a polished right-side assistant drawer while keeping the
current page visible.

The assistant drawer must be designed to eventually understand UI context.

Create the UI-context contract now, including safe state such as:

- active route;
- selected client/entity;
- selected relationship;
- current filters;
- source lanes;
- geographic scope;
- selected network node;
- selected network edge;
- current bounded/truncated state.

If an existing governed AI read interface can safely answer a question without
changing authority semantics, wire it appropriately.

Otherwise build the assistant UI/context infrastructure now and clearly identify
unavailable actions rather than fabricating responses.

The assistant must NEVER silently create relationship truth.

Example future query:

"What is the relationship between NVIDIA and TSMC?"

Expected product behavior:

1. Search current Lending governed/supplemental relationship data.
2. If a relationship exists:
   - focus the entities;
   - highlight the edge;
   - show exact relationship type;
   - show CAM / SEC / WEB / AI / V2 provenance;
   - offer Evidence.
3. If no governed connection exists:
   display:

   NO GOVERNED CONNECTION CURRENTLY ESTABLISHED

   and offer:

   RESEARCH CONNECTION

Do not answer from generic model knowledge and silently create a Lending edge.

==================================================
AI UI ACTION MODEL
==================================================

Prepare the frontend architecture so Ask Lending Intelligence can eventually
perform safe UI actions such as:

- navigate;
- search;
- focus client;
- focus entity;
- set filters;
- select relationship;
- focus network;
- show geography;
- open evidence;
- open inspector;
- explain visible deterministic information.

These are READ/NAVIGATION actions.

Do NOT add hidden provider execution.

Actions such as:

- SEC research;
- Web research;
- Stylus/provider call;
- creating proposals;
- approving;
- publishing;
- changing review state;

must remain explicit user-confirmed actions.

==================================================
SHARED COMPONENTS
==================================================

Do not continue growing the existing monolithic page implementation.

Create a clean reconstruction structure under frontend/src.

Use repository conventions, but establish reusable equivalents of:

ProductShell
PrimaryRail
CommandBar
CommandSearch
ContextStrip
MetricBand
SourceLaneBadge
AuthorityBadge
StateBadge
BoundedResultNotice
InspectorDrawer
NetworkLegend
AskLendingDrawer
EmptyState
UnavailableState

Do not create meaningless wrapper components.

==================================================
DATA CONTRACT
==================================================

Use only bounded existing Lending APIs.

Preserve:

CAM/V3
= authoritative Lending relationship truth.

V2
= fallback/history.

External SEC/Web
= supplemental.

Governed AI
= separate governed lane.

Review-required
= workflow state, not risk.

Reported OSUC
= source-reported/supplemental.

Do NOT read or depend on:

CCR
Customer_latest
CCR customer master
CCR relationship data.

==================================================
PERFORMANCE
==================================================

Ordinary /lending load must NOT:

- load full normalized 32,957-row history;
- adapt the ~2.8 GB normalized artifact;
- call broad semantic groups that materialize everything first;
- run AI generation;
- call SEC;
- call Web;
- call Stylus;
- invoke external providers;
- create proposals;
- mutate data.

Use bounded existing API reads.

==================================================
STATE SEMANTICS
==================================================

Visually distinguish:

LOADING
EMPTY
NOT ESTABLISHED
REVIEW REQUIRED
UNRESOLVED
SUPPLEMENTAL
NOT PERFORMED
DISABLED
TRUNCATED
UNAVAILABLE
ERROR

Do not show 0 until a successful bounded request establishes 0.

==================================================
RESPONSIVE DESIGN
==================================================

Prioritize professional large displays.

Validate at minimum:

- large monitor;
- 1440px desktop;
- standard laptop;
- narrow desktop/tablet-like width.

Rail may collapse at narrower sizes.

Inspector may become a bottom sheet.

Map/network must remain usable.

==================================================
VALIDATION
==================================================

After implementation:

1. run frontend build;
2. run lint;
3. fix all NEW errors;
4. start the application;
5. open /lending;
6. visually inspect the page;
7. verify real data;
8. test navigation;
9. test search;
10. test geographic preview;
11. focus a client in the compact network;
12. click an edge;
13. verify inspector;
14. verify direct CAM/SEC/WEB provenance labels;
15. open Ask Lending Intelligence drawer;
16. test responsive widths;
17. inspect request traces.

Confirm ordinary page load made NO automatic:

AI
SEC
Web
Stylus
provider
proposal
mutation
full-normalized-history

requests.

==================================================
IMPLEMENTATION REPORT
==================================================

Only AFTER implementation is finished, create:

backend/data/LENDING_UI_U1_IMPLEMENTATION_REPORT.md

Keep the report concise.

Include:

- frontend files created/changed;
- new shell structure;
- Executive Intelligence implementation;
- geographic preview;
- compact network;
- edge provenance behavior;
- Ask Lending Intelligence implementation;
- APIs used;
- request trace;
- build/lint results;
- visual/browser validation;
- limitations;
- remaining U2 work.

==================================================
SUCCESS CRITERIA
==================================================

U1 is NOT complete unless:

[ ] /lending visibly looks like a completely new product
[ ] old dashboard composition is replaced
[ ] new rail exists
[ ] new command bar exists
[ ] context strip exists
[ ] Executive Intelligence uses real data
[ ] shiny geographic preview is visible
[ ] compact relationship network is visible
[ ] graph contains no arbitrary disconnected nodes
[ ] CAM appears directly on CAM edges
[ ] SEC appears directly on actual SEC edges
[ ] WEB appears directly on actual Web edges
[ ] source lanes cannot masquerade as CAM
[ ] edge Inspector works
[ ] Expand Network exists
[ ] Research Connection state exists
[ ] Ask Lending Intelligence drawer is mounted
[ ] ordinary load invokes no provider/AI generation
[ ] build passes
[ ] no NEW lint errors

DO THE IMPLEMENTATION NOW.

Do not return another blueprint.
Do not ask for permission to code.

Inspect -> code -> run -> visually validate -> test -> report.

End exactly:

READY FOR LENDING UI RECONSTRUCTION U2
