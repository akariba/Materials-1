
Perform a READ-ONLY CURRENT-STATE EXPLAINABILITY AND UI FLOW AUDIT of the Lending Relationship Intelligence application.

DO NOT modify code.
DO NOT redesign the UI yet.
DO NOT change databases, APIs, mappings, relationship logic, extraction rules, or deployment.
DO NOT propose a new architecture yet.

The purpose is to document exactly how the application works TODAY so that we can redesign it safely afterward.

We already completed the relationship-data reconciliation and loss-attribution analysis.

Now inspect the frontend + backend together and answer:

1. What exactly does the user see?
2. Where does each visible value come from?
3. What does each status actually mean?
4. What happens when the user clicks/drills/actions something?
5. Where is explainability currently missing or misleading?
6. How does AI Create Relationship currently work end-to-end?

==================================================
PART 1 — CURRENT SCREEN INVENTORY
==================================================

Inspect all Lending surfaces, including at minimum:

- Overview
- Clients
- Client Detail
- Network
- Relationship Explorer
- Review Queue
- External Research
- AI Create Relationship / governed relationship workflow

For each screen produce a table:

Screen
UI section/component
What the user sees
Frontend component/file
API endpoint called
Backend function
Underlying data/store
Relationship universe used:
  - V3
  - V2 fallback
  - normalized
  - external overlay
  - AI definition/instance
  - mixed
Filters applied
Statuses displayed
User actions available
Navigation/drill-down target

Verify from code. Do not infer.

==================================================
PART 2 — EXPLAINABILITY INVENTORY
==================================================

For every relationship displayed to the user, determine which of the following are currently visible or accessible:

- subject entity
- related entity
- relationship type
- relationship family
- direction
- lifecycle/state
- canonical/review status
- evidence count
- evidence excerpt
- source document
- page/paragraph/source location
- extraction confidence
- quality confidence
- entity-resolution method
- taxonomy mapping/substitution
- rejection/review reason
- source lane
- discovery origin
- V2/V3/normalized provenance
- global API visibility
- external research provenance
- AI-generated vs governed-source relationship
- publication status
- audit/version history

Classify each field:

VISIBLE DIRECTLY
VISIBLE AFTER CLICK
AVAILABLE IN BACKEND BUT NOT UI
NOT STORED
UNKNOWN

This is critical.

==================================================
PART 3 — TRACE REAL RELATIONSHIPS END-TO-END
==================================================

Use several relationships from our benchmark and trace them through the ACTUAL application.

At minimum trace:

1. Lambda -> NVIDIA : supplier
2. Lambda -> NVIDIA : strategic_partner
3. Applied Digital -> CoreWeave : contracted_customer
4. Serverfarm -> Meta : contracted_customer
5. BO Westover -> Blue Owl NLT : guarantor
6. Project Indigo -> CoreWeave : parent_company or guarantor

For every example show:

SOURCE
  ↓
raw/extracted candidate if available
  ↓
entity resolution
  ↓
taxonomy mapping
  ↓
evidence/quality evaluation
  ↓
state/direction
  ↓
canonical/review decision
  ↓
scope/publication
  ↓
API
  ↓
screen(s) where user sees it

At every stage state:

- actual stored value
- actual status
- whether transition evidence exists
- whether the UI exposes it
- whether the user can understand WHY the final result looks the way it does

If a transition was not persisted, write UNKNOWN.
Do not reconstruct a transition from assumptions.

==================================================
PART 4 — USER WORKFLOW
==================================================

Document the current workflow from a user's perspective.

Example:

Portfolio Overview
→ select client
→ Client Detail
→ view relationships
→ open Network
→ inspect relationship
→ open evidence
→ review / approve / reject

Determine whether this workflow actually works today.

For each step state:

- what the user expects
- what actually happens
- what data universe is used
- whether the same relationship ID survives the transition
- whether context is preserved
- whether counts reconcile
- whether the user can reach evidence
- whether the user can understand why something is review-required/rejected/canonical

Highlight dead ends and context switches.

==================================================
PART 5 — REVIEW QUEUE SEMANTICS
==================================================

This needs special attention.

Determine exactly what causes something to appear in Review Queue today.

Compare:

- V3 review-required
- normalized review-required
- normalized rejected
- external proposals/conflicts
- AI-created relationships

Show which are included and excluded.

Explain whether a user looking at Review Queue could reasonably assume it contains ALL relationships requiring human review.

Do not make a product recommendation yet. Just establish the facts.

==================================================
PART 6 — AI CREATE RELATIONSHIP CURRENT FLOW
==================================================

Inspect the AI Create Relationship UI and backend exactly as implemented.

Trace:

Describe
→ Configure
→ Preview
→ Publish

For every stage document:

- user inputs
- AI inputs
- deterministic inputs
- prompt/configuration used
- API call
- generated object/schema
- validation
- preview behavior
- persistence behavior
- publish behavior
- versioning
- audit history
- relationship instances created
- impact on Network / Explorer / Review Queue

Also determine:

- Are AI definitions currently persisted?
- Are versions persisted?
- Are instances persisted?
- Does publishing actually modify anything visible?
- Is CAM immutable?
- What happens when the user leaves the workflow?
- What is the purpose of Save Draft?
- What does Preview Impact actually calculate?
- What does Publish actually do today?

If a Preset/external research configuration is referenced by the application, identify the integration point.
Do not invent external preset behavior if it is outside the repository.

==================================================
PART 7 — COUNT AND SEMANTIC CONSISTENCY
==================================================

For the same client or relationship, compare what is shown on:

Overview
Clients
Client Detail
Network
Relationship Explorer
Review Queue

Identify situations where:

- counts differ
- status labels differ
- relationship types differ
- a relationship is visible on one screen but absent from another
- V2 fallback appears on one screen but not another
- normalized status conflicts with V3 publication state

Give concrete examples.

==================================================
PART 8 — CURRENT EXPLAINABILITY GAPS
==================================================

Do NOT redesign.

Rank the current gaps by severity:

CRITICAL
HIGH
MEDIUM
LOW

Examples of the kind of issues to investigate:

- relationship displayed without source
- review-required without reason
- rejected interpreted as false
- taxonomy substitution invisible
- entity alias invisible
- V2/V3 provenance invisible
- evidence inaccessible
- multiple universes presented as one
- counts with different denominators
- AI-created relationship indistinguishable from CAM-derived relationship
- no relationship history
- no transition/audit trail

Only report a gap when supported by code/data/UI evidence.

==================================================
PART 9 — DELIVERABLE
==================================================

Return:

A. Executive current-state summary

B. Screen → API → Store matrix

C. Current user workflow diagram

D. Relationship lifecycle diagram

E. Explainability-field coverage matrix

F. Review Queue semantics

G. AI Create Relationship current lifecycle

H. Six benchmark relationship traces

I. Cross-screen inconsistencies

J. Ranked explainability gaps

K. Exact files/functions/endpoints responsible

L. A short section titled:

"WHAT MUST BE UNDERSTOOD BEFORE REDESIGN"

Do not implement any fixes.

This task is forensic documentation of the existing product.
