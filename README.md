Apply the LENDING RELATIONSHIP INTELLIGENCE — ENGINEERING OPERATING CONTRACT.

TASK: FINAL READ-ONLY FOUNDATION AUDIT

READ ONLY.

Do not modify:
- source code
- databases
- JSON artifacts
- parquet
- CSV
- configuration
- frontend
- deployment
- tests

No migrations.
No external calls.
No SEC calls.
No web calls.
No Stylus calls.
No AI-generation calls.

PURPOSE

Produce the final engineering map needed before consolidating Lending Relationship Intelligence.

We already know the application exposes several independent relationship universes. I now need an exact implementation-level map of how to construct a canonical foundation WITHOUT destroying source-lane governance.

Inspect at minimum:

Backend:
- lending_portfolio.py
- lending_relationship_database.py
- lending_ai_relationships.py
- lending_external_research.py
- lending_external_overlay.py
- workbench.py
- all related models/schema utilities
- migration scripts
- tests
- SQLite databases and their schemas
- V2/V3 JSON artifacts and reports

Frontend:
- PortfolioAnalytics.tsx
- AICreateRelationship.tsx
- LendingIntelligenceViews.tsx
- ReviewQueue components
- Client Detail
- Network
- Relationship Explorer
- External Research
- Workbench
- route configuration

Also inspect every relationship/entity/evidence table before proposing anything new.

==================================================
A. ENTITY MODEL
==================================================

Report every current entity concept and store.

For each report:
- table/artifact
- primary key
- CAGID handling
- legal name
- display name
- aliases
- external/non-CAGID entities
- source
- identity status
- resolution method
- whether identity is stable
- relationship foreign keys pointing to it

Identify:
- null entity IDs
- null CAGIDs
- unresolved entities
- aliases masquerading as entities
- document subjects masquerading as legal entities
- SPVs/project entities
- truncated names
- prose-fragment entities

Answer:

1. Is there already a viable universal entity registry?
2. If yes, what must be extended?
3. If no, which existing table is the safest foundation?
4. Which current foreign keys prevent external entities from participating?
5. Which identity fields are trustworthy enough for canonical identity?

==================================================
B. RELATIONSHIP MODEL
==================================================

Map every existing relationship representation.

For each store identify:
- relationship ID/key
- subject endpoint
- related endpoint
- relationship type
- family
- direction
- state
- connectivity
- source lane
- origin
- quality status
- review status
- canonical status
- evidence linkage
- source linkage
- amount/materiality
- confidence
- temporal dates
- API visibility
- UI visibility

Identify which stores are:
- observations
- candidate relationships
- canonical relationships
- review queues
- projections
- legacy artifacts

Do not treat them as interchangeable.

==================================================
C. OBSERVATION → DECISION LINEAGE
==================================================

Determine exactly what is persisted for:

source document
→ raw observation
→ entity mention
→ entity resolution
→ candidate relationship
→ taxonomy mapping
→ evidence assessment
→ direction/state assessment
→ deduplication/reconciliation
→ canonical/review/rejected result
→ API projection
→ UI projection

For each transition classify as:

PERSISTED_AND_LINKED
PERSISTED_NOT_LINKED
DERIVABLE
LOST
UNKNOWN

Explicitly identify why the existing 37 benchmark rows cannot always be traced through the complete lifecycle.

==================================================
D. TAXONOMIES
==================================================

Inventory every relationship vocabulary:
- V3 taxonomy
- normalized taxonomy
- internal/governed taxonomy
- external research preset
- AI definition vocabulary
- frontend labels

Produce a crosswalk.

Highlight:
- exact equivalents
- broader/narrower substitutions
- missing mappings
- ambiguous mappings
- types appearing only in one store
- UI labels that imply semantics not persisted in data

Pay special attention to:
- supplier
- technology_dependency
- strategic_partner
- contracted_customer
- guarantor
- backleverage_financing
- lender
- equity_investor
- parent_company
- subsidiary
- sponsor
- service_provider
- competitor
- concentration/offtaker semantics

==================================================
E. EVIDENCE MODEL
==================================================

Inventory:
- documents
- document versions
- excerpts
- evidence IDs
- source subject
- page/location
- source role
- evidence strength
- independent source count
- embedded evidence
- external claims
- exact excerpts

Determine which evidence fields are lost when moving from raw V3 to portfolio projections.

==================================================
F. EXTERNAL RESEARCH
==================================================

Map both:
1. legacy pairwise research
2. V3-aware overlay

Report:
- inputs
- cache behavior
- provider adapters
- persistence
- evidence
- proposals
- conflicts
- entity matching
- review lifecycle
- API exposure
- UI exposure
- failure behavior

Identify the safest future orchestration point for:
CAM → SEC → Stylus/Web fallback/corroboration.

==================================================
G. AI RELATIONSHIP DEFINITIONS
==================================================

Map:
Describe
→ Configure
→ Save Draft
→ Preview
→ Approval
→ Publish
→ AI instances

Report exact persisted objects/tables and identify whether the existing mechanism can support a governed relationship-definition/preset library.

==================================================
H. TARGET REUSE PLAN
==================================================

For each required future capability classify existing components:

REUSE_AS_IS
EXTEND
MIGRATE
DEPRECATE_LATER
DO_NOT_USE

Required capabilities:
- canonical entity registry
- identifier/alias registry
- portfolio membership
- observations
- evidence
- canonical relationships
- relationship lineage
- taxonomy registry
- taxonomy mappings
- external findings
- AI definitions
- events/signals
- review decisions
- unified read projection

==================================================
I. DELIVERABLE
==================================================

Create:

backend/data/LENDING_FOUNDATION_AUDIT.md

The report must contain:

1. Current-state architecture.
2. Exact authoritative stores.
3. Complete table/artifact inventory.
4. Source → API → UI matrix.
5. Identity gaps.
6. Relationship gaps.
7. Evidence gaps.
8. Lineage gaps.
9. Taxonomy gaps.
10. Reusable components.
11. Components to retire eventually.
12. Proposed canonical foundation at conceptual level ONLY.
13. Exact migration dependencies.
14. Risks if implementation starts before each dependency is addressed.

Do not implement the proposed architecture.

STOP.
