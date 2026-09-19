You are continuing the CCRIG Credit Relationship Workbench.

Act as the lead engineer working with a senior credit portfolio analyst.

IMPORTANT:
The internal Lending relationship database has now passed strict validation.

Current trusted baseline:

- 54/54 files processed
- 48/48 relationship documents processed
- 69 confirmed Lending clients
- 3 pending-review clients
- 767 VALIDATED relationships
- 916 REVIEW_REQUIRED relationships
- 31,274 REJECTED relationships
- 181 validated indirect relationships
- 0 cross-document discoveries currently reported
- Golden sample PASS
- 100% of validated relationships have exact entity-pair/type evidence and identifiable source locations
- Low-confidence records remain outside the trusted canonical view

DO NOT rebuild the extraction architecture.
DO NOT broaden the taxonomy.
DO NOT introduce R2D2, Web or SEC yet.
DO NOT touch CCR.

The next phase has THREE tightly controlled objectives:

1. Verify and fix CROSS-DOCUMENT / HIDDEN DISCOVERY
2. Freeze the validated database as a trustworthy baseline
3. Build a simple database-driven Lending relationship map

==================================================
OBJECTIVE 1 — CROSS-DOCUMENT DISCOVERY
==================================================

The current result reports:

0 cross-document discoveries.

This needs to be investigated carefully.

A cross-document discovery means:

A relationship involving Company A is NOT sourced from Company A's own CAM/document,
but is explicitly evidenced in another internal company's credit document.

Example:

CoreWeave's own CAM may not mention Supermicro.

Another company's CAM explicitly states:

Supermicro -> CoreWeave = supplier/customer/other relationship

When searching CoreWeave, that relationship should still appear.

This is a CROSS-DOCUMENT DISCOVERY.

IMPORTANT:

Do NOT confuse:

CONNECTIVITY
DIRECT / INDIRECT

with:

DISCOVERY ORIGIN
SUBJECT_DOCUMENT / CROSS_DOCUMENT

These are independent dimensions.

A relationship can be:

DIRECT + CROSS_DOCUMENT

For example:
a real direct supplier relationship discovered from the supplier's CAM instead of the client's own CAM.

==================================================
1A. IMPLEMENT / VERIFY DISCOVERY ORIGIN
==================================================

Every validated relationship should support:

discovery_origin:

SUBJECT_DOCUMENT
CROSS_DOCUMENT
MULTI_DOCUMENT

Use MULTI_DOCUMENT where the relationship appears in both the subject's own document and other internal sources.

Do NOT infer cross-document solely because filenames differ.

Determine document subject first.

Example:

Subject company:
CoreWeave

Source document subject:
NVIDIA

Relationship:
NVIDIA -> CoreWeave

Then:

discovery_origin = CROSS_DOCUMENT

if there is no CoreWeave-subject evidence supporting the same relationship.

==================================================
1B. TEST REAL CASES
==================================================

Do not invent examples.

Search the existing validated evidence and identify genuine candidate cases where:

- Entity A appears in another company's CAM
- the relationship is explicit
- the relationship is validated

Create at least 5 real cross-document test cases if available.

For each show:

Entity A
Entity B
Relationship Type
Economic Connectivity
Discovery Origin
Source Document
Document Subject
Exact Evidence
Confidence

If zero genuine cases exist, prove that rather than fabricating results.

But first verify that the extraction/reconciliation logic is capable of detecting them.

==================================================
1C. SEARCH BEHAVIOR
==================================================

When I search Entity A:

return ALL validated relationships involving Entity A,
regardless of which source document produced the evidence.

This is critical.

The search should not be restricted to:

"relationships extracted from Entity A's own CAM."

It should query the canonical relationship database.

==================================================
OBJECTIVE 2 — FREEZE TRUSTED DATABASE BASELINE
==================================================

The 767 validated relationships now form the trusted baseline.

Freeze/version this state.

Create a clear baseline identifier such as:

LENDING_INTERNAL_BASELINE_V1

Record:

- build timestamp
- quality-control version
- source inventory version
- number of confirmed Lending clients
- number of validated relationships
- number review-required
- number rejected
- golden sample version

Do NOT silently replace this baseline during normal UI operations.

Future R2D2 / SEC / web enrichment will build ON TOP of this baseline, not rewrite it.

==================================================
2A. TRUSTED STATUS MODEL
==================================================

Keep:

VALIDATED
REVIEW_REQUIRED
REJECTED

Default user-facing relationship views must use:

VALIDATED only.

Allow review-required data only through an explicit filter/review workflow.

Rejected records must never appear in the normal relationship graph.

==================================================
2B. BASELINE IMMUTABILITY
==================================================

Normal navigation, search, graph interactions and future enrichment must not mutate validated baseline records.

Any future external proposal should be stored separately.

Do not implement external proposals now.
Just preserve the architecture boundary.

==================================================
OBJECTIVE 3 — SIMPLE DATABASE-DRIVEN NETWORK MAP
==================================================

Now create the FIRST USEFUL NETWORK MAP.

Do NOT build a complicated visualization.

The goal is simple, intuitive exploration of the trusted Lending database.

==================================================
3A. BASIC MAP EXPERIENCE
==================================================

Workflow:

1. User searches/selects an entity
2. Selected entity appears in the center
3. All VALIDATED connected entities appear around it
4. Draw edges representing validated relationships
5. Label or encode the relationship type clearly
6. Click any connected entity
7. That entity becomes the new center
8. Its validated relationship network is displayed

This should let the analyst "walk through" the credit network.

Example:

CoreWeave
   |
   | Contracted Customer
   |
Microsoft

Click Microsoft.

Now show Microsoft's validated internal relationships.

==================================================
3B. MAP MUST USE ONLY CANONICAL DATABASE
==================================================

The map must NOT independently infer relationships.

It must render only:

VALIDATED canonical relationships.

The database is the source of truth.

No direct extraction logic in the graph component.

==================================================
3C. MULTIPLE RELATIONSHIPS BETWEEN SAME ENTITIES
==================================================

If two entities have multiple atomic relationships:

CoreWeave <-> NVIDIA

Supplier
Equity Investor
Customer

Do NOT merge the underlying records.

Visually either:

- show one edge with "3 relationships"
OR
- show concise multiple labels

When clicked, show all relationship records.

==================================================
3D. DIRECT / INDIRECT
==================================================

Use simple visual distinction:

DIRECT:
solid edge

INDIRECT:
dashed edge

But remember:

CROSS_DOCUMENT is NOT the same thing as INDIRECT.

Cross-document status should appear in the inspector / badge / tooltip,
not alter economic connectivity.

==================================================
3E. RELATIONSHIP STATE
==================================================

By default show:

CURRENT + UNKNOWN where valid and appropriate

Provide toggles for:

Current
Historical
Emerging / other supported states

Historical relationships should not dominate the initial map.

==================================================
3F. TOOLTIP
==================================================

Hovering over a connected node or relationship should show concise useful data:

Entity name
Relationship type
Direction
Confidence
State
Direct / indirect
Discovery origin
Source count

Do not overload the tooltip.

==================================================
3G. CLICK / INSPECT
==================================================

Click an edge or relationship:

show:

Entity A
Entity B
Relationship Type
Direction
State
Connectivity
Discovery Origin
Confidence
Source Document(s)
Exact Evidence
Source Location

This directly addresses transparency.

==================================================
3H. ENTITY PROFILE
==================================================

When a company is selected, show:

Canonical name
CAGID if available
Portfolio client / external entity
Entity type/category if supported
Number of validated relationships
Direct count
Indirect count
Cross-document discoveries
Source-document count

Keep it small.

==================================================
3I. EXTERNAL ENTITIES
==================================================

Do NOT restrict navigation to the 69 Lending clients.

If an external/non-client entity exists in the validated database:

allow the analyst to click it and pivot to it.

This is important for finding hubs.

Example:

NVIDIA may connect multiple Lending clients.

Search/click NVIDIA and show all validated Lending relationships around it.

==================================================
3J. HUB SIGNAL
==================================================

Add ONE simple network metric:

Validated relationship count / degree.

For each entity:

degree = number of unique validated connected entities

This is NOT a risk score.

Use it only to help identify major hubs.

Show:

Connections: 12

Do not calculate advanced centrality yet.

==================================================
DO NOT ADD YET
==================================================

Do NOT add:

- OSUC sizing
- exposure overlays
- R2D2
- Web
- SEC
- AI Assist
- correlation configuration redesign
- advanced centrality
- contagion scoring
- risk scoring
- scenario analysis
- fancy animations
- large dashboards

Those come after this foundation works.

==================================================
TERMINAL / PROCESS CHECK
==================================================

One screenshot showed PowerShell terminated with exit code 1 even though application validation passed.

Investigate this briefly.

Confirm whether:

- it was only a completed/terminated helper command
OR
- an important service crashed

Required services should remain healthy:

Frontend
Workspace API
Existing preserved API if still intentionally required

Do not refactor service architecture.

Just verify health.

==================================================
UI FOCUS
==================================================

The page should now prioritize:

1. Trusted database status
2. Entity search
3. Network map
4. Entity profile
5. Relationship inspector
6. Canonical relationship table

Reduce visual emphasis on:

source inventory
technical extraction details
rejected counts

Those remain available lower on the page / quality panel.

The main user is now a CREDIT PORTFOLIO ANALYST, not the developer.

==================================================
ACCEPTANCE TESTS
==================================================

TEST 1 — BASELINE

Verify:

Baseline = LENDING_INTERNAL_BASELINE_V1 or equivalent

Validated relationships = current trusted baseline

No normal application action mutates it.

PASS / FAIL

--------------------------------------------------

TEST 2 — CROSS-DOCUMENT LOGIC

Verify:

discovery_origin supports:

SUBJECT_DOCUMENT
CROSS_DOCUMENT
MULTI_DOCUMENT

PASS / FAIL

--------------------------------------------------

TEST 3 — REAL CROSS-DOCUMENT EXAMPLES

Identify genuine examples from the current source set.

If examples exist:

verify searching either entity returns the canonical relationship.

If none exist:

document that no genuine case exists,
but verify the logic with repository-supported test fixtures if already available.

Do not fabricate production data.

PASS / FAIL

--------------------------------------------------

TEST 4 — DIRECT VS CROSS-DOCUMENT

Verify a DIRECT relationship can still be CROSS_DOCUMENT.

These dimensions must not be coupled.

PASS / FAIL

--------------------------------------------------

TEST 5 — TRUSTED MAP ONLY

Verify graph renders VALIDATED relationships only by default.

No REVIEW_REQUIRED or REJECTED records appear.

PASS / FAIL

--------------------------------------------------

TEST 6 — PIVOT

Select Entity A.

Click connected Entity B.

Entity B becomes the center and its relationships load.

PASS / FAIL

--------------------------------------------------

TEST 7 — EXTERNAL ENTITY

Select at least one validated external/non-client entity.

Verify it can be used as the center of the network.

PASS / FAIL

--------------------------------------------------

TEST 8 — MULTIPLE RELATIONSHIP TYPES

Find an entity pair with multiple validated relationship types.

Verify all remain distinct in the database and accessible from the edge inspector.

PASS / FAIL

--------------------------------------------------

TEST 9 — PROVENANCE

Select a relationship.

Verify:

source document
source location
exact evidence
confidence

are accessible.

PASS / FAIL

--------------------------------------------------

TEST 10 — SERVICE HEALTH

Frontend healthy.
Workspace API healthy.
Required API routes healthy.

Explain the PowerShell exit-code-1 event.

PASS / FAIL

==================================================
IMPLEMENTATION DISCIPLINE
==================================================

Inspect first.

Make additive changes.

Do NOT rebuild the validated database unless required to calculate discovery_origin.

Do NOT broaden extraction.

Do NOT change existing relationship definitions.

Do NOT weaken validation.

Do NOT introduce external evidence.

Reuse existing:

- entity API
- canonical relationship API
- explorer API
- provenance API
- review APIs
- RelationshipDatabase UI
- graph components where possible

Keep scope small.

Proceed autonomously through the full approved scope.

Do not stop to ask for confirmation.

Stop immediately once all acceptance tests pass or a genuine external blocker exists.

==================================================
FINAL RESPONSE FORMAT
==================================================

When complete provide ONLY:

1. Baseline version created
2. Validated relationship count
3. Cross-document discovery count
4. 3–5 real cross-document examples, if available
5. Files materially changed
6. Map functionality added
7. PowerShell exit-code explanation
8. Acceptance tests:
   TEST 1 PASS/FAIL
   ...
   TEST 10 PASS/FAIL
9. Genuine blockers

No long architecture report.

==================================================
CORE OBJECTIVE
==================================================

Freeze the trusted Lending internal relationship database, correctly distinguish cross-document discovery from indirect economic connectivity, and expose the validated database through a simple transparent pivotable network map where analysts can move from one entity to another and inspect the exact evidence behind every relationship.
