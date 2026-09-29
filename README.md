OBJECTIVE: MODERNIZE THE EXISTING COUNTERPARTY RELATIONSHIP INTELLIGENCE UI — PRESERVE THE WORKING CORE
We now understand the existing solution. Do not redesign the backend, replace the data model, or create another relationship engine.
The existing backend, analysis pipeline, generated report contract, and relationship data are the trusted foundation.
The goal is now to create a clean, modern, analyst-friendly UI on top of the existing working data, while preserving all existing functionality.
1. NON-NEGOTIABLE ARCHITECTURE
Treat the existing generated-report relationship data as the source of truth.
Existing flow:
CAM/source documents
    ↓
ingestion
    ↓
Step 1: cam_distiller.py
    ↓
Step 2: subportfolio.py
    ↓
Step 3: portfolio.py
    ↓
Step 4: html_agent.py
    ↓
generated correlation HTML
    ↓
correlation_report.py
    ↓
/api/v1/jobs/{job_id}/correlation-data
    ↓
React correlation workspace

Preserve the existing embedded report contract, including where available:
- REL
- REFERENCE_ENTITIES
- ENTITY_IDS
- CATEGORIES
- HUB_GROUPS
- TFA_TOTAL_MM
- exposure values
- source
- excerpts
- confidence
- identifiers
- community/group information
REL remains the relationship truth consumed by the UI.
Do not independently regenerate relationships in React.
Do not create another relationship database.
Do not change CAM extraction or maker/checker logic.
Do not change exposure calculations.
Do not redesign R2D2, SEC, Web, authentication, or research infrastructure.
Do not revive any unrelated Stage 7 / GLEIF / CCR experimental architecture.
2. IMPORTANT EXISTING SEMANTIC
Preserve the current distinction:
856 canonical/distinct relationship pairs in REL
                  ↓
UI directional expansion
                  ↓
1,712 A→B / B→A display records

Do not persist 1,712 as a second source of truth if this is currently only a presentation transformation.
3. WHAT WE ARE CHANGING
Only the consumption and presentation layer.
Turn the existing long report/workspace into a focused analyst application.
The first screen should communicate the important information immediately instead of displaying every technical detail at once.
4. NEW PRIMARY WORKSPACE
Build the main page approximately as:
┌──────────────────────────────────────────────────────────────┐
│ Citi | Counterparty Relationship Intelligence              │
│ Search entity...                          As-of | Sources   │
├──────────────────────────────────────────────────────────────┤
│ 521 Companies | 856 Relationships | 49 Hubs | $817.7bn TFA │
│                                         $6.2bn Indirect Exp │
├────────────────────────────────────────┬─────────────────────┤
│                                        │                     │
│          RELATIONSHIP NETWORK          │ ENTITY INSPECTOR    │
│                                        │                     │
│                                        │ Selected company    │
│                                        │ identifiers         │
│                                        │ relationships       │
│                                        │ exposure            │
│                                        │ categories          │
│                                        │ sources             │
├────────────────────────────────────────┴─────────────────────┤
│ Overview | Relationships | Evidence | Community | Sources   │
└──────────────────────────────────────────────────────────────┘

Use the existing React application and API contract rather than generating another standalone frontend unless there is a concrete technical reason not to.
5. ENTITY SEARCH
Preserve the current search capability.
Search across all existing identifiers available in ENTITY_IDS / report data, including where present:
- company name
- CAGID
- GFCID
- LEI
- ISIN
- CUSIP
- CIK
- BBG
Selecting an entity must drive the whole workspace:
selected entity
     ↓
network focus
     ↓
entity inspector
     ↓
relationships table
     ↓
evidence/source view

There must be one shared selected-entity state.
6. NETWORK — MAKE THIS THE HERO FEATURE
The network should occupy the largest part of the screen.
Preserve the existing entity and relationship data.
Improve the interaction and visual presentation.
Required:
- selected entity clearly highlighted
- directional relationships where relevant
- node category colors
- relationship-type legend
- zoom
- pan
- reset
- re-layout
- fit to screen
- labels
- click node → update Entity Inspector
- click edge → relationship/evidence details
- current community grouping where available
- category grouping where available
Add:
Full-screen Network
Clicking Expand Network should turn the graph into a near-full-page workspace so a user can comfortably explore large networks.
Do not force the user to inspect a large graph inside a small dashboard card.
Preserve the existing community detection functionality rather than replacing it.
7. ENTITY INSPECTOR
When a node is selected, show a concise panel containing available current data such as:
Entity
Microsoft
Category
Big Tech / Hyperscaler
Identifiers
CAGID / GFCID / LEI / ISIN / CUSIP / CIK / BBG when available
Relationships
20
Community
current community identifier/name
Financial context
TFA / OSUC / indirect exposure when available
Actions
- View relationships
- Filter database to this entity
- Center network
- View sources/evidence
Do not fill the inspector with implementation/debug information.
8. RELATIONSHIPS VIEW
Preserve the existing filterable relationship database.
Use the existing directional presentation records derived from REL.
Display important columns such as:
- Company A
- Company B
- Relationship Type
- Relationship / A's perspective
- Deal / Commitment
- Citi Indirect Exposure
- Source
- Key Excerpt
- Confidence
Preserve:
- filtering
- search
- entity filtering
- CSV export
- XLSX export
Exports should continue respecting the current filtered view.
Do not make the relationship database the dominant landing-page element.
Put it behind the Relationships tab.
9. EVIDENCE VIEW
Create a clean evidence/source view using the data already returned by the report.
When a relationship is selected show:
Relationship
Microsoft → Stack HK

Type
Key Customer / Offtaker with Parent Guaranty

Source
Coral II GIE CAM

Evidence
[existing excerpt]

Confidence
Very High

Deal / Commitment
$6.25bn guarantee

If multiple evidence/source fields already exist, show them.
Do not manufacture new evidence.
10. PORTFOLIO SUMMARY
Keep the existing important KPIs but simplify them visually.
Current values include:
- 521 unique companies
- 856 unique relationships
- 1,712 directional database records
- 49 reference entities
- approximately $817,675.5MM Total Facility Amount
- approximately $6,205.4MM Citi Indirect Exposure
All values must continue to come from existing report/backend data.
Do not hardcode current values.
11. HIDE TECHNICAL NOISE
Do not show users implementation concepts such as:
- data contract internals
- React transformation details
- job orchestration details
- pipeline stages
- API semantics
- runtime stores
- checker internals
These belong in technical documentation, not the main analytical workspace.
Similarly, methodology/provenance information should be accessible through:
Sources / Methodology / Audit
rather than consuming the main page.
12. PRESERVE EXISTING SOURCE PROVENANCE
Do not remove:
- CAM provenance
- SEC provenance
- verified-news provenance
- excerpts
- confidence
- source document identifiers
- existing methodology
The application should become visually simpler without losing traceability.
13. PREPARE FOR AI — DO NOT BUILD A SECOND AI SYSTEM
The backend already has:
- llm_client.py
- R2D2 support
- maker/checker infrastructure
- SEC/Web research capabilities
Do not implement a new AI architecture now.
Instead, make the new UI structurally ready for a future AI Analyst panel.
Reserve a right-side collapsible area/component:
AI Analyst

but do not invent insights or create a second research pipeline in this task.
The future AI Analyst should consume:
selected entity
+ REL
+ evidence/excerpts
+ network context
+ existing backend AI services

14. PREPARE FOR FUTURE ADDITIONS
Structure the frontend so these can later be added without redesigning the application:
- richer multi-hop network
- world map
- news/events
- AI Analyst
- stress/scenario analysis
- SEC/Web enrichment actions
But do not implement those now unless required for the basic workspace architecture.
15. DO NOT REWRITE WORKING BACKEND CODE
Before touching backend code ask:
Can this requirement be implemented entirely from the existing /correlation-data contract?
If yes, do it in the frontend.
Only add a backend endpoint when the existing API genuinely cannot expose required existing data.
Any backend change must be:
- additive
- read-only where possible
- backwards compatible
- not alter the existing generated report
- not alter REL
16. IMPLEMENTATION APPROACH
You have already inspected the architecture. Do not perform another broad repository investigation.
Start from the existing:
- client.ts
- CorrelationWorkspace.tsx
- existing network components
- existing relationship table components
- /api/v1/jobs/{job_id}/correlation-data
Reuse components and data transformations where practical.
Refactor presentation rather than rebuilding everything.
17. FIRST DELIVERY
Deliver a usable first version containing:
1. clean application header
2. compact portfolio summary
3. global entity search
4. large interactive relationship network
5. entity inspector
6. relationships tab/table
7. evidence/source view
8. full-screen network mode
9. existing filters
10. existing CSV/XLSX export
Use the current dataset so I can immediately test:
- Digital Realty
- CoreWeave
- Stack HK
- ISG
- CyrusOne
- Equinix
- Microsoft if available
18. ACCEPTANCE TEST
I should be able to:
open app
  ↓
see portfolio summary
  ↓
search/select an entity
  ↓
see its network immediately
  ↓
click connected entity
  ↓
inspector updates
  ↓
inspect relationship
  ↓
see source + excerpt
  ↓
filter all relationships to entity
  ↓
expand network full screen
  ↓
export filtered relationship rows

All results must be derived from the existing trusted backend/report data.
19. WORKING RULE
Do not stop for architecture discussion or produce another architecture report.
Implement the UI.
Make normal frontend decisions yourself.
Stop only for a genuine blocker where the existing backend does not expose information required for the UI.
If that happens, report:
BLOCKER: <precise missing data/API>
SMALLEST ADDITIVE FIX: <proposal>
Otherwise continue until the first redesigned workspace is running and ready for me to test.
Do not replace what already works. Build on it.
