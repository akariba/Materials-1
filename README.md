Objective

Do not reconstruct the whole page.

I only want you to improve the map experience on the Overview / first page, so it becomes a stronger visual entry point for users and better reflects the intent of the tool.

The goal is to make the top page feel more interactive and relationship-driven, while keeping the current application structure, layout language, and existing components intact.

What to change

Enhance the existing Portfolio geography / map section only.

Core requirement

Create a richer, more dynamic world map visualization that fits the current tool content and supports the lending / relationship intelligence workflow.

Design intent

The map should help users quickly understand:

where client exposure is concentrated
where major client clusters exist
where AI-detected or research-supported relationships exist
where cross-border relationships or concentrations may matter
which regions / countries deserve attention
Important constraint
Do NOT rebuild the whole dashboard.

Do NOT redesign all cards or the page structure.

Keep the existing Overview page intact and enhance the map area within the current experience.

The implementation should feel like an upgrade of the current product, not a brand-new screen.

Use the existing preset

Use the existing preset concept already configured in the tool:

“Lending External Relationship Research”

Use that preset as the conceptual AI layer behind the map experience.

This means the map should visually support the idea that AI / preset-backed research can enrich the geography view with relationship context.

Do not hardcode fake business logic. Reuse existing data and existing APIs where available.
If preset-backed relationship overlays are not fully available yet, structure the map so that it can display them cleanly now or later.

What the upgraded map should show

The map should support a layered view with the following visual ideas:

1. Exposure circles / bubbles

Show country or regional nodes as circles scaled by portfolio significance, for example using:

reported OSUC
client count
CAM-covered count
exposure amount

These circles should feel alive and visual, not static.

2. Relationship overlay

Add an optional overlay for relationships:

lines / arcs between regions or countries
dotted or curved connectors
different visual treatment for:
known source-backed relationships
AI-reviewed / preset-backed relationships
higher-attention links
3. Clear hover behavior

On hover or click, show a compact info panel / tooltip with useful fields such as:

country / region
exposure
client count
CAM-covered count
number of relationships
number of AI-supported relationships
review-required items if available
4. Filters / controls

Add lightweight map controls so the user can switch views without leaving the page. For example:

metric selector:
Reported OSUC
Client Count
CAM Coverage
Relationship Count
layer toggles:
Exposure
Relationships
AI-reviewed links
Review-needed hotspots
geography scope:
Global
Region filters
5. Dynamic visual feel

Make the map feel more analytical and interactive by using:

circles of different sizes
layered markers
subtle glow or ring treatment
curved connectors
emphasis on hotspots
clean legend

Do this in a professional enterprise style, not in a flashy consumer style.

Product behavior expectation

The user should be able to look at the map and immediately understand:

“Where is the portfolio concentrated?”
“Where are important relationship clusters?”
“Where is AI adding extra relationship context?”
“Which geography should I inspect next?”

The map should act as an analytical navigation aid, not just decoration.

Functional expectations

Implement this enhancement in a way that:

Reuses existing page structure and existing data sources where possible.
Does not break existing Overview page behavior.
Works even if some AI / preset relationship data is missing.
Gracefully falls back to geography + exposure only.
Is ready to support richer preset-driven overlays when available.
Technical guidance
Inspect the current Overview / Portfolio Analytics page and identify the existing map section.
Upgrade that section rather than replacing the whole page.
Reuse current frontend patterns, styling conventions, and component structure.
Prefer clean, maintainable implementation over a large redesign.
Keep the rest of the Overview page unchanged unless a very small surrounding adjustment is necessary for the new map to fit properly.

If a visualization library is already used or appropriate, use it carefully.
If not, implement with the least disruptive option.

Deliverable

Please do the following:

Briefly state your implementation plan.
Identify the frontend files you will modify.
Implement the enhanced interactive map.
Keep changes scoped to the map experience only.
Summarize what was changed and any assumptions about data availability.
Visual tone

Use the same product tone as the current application:

enterprise
clean
analytical
credible
relationship intelligence oriented

The result should feel like a natural extension of the current tool and should visually align with the purpose of the preset.
