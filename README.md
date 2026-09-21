You have just completed the Lending Relationship Intelligence repository audit.

Use the findings from that audit as context, but DO NOT start the Unix/Linux deployment refactor yet.

The long-term target remains that the application will eventually run as a packaged application on a Unix instance and be accessed through a link.

Therefore, avoid introducing new:

- Windows-only dependencies
- hardcoded local paths
- PowerShell-only business logic
- frontend-held credentials
- development-only architectural assumptions

FOR THIS TASK, HOWEVER, FOCUS ONLY ON MAKING THE RELATIONSHIP INTELLIGENCE TOOLS WORK END TO END IN THE CURRENT ENVIRONMENT.

Do not spend time creating:

- deployment scripts
- systemd services
- Unix installers
- packaging scripts
- reverse proxies
- production hosting configuration

==================================================
PRIMARY OBJECTIVE
==================================================

Implement and fully connect:

RELATIONSHIP DEFINITIONS
+
AI CREATE RELATIONSHIP
+
LIVE PREVIEW
+
RELATIONSHIP INSTANCES
+
RELATIONSHIP EXPLORER
+
NETWORK PREVIEW / DISPLAY
+
REVIEW QUEUE GOVERNANCE

The completed workflow must allow me to:

1. Open Relationship Explorer.
2. Open Relationship Definitions.
3. Create a new definition using AI Create Relationship.
4. Describe the desired relationship in natural language.
5. Have the system generate a structured relationship configuration.
6. Edit the configuration.
7. Preview the configuration against actual application data.
8. See actual candidate relationships.
9. Inspect why each candidate was detected.
10. Save the definition as Draft.
11. Version the definition.
12. Publish or activate the definition.
13. Generate relationship instances from the definition.
14. See those instances in Relationship Explorer.
15. Preview or display them in the existing Network.
16. Route review-required instances into the existing Review Queue.
17. Preserve CAM as authoritative and unchanged.

This must be a real connected workflow.

Do not build static mock screens whose controls are disconnected from the backend.

==================================================
CORE PRODUCT ARCHITECTURE
==================================================

Preserve these three separate concepts.

1. RELATIONSHIP DEFINITION

A reusable governed configuration describing how relationships are detected.

Example:

COMMON_GUARANTOR

Company ↔ Company

Condition:
Both companies share at least one qualifying guarantor.


2. RELATIONSHIP INSTANCE

A concrete detected relationship between actual entities.

Example:

ABC Corp
↔ Common Guarantor ↔
XYZ Corp

Shared connector:
Guarantor Holdings Ltd


3. CORRELATION

A higher-order pattern composed from one or more relationship instances.

Example:

Company A
   |
ownership
   |
Company B
   |
guarantee
   |
Company C

→ Economic Group / Connected Borrower correlation

DO NOT collapse these into one object.

This task focuses primarily on:

Relationship Definition
        ↓
Relationship Instance

==================================================
IMPORTANT GOVERNANCE PRINCIPLE
==================================================

CAM remains authoritative.

AI-created relationship definitions and resulting instances must NOT mutate CAM.

The flow is:

Relationship Definition
        ↓
Detection
        ↓
Candidate Relationship Instances
        ↓
Qualification / Review
        ↓
Supplemental Relationship Intelligence

Do not silently promote relationships into CAM.

==================================================
STEP 1 — INSPECT AND REUSE EXISTING IMPLEMENTATION
==================================================

Before adding new modules, inspect the existing repository for components already created for:

- relationship definitions
- definition versions
- AI relationship configuration
- relationship synthesis
- higher-order synthesis
- common guarantor
- common collateral
- common ownership
- common control
- shared management
- shared address
- relationship preview
- relationship persistence
- relationship instance persistence
- evidence aggregation
- confidence scoring
- review workflow
- network graph
- external relationship lane

Reuse existing implementation whenever possible.

Do NOT create parallel duplicate services if equivalent functionality already exists.

Specifically determine whether existing backend capabilities already support:

- definition CRUD
- definition versions
- preview
- publish
- higher-order synthesis
- evidence aggregation
- confidence calculation
- instance generation

If something already exists, connect the UI to it rather than rewriting it.

Before coding, briefly identify:

EXISTING COMPONENT
CURRENT PURPOSE
CAN REUSE?
REQUIRED CHANGE

Then proceed with implementation.

==================================================
STEP 2 — RELATIONSHIP EXPLORER NAVIGATION
==================================================

Do NOT add another main navigation item.

Relationship Definitions belongs inside the existing Relationship Explorer.

At the top of Relationship Explorer add two subviews:

[ Relationship Records ]   [ Relationship Definitions ]

Default:

Relationship Records

Relationship Records continues showing actual relationship instances.

Relationship Definitions manages reusable detection configurations.

Do not break existing Relationship Explorer behavior.

==================================================
STEP 3 — RELATIONSHIP DEFINITIONS LIBRARY
==================================================

Build the Relationship Definitions view.

Header:

Relationship Definitions

Primary action:

+ Create Relationship

Clicking it should provide:

AI Create Relationship
Use Template
Create Manually

AI Create Relationship should be the primary option.

Add summary metrics such as:

ACTIVE DEFINITIONS
DRAFT DEFINITIONS
TESTING
PENDING REVIEW
AI ASSISTED

Use actual backend values.

Do not hardcode fake counts.

Main table should support columns similar to:

Relationship
Category
Source Entity
Target Entity
Detection Method
Source Lane
Confidence Threshold
Generated Instances
Creation Method
Version
Status
Last Tested
Last Updated

Statuses:

Draft
Testing
Pending Approval
Active
Paused
Archived

Creation method:

System
Manual
AI Assisted

==================================================
STEP 4 — AI CREATE RELATIONSHIP WORKSPACE
==================================================

AI Create Relationship must open as an integrated workspace.

Prefer:

- large right-side drawer

or

- large in-context panel

Do not build a separate chatbot page.

Header:

AI Create Relationship

Under the header show:

CAM remains authoritative.
AI relationship definitions create supplemental,
evidence-backed relationship intelligence only.

Use four stages:

Describe
Configure
Preview
Publish

The stages must have real application state and navigation.

The user must be able to move backward without losing the current configuration.

==================================================
STEP 5 — DESCRIBE
==================================================

Provide a large natural-language field:

Describe the relationship you want the system to identify

Example:

Identify companies that share a common guarantor.
Use internal guarantee records first.
Allow SEC evidence as supporting evidence.
Require at least one qualifying shared guarantor.

Suggested starting points:

Common Guarantor
Common Collateral
Common Ownership / Control
Shared Management
Shared Address
Parent / Subsidiary
Economic Group

Primary action:

Generate Configuration

The output must become a structured configuration.

Do NOT simply save the natural-language prompt.

==================================================
STEP 6 — STRUCTURED CONFIGURATION
==================================================

The generated configuration should contain structured sections.

A. RELATIONSHIP DEFINITION

Fields:

Name
Code
Description
Category
Relationship Type
Direction
Strength Method

Example:

Name:
Common Guarantor

Code:
COMMON_GUARANTOR

Category:
Credit Support

Direction:
Bidirectional


B. ENTITIES

Source Entity
Target Entity

Examples:

Company ↔ Company
Borrower → Guarantor
Loan → Collateral
Company → Parent Company

Reuse the existing Lending Relationship Intelligence entity model.

Do not create another duplicate taxonomy unless necessary.


C. DETECTION LOGIC

Implement a readable structured rule builder.

Support:

ALL
ANY
NONE

Support nested AND / OR where the backend supports it.

Example:

ANY

Shared qualifying guarantor >= 1

OR

Explicit guarantee relationship supported by authoritative evidence

For connector-based relationships support fields such as:

Connector Type
Minimum Shared Connectors
Maximum Connector Group Size
Minimum Connector Confidence
Connector Status
Connector Recency

Maximum Connector Group Size is important.

For example:

If one registered address, agent, guarantor, service provider, or other connector links hundreds of entities, the definition must be able to prevent meaningless mass relationships.

==================================================
STEP 7 — RELATIONSHIP TYPES
==================================================

Expose existing supported relationship synthesis rather than implementing arbitrary new types.

Prioritize:

1. Common Guarantor
2. Common Collateral Provider
3. Common Ownership / Control
4. Shared Management
5. Shared Address
6. Parent / Subsidiary where evidence exists

Shared Address must only produce relationships if governed address signals actually exist.

Do not fabricate shared-address results.

If current data contains no governed shared-address signals, preview should correctly return zero.

Zero valid results is a legitimate result, not an application error.

==================================================
STEP 8 — EVIDENCE CONFIGURATION
==================================================

Add an Evidence section.

Support fields such as:

Minimum Evidence Records
Minimum Independent Sources
Require Source Document
Require Supporting Entity ID
Require Connector ID
Minimum Evidence Quality

Distinguish visibly between:

Deterministic Rule

and

AI Inference

An AI-inferred relationship must remain explainable.

Evidence generated for a relationship must retain provenance.

Where available retain:

source system
source document
source record ID
entity ID
connector ID
retrieval timestamp
evidence timestamp
evidence type
evidence quality

==================================================
STEP 9 — SOURCE GOVERNANCE
==================================================

Reuse the source concepts already established in the application.

Support source priorities such as:

CAM / Internal Data                Primary
SEC Regulatory Filings            Primary External
Corporate Filings                 Supporting
Corporate Website                 Supporting
Trusted Public Web                Supporting
Unverified Web                    Excluded

Do not hardcode specific websites unnecessarily.

Use governed source categories where the architecture supports them.

IMPORTANT:

Do not implement the new Helix/Stylus refresh architecture in this task.

SEC integration will be handled in the next task.

For now:

- preserve existing SEC behavior
- preserve existing external research behavior
- preserve existing source controls
- do not break current SEC execution

==================================================
STEP 10 — CONFIDENCE AND QUALIFICATION
==================================================

Add configurable confidence rules.

Example:

95–100    Auto Qualified
85–94     Review Required
Below 85  Reject

These values must be editable/configurable.

Do not hardcode the example thresholds as universal business rules.

Support at minimum:

Minimum Confidence
Auto-Qualify Threshold
Review Threshold
Reject Threshold

Validate that thresholds are logically consistent.

For example:

Auto-Qualify Threshold must not be below Review Threshold.

==================================================
STEP 11 — APPROVAL MODE
==================================================

Provide:

Creation / Approval Mode

Options:

Automatically Qualify
Send for Review
Suggest Only

For newly AI-created definitions, default to:

Send for Review

Do not default to automatically publishing inferred relationships.

==================================================
STEP 12 — TEMPORAL SETTINGS
==================================================

Where supported, expose:

Current Only
Historical
Current + Historical

Also support where actual backend capability exists:

Effective Date Source
Expiration / Revalidation
Revalidation Frequency

Do not invent historical capability if the backend cannot support it.

If temporal functionality does not yet exist:

- show it as unavailable
- disable it clearly
- or omit it

Do not create UI controls that appear functional but are disconnected.

==================================================
STEP 13 — NETWORK BEHAVIOR
==================================================

Definition configuration should include:

Show on Network
Edge Label
Edge Weight
Direction
Relationship Priority
Maximum Traversal Depth
Allow Relationship Chaining

Reuse the existing Network graph.

Do not build a second graph component.

Do not create another graph persistence model.

==================================================
STEP 14 — PREVIEW
==================================================

This is critical.

The Preview stage must execute the actual relationship detection logic against actual application data.

Do not show mock metrics.

Surface real backend metrics such as:

Candidate Source Records
Shared Connectors
Synthesized Relationship Pairs
High Confidence
Review Required
Rejected

If the existing backend reports values such as:

116 candidate records
22 shared connectors
26 synthesized pairs

show those actual values.

Preview must NOT:

- publish the definition
- modify CAM
- permanently publish instances
- alter review state
- leave persistent graph edges unless explicitly saved later

==================================================
STEP 15 — PREVIEW CANDIDATES
==================================================

Show actual candidate relationships.

Each candidate should show:

Entity A
Entity B
Relationship Type
Connector(s)
Confidence
Evidence Count
Source Lane
Qualification State

Actions:

Inspect
Why Detected?
Exclude

Use actual entities from current source data.

Do not generate placeholder companies.

==================================================
STEP 16 — WHY DETECTED
==================================================

Implement explainability for each candidate.

Example:

WHY THIS RELATIONSHIP WAS DETECTED

Definition:
Common Guarantor

Company A:
ABC Corp

Company B:
XYZ Corp

Shared Connector:
Guarantor Holdings Ltd

Triggered Rule:
Minimum shared connectors >= 1

Observed:
1

Evidence Records:
3

Sources:
Internal Guarantee Data
SEC Filing

Confidence:
96%

Required Confidence:
85%

Qualification:
PASSED

Where possible, show:

rule ID
source records
connector IDs
evidence IDs
confidence components

Do not expose sensitive authentication material.

The explanation should come from actual detection provenance.

Do not reconstruct a fake explanation in the frontend if the backend has the real provenance.

==================================================
STEP 17 — EXCLUSION / FEEDBACK
==================================================

If the user excludes a preview candidate, allow a reason such as:

Incorrect Entity Match
Connector Not Meaningful
Outdated Relationship
Insufficient Evidence
False Positive
Other

Do not automatically rewrite the definition.

Optionally offer:

Suggest Configuration Change

Example:

This candidate was rejected because the connector is shared by many unrelated entities.

Suggested rule:

Maximum Connector Group Size = 20

Buttons:

Apply Suggestion
Dismiss

The user remains in control.

If Apply Suggestion is selected:

update the draft configuration

do not immediately publish it

and require preview to be rerun.

==================================================
STEP 18 — PREVIEW IN NETWORK
==================================================

Add:

Preview in Network

Reuse the existing Relationship Network.

Introduce a temporary visual state/lane:

AI Preview

AI Preview relationships must be visually distinguishable from:

CAM Canonical
CAM Review
External Supplemental
Published AI / Supplemental Relationships

Do not persist AI Preview graph edges as published instances.

Closing or leaving preview should not leave phantom graph state.

The graph must continue to allow opening the existing relationship inspector.

==================================================
STEP 19 — SAVE DRAFT
==================================================

Allow:

Save Draft

Draft must persist using the existing definition persistence mechanism.

Draft should appear in Relationship Definitions with:

Status = Draft

Do not silently save a draft only into React/browser state.

==================================================
STEP 20 — VERSIONING
==================================================

Material changes should create or support a version.

Example:

COMMON_GUARANTOR

v1
minimum connectors = 1

v2
minimum connectors = 1
maximum connector group size = 20

Store where supported:

Version
Created By
Created At
Change Summary
Status

Do not silently overwrite an active published definition when materially changed.

Prefer:

Active Version
        ↓
Create New Draft Version
        ↓
Preview
        ↓
Publish New Version

==================================================
STEP 21 — PUBLISH
==================================================

Publish should operate on a Definition Version.

Before publish show a summary:

Relationship
Entities
Detection Logic
Evidence Requirements
Sources
Confidence
Approval Mode
Network Behavior

Actions:

Publish
Save Draft
Return to Preview

Publishing must NOT mutate CAM.

Publishing means:

this relationship definition/version is approved for use by the supplemental relationship-intelligence engine.

==================================================
STEP 22 — RELATIONSHIP INSTANCE GENERATION
==================================================

After publication/activation, the definition must be able to generate actual Relationship Instances.

Instances should retain linkage back to:

definition_id
definition_version
detection timestamp
source evidence
connector IDs
confidence
qualification state

Also retain where supported:

source lane
review state
effective date
relationship strength
evidence IDs

Do not store only a pair of entity IDs without provenance.

==================================================
STEP 23 — RELATIONSHIP EXPLORER INTEGRATION
==================================================

Generated instances must appear in:

Relationship Explorer
→ Relationship Records

Users should be able to filter by:

Relationship Type
Definition
Source Lane
State
Confidence
Review Status

Opening an instance should show:

Entities
Relationship Type
Definition
Version
Evidence
Sources
Connector(s)
Confidence
Why Detected
Review Status

Do not create a disconnected second relationship-record screen.

==================================================
STEP 24 — NETWORK INTEGRATION
==================================================

Qualified/published relationship instances should be displayable in the existing Network.

Reuse current graph entities and edge rendering.

Do not create duplicate graph data stores.

Each graph edge should retain enough information to open its relationship inspector.

Preserve source-lane visual distinctions.

The user should be able to understand whether an edge is:

CAM canonical
CAM review
External supplemental
AI/supplemental
AI preview

without examining backend data.

==================================================
STEP 25 — REVIEW QUEUE INTEGRATION
==================================================

Do not create another approval application.

Use the existing Review Queue.

Add support/filter/tab for:

AI Relationship Proposals

or integrate into the existing supplemental proposal queue if that is cleaner architecturally.

Review-required instances should contain:

Entity A
Entity B
Relationship Type
Definition
Confidence
Evidence Count
Primary Source
Reason for Review

Actions should use existing review patterns:

Inspect
Approve
Reject

Approval means:

approved supplemental relationship intelligence.

It does NOT mean:

write into CAM.

==================================================
STEP 26 — EXTERNAL RESEARCH BOUNDARY
==================================================

Do not duplicate External Research in the definition builder.

A Relationship Definition may declare:

External Research Allowed = Yes

But actual external research remains owned by the existing External Research service/page.

Conceptually:

Definition
   ↓
Internal Detection
   ↓
Evidence Insufficient
   ↓
External Research
   ↓
Evidence
   ↓
Relationship Candidate
   ↓
Review

Do not let relationship-definition code directly implement SEC/web retrieval.

Maintain a service boundary.

This separation is important for the later Unix-hosted architecture.

==================================================
STEP 27 — API CONTRACTS
==================================================

Use existing API conventions.

If missing, implement clean endpoints for concepts such as:

list definitions
get definition
create definition
update draft
create version
preview definition
publish definition
list instances for definition
explain instance

Do not invent duplicate endpoints if equivalents already exist.

Return typed, stable response models.

Preview responses should include:

real metrics
actual candidate results
qualification state
evidence/provenance references

==================================================
STEP 28 — ERROR HANDLING
==================================================

Handle at minimum:

Invalid entity type
Invalid rule
Unsupported relationship family
No source data
No candidates found
Preview failure
Persistence failure
Definition version conflict
Publish failure
Instance generation failure

Show clear business-readable UI errors.

Do not expose raw stack traces in React.

"No candidates found" is a valid preview result, not necessarily an error.

==================================================
STEP 29 — EMPTY STATES
==================================================

Relationship Definitions empty state:

Create relationship intelligence for your lending network.

Actions:

AI Create Relationship
Use Template
Create Manually

Preview with no candidates should show:

No relationships matched the current definition.

Do not present this as a system failure.

==================================================
STEP 30 — DO NOT REDESIGN EXISTING PRODUCT
==================================================

Preserve the current visual language.

The application already contains:

Overview
Clients
Network
Relationship Explorer
External Research
Review Queue

Extend it.

Do not replace it.

Do not introduce a new design system.

Do not convert the interface into a chatbot.

AI should behave as an embedded configuration assistant.

==================================================
STEP 31 — PORTABILITY GUARDRAIL
==================================================

Remember the future deployment target is Unix/Linux.

For new code added in this task:

Use pathlib or existing portable path utilities.

Do not add:

C:\ paths
PowerShell requirements
cmd.exe requirements
Windows-only filesystem assumptions
frontend-held secrets
localhost dependencies in business logic

But DO NOT perform the broader Unix migration in this task.

The priority remains making the tools work end to end now.

==================================================
STEP 32 — TESTS
==================================================

Add or extend backend tests for:

create definition
save draft
read definition
create new version

preview common guarantor
preview common collateral
preview common ownership/control
preview shared management

shared address with no governed data returns zero correctly

preview does not publish
preview does not mutate CAM

publish definition

generate relationship instances

instance links to definition/version

review-required instance routed correctly

published instance appears in relationship records

explain / why detected returns evidence and triggered logic

definition persistence survives service reload if the current persistence design supports it

Add frontend tests for:

Definitions tab
Create Relationship menu
AI Create workspace
Describe
Generate Configuration
Configure
Preview
Why Detected
Save Draft
Publish
Preview in Network
Review routing
empty states
error states

==================================================
STEP 33 — END-TO-END VALIDATION
==================================================

Run an actual end-to-end workflow.

Use one supported relationship type, preferably:

Common Guarantor

Scenario:

1. Open Relationship Explorer.
2. Open Relationship Definitions.
3. Click Create Relationship.
4. Choose AI Create Relationship.
5. Enter:

   Identify companies that share a common guarantor.
   Require at least one qualifying shared guarantor.
   Use internal evidence as the primary source.
   Send relationships below the auto-qualification threshold for review.

6. Generate structured configuration.
7. Confirm generated configuration contains actual structured fields.
8. Preview against actual data.
9. Confirm real candidate metrics.
10. Inspect at least one actual candidate.
11. Open Why Detected.
12. Confirm provenance and triggered rule are real.
13. Preview it in Network.
14. Confirm preview edge is temporary.
15. Save Draft.
16. Confirm draft appears in Relationship Definitions.
17. Publish/activate according to existing governance.
18. Generate relationship instances.
19. Confirm instance appears in Relationship Records.
20. Confirm applicable instance appears in Network.
21. Confirm review-required instance appears in Review Queue.
22. Confirm CAM was not modified.

Also validate the other existing relationship families at API/service level.

==================================================
STEP 34 — RUN EXISTING QUALITY CHECKS
==================================================

Run:

all backend tests
frontend TypeScript check
frontend tests if present
frontend production build
existing diagnostics

Do not leave temporary test definitions in the live production-like store unless deliberately created as part of validated application state.

Clean up temporary test artifacts.

Do not delete existing legitimate definitions or relationship data.

==================================================
FINAL REPORT
==================================================

After implementation provide a concise but complete report with:

IMPLEMENTED

EXISTING COMPONENTS REUSED

FILES CHANGED

DATABASE / PERSISTENCE CHANGES

API ENDPOINTS USED / ADDED

RELATIONSHIP TYPES VERIFIED

AI CREATE RELATIONSHIP FLOW

PREVIEW RESULTS

RELATIONSHIP INSTANCE FLOW

NETWORK INTEGRATION

REVIEW QUEUE INTEGRATION

CAM IMMUTABILITY VALIDATION

TEST RESULTS

MANUAL END-TO-END VALIDATION

KNOWN LIMITATIONS

NEXT RECOMMENDED STEP

Do not mark the task complete merely because the UI renders.

The task is complete only when the workflow is connected end to end using real backend data and actual relationship detection.

Do not spend time on Unix deployment infrastructure in this task.

The next implementation phase after this one will focus on making SEC execution operational end to end, including Helix/Stylus readiness, manual refresh control, automatic credential preflight, and evidence integration.
