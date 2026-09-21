You have completed the repository audit.

NOW IMPLEMENT.

Do not perform another broad architecture audit.

Do not begin Unix deployment work.

The long-term deployment target remains Unix/Linux, so do not introduce new Windows-only dependencies, but the immediate objective is to make the existing Lending Relationship Intelligence tools work end to end in the current environment.

==================================================
IMPORTANT FINDINGS FROM THE AUDIT
==================================================

Use these findings as architectural constraints.

1. The existing backend already contains a governed AI relationship workflow in:

   lending_ai_relationships.py

The audit found that this workflow already supports or substantially supports:

- interpreting an analyst prompt into structured configuration
- saving a relationship definition
- saving versioned drafts
- previewing eligible source-backed matches
- requiring a saved version before review
- explicit analyst approval / actor identity
- publishing versioned AI relationship instances
- audit events
- provenance

DO NOT recreate this capability in another service.

Extend and expose it.

2. The primary operational SQLite store already contains:

- AI relationship definitions
- definition versions
- relationship instances
- audit events
- ingestion state
- evidence
- review decisions
- external-research related state

Reuse this persistence.

Do NOT introduce another relationship-definition database.

3. Higher-order relationships already support deterministic shared-connector synthesis.

Existing supported or partially supported families include:

- Common Guarantor
- Common Collateral Provider
- Common Ownership / Control
- Shared Management
- Shared Address when governed address evidence exists

Reuse the existing synthesis code.

4. Published AI rows already enter the Lending read layer with explicit origin / quality metadata.

They do NOT mutate the frozen CAM source payload.

Preserve this behavior.

5. External research remains a separate evidence lane.

External evidence is proposal-only and cannot independently create a published Lending relationship instance.

Preserve that governance boundary.

6. There is also a separate external overlay store.

Do not merge this blindly into the primary relationship store.

7. Do NOT work on SEC / Stylus / Helix authentication in this task.

The audit established:

- SEC research is delegated through Stylus Runner.
- There is no direct SEC/EDGAR client.
- Stylus authentication is separate from Helix/R2D2.
- Credential refresh requires a separate focused implementation.

Leave current provider behavior intact for now.

==================================================
PRIMARY OBJECTIVE
==================================================

Make the existing AI Relationship Definition workflow usable from the application UI from beginning to end.

The user journey must become:

Relationship Explorer
        ↓
Relationship Definitions
        ↓
AI Create Relationship
        ↓
Describe
        ↓
Generate structured configuration
        ↓
Configure
        ↓
Preview against real data
        ↓
Inspect candidate relationships
        ↓
Why Detected
        ↓
Save Draft
        ↓
Version / Review
        ↓
Publish
        ↓
Generate governed relationship instances
        ↓
Relationship Records
        ↓
Network
        ↓
Review Queue where required

This must use the actual existing backend and actual application data.

DO NOT create mock candidates or disconnected UI.

==================================================
STEP 0 — PRESERVE CURRENT WORK
==================================================

Before modifying files:

- inspect the current git diff / working tree
- identify existing uncommitted changes
- preserve already implemented work
- do not overwrite working relationship functionality
- do not reset the repository
- do not discard current changes

There are already substantial modifications in the working tree.

Integrate with them.

==================================================
STEP 1 — MAP EXISTING BACKEND TO UI
==================================================

Inspect the existing AI relationship code specifically.

Focus on:

lending_ai_relationships.py
lending_relationship_database.py
workbench.py
main.py

and any associated:

models
schemas
tests
relationship read-layer functions
network functions
review functions

Determine the existing functions/routes for:

- create definition
- interpret prompt
- save draft
- list definitions
- get definition
- version definition
- preview
- approve
- publish
- list published instances
- retrieve provenance
- retrieve evidence
- higher-order synthesis

DO NOT stop after reporting this.

Immediately use those existing capabilities to implement the UI.

Only add API routes when an existing backend capability cannot currently be reached cleanly by the frontend.

==================================================
STEP 2 — RELATIONSHIP EXPLORER
==================================================

Do not add another top-level navigation destination.

Extend the existing Relationship Explorer.

Add two internal views:

[ Relationship Records ]    [ Relationship Definitions ]

Default:

Relationship Records

Relationship Records must preserve the current functionality.

Relationship Definitions exposes the governed definition layer.

==================================================
STEP 3 — RELATIONSHIP DEFINITIONS LIBRARY
==================================================

Implement the Relationship Definitions view using actual persisted definitions.

Header:

Relationship Definitions

Primary action:

+ Create Relationship

Create Relationship options:

AI Create Relationship
Use Template
Create Manually

For this implementation, AI Create Relationship must be fully functional.

Use Template and Create Manually may reuse the same structured editor if appropriate.

Add actual summary metrics:

Active
Draft
Testing / Review
AI Assisted

Do not use hardcoded numbers.

Display a table/list using persisted backend values.

Recommended columns:

Relationship
Category
Entities
Detection Method
Source Lane
Confidence
Instances
Creation Method
Version
Status
Last Tested
Last Updated

Clicking a definition should open its details/version information.

==================================================
STEP 4 — AI CREATE RELATIONSHIP
==================================================

Use an integrated workspace.

Prefer:

large right-side drawer

or

large in-page workspace

Do NOT create a chatbot page.

Workflow:

Describe
Configure
Preview
Publish

The workflow must maintain state when moving backward and forward.

==================================================
STEP 5 — DESCRIBE
==================================================

Provide:

Describe the relationship you want the system to identify

Large textarea.

Suggested relationship starters:

Common Guarantor
Common Collateral
Common Ownership / Control
Shared Management
Shared Address
Parent / Subsidiary

Example:

Identify companies that share a common guarantor.
Require at least one qualifying shared guarantor.
Use internal evidence as the primary source.
Send uncertain relationships for review.

Action:

Generate Configuration

IMPORTANT:

Call the existing backend interpretation/configuration logic.

Do not implement a second natural-language parser in React.

Do not simply copy the prompt into a database field and call that configuration.

==================================================
STEP 6 — CONFIGURE
==================================================

Render the structured configuration returned/generated by the backend.

Organize it into sections.

RELATIONSHIP

Name
Code
Description
Category
Relationship Type
Direction

ENTITIES

Source Entity
Target Entity

DETECTION

Detection Family
Connector Type
Minimum Shared Connectors
Maximum Connector Group Size
Minimum Connector Confidence

EVIDENCE

Minimum Evidence Records
Minimum Evidence Quality
Require Source Document
Require Connector ID
Require Entity IDs

SOURCES

Internal / CAM
External Research
SEC Regulatory Filing
Corporate Filing
Corporate Website
Trusted Web

CONFIDENCE

Minimum Confidence
Auto Qualification Threshold
Review Threshold

GOVERNANCE

Automatically Qualify
Send for Review
Suggest Only

NETWORK

Show on Network
Edge Label
Edge Weight
Direction
Maximum Traversal Depth

Only display configuration fields actually supported by the backend.

If a field is planned but not implemented:

do NOT create a fake interactive control.

Either:

- hide it
- disable it with an explanatory label
- or explicitly mark it as future capability

==================================================
STEP 7 — HIGHER-ORDER RELATIONSHIP CONFIGURATION
==================================================

Expose the deterministic shared-connector functionality already present.

Prioritize:

COMMON GUARANTOR

Company A
        \
       Guarantor X
        /
Company B

→ Common Guarantor


COMMON COLLATERAL

Company A
        \
       Collateral X
        /
Company B

→ Common Collateral Provider / Shared Collateral


COMMON OWNERSHIP / CONTROL

Company A
        \
        Owner X
        /
Company B

→ Common Ownership / Control


SHARED MANAGEMENT

Company A
        \
       Executive X
        /
Company B

→ Shared Management


SHARED ADDRESS

Only create this relationship when governed shared-address evidence actually exists.

If no qualifying address signal exists:

return zero candidates.

Zero is correct.

Do not manufacture candidates.

==================================================
STEP 8 — PREVIEW MUST USE REAL DATA
==================================================

Preview is the most important stage.

The existing backend has already demonstrated live synthesis results.

Connect the Preview UI to the real preview backend.

Show actual values returned by the engine.

Metrics may include:

Candidate Records
Shared Connectors
Synthesized Entity Pairs
High Confidence
Review Required
Rejected

Do NOT hardcode previously observed counts.

Always display the current preview response.

Preview must NOT:

- publish the definition
- modify CAM
- create permanent canonical relationships
- change review decisions
- leave permanent graph state

==================================================
STEP 9 — CANDIDATE RELATIONSHIPS
==================================================

Below Preview metrics show actual candidates.

Each row/card should include:

Entity A
Entity B
Relationship Type
Shared Connector
Confidence
Evidence Count
Source Lane
Qualification

Actions:

Inspect
Why Detected
Exclude from Preview

If multiple connectors contribute, display the connector count and allow inspection.

==================================================
STEP 10 — WHY DETECTED
==================================================

This must come from actual provenance.

Show:

WHY DETECTED

Relationship Definition
Definition Version

Entity A
Entity B

Detection Family

Shared Connector(s)

Triggered Condition

Required Value

Observed Value

Evidence Records

Evidence IDs

Supporting Relationship IDs

Source Documents

Confidence

Confidence / Quality Components where available

Qualification State

Example:

Definition
Common Guarantor

Entity A
ABC Corp

Entity B
XYZ Corp

Connector
Guarantor Holdings Ltd

Rule
Minimum shared connectors >= 1

Observed
1

Evidence
3 records

Confidence
96%

Qualification
Review / Qualified

Do not reconstruct fake provenance in React.

Use backend evidence/provenance.

==================================================
STEP 11 — SOURCE / EVIDENCE VIEW
==================================================

For a preview candidate allow the analyst to inspect supporting evidence.

Reuse existing evidence display concepts already used by Relationship Explorer.

Show where available:

source lane
source document
source record
relationship record
connector record
evidence ID
evidence quality
origin

Do not expose authentication data.

==================================================
STEP 12 — SAVE DRAFT
==================================================

Connect Save Draft to the existing persisted AI definition/version store.

Do not save only in frontend state.

After saving:

- definition appears in Relationship Definitions
- status is Draft
- version is visible
- reopening it restores the structured configuration

==================================================
STEP 13 — VERSIONING
==================================================

Reuse existing definition-version behavior.

An active version must not be silently overwritten.

Preferred flow:

Active v1
    ↓
Edit
    ↓
Draft v2
    ↓
Preview
    ↓
Review
    ↓
Publish v2

Display:

Version
Status
Created At
Created By / Actor
Change Summary where available

==================================================
STEP 14 — PUBLISH / APPROVE
==================================================

Use the governed workflow already implemented.

The audit says the existing model requires:

- saved version
- review
- explicit analyst approval
- actor identity
- publication

Preserve these requirements.

Do NOT bypass them to make the UI easier.

If actor identity is currently required by the API, provide the appropriate current-user/operator input using the existing application pattern.

Publishing should create governed AI relationship instances using the existing backend.

Publishing must not modify CAM.

==================================================
STEP 15 — RELATIONSHIP INSTANCES
==================================================

Published instances must retain existing provenance.

At minimum preserve:

definition ID
definition version
entity IDs
relationship type
connector information
supporting relationship IDs
evidence IDs
source documents
confidence
quality
origin
publication/audit metadata

Do not create a simplified frontend publication mechanism that loses this information.

==================================================
STEP 16 — RELATIONSHIP RECORDS INTEGRATION
==================================================

Published AI relationship instances already enter the Lending read layer.

Expose them correctly in:

Relationship Explorer
→ Relationship Records

Do not build another separate instance repository.

Users should be able to identify origin:

CAM / Internal
AI Definition
External / Supplemental

Add filtering by Definition if practical.

Opening the record should show its provenance.

==================================================
STEP 17 — NETWORK INTEGRATION
==================================================

Reuse the existing Relationship Network.

Two modes are needed.

A. PREVIEW MODE

From the Preview stage:

Preview in Network

Display temporary candidate edges with:

AI Preview

visual semantics.

These are not persisted.

B. PUBLISHED MODE

Published instances should appear through the existing Lending relationship read layer.

Do not create another graph database.

Do not duplicate graph nodes.

Graph edges must remain inspectable.

==================================================
STEP 18 — REVIEW QUEUE
==================================================

Reuse the existing Review Queue.

Do NOT create another review application.

Where the existing governance requires review, surface AI relationship proposals through the existing review workflow.

Possible presentation:

CAM Review
AI Relationship Proposals
External Proposals
Conflicts

or equivalent filtering within the existing page.

Each AI relationship review item should show:

Entity A
Entity B
Relationship Type
Definition
Definition Version
Confidence
Evidence Count
Primary Evidence
Reason for Review

Actions:

Inspect
Approve
Reject

Approval creates/permits governed supplemental intelligence.

It must NOT write to CAM.

==================================================
STEP 19 — EXTERNAL RESEARCH BOUNDARY
==================================================

Preserve the architecture discovered in the audit.

External research is separate.

Do NOT make the AI relationship-definition module directly call Stylus or web research.

Relationship workflow may indicate that additional external evidence is required.

External Research remains responsible for gathering that evidence.

External findings remain proposal-only until governed review/acceptance.

Do not allow external evidence alone to silently create a published relationship instance.

==================================================
STEP 20 — DO NOT IMPLEMENT SEC CREDENTIAL CHANGES YET
==================================================

Do not modify:

Helix refresh
R2D2 authentication
Stylus token acquisition
Stylus token refresh
Runner Service authentication
SEC provider authentication

in this task.

The audit established that these require separate treatment.

For now preserve their current behavior.

The next implementation phase will handle these integrations.

==================================================
STEP 21 — KEEP THE CURRENT UI
==================================================

Do not redesign:

Overview
Clients
Network
Relationship Explorer
External Research
Review Queue

Use the existing styling and design system.

Do not create:

- a separate AI application
- a chatbot-style screen
- a second Network
- a second Review Queue
- a second evidence explorer

Extend the existing application.

==================================================
STEP 22 — PORTABILITY GUARDRAIL
==================================================

The later target is Unix/Linux deployment.

For all NEW code in this task:

do not introduce:

C:\ paths
PowerShell requirements
cmd.exe requirements
Windows-only path handling
new working-directory assumptions
frontend credentials
new hardcoded localhost business logic

Use existing portable Python/path utilities.

But do not spend this task fixing the broader deployment blockers from the audit.

TOOLS FIRST.

==================================================
STEP 23 — TEST EXISTING BACKEND CAPABILITY FIRST
==================================================

Before UI validation, exercise the actual backend AI workflow directly.

At minimum verify:

create definition
create version
preview definition
approve where required
publish
read published instance
read provenance

Verify higher-order preview for:

Common Guarantor
Common Collateral
Common Ownership / Control
Shared Management

Verify Shared Address safely returns zero when qualifying governed signals do not exist.

Do not insert permanent test data into the live-like store unless required.

Use isolated tests where possible.

==================================================
STEP 24 — FRONTEND TESTS
==================================================

Validate:

Relationship Definitions tab opens

Definitions list loads from backend

AI Create Relationship opens

Natural language description can generate configuration

Generated configuration renders correctly

Configuration can be edited

Save Draft works

Saved Draft reloads

Preview works

Preview returns real candidates

Candidate Inspect works

Why Detected works

Evidence can be inspected

Preview in Network works

Preview edges are temporary

Publish workflow works

Published instances become visible in Relationship Records

Published relationships appear in Network where appropriate

Review-required relationships appear in Review Queue

CAM data remains unchanged

==================================================
STEP 25 — END-TO-END VALIDATION
==================================================

Perform one full live workflow using:

COMMON GUARANTOR

Use this description:

Identify companies that share a common guarantor.
Require at least one qualifying shared guarantor.
Use internal evidence as the primary source.
Relationships that do not qualify for automatic acceptance should require analyst review.

Then perform:

1. Generate Configuration
2. Inspect generated structured definition
3. Save Draft
4. Reopen Draft
5. Preview
6. Record actual preview metrics
7. Inspect an actual candidate
8. Verify actual shared connector
9. Open Why Detected
10. Verify evidence/provenance
11. Preview in Network
12. Confirm graph preview is temporary
13. Complete required analyst approval
14. Publish
15. Confirm versioned instance was created
16. Confirm instance appears in Relationship Records
17. Confirm published edge can appear in Network
18. Confirm review routing where applicable
19. Confirm audit event exists
20. Confirm CAM source payload is unchanged

==================================================
STEP 26 — REGRESSION VALIDATION
==================================================

Run:

all backend tests

the existing AI relationship tests

frontend TypeScript validation

frontend build

frontend tests if configured

diagnostics for modified files

Existing audit information indicated:

56 backend full-suite tests previously passed
5 focused AI tests previously passed
frontend production build previously passed

Do not regress these.

==================================================
FINAL RESPONSE
==================================================

When finished report:

IMPLEMENTED

EXISTING BACKEND CAPABILITIES REUSED

FILES CHANGED

NEW API ROUTES, IF ANY

DEFINITIONS UI

AI CREATE RELATIONSHIP

DRAFT / VERSION WORKFLOW

PREVIEW RESULTS

COMMON GUARANTOR TEST RESULT

COMMON COLLATERAL TEST RESULT

COMMON OWNERSHIP / CONTROL TEST RESULT

SHARED MANAGEMENT TEST RESULT

SHARED ADDRESS RESULT

WHY DETECTED / PROVENANCE

PUBLISH RESULT

RELATIONSHIP EXPLORER INTEGRATION

NETWORK INTEGRATION

REVIEW QUEUE INTEGRATION

AUDIT EVENTS

CAM IMMUTABILITY CHECK

BACKEND TEST RESULTS

FRONTEND BUILD RESULT

KNOWN LIMITATIONS

Do not mark the task complete because components merely compile or render.

Completion requires a real Definition → Preview → Inspect → Approve → Publish → Relationship Record → Network / Review flow using actual source-backed data.

Do not start Unix deployment work.

Do not start SEC / Helix / Stylus credential work.

Focus exclusively on making the relationship tools operate end to end.
