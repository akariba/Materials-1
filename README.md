CLIENT CORRELATION — STAGE 2A.1 CORRECTION
CREATE THE ACTUAL STYLUS DEPLOYMENT PACK

IMPORTANT:

The prior migration correctly preserved the original Stylus material,
but inspection now confirms that the adapted V1 YAML still contains OLD CAM
semantics such as:

- corroborate an existing CAM relationship
- propose a new relationship relative to CAM
- identify a conflict with CAM
- never overwrite CAM
- CAM_CORROBORATION
- CAM_CONFLICT

That is NOT the final Client Correlation policy.

DO NOT modify the preserved originals.

Use the existing local files as source material, especially:

backend/config/lending_relationship_research_preset_v1.yaml

and the migrated V1 knowledge files already created.

This task must now create a SEPARATE deployment-ready policy pack.

==================================================
1. PRESERVE ORIGINALS
==================================================

Do not change:

- original Stylus preset
- original knowledge files
- preserved recovery/archive material

Also preserve the current migrated V1 YAML for audit.

We are producing a NEW deployment representation.

==================================================
2. NEW AUTHORITY MODEL
==================================================

Replace CAM-centric authority semantics in the DEPLOYMENT version only.

NEW MODEL:

The 3.67M Client Universe is authoritative ONLY for:

- internal client identity
- GFCID
- client_id
- master-source attributes
- source lineage

It is NOT authoritative for external relationships.

External evidence from approved sources may independently establish a
relationship observation when the evidence policy is satisfied.

External evidence may NEVER silently alter Client Universe identity.

There is no CAM relationship authority in the new product.

==================================================
3. REPLACE OLD FINDING SEMANTICS
==================================================

Remove these from the deployment contract:

CAM_CORROBORATION
CAM_CONFLICT
NO_EXTERNAL_CORROBORATION
CAM-confirmed
CAM relationship authority

Use:

RELATIONSHIP_OBSERVATION
RELATIONSHIP_CANDIDATE
EVIDENCE_CONFLICT
MENTION_ONLY
NO_EVIDENCE

Definitions:

RELATIONSHIP_OBSERVATION
= admissible evidence directly establishes the relationship.

RELATIONSHIP_CANDIDATE
= discovery signal exists but acceptance requirements are not yet satisfied.

EVIDENCE_CONFLICT
= credible sources materially disagree about the relationship semantics,
direction, status, identity, or timing.

MENTION_ONLY
= entities are mentioned but relationship semantics are not established.

NO_EVIDENCE
= no admissible evidence supports the requested relationship.

==================================================
4. DISCOVERY PHILOSOPHY
==================================================

Add this explicit principle:

SEARCH BROADLY.
ACCEPT NARROWLY.

Discovery may investigate many plausible relationships.

Only policy-compliant evidence may create a RELATIONSHIP_OBSERVATION.

A candidate is never automatically an observation.

Co-mention is never sufficient.

==================================================
5. SOURCE CHANNELS
==================================================

Deployment source channels must support exactly:

SEC_FILING
R2D2_WEB
GLEIF

Maintain R2D2_WEB for Stylus compatibility.

Document:

R2D2_WEB semantically represents APPROVED_WEB in the application.

GLEIF is primarily appropriate for:

- legal-entity identity
- direct parent
- ultimate parent
- ownership hierarchy
- LEI resolution

SEC and Web support broader relationship research.

==================================================
6. KEEP SIX INPUTS EXACTLY
==================================================

Preserve names and order:

SubjectEntity
RelatedEntity
RelationshipScope
SourceChannels
ResearchInstruction
AsOfDate

Rules:

SubjectEntity = required
RelatedEntity = OPTIONAL
RelationshipScope = required
SourceChannels = required
ResearchInstruction = required
AsOfDate = required

Do not add runtime fields.

==================================================
7. RELATIONSHIP SCOPE
==================================================

Support:

MAXIMUM_RELATIONSHIP_DISCOVERY

Meaning:

Discover the maximum defensible credit-relevant relationships permitted by
the canonical taxonomy.

Prioritize:

ownership
parent/subsidiary
suppliers
customers
customer dependency
critical suppliers
lenders/financing
investors/sponsors
guarantors
joint ventures
strategic partners
contractual counterparties
technology dependencies
infrastructure dependencies
service providers
revenue concentration
other existing taxonomy-approved relationship types

Do not invent types outside the canonical taxonomy.

==================================================
8. HIDDEN / INDIRECT PATHS
==================================================

Preserve the existing strong Stylus rule:

A -> B -> C

A -> B must independently have admissible evidence.
B -> C must independently have admissible evidence.

If either hop is insufficient:

A -> B -> C must not be represented as a validated hidden path.

Do NOT create a synthetic direct A -> C relationship.

Overall hidden-path strength cannot exceed the weakest hop.

==================================================
9. RESOLVE FINDINGS VS EVIDENCE CONTRACT
==================================================

The previous migration identified an inherited ambiguity between
`findings` and `evidence`.

Resolve it now.

Canonical output:

findings[]

Each finding represents ONE semantic relationship.

Each finding contains:

evidence[]

Therefore:

finding != evidence object

Evidence objects support findings.

Do not maintain two competing top-level relationship representations.

For the same:

subject
related_entity
relationship_type
direction

return ONE finding and aggregate admissible supporting evidence into its
evidence[] array.

If the same pair has different relationship types, return separate findings.

==================================================
10. OUTPUT MODEL
==================================================

Each finding should support:

subject_entity
related_entity

relationship_type
relationship_status
connectivity
direction

finding_type

confidence
credit_materiality

evidence[]

conflict

analyst_review_required

Entity references should support where available:

client_id
gfcid
source_master_id
legal_name
external_entity_id

Use null where unavailable.

Never invent identifiers.

Each evidence object should support:

source_channel
source_tier
source_title
source_reference
publication_date
exact_excerpt
evidence_role

Preserve other existing useful policy fields when compatible.

==================================================
11. UPDATE KNOWLEDGE FILES FOR DEPLOYMENT
==================================================

Create:

backend/config/relationship_discovery/stylus_deployment/

and:

backend/config/relationship_discovery/stylus_deployment/knowledge/

Create deployment-ready adapted copies of:

00 readiness policy
01 relationship taxonomy/policy
02 evidence/confidence/materiality
03 structured output/runtime inputs
04 examples/guardrails

Do not overwrite original copies.

Remove CAM authority semantics from the deployment versions.

Update examples so they use the Client Universe / external-evidence model.

==================================================
12. CREATE ACTUAL STYLUS PROMPT TXT
==================================================

CREATE THIS FILE — it does not currently exist:

backend/config/relationship_discovery/stylus_deployment/
LENDING_RELATIONSHIP_RESEARCH_V1_PROMPT.txt

Generate it from the adapted policy.

This is the exact text I will manually paste into Stylus.

It must contain ZERO CAM authority references.

It must preserve the six exact runtime placeholders:

{{SubjectEntity}}
{{RelatedEntity}}
{{RelationshipScope}}
{{SourceChannels}}
{{ResearchInstruction}}
{{AsOfDate}}

==================================================
13. CREATE DEPLOYMENT MANIFEST
==================================================

Create:

backend/config/relationship_discovery/stylus_deployment/
STYLUS_DEPLOYMENT_MANIFEST.md

Include:

Preset name:
Lending Relationship Research - Web + SEC + GLEIF

Prompt path

Six input fields + required state

Knowledge files in exact upload order

SHA-256 of prompt and every knowledge file

Supported RelationshipScope values

Supported SourceChannels

==================================================
14. VALIDATION
==================================================

Run deterministic tests.

Required checks:

CAM authority references in deployment pack = 0

CAM_CORROBORATION occurrences = 0

CAM_CONFLICT occurrences = 0

six input names preserved exactly

RelatedEntity optional

SEC_FILING accepted

R2D2_WEB accepted

GLEIF accepted

MAXIMUM_RELATIONSHIP_DISCOVERY accepted

co-mention rejected

findings/evidence hierarchy validated

duplicate semantic relationship consolidation validated

multi-relationship same-pair behavior validated

direction semantics validated

hidden-path weakest-hop rule validated

invalid relationship type rejected

structured JSON schema validated

Do not call external providers.

Do not run Stylus.

Do not create relationships.

==================================================
15. FINAL RESPONSE
==================================================

STYLUS DEPLOYMENT PACK: PASS / FAIL

SOURCE V1 YAML:
<path>

DEPLOYMENT PROMPT CREATED:
YES / NO

DEPLOYMENT PROMPT:
<exact path>

CAM REFERENCES:
0 / FAIL

CAM_CORROBORATION:
0 / FAIL

CAM_CONFLICT:
0 / FAIL

INPUT COUNT:
6 / FAIL

RELATEDENTITY OPTIONAL:
YES / NO

MAXIMUM_RELATIONSHIP_DISCOVERY:
PASS / FAIL

SEC_FILING:
PASS / FAIL

R2D2_WEB:
PASS / FAIL

GLEIF:
PASS / FAIL

FINDINGS/EVIDENCE CONTRACT:
RESOLVED / FAIL

KNOWLEDGE FILES:
<actual count>

TESTS:
<passed>/<total>

MANIFEST:
<path>

EXTERNAL RESEARCH EXECUTED:
0

RELATIONSHIPS CREATED:
0

STOP.
