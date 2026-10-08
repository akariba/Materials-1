CLEANUP IS ACCEPTED.

Do not undo the completed cleanup commits.

Do not continue repository cleanup now.
Do not change the frontend yet.
Do not reopen ADK grounding debugging.
Do not restore SQLite.

We now move to the REAL production CCR relationship pipeline.

==================================================
FIRST: CONFIRM THE PRODUCTION RELATIONSHIP STORE
==================================================

Before implementing anything, inspect the current 364-row production
relationship artifact loaded by the production API.

Report:

- exact Parquet/file path
- schema
- row count
- unique entity count
- relationship types
- evidence-status values
- source/provenance values
- direct/indirect/hidden representation if any
- canonical entity ID fields
- whether multiple relationships between the same pair are supported
- whether hierarchy/ownership relationships already exist
- whether relationship strength/scoring already exists

Do not create another relationship store.

This current production relationship artifact must be reused or carefully
extended.

==================================================
SECOND: NVIDIA PRODUCTION SLICE
==================================================

Find NVIDIA Corporation by canonical CAGID/entity ID in the production
canonical universe.

Then extract the complete NVIDIA-connected slice from:

1. current production relationship artifact
2. CAM passages / entity mentions
3. existing CAM-derived relationship candidates
4. existing validated external evidence
5. existing review-required candidates

Report what ALREADY exists before generating anything new.

==================================================
THIRD: CAM FACTS AND EXPOSURES
==================================================

For NVIDIA and its connected entities, inspect CAM deterministically for:

- Citi EXP
- TFA
- facility amounts
- lending exposure
- RLR
- FORR
- country of risk
- industry / sector
- parent
- subsidiary
- ownership
- guarantor
- collateral
- maturity
- customer
- supplier
- investor / investee
- strategic partnership
- lease
- offtake
- financing
- material contracts
- hierarchy relationships

For each extracted value preserve:

- canonical entity ID
- field name
- raw value
- normalized value
- CAM document
- page/section
- exact excerpt
- extraction timestamp

Do not infer numerical exposure fields.

==================================================
FOURTH: CANONICAL DATA CLASSES
==================================================

Use:

FACT
DERIVED
EXPOSURE
AI_CANDIDATE

FACT
= explicit CAM or validated external evidence.

EXPOSURE
= Citi internal exposure information.

DERIVED
= deterministic calculation from verified facts.

AI_CANDIDATE
= proposed relationship requiring further validation.

Do not mix these classes.

==================================================
FIFTH: RELATIONSHIP TYPES
==================================================

Ensure the production relationship model supports at least:

parent
subsidiary
ownership
investor
investee
supplier
customer
guarantor
borrower
lender
strategic_partner
joint_venture
lessor
lessee
offtaker
provider
financing
collateral_dependency
commercial_dependency
shared_project
SPV_relationship

Do not fabricate missing relationships.

Do not collapse different relationship types between the same entity pair.

==================================================
SIXTH: INDIRECT
==================================================

Indirect relationships must be graph-derived from VERIFIED direct edges.

Example:

NVIDIA → A
A → B

creates:

NVIDIA → A → B

Store separately from direct facts:

- origin
- destination
- path
- hop count
- edge relationship types
- path strength
- supporting edge IDs

Use recovered typed-path logic if it exists.

==================================================
SEVENTH: HIDDEN / REVIEW REQUIRED
==================================================

Hidden relationships are not automatically facts.

R2D2 / Opus may identify:

- common supplier
- common customer
- shared project
- shared SPV
- common financing
- common guarantor
- infrastructure dependency
- revenue dependency

Initially store as:

AI_CANDIDATE
REVIEW_REQUIRED

For every REVIEW_REQUIRED item, retain an explicit reason such as:

ENTITY_AMBIGUOUS
INSUFFICIENT_EVIDENCE
CONTRADICTORY_EVIDENCE
MISSING_DIRECT_SOURCE
UNRESOLVED_DIRECTION
UNRESOLVED_CANONICAL_ID

This will make "Review Required" meaningful in the UI later.

==================================================
EIGHTH: R2D2 + OPUS
==================================================

Only after existing production/CAM facts have been inventoried:

Use R2D2 for targeted evidence retrieval.

Then use Opus to refine:

- entity reconciliation
- hierarchy
- ownership
- relationship classification
- direction
- duplicate handling
- contradictions
- candidate ranking

Opus must return structured JSON.

Opus may not create Citi EXP/TFA.

Opus may not promote unsupported relationships to FACT.

==================================================
NINTH: DIRECT EXTERNAL SOURCES
==================================================

Reuse the already-proven direct-fetch implementation.

Do not depend on generic grounded-search metadata.

Use:

SEC
official company IR
company newsroom
annual reports
approved direct publisher sources

Known URL
→ direct fetch
→ source text
→ exact excerpt
→ deterministic validator

==================================================
TENTH: DO NOT TOUCH FRONTEND YET
==================================================

The frontend currently has only a static delivered artifact.

Do not continue editing frontend/dist/index.html while building the backend.

First make the NVIDIA backend production slice correct.

Frontend integration will be a separate phase.

==================================================
ACCEPTANCE REPORT
==================================================

Report:

PRODUCTION RELATIONSHIP ARTIFACT:
<path>

ROWS:
<count>

NVIDIA EXISTING DIRECT:
<count>

NVIDIA NEW VERIFIED DIRECT:
<count>

NVIDIA INDIRECT:
<count>

NVIDIA REVIEW_REQUIRED:
<count>

HIERARCHY RELATIONSHIPS:
<count>

OWNERSHIP RELATIONSHIPS:
<count>

CITI EXP:
POPULATED / NOT_PRESENT

TFA:
POPULATED / NOT_PRESENT

RLR:
<value/not present>

FORR:
<value/not present>

R2D2:
WORKING / BLOCKED

OPUS:
WORKING / BLOCKED

DIRECT SOURCE:
WORKING / BLOCKED

TESTS:
<passed>/<total>

Do not alter the frontend.

STOP after the NVIDIA production backend slice is complete.