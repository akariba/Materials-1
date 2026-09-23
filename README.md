PROMPT 4B — LENDING PORTFOLIO + CLIENT EXPERIENCE REFINEMENT

Continue from the completed Prompt 4A implementation and its authoritative report:

backend/data/LENDING_PROMPT4A_EXECUTIVE_HOME_REPORT.md

The Common Operating Contract remains in force. Do NOT reinterpret, replace, or relax it.

Prompt 4A is complete.
Do NOT redo Prompt 4A.
Do NOT start Prompt 4C or later work.

OBJECTIVE

Productize the Portfolio and Client Detail journeys for senior lending users while preserving the trusted Lending authority model established in Prompts 1–4A.

The intended user journey is:

HOME
→ PORTFOLIO
→ CLIENT DETAIL
→ NETWORK
→ RELATIONSHIPS
→ INTELLIGENCE
→ REVIEW

Prompt 4B owns only:

1. Portfolio experience refinement.
2. Client population/navigation refinement.
3. Client Detail experience refinement.
4. Deterministic exposure/CAM/relationship-context handoffs from these screens.
5. Senior-user visual hierarchy, explainability, loading/error/empty states, and bounded performance.

Do NOT implement Network redesign.
Do NOT implement graph interactions beyond existing navigation.
Do NOT redesign Relationship Explorer.
Do NOT redesign governed Intelligence/AI authoring.
Do NOT redesign External Research.
Do NOT redesign Review.
Do NOT change CAM/V3 authority.
Do NOT introduce a new relationship store.
Do NOT create inferred risk scores or unsupported credit conclusions.

AUTHORITY

Preserve exactly:

- CAM/V3 is authoritative for the Lending CAM relationship layer.
- V2 is client-specific fallback/history only.
- Normalized workbench remains a separate governed projection.
- External research remains supplemental.
- Governed AI remains a separate governed lane.
- Portfolio analytics remains read-only.
- Reported OSUC remains source-reported/supplemental according to the existing API contract.
- CAM coverage means the deterministic source-population CAM measure already defined by the backend; it must not be relabeled as document freshness.
- Relationship review status is not a credit-risk rating.
- No unsupported materiality thresholds may be invented.

DATA BOUNDARY

Use existing deterministic Lending portfolio APIs wherever possible.

Do not load the 32,957-row normalized relationship history in Portfolio or Client Detail.

Do not invoke:

- AI generation endpoints,
- AI authoring endpoints,
- external research execution,
- provider calls,
- external proposal creation,
- the unbounded unified relationship assertion read,

during ordinary Portfolio or Client Detail loading.

Existing deeper workflows may retain those capabilities when explicitly opened by the user.

PART A — PORTFOLIO EXPERIENCE

Refine /lending/clients into a senior-user portfolio workspace.

The page should immediately answer:

1. Which clients matter most by reported exposure?
2. Which large exposures have CAM coverage?
3. Which large exposures have no CAM coverage?
4. Which clients have relationship records requiring review?
5. Where are concentration patterns visible?
6. Which clients deserve investigation next?
7. Why is each item being surfaced?

Preserve deterministic ranking by the backend/reporting contract.

Improve the visual hierarchy so that the page contains, at minimum:

A. Portfolio command/header area
- Portfolio population count.
- Portfolio reported OSUC context.
- CAM coverage context.
- Current deterministic filters.
- Clear CAM/V3 authority messaging.
- Search by client name or CAGID.
- No excessive technical wording in the primary view.

B. Executive attention strip
Surface bounded, deterministic attention views such as:

- Largest exposures.
- Largest uncovered exposures.
- Largest exposures with review-required relationship records.
- Clients with CAM coverage.
- Clients without CAM coverage.

These are navigation/attention aids, not risk rankings.

Do not create a composite score.

C. Client population
Provide an efficient, visually strong, sortable/filterable client population.

At minimum retain or support:

- Client / CAGID
- Reported OSUC
- Portfolio share
- CAM count / CAM coverage state
- Sector
- Country
- Risk rating if already supplied by the source
- Credit classification if already supplied by the source
- Relationship coverage
- Review-required count

Do not fabricate missing values.

Use explicit Unknown / Not available semantics where appropriate.

D. Filters
Retain and improve deterministic filtering for relevant existing dimensions, including where available:

- Search
- Sector
- Country
- CAM yes/no
- CAM count
- Risk rating
- Credit classification
- Relationship coverage
- Reported OSUC sorting

Filters must remain deterministic and must not invoke AI.

E. Investigation handoffs
Rows/cards should support clear navigation to:

- Client Detail
- Relevant relationship context where appropriate
- Review when review-required records exist

Do not perform mutations from Portfolio.

PART B — CLIENT DETAIL

Refine /lending/client/{cagid} into a strong lending-client intelligence page.

The page must preserve the client-specific deterministic contract and should answer:

1. Who is this client?
2. What is our reported exposure?
3. What share of the portfolio does it represent?
4. What CAM coverage exists?
5. What trusted relationships exist?
6. What requires review?
7. What relationship/network context is available?
8. What evidence or external investigation can the user deliberately open next?

Build a clear senior-user hierarchy.

At minimum include:

A. Client identity header
- Legal/display name from source.
- CAGID.
- Sector.
- Country.
- Existing source classifications.
- CAM coverage badge/count.
- Explicit authority/source semantics.

B. Exposure summary
- Reported OSUC.
- Portfolio share/rank where available.
- CAM count.
- Relationship counts.
- Review-required count.

Do not create inferred materiality labels unless supported by existing deterministic data.

C. Relationship snapshot
Use the bounded client relationship read already defined by the Lending contract.

Show compact grouped relationship context by useful deterministic dimensions such as:

- endpoint pair,
- relationship type,
- state,
- direction,
- connectivity,
- authority/source lane,
- review status.

Do not silently merge CAM, external, normalized, and AI rows into one authority class.

D. Explainability
For relationship/context cards provide a compact:

“Why am I seeing this?”

It should use actual available fields such as:

- authoritative source lane,
- relationship type,
- state,
- direction,
- evidence count,
- source count where available,
- review status,
- inclusion rule / projection boundary.

Do not create unsupported narrative conclusions.

E. Investigation actions
Provide deliberate handoffs such as:

- Open Network
- Open Relationships
- Open Review when applicable
- Research relationship
- Open governed Intelligence/Assist where appropriate

These buttons navigate to the relevant governed workflow.

They must NOT automatically invoke AI generation or external research.

PART C — VISUAL DESIGN

Continue the light executive visual language established in Prompt 4A.

Target:

- professional institutional-credit application,
- light background,
- strong whitespace,
- restrained color,
- sharp typography,
- clear hierarchy,
- sophisticated but not decorative,
- highly readable on a large desktop monitor,
- responsive at narrower widths.

Improve interaction quality with:

- clear hover states,
- selected-row states,
- concise badges,
- purposeful tooltips,
- smooth deterministic transitions where useful,
- loading skeletons,
- strong empty states,
- recoverable error states.

Do not add visual effects that imply analytical meaning not present in the data.

Reserve stronger attention styling for genuine deterministic conditions such as:

- review required,
- missing CAM coverage,
- supplemental/external lane,
- unavailable/unknown data.

PART D — PERFORMANCE

Portfolio and Client Detail must remain bounded.

Do not load the full normalized history.

Prefer:

- paginated portfolio client reads,
- bounded client relationship reads,
- cached existing deterministic portfolio summaries where already available.

Do not fix the large unified semantic-group endpoint as part of Prompt 4B unless a minimal change is strictly required to prevent Portfolio/Client Detail from calling it.

If encountered, document it for Prompt 4C/later.

PART E — EMPTY, UNKNOWN, AND FAILURE STATES

Senior users must never face an unexplained blank panel.

Implement explicit states for:

- no relationships,
- no CAM coverage,
- no review items,
- unknown/supplemental OSUC semantics,
- unavailable relationship data,
- API/read failure,
- incomplete source fields.

Always distinguish:

- zero,
- unknown,
- unavailable,
- not applicable,
- filtered out.

Do not convert these into one generic “0”.

PART F — VALIDATION

Before declaring completion:

1. Run frontend build.
2. Run scoped lint.
3. Check changed-file diagnostics.
4. Smoke-test:
   - /lending/clients
   - at least one client with CAM relationships
   - at least one client without relationships
   - at least one client with review-required relationships
5. Confirm Portfolio and Client Detail ordinary loading do not invoke:
   - AI generation,
   - external research execution,
   - provider calls,
   - external proposal creation,
   - unbounded normalized relationship reads.
6. Confirm CAM/V3 authority language remains intact.
7. Confirm existing Home, Network, Relationships, Intelligence, Review, and External Research routes still resolve.
8. Confirm no CCR/customer-master work was introduced.

PART G — REPORT

Create:

backend/data/LENDING_PROMPT4B_PORTFOLIO_CLIENT_REPORT.md

The report must document:

- files changed,
- Portfolio UX implemented,
- Client Detail UX implemented,
- APIs used,
- authority semantics,
- empty/unknown states,
- performance decisions,
- screenshots/routes manually inspected if available,
- build/lint/diagnostic results,
- remaining items intentionally deferred to Prompt 4C+.

End the report with exactly:

READY FOR PROMPT 4C

STOP after Prompt 4B.

Do not begin Network redesign or any Prompt 4C work.
