CCR V1 — STAGE 6.1 SEMANTIC UI CORRECTION
Use the completed Stage 6 UI and Stage 5.1 contracts as the baseline.
This is a narrowly scoped semantic-correction stage. Do not redesign the architecture, broaden relationship discovery, perform provider research, implement AI Create Correlation, or add new correlation definitions.
1. Fix network truth semantics
Audit the current network source for every rendered node and edge.
The network must never render a context-only, candidate, or unresolved-endpoint claim using accepted factual-edge semantics.
Enforce these states:
- ACCEPTED relationship + valid endpoint identity: solid factual edge.
- ACCEPTED relationship to Legal Entity where Client match-back is unresolved/ambiguous: solid factual edge, but Legal Entity must use a visibly external/unresolved node treatment and must not masquerade as a Client Record.
- CANDIDATE relationship: distinct dashed/muted treatment and hidden by default unless Show candidates is explicitly enabled.
- CONTEXT-only claim: no factual graph edge. It may appear only in a separate contextual/mentions surface if one already exists; do not invent a relationship.
- Unresolved unnamed endpoint: no graph node.
- Derived correlation: overlay/path visualization only; never create or render a synthetic direct relationship.
Specifically regression-test the current 3M pilot:
- 3M → 3M India accepted ownership remains factual.
- accepted Solventum relationships remain factual even if Client match-back is ambiguous; endpoint must be represented as the Legal Entity/external resolution state.
- Cabot must not appear as a factual relationship edge if the current V1 repository contains only context-only indemnification evidence and no accepted V1 relationship.
Do not use historical Stage 2 graph rows as factual Stage 6 edges unless they have valid accepted V1 relationship/version support.
2. Fix exact Client Universe identifier search
Audit the search path for exact GFCID input.
For a full exact GFCID such as:
0000426083
the query must use the authoritative exact-identifier lookup and return the unique corresponding Client Record.
It must not:
- expand through CAGID;
- expand to aliases/group members;
- mix fuzzy/text results under the EXACT_IDENTIFIER label;
- return multiple unrelated records.
Keep fuzzy/name/alias search as a separate search mode/path.
CAGID may support explicitly labelled grouping exploration later, but must not masquerade as exact client identity.
Add regression tests proving:
- exact known GFCID → exactly one Client Record;
- exact GFCID search does not expand to same-CAGID members;
- fuzzy/name search remains available independently.
3. Populate and expose real enrichment coverage for the controlled 3M pilot
Do not invent coverage.
Using already persisted research/evidence/history only, create or reconcile valid CCR V1 coverage records for the controlled 3M/3M India/Solventum/Cabot pilot where the historical/revalidated work genuinely supports them.
Coverage must remain governed by the existing outcomes:
- NOT_ELIGIBLE
- NOT_RESEARCHED
- RESEARCHED_FOUND
- RESEARCHED_NONE_FOUND
- PARTIAL
- UNAVAILABLE
with freshness independently CURRENT/STALE.
Do not convert missing coverage into RESEARCHED_NONE_FOUND.
Do not claim comprehensive real-world coverage.
Replace the analyst-facing aggregate Coverage: 0 records treatment with a meaningful coverage summary.
Where there are no coverage rows, say this explicitly in analyst language such as:
Research coverage not yet recorded
rather than implying that no relationships exist.
Expose family-level coverage when available.
Correlation zero-result messaging must continue to say that no qualifying correlation was found in the currently available eligible graph, not that no real-world correlation exists.
4. Relationship register completeness
Ensure the selected-client factual relationship register does not silently hide accepted relationships merely because Client match-back is unresolved.
The register should distinguish:
- accepted relationship to uniquely matched Client Record;
- accepted relationship to Legal Entity with unresolved/ambiguous Client match-back;
- candidates/context separately.
For 3M, accepted Solventum facts must remain visible even if Solventum's Client Record match-back is ambiguous.
5. Evidence replay caveat
Preserve the existing evidence metadata.
If evidence is LEGACY_REFERENCE, PASSAGE_REPLAY, PARTIAL_REPLAY, or otherwise not full retained-snapshot replayable, expose a clear evidence-status/caveat in the inspector.
Do not downgrade or alter accepted relationship truth solely because of the UI treatment, and do not claim FULL_REPLAY when no stored document supports it.
6. Plain-language presentation
Add a small presentation translation layer for analyst-facing terminology.
Do not alter backend enum values.
Examples:
- EXACT_IDENTIFIER → Exact identifier match
- VERIFIED / EXACT → Verified legal-entity match
- BLOCKED_BY_IDENTITY → Client identity unresolved
- SUPPRESSED_HUB → Hidden from default view: high-connectivity hub
Preserve raw values in audit/detail views where useful.
Hard non-actions
Do not:
- perform new SEC/GLEIF/Web/Stylus research;
- broaden enrichment beyond the controlled persisted pilot;
- create synthetic edges;
- fuzzy merge identities;
- modify Customer_latest.parquet;
- modify authoritative Client Universe rows;
- implement correlation-definition authoring;
- implement AI Create Correlation;
- add recursive traversal;
- migrate to PostgreSQL;
- redesign overall visual styling.
Validation
Run full backend and frontend suites.
Add focused regression tests for:
1. Cabot is not rendered as accepted factual edge.
2. 3M India accepted ownership remains visible.
3. Solventum accepted relationships remain visible as Legal Entity relationships despite ambiguous Client match-back.
4. exact 0000426083 GFCID lookup returns exactly one authoritative Client Record.
5. CAGID does not expand an exact GFCID lookup.
6. coverage states are shown independently from relationship presence.
7. zero correlation results remain non-universal negatives.
8. candidate/context claims never become accepted graph edges.
9. derived correlations never become persisted direct edges.
10. evidence replay limitations remain visible.
Produce:
backend/data/CCR_V1_STAGE_6_1_SEMANTIC_CORRECTION_REPORT.md
Include before/after screenshots or exact UI acceptance observations for the 3M pilot.
Stop after Stage 6.1. Do not start enrichment expansion or correlation-authoring.
