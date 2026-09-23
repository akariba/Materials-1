You are working on the existing Lending Relationship Intelligence repository.

READ-ONLY ANALYSIS ONLY.

Do not modify source code.
Do not modify databases.
Do not change V2 or V3.
Do not change the normalized store.
Do not change the UI.
Do not change the Stylus preset yet.

We now have a manually adjudicated benchmark of 37 source-supported relationships.

The previous analysis established that relationship loss is mixed across:

- extraction / source scope
- entity resolution
- taxonomy mapping
- evidence gating
- confidence gating
- direction/state gating
- deduplication
- V3 scope policy
- global API visibility

I now need a STAGE-BY-STAGE LOSS ATTRIBUTION.

For each of the 37 benchmark relationships, trace the relationship through the actual pipeline as far upstream as the repository artifacts allow.

For every benchmark relationship produce one row with:

1. source document
2. expected subject
3. expected related entity
4. expected relationship type
5. exact source evidence / source location
6. raw relationship observation found? YES/NO/UNKNOWN
7. candidate extracted? YES/NO/UNKNOWN
8. extracted subject text
9. extracted related-entity text
10. extracted relationship type
11. entity resolution result
12. canonical subject
13. canonical related entity
14. taxonomy mapping result
15. evidence gate result
16. confidence gate result
17. direction/state gate result
18. deduplication result
19. V3 scope result
20. final V3 status
21. normalized-store status
22. global API visible? YES/NO
23. primary loss stage
24. secondary contributing issue
25. evidence supporting that diagnosis

Use only evidence that actually exists in repository artifacts.

If an intermediate stage was not persisted and therefore cannot be inspected, mark it UNKNOWN.
Do not infer that "missing from V3" means extraction failure.

--------------------------------------------------
LOSS STAGES
--------------------------------------------------

Assign exactly one PRIMARY stage where possible:

A_RAW_NOT_FOUND
B_EXTRACTION
C_ENTITY_RESOLUTION
D_TAXONOMY
E_EVIDENCE_GATE
F_CONFIDENCE_GATE
G_STATE_DIRECTION
H_DEDUPLICATION
I_SCOPE_POLICY
J_API_VISIBILITY
K_MALFORMED_REPRESENTATION
UNKNOWN

Also allow secondary contributing stages.

--------------------------------------------------
SPECIAL TRACES
--------------------------------------------------

Perform particularly detailed traces for:

1. Project Indigo → CoreWeave
2. Project Indigo → NVIDIA
3. Project Indigo SPV → Meta
4. Hut 8 → NVIDIA
5. Hut 8 → Anthropic
6. Hut 8 → Fluidstack
7. Lambda → NVIDIA
8. Lambda → Anthropic
9. Applied Digital → CoreWeave
10. Applied Digital → Oracle
11. Applied Digital → Meta
12. OpenAI investor relationships
13. OpenAI compute/service relationships
14. Cavalry historical CyrusOne acquisition
15. BO Westover → Blue Owl Capital

For relationships where the correct entity pair exists under the wrong
relationship type, explicitly classify this as TAXONOMY rather than
EXTRACTION.

For relationships where the exact relationship exists in the normalized
store but is REJECTED, determine exactly which gate produced that state.

For relationships existing in V2/normalized but absent from the global
portfolio API, classify the visibility issue separately from extraction.

--------------------------------------------------
OUTPUT
--------------------------------------------------

Return:

1. EXECUTIVE SUMMARY

2. 37-RELATIONSHIP ATTRIBUTION MATRIX

3. LOSS FUNNEL

Show counts:

37 benchmark relationships
→ raw evidence available
→ extracted candidate
→ identity resolved
→ taxonomy correctly mapped
→ evidence passed
→ confidence passed
→ state/direction passed
→ within V3 scope
→ published
→ visible in global API

4. LOSS BY STAGE

Example format:

Extraction          X
Entity resolution   X
Taxonomy            X
Evidence gate       X
Confidence gate     X
State/direction     X
Scope policy        X
API visibility      X
Malformed/other     X
Unknown             X

Do not force the totals if multiple relationships cannot be attributed
with evidence. Explicitly report UNKNOWN.

5. FALSE REJECTION ANALYSIS

List source-supported relationships that were extracted but later rejected
and identify the exact rejection rule.

6. TAXONOMY SUBSTITUTION ANALYSIS

Show expected type → actual stored type.

7. ENTITY RESOLUTION FAILURES

Show raw name → expected canonical entity → actual resolution.

8. SCOPE EXCLUSIONS

Separate intentional V3 policy exclusions from implementation failures.

9. API VISIBILITY DIFFERENCES

Identify relationships present in a store but absent from Network /
Explorer / Client Detail / Review Queue because of source selection.

10. RECOMMENDED PIPELINE CHANGES

Do not implement them.

Rank changes by which stage would recover the most benchmark
relationships without increasing false positives.

The purpose of this task is not to maximize counts.

The purpose is to establish exactly WHERE legitimate source-supported
relationships are being lost so we can redesign the extraction and
governance pipeline correctly.
