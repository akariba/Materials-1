CCR RELATIONSHIP INTELLIGENCE — EVIDENCE + PATH POLICY FOUNDATION

Work only in the CURRENT CCR repository.

Read first:

backend/data/CCR_CANONICAL_DATA_MODEL_REPORT.md
backend/data/CCR_RELATIONSHIP_UNIVERSE_MODEL_REPORT.md

Inspect the existing Phase-3:

source policy
research runs
source_documents
evidence_snippets
GLEIF relationship observations
correlation candidate tables
relationship taxonomy

Do NOT duplicate existing tables unnecessarily.

No SEC calls.
No GLEIF calls.
No Web calls.
No Helix/AI calls.
No frontend work.
No production relationship discovery.

OBJECTIVE

Create the policy/schema foundation for a high-quality intelligence system
supporting:

DIRECT RELATIONSHIPS
INDIRECT PATHS
HIDDEN EXTERNALLY DISCOVERED RELATIONSHIPS
LOCAL CORRELATIONS
OBSERVED EVENTS
STRESS SCENARIOS

All must remain distinct.

==================================================
1. DIRECT RELATIONSHIP
==================================================

Define DIRECT as:

an evidence-backed relationship edge between two identified entities.

Examples:

SUPPLIER
CUSTOMER
PARENT
LENDER
TECHNOLOGY_PROVIDER

A direct relationship must have admissible evidence supporting that exact edge.

Do not allow:

same sector
same country
name similarity
candidate score
AI assertion

to create a direct relationship.

==================================================
2. INDIRECT RELATIONSHIP
==================================================

Define INDIRECT as:

a path composed of two or more defensible relationship edges.

Example:

CCR Client A
→ Technology Provider B
→ Critical Supplier C

The system may state:

"A has an indirect two-hop path to C."

Do NOT create a synthetic:

A → C

relationship edge.

The path itself is the analytical object.

==================================================
3. HIDDEN RELATIONSHIP
==================================================

Define:

HIDDEN_DIRECT

A real direct relationship absent from internal CCR data but discovered from
external admissible evidence.

HIDDEN_INDIRECT

A newly discovered multi-hop path assembled from defensible underlying edges.

"HIDDEN" must never mean unsupported inference.

==================================================
4. SOURCE QUALITY TIERS
==================================================

Create/validate:

TIER_0_INTERNAL

Validated CCR/master/internal authoritative data.

TIER_1_AUTHORITATIVE_EXTERNAL

Examples:
SEC
GLEIF
regulators
government
stock exchanges
official company filings
official investor relations
official company disclosures

TIER_2_HIGH_QUALITY_SECONDARY

Established financial/business journalism and high-quality specialist sources.

TIER_3_CORROBORATIVE

Specialist corroborating sources that normally should not establish a material
relationship alone.

INADMISSIBLE

Examples:
search snippets
anonymous posts
low-quality aggregators
SEO pages
AI-generated pages
unverified scraped copies

Search results are discovery aids, not evidence.

==================================================
5. RELATIONSHIP-SPECIFIC SOURCE STRATEGY
==================================================

Create configurable preferred source strategies.

Examples:

PARENT / ULTIMATE_PARENT
GLEIF
→ SEC
→ authoritative corporate/regulatory Web

SUBSIDIARY
SEC
→ GLEIF
→ authoritative corporate Web

SUPPLIER / CRITICAL_SUPPLIER
SEC
→ official company disclosure
→ high-quality secondary Web

CUSTOMER / KEY_CUSTOMER
SEC
→ official company disclosure
→ high-quality secondary Web

TECHNOLOGY_DEPENDENCY
SEC
→ official company disclosure
→ high-quality Web

INVESTOR / SPONSOR
SEC/regulatory
→ official corporate source
→ high-quality Web

LENDER / FINANCING
SEC
→ official disclosures
→ high-quality Web

STRATEGIC_PARTNER / JV
official company/regulatory
→ SEC
→ high-quality Web

This is configuration only.

No external execution yet.

==================================================
6. EVIDENCE DIMENSIONS
==================================================

Do NOT create one opaque confidence percentage.

Model separately:

IDENTITY_QUALITY
SOURCE_QUALITY
EVIDENCE_STRENGTH
FRESHNESS
CONSISTENCY
RELATIONSHIP_STATUS

Suggested controlled values:

HIGH
MEDIUM
LOW
UNKNOWN

where appropriate.

Relationship status should remain separately governed.

==================================================
7. RELATIONSHIP LIFECYCLE
==================================================

Support:

DISCOVERED_CLAIM
EVIDENCE_COLLECTED
PROPOSAL_PENDING_REVIEW
CONFIRMED
INSUFFICIENT_EVIDENCE
CONFLICT
REJECTED
HISTORICAL

RESEARCH_CANDIDATE remains outside the factual relationship lifecycle.

Do not automatically promote between states.

==================================================
8. PATH MODEL
==================================================

Create or validate structures capable of storing:

path_id
path_type

origin_entity_key
destination_entity_key

hop_count

created_from_event_id nullable
created_from_research_run nullable

and ordered path hops:

path_id
hop_number
from_entity_key
relationship_observation_id
to_entity_key

Every hop must point to a defensible stored relationship observation.

No synthetic hops.

==================================================
9. EVENT CONTRACT
==================================================

Prepare schema/contracts only.

Support:

OBSERVED_EVENT

Something that actually happened and must have evidence.

STRESS_SCENARIO

A hypothetical analyst scenario.

Never mix them.

Possible future event links:

event → entity
event → country
event → sector
event → industry
event → theme
event → relationship path
event → CCR subject/entity

Do not populate production events yet.

==================================================
10. EVENT TRANSMISSION
==================================================

Future event impact must preserve paths.

Example:

RATE SHOCK
→ refinancing pressure
→ company B
→ financing relationship
→ CCR client A

or:

TAIWAN DISRUPTION
→ semiconductor entity B
→ supplier relationship
→ CCR client A

Do not create relationship edges merely because an event may propagate through
them.

==================================================
11. CORRELATION SEPARATION
==================================================

Existing local correlation rows remain:

RESEARCH_CANDIDATE

They answer:

"Who should we research?"

Relationships answer:

"What can we substantiate?"

Events answer:

"What happened or what scenario are we testing?"

Paths answer:

"How could effects transmit?"

These four objects must remain distinct.

==================================================
12. AI POLICY
==================================================

Persist/document the following rules:

AI MAY:

- choose research strategy
- extract structured claims
- resolve context
- summarize evidence
- compare sources
- detect contradictions
- explain direct/indirect paths
- analyze events/scenarios

AI MAY NOT:

- be treated as evidence
- create a confirmed relationship without admissible evidence
- turn correlation into relationship
- invent missing path hops
- invent a source
- silently upgrade supplier to critical supplier

==================================================
13. VALIDATION
==================================================

Prove:

CCR subjects unchanged = 16,769

Canonical entities unchanged = 16,767

Production external entities unchanged = 0

Production relationships created = 0

Production events created = 0

Synthetic path hops = 0

Candidates promoted to relationships = 0

AI evidence rows = 0

External calls = 0

Foreign keys = PASS

Source hashes unchanged

==================================================
14. REPORT
==================================================

Create:

backend/data/CCR_RELATIONSHIP_EVIDENCE_PATH_POLICY.md

Include:

direct definition
indirect definition
hidden-direct definition
hidden-indirect definition
source tiers
relationship-specific source strategy
evidence dimensions
relationship lifecycle
path model
event vs stress distinction
correlation separation
AI policy
validation

FINAL RESPONSE:

CCR RELATIONSHIP EVIDENCE/PATH POLICY: PASS / FAIL

DIRECT MODEL:
PASS / FAIL

INDIRECT PATH MODEL:
PASS / FAIL

HIDDEN DIRECT MODEL:
PASS / FAIL

HIDDEN INDIRECT MODEL:
PASS / FAIL

SOURCE TIERS:
PASS / FAIL

RELATIONSHIP SOURCE STRATEGIES:
PASS / FAIL

EVIDENCE DIMENSIONS:
PASS / FAIL

RELATIONSHIP LIFECYCLE:
PASS / FAIL

EVENT / STRESS CONTRACT:
PASS / FAIL

CORRELATION SEPARATION:
PASS / FAIL

AI AS EVIDENCE:
0 / FAIL

SYNTHETIC PATH HOPS:
0 / FAIL

PRODUCTION RELATIONSHIPS CREATED:
0 / FAIL

PRODUCTION EVENTS CREATED:
0 / FAIL

EXTERNAL CALLS:
0 / FAIL

FOREIGN KEYS:
PASS / FAIL

REPORT:
backend/data/CCR_RELATIONSHIP_EVIDENCE_PATH_POLICY.md

STOP.
