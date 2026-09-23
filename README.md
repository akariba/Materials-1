CCR RELATIONSHIP INTELLIGENCE — RESEARCH ORCHESTRATOR FOUNDATION

Work only in the CURRENT CCR repository.

Read first:

backend/data/CCR_CANONICAL_DATA_MODEL_REPORT.md
backend/data/CCR_RELATIONSHIP_UNIVERSE_MODEL_REPORT.md
backend/data/CCR_RELATIONSHIP_EVIDENCE_PATH_POLICY.md

Inspect existing:

research_runs
research_requests
provider cache
source_documents
evidence_snippets
SEC provider code
GLEIF provider code
Web provider interface
relationship source strategies
analysis configurations

Do not duplicate working Phase-3 infrastructure.

IMPORTANT

This task builds the research orchestration layer.

Do NOT perform broad external research yet.

Do NOT create production confirmed relationships.

Do NOT run across the full CCR population.

A few bounded connectivity/contract tests are allowed only if required,
but the primary objective is orchestration logic.

==================================================
1. OBJECTIVE
==================================================

Create a central Research Orchestrator that receives a structured research
question such as:

"Does Entity A have a technology dependency on Entity B?"

or:

"Discover material suppliers for Entity A."

and determines:

- relationship type
- direction
- eligible source channels
- preferred source order
- required evidence threshold
- entity-resolution requirements
- stopping conditions
- final governed outcome

The orchestrator must return one of:

PROPOSAL_PENDING_REVIEW
INSUFFICIENT_EVIDENCE
CONFLICT
NOT_FOUND
PROVIDER_UNAVAILABLE
IDENTITY_UNRESOLVED

Never silently return CONFIRMED.

==================================================
2. CREATE ORCHESTRATOR MODULE
==================================================

Create a focused backend module such as:

backend/app/core/relationship_research_orchestrator.py

or equivalent consistent project location.

Core input:

subject_entity_key
optional related_entity_key
relationship_type
analysis_config_id/version
as_of_date
research_scope

Supported research scopes:

PAIR_RESEARCH
ENTITY_RELATIONSHIP_DISCOVERY

PAIR_RESEARCH:

A and B are known.

Question:
does relationship X exist?

ENTITY_RELATIONSHIP_DISCOVERY:

A is known.

Question:
which entities have relationship X with A?

==================================================
3. SOURCE STRATEGY SELECTION
==================================================

Read the existing relationship-specific source policy.

Do not hardcode one global order.

Examples:

PARENT / ULTIMATE_PARENT
GLEIF
→ SEC
→ authoritative Web

SUPPLIER / CRITICAL_SUPPLIER
SEC
→ official company Web
→ high-quality Web

CUSTOMER / KEY_CUSTOMER
SEC
→ official company Web
→ high-quality Web

TECHNOLOGY_DEPENDENCY
SEC
→ official company Web
→ high-quality Web

INVESTOR / SPONSOR
SEC/regulatory
→ official company source
→ high-quality Web

LENDER / FINANCING
SEC
→ official disclosure
→ high-quality Web

STRATEGIC_PARTNER / JV
official company/regulatory
→ SEC
→ high-quality Web

Return the selected strategy with every research run.

==================================================
4. FALLBACK LOGIC
==================================================

Implement source fallback correctly.

Example:

Try preferred Tier-1 source.

If:

NOT_APPLICABLE
NOT_FOUND
PROVIDER_UNAVAILABLE

then continue to the next permitted source.

Do NOT interpret:

NOT_FOUND

as proof that the relationship does not exist.

Do NOT downgrade automatically to low-quality sources.

If only inadmissible evidence exists:

INSUFFICIENT_EVIDENCE

==================================================
5. EVIDENCE THRESHOLDS
==================================================

Create configurable evidence rules per relationship type.

Example conceptual rules:

PARENT / ULTIMATE_PARENT

one authoritative Tier-1 structural source may be sufficient for proposal.

SUPPLIER / CUSTOMER

explicit Tier-1 disclosure preferred.

Tier-2 alone should normally require corroboration.

CRITICAL_SUPPLIER / KEY_CUSTOMER

must require explicit materiality/dependency/concentration evidence.

TECHNOLOGY_DEPENDENCY

must require explicit use/dependency/support evidence.

Do not treat simple company-name co-occurrence as relationship evidence.

==================================================
6. RESEARCH PLAN
==================================================

Before execution produce a research plan:

research_plan_id
subject
related entity if supplied
relationship type

sources planned
source order
minimum source tier
minimum evidence count
primary-source requirement
multi-source requirement
entity-resolution requirement

Persist the plan.

==================================================
7. PROVIDER ABSTRACTION
==================================================

Normalize provider outputs.

Each provider attempt should return:

provider
status

documents_found
claims_found
identity_candidates
evidence_candidates

network_requests
cache_hits

error_category
error_message_safe

Statuses:

SUCCESS
NOT_FOUND
NOT_APPLICABLE
UNAVAILABLE
ERROR

The orchestrator should not need provider-specific response logic everywhere.

==================================================
8. ENTITY RESOLUTION GATE
==================================================

Before creating a relationship proposal:

subject identity must be trusted.

related entity identity must be trusted enough to become:

existing entity

or

defensible EXTERNAL_ENTITY

Do NOT create external entities from:

search snippets
name similarity only
AI guesses
local correlation only

Identity evidence must support creation.

==================================================
9. CLAIM MODEL
==================================================

Create a structured discovered-claim object.

Fields/concepts:

claim_id
research_run_id
subject_entity_key
candidate_related_entity_key nullable
relationship_type
direction

claim_text
source_document_id
evidence_snippet_id

source_tier
evidence_strength

current/historical/unknown
claim_status

A discovered claim is NOT yet a production relationship.

==================================================
10. CONTRADICTION HANDLING
==================================================

The orchestrator must compare evidence.

Examples:

Source A says parent = X.
Source B says parent = Y.

Outcome:

CONFLICT

not:

pick whichever appears first.

Historical vs current differences must also be preserved.

==================================================
11. STOPPING RULES
==================================================

Research should stop when:

required evidence threshold is satisfied

OR

all permitted source channels exhausted

OR

identity cannot be resolved

OR

policy prohibits weaker fallback

OR

provider availability prevents completion

Persist why research stopped.

==================================================
12. AI ROLE CONTRACT
==================================================

Prepare integration points for Helix AI, but do not require AI execution yet.

AI will later be allowed to:

extract claims
classify relationship type
extract direction
summarize evidence
detect contradiction
explain findings

AI may NOT:

be evidence
create an entity without identity evidence
upgrade a proposal to confirmed
invent missing documents

The orchestrator must remain usable with deterministic/provider extraction
without AI.

==================================================
13. OUTPUT CONTRACT
==================================================

Research result should return:

research_run_id
research_plan
subject
related entity/entities
relationship type

outcome

claims
evidence
source attempts

identity_quality
source_quality
evidence_strength
freshness
consistency

research_gaps

recommended_next_action

No single opaque confidence percentage.

==================================================
14. NO AUTOMATIC CONFIRMATION
==================================================

This phase must not directly create:

CONFIRMED

relationships.

At most create:

PROPOSAL_PENDING_REVIEW

after evidence threshold passes.

Review/promotion comes later.

==================================================
15. BOUNDED TESTS
==================================================

Use mocks/fixtures or existing cached provider data where possible.

Prove scenarios:

A. Tier-1 evidence found
→ proposal

B. preferred source not applicable
→ fallback to next source

C. Tier-2 weak evidence only
→ insufficient evidence

D. conflicting authoritative evidence
→ conflict

E. identity unresolved
→ identity unresolved

F. providers unavailable
→ provider unavailable

G. AI unavailable
→ orchestrator still functions

No broad production research.

==================================================
16. PRODUCTION SAFETY
==================================================

After tests:

Production external entity count should remain unchanged unless an explicitly
approved isolated identity fixture is rolled back.

Production relationship count must remain:

0

Production event count:

0

No candidate promotion.

No source file changes.

==================================================
17. REPORT
==================================================

Create:

backend/data/CCR_RESEARCH_ORCHESTRATOR_REPORT.md

Include:

architecture
research-plan contract
source selection
fallback rules
evidence thresholds
provider result contract
identity gate
claim model
contradiction handling
stopping rules
AI boundary
tests
known limitations

==================================================
18. FINAL RESPONSE
==================================================

Return:

CCR RESEARCH ORCHESTRATOR: PASS / FAIL

PAIR RESEARCH:
PASS / FAIL

ENTITY DISCOVERY:
PASS / FAIL

SOURCE STRATEGY SELECTION:
PASS / FAIL

SOURCE FALLBACK:
PASS / FAIL

EVIDENCE THRESHOLDS:
PASS / FAIL

IDENTITY GATE:
PASS / FAIL

CLAIM MODEL:
PASS / FAIL

CONTRADICTION HANDLING:
PASS / FAIL

STOPPING RULES:
PASS / FAIL

AI OPTIONAL:
PASS / FAIL

TEST CASES:
Tier-1 success:
Fallback:
Weak Tier-2:
Conflict:
Identity unresolved:
Provider unavailable:

PRODUCTION EXTERNAL ENTITIES CREATED:
0 / FAIL

PRODUCTION RELATIONSHIPS CREATED:
0 / FAIL

CANDIDATES PROMOTED:
0 / FAIL

EXTERNAL CALLS:
<actual bounded count>

FOREIGN KEYS:
PASS / FAIL

REPORT:
backend/data/CCR_RESEARCH_ORCHESTRATOR_REPORT.md

STOP.
