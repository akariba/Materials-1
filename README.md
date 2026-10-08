POLISH THE EXISTING WORLD MAP ONLY.

The world-map logic is now correct.

Do NOT change:
- backend
- API
- country matching
- stress logic
- Correlation page
- CCRIG recovery
- DuckDB / Parquet
- data model

This is visual refinement of the existing Stress Analytics world map only.

==================================================
OBJECTIVE
==================================================

Make the current global country-of-risk map look like a professional
institutional risk dashboard.

Keep the full-world Natural Earth projection.

Do NOT zoom to live countries.

==================================================
1. COUNTRY GEOMETRY
==================================================

Keep all world polygons visible.

Increase visual definition:

- neutral countries should remain light grey
- country boundaries should be clearly visible
- active/risk countries should have significantly stronger fill contrast
- coastlines/borders should remain subtle but readable

Avoid an almost-white world map.

Do not use bright decorative colors.

==================================================
2. ACTIVE COUNTRY EMPHASIS
==================================================

A country with live rows must be immediately identifiable.

Current example:
United States

Make the USA clearly stand out from countries with no live rows.

Preserve existing risk categories:

RED
AMBER
GREEN
UNKNOWN
NO DATA

UNKNOWN must still look visibly different from NO DATA.

==================================================
3. MAP COMPOSITION
==================================================

Use the available map panel efficiently.

Fit the COMPLETE world geometry with balanced margins.

The world should occupy most of the map canvas while preserving its
correct aspect ratio.

Do not stretch the geometry.

Avoid excessive unused whitespace above/below the map.

==================================================
4. ENTITY MARKERS
==================================================

Current entity markers around the USA overlap heavily.

Improve marker layout.

For multiple entities mapped to the same country:

- place a primary country centroid marker
- optionally show a count badge, e.g. "5"
OR
- deterministically offset markers around the centroid

Do not place five labels directly on top of one another.

On hover/click show the underlying entities.

Do not alter geography to make markers fit.

==================================================
5. LABELS
==================================================

Do not permanently label every entity on the map.

Default map should stay clean.

For active countries show only useful information such as:

United States
5 entities
Stress: Unknown

Detailed entity names can appear on hover/click or in the existing side panel.

==================================================
6. LEGEND
==================================================

Make the legend clearly readable.

Keep:

Red
Amber
Green
Unknown
No data

Use compact professional swatches with readable text.

Keep legend inside or directly beneath the map, aligned consistently.

==================================================
7. HEADER METRICS
==================================================

Review:

"258 countries"

If 258 is the number of GeoJSON polygons/features rather than sovereign
countries, DO NOT call them countries.

Either change to:

"258 geographic features"

or omit this number.

Prefer the useful business metrics:

1 country with live exposure
5 mapped entities

Likewise, only display "live arcs" if arcs are actually rendered and meaningful.

==================================================
8. INTERACTION
==================================================

Maintain:

hover country
click country
entity inspection

If possible within the existing implementation:

hover country:
- country name
- number of entities
- stress signal
- TFA / exposure if available

Do not invent missing exposure values.

==================================================
9. STYLE TARGET
==================================================

The visual target is:

institutional bank risk dashboard
not consumer map
not decorative infographic
not GIS application

Clean
restrained
high information density
clear active-risk emphasis

Preserve current application typography and general styling.

==================================================
10. ACCEPTANCE
==================================================

With the current USA-only live dataset verify:

[ ] complete world visible
[ ] world occupies map area appropriately
[ ] country borders readable
[ ] USA clearly differentiated
[ ] UNKNOWN visibly different from NO DATA
[ ] entity markers do not overlap
[ ] legend readable
[ ] no misleading "258 countries" label
[ ] no unnecessary labels cluttering the map
[ ] side analytics panel remains unchanged
[ ] responsive layout still works
[ ] compile passes

Take a browser screenshot after the change.

STOP after visual map polish.