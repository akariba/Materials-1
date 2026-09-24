CCR UI-2 — STAGE 2
HUMAN-DESIGNED ANALYST WORKSPACE

Work only in the existing CCR repository.

Do not change backend business semantics.
Do not fabricate relationships, events, risk scores, exposure totals,
AI results, evidence, provider readiness or analytical conclusions.

Preserve all existing real-data safeguards.

OBJECTIVE

The existing dark UI still looks like a generic AI-generated dashboard.

Redesign the PRESENTATION SYSTEM so it looks like a deliberately designed
institutional intelligence application built for professional analysts.

This is NOT a color/theme exercise.

The objective is:

- stronger information hierarchy
- fewer generic cards
- less repeated visual structure
- higher analytical density
- deliberate use of whitespace
- bespoke analytical components
- contextual information instead of KPI-card grids
- stronger typography hierarchy
- better entity-centric navigation
- better use of the entire viewport
- more professional interaction patterns

DESIGN PRINCIPLE

Do not make every information group a bordered rectangle.

Use a mixture of:

- inline metrics
- data tables
- split panes
- timelines
- evidence strips
- expandable rows
- segmented controls
- contextual drawers
- analytical canvases
- relationship legends
- compact status markers
- semantic grouping
- progressive disclosure

Cards should be used only where they materially improve comprehension.

REMOVE THE “AI DASHBOARD” LOOK

Avoid:

- excessive glowing borders
- neon everywhere
- identical KPI cards
- excessive rounded rectangles
- large empty boxes
- decorative gauges
- decorative circles
- fake charts
- giant empty vertical regions
- centered empty-state messages occupying large panels
- repeated title/subtitle/card patterns
- visual effects without analytical meaning

TYPOGRAPHY

Create a clear editorial hierarchy.

Entity/page title:
large but compact.

Section headings:
small institutional uppercase or concise human-readable section labels.

Metadata:
small muted typography.

Important values:
high contrast but not oversized dashboard typography.

Tables:
dense and highly readable.

The interface should feel designed for sustained professional use.

ENTITY HEADER

Create a reusable entity header.

When an entity is selected show, where available:

LEGAL NAME
entity class
country
industry/sector
GFCID
CAGID
LEI
CIK
ticker
identity quality/status

Below it show compact inline counts:

Relationships
Research
Evidence
Events
Reviews

Do NOT render these as six large cards.

WORKSPACE GRID

Use a professional multi-pane structure.

LEFT
navigation and analytical layers.

CENTER
primary analytical workspace.

RIGHT
contextual inspector / AI / evidence.

Allow contextual panels to collapse so the analytical canvas can use nearly
the full browser width.

NETWORK PAGE

Do not use the current circular orbit layout.

Prepare a semantic analytical graph canvas.

Selected entity is the anchor.

Relationship groups should be visually organized around semantic categories:

OWNERSHIP
SUPPLIERS
CUSTOMERS
PARTNERS
FINANCING
TECHNOLOGY
INFRASTRUCTURE
OTHER

Solid edges:
evidence-backed observations only.

Dotted edges:
research candidates only.

Each visible edge must preserve:
relationship type
direction
state
source/evidence availability

Never visually imply an unsupported relationship.

The graph canvas must be capable of expanding to almost full browser size.

Add view modes:

GRAPH
VALUE CHAIN
OWNERSHIP
GEOGRAPHY
EVIDENCE
TIMELINE

Only activate modes supported by existing data.

ENTITY INSPECTOR

Redesign the right panel into meaningful sections rather than stacked cards.

Use tabs:

OVERVIEW
IDENTITY
RELATIONSHIPS
RESEARCH
EVIDENCE
SOURCES

Use dense key/value presentation.

No fabricated values.

EMPTY STATES

Redesign empty states to be compact.

Example:

Events
No persisted events.
Approved event ingestion has not yet populated this entity.

Do not create a 500px empty rectangle around this message.

PORTFOLIO

Replace the KPI-card-grid feeling with an institutional command view.

Use:

compact metric strip
large map
analytical table or distribution section
research/evidence posture
identity coverage
provider state

Map should remain the visual anchor.

ENTITIES

Make this feel like a professional entity browser.

Use:
sticky table header
dense rows
hover state
selected-row state
keyboard navigation where practical
server-backed search
column alignment
compact identifier presentation

Avoid excessive badge pills.

RADAR

Redesign the layout even when persisted radar data is unavailable.

Prepare areas for:

theme pressure
signal timeline
entity candidate signals
event categories
monitoring state

When data is unavailable, show compact unavailable states.

Do not fabricate radar values.

EVENTS

Use a timeline/event-stream information architecture.

Left:
event stream.

Center:
event detail.

Right/context:
affected entities / evidence / provenance.

Again, no large empty generic cards.

RESEARCH

Make research resemble an investigation workbench.

Use:

research question
provider/source status
evidence collected
claim state
identity state
direction state
review state

Prefer rows/timeline/progress structures over cards.

EVIDENCE

Design an evidence ledger.

Columns should support where available:

Source
Document
Date
Tier
Admissibility
Related entity
Relationship
Research run
Evidence status

Clicking evidence should open a contextual evidence reader.

AI ENTRY POINT

Do not treat AI as a standalone decorative button.

Prepare the existing AI drawer as a contextual analytical companion.

It should visually receive:

selected entity
current page
visible graph scope
current filters
available evidence
research context

Do NOT create new AI backend behavior in this stage.

If AI is unconfigured, clearly show that status.

VISUAL STYLE

Institutional intelligence terminal.

Dark neutral navy/graphite surfaces.

Use accent colors sparingly and semantically:

teal = verified / available / primary interaction
orange = attention / unresolved
purple = research candidate
red = error/unavailable

Avoid neon glow.

Use subtle separators and depth rather than borders around everything.

Use restrained 2–6px radii.

No excessive shadows.

No gradients unless extremely subtle and functional.

VALIDATION

Preserve:

all existing navigation
entity selection
URL-selected entity state
map rendering
search
research reads
evidence reads
provider state
AI status reads
backend API contracts
database hashes
relationship safeguards

Run:

frontend build
frontend lint
backend regression
API smoke tests

Create:

backend/data/CCR_ADVANCED_FRONTEND_UI2_STAGE2_REPORT.md

The report must list:

pages changed
components redesigned
design-system changes
removed generic-card patterns
network-canvas changes
empty-state changes
entity-header implementation
inspector implementation
validation results
known remaining limitations

FINAL RESPONSE

CCR UI-2 STAGE 2: PASS / FAIL

PORTFOLIO:
PASS / FAIL

ENTITY BROWSER:
PASS / FAIL

ENTITY HEADER:
PASS / FAIL

NETWORK ANALYTICAL CANVAS:
PASS / FAIL

RADAR WORKBENCH:
PASS / FAIL

EVENT TIMELINE:
PASS / FAIL

RESEARCH WORKBENCH:
PASS / FAIL

EVIDENCE LEDGER:
PASS / FAIL

INSPECTOR:
PASS / FAIL

AI CONTEXT SHELL:
PASS / FAIL

NO FABRICATED DATA:
PASS / FAIL

FRONTEND BUILD:
PASS / FAIL

BACKEND REGRESSION:
passed / failed / errors

REPORT:
backend/data/CCR_ADVANCED_FRONTEND_UI2_STAGE2_REPORT.md

STOP.
