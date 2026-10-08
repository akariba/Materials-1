Before frontend integration, validate the NVIDIA backend artifacts.

Do NOT modify frontend.
Do NOT run new enrichment.
Do NOT create another relationship store.

1. Explain exactly what the 246-row additive production snapshot is.

Report:
- source artifact(s)
- original production row count
- snapshot row count
- whether it is a subset, deduplicated view, merged view, or replacement
- whether any production relationships were dropped
- whether the canonical production relationship artifact was modified

The existing production relationship source of truth must NOT be replaced
by a bounded NVIDIA artifact.

2. Validate the 31 indirect paths.

For every indirect path confirm:
- origin = NVIDIA where applicable
- destination
- intermediate entities
- hop count
- every underlying edge ID
- every underlying edge evidence status

No REVIEW_REQUIRED, AI_CANDIDATE, unsupported, or rejected edge may be used
to generate a VERIFIED indirect path.

Report:
VERIFIED_EDGE_ONLY_PATHS = YES/NO

3. Validate Citi EXP / TFA absence.

Search the repaired CAM index and exact NVIDIA-linked CAM records for:
- Citi EXP
- Citi exposure
- TFA
- facility amount
- total facility
- exposure
- committed amount
- limit

Determine whether:
A. NVIDIA genuinely has no exact subject-level value, or
B. values exist but current field mapping failed.

Return:
CITI_EXP = NOT_PRESENT_IN_SOURCE / MAPPING_GAP / POPULATED
TFA = NOT_PRESENT_IN_SOURCE / MAPPING_GAP / POPULATED

Do not estimate values.

4. Confirm the 3 verified direct relationships.

For each report:
- source entity
- target entity
- relationship type
- direction
- exact evidence source
- exact excerpt
- canonical IDs
- evidence status

5. Confirm candidate isolation.

The 63 candidates and all review-required records must remain outside
verified graph calculations.

Report:
CANDIDATES_USED_AS_VERIFIED = 0

6. Final status

Return:

PRODUCTION_SOURCE_OF_TRUTH_PRESERVED = YES/NO
VERIFIED_EDGE_ONLY_PATHS = YES/NO
CANDIDATES_USED_AS_VERIFIED = <count>
CITI_EXP = ...
TFA = ...
VERIFIED_DIRECT = <count>
INDIRECT_PATHS = <count>
TESTS = <passed>/<total>

STOP after validation.