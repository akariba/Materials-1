You are working on the CCRIG Credit Relationship Workbench.

I want you to act as the lead implementation engineer for the Lending business view and build the next iteration of the product in a business-facing, impressive, and credit-useful way.

IMPORTANT CONTEXT
- This is for LENDING BUSINESS only.
- For now, REMOVE CCR from the implementation scope and focus only on Lending.
- CAM is the authoritative baseline.
- R2D2 / external evidence is supplementary only and must never silently overwrite CAM truth.
- We already created a validated Lending relationship database and baseline.
- The database is the priority foundation. The UI should now present it in a much better and more business-useful way.
- The client has shown a prototype with:
  - a front-page relationship/network map,
  - summary KPI tiles,
  - category filters,
  - confidence indicators,
  - relationship table,
  - excerpts / evidence.
- We want to combine that direction with our validated internal lending baseline and current implementation.

CURRENT REALITY / GROUNDING
- We already have a validated Lending baseline and a working internal relationship database.
- The trusted default view must remain based on validated/canonical relationships only.
- Review-required and rejected items must remain governed separately.
- Do not fabricate cross-document examples if the data does not support them.
- The current implementation already supports:
  - validated canonical relationships,
  - relationship types,
  - current / hidden / historical state,
  - connected-entity pivoting,
  - evidence provenance,
  - multi-type endpoint pairs,
  - map functionality.
- Build on top of the current validated implementation. Do not throw it away.
- Minimize unnecessary refactoring. Reuse proven components and backend routes where possible.
- Keep this as a practical POC / working product, not an abstract architecture exercise.

PRIMARY OBJECTIVE
Build a strong Lending-first front page that immediately impresses the user but is also truly useful for credit analysis.

The first page should make most of the important things visible immediately:
1. a relationship network map in the main area,
2. high-value summary metrics on top,
3. relationship-type filtering,
4. evidence / source-backed relationship inspection,
5. quick pivoting from one entity to another,
6. visible distinction between direct, hidden/indirect, and historical relationships,
7. clear presentation of why the relationship matters for credit.

BUSINESS INTENT
This tool is for portfolio / credit analysis, not a generic graph toy.
The user should be able to quickly understand:
- who the main lending clients are,
- how they are connected,
- what relationship types exist,
- where there are concentrations,
- which relationships are current vs hidden vs historical,
- what evidence supports them,
- and what the exact source excerpt is.

LENDING-ONLY SCOPE
Implement only Lending now.
- Remove or hide CCR from the user-facing workflow for this iteration.
- The page should feel like a dedicated Lending product.
- Any shared code can remain under the hood, but the visible UI should focus only on Lending.

NON-NEGOTIABLE DATA RULES
1. CAM is immutable baseline truth.
2. External / R2D2 / corroborative evidence can support, enrich, or propose — but not overwrite CAM.
3. The default main view should use the validated canonical Lending baseline.
4. Review / proposal data must be visually separated from validated canonical data.
5. If no reliable relationship exists, show that clearly instead of implying connectivity.
6. All displayed relationships must retain exact provenance: source document, location, evidence excerpt, and confidence.

WHAT I WANT YOU TO BUILD

PHASE 1 — TURN THE CURRENT DATABASE INTO A BUSINESS-FACING FRONT PAGE

Create a new or upgraded Lending landing page / main analysis page with this structure:

A. TOP HEADER / SUMMARY STRIP
Show compact KPI cards such as:
- Total validated canonical relationships
- Total unique counterparties / connected entities
- Current relationships count
- Hidden / indirect relationships count
- Historical relationships count
- Relationship types count
- Top concentration indicators (if derivable from current data)
- Count of pending review / proposed relationships (shown separately, not mixed into canonical)

B. MAIN HERO AREA = RELATIONSHIP NETWORK MAP
This should be the centerpiece of the page.

Requirements:
- Put the relationship map at the top / center of the first page.
- The map should visually connect the selected Lending entity to related entities.
- Clicking a node should pivot the whole view to that entity.
- Clicking an edge should open / update a relationship inspector panel.
- Support zoom / reset / re-layout if needed.
- Show different visual treatment for:
  - direct/current relationships,
  - hidden/indirect relationships,
  - historical relationships.
- The map should remain readable and not overly cluttered.
- Prefer business clarity over technical complexity.

Map semantics:
- Node size: based on degree / importance / number of validated connections.
- Node color: by entity category / ecosystem category.
- Edge style: by relationship state (solid direct, dashed hidden/indirect, dotted historical, or equivalent).
- Edge tooltip: relationship type, direction, confidence, state, source count.
- If multiple atomic relationship types exist between the same two entities, do not collapse them misleadingly — preserve inspectability.

C. FILTER / CONTROL PANEL
Provide business-friendly filters that are visible and immediately usable:
- Search by company / alias / CAGID
- Relationship type
- State: Current / Hidden / Historical
- Connectivity: Direct only / Indirect only / Both
- Confidence
- Evidence status:
  - CAM confirmed
  - Corroborated
  - External proposed / review
- Category / ecosystem filters (only if supported by the current data model in a clean way)
- Optional “show only highly connected entities”
- Optional “show only portfolio / client entities”
- Optional “show pending proposals” as a clearly separate toggle

D. RELATIONSHIP INSPECTOR / FACT PANEL
When a node or edge is selected, show a rich inspector panel:
- Company A
- Company B
- Relationship type
- Relationship family
- Direction
- Current / hidden / historical state
- Confidence
- Why it matters for credit (if available or derivable)
- Source / provenance list
- Exact evidence excerpt
- Source document name
- Location / section / page if available
- Number of corroborating sources
- Discovery origin (subject-document, cross-document, etc.) — but do not fabricate this.

This inspector is critical. Transparency is the main concern.
The user must be able to understand WHY the relationship exists and HOW reliable it is.

E. RELATIONSHIP TABLE BELOW THE MAP
Below the map, show a relationship table that mirrors the current filtered state.
Suggested columns:
- Company A
- Company B
- Relationship type
- Direction
- State
- Confidence
- Category
- Source count
- Evidence status
- Short excerpt
- Inspect action

This table should be auditable and export-friendly in future, but for now just make it very usable.

F. ENTITY PROFILE PANEL
When an entity is selected, show a profile box:
- Entity name
- CAGID
- Entity type
- Category
- Number of direct relationships
- Number of indirect relationships
- Number of historical relationships
- Number of connected entities
- Number of unique source documents
- Whether it is a portfolio / internal subject / external entity

G. SOURCE TRANSPARENCY / GOVERNANCE PANEL
Somewhere on the page, clearly state:
- CAM is the authoritative baseline
- External evidence is supplementary / corroborative / proposal-only
- Default view shows validated canonical relationships only
- Low-confidence or review-required items are excluded by default
- No cross-document examples should be invented

This is important for Leslie’s transparency concern.

UX / VISUAL DIRECTION
Use the client prototype as inspiration, but adapt it to our validated Lending implementation.
The page should feel:
- professional,
- clean,
- analytical,
- visually strong,
- immediately understandable,
- and impressive when opened.

It should not feel like a raw technical explorer.
It should feel like a credit intelligence workspace.

SUGGESTED BUSINESS WORDING
Use “Credit Relationships” or “Lending Credit Relationships”.
Avoid generic “counterparty intelligence” wording on the main Lending page if it confuses the business.
Use clear business terms such as:
- Relationship map
- Credit relationship
- Hidden relationship
- Historical relationship
- Corroborated evidence
- CAM confirmed
- Pending review
- Why it matters
- Source evidence

IMPORTANT CLARIFICATION
This is LENDING BUSINESS.
So frame the UI around:
- Lending relationship intelligence
- CAM-backed relationship discovery
- Credit relevance
- Exposure / concentration awareness (where supported)
- Supporting evidence and transparency

Do not drift into a generic CCR / trading / counterparty dashboard.

IMPLEMENTATION APPROACH
- Build on the current validated Lending database and current routes.
- Reuse existing map work and relationship explorer logic where appropriate.
- Keep the backend stable unless small extensions are genuinely needed.
- Prefer additive implementation over destructive redesign.
- Preserve acceptance-tested behavior.
- Do not reopen the whole architecture.
- Do not bring in ungrounded external data for the default trusted view.

IF YOU HAVE TO CHOOSE PRIORITIES, DO THEM IN THIS ORDER
1. Lending-only business-facing front page
2. Strong map + entity pivoting
3. Transparent relationship inspector with exact evidence
4. Better filters
5. Better summary cards
6. Cleaner relationship table
7. UI polish

ACCEPTANCE CRITERIA
The implementation is only complete if all of the below are true:

1. Lending-only focus
- The visible user flow is Lending-focused.
- CCR is removed or hidden from this phase.

2. Impressive first page
- The first page visibly centers the relationship map and summary insight.
- The page looks materially more business-facing than the current raw explorer.

3. Business usefulness
- A user can search a Lending entity and immediately see its network, relationship breakdown, and exact evidence.

4. Transparency
- Selecting a relationship shows exact source-backed evidence and provenance.
- The user can tell whether the relationship is CAM-confirmed, corroborated, or pending review/proposed.
- No silent blending of canonical and review data.

5. Correct governance
- Default view shows validated canonical relationships only.
- Review-required or low-confidence items are excluded unless deliberately requested.
- CAM remains authoritative.

6. Map behavior
- Node click pivots to the selected entity.
- Edge click opens relationship inspection.
- The map reflects the active filters.

7. Table behavior
- The relationship table stays synchronized with the current selection / filters.

8. Honest data handling
- If genuine cross-document examples do not exist, do not fabricate them.
- Keep the product honest.

DELIVERABLES
When done, provide:
1. The implemented UI and backend changes
2. Short summary of what changed
3. Exact files modified
4. Acceptance test results
5. Any remaining real blockers only

DO NOT
- do a long architecture essay,
- redesign unrelated flows,
- add fake intelligence,
- fabricate evidence,
- or keep asking for confirmation.

Proceed autonomously and implement the best Lending-first version of this front page based on the current validated database and the client’s prototype direction.
