CONTINUE FROM CURRENT STATE — DO NOT START OVER

Continue the Lending External Research Overlay backend task from exactly the
current repository/session state.

Do NOT restart the implementation.
Do NOT rerun V3 extraction.
Do NOT modify V1, V2, V3 relationship data or source artifacts.
Do NOT modify the Stylus preset.
Do NOT modify the frontend.
Do NOT touch CCR.

First inspect the current working tree and distinguish:

1. changes that existed before this external-overlay task;
2. changes created by this task.

IMPORTANT:
The existing V3 files visible in the working tree may contain approved
pre-existing changes from the completed V3/Project Miner work.

Do NOT overwrite, revert, regenerate, or normalize them merely because they
appear modified.

Continue only the external-overlay implementation.

Complete ALL remaining tasks:

1. Finish backend conventions/fixture integration.
2. Finish overlay data models/schema.
3. Finish normalization and governance service.
4. Finish explicit external-research API boundary.
5. Finish cache implementation.
6. Finish focused automated tests.
7. Run validation and produce the required statistics report.

Use:
CoreWeave_NVIDIA_Relationship_Research.json

as the golden fixture.

Acceptance requirements remain:

- exactly 2 semantic findings:
  supplier
  technology_dependency

- supplier direction:
  NVIDIA -> CoreWeave / B_TO_A

- technology_dependency direction:
  CoreWeave -> NVIDIA / A_TO_B

- external data remains separate from CAM V3
- SEC source normalization enforced
- duplicate evidence controlled
- cross_source_corroboration recomputed by backend
- no fuzzy entity guessing
- no invented CAGIDs
- caching works
- read endpoints never trigger external research
- startup never triggers external research
- external execution requires explicit POST/user action
- frontend untouched
- CCR untouched

Do not make a live Stylus/R2D2/SEC call unless absolutely required for the
final acceptance test and the existing configured runner is already
available.

The local golden-fixture test is sufficient for this stage.

Before completion verify regression protection:

- V1 unchanged
- V2 unchanged
- V3 canonical relationships = 13
- V3 review-required relationships = 28
- V3 unresolved document subjects = 0
- approved V3 digest/hash unchanged from the state at the start of this task
- Stylus preset unchanged

If any unexpected V3 difference is detected:
STOP modifying it.
Report the difference.
Do not attempt to repair V3 automatically.

At the end generate:

backend/data/LENDING_EXTERNAL_OVERLAY_VALIDATION_REPORT.md

and, if already planned,
backend/data/LENDING_EXTERNAL_OVERLAY_VALIDATION_REPORT.json

Final response must contain:

LENDING EXTERNAL OVERLAY BACKEND: PASS / FAIL

Golden fixture parsed:
Fixture findings received:
Semantic findings retained:

Supplier direction:
Technology dependency direction:

Evidence received:
Evidence retained:
Evidence filtered/flagged:

SEC evidence normalized:
SEC duplicated as Web:

Backend cross-source corroboration recomputed:

Entity matches:
Unresolved entity matches:

CAM_CORROBORATION:
EXTERNAL_PROPOSAL_PENDING_REVIEW:
CONFLICT_REVIEW_REQUIRED:
NO_EXTERNAL_CORROBORATION:
MENTION_ONLY:
INSUFFICIENT_EVIDENCE:

Cache write:
Cache read:
Duplicate execution prevented:

Explicit-run-only:
Automatic startup executions:
Automatic read executions:

Tests passed:
Tests failed:

V1 unchanged:
V2 unchanged:
V3 unchanged:
Stylus preset unchanged:
Frontend unchanged:
CCR untouched:

Validation report:
<path>

READY FOR PORTFOLIO API + UI INTEGRATION:
YES / NO

If NO, list only genuine blockers.

Then STOP.
