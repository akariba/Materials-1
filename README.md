IMPLEMENT THE NEXT NETWORK INTELLIGENCE PHASE.

Do not perform another broad architecture audit.

Do not redesign the entire application.

Do not start Unix deployment packaging yet.

The immediate objective is to turn the existing Network page into the primary relationship-intelligence surface, with:

1. a World Relationship Map near the top
2. multiple network/map views
3. AI Tools available directly beside the map
4. AI tools connected to actual relationship data
5. automatic Helix and Stylus credential readiness / refresh
6. no CAM mutation
7. no duplicate graph or relationship stores

The existing relationship-definition and AI relationship work has already passed:

- backend suite
- focused AI tests
- higher-order relationship-family validation
- TypeScript diagnostics
- production frontend build

Preserve that work.

==================================================
CORE PRODUCT INTENT
==================================================

The Network page should answer immediately:

- Where are our major lending relationships?
- Which clients are connected?
- Which relationships cross countries or regions?
- Where are ownership / guarantor / collateral / management concentrations?
- Which relationships came from CAM?
- Which were AI-defined?
- Which are external / supplemental?
- Which are under review?
- Where are major relationship clusters?
- Where should an analyst investigate further?

The user should be able to move from:

GLOBAL VIEW
    ↓
REGION
    ↓
COUNTRY
    ↓
GROUP
    ↓
CLIENT
    ↓
RELATIONSHIP
    ↓
EVIDENCE

without leaving the intelligence workflow.

==================================================
1. NETWORK PAGE — NEW TOP STRUCTURE
==================================================

Keep the existing main navigation.

Network remains the top-level destination.

At the top of the Network page use:

Network Intelligence

Subtitle:

Explore relationships across the lending portfolio,
identify concentrations, inspect connected groups,
and discover evidence-backed patterns.

Immediately below the title add the view selector:

[ World Map ]
[ Client Network ]
[ Group View ]
[ Sector View ]
[ Geographic View ]
[ Supply Chain ]
[ Custom View ]

IMPORTANT:

World Map should become the first/highest-level view.

It should appear near the top of the page.

Do not hide it deep below existing tables.

==================================================
2. TOP NETWORK INTELLIGENCE LAYOUT
==================================================

For World Map view use a two-column top layout.

LEFT:
approximately 70% width

WORLD RELATIONSHIP MAP

RIGHT:
approximately 30% width

AI TOOLS + CURRENT SELECTION / INSIGHTS

Conceptually:

------------------------------------------------------------
|                                                          |
|               WORLD RELATIONSHIP MAP                     |
|                                                          |
|                                                          |
|                                            | AI TOOLS    |
|                                            |             |
|                                            | Create Rel. |
|                                            | Analyze Net |
|                                            | Concentrate |
|                                            | Research    |
|                                                          |
------------------------------------------------------------

Below this top area show:

portfolio relationship metrics
network insights
relationship distributions
selected entity / relationship details
recent activity

Do not place the map below several screens of statistics.

The map is the primary visual object.

==================================================
3. WORLD MAP
==================================================

Build a real interactive world map.

Do not use a static image.

Reuse existing portfolio geography and relationship data.

If the current project already contains geographic normalization / country data, reuse it.

Do not create another geographic dataset unless required.

The map should display:

- countries
- portfolio entities
- relationship clusters
- cross-border relationships
- relationship concentration
- selected groups
- selected clients

Map should support:

zoom
pan
fit to world
reset
country selection
region selection
entity selection
relationship selection

==================================================
4. MAP REPRESENTATION
==================================================

Use clustered points at global zoom.

Example:

North America
142 relationships
42 entities

Europe
96 relationships
36 entities

Asia-Pacific
78 relationships
28 entities

Middle East
28 relationships
10 entities

Africa
16 relationships
8 entities

Latin America
34 relationships
12 entities

DO NOT hardcode these numbers.

Use actual backend results.

At higher zoom levels break regional clusters into:

country
city / entity clusters where supported
individual entities

==================================================
5. CROSS-BORDER RELATIONSHIP ARCS
==================================================

Show relationship arcs between regions / countries.

Examples:

United States → United Kingdom
Parent / Subsidiary

United States → Ireland
Common Guarantor

Germany → United States
Ownership / Control

Japan → United States
Supplier / Customer

The arcs must come from actual relationship instances.

Do not fabricate links.

==================================================
6. RELATIONSHIP ORIGIN / LANE SEMANTICS
==================================================

Preserve the existing governance lanes.

Map legend should distinguish:

CAM / Internal
AI Defined — Published
AI Preview
External / Supplemental
Review Required

Use the same semantics already introduced in Network and Relationship Explorer.

Do not create another definition of source origin.

All views must use the same underlying relationship-lane model.

==================================================
7. RELATIONSHIP FAMILY FILTERS
==================================================

Add top filters:

Relationship Type
Source Lane
Status
Sector
Country / Region
Confidence
Definition
Exposure

Relationship Type should include existing supported families such as:

Ownership / Control
Parent / Subsidiary
Guarantor
Common Guarantor
Collateral
Common Collateral
Management
Shared Management
Shared Address
Commercial
Supplier / Customer
Other

Only expose families actually present in the data model.

==================================================
8. WORLD MAP SELECTION
==================================================

Clicking a regional cluster should zoom.

Clicking a country should:

- highlight that country
- filter relevant relationships
- open a right-side summary panel

Example:

UNITED STATES

Clients
128

Relationships
342

Connected Groups
17

Cross-Border Relationships
86

Reported OSUC
$...

CAM Coverage
...

AI-Defined Relationships
...

Review Required
...

Actions:

View Clients
View Relationships
Analyze Region
Open Network

Use actual data.

==================================================
9. ENTITY SELECTION
==================================================

Clicking an entity should open the existing-style entity inspector.

Show:

Entity Name
CAGID / entity ID
Entity Type
Country
Sector
Reported OSUC
CAM Coverage
Risk Rating if available
Relationship Count
Connected Clients
Connected Groups

Tabs:

Overview
Relationships
Groups
Exposure
Evidence

Do not invent risk scores if none exist.

==================================================
10. RELATIONSHIP SELECTION
==================================================

Clicking a relationship arc or edge should open:

RELATIONSHIP INSPECTOR

Show:

Subject
Related Entity
Relationship Type
Direction
Source Lane
Definition
Definition Version
Confidence
Evidence Count
State
Review Status

Actions:

Why Detected
View Evidence
Open in Relationship Explorer
Focus Network

Reuse existing relationship provenance.

==================================================
11. TOP PORTFOLIO METRICS
==================================================

Directly under the map show compact metrics.

Examples:

Countries
Entities
Relationships
Connected Groups
Cross-Border Relationships
AI-Defined Relationships
Review Required
High Concentration Alerts

Do not show every metric at once if space becomes cluttered.

Prioritize the most useful 5–7.

All values must come from current backend state.

==================================================
12. MULTIPLE NETWORK VIEWS
==================================================

World Map is one lens over the same relationship graph.

Implement these views using the same data source.

WORLD MAP

Global geographic relationship view.

CLIENT NETWORK

Existing focal-entity graph.

GROUP VIEW

Connected borrower / economic-group view.

SECTOR VIEW

Relationships grouped by sector.

GEOGRAPHIC VIEW

Country / region concentration and connectivity.

SUPPLY CHAIN

Commercial / supplier / customer relationships where available.

CUSTOM VIEW

User-selected filters / relationship families.

Do not create separate duplicated datasets for each view.

==================================================
13. GROUP VIEW
==================================================

Group View should show connected groups rather than individual raw relationships first.

Example group card:

CONNECTED GROUP

Global Holdings Group

12 entities
4 countries
$4.2B Reported OSUC
18 relationships

Primary drivers:

Ownership
Common Guarantor
Shared Management

Review Required:
2

Actions:

Open Group
View Map
Analyze Group

Group membership should come from existing relationship/correlation logic.

Do not create unsupported legal conclusions.

==================================================
14. AI TOOLS PANEL — TOP RIGHT
==================================================

Beside the map place a persistent panel:

AI Tools

Include:

CREATE RELATIONSHIP
Define a new relationship using AI.

ANALYZE NETWORK
Find patterns and hidden connections.

IDENTIFY CONCENTRATIONS
Detect shared connectors and concentration points.

RESEARCH RELATIONSHIP
Use governed external research to investigate a selected relationship.

GENERATE REPORT
Generate a relationship intelligence summary.

The panel should be compact.

Do not turn the page into an AI chat application.

==================================================
15. CREATE RELATIONSHIP
==================================================

Create Relationship must open the existing:

AI Create Relationship

workflow.

Do not create another tool.

If a country / entity / group is currently selected on the map, pass that context into AI Create Relationship.

Example:

Current context:

Selected group:
Global Holdings

Selected countries:
US, UK, Ireland

The user can then enter:

Identify companies in this network that share a common guarantor.

The AI relationship-definition tool should start with that scope.

==================================================
16. ANALYZE NETWORK
==================================================

Click:

Analyze Network

Open an AI analysis drawer.

It should NOT be a generic chatbot.

Show:

Analysis Scope

Current World
Selected Region
Selected Country
Selected Group
Selected Client
Current Filters

User can choose one.

Prompt examples:

Find major common guarantor clusters.

Identify ownership chains.

Find shared management across unrelated clients.

Identify cross-border concentration.

Find highly connected entities.

Identify potential economic groups.

Find relationships supported by multiple evidence types.

Primary action:

Run Analysis

==================================================
17. NETWORK ANALYSIS OUTPUT
==================================================

Output should be structured.

Example:

NETWORK ANALYSIS

Patterns Detected
4

1. COMMON GUARANTOR CONCENTRATION

Universal Guarantor Ltd

Connected Clients:
5

Countries:
3

Reported OSUC:
$...

Evidence:
12 records

Confidence:
...

[View on Map]
[Inspect Relationships]


2. OWNERSHIP CLUSTER

...


3. SHARED MANAGEMENT CLUSTER

...

Do not output long unstructured AI prose as the primary result.

==================================================
18. AI RESULTS ON MAP
==================================================

AI analysis results should be able to highlight map elements.

Actions:

View on Map
Highlight Network
Open Relationships
Inspect Evidence

Example:

AI detects a common-guarantor cluster.

Click:

View on Map

The map highlights all connected entities and their geographic locations.

Do not automatically publish new relationships.

Analysis is exploratory unless routed through the governed Relationship Definition workflow.

==================================================
19. IDENTIFY CONCENTRATIONS
==================================================

This AI tool should use deterministic metrics first where possible.

Analyze:

shared guarantors
shared collateral
common owners
management overlap
country concentration
sector concentration
connected-group exposure
cross-border relationship concentration

Output:

Concentration
Entities
Countries
Relationship Count
Exposure
Evidence
Review State

Do not invent risk materiality thresholds.

Where thresholds do not exist, label:

Observed concentration

rather than:

High Risk

unless governed rules define High Risk.

==================================================
20. RESEARCH RELATIONSHIP
==================================================

Research Relationship should reuse the existing External Research service.

Do NOT create another external research implementation.

When triggered from Network:

automatically pass current context:

Subject Entity
Related Entity
Relationship Type
Current Evidence
Current Definition
Current Source Lane

The External Research service remains responsible for:

web research
Stylus Runner
SEC filing research where supported
evidence caching
proposal generation

==================================================
21. HELIX AND STYLUS — IMPORTANT ARCHITECTURE
==================================================

Implement reliable automatic readiness and refresh for the AI tools.

IMPORTANT:

Helix/R2D2 and Stylus are separate integrations.

DO NOT incorrectly merge them into a single token mechanism.

The audit found:

HELIX / R2D2

Helix is used by the R2D2 / AI integration.

The existing flow uses the Helix CLI / token mechanism and the existing Python integration.

STYLUS

Stylus Runner is independent.

Stylus is used for live external research / SEC-related research through the Runner Service contract.

Use the actual existing provider implementations.

Do not invent a new authentication mechanism.

==================================================
22. BACKEND CREDENTIAL MANAGERS
==================================================

Centralize each provider behind its own backend readiness manager.

Conceptually:

AI Tools Orchestrator
       |
       +---- AI / R2D2
       |       |
       |       └── Helix Credential Manager
       |
       +---- External Research
               |
               └── Stylus Credential Manager

Do not put token logic in React.

Do not pass raw tokens to the frontend.

==================================================
23. HELIX AUTO REFRESH
==================================================

Before an operation requiring Helix/R2D2:

ensure_helix_access()

Behavior:

Check existing Helix token.

If valid beyond safety window:
reuse token.

If missing / expired / expiring:
invoke the existing supported Helix refresh mechanism.

Then retry readiness.

If refresh succeeds:
continue AI operation.

If refresh fails:
fail only the dependent AI operation with a clear error.

Do not break the rest of the application.

Use existing Helix mechanisms found in the repository.

Do not invent new credentials.

==================================================
24. STYLUS AUTO REFRESH / TOKEN READINESS
==================================================

Before an operation requiring Stylus:

ensure_stylus_access()

Use the existing Stylus token implementation.

The audit found that Stylus already performs local token-expiry validation and treats tokens with less than approximately five minutes remaining as unusable.

Reuse that behavior.

If the current environment provides a supported token renewal / token-seeding mechanism:

use it.

If automatic token renewal is not actually supported by the existing Runner Service integration:

DO NOT fake a refresh.

Instead:

1. attempt the supported existing credential acquisition mechanism
2. return a clear Authentication Required state if it cannot obtain a usable token

Do not create an undocumented refresh-token protocol.

==================================================
25. AUTO PREFLIGHT
==================================================

The user should not have to manually refresh credentials before using AI tools.

For each operation:

Analyze Network
Create Relationship if AI inference is required
Research Relationship
External Research
SEC-related research

run provider preflight automatically.

Example:

Analyze Network
      ↓
requires R2D2?
      ↓
ensure Helix
      ↓
execute


Research Relationship
      ↓
requires Stylus?
      ↓
ensure Stylus
      ↓
execute

If one operation requires both:

ensure each provider separately.

==================================================
26. MANUAL REFRESH CONTROL
==================================================

Also provide an operator convenience action.

In the AI Tools panel or status popover:

AI / Research Access

Helix
Ready

Stylus
Ready

[ Refresh Access ]

Refresh Access should:

- check Helix
- refresh/reacquire if needed
- check Stylus
- reacquire/refresh only through supported existing mechanisms

Do not display tokens.

Optionally allow:

Refresh Helix
Refresh Stylus

inside a detail popover.

==================================================
27. STATUS DISPLAY
==================================================

Use small status indicators.

Example:

AI Access
Helix ● Ready

Research Access
Stylus ● Ready

Other states:

Ready
Expiring Soon
Refreshing
Authentication Required
Unavailable

Do not show:

bearer token
JWT
Authorization header
credential contents
cookie
secret environment variables

==================================================
28. SINGLE-FLIGHT REFRESH
==================================================

Prevent multiple simultaneous refreshes.

If several AI operations arrive while Helix or Stylus needs refresh:

one refresh should occur.

Other callers should await that result.

Implement backend locking / single-flight behavior.

Do not allow token-refresh race conditions.

==================================================
29. PROVIDER FAILURE BEHAVIOR
==================================================

Provider failures must be isolated.

Example:

Helix unavailable

Network browsing:
WORKS

Relationship Explorer:
WORKS

Existing relationships:
WORK

Analyze Network:
UNAVAILABLE

Show:

AI analysis unavailable.
Helix authentication could not be established.

[Retry]


Stylus unavailable

Network:
WORKS

AI internal analysis:
WORKS if it does not require Stylus

External Research:
UNAVAILABLE

Show:

External research unavailable.
Stylus authentication could not be established.

[Retry]

==================================================
30. NO RAW SECRET LOGGING
==================================================

Never log:

Helix bearer tokens
Stylus JWT
Authorization header
cookies
refresh tokens
credential environment values

Safe audit events:

HELIX_ACCESS_CHECK
HELIX_REFRESH_STARTED
HELIX_REFRESH_SUCCEEDED
HELIX_REFRESH_FAILED

STYLUS_ACCESS_CHECK
STYLUS_REFRESH_STARTED
STYLUS_REFRESH_SUCCEEDED
STYLUS_REFRESH_FAILED

AI_NETWORK_ANALYSIS_STARTED
AI_NETWORK_ANALYSIS_COMPLETED

EXTERNAL_RESEARCH_STARTED
EXTERNAL_RESEARCH_COMPLETED

==================================================
31. AI TOOL CONTEXT
==================================================

All AI tools should understand current UI context.

Pass only governed context.

Examples:

Selected Client
Selected Relationship
Selected Country
Selected Region
Selected Group
Current Relationship Filters

Example:

User selects Germany on World Map.

Clicks:

Analyze Network

The analysis scope defaults to:

Germany

User selects:

Common Guarantor

AI analysis should analyze the current German subnetwork rather than the entire portfolio unless changed.

==================================================
32. WORLD MAP + AI INTERACTION
==================================================

Allow AI results to control the map.

Examples:

Highlight these entities
Zoom to cluster
Show only this relationship family
Show connected countries
Show evidence-backed path
Show cross-border chain

But do not allow AI to change underlying relationship records merely by changing the map.

Map state is presentation state.

==================================================
33. AI FINDINGS PANEL
==================================================

Below or beside the map include:

Network Insights

Tabs:

Key Insights
Concentration
Emerging Patterns
AI Findings

Examples:

Shared guarantor concentration
5 clients connected through the same guarantor

[View]


Cross-border ownership cluster
7 entities across 4 countries

[View]


Shared management cluster
3 companies share senior management

[View]


Potential new relationship
Additional evidence may support common control

[Review]

Use actual source-backed results.

==================================================
34. PORTFOLIO EXPOSURE CONTEXT
==================================================

Where exposure data exists, map and analysis should include:

Reported OSUC

Do not invent adjusted exposure or relationship risk exposure.

Examples:

Connected Group
$4.2B Reported OSUC

Country Network
$12.8B Reported OSUC

Relationship Cluster
$820M Reported OSUC

Always label the metric clearly as Reported OSUC where that is the source metric.

==================================================
35. MAP PERFORMANCE
==================================================

Do not attempt to render thousands of individual nodes at world zoom.

Implement clustering / aggregation.

At world level:

region clusters

At regional level:

country clusters

At country level:

entity clusters

At detailed level:

individual entities and relationships

Use progressive rendering.

==================================================
36. MAP DATA CONTRACT
==================================================

Prefer a backend map/network summary endpoint if necessary.

Do not send the entire raw relationship database to the browser.

Return only what is required for the current view.

Possible map response:

regions
countries
entity counts
relationship counts
relationship-family counts
cross-border connections
exposure aggregates
review counts

Then fetch detailed relationships after selection.

Use existing endpoints if they already provide equivalent data.

==================================================
37. WORLD MAP EMPTY / INCOMPLETE GEO DATA
==================================================

Not every entity may have usable geography.

Show:

Mapped Entities
Unmapped Entities

Do not guess coordinates.

If only country is available:

place at country centroid / aggregated country marker.

If country is missing:

keep entity out of geographic placement and surface:

Unmapped Geography

Do not invent locations.

==================================================
38. MAP LEGENDS
==================================================

Legend should support two dimensions without becoming confusing.

RELATIONSHIP ORIGIN

CAM
AI Published
AI Preview
External
Review Required

ENTITY TYPE

Client
Parent
Subsidiary
Guarantor
Other Entity

For relationship family use filters instead of too many simultaneous colors where possible.

Avoid an unreadable rainbow network.

==================================================
39. CLIENT NETWORK
==================================================

Preserve the existing focal relationship graph.

World Map and Client Network must complement each other.

From World Map entity:

Open Client Network

From Client Network:

Show on World Map

This should maintain selected entity context.

==================================================
40. GROUP VIEW
==================================================

From a connected cluster:

Open Group View

Show:

Group Name / generated group label
Entities
Countries
Relationships
Reported OSUC
Primary Relationship Drivers
Evidence Coverage
Review Required

Display a group graph.

Allow:

Show Group on World Map

==================================================
41. CUSTOM VIEW
==================================================

Allow analyst to save a temporary or persisted network filter configuration if existing persistence makes sense.

Example:

North America
+
Common Guarantor
+
Exposure > configured threshold
+
AI Published + CAM

Do not create another complex configuration system in this phase unless straightforward.

==================================================
42. EXISTING RELATIONSHIP TOOL INTEGRATION
==================================================

AI Create Relationship must remain the governed route for defining new relationship logic.

The Network AI tool may suggest:

Potential Common Control pattern detected.

But the action should be:

Create Relationship Definition

or

Review Candidate

It must NOT silently convert exploratory AI findings into published relationships.

==================================================
43. REVIEW QUEUE INTEGRATION
==================================================

When map/AI analysis discovers a candidate requiring review:

route it to the existing governed review workflow.

The user should be able to:

View on Map
Inspect Evidence
Open Review Queue

Do not create another approval queue.

==================================================
44. TOP PAGE LAYOUT TARGET
==================================================

The final Network page should visually resemble:

------------------------------------------------------------
NETWORK INTELLIGENCE
[World Map] [Client Network] [Group] [Sector] [...]

------------------------------------------------------------
| WORLD RELATIONSHIP MAP             | AI TOOLS            |
|                                    |                     |
| region / country clusters          | Create Relationship |
| cross-border arcs                  | Analyze Network     |
| CAM / AI / External lanes          | Concentrations      |
|                                    | Research            |
|                                    | Generate Report     |
------------------------------------------------------------

[ Countries ] [ Entities ] [ Relationships ]
[ Connected Groups ] [ Review Required ]

------------------------------------------------------------
| NETWORK INSIGHTS        | RELATIONSHIP TYPES             |
|                         |                                |
| concentration           | distribution                   |
| emerging patterns       | trends                         |
| AI findings             |                                |
------------------------------------------------------------

[selected relationship / entity details as appropriate]

==================================================
45. DO NOT REDESIGN THE ENTIRE APPLICATION
==================================================

Keep existing:

header
navigation
cards
typography
filters
Relationship Explorer
External Research
Review Queue
Network graph
relationship inspectors

Extend them.

Do not introduce a new design system.

==================================================
46. TESTS
==================================================

Add backend tests where needed for:

world map aggregation
country aggregation
cross-border relationship aggregation
source-lane filtering
relationship-family filtering
AI-analysis scope
Helix preflight
Helix refresh/reacquisition
Stylus preflight
Stylus usable-token handling
Stylus unavailable state
single-flight refresh behavior
provider failure isolation

Frontend validation:

World Map renders
filters work
cluster selection works
country selection works
entity selection works
relationship inspector works
AI Tools panel renders
Analyze Network scope works
AI results can highlight map
Create Relationship opens existing workflow
Research Relationship opens existing External Research flow
provider status appears safely
no tokens appear in frontend state/responses
existing Client Network still works

==================================================
47. END-TO-END VALIDATION
==================================================

Perform this actual workflow:

1. Open Network.
2. World Map is visible near the top.
3. Confirm actual entities/relationships are represented.
4. Select a region.
5. Select a country.
6. Select an entity.
7. Inspect its top relationships.
8. Open Client Network.
9. Return to World Map.
10. Run Analyze Network for the selected geography.
11. Verify Helix preflight occurs automatically if required.
12. Confirm no manual token copying is required.
13. Highlight one AI finding on the map.
14. Select one relationship.
15. Run Research Relationship.
16. Verify Stylus preflight occurs automatically.
17. Confirm External Research receives the selected entities / relationship as context.
18. Return research evidence.
19. Confirm no CAM record is modified.
20. Open Create Relationship from AI Tools.
21. Confirm existing AI Create Relationship workflow opens with selected context.
22. Generate / preview a relationship definition.
23. Confirm preview can be shown on Network.
24. Confirm review-required candidate routes to Review Queue.

==================================================
48. IMPORTANT TOKEN VALIDATION
==================================================

After implementation explicitly verify:

- no Helix token is returned to React
- no Stylus token is returned to React
- no bearer token is rendered in UI
- no token is written to localStorage
- no token is written to sessionStorage
- no token is placed in a URL
- no token appears in application logs
- no token appears in audit records

==================================================
49. FINAL REPORT
==================================================

Report:

IMPLEMENTED

WORLD MAP

MAP DATA SOURCE

REGIONS / COUNTRIES MAPPED

UNMAPPED GEOGRAPHY

CROSS-BORDER RELATIONSHIPS

NETWORK VIEW TABS

AI TOOLS PANEL

CREATE RELATIONSHIP INTEGRATION

ANALYZE NETWORK

IDENTIFY CONCENTRATIONS

RESEARCH RELATIONSHIP

HELIX PREFLIGHT

HELIX AUTO REFRESH / REACQUISITION

STYLUS PREFLIGHT

STYLUS AUTO REFRESH / REACQUISITION

PROVIDER FAILURE BEHAVIOR

TOKEN LEAKAGE CHECK

NETWORK INSIGHTS

RELATIONSHIP EXPLORER INTEGRATION

EXTERNAL RESEARCH INTEGRATION

REVIEW QUEUE INTEGRATION

CAM IMMUTABILITY CHECK

BACKEND TEST RESULTS

FRONTEND BUILD RESULT

KNOWN LIMITATIONS

Do not mark complete because the map visually renders.

Completion requires:

- real relationship data
- working filters
- functioning selections
- actual AI tools
- automatic credential preflight
- map-to-AI context
- map-to-research context
- relationship workflow integration
- CAM immutability
