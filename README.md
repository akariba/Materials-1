PROMPT 4C — LENDING NETWORK INTELLIGENCE + BOUNDED INTERACTIVE GRAPH

Continue from the completed Prompt 4A and Prompt 4B implementations and their reports:

backend/data/LENDING_PROMPT4A_EXECUTIVE_HOME_REPORT.md
backend/data/LENDING_PROMPT4B_PORTFOLIO_CLIENT_REPORT.md

The Common Operating Contract remains fully in force.

Do NOT redo Prompt 4A.
Do NOT redo Prompt 4B.
Do NOT start Prompt 4D or later work.

Prompt 4C owns only:

1. /lending/network
2. bounded relationship-network visualization
3. deterministic graph/map interactions
4. entity/network drill-down behavior
5. network explainability
6. network-specific performance and loading behavior
7. visual productization of relationship intelligence

Do NOT redesign Relationship Explorer in this prompt.
Do NOT redesign Intelligence / AI authoring.
Do NOT redesign External Research.
Do NOT redesign Review.
Do NOT change CAM/V3 authority.
Do NOT create a new universal relationship database.
Do NOT merge CAM, normalized, AI, and external lanes into one truth layer.
Do NOT introduce inferred credit-risk scores.

==================================================
1. PRODUCT INTENT
==================================================

Transform the current Network page from a technical bounded graph view into a senior-user relationship intelligence workspace.

The user should be able to enter Network and understand, without configuration knowledge:

- where portfolio exposure is concentrated,
- which clients have trusted CAM relationships,
- what entities those clients connect to,
- what relationship families are present,
- which relationships require review,
- where external or AI supplemental information exists,
- what evidence supports a relationship,
- which entities deserve investigation next,
- and how to move into the relevant governed workflow.

The Network page should feel like an institutional relationship-intelligence product.

It must remain accurate, explainable, bounded, and read-only.

==================================================
2. AUTHORITY MODEL
==================================================

Preserve exactly:

- CAM/V3 is authoritative for current Lending CAM relationship truth.
- V2 is fallback/history only under the existing client-specific rules.
- Normalized workbench is a separate governed projection.
- External research is supplemental.
- Published AI relationships are a separate governed projection.
- Review-required does not mean invalid and does not mean high credit risk.
- External proposals are not CAM truth.
- AI relationships are not CAM rows.
- No automatic mutation occurs from Network.

Every graph edge and node must retain its source/authority identity.

Do not visually imply that all visible edges have equivalent authority.

==================================================
3. PERFORMANCE BOUNDARY
==================================================

Network must not load or adapt the entire 32,957-row normalized history merely to render the initial page.

The existing unified semantic-group implementation is known to adapt the approximately 2.8 GB normalized artifact before applying a result limit.

Do NOT use that implementation for ordinary initial Network rendering.

First inspect the existing Network APIs and current frontend request path.

Prefer existing bounded sources such as:

- portfolio CAM/V3 relationship projection,
- bounded client relationship endpoints,
- existing portfolio/client exposure reads,
- existing status/review reads.

If a new backend read is genuinely required for Network, it must be:

- read-only,
- Lending-only,
- bounded before expensive processing,
- explicitly source-scoped,
- paginated or limited,
- deterministic,
- CAM/V3-safe,
- covered by regression tests.

Do not create a second relationship store.

Do not optimize or rewrite unrelated normalized-history infrastructure.

==================================================
4. NETWORK PAGE STRUCTURE
==================================================

Refine /lending/network into the following high-level composition:

A. Network command header
B. Executive network indicators
C. Main interactive network canvas
D. Context / investigation panel
E. Deterministic filters and layers
F. Selected-entity / selected-relationship inspector
G. Bounded underlying-record table

The experience should be visually lighter and more sophisticated than the existing screen.

Avoid excessive form controls above the graph.

Senior users should see intelligence first and configuration second.

==================================================
5. NETWORK COMMAND HEADER
==================================================

Provide a compact command area containing:

- Network title and short purpose statement.
- Current scope.
- Active authority/source lanes.
- Current filter summary.
- Global client/entity search.
- Reset view.
- Optional layout/view selector.

Search must remain deterministic.

Search must not invoke AI or external providers.

Where appropriate support search by:

- client name,
- CAGID,
- entity name,
- governed entity identifier.

==================================================
6. EXECUTIVE NETWORK INDICATORS
==================================================

Add a compact indicator strip above or adjacent to the network canvas.

Use only deterministic metrics actually supported by loaded data.

Possible metrics include:

- visible portfolio clients,
- visible connected entities,
- canonical CAM/V3 relationships,
- review-required relationships,
- relationship families represented,
- visible countries,
- visible high-exposure clients,
- supplemental external/AI counts when those layers are explicitly enabled.

Never present:

- synthetic credit score,
- inferred materiality score,
- inferred systemic-risk score,
- unsupported relationship strength score.

Each metric should be clickable where useful to filter or focus the graph.

==================================================
7. MAIN NETWORK CANVAS
==================================================

Create a visually strong interactive relationship canvas.

The canvas should support:

- pan,
- zoom,
- fit-to-view,
- reset,
- entity selection,
- edge selection,
- neighborhood expansion,
- collapse,
- hover details,
- keyboard-accessible selection where practical.

Use the current React application.

Reuse the existing graph library if technically sound.

Do not introduce a major new visualization dependency unless required.

If existing SVG/React graph rendering can support the requirement cleanly, prefer it.

The graph should feel fluid but should not use decorative animation that suggests unsupported analysis.

==================================================
8. NODE VISUAL LANGUAGE
==================================================

Nodes must encode deterministic meaning.

At minimum distinguish:

- portfolio client,
- related governed entity,
- V2 fallback/history context if visible,
- external supplemental entity/context if enabled,
- published governed AI context if enabled.

Suggested visual dimensions:

NODE SIZE
- May reflect reported exposure only for portfolio clients where reported OSUC is available.
- Must not imply risk.
- Non-client entities should use a neutral standard size unless another deterministic metric exists.

NODE BORDER / BADGE
- CAM/V3 authoritative
- review required
- supplemental external
- governed AI
- fallback/history

NODE LABEL
- entity/client name
- optional compact secondary identifier

Do not encode too many dimensions simultaneously.

Use a restrained, institutional palette.

==================================================
9. EDGE VISUAL LANGUAGE
==================================================

Edges must preserve actual relationship semantics.

Visually encode, where available:

- relationship type/family,
- direction,
- connectivity,
- authority/source lane,
- review status.

Use arrowheads for governed directional relationships when direction is supported.

Use a non-directional treatment where direction is bidirectional.

If direction is unresolved, render it explicitly as unresolved.

Do not infer direction.

Use line styling carefully:

- authoritative CAM/V3: primary trusted treatment
- review-required: visible attention treatment
- external supplemental: clearly supplemental
- governed AI: clearly separate
- V2 fallback/history: historical/fallback treatment

The legend must explain these meanings.

==================================================
10. PURPOSEFUL MOTION
==================================================

The product may use subtle motion to make the network understandable.

Permitted examples:

- brief highlight pulse on a newly selected node,
- smooth focus transition,
- animated path tracing when the user explicitly asks to inspect a relationship path,
- subtle edge illumination during selection.

Do NOT continuously animate the graph.

Do NOT create moving particles that imply transaction flow, money flow, exposure flow, contagion, or causal propagation unless such data actually exists.

Visual elegance must never invent meaning.

==================================================
11. MAP / GEOGRAPHY MODE
==================================================

The existing product already uses portfolio geography.

If current data and implementation allow it without introducing new authority assumptions, Network may provide a geographic network mode.

Examples:

- portfolio clients positioned by known country,
- relationship arcs between client-country and related-entity country when both locations are genuinely available,
- country-level aggregation at broad zoom,
- entity-level expansion after selection.

However:

- do not geocode unknown entities by inference,
- do not fabricate headquarters,
- do not infer legal domicile,
- do not convert source country into headquarters unless that is what the field means.

If geographic coordinates are not reliably available, retain the existing map for portfolio geography and make the relationship canvas the primary Network visualization.

Document the decision.

==================================================
12. NETWORK LAYERS
==================================================

Provide an understandable layer control.

Recommended user-facing language:

- Portfolio exposure
- CAM relationships
- Review required
- External research
- Governed AI
- Fallback/history

Do not expose internal storage architecture as the primary user language.

However, source authority must remain inspectable.

Initial/default view should prioritize:

1. portfolio clients,
2. CAM/V3 trusted relationships,
3. review-required CAM/V3 context.

External and AI overlays should be opt-in or clearly supplemental unless current product contract explicitly enables them.

==================================================
13. SENIOR-USER PRESETS
==================================================

Introduce deterministic Network presets.

Presets are view configurations, not new data or AI analysis.

Examples:

- Portfolio overview
- Largest exposures
- CAM relationship network
- Review required
- Relationship concentration
- Geographic view

A preset may adjust:

- filters,
- zoom,
- relationship families,
- visible node classes,
- layout mode.

A preset must not:

- mutate data,
- call an AI provider,
- invoke external research,
- generate proposals,
- create risk conclusions.

Presets should make the application useful immediately for senior users who do not want to configure graph controls.

==================================================
14. SELECTED NODE INSPECTOR
==================================================

Selecting a node should open a focused contextual panel rather than requiring immediate navigation away.

For portfolio clients show available deterministic context such as:

- client name,
- CAGID,
- reported OSUC,
- portfolio share/rank,
- CAM count,
- connected-entity count,
- review-required count,
- sector,
- country,
- relevant relationship counts.

For non-client entities show only fields genuinely available.

Provide clear actions such as:

- Open Client Detail
- Focus Network
- Open Relationships
- Open Review if relevant
- Research Relationship
- Open Governed Intelligence

These are navigation actions only.

No external research or AI should execute merely by opening or selecting a node.

==================================================
15. SELECTED RELATIONSHIP INSPECTOR
==================================================

Selecting an edge should expose a compact evidence-backed relationship explanation.

Where available show:

- subject,
- related entity,
- relationship type,
- family,
- direction,
- state,
- connectivity,
- authority/source lane,
- quality/review status,
- evidence count,
- source count,
- source document,
- source location/page,
- exact excerpt when available.

Include:

“Why am I seeing this?”

The answer must be deterministic and based on actual projection/source fields.

Do not generate a speculative credit interpretation.

If exact evidence is unavailable in the Network projection, say so and provide a handoff to Relationship Explorer / Intelligence rather than fabricating it.

==================================================
16. RELATIONSHIP FAMILIES
==================================================

The Network should help users understand real-world relationship categories holistically.

Use the actual governed taxonomy.

Where appropriate group relationship types into understandable families for visualization, while retaining the exact governed relationship type underneath.

Examples may include only if supported by current taxonomy/data:

- Ownership & Capital
- Commercial
- Credit Support
- Financing
- Market / Competitive
- Strategic / Operational
- M&A / Corporate Actions

Do not silently remap taxonomy.

If a family is UI-derived, explicitly preserve the exact source relationship type in the inspector.

==================================================
17. NETWORK ATTENTION SIGNALS
==================================================

Add deterministic attention signals, not risk scoring.

Examples:

- large reported exposure with no CAM relationships,
- review-required relationship,
- unresolved direction,
- unresolved state,
- multiple relationship types for the same endpoint pair,
- concentration of relationships around a portfolio client,
- source/evidence limitation.

Each signal must provide:

- what condition was detected,
- which deterministic fields caused it,
- what the user can inspect next.

Do not label these as risk alerts unless the underlying source explicitly provides a risk classification.

==================================================
18. BOUNDED EXPANSION
==================================================

Graph exploration must remain bounded.

Initial graph:
- use a reasonable bounded number of nodes/edges.

When the user expands a node:
- fetch only that entity/client's bounded first-degree context where possible.

Do not automatically recursively traverse the complete graph.

Provide explicit controls for further expansion.

If a result is truncated, visibly state:

“Showing X of Y available relationships”

where Y is known.

Do not imply completeness if the API response is bounded.

==================================================
19. UNDERLYING RECORD TABLE
==================================================

Retain a compact underlying-record table below the canvas.

It should be synchronized with current graph scope and selection.

Columns may include where available:

- source lane
- subject
- related entity
- relationship type
- family
- state
- direction
- connectivity
- evidence count
- review state

Rows should be clickable and focus the graph.

Do not render thousands of rows at once.

Use pagination or bounded rendering.

==================================================
20. EMPTY / UNKNOWN / PARTIAL STATES
==================================================

Provide explicit states for:

- no CAM relationships,
- no related entities,
- no graph matches for current filters,
- relationship endpoint unavailable,
- source lane unavailable,
- unresolved entity,
- unresolved direction,
- unresolved state,
- truncated network,
- supplemental-only context,
- API failure.

Distinguish:

0
Unknown
Unavailable
Not applicable
Filtered out
Not loaded
Truncated

These must not collapse to the same visual state.

==================================================
21. VISUAL DESIGN
==================================================

Continue the light executive design system from Prompts 4A and 4B.

Desired qualities:

- institutional,
- modern,
- premium,
- spacious,
- highly legible,
- visually engaging,
- restrained,
- interactive.

Use stronger visual emphasis only when the underlying data supports it.

The network should be the visual center of the page.

Avoid the current appearance of a large form beside a small graph.

Move advanced controls into:

- collapsible filter panel,
- drawer,
- compact toolbar,
- popover,

as appropriate.

Senior users should see the network intelligence before seeing configuration complexity.

==================================================
22. CROSS-ROUTE HANDOFFS
==================================================

Preserve navigation to existing workflows.

Network should hand off cleanly to:

- /lending/client/{cagid}
- /lending/relationships
- /lending/review
- /lending/external-research
- /lending/workbench

Do not redesign those destination workflows during Prompt 4C.

Carry useful context through URL/search state where safe and already supported.

Examples:

- selected client,
- selected entity,
- relationship type,
- review-required filter.

Do not create hidden mutable cross-page state.

==================================================
23. NO AUTOMATIC AI / PROVIDER EXECUTION
==================================================

Ordinary Network loading and graph interaction must not automatically invoke:

- AI generation,
- AI definition generation,
- external research,
- Stylus,
- SEC/web providers,
- external proposal creation,
- normalized full-history scans.

“Research relationship” and “Governed Intelligence” are explicit handoffs.

Provider execution occurs only after the user deliberately enters the appropriate workflow and invokes it.

==================================================
24. TESTING
==================================================

Add focused tests for any new bounded network backend/read contract.

Regression coverage should verify:

- CAM/V3 authority preserved,
- source lanes preserved,
- bounded initial graph,
- deterministic grouping,
- no duplicate endpoint/relationship corruption,
- direction preserved,
- unresolved direction preserved,
- review-required state preserved,
- supplemental lanes remain supplemental,
- no full normalized-history loading for ordinary Network.

Frontend validation should include:

- build,
- lint,
- changed-file diagnostics,
- graph render with CAM relationships,
- graph render with review-required relationships,
- graph render with zero relationships,
- node selection,
- edge selection,
- filter application,
- preset application,
- reset view,
- bounded expansion,
- table synchronization,
- responsive layout.

==================================================
25. REQUEST-TRACE VALIDATION
==================================================

Run the application locally and validate Network request behavior.

Confirm initial /lending/network loading does NOT invoke:

- AI generation,
- external research execution,
- provider execution,
- external proposal creation,
- the full normalized-history adaptation path.

Record actual request traces in the report.

==================================================
26. HUMAN VISUAL REVIEW
==================================================

Open /lending/network in the browser after implementation.

Inspect at least:

- default portfolio network,
- a high-exposure client,
- a client with CAM relationships,
- a client with review-required relationships,
- a client/entity with no relationships,
- filtered view,
- selected node,
- selected relationship,
- narrow browser width.

If automated DOM inspection is unavailable, explicitly document that human visual confirmation is required and leave the page open for inspection.

==================================================
27. REPORT
==================================================

Create:

backend/data/LENDING_PROMPT4C_NETWORK_REPORT.md

Document:

- files changed,
- graph architecture,
- APIs used,
- initial graph boundary,
- expansion boundary,
- source/authority handling,
- node semantics,
- edge semantics,
- presets,
- explainability behavior,
- request traces,
- performance results,
- visual validation performed,
- build/lint/test results,
- any remaining limitations,
- items intentionally deferred to Prompt 4D+.

The report must explicitly state whether the implementation ever adapts the complete normalized artifact during ordinary Network loading.

If yes, Prompt 4C is NOT complete.

End the report with exactly:

READY FOR PROMPT 4D

STOP after Prompt 4C.

Do not begin Relationship Explorer redesign.
Do not begin governed Intelligence redesign.
Do not begin External Research redesign.
Do not begin Review redesign.
