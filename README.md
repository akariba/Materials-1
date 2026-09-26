CCR V1 — STAGE 6A–6F
CLIENT CORRELATION WORKSPACE — FIRST REAL UI

ROLE
You are the implementation agent.

Implement the first real CCR V1 Client Correlation Workspace against the already-approved Stage 5.1 backend.

This is NOT a redesign of the backend.
This is NOT a new research stage.
This is NOT a provider/enrichment stage.
This is NOT a correlation-authoring stage.

The objective of Stage 6A–6F is to expose the existing governed CCR backend as a serious institutional client-correlation workspace and allow us to begin evaluating the product in the browser.

STOP after 6F.

Do not implement 6G–6K.
Do not implement Manual Create Correlation.
Do not implement AI Create Correlation.
Do not implement provider research.
Do not implement new enrichment.
Do not implement portfolio-wide network scanning.
Do not implement statistical/market correlation.
Do not modify the authoritative Client Universe.
Do not create synthetic relationships in production data.

========================================================
0. AUTHORITATIVE INPUTS AND PRECEDENCE
========================================================

Use these sources in this order of authority:

1. CURRENT Stage 5.1 runtime/API/database contracts.
2. Current CCR V1 Stage 4.1 + Stage 5 + Stage 5.1 reports/tests.
3. Current Client Universe repository/API.
4. The senior UI/UX architecture document supplied by the product owner as the UI DESIGN reference.
5. Historical screenshots/reports only as historical reference.

IMPORTANT:
The senior UI document contains examples that may be stale relative to the final Stage 5.1 backend.

Runtime truth ALWAYS wins over stale example text.

Examples:

- 3M internal client_id = 437487.
- 3M GFCID = 0000426083.
- NEVER display client_id 437487 as though it were the GFCID.
- Use actual source identifiers from the API.

- Explicitly selected/named clients use their own persisted CCR identity links.
- Current Stage 5.1 permits VERIFIED + EXACT named endpoint resolution symmetrically.
- Explicit 3M → Solventum queries currently return valid accepted factual relationships.
- Do NOT reproduce older UI language saying explicit Solventum is still identity-blocked if the current API says otherwise.
- Broad discovered-entity ambiguity and explicit named-client resolution are separate concepts. Preserve that distinction.

Before implementation, inspect the actual Stage 5.1 response payloads.

DO NOT code from screenshots alone.

========================================================
1. FIRST ACTION — AUDIT THE EXISTING FRONTEND
========================================================

Before writing UI code:

Inspect:

- frontend/package.json
- framework
- TypeScript configuration
- routing
- styling system
- existing components
- existing API client
- current application shell
- current client search implementation
- build/test tooling
- any existing graph packages
- frontend environment/configuration

Produce a short implementation note:

backend/data/CCR_V1_STAGE_6_FRONTEND_AUDIT.md

Record:

- current framework
- current package structure
- reusable components
- packages already installed
- packages required for Stage 6
- files planned for modification
- whether the existing frontend can be safely extended

RULE:
Extend the existing frontend if reasonably possible.

Do NOT perform a ground-up frontend rewrite as the first action.

If the current frontend architecture is fundamentally incompatible and implementing this stage would require replacing it wholesale:

STOP.
Do not rewrite it.
Report the conflict first.

Otherwise continue.

========================================================
2. PRODUCT MODEL — NON-NEGOTIABLE
========================================================

This is ONE CLIENT CORRELATION WORKSPACE.

The selected Client Record is the persistent context.

Do NOT create independent mini-apps for:

- Network
- Relationships
- Correlations
- Evidence
- Intelligence

Network and table/list are different renderings of the same client investigation context.

Required application hierarchy:

GLOBAL BAR
    Client Universe search
    as-of date
    investigation navigation/history where feasible
    global Correlation Definitions entry

CLIENT CONTEXT HEADER
    legal/client name
    actual GFCID
    country/jurisdiction if available
    identity state
    coverage summary
    direct relationship count
    correlation-definition match summary
    Expand Network

PRIMARY WORKSPACE
    Network — DEFAULT
    Relationships & Correlations — alternate view

LEFT CONTROL RAIL
    Layers
    Filters
    correlation-pattern visibility

RIGHT INSPECTOR
    selected client/entity
    direct relationship
    derived correlation
    evidence
    identity
    coverage

Evidence normally belongs in the inspector/drawer, not as an unrelated standalone dashboard page.

========================================================
3. CORE GOVERNANCE RULES
========================================================

These rules override visual convenience.

RULE 1 — DIRECT FACT ≠ DERIVED CORRELATION

DIRECT_RELATIONSHIP is factual.

DERIVED_CORRELATION is the result of evaluating governed patterns over factual relationships.

They MUST NOT render as the same visual object.

A derived correlation MUST NOT be drawn as a new direct edge between Client A and Client B.

Instead, when a correlation exists:

- retain the real factual relationship edges;
- highlight the qualifying two-hop path;
- render a visually distinct correlation halo/path overlay;
- label that overlay with the correlation definition.

Example conceptual representation:

Client A
    <- supplies -
Supplier X
    - supplies ->
Client B

SHARED_SUPPLIER is an overlay around those factual edges.

NEVER:

Client A ----- SHARED_SUPPLIER ----- Client B

as though SHARED_SUPPLIER were a factual relationship edge.

RULE 2 — ZERO IS NOT PROOF OF NON-EXISTENCE

Every zero correlation result must retain:

- execution_status
- research coverage
- as-of date if available
- warnings
- zero_is_not_universal_negative

UI wording must make this understandable.

For example:

0 matches found.
Supply coverage: PARTIAL.
This does not confirm that no such real-world relationships exist.

Do not display a blank panel that implies comprehensive research found nothing.

RULE 3 — EVIDENCE IS FIRST-CLASS

Every visible factual relationship must reach its evidence in no more than two user interactions.

Expose available:

- source class
- document/reference
- passage/excerpt
- publication/retrieval dates
- evidence basis
- claim/relationship lineage
- relationship version
- qualifier evidence when available

Never fabricate missing evidence metadata.

RULE 4 — IDENTITY IS VISIBLE

Where identity affects eligibility, show it.

Use actual persisted states:

VERIFIED
PROBABLE
UNVERIFIED
REJECTED

and link type:

EXACT
ASSOCIATED

Current accepted correlation gate remains the Stage 5.1 contract.

Do not weaken backend governance in the frontend.

RULE 5 — NO NUMERIC CORRELATION SCORE

Do not create:

- confidence percentage
- connection-strength score
- correlation-strength number
- AI probability
- risk score

Use factual structure, evidence basis, coverage, status, freshness and explicit suppression metadata.

RULE 6 — INTERNAL SOURCE GROUPING IS NOT A RELATIONSHIP

CAGID or other source grouping values must never look like proven entity relationships.

If displayed, label clearly as source/internal grouping with unconfirmed semantics.

========================================================
4. TECHNOLOGY DIRECTION
========================================================

Only adopt packages after auditing the existing frontend.

Preferred architecture if compatible with the current app:

- React + TypeScript
- existing Vite setup if already present
- existing router if suitable; otherwise React Router/TanStack Router
- TanStack Query for server state
- Zustand or existing lightweight equivalent for workspace/investigation UI state
- Cytoscape.js for investigative network rendering
- Radix/shadcn primitives only if compatible with the current stack
- institutional custom token layer rather than default shadcn theme
- TanStack Table/Virtual or current equivalent for dense tables

Do NOT introduce technology merely because it was named in a design document.

Prefer existing compatible infrastructure.

The investigative graph data model must be engine-agnostic.

Do NOT leak Cytoscape-specific objects throughout application/domain state.

Create shared frontend domain types for:

- ClientRecordReference
- LegalEntityReference
- IdentityLink
- DirectRelationship
- RelationshipVersion
- RelationshipQualifier
- EvidenceReference
- CoverageRecord
- CorrelationDefinition
- DerivedCorrelation
- CorrelationHop
- ExecutionStatus
- CoverageOutcome

Names may adapt to current code conventions.

========================================================
5. DESIGN SYSTEM
========================================================

This must not look like a generic CRUD/SaaS dashboard.

Target:

institutional analyst research terminal.

Primary theme:
dark.

Also preserve the architecture for a legitimate light theme if the current system supports themes.

Use a design-token layer.

Do not scatter hardcoded colors through components.

Design properties:

- dense typography
- approximately 13–14px normal analytical text
- compact spacing
- clear information hierarchy
- restrained neutral palette
- semantic accents only
- minimal radius
- no giant cards
- no excessive white/empty space
- no decorative gradients
- no ambient glow
- no animated particle effects
- no marketing-style hero section
- no consumer dashboard tiles

Color must never be the sole status encoding.

Use combinations of:

- shape
- stroke
- icon
- text
- color

========================================================
6A. APPLICATION SHELL + REAL CLIENT SEARCH
========================================================

Implement first.

Visible outcome:
A polished search → select client workflow connected to the real Client Universe.

GLOBAL BAR

Include:

- product label: Client Correlation
- Client Universe search
- as-of-date control/indicator
- route to read-only Correlation Definitions catalogue
- investigation navigation if simple to preserve

CLIENT SEARCH

Use the existing Client Universe backend search API.

Do NOT download or load the 3.67M Client Universe into the browser.

Support whatever the current backend actually supports, prioritizing:

1. exact GFCID
2. legal/client name
3. alias
4. other exact identifiers supported by current API

Search results should be dense rows showing actual available fields:

- legal/client name
- GFCID
- country
- optional identity state if available efficiently

Never show internal client_id in place of GFCID.

Do not invent fuzzy search if the current backend does not provide it.

Use debounced/cancellable search.

Selecting a client opens the client workspace.

URL/state should preserve selected client identity where practical.

Use real GFCID for user-facing route semantics if current routing architecture supports it safely; internally the Stage 5 endpoints can continue using client_id as required.

Implement a clear translation boundary between:

user-facing GFCID
and
backend internal client_id.

========================================================
6B. CLIENT HEADER + DIRECT RELATIONSHIPS + FIRST EVIDENCE
========================================================

Wire to the real Stage 5/5.1 read model.

Current Stage 5 public surface includes routes equivalent to:

GET /api/ccr/correlation-definitions

GET /api/ccr/clients/{client_id}/summary

GET /api/ccr/clients/{client_id}/relationships

GET /api/ccr/clients/{client_id}/correlations

GET /api/ccr/clients/{source_client_id}/relationships/{target_client_id}

GET /api/ccr/clients/{source_client_id}/correlations/{target_client_id}

Inspect the actual registered routes before coding.
Do not duplicate routes unnecessarily.

CLIENT CONTEXT HEADER

Show:

- client/legal name
- GFCID
- country
- identity link state/type
- coverage indicators
- number of factual direct relationships
- “N of 6 correlation definitions matched”
- as-of context

Do NOT simply display “0 correlations”.

DIRECT RELATIONSHIP TABLE

Columns should include as appropriate:

- relationship type
- canonical direction
- counterparty
- internal-client vs external-entity state
- important qualifier
- evidence basis
- freshness/current state
- history indicator

For OWNERSHIP:

surface ownership percentage prominently when available.

Use relationship history instead of overwriting prior facts.

For the existing Solventum example, if current runtime reports 14.8% as the current version with a prior 19.9% version, expose both correctly.

FIRST EVIDENCE INSPECTOR

Selecting a direct relationship opens the right rail.

Show:

- plain-language factual statement
- relationship/version metadata
- endpoint identity information
- qualifiers
- evidence records
- actual excerpts if stored
- source/reference
- evidence basis
- dates where available

No missing value may be manufactured.

========================================================
REAL ACCEPTANCE CHECK — 3M
========================================================

Use current persisted real data.

Locate 3M by actual source identity.

Expected user-facing anchor:

GFCID:
0000426083

Internal client_id currently:
437487

The UI must display those concepts correctly.

Validate at minimum:

A. Search finds 3M COMPANY.

B. Selecting it loads Stage 5.1 summary.

C. 3M → 3M India accepted ownership appears.

D. Ownership qualifier 75% appears if present in the API.

E. Evidence can be opened.

F. Explicit 3M → Solventum returns the CURRENT Stage 5.1 factual result set.

Do NOT hard-code those values into UI logic.

They are acceptance examples only.

========================================================
6C. BASIC INVESTIGATIVE NETWORK
========================================================

Implement Cytoscape.js if compatible after audit.

The default workspace view becomes Network.

Start with accepted direct relationships only.

Do NOT implement recursive graph crawling.

Use existing bounded data.

NODE VISUAL LANGUAGE

Internal Client Record / resolved client:
    rounded-square style
    “client” marker

External Legal Entity:
    circle

Root client:
    thick selected outline
    persistent label

Selected non-root:
    visibly distinct selection outline

Unresolved mention:
    do not show by default

EDGE VISUAL LANGUAGE

Accepted factual relationship:
    solid
    directional arrowhead
    relationship label

Candidate:
    not shown in default graph

Disputed:
    only if current API exposes such data
    state marker distinct from accepted

Stale:
    explicit stale marker/icon
    not just different color

Direction must be unambiguous.

Do not fabricate inverse facts.

If query orientation is reversed, distinguish:

canonical relationship direction
vs
query-relative direction.

GRAPH INTERACTION — BASIC

Required:

- click node → inspector
- click edge → relationship/evidence inspector
- pan
- zoom
- fit
- layout control
- simple node dragging if supported cleanly

Do not yet implement large expansion/frontier research.

========================================================
6D. FULL IDENTITY / EVIDENCE / COVERAGE INSPECTOR
========================================================

Expand the right inspector into the trust/audit surface.

RELATIONSHIP INSPECTOR

Show:

- relationship type
- canonical direction
- query-relative direction where relevant
- current relationship version
- prior/superseded versions
- qualifiers
- acceptance/freshness
- source/legal entity endpoint information
- identity links
- evidence references
- passage/excerpt
- evidence basis

IDENTITY INSPECTOR

Show:

- Client Record identity
- Legal Entity
- link state
- link type
- basis
- provider identifier where stored
- identity evidence
- ambiguity/unresolved state where applicable

Do not reduce identity to one green tick.

COVERAGE

Show governed research coverage separately from execution status.

Coverage states may include current backend values such as:

NOT_ELIGIBLE
NOT_RESEARCHED
RESEARCHED_FOUND
RESEARCHED_NONE_FOUND
PARTIAL
UNAVAILABLE

Freshness remains separate where provided.

Execution status is a query/evaluator condition.

Coverage is a research/enrichment condition.

Do not conflate them.

========================================================
6E. DERIVED CORRELATIONS — REAL API RESULTS
========================================================

Expose the six approved derived definitions.

Current approved catalogue:

SHARED_CONTROLLER
SHARED_SUPPLIER
SHARED_CUSTOMER
SUPPLY_CHAIN
SHARED_LENDER
SHARED_PRODUCT_DEPENDENCY

Use the live catalogue API rather than hardcoding it as UI truth wherever practical.

Provide two things:

1. Read-only global Correlation Definitions catalogue.
2. Client-scoped correlation results in the Relationships & Correlations view.

READ-ONLY DEFINITION CATALOGUE

This is governance transparency only.

Display:

- definition name/code
- version
- category
- pattern kind
- relationship roles/types
- qualifier predicates
- hub policy
- visibility metadata

NO EDIT.
NO CREATE.
NO ACTIVATE.
NO AI.

Those are later stages.

CLIENT CORRELATION RESULTS

Group results by definition.

Every definition remains visible even at zero.

Each definition header should show:

- name/code
- category
- execution status
- coverage
- result count
- warnings

For a positive derived result show:

- source client
- target client
- intermediate entity
- two exact path hops
- relationship IDs/version IDs
- relationship type/direction
- qualifiers
- evidence references
- identity lineage
- temporal metadata
- visibility/suppression state
- deterministic explanation

For zero:

show explicit zero state.

Never omit a definition merely because it returned no matches.

Current real 3M data may legitimately return zero for all six derived definitions.

That is acceptable.

Render that truth correctly.

========================================================
6F. FULL-SCREEN NETWORK + CORRELATION HALO
========================================================

Implement the first mature investigation interaction.

FULL-SCREEN MODE

The network can expand to occupy nearly the whole viewport.

Do not make this a completely unrelated application.

Retain thin persistent client context.

Left controls and right inspector should become overlay/sliding surfaces so they do not permanently consume graph width.

Provide:

- Exit
- selected client context
- as-of date
- Layers
- Filters
- Patterns
- graph search if feasible
- Inspector
- Fit
- layout selection
- minimap if Cytoscape support is practical
- breadcrumb/expansion state only if based on actual interaction state

CORRELATION HALO

This is mandatory as a COMPONENT/MECHANIC.

When a DerivedCorrelation exists, show it as an overlay over the real underlying accepted path.

Never create a new client-to-client relationship edge.

Recommended treatment:

- factual edges remain unchanged
- translucent band/halo traces the qualifying path
- definition label sits on/near the overlay
- selecting halo opens derived-correlation inspector
- inspector exposes both path hops and their evidence

If the real 3M graph still contains no positive two-hop derived correlation:

DO NOT insert synthetic relationship records into:
- relationship_ingestion.sqlite3
- Client Universe
- Stage 2 historical tables
- CCR V1 relationship tables

Instead:

- validate halo rendering through isolated frontend/component/fixture tests;
- fixture data must be clearly test-only;
- normal production-like local workspace must continue to display real zero results.

No fake “demo correlation” may appear as a real client result.

========================================================
7. RELATIONSHIPS & CORRELATIONS TABLE VIEW
========================================================

The client workspace has one central view switch:

NETWORK
RELATIONSHIPS & CORRELATIONS

This must preserve client context and filters.

RELATIONSHIPS section:
flat factual relationship list.

CORRELATIONS section:
grouped by definition.

Do not treat them as equivalent data types.

Use visible labels such as:

FACTUAL RELATIONSHIPS
DERIVED CORRELATIONS

========================================================
8. LEFT CONTROL RAIL
========================================================

Implement only controls supported by existing backend/data.

Potential sections:

LAYERS
    internal client nodes
    external entities

FILTERS
    relationship family/type
    evidence basis
    current/stale
    as-of

PATTERNS
    six derived correlation definitions

Do not add arbitrary graph-query functionality.

The application is governed and bounded.

========================================================
9. PERFORMANCE
========================================================

The Client Universe contains 3,670,650 source records.

Never attempt to render/browse/load all clients.

Search-to-select only.

Network:

- bounded
- incremental
- do not recreate the entire Cytoscape instance for every minor interaction
- keep graph rendering state separate from server data
- do not pre-expand multi-hop neighborhoods
- do not perform provider/network research on graph expansion

Tables:

virtualize only where beneficial.

Server state:

cache by appropriate inputs such as:

client
as-of date
filters
definition

Cancel superseded requests during rapid navigation/search.

========================================================
10. ERROR / LOADING / PARTIAL STATES
========================================================

Do not use one generic spinner and one generic “no data” page.

Implement distinct states:

LOADING

FAILED REQUEST

IDENTITY UNRESOLVED/BLOCKED

NOT RESEARCHED

PARTIAL COVERAGE

UNAVAILABLE COVERAGE

ZERO RESULT WITH COMPLETE EXECUTION

ZERO RESULT WITH PARTIAL COVERAGE

POSITIVE RESULT WITH PARTIAL COVERAGE

A structurally valid positive fact remains valid even if broader research coverage is incomplete.

Do not invalidate positive accepted facts because coverage is PARTIAL.

========================================================
11. DO NOT BUILD IN THIS STAGE
========================================================

Do NOT implement:

- Manual Create Correlation
- AI Create Correlation
- XYFlow authoring canvas
- definition write APIs
- DRAFT/ACTIVE workflow
- correlation-definition editing
- arbitrary graph authoring
- provider orchestration
- SEC calls
- GLEIF calls
- Web calls
- Stylus execution
- new enrichment
- frontier research
- Stage 2A.8
- recursive traversal
- natural-language research
- news provider integration
- portfolio/network-wide scanning
- all-3.67M visualization
- graph database migration
- PostgreSQL migration
- statistical correlation
- market correlation
- exposure-based priority logic
- old 16K priority cohort
- synthetic relationship creation
- fuzzy identity auto-merge

Do not modify the authoritative source:

backend/Customer_latest.parquet

Do not modify Client Universe population.

========================================================
12. AUTHORING PLACEHOLDER / FUTURE CONFIGURATION
========================================================

We DO want the application architecture to make the future correlation configuration feature natural.

Therefore include a global:

Correlation Definitions

read-only navigation surface.

But DO NOT implement editing yet.

Future architecture, NOT Stage 6A–6F:

Correlation Definitions
    → View Definition
    → Create Correlation
        Manual
        AI-assisted

Future manual and AI paths will share one governed builder.

AI will only pre-fill governed fields.

AI will never be permitted to directly:

- create relationships
- create identity links
- bypass ontology
- bypass evidence requirements
- activate definitions without human governance

Do not implement this future write path now.

========================================================
13. TESTS
========================================================

Add focused frontend tests appropriate to the existing frontend stack.

At minimum validate:

A. Search result shows correct GFCID vs internal client_id.

B. 3M can be selected.

C. selected-client summary renders real identity state.

D. direct relationship serialization renders correctly.

E. 3M → 3M India ownership is visible from real API data.

F. 75% ownership qualifier renders if API returns it.

G. evidence inspector uses real returned evidence metadata.

H. reverse query does not fabricate inverse ownership.

I. explicit 3M → Solventum follows current Stage 5.1 named-client identity behavior.

J. all six correlation definitions render even when result count = 0.

K. zero result includes zero_is_not_universal_negative semantics.

L. execution_status and research_coverage are rendered independently.

M. derived correlation fixture renders as path halo, not a synthetic direct edge.

N. normal UI never exposes fixture correlation as real persisted data.

O. no GET/read operation modifies relationship database.

P. no frontend action in Stage 6A–6F calls external relationship research providers.

Q. Client Universe row count remains unchanged.

========================================================
14. REAL-DATA BROWSER ACCEPTANCE
========================================================

At the end run the real local application.

Validate manually against real data.

Required flow:

1. Start backend.
2. Start frontend.
3. Search:
   0000426083
4. Select 3M.
5. Confirm:
   displayed GFCID = 0000426083
   internal client_id is not mislabeled as GFCID.
6. Confirm identity state from real API.
7. Open direct relationships.
8. Open 3M → 3M India.
9. Verify owns relationship.
10. Verify 75% qualifier if returned.
11. Open evidence inspector.
12. Verify actual persisted source/excerpt metadata is shown.
13. Open 3M → Solventum if exposed by current API.
14. Verify current Stage 5.1 behavior rather than stale historical assumptions.
15. Open Correlations.
16. Verify all six definitions are visible.
17. Verify zero matches are explained honestly when result count is zero.
18. Open Network.
19. Verify factual relationships are real edges.
20. Verify no derived correlation is rendered as a direct relationship edge.
21. Enter full-screen Network mode.
22. Verify inspector/evidence remains accessible.

Take screenshots for the implementation report.

========================================================
15. REQUIRED IMPLEMENTATION REPORT
========================================================

Create:

backend/data/CCR_V1_STAGE_6A_6F_UI_REPORT.md

Include:

1. Status PASS / PARTIAL / FAIL
2. Frontend audit
3. Packages added/removed
4. Files changed
5. Architecture summary
6. Routes/screens implemented
7. Existing APIs consumed
8. Client-search behavior
9. GFCID/client_id handling
10. Client context header
11. Direct relationship UI
12. Evidence inspector
13. Identity inspector
14. Coverage UI
15. Correlation results UI
16. Definition catalogue
17. Cytoscape network implementation
18. Full-screen network
19. correlation-halo implementation
20. real 3M acceptance results
21. exact real API responses/issues that affected UI behavior
22. automated test results
23. frontend build result
24. backend regression test result
25. database integrity confirmation
26. authoritative Client Universe integrity confirmation
27. external provider calls count
28. known limitations
29. screenshots/paths if practical
30. recommendation for next stage

========================================================
16. HARD STOP
========================================================

STOP after 6F.

Do not continue automatically into:

6G pairwise UX expansion
6H intelligence/news
6I broader definition governance UX
6J Manual Create Correlation
6K AI Create Correlation

Some basic read-only pairwise data may naturally exist through the existing APIs, but do not turn it into a new Stage 6G experience.

Do not begin write-capable correlation configuration.

We will review the first real browser workspace before authorizing the next increment.

========================================================
17. DEFINITION OF DONE
========================================================

Stage 6A–6F is complete only when I can open the local application and:

- search the real 3.67M Client Universe;
- select a real Client Record;
- see the correct GFCID and identity state;
- see factual direct relationships;
- distinguish internal clients from external entities;
- open evidence supporting those facts;
- understand coverage and query execution separately;
- see all six governed derived correlation definitions;
- understand zero-result correlation states honestly;
- explore the client's real neighborhood on an interactive network;
- expand that network to full-screen;
- clearly distinguish factual relationship edges from derived-correlation path overlays;
- never see a synthetic relationship presented as truth.

The purpose of this stage is to finally let the product owner SEE and TEST the Client Correlation product.

Do not optimize for number of UI components.
Optimize for whether the analyst can reach a defensible answer quickly and understand exactly why two clients are, or are not yet known to be, connected.
