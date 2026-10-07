Continue the existing NVIDIA CAM relationship task from the current state.

Do NOT start SEC/web enrichment yet.
Do NOT change architecture, prompts, taxonomy, entity resolution, or relationship logic unless a validation failure proves a concrete defect.

Complete the remaining existing TODO items only:

1. Inspect all generated NVIDIA relationship artifacts.
2. Validate every final VERIFIED relationship directly against its source CAM evidence:
   - correct NVIDIA identity
   - correct target identity
   - correct relationship type
   - correct direction
   - exact evidence excerpt
   - document/page/section provenance
   - semantic checker result
   - deterministic checker result
3. Confirm all REVIEW_REQUIRED candidates remain outside the verified Parquet.
4. Confirm NO_RELATIONSHIP passages remain excluded from relationship output.
5. Run the focused NVIDIA tests and full regression suite.
6. Report any failures or warnings.
7. Produce the final CAM-only NVIDIA summary.
8. Mark all current TODO items complete.

Do not rerun expensive LLM extraction unless required to reproduce a failed validation.

Final summary must report:

- passages processed
- candidates proposed
- verified relationships
- review-required candidates
- no-relationship passages
- rejected candidates
- regression tests passed/failed
- warnings
- exact final verified relationships with evidence and canonical target resolution

Return exactly one final status:

NVIDIA_CAM_PHASE_COMPLETE

NVIDIA_CAM_PHASE_COMPLETE_WITH_WARNINGS

BLOCKED_BY_VALIDATION_FAILURE

STOP after closing the existing TODO list.

Do NOT proceed automatically to SEC/web enrichment.
