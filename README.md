CCR — FINAL DELIVERY READINESS AUDIT

Work only in the CURRENT CCR repository.

IMPORTANT:
THIS IS AN AUDIT ONLY.

Do NOT redesign the UI.
Do NOT change CSS.
Do NOT refactor.
Do NOT add features.
Do NOT change database data.
Do NOT create relationships.
Do NOT run broad external research.
Do NOT change existing relationship semantics.
Do NOT fabricate missing data.
Do NOT fix anything yet.

I need an exact current-state assessment because this application must be
delivered TODAY.

==================================================
1. OBJECTIVE
==================================================

Inspect the complete current CCR implementation and tell me exactly:

- what is implemented
- what is actually working
- what is partially working
- what is only visual
- what is disconnected
- what data exists
- what data does not exist
- what is intentionally empty
- what is broken
- what must be fixed before delivery
- what can safely wait until after delivery

Do not infer from filenames or comments alone.

Verify behavior from code, API, database and, where possible, the running app.

==================================================
2. STARTUP / RUNTIME
==================================================

Determine the exact current startup architecture.

Report:

FRONTEND:
- framework
- package manager
- start command
- build command
- expected port

BACKEND:
- framework
- start command
- expected port

DATABASE:
- exact SQLite path currently used by the running application

NETWORK / PROXY:
- current approved Windows proxy handling
- SEC status
- GLEIF status
- Web/provider status

AI:
- exact HELIX integration path
- configuration source
- status endpoint
- analysis endpoint
- whether it is currently executable
- whether credentials are actually available
- whether responses are persisted
- whether AI is read-only / explanation-only
- whether AI has any authority to create evidence or relationships

Also identify any mismatch between:
development mode,
local mode,
and the currently exposed remote/tunnel URL.

==================================================
3. CURRENT FRONTEND ROUTES
==================================================

Inspect every current CCR page.

At minimum:

/portfolio
/entities
/network
/radar
/events
/research
/evidence
/review

Also inspect any:

entity intelligence page
entity detail page
timeline page
relationship detail page
source/evidence reader
AI drawer
full-screen network view
legacy routes still reachable

For every route return:

ROUTE
IMPLEMENTED: YES / PARTIAL / NO
LOADS: YES / NO
REAL BACKEND DATA: YES / PARTIAL / NO
INTERACTIVE: YES / PARTIAL / NO
ENTITY CONTEXT PRESERVED: YES / NO
EMPTY DUE TO NO DATA: YES / NO
ACTUAL DEFECTS
DELIVERY BLOCKER: YES / NO

Do not classify an intentionally empty dataset as a frontend defect.

==================================================
4. GLOBAL SHELL
==================================================

Audit:

- navigation
- global entity search
- selected entity persistence
- URL state
- inspector
- inspector tabs
- provider status
- system status
- data-truth banners
- AI Analyst entry point
- loading states
- error states
- empty states
- responsive behavior
- scrolling
- sticky headers
- browser back/forward behavior

Identify any controls that look clickable but do nothing.

Identify any controls that contain placeholder behavior.

==================================================
5. PORTFOLIO
==================================================

Verify every visible number and section on Portfolio.

Report the exact backend/API/database origin for:

- CCR population
- canonical entity count
- exposure row count
- research candidate count
- evidence count
- relationship count
- country concentration
- entity class counts
- identifier coverage
- research posture
- industry/classification
- source/provider posture
- world-map values

For the map verify:

- GeoJSON loading
- country matching
- unmapped countries
- hover behavior
- click behavior
- filtering behavior
- entity navigation
- legend
- whether every displayed value is real

Report any misleading or decorative metric.

==================================================
6. ENTITIES
==================================================

Verify:

- entity registry count
- search
- search by legal name
- GFCID
- CAGID
- LEI
- CIK
- ticker if supported
- filters
- pagination / virtualization
- entity selection
- URL persistence
- selected row
- inspector synchronization
- entity detail navigation

Confirm the displayed entity population is canonical and not fabricated.

Check performance with the full entity registry.

==================================================
7. ENTITY INTELLIGENCE
==================================================

Inspect the selected-entity intelligence experience.

Report which of these are currently supported with REAL data:

- overview
- identity
- identifiers
- classification
- exposure rows
- relationships
- candidates
- research
- evidence
- sources
- timeline/events
- external identities
- review state
- research eligibility
- monitoring state

Identify fields that currently show:
NOT AVAILABLE
NO DATA
UNKNOWN
NOT STORED

For each one state whether that is:
A. correct because source data does not contain it
B. backend/API omission
C. frontend omission
D. actual defect

==================================================
8. NETWORK
==================================================

Audit the network very carefully.

Report:

SELECTED ENTITY
VISIBLE NODES
VISIBLE EDGES

Separate counts for:

- evidence-backed relationship edges
- production relationship edges
- confirmed relationships
- research candidate edges
- external entities
- local entities

Verify:

- solid/dotted semantics
- edge direction
- relationship type
- candidate vs relationship separation
- click node
- click edge
- inspector linkage
- filters
- semantic group layout
- graph mode
- value-chain mode
- ownership mode
- geography mode
- evidence mode
- timeline mode

For each mode say:
WORKING / PARTIAL / DISABLED / NOT IMPLEMENTED

Check whether the graph can expand to full-screen.

Check whether the current layout remains usable with 50+ nodes.

Check whether any candidate edge visually looks like a confirmed relationship.

That is a critical defect if present.

==================================================
9. RADAR
==================================================

Determine precisely what Radar currently represents.

Separate:

- persisted event themes
- research candidate signals
- local correlation signals
- source-backed monitoring information
- unavailable analytics

Verify that candidate scores are NOT presented as:

risk scores
probability of default
relationship evidence
impact evidence

Explain why the current Radar may be empty for the selected entity.

Determine whether Radar is functioning correctly despite empty persisted event data.

==================================================
10. EVENTS
==================================================

Inspect event schema, APIs and frontend.

Report:

production event count
selected-entity event count
event source count
event-to-entity linkage count

Determine whether the page is empty because:

A. ingestion is not implemented
B. ingestion is implemented but no events exist
C. backend route is missing
D. frontend is disconnected
E. filter/entity bug exists

Do not create events.

==================================================
11. RESEARCH
==================================================

Audit the full research workflow.

Report existing counts for:

research plans
research claims
research runs
provider requests
source documents
evidence snippets
candidate relationships
review-required items

Verify:

- Open Research action
- provider selection
- SEC fallback
- GLEIF fallback
- approved Web fallback
- cache use
- source policy
- identity gates
- direction gates
- evidence gates
- candidate/relationship separation
- review requirements

State clearly which operations are:

READ ONLY
EXECUTABLE
HUMAN REVIEW REQUIRED
DISABLED

==================================================
12. EVIDENCE
==================================================

Audit the evidence ledger.

Report:

total source documents
total admissible source documents
total evidence snippets
selected-entity evidence
relationship-linked evidence
research-linked evidence

Verify:

- source
- document title
- URL
- publication date
- retrieval date
- source tier
- admissibility
- excerpt
- content hash
- related entity
- relationship/research linkage

Verify clicking evidence opens a readable evidence-detail surface.

If zero selected-entity evidence is shown, determine whether zero is correct.

==================================================
13. REVIEW
==================================================

Audit the human-review surface.

Report counts for:

research claims awaiting review
candidate leads
relationship proposals
identity review items
direction unresolved
conflicts
AI-generated explanations awaiting review if any

Identify every button/action available on Review.

For each action state whether it:

works
is read-only
mutates research state
mutates production relationship state
requires confirmation
is placeholder

Do NOT execute mutation actions during the audit.

==================================================
14. AI / HELIX
==================================================

Inspect the current AI Analyst implementation end-to-end.

The screenshots show a HELIX integration surface.
Do not assume it is correct.

Verify:

- status endpoint
- execution endpoint
- credentials
- request payload
- selected entity context
- current route/page context
- graph context
- evidence context
- research context
- conversation/history behavior
- response persistence
- error handling
- timeout handling

Run only ONE safe bounded AI test if the current implementation already
supports a read-only analyst query.

Use a simple question such as:

"Explain the selected entity using only currently available CCR context."

Do not allow the test to create:

relationships
evidence
external entities
events
claims
production observations

Report:

AI EXECUTION: PASS / FAIL
CONTEXT PROVIDED:
actual
RESPONSE RECEIVED:
YES / NO
RESPONSE PERSISTED:
YES / NO
DATA MUTATION:
0 / FAIL

Check specifically whether the AI can reason only over provided source
references or whether the implementation supports approved research fallback.

Do not silently add Web research.

==================================================
15. DATA LAYER
==================================================

Inspect the actual SQLite schema and current counts.

Return current counts for the important tables including, where present:

ccr_subjects
canonical_clients
entity_registry
identifier_aliases
entity identifiers
entity name aliases
relationship taxonomy
relationship observations
confirmed relationships
relationship claims
correlation candidates
research plans
research claims
research runs
source documents
evidence snippets
events
event/entity links
relationship paths
path hops
external entities
GLEIF relationship observations
provider request/audit tables

Use actual current values.

Also report:

PRAGMA integrity_check
foreign_key_check

==================================================
16. DATA BOUNDARY VALIDATION
==================================================

Confirm that the application currently does NOT falsely represent:

ACTIVE CLIENT
INACTIVE CLIENT
monetary exposure totals where amount semantics are unresolved
risk score
probability of default
relationship confirmation from correlation alone
AI response as evidence
research candidate as production relationship
event candidate as established event
unnamed supplier as identified legal entity
external entity without identity evidence

Any violation is P0.

==================================================
17. TESTS
==================================================

Run the current supported validation suite.

At minimum:

frontend TypeScript/build
frontend lint
backend pytest regression
API smoke checks
SQLite integrity
foreign keys

If browser automation exists, run it.

Do not alter production/source data to make tests pass.

Return exact:

passed
failed
errors
warnings

For every failure state:

NEW REGRESSION
PRE-EXISTING
NON-BLOCKING
DELIVERY BLOCKER

==================================================
18. DEAD / DUPLICATE CODE
==================================================

Identify:

- old UI versions
- legacy pages
- dead routes
- duplicate APIs
- unused CSS systems
- obsolete report files
- obsolete frontend components
- test-only assets accidentally reachable by production UI

Do not delete them yet.

Just report them.

==================================================
19. DELIVERY BLOCKER MATRIX
==================================================

Create three groups.

P0 — MUST FIX TODAY BEFORE DELIVERY

Only genuine blockers:
crashes
wrong data
broken navigation
broken core actions
false relationships
false evidence
database corruption
AI mutation outside contract
security/config problem
major unreadable UI
critical browser failure

P1 — SHOULD FIX TODAY

Important usability / completeness issues.

P2 — CAN WAIT

Enhancements and polish.

For each item provide:

ISSUE
SURFACE
ROOT CAUSE
FILES
ESTIMATED CHANGE SIZE: SMALL / MEDIUM / LARGE
RISK
RECOMMENDED FIX ORDER

==================================================
20. TODAY DELIVERY PLAN
==================================================

Based on the ACTUAL repository state, propose the shortest path from the
current implementation to a deliverable build TODAY.

Do not propose another redesign.

Use this order:

1. runtime blockers
2. incorrect data / semantics
3. disconnected core functionality
4. AI functionality
5. network usability
6. entity workflow
7. research/evidence/review workflow
8. empty-state correctness
9. visual polish
10. final regression
11. final launch script

Estimate the number of implementation batches required.

Prefer small/medium focused batches.

==================================================
21. REPORT
==================================================

Create:

backend/data/CCR_FINAL_DELIVERY_READINESS_AUDIT.md

DO NOT MODIFY ANYTHING ELSE.

==================================================
FINAL RESPONSE
==================================================

Return exactly:

CCR FINAL DELIVERY READINESS: READY / NOT READY

P0 BLOCKERS:
<count>

P1 ISSUES:
<count>

P2 ISSUES:
<count>

FRONTEND BUILD:
PASS / FAIL

BACKEND REGRESSION:
passed / failed / errors

DATABASE INTEGRITY:
PASS / FAIL

FOREIGN KEYS:
PASS / FAIL

PORTFOLIO:
PASS / PARTIAL / FAIL

ENTITIES:
PASS / PARTIAL / FAIL

ENTITY INTELLIGENCE:
PASS / PARTIAL / FAIL

NETWORK:
PASS / PARTIAL / FAIL

RADAR:
PASS / PARTIAL / FAIL

EVENTS:
PASS / PARTIAL / FAIL

RESEARCH:
PASS / PARTIAL / FAIL

EVIDENCE:
PASS / PARTIAL / FAIL

REVIEW:
PASS / PARTIAL / FAIL

HELIX:
PASS / PARTIAL / FAIL

DATA-TRUTH CONTROLS:
PASS / FAIL

PRODUCTION RELATIONSHIP SAFETY:
PASS / FAIL

ESTIMATED IMPLEMENTATION BATCHES TO DELIVERY:
<number>

FIRST REQUIRED FIX:
<one concise statement>

REPORT:
backend/data/CCR_FINAL_DELIVERY_READINESS_AUDIT.md

STOP.

DO NOT IMPLEMENT THE FIXES.
