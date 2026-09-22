Implement a focused UI enhancement on the first page only.

Page:
Overview / Lending Portfolio Intelligence

Do not redesign the whole application.
Do not work on Unix deployment in this task.
Do not change unrelated pages.
Keep the current visual style and existing top summary cards.

OBJECTIVE

Enhance the Overview page so it becomes a stronger entry point into relationship intelligence.

Make these changes only:

1. Add a world / portfolio geography map below the existing “Sector concentration” area.
2. Add an “AI Config / Correlation” panel on the right side of that section.
3. Add visible controls to refresh Helix and Stylus access.
4. Add a visible “Refresh Helix” link/button in that AI panel.
5. Keep the page clean and analytic, not crowded.

LAYOUT TARGET

Keep the top part of the page as it is:
- Portfolio Clients
- Reported OSUC
- CAM-covered OSUC
- Items Requiring Review
- Exposure ranking
- Sector concentration

Below the current row that contains Exposure ranking and Sector concentration, create a new section.

Recommended layout:

LEFT / MAIN COLUMN
- Portfolio Geography Map
- compact map legend
- top countries / regions summary

RIGHT SIDEBAR
- AI Config / Correlation panel
- Helix / Stylus access status
- Refresh buttons / links
- entry points into AI tools

VISUAL STRUCTURE

--------------------------------------------------
Portfolio Geography / Relationship Intelligence
--------------------------------------------------
| World Map / Geography View      | AI Config    |
|                                 | Correlation  |
| country highlights              |              |
| concentration markers           | AI Create    |
| relationship hotspots           | Correlation  |
|                                 | Review defs  |
|                                 |              |
|                                 | Helix status |
|                                 | Stylus status|
|                                 | Refresh btns |
--------------------------------------------------

MAP REQUIREMENTS

Place the map below “Sector concentration”.
It should feel like a natural continuation of the Overview story.

Use actual portfolio geography data if already available.
Reuse the existing country / geography data pipeline if one exists.
Do not introduce fake hardcoded portfolio values.

The map should show:
- countries with portfolio presence
- concentration by geography
- highlighted top countries
- simple portfolio distribution view

This is an Overview-page map, so keep it lighter than the full Network map.

If current data supports only country-level data, that is enough.
Do not invent coordinates.

Add a small summary beside or below the map:
- Top portfolio countries
- client count
- reported OSUC where available

Example blocks:
United States
United Kingdom
Ireland
Germany
Japan

AI CONFIG / CORRELATION PANEL

Add a compact panel on the right.

Panel title:
AI Config / Correlation

Subtitle:
Configure AI-driven relationship and correlation workflows.

This panel should provide quick actions to the existing AI relationship capability.

Include buttons or links such as:
- Create Relationship
- Relationship Definitions
- Review AI Correlations
- Open Network Intelligence

If “Correlation” is not yet a fully separate module, present it as:
- AI Correlation (coming from relationship patterns / connected groups)
But do not create fake backend behavior.

HELIX / STYLUS ACCESS AREA

Within the AI Config / Correlation panel add a small access/status card.

Title:
AI / Research Access

Show:
Helix
Stylus

Each should display a status badge:
- Ready
- Expiring Soon
- Refresh Required
- Unavailable

Add actions:
- Refresh Helix
- Refresh Stylus
- Refresh All

Important:
These are operator controls only.
Do not expose tokens, JWTs, bearer strings, or secrets.

If backend routes for refresh/status already exist, use them.
If they do not exist, add minimal backend endpoints needed for:
- get access status
- request Helix refresh / reacquisition
- request Stylus refresh / reacquisition through supported existing mechanisms

Do not invent a fake refresh protocol.
Reuse the existing provider logic already present in the codebase.

HELIX BUTTON / LINK

The user specifically wants a visible button/link to refresh Helix.

Add a clear action:
[ Refresh Helix ]

This can be:
- a button in the access card
or
- a text link styled like an action row

Preferred layout:

Helix        [Ready]
Refresh Helix

Stylus       [Ready]
Refresh Stylus

[ Refresh All ]

STYLUS BUTTON

Also add:
[ Refresh Stylus ]

because both provider controls should be visible together.

BEHAVIOR

When refresh is triggered:
- show loading state
- call backend
- update status
- show success/failure toast

Example toasts:
Helix access refreshed
Stylus access refreshed
Unable to refresh Helix
Stylus authentication required

Do not block the rest of the page if refresh fails.

PAGE INTEGRATION

The new section must integrate naturally with the Overview page.
Do not push critical existing content too far down.
Keep spacing compact and enterprise-like.

Preserve:
- existing page header
- existing analytics story tabs
- existing ranking and sector cards
- existing style language

Do not replace the first page with the full Network page.
This is only an Overview-page enhancement.

TECHNICAL CONSTRAINTS

- Reuse existing components where possible.
- Reuse existing map/geography utilities if present.
- Reuse existing AI relationship entry points.
- Reuse existing Helix / Stylus provider logic.
- Do not move token logic to the frontend.
- Do not log secrets.
- Do not redesign unrelated pages.

MINIMAL BACKEND SUPPORT

If needed, add only minimal endpoints for:
- provider status
- refresh Helix
- refresh Stylus

Return only safe status info such as:
- provider name
- status
- last checked
- message

Do not return tokens.

VALIDATION

After implementation validate:
1. Overview page still loads.
2. Existing top summary cards still work.
3. Map renders below sector concentration.
4. AI Config / Correlation panel renders on the right.
5. Refresh Helix button is visible and clickable.
6. Refresh Stylus button is visible and clickable.
7. Status updates after refresh.
8. No secrets appear in the frontend.
9. Existing build still passes.

FINAL REPORT

After implementation report:
- Files changed
- Overview page UI changes
- Map data source used
- AI Config / Correlation actions added
- Helix status / refresh implementation
- Stylus status / refresh implementation
- Any backend endpoints added
- Validation results
- Known limitations
