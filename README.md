CCR RELATIONSHIP INTELLIGENCE — FRONTEND LAYOUT, GRAPH AND SELECTION SYNCHRONIZATION FIX

Act as a senior frontend engineer, graph visualization specialist, and full-stack engineer.

Objective

Fix the existing CCR Relationship Intelligence frontend so that it becomes a clean, professional, responsive, interactive application.

The current screenshots show:

* A very long entity list extending down the page.
* Too many graph nodes clustered together, with overlapping names and edges.
* Graph nodes that are visually heavy and difficult to navigate.
* Large amounts of unused white space.
* A Credit Risk Intelligence panel that is too narrow.
* The physical relationship records table positioned far below the graph.
* Inconsistent selection behavior between entity list, graph, Credit Risk Intelligence, and relationship records.
* Cases where a selected entity has many PHR review candidates but zero verified physical records.

I want the entire page to behave as ONE synchronized analytical workspace.

IMPORTANT: Modify the existing CCR project. Do not create another frontend, another backend, another data pipeline, or a parallel demo. Preserve the current FastAPI services, DuckDB/Parquet architecture, canonical identifiers, evidence validation, relationship eligibility rules, and existing working features.

1. Inspect the existing implementation first

Locate the actual frontend source, currently served frontend, API contracts, graph-rendering code, entity-selection handlers, and relationship-table logic.

Determine whether the browser is displaying the live application or an outdated frontend/dist build.

Identify the existing graph library and reuse it if technically suitable.

Trace:

* Entity list selection
* Graph node selection
* Graph expansion
* Relationship filtering
* Credit Risk Intelligence loading
* Physical relationship records loading
* Focus anchors and multiple-selection behavior
* PHR review candidate rendering

Perform this targeted inspection, then IMPLEMENT the changes. Do not stop after producing an audit.

2. Rebuild the page layout using balanced, resizable panels

Use a professional three-column analytical workstation layout.

Suggested initial desktop proportions:

LEFT — Entity Universe: 23%
CENTER — Relationship Graph: 47%
RIGHT — Credit Risk Intelligence: 30%

Use CSS Grid or the project’s existing layout system.

Requirements:

* All three main panels should share the same visible workspace height.
* Target a workspace height around 75–80vh, with sensible minimum dimensions.
* Each panel must scroll independently where appropriate.
* The page must not become excessively long simply because hundreds of entities exist.
* Make the three columns resizable with drag handles if compatible with the current implementation.
* Give Credit Risk Intelligence at least 30% of the usable width by default.
* Use responsive breakpoints for smaller screens.
* Prevent horizontal text overflow.
* Preserve the existing Citi-inspired visual identity.
* Avoid unnecessary cards, giant margins, duplicated headings, and excessive empty space.

The Credit Risk Intelligence panel must become substantially easier to read.

3. Fix the entity list

The current entity list can contain 57 or more PHR entities and should eventually support hundreds or thousands.

Implement:

* A fixed-height, independently scrollable entity list.
* A sticky search field.
* Search by entity name, CAGID, GFCID, LEI, CIK, BBG ticker, and approved aliases.
* Virtualized rendering or efficient pagination for large lists.
* Clear highlighting of selected entities.
* Compact rows displaying the legal name and important identifiers.
* TFA and relationship counts only when returned by authoritative data.
* A visible distinction between verified relationships and review-only candidates.
* One-click focus on a company.
* A clear action to remove that company from the current focus.

Do not render a several-thousand-pixel-long entity list.

4. Redesign graph nodes to be lightweight and readable

The current graph uses relatively large, glossy circular nodes clustered close together.

Replace their presentation with compact, flat, professional 2D nodes.

Suggested sizes:

* Ordinary node: 12–16px diameter.
* Selected node: 20–24px diameter.
* Important hub: up to 22px diameter.
* Avoid oversized 3D-looking spheres, thick borders, shadows, and decorative effects.

Use restrained color coding:

* Selected/focus entity: Citi blue.
* Verified connected entities: neutral blue/gray.
* Review-only candidates: muted amber.
* Indirect or hidden-risk indicators: visually distinct, with clear legends.

Node color must not imply a verified relationship where none exists.

Labels:

* Display short readable names.
* Use full legal names in hover tooltips and detail panels.
* Apply intelligent label collision avoidance.
* Reveal additional labels on hover, selection, or zoom.
* Never place dozens of overlapping labels on top of one another.

Optimize the rendering so that hundreds of nodes do not freeze the browser.

5. Space graph nodes much farther apart

The graph must have meaningful spacing.

The current nodes are compressed into a small cluster while most of the canvas is empty.

Improve the existing layout algorithm or use an appropriate layout supported by the installed visualization library.

Use:

* Greater node repulsion or collision separation.
* Longer link distances.
* Hub-aware spacing.
* Cluster separation.
* Deterministic initial positions where possible.
* Stable layout when adding or removing nodes.
* Zoom-to-fit after initial rendering.
* Smooth animations without excessive simulation.

Suggested starting targets:

* Minimum screen-space separation of approximately 35–50px between visible node centers at the default fitted view, where achievable.
* Hub-to-connected-node distance around 100–160px at normal zoom, adjusted to available canvas size.
* Larger spacing between disconnected communities.

These are starting visual targets, not rigid physics constraints.

Do not keep the entire network permanently compressed into the center.

6. Make the graph easy to rearrange

Implement intuitive controls:

* Drag individual nodes.
* Drag the background to pan.
* Mouse wheel to zoom.
* Double-click a node to focus and expand its neighborhood.
* Single-click a node to select it.
* Reset layout.
* Fit to screen.
* Center selected node.
* Clear focus.
* Expand one additional relationship level.
* Collapse an expanded neighborhood.

When a node is manually repositioned, preserve its position until Reset Layout or a deliberate re-layout.

Do not trigger complete graph reconstruction on every minor interaction.

If the graph is large, render the selected entity’s neighborhood first and expand progressively instead of displaying every available entity at once.

7. Implement one authoritative synchronized selection state

This is the most important functional requirement.

There must be ONE shared frontend selection model used by all components.

Suggested state contract:

selectedEntityId
selectedEntityIds
selectedRelationshipId
expandedNodeIds
graphDepth
relationshipFilter
evidenceFilter
activeDossierTab

Use existing canonical identifiers rather than display names as state keys.

Every selection action must update the same shared state.

A. Click an entity in the left table

When I click Oracle, NVIDIA, Digital Realty, or another entity:

1. Highlight it in the entity list.
2. Focus it in the graph.
3. Expand its eligible verified direct relationships.
4. Show separately labeled review-only candidates where available and enabled.
5. Update Credit Risk Intelligence for the selected canonical entity.
6. Filter the physical relationship table to records where that entity is a subject or related entity.
7. Recalculate visible graph metrics from eligible verified edges.
8. Update the selected-entity name and relationship counts consistently.

All updates must happen without refreshing the entire page.

B. Click a node in the graph

When I click a graph node:

1. Make that node the active entity.
2. Highlight its corresponding row in the left entity table.
3. Scroll the selected row into view without moving the entire page.
4. Update Credit Risk Intelligence.
5. Update the physical relationship records table.
6. Highlight its immediate eligible connections.
7. Show the selected entity’s relationship count, with separate verified and candidate counts.

A double-click should expand the node’s eligible neighborhood rather than create duplicate nodes.

C. Click a relationship edge

When I click a line connecting two entities:

1. Highlight the relationship.
2. Identify both endpoint entities.
3. Show all physical relationship records supporting that pair.
4. Show relationship type, direction, evidence, provenance, confidence, and verification state.
5. Distinguish multiple physical records from one consolidated graph connection.

Do not collapse or delete the original physical records.

D. Click a row in the physical relationship table

When I click a relationship row:

1. Highlight the corresponding graph nodes.
2. Highlight the corresponding edge if it is graph-eligible.
3. Center or fit the involved nodes within the graph.
4. Display the selected relationship’s evidence.
5. Show the exact source document and excerpt where available.
6. Allow the user to select either endpoint as the primary entity.

If the row is review-required and not eligible for the verified graph, show it as review-only without creating a verified edge.

E. Multiple selected entities

Support multiple focus anchors without confusing them with the primary selected entity.

For example, when I select NVIDIA, Oracle, and Digital Realty:

* Highlight all three focus anchors.
* Display their eligible combined neighborhood.
* Avoid duplicate entities.
* Show shared counterparties where they exist.
* Clearly distinguish shared verified relationships from candidate links.
* Keep one primary entity for the Credit Risk Intelligence dossier.
* Allow switching the primary entity without removing the other anchors.

8. Synchronize the two tables and the Credit Risk Intelligence panel

Treat these components as one workspace:

1. Entity Universe table.
2. Physical Relationship Records table.
3. Credit Risk Intelligence dossier.
4. Relationship graph.

Every selection must propagate consistently to the other relevant components.

Use a clear distinction between:

* Primary selected entity.
* Additional focus anchors.
* Selected relationship.
* Current table filtering.
* Visible graph neighborhood.

Maintain selection consistency when the user changes tabs or filters.

Avoid circular selection events and unnecessary repeated API calls.

If an entity has zero eligible physical relationship records, explicitly display:

“No physical relationship records are available for this entity under the current scope and filters.”

If it has review-only PHR candidates, show their count separately and provide a review-candidate view. Do not misrepresent candidate records as verified physical relationships.

9. Fix the vertical length and scrolling behavior

The current layout has severe height imbalance.

Implement:

TOP:
Compact statistics cards, with minimal wasted space.

MIDDLE:
The three synchronized columns:
Entity Universe | Graph | Credit Risk Intelligence

BOTTOM:
Physical Relationship Records table.

Requirements:

* The bottom table should begin immediately below the middle workspace.
* The table should have a sensible bounded height, approximately 300–400px by default.
* Its rows should scroll independently.
* Its header and filters should remain visible.
* It should support an optional Expand Table action for full-screen or enlarged inspection.
* Do not create a huge blank table when no records exist.
* Do not let long entity lists determine the entire page height.
* Keep all table widths within the viewport, with deliberate horizontal scrolling where needed.
* Avoid nested scrolling that traps the user or prevents normal mouse interactions.

The Credit Risk Intelligence panel must remain wide enough to display financial metrics, ratings, identities, relationships, and distance metrics comfortably.

10. Improve physical relationship navigation

Keep the current physical-record-preserving data model.

Do not collapse records merely because they share entity endpoints.

Add effective navigation:

* Search by either counterparty.
* Relationship-type filtering.
* Direct / Indirect / Hidden classifications where supported.
* Verified / Review Required filters.
* Source filtering.
* Click-to-expand evidence.
* Click-to-focus graph behavior.
* Clear record counts.
* Consistent empty states.

Use compact, readable columns with reasonable column widths.

Preserve original source provenance and exact verification states.

11. Prevent false graph connections

Graph topology must continue respecting the project’s evidence contract.

Solid edges must represent verified eligible relationships.

Review-required or PHR candidate links must not silently become verified.

Use dashed lines only for clearly identified review candidates when that layer is enabled.

Do not infer direct links from:

* Co-mentions.
* Shared CAM membership.
* Similar company names.
* Unverified aliases.
* Graph proximity.
* A model-generated relationship with unresolved identity.
* A common industry or geography.

Only compute hop distance, Jaccard, or weighted paths from the permitted graph evidence set.

Preserve the distinction between actual relationship facts and graph-derived analytical indicators.

12. Improve performance and frontend rendering

The application should remain responsive with the current 57-entity PHR cohort and larger future datasets.

Implement:

* Efficient incremental graph updates.
* Memoized or appropriately cached derived views.
* Reduced unnecessary API requests.
* Bounded graph expansion.
* A suitable rendering mode for medium and large graphs.
* Label collision control.
* Cleanup of inactive graph simulations/listeners.
* Loading indicators only during genuine loading.
* Stable state when moving between frontend tabs.

No expensive backend recomputation should be triggered by purely visual graph dragging, zooming, or panel resizing.

13. Validate with real project data

Test at least these workflows:

TEST A — Oracle:
Select Oracle from the entity table. Verify graph focus, dossier identity, relationship records, and consistent counts.

TEST B — NVIDIA:
Select NVIDIA. Verify eligible verified links, review-only candidate separation, and appropriate dossier data.

TEST C — Digital Realty:
Select Digital Realty. Verify its larger relationship neighborhood displays with adequate spacing and minimal overlapping labels.

TEST D — Wells Fargo Securities:
Select an entity that currently returns no physical relationship records. Verify correct empty states without losing selection or incorrectly clearing the graph.

TEST E — Multiple selection:
Select three companies and test combined graph neighborhoods and primary dossier switching.

TEST F — Table-to-graph synchronization:
Click a relationship row and confirm correct graph focus and evidence details.

TEST G — Graph-to-table synchronization:
Click a graph node and confirm the entity list, physical records, and dossier update consistently.

TEST H — Responsive layout:
Test at 1920×1080, 1440×900, and smaller widths.

TEST I — Rendering:
Confirm that the exact frontend source modified is rebuilt and served by the live application at localhost:8000. Do not validate only an unrelated file:// HTML build.

Run relevant existing regression tests and add focused tests for shared selection state, graph eligibility, expansion, filtering, and responsive behavior.

14. Engineering restrictions

* Use the existing frontend and production API.
* Preserve existing verified data and canonical identifiers.
* Do not modify the CAM MapReduce pipeline.
* Do not rerun expensive LLM extraction.
* Do not regenerate the 57-entity cohort.
* Do not create mock relationship data.
* Do not overwrite database artifacts.
* Do not weaken evidence gates.
* Do not redesign unrelated Stress Analytics or Portfolio Analytics features.
* Make targeted, maintainable changes rather than inserting another large block of duplicate frontend code.
* Avoid breaking existing workflows.
* Inspect before editing, but proceed to implementation in this same task.

15. Required outcome

I want the final result to behave like a professional credit-risk investigation workspace.

When I select a company, the graph, entity list, dossier, and physical records must all react together.

The graph must be spacious, compact, readable, draggable, zoomable, and expandable.

The entity list must remain within a controlled scrolling area.

The Credit Risk Intelligence panel must be larger.

The physical relationship table must be conveniently positioned below the graph, rather than far down the page.

After implementation, provide:

* Root causes fixed.
* Exact files modified.
* Summary of layout changes.
* Selection synchronization design.
* Graph performance improvements.
* Validation results with passed/failed test counts.
* Remaining limitations.

Do not claim browser behavior is verified unless it has actually been tested.

Implement now, using the current CCR project and existing production data.