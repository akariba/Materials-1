CCR RELATIONSHIP INTELLIGENCE — 3M / SOLVENTUM POSITIVE CONTROL

Work only in the CURRENT CCR repository.

Read first:

backend/data/CCR_RELATIONSHIP_PILOT_SEMANTICS_REPORT.md
backend/data/CCR_3M_RELATIONSHIP_PILOT_REPORT.md
backend/data/CCR_RESEARCH_ORCHESTRATOR_REPORT.md
backend/data/CCR_RELATIONSHIP_EVIDENCE_PATH_POLICY.md

This task is the FIRST positive-control relationship pilot.

Use only the already identified candidate:

3M CO
↔
SOLVENTUM CORP

Target relationship type:

MANUFACTURING_PARTNER

Do NOT broaden to other entities.

Do NOT run broad discovery.

Do NOT create CONFIRMED relationships.

Do NOT create production relationship_observations.

Do NOT use AI as evidence.

Do NOT use local correlation as evidence.

OBJECTIVE

Prove that one real, strongly evidenced relationship can pass:

identity
→ source
→ evidence
→ direction
→ taxonomy
→ qualification

and reach:

PROPOSAL_PENDING_REVIEW

without writing a production confirmed relationship.

==================================================
1. PIN BOTH ENTITIES
==================================================

Resolve both endpoints only from the existing CCR entity registry.

Use the existing master-backed entities already identified in the semantics
report.

Confirm for each:

entity_key
legal_name
GFCID where present
CAGID where present
LEI where present
identity class
identity quality
research eligibility

Expected:

3M CO = local/master-backed HIGH identity

SOLVENTUM CORP = local/master-backed HIGH identity

Do not create an EXTERNAL_ENTITY for Solventum.

==================================================
2. RESEARCH QUESTION
==================================================

Execute exactly one pair-research question:

Does the admissible evidence establish a MANUFACTURING_PARTNER relationship
between 3M CO and SOLVENTUM CORP?

Do not test:

CUSTOMER
SUPPLIER
SERVICE_PROVIDER
STRATEGIC_PARTNER

in this run.

Those remain separate hypotheses.

==================================================
3. PRIMARY EVIDENCE
==================================================

Use the existing cached official 2024 3M SEC 10-K identified in the prior
pilot as the first source.

Do not retrieve another document unless the configured evidence policy
requires corroboration.

Source must remain:

TIER_1_AUTHORITATIVE_EXTERNAL

Preserve:

source_document_id
official URL
filing/accession
filing date
content hash
evidence excerpt

Do not use a search snippet.

==================================================
4. EXACT CLAIM
==================================================

Extract only the claim supported by the filing.

The claim must identify:

subject = 3M CO
related entity = SOLVENTUM CORP
relationship_type = MANUFACTURING_PARTNER
direction

The evidence must explicitly support manufacturing/commercial/supply
arrangements sufficient for this taxonomy.

Do not interpret generic transition agreements or name co-occurrence as a
manufacturing partnership.

If the evidence does not specifically support MANUFACTURING_PARTNER:

return INSUFFICIENT_EVIDENCE.

==================================================
5. DIRECTION
==================================================

Direction must be explicit.

Use:

SUBJECT_TO_RELATED

only if the evidence and taxonomy contract support 3M → Solventum for the
requested relationship.

If the relationship is inherently reciprocal under the configured taxonomy,
store the configured reciprocal semantics explicitly.

Do not silently invent an inverse relationship.

If direction cannot be governed:

DIRECTION_UNRESOLVED

and do not qualify the proposal.

==================================================
6. TEMPORAL SEMANTICS
==================================================

Preserve whether the filing evidence describes:

CURRENT
HISTORICAL
TRANSITIONAL
UNKNOWN

Do not call a transitional manufacturing arrangement permanently current
without evidence.

If the evidence is tied to the 3M/Solventum separation period, retain that
temporal context.

==================================================
7. CLAIM QUALIFICATION
==================================================

The claim may qualify only if all gates pass:

subject identity resolved
related identity resolved
relationship type supported
direction resolved
admissible source
explicit evidence
evidence threshold met
no contradiction
review policy satisfied

Expected maximum state:

PROPOSAL_PENDING_REVIEW

Never CONFIRMED.

==================================================
8. SECOND SOURCE
==================================================

Use a second authoritative source only if the existing configured
MANUFACTURING_PARTNER policy requires it.

If required, prefer:

official Solventum disclosure
official 3M disclosure
SEC filing
other Tier-1 authoritative source

Do not introduce Tier-2 merely to force corroboration.

Do not lower evidence standards if no second source exists.

==================================================
9. PERSISTENCE
==================================================

Allowed research-layer persistence:

research plan
research run
research claim
source document reference
evidence snippet/reference
semantic outcome
proposal/review state if the existing model stores it outside production
relationship_observations

Do NOT create:

production relationship_observations
CONFIRMED relationship
synthetic relationship
external entity
indirect path
event
stress scenario

==================================================
10. POSITIVE-CONTROL EXPECTATION
==================================================

This is a positive-control candidate, not a forced positive result.

Expected if all evidence gates pass:

PROPOSAL_PENDING_REVIEW

Otherwise return the correct governed failure:

INSUFFICIENT_EVIDENCE
DIRECTION_UNRESOLVED
RELATIONSHIP_NOT_ESTABLISHED
CONFLICT_REVIEW_REQUIRED

Do not change logic merely to achieve a proposal.

==================================================
11. QUALITY REVIEW
==================================================

Before qualifying the claim verify:

3M is the correct subject
Solventum is the correct counterparty
both identities are resolved
the quoted evidence supports manufacturing partnership
the relationship type is not overstated
direction is governed
temporal meaning is preserved
the source is admissible
the source document and evidence excerpt are linked

==================================================
12. VALIDATION
==================================================

Run targeted positive-control tests first.

Then run full backend regression.

Expected:

0 failed
0 errors

Confirm:

Phase-2 protected hash unchanged
canonical counts unchanged
production relationship observations = 0
confirmed relationships = 0
external entities created = 0
synthetic edges = 0
AI evidence = 0
foreign-key violations = 0
SQLite integrity = ok

==================================================
13. REPORT
==================================================

Create:

backend/data/CCR_3M_SOLVENTUM_POSITIVE_CONTROL_REPORT.md

Include:

entity identities
research question
taxonomy
source document
exact evidence excerpt
direction decision
temporal semantics
qualification gates
semantic outcome
persistence performed
quality review
regression

==================================================
FINAL RESPONSE
==================================================

CCR 3M / SOLVENTUM POSITIVE CONTROL: PASS / FAIL

SUBJECT:
3M CO

RELATED ENTITY:
SOLVENTUM CORP

RELATIONSHIP TYPE:
MANUFACTURING_PARTNER

SUBJECT IDENTITY:
RESOLVED / FAIL

RELATED IDENTITY:
RESOLVED / FAIL

PRIMARY SOURCE:
<source>

SOURCE TIER:
<actual>

EVIDENCE EXCERPT:
<short exact excerpt>

DIRECTION:
<actual>

TEMPORAL SEMANTICS:
<actual>

EVIDENCE THRESHOLD:
PASS / FAIL

SEMANTIC OUTCOME:
<actual>

PROPOSAL_PENDING_REVIEW:
YES / NO

PRODUCTION RELATIONSHIP OBSERVATIONS CREATED:
0 / FAIL

CONFIRMED RELATIONSHIPS CREATED:
0 / FAIL

EXTERNAL ENTITIES CREATED:
0 / FAIL

SYNTHETIC EDGES:
0 / FAIL

AI AS EVIDENCE:
0 / FAIL

REGRESSION
passed:
failed:
errors:

SQLITE INTEGRITY:
PASS / FAIL

FOREIGN KEYS:
PASS / FAIL

REPORT:
backend/data/CCR_3M_SOLVENTUM_POSITIVE_CONTROL_REPORT.md

STOP.
