CCR ADVANCED UI RECONSTRUCTION — STAGE 1
VISUAL SYSTEM + ANALYTICAL WORKSPACE SHELL

Work ONLY in the current CCR repository.

This is an IMPLEMENTATION task.

Do not merely inspect, propose, summarize, or write a report.
Continue modifying and validating the application until the required UI is
implemented and the acceptance criteria below pass.

The existing UI-1 application is functional and must be preserved as the
technical/data foundation.

DO NOT change:

- canonical CCR business data
- protected Phase-2 data
- relationship semantics
- evidence semantics
- research semantics
- candidate semantics
- source-policy semantics
- provider execution behavior
- database truth
- production relationship counts
- API meaning

Do not fabricate:

- relationships
- events
- AI output
- exposure totals
- risk scores
- active/inactive states
- source readiness

==================================================
CURRENT PROBLEM
==================================================

The current UI is structurally correct but visually inadequate.

Problems to fix:

1. Too much blank white space.
2. Low visual hierarchy.
3. Pages feel disconnected.
4. The interface resembles a technical administration console rather than an
   institutional relationship-intelligence platform.
5. Right inspector consumes too much permanent screen width.
6. The global navigation is visually weak.
7. Analytical content lacks density.
8. Empty states occupy large areas with almost no analytical value.
9. Network/Radar/Events/Research currently appear like unfinished placeholders.
10. The visual system does not communicate relationship layers, research state,
    evidence state, source confidence, provider state, or selected context
    strongly enough.
11. The current application is far lighter and flatter than the desired
    intelligence-workstation experience.

==================================================
TARGET EXPERIENCE
==================================================

Reconstruct the interface into a premium institutional analytical product.

Think:

- Bloomberg-style information density
- modern graph intelligence platform
- credit-risk workstation
- Palantir-like analytical workspace
- sophisticated relationship/network investigation interface

Do NOT imitate any product directly.

The visual goal is:

DARK ANALYTICAL WORKSPACE
+
HIGH INFORMATION DENSITY
+
STRONG ENTITY CONTEXT
+
WORLD / NETWORK VISUALIZATION
+
EVIDENCE / RESEARCH TRACEABILITY
+
LOW WASTED SPACE

==================================================
1. DEFAULT THEME
==================================================

Make DARK MODE the default.

Use approximately:

page background:
#071018 / #08131c family

primary surface:
#0d1822

secondary surface:
#111f2b

raised surface:
#152633

border:
rgba(130,165,185,0.18)

primary text:
#edf5f7

secondary text:
#a7bbc5

muted:
#6f8793

teal:
#2fc5b4

blue:
#4fa3ff

purple:
#9b7cff

orange:
#f0a34a

red:
#eb6464

green:
#49c885

Do not scatter hard-coded colors everywhere.

Create centralized design tokens.

Use status colors consistently.

==================================================
2. GLOBAL WORKSPACE LAYOUT
==================================================

Reconstruct the application shell as:

LEFT RAIL
+
TOP COMMAND BAR
+
MAIN ANALYTICAL CANVAS
+
COLLAPSIBLE RIGHT INSPECTOR
+
OPTIONAL BOTTOM CONTEXT DRAWER

Target 1920x1080 first.

Must remain usable at 1440 width.

LEFT RAIL:

width approximately 210–230px expanded.

Sections:

PORTFOLIO
ENTITIES
NETWORK
RADAR
EVENTS
RESEARCH
EVIDENCE
REVIEW

Bottom:

PROVIDERS
SYSTEM

Use icons + labels.

Active destination must be visually strong.

Allow rail collapse to icon-only mode.

==================================================
3. TOP COMMAND BAR
==================================================

Create one strong persistent command bar.

Left:

CCR / RELATIONSHIP INTELLIGENCE

Center:

global entity search

Placeholder:

Search entity, GFCID, CAGID, LEI, CIK, ticker...

Right:

selected entity context
provider pulse
AI Analyst
workspace controls

Selected entity chip must remain visible.

Example:

07 Holdings, LLC
MASTER:1034329369

Clicking it should open entity quick context.

==================================================
4. ENTITY CONTEXT
==================================================

Keep current selected entity URL behavior.

Do not lose selected entity when navigating.

Make selection feel like the permanent investigation context.

At the top of analytical pages show a compact context row:

ENTITY
CLASS
COUNTRY
IDENTITY QUALITY
CCR MEMBERSHIP
RESEARCH STATUS

Do not repeat large entity cards everywhere.

==================================================
5. INSPECTOR BEHAVIOR
==================================================

Current inspector is too permanently dominant.

Change it to:

COLLAPSIBLE
RESIZABLE if practical

Default width:
340px

Closed state:
48px vertical handle

Inspector tabs:

OVERVIEW
IDENTITY
RELATIONSHIPS
RESEARCH
EVIDENCE
SOURCE

Inspector content changes based on selection.

If nothing special is selected:
show selected entity overview.

If a map country is selected:
show country analytics.

If a graph node is selected:
show entity details.

If an edge is selected:
show relationship/evidence details.

If a research run is selected:
show run details.

==================================================
6. PAGE DENSITY
==================================================

Remove giant empty areas.

Use a responsive analytical grid.

Cards should typically be:

compact
12–20px padding
6–10px radius maximum
subtle borders

Avoid huge rounded cards.

Avoid giant page headings.

Page title should usually fit within 60–90px vertical space.

==================================================
7. TYPOGRAPHY
==================================================

Use a serious analytical hierarchy.

Page title:
28–34px

section heading:
14–18px

micro-label:
10–11px uppercase

body:
12–14px

table:
11–13px

numeric KPIs:
22–30px

Use monospace only for:

IDs
run IDs
hashes
technical provenance

==================================================
8. STATUS SYSTEM
==================================================

Create reusable semantic badges.

RELATIONSHIP STATES:

CONFIRMED
PROPOSAL
CANDIDATE
HISTORICAL
CONFLICT
REJECTED
NO_DATA

RESEARCH STATES:

READY
RUNNING
PROPOSAL_PENDING_REVIEW
INSUFFICIENT_EVIDENCE
NOT_FOUND
PROVIDER_UNAVAILABLE
IDENTITY_UNRESOLVED
RELATED_ENTITY_UNRESOLVED
DIRECTION_UNRESOLVED
CONFLICT_REVIEW_REQUIRED

PROVIDER STATES:

READY
AVAILABLE
DEGRADED
UNAVAILABLE
NOT_CONFIGURED

Do not map all states to generic red/green.

==================================================
9. DATA-TRUTH BANNERS
==================================================

Keep important governance warnings.

But redesign them as compact inline banners.

Examples:

Exposure:
"Currency, units and additive semantics are not governed."

Candidates:
"Research candidates are leads, not relationship evidence."

AI:
"AI is an analytical assistant, not relationship evidence."

No giant warning boxes.

==================================================
10. EMPTY STATE DESIGN
==================================================

Current empty states waste too much space.

Replace them with compact analytical empty states.

Example:

NO GOVERNED EVENTS

0 source-backed events are currently stored.

Available signals:
• 49 source documents
• 144 research candidates
• provider research available where configured

[Open Research]

Do NOT invent event data.

==================================================
11. LOADING / INTERACTION
==================================================

Add:

skeleton loaders
hover states
keyboard focus
compact tooltips
sticky table headers
smooth inspector transitions
selected row highlighting
selected graph-node highlighting
URL-preserved filters

Keep animations restrained.

==================================================
12. REMOVE OLD VISUAL SYSTEM
==================================================

Do not keep the current washed-out styling mounted underneath.

Identify old UI-1 visual classes and replace or isolate them.

Do not break old backend behavior.

==================================================
13. VALIDATION
==================================================

Run:

npm run build
npm run lint

Run backend regression.

Fix all new frontend TypeScript/lint errors caused by this stage.

Do not stop because of one pre-existing warning if it is unrelated.

==================================================
14. ACCEPTANCE CHECK
==================================================

Before stopping, verify manually or programmatically:

- Dark workspace loads.
- Left rail works.
- Left rail collapses.
- Top command bar works.
- Selected entity persists across navigation.
- Inspector opens/closes.
- Existing Portfolio page renders inside new shell.
- Existing Entities page renders inside new shell.
- Existing Network page renders inside new shell.
- Existing Radar page renders inside new shell.
- Existing Events page renders inside new shell.
- Existing Research page renders inside new shell.
- Existing Evidence page renders inside new shell.
- Existing Review page renders inside new shell.
- No fake data introduced.
- Backend data unchanged.
- Frontend production build passes.

Create/update:

backend/data/CCR_ADVANCED_FRONTEND_UI2_STAGE1_REPORT.md

FINAL RESPONSE:

CCR UI2 STAGE 1: PASS / FAIL

WORKSPACE SHELL:
PASS / FAIL

DARK ANALYTICAL DESIGN:
PASS / FAIL

COLLAPSIBLE INSPECTOR:
PASS / FAIL

ENTITY CONTEXT PERSISTENCE:
PASS / FAIL

FRONTEND BUILD:
PASS / FAIL

BACKEND REGRESSION:
passed:
failed:
errors:

FAKE DATA CREATED:
0 / FAIL

STOP ONLY AFTER IMPLEMENTATION AND VALIDATION ARE COMPLETE.
