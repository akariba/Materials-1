CCR RELATIONSHIP INTELLIGENCE — FIRST EVIDENCE-BACKED RELATIONSHIP PILOT

Work only in the CURRENT CCR repository.

Read first:

backend/data/CCR_EXTERNAL_PROVIDER_READINESS_REPORT.md
backend/data/CCR_RESEARCH_ORCHESTRATOR_REPORT.md
backend/data/CCR_RELATIONSHIP_EVIDENCE_PATH_POLICY.md
backend/data/CCR_RELATIONSHIP_UNIVERSE_MODEL_REPORT.md

Use the already validated pilot CCR entity:

3M CO
GFCID: 0000426083
CIK: 66740
Ticker: MMM

Do NOT broaden to additional CCR clients.

Do NOT create CONFIRMED relationships.

Do NOT use AI as evidence.

Do NOT lower evidence standards.

OBJECTIVE

Prove the complete relationship pipeline for one well-identified CCR entity
using real admissible evidence.

Run a maximum of 3 relationship analyses for 3M.

==================================================
1. USE EXISTING VERIFIED IDENTITY
==================================================

Reuse the validated identity:

CCR entity
GFCID
CAGID
LEI
CIK
Ticker

Do not re-resolve unless required for validation.

Identity quality must remain HIGH.

==================================================
2. RELATIONSHIP QUESTIONS
==================================================

Run at most three evidence-oriented analyses:

A. PARENT / ULTIMATE_PARENT

Use GLEIF Level-2 if applicable.

B. SUPPLIER / CRITICAL_SUPPLIER / SOURCE_OF_INPUTS

Use the retrieved SEC filings first.

C. CUSTOMER / KEY_CUSTOMER or STRATEGIC_PARTNER

Use SEC filings first.

If a selected relationship type is clearly not applicable to the filings,
return NOT_FOUND or INSUFFICIENT_EVIDENCE.

Do not force three proposals.

==================================================
3. SEC DOCUMENT SET
==================================================

Use the already retrieved official SEC filings where valid.

Additional SEC retrieval is allowed only if required for the three bounded
questions.

Maximum additional filings:

3

Source tier:

TIER_1_AUTHORITATIVE_EXTERNAL

==================================================
4. GLEIF LEVEL-2
==================================================

For the parent / ultimate-parent question only:

perform bounded official GLEIF Level-2 research.

Preserve exact GLEIF semantics:

direct accounting consolidating parent

ultimate accounting consolidating parent

Do not translate these automatically into generic ownership claims.

Possible outcomes:

PROPOSAL_PENDING_REVIEW
NOT_FOUND
NOT_APPLICABLE
INSUFFICIENT_EVIDENCE

==================================================
5. CLAIM EXTRACTION
==================================================

Extract candidate relationship claims only where the source explicitly supports
them.

For every claim capture:

subject entity
related entity name
relationship type
direction

source document
source section if available
evidence snippet

source tier
evidence strength
freshness

current / historical / unknown

Do not treat ordinary name co-occurrence as relationship evidence.

==================================================
6. RELATED ENTITY RESOLUTION
==================================================

For every named related entity:

attempt governed identity resolution.

Prefer:

LEI
CIK
official legal name
verified ticker
official domain

If identity cannot be resolved sufficiently:

IDENTITY_UNRESOLVED

Do not create an external entity from name similarity alone.

==================================================
7. EXTERNAL ENTITY CREATION
==================================================

A new EXTERNAL_ENTITY may be created only when:

identity evidence is defensible

and

the entity is required for an evidence-backed relationship proposal.

Persist provenance.

Do not create unrelated discovered names as entities.

==================================================
8. MATERIALITY GUARDRAIL
==================================================

Do not assign:

CRITICAL_SUPPLIER
KEY_CUSTOMER
TECHNOLOGY_DEPENDENCY

unless the evidence explicitly establishes:

materiality
dependency
concentration
criticality
or equivalent language.

Otherwise use the lower-order relationship type or return insufficient evidence.

==================================================
9. RELATIONSHIP DIRECTION
==================================================

Direction must match the evidence.

Examples:

Supplier X supplies 3M:

X --SUPPLIER_OF--> 3M

3M depends on X:

3M --TECHNOLOGY_DEPENDENCY--> X

Parent X consolidates 3M:

X --PARENT_OF--> 3M

Do not silently infer inverse relationships.

==================================================
10. RELATIONSHIP STATE
==================================================

At most create:

PROPOSAL_PENDING_REVIEW

Never:

CONFIRMED

during this task.

If threshold fails:

INSUFFICIENT_EVIDENCE
NOT_FOUND
IDENTITY_UNRESOLVED
CONFLICT
NOT_APPLICABLE

==================================================
11. DIRECT / HIDDEN DIRECT
==================================================

Every accepted proposal from external evidence that was absent from internal
CCR relationship data may be classified:

HIDDEN_DIRECT

This means:

externally discovered evidence-backed direct relationship.

It does NOT mean inferred or synthetic.

==================================================
12. INDIRECT PATHS
==================================================

If two or more accepted direct proposals happen to form a valid path:

record the path separately.

Do not create a synthetic shortcut edge.

No path hop may use unsupported relationships.

==================================================
13. AI / HELIX
==================================================

If Helix is available, it may assist with:

document section classification
candidate claim extraction
relationship taxonomy classification
direction extraction
contradiction detection
evidence summarization

But AI output must never be stored as source evidence.

All accepted claims must point to admissible source documents.

==================================================
14. QUALITY REVIEW
==================================================

Before persisting any proposal verify:

source supports exact relationship
entities match
direction correct
relationship type not overstated
current/historical meaning preserved
materiality requirement respected

If uncertain:

INSUFFICIENT_EVIDENCE

Prefer no relationship over a weak relationship.

==================================================
15. VALIDATION
==================================================

Report:

relationship questions = <= 3

SEC documents used

GLEIF Level-2 requests

candidate claims

accepted claims

rejected claims

external entities created

relationship proposals

hidden-direct relationships

indirect paths

confirmed relationships = 0

synthetic edges = 0

AI evidence = 0

==================================================
16. REPORT
==================================================

Create:

backend/data/CCR_3M_RELATIONSHIP_PILOT_REPORT.md

For each question show:

question
provider strategy
documents inspected
candidate claims
accepted/rejected evidence
entity resolution
governed outcome

Also include an Evidence Table:

Relationship
Subject
Related entity
Direction
Source
Evidence strength
Identity quality
Status

==================================================
17. FINAL RESPONSE
==================================================

Return:

CCR 3M RELATIONSHIP PILOT: PASS / FAIL

SUBJECT:
3M CO

QUESTIONS:
actual

SEC DOCUMENTS USED:
actual

GLEIF LEVEL-2 REQUESTS:
actual

CLAIMS
Discovered:
Accepted:
Rejected:

EXTERNAL ENTITIES CREATED:
actual

RELATIONSHIP PROPOSALS:
actual

HIDDEN DIRECT:
actual

INDIRECT PATHS:
actual

OUTCOMES
Proposal pending review:
Insufficient evidence:
Not found:
Not applicable:
Identity unresolved:
Conflict:

QUALITY
Unsupported claims accepted:
0 / FAIL

Wrong entity matches:
0 / FAIL

Overstated critical/key relationships:
0 / FAIL

AI AS EVIDENCE:
0 / FAIL

CONFIRMED RELATIONSHIPS:
0 / FAIL

SYNTHETIC EDGES:
0 / FAIL

REGRESSION
passed:
failed:
errors:

REPORT:
backend/data/CCR_3M_RELATIONSHIP_PILOT_REPORT.md

STOP.
