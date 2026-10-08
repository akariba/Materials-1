CCR Relationship Intelligence — Professional Layout Rebalancing

Act as a senior frontend engineer and UI/UX architect.

Project: C:\Users\ak5743\Downloads\Param\CCR Correlation

Application: http://127.0.0.1:8000

Objective

Improve the existing Correlation page layout without changing its functionality, backend, data contracts, or visual identity.

The priority is to make Credit Risk Intelligence significantly wider, balance the three main columns, eliminate unnecessary whitespace, and make the relationship database easier to read.

This is a frontend layout implementation task, not a redesign.

1. Main three-column layout

Current layout has three areas:

1. Live Entity Universe
2. Relationship Graph
3. Credit Risk Intelligence

Implement these desktop proportions:

* Entity Universe: 25%
* Relationship Graph: 40%
* Credit Risk Intelligence: 35%

Use CSS Grid or the existing layout framework.

Apply sensible minimum widths and responsive breakpoints. On smaller screens, stack panels rather than allowing overlapping content or excessive horizontal scrolling.

Do not modify the existing application color palette or components unnecessarily.

2. Credit Risk Intelligence — main priority

Increase the width of Credit Risk Intelligence to approximately 35% of the main content area.

Make the following elements comfortably readable:

* Company name and canonical identifiers
* Stress and ORR indicators
* External agency ratings
* CAM internal ratings
* Financial metrics
* Credit exposure
* Entity identity
* Relationship evidence
* Distance analytics
* Grounded investigation

Prevent identifier text, financial labels and metric values from wrapping into narrow columns unnecessarily.

Use a responsive two-column grid for financial metrics when space permits.

On narrow widths, automatically switch financial metric cards to one column.

Preserve all five existing dossier tabs:

RATING | FINANCIALS | IDENTITY | RELS | DISTANCE

Keep the panel independently scrollable when necessary.

Make its content height visually aligned with the graph rather than arbitrarily extending beyond it.

3. Entity Universe — reduce excessive length

The entity list should not determine the total height of the page.

Set a reasonable fixed or viewport-relative panel height, using min()/clamp() or equivalent responsive CSS.

Use internal vertical scrolling for long entity lists.

Keep the search field visible while scrolling.

Preserve:

* All entity names
* Canonical identifiers
* Search functionality
* Selection state
* Recent entities
* Entity filtering

Do not delete or restrict the existing PHR entity universe.

4. Relationship graph — use space efficiently

Reduce the excessive blank space surrounding a small number of nodes.

The graph should:

* Fit the selected network into the available canvas
* Automatically center the selected entity
* Use an appropriate initial zoom level
* Preserve pan and manual zoom
* Preserve node selection and relationship expansion
* Preserve verified and review-required edge styling
* Recalculate dimensions when the panel size changes

Use the existing graph library and layout engine.

Do not change graph data or relationship eligibility.

For a dense network such as Digital Realty Trust, maintain readable node spacing and avoid label overlap as much as practical.

For a small network, do not leave three tiny nodes lost in a huge blank canvas.

5. Harmonize vertical dimensions

The three main panels should align at their top and bottom edges on desktop.

Use a common responsive height, for example:

clamp(620px, 76vh, 900px)

Treat this as a starting point, not a hardcoded requirement if it conflicts with the existing layout.

Entity list, graph and dossier should manage their own scrolling or canvas dimensions.

Avoid nested scrollbars wherever possible.

The page itself must remain scrollable so that the Relationship Records table can be reached.

6. Physical Relationship Records — improve readability

Keep the relationship database below the main three-column workspace.

Make the table full-width.

Improve the balance of its columns:

* Connectivity
* Subject
* Related Entity
* Relationship Type
* Source / Date
* Citi Exposure
* TFA
* Evidence Status
* Verification
* Evidence Detail
* Confidence

Use suitable column widths.

Allow horizontal scrolling within the table only when required.

Make row evidence expansion easy to access.

Keep table headers visible during internal table scrolling where supported.

Do not compress text into unreadable columns or change any stored relationship records.

7. General styling

Preserve the current Citi-inspired styling.

Improve only:

* Column proportions
* Container heights
* Internal scrolling
* Text wrapping
* Alignment
* Card spacing
* Graph canvas scaling
* Responsive behavior

Do not rewrite the frontend, replace components or introduce a new design system.

Do not modify Portfolio Analytics, Stress Analytics or Risk Heatmap unless a shared CSS change would otherwise break them.

8. Technical implementation

Inspect the actual frontend source files and CSS.

Make changes to the authoritative source, not only the compiled HTML in frontend/dist.

Rebuild the frontend correctly.

Ensure the production application serves the updated build.

Avoid stale compiled assets and cache confusion.

9. Validation

Test at desktop widths of approximately:

* 1920px
* 1440px
* 1280px

Also check a narrower viewport.

Validate these entity selections:

1. Digital Realty Trust — dense network
2. Oracle Corporation — sparse or review-only network
3. NVIDIA Corporation — small verified network

Check that:

* Credit Risk Intelligence is visibly wider
* Financial metric cards are readable
* Entity list scrolls independently
* Search remains usable
* Graph fits its available area
* Dense labels do not overlap excessively
* Evidence rows remain accessible
* Relationship table remains usable
* Tab switching preserves state
* No API or data behavior changes
* No unintended regressions occur on other pages

10. Final delivery

Provide:

1. Files modified.
2. Final desktop column proportions.
3. New panel-height strategy.
4. Graph auto-fit changes.
5. Relationship table changes.
6. Frontend build result.
7. Tests and manual UI validation results.
8. Application URL.

Only commit after validation.

Do not perform another backend audit, CAM extraction, database rebuild or entity-enrichment operation. Focus exclusively on layout quality and usability.