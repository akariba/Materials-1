LENDING POC — APPLY THE APPROVED VISUAL DESIGN

The current application functionality and backend wiring are accepted.

DO NOT change:
- Portfolio API
- V1/V2/V3
- 13 canonical relationships
- 28 review-required relationships
- relationship extraction
- external-overlay governance
- Stylus / SEC / R2D2
- CCR
- RPR
- business calculations

THIS TASK IS VISUAL / INTERACTION DESIGN ONLY.

The current frontend presentation is NOT the approved design.

Replace the current visual presentation with the previously approved
"Lending Relationship Intelligence" design described below.

==================================================
1. DESIGN LANGUAGE
==================================================

Overall appearance:

- modern institutional credit-risk analytics
- light blue / white background
- clean Citi-style professional visual language
- soft cards
- subtle shadows
- rounded corners
- blue / teal analytical accents
- network visualization is the visual centerpiece

Use this palette consistently:

Page background:
#F5F8FC

Card background:
#FFFFFF

Primary dark text:
#15263A

Secondary text:
#66768A

Border:
#DCE5EF

Primary blue:
#376FF6

Light blue:
#7DB7FF

Cyan:
#55C7E8

Teal:
#37B6A4

Green:
#57B879

Purple:
#8B78E6

Amber:
#E8AD55

Orange:
#E78A57

Red:
#D96767

Muted gray:
#9AA8B7

Do NOT use a plain monochrome network.

==================================================
2. TOP APPLICATION HEADER
==================================================

Use:

Lending Relationship Intelligence

Subtitle:

CAM-authoritative relationship intelligence with corroborating Web and SEC
evidence.

Top navigation:

Overview
Network View
Relationship Explorer
Review Queue
Reports

Network View should have the strongest visual treatment when selected.

Keep navigation clean and horizontal.

==================================================
3. NETWORK VIEW — MATCH APPROVED CONCEPT
==================================================

The Network View must visually resemble the previously approved design:

LEFT COLUMN
Network Filters

CENTER
large relationship intelligence map

RIGHT COLUMN
Entity Overview / Relationship Inspector

The graph must occupy most of the visual area.

Do not use the current small circular ring graph.

==================================================
4. NETWORK LAYOUT
==================================================

Use focal-entity architecture.

Selected company in the CENTER.

Example layout concept:

                 Research / Academic

       Customers                     Financial / Advisory


Infrastructure        FOCAL ENTITY       Regulatory


       Compute                       Investors / Sponsors

              Supply Chain / Infrastructure


Actual categories must come from supported relationship data.

Do not fabricate relationship categories merely to fill the layout.

==================================================
5. RELATIONSHIP GROUP BUBBLES
==================================================

Create softly colored ecosystem regions / halos around related entities.

Examples:

Compute Infrastructure
BLUE

Infrastructure & Supply Chain
ORANGE

Customers
CYAN

Investors & Sponsors
TEAL

Financial & Advisory
AMBER

Research / Academic / Strategic
GREEN

Regulatory
RED

Other supported strategic ecosystem relationships
PURPLE

These are visual groupings only.

Do not alter relationship taxonomy in backend.

Group bubbles should use:

- very pale tinted background
- subtle outline
- group label at top
- related nodes inside the group

==================================================
6. NODE DESIGN
==================================================

FOCAL NODE:

- largest node
- dark blue outer ring
- soft blue glow
- company/entity name underneath or inside
- selected state clearly visible

RELATED NODES:

- smaller
- relationship-family color
- white or very pale center
- colored outline
- clear readable label

PORTFOLIO CLIENT:
slightly stronger node styling

RELATED NON-PORTFOLIO ENTITY:
lighter styling

REVIEW-REQUIRED ENTITY:
small amber review indicator

EXTERNAL ENTITY:
small purple/blue supplementary indicator

==================================================
7. EDGE DESIGN
==================================================

CAM canonical:
solid blue line

CAM review-required:
amber dashed line

Hidden / indirect:
purple dashed / dotted line

External proposal:
teal/purple dotted line

Conflict:
red accented line

Historical:
muted gray dotted line

Do not rely only on color.
Line pattern must also communicate state.

==================================================
8. ANIMATED LIGHT / SIGNAL EFFECTS
==================================================

Add tasteful analytical animation.

The user specifically wants visible "light" movement through the network.

Implement subtle animated effects:

A. SELECTED RELATIONSHIP
A small glowing pulse should travel along the selected edge.

B. HOVER RELATIONSHIP
Edge brightens and a short moving highlight travels from source to target.

C. SELECTED NODE
Soft breathing / pulsing outer glow.

D. NEW / EXTERNAL FINDING
Subtle purple pulse around node or edge.

E. REVIEW REQUIRED
Soft amber pulse, not aggressive flashing.

F. HIDDEN PATH
When selected:
animate the complete path sequentially:

A → B
then
B → C

This should visually explain propagation.

IMPORTANT:

Do NOT create constant distracting flashing.

Animation should be:
subtle
professional
slow
analytical

Use SVG/CSS/requestAnimationFrame or the graph library's native animation.

==================================================
9. NETWORK INTERACTIONS
==================================================

Required:

mouse drag = pan

mouse wheel = zoom

buttons:
+
-
Fit
Reset

Double click node:
make it the focal entity

Single click node:
open Entity Overview

Single click edge:
open Relationship Detail

Hover node:
show small tooltip

Hover edge:
show:
relationship type
direction
state
confidence
source layer

Search:
entity name
CAGID

Search result:
focus node
animate camera toward it
highlight node

==================================================
10. NETWORK TRANSITIONS
==================================================

When focal entity changes:

Do NOT instantly redraw harshly.

Animate:

old nodes fade
selected node moves toward center
new first-degree entities expand outward
edges appear progressively

Transition duration approximately:
300–600ms

The effect should feel like exploring an intelligence network.

==================================================
11. RIGHT ENTITY OVERVIEW PANEL
==================================================

Match the previously approved panel concept.

Header:

Entity Overview

Show:

Entity Name
CAGID
Country
Sector

Tags / badges

Relationship Summary

Reported OSUC
Portfolio Share
Exposure Rank
CAM Count

Direct Relationships
Indirect Relationships
Review Required

Then:

Why it matters for Lending

Only show a generated summary when supported by deterministic backend data.
Do not invent conclusions.

Materiality card:
Exposure-based context only

Confidence card:
relationship/evidence confidence

Evidence Channels:

CAM
Web
SEC

Show availability/status indicators.

Potential Risk Flags:
only backend-supported flags.

==================================================
12. NETWORK METRICS ABOVE GRAPH
==================================================

Use compact metrics similar to the approved design:

Total Entities

Direct Relationships

Indirect Relationships

Pending Review

External Findings

Do not force a metric if unavailable.

==================================================
13. RELATIONSHIP RECORDS UNDER NETWORK
==================================================

Below network provide:

Relationship Records

Columns:

Entity
Relationship
Related Entity
Direction
State
Confidence
Source
Evidence
Review

Keep it compact.

Click a row:
highlight the corresponding edge in the graph.

==================================================
14. ANALYTICAL SUB-TABS UNDER NETWORK
==================================================

Use:

Concentration Analysis
Geographic View
Risk Insights
Recent Mentions

Only activate views supported by real data.

Unsupported future capability:
disabled state

Do not invent contents.

==================================================
15. OVERVIEW PAGE
==================================================

Restyle Overview to use the SAME visual language.

Use:

top KPI strip

Exposure ranking

CAM coverage

Sector concentration

Portfolio geography

Small relationship-network preview

Review attention

Avoid large empty sections.

==================================================
16. REAL PORTFOLIO GEOGRAPHIC MAP
==================================================

Use an actual world map using country polygons.

Background:
very pale blue-gray.

Countries with no portfolio exposure:
#E8EEF5

Portfolio countries:
blue intensity based on selected metric.

Highest exposure:
deep blue.

Modes:

Reported OSUC
Client Count
CAM Coverage

Hover country:
Country
Clients
Reported OSUC
CAM-covered clients
CAM coverage %

Click country:
highlight country with animated blue outline
open filtered client context.

Selected country:
soft glow/pulse.

Do NOT use fake coordinates.

==================================================
17. MAP ANIMATION
==================================================

When switching metric:

smoothly transition country shading.

When hovering:

country outline brightens.

When selected:

subtle animated perimeter glow.

When selecting a country from ranking list:

map smoothly focuses/highlights that country.

No aggressive animation.

==================================================
18. EXPOSURE RANKING VISUAL
==================================================

Restyle the current ranking.

Use:

rank number
client
CAGID
CAM badge
Reported OSUC
portfolio share
small visual exposure bar

Top clients should visually stand out without suggesting a risk conclusion.

Click:
open Client Detail.

==================================================
19. CLIENT DETAIL
==================================================

Use clean profile header.

Then compact tabs:

Overview
Relationships
External Intelligence
Evidence

Add a small client relationship map on Overview.

The client should appear centrally with its strongest first-degree
relationships.

==================================================
20. FULL NETWORK LENSES
==================================================

Keep:

CAM
Exposure
Hidden / Indirect
External

Style them as attractive pill/toggle controls.

CAM:
blue

Exposure:
teal

Hidden:
purple

External:
cyan/purple

Future:

Market & News
AI Ecosystem
Potential Impact

Display as muted disabled pills:
COMING LATER

==================================================
21. SELECTED HIDDEN RELATIONSHIP EXPERIENCE
==================================================

If a legitimate hidden relationship path exists:

Example:

A → B → C

show:

A highlighted
B highlighted
C highlighted

dim unrelated network nodes

animate light sequentially:

A → B → C

Right panel shows:

Hidden path
Hop 1
relationship type
evidence

Hop 2
relationship type
evidence

Overall path confidence cannot exceed weakest hop.

==================================================
22. EXTERNAL RELATIONSHIP EXPERIENCE
==================================================

When external findings exist:

CAM layer remains visible but slightly muted.

External nodes/edges appear with purple/cyan styling.

Animate new external edge once when shown.

Do not continuously flash.

External result must remain visually distinguishable from CAM truth.

==================================================
23. VISUAL HIERARCHY
==================================================

The user should immediately see:

1. focal entity
2. important connected entities
3. relationship type
4. exposure context
5. review status
6. evidence provenance

Not:

technical implementation details
API status text
long explanatory paragraphs
development terminology

==================================================
24. RESPONSIVENESS
==================================================

Optimize primarily for:

1920x1080
1440x900
1366x768

Network center should always receive maximum usable space.

Right panel approximately:
280–340px

Left filter panel approximately:
220–260px

Center graph fills remaining area.

==================================================
25. DO NOT CHANGE DATA
==================================================

After visual redesign confirm:

Portfolio clients unchanged
Reported OSUC unchanged
CAM coverage unchanged
13 canonical unchanged
28 review-required unchanged

No extraction rerun.

No external automatic executions.

==================================================
26. FINAL ACCEPTANCE
==================================================

Verify:

APPROVED LIGHT-BLUE VISUAL STYLE: PASS/FAIL

GROUPED RELATIONSHIP BUBBLES: PASS/FAIL

FOCAL ENTITY NETWORK: PASS/FAIL

PAN: PASS/FAIL

ZOOM: PASS/FAIL

FIT: PASS/FAIL

NODE SEARCH: PASS/FAIL

NODE CLICK: PASS/FAIL

EDGE CLICK: PASS/FAIL

MOVING EDGE LIGHT EFFECT: PASS/FAIL

SELECTED NODE PULSE: PASS/FAIL

HIDDEN PATH ANIMATION: PASS/FAIL

EXTERNAL OVERLAY VISUAL SEPARATION: PASS/FAIL

RIGHT ENTITY PANEL: PASS/FAIL

WORLD MAP: PASS/FAIL

MAP HOVER: PASS/FAIL

MAP CLICK: PASS/FAIL

MAP SHADING: PASS/FAIL

MAP SELECTION GLOW: PASS/FAIL

EXPOSURE RANKING: PASS/FAIL

CAM COVERAGE: PASS/FAIL

SECTOR ANALYTICS: PASS/FAIL

NO MOCK DATA: PASS/FAIL

NO AUTOMATIC EXTERNAL CALLS: PASS/FAIL

V3 UNCHANGED: PASS/FAIL

CCR UNCHANGED: PASS/FAIL

Then STOP.
