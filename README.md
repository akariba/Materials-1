CCR RELATIONSHIP PILOT — OUTCOME SEMANTICS AND POSITIVE-CONTROL READINESS

Work only in the CURRENT CCR repository.

Read first:

backend/data/CCR_3M_RELATIONSHIP_PILOT_REPORT.md

Also inspect the code, schemas, enums, tests, research-run records,
candidate-claim records, provider audit records, and relationship proposal
logic used by the bounded 3M relationship pilot.

This is a focused remediation and readiness task.

Do NOT start portfolio-scale discovery.
Do NOT run a broad CCR crawl.
Do NOT modify Lending.
Do NOT weaken evidence requirements.
Do NOT create synthetic relationships.
Do NOT convert rejected claims into accepted relationships.
Do NOT use AI/Helix to manufacture evidence.
Do NOT mutate existing Phase-2 protected source assets.
Do NOT redesign the frontend.

OBJECTIVE

Use the completed 3M pilot as a negative-control benchmark and correct any
semantic ambiguity revealed by that pilot before running a positive-control
relationship benchmark.

The 3M pilot must remain a PASS and its substantive decisions must remain
unchanged:

- no parent relationship was established;
- unnamed upstream suppliers did not create governed entities or relationships;
- NEOGEN identity resolution did not by itself establish a customer relationship;
- no weak relationship was forced;
- no synthetic edge was created.

==================================================
1. RECONSTRUCT THE THREE PILOT DECISIONS
==================================================

Trace each 3M research question from:

research question
→ provider strategy
→ provider response
→ evidence
→ candidate claim
→ entity resolution
→ relationship-semantic evaluation
→ governed outcome
→ persistence decision.

Produce an exact trace for:

A. parent / ultimate parent
B. supplier / critical supplier / source of inputs
C. customer / key customer / strategic partner

Do not infer fields that are not persisted.

==================================================
2. AUDIT OUTCOME SEMANTICS
==================================================

Determine whether the current outcome/status vocabulary correctly distinguishes:

- provider returned no record;
- related entity not identified;
- entity identified but identity resolution failed;
- entity resolved successfully but relationship was not established;
- relationship type unsupported by evidence;
- relationship direction unresolved;
- insufficient evidence;
- conflicting evidence;
- relationship proposal pending review;
- confirmed relationship.

In particular inspect the 3M / NEOGEN trace.

If NEOGEN was successfully identity-resolved, do not classify the failure
as ENTITY/IDENTITY_UNRESOLVED merely because the proposed customer
relationship or direction was not proven.

Inspect the apparent reporting distinction between:

- rejected/insufficient candidate claims = 2

and

- insufficient-evidence governed outcome count = 0.

Determine whether this is intentional and correctly modeled or whether the
vocabulary/report aggregation is conflating claim disposition with research-run
outcome.

==================================================
3. DEFINE THE GOVERNED FAILURE TAXONOMY
==================================================

Reuse existing statuses/enums where they already express the required meaning.

Do NOT create duplicate concepts.

Only if required, minimally extend the governed vocabulary so the system can
distinguish concepts such as:

NOT_FOUND
ENTITY_UNRESOLVED
RELATIONSHIP_NOT_ESTABLISHED
DIRECTION_UNRESOLVED
INSUFFICIENT_RELATIONSHIP_EVIDENCE
CONFLICT_REVIEW_REQUIRED
PROPOSAL_PENDING_REVIEW
CONFIRMED

Names may differ if the repository already has canonical equivalents.

Document exact meaning and allowed lifecycle transitions for each status.

Do not collapse:

entity identity quality
relationship evidence quality
relationship direction
provider status
candidate-claim disposition
proposal state
relationship confirmation

into one field.

==================================================
4. PRESERVE 3M DECISIONS
==================================================

After any semantic remediation, replay/rebuild the bounded 3M pilot from the
same persisted inputs.

Expected substantive result remains:

Parent:
- no governed parent relationship created.

Supplier/source of inputs:
- source evidence exists;
- no individual supplier endpoint established;
- no supplier relationship created.

NEOGEN:
- preserve successful identity resolution if it exists;
- do not establish CUSTOMER / KEY_CUSTOMER unless the evidence actually proves it;
- represent the failure reason accurately.

Expected aggregate result:

- accepted relationships: 0
- confirmed relationships: 0
- synthetic edges: 0
- AI evidence: 0
- production relationship mutation: 0

The semantic labels may become more precise, but the evidence decision must not
be weakened.

==================================================
5. BUILD POSITIVE-CONTROL SELECTION LOGIC
==================================================

Do NOT yet run broad discovery.

Identify 3–5 candidate positive-control relationship cases already supported by
existing CCR repository evidence or already-persisted admissible provider data.

A positive-control case must have:

- a validated CCR subject identity;
- an explicit related legal entity;
- admissible source evidence;
- an explicit relationship statement;
- sufficient relationship type evidence;
- sufficient direction evidence where direction is required;
- deterministic entity resolution;
- no need to infer the relationship from weak contextual language.

Prefer cases exercising different relationship families, for example:

- parent / subsidiary;
- guarantor / guarantee;
- explicitly named supplier;
- explicitly named customer;
- financing/lender;
- ownership/control.

Do not select a case merely because an old candidate row exists.

Verify the underlying evidence first.

For each candidate provide:

- subject;
- related entity;
- expected relationship type;
- expected direction;
- source;
- exact evidence basis;
- identity basis;
- why it qualifies as a positive control;
- which provider path would be exercised.

Rank them by benchmark usefulness, not by commercial importance.

==================================================
6. PROVIDER STRATEGY READINESS
==================================================

For the selected positive-control candidates, identify which existing provider
strategies are sufficient:

- existing SEC cache;
- additional official SEC retrieval;
- GLEIF Level 1;
- GLEIF Level 2;
- existing governed web adapter;
- other already-governed source.

Do NOT execute broad web search in this task.

Do NOT enable Stylus, Helix, or generic AI unless already part of an explicitly
governed test path.

Document where the current strategy has deterministic fallback capability and
where it does not.

==================================================
7. TESTS
==================================================

Add or update focused regression tests covering at least:

- provider NOT_FOUND is not entity unresolved;
- unnamed related entity cannot create a relationship;
- successfully resolved entity can still fail relationship proof;
- unresolved direction cannot silently become directed;
- rejected candidate claim cannot become confirmed relationship;
- accepted relationship requires admissible evidence;
- synthetic edge count remains zero unless an explicitly governed synthetic
  mechanism exists;
- 3M negative-control decisions remain unchanged.

All existing Phase-2 immutability/integrity tests must continue to pass.

==================================================
8. REPORT
==================================================

Create:

backend/data/CCR_RELATIONSHIP_PILOT_SEMANTICS_REPORT.md

Include:

1. 3M trace reconstruction
2. semantic problems found
3. exact remediation performed
4. schema/enums/status changes, if any
5. before/after 3M outcome representation
6. evidence-decision invariance confirmation
7. positive-control candidate table
8. recommended first positive-control case
9. provider strategy for that case
10. tests and validation
11. protected-asset integrity results
12. exact next-step command/prompt boundary

The report must explicitly answer:

- Was NEOGEN identity actually resolved?
- If yes, why did the relationship fail?
- Are candidate-claim disposition and research-run outcome currently distinct?
- Can the engine distinguish “entity unresolved” from “relationship not proven”?
- Which positive-control case should be executed next and why?
- Can that case be executed without broad web/AI discovery?

STOP after the report and focused remediation.

Do NOT run the positive-control pilot yet.

End with exactly:

READY FOR CCR POSITIVE-CONTROL RELATIONSHIP PILOT
