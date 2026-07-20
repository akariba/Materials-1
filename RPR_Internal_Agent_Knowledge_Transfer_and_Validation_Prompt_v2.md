# Rapid Portfolio Review (RPR)
## Internal Agent Knowledge Transfer, Alignment Audit, Upload/Deployment Guide, and Implementation Prompt

**Purpose:** Give an internal coding/architecture agent enough business and technical context to verify the existing RPR MVP against the project walkthrough, challenge prior-agent assumptions, validate the exact prompt and upload sequence, test the full workflow, and propose or implement the next safe changes.

**Classification note:** Internal-use knowledge-transfer draft. Do not place credentials, client secrets, certificate contents, internal hostnames, service-account identifiers, raw CAMs, or confidential client data in prompts, logs, source control, screenshots, or generated reports.

---

# 1. Executive Summary

The **AI-Assisted Rapid Portfolio Review (RPR)** project is an internal ICM Portfolio Management workflow intended to compress a credit-risk portfolio review that can otherwise require days of manual analysis into a guided, human-controlled workflow.

The application is not intended to let an LLM make a final credit decision. It is an **AI-assisted decision-support and workflow orchestration system**. AI proposes event narratives, forward-looking scenarios, risk-factor methodologies, evidence-based company assessments, and portfolio commentary. Portfolio managers or credit professionals review, edit, challenge, and confirm the output before the workflow proceeds.

The current MVP already contains a strong foundation:

- a single-page HTML/JavaScript interface;
- a FastAPI backend;
- an internal R2D2/GenAI gateway integration;
- step-specific prompt files;
- structured JSON response handling and validation;
- deterministic scoring and credit-anchoring logic;
- local CSV and CAM/PDF evidence loading;
- end-to-end workflow screens from risk-narrative intake to portfolio assessment;
- a Market Dev environment intended for shared internal testing.

The next task is **not to rebuild the project from scratch**. The first task is to verify whether the current implementation faithfully represents the business workflow explained in the project walkthrough, especially the distinctions that were not obvious from the PowerPoint alone.

---

# 2. Business Objective and Intended Outcome

The system should help a portfolio manager answer the following question:

> Given a material market event and a defined forward-looking scenario, which companies in the selected portfolio are most vulnerable, why, what mitigants exist, what credit actions may be appropriate, and what is the aggregate portfolio impact?

The system must combine:

1. **Event-specific analysis** — risks created by the current event.
2. **Sector-inherent analysis** — persistent risks that matter for the company’s industry even when they are not the main theme of the current event.
3. **External/public evidence** — SEC filings, company disclosures, public web information, market/news sources where approved.
4. **Internal credit analysis** — CAM/credit memo or annual-review material, where available and authorized.
5. **Deterministic business rules** — scoring, weighting, classifications, aggregation, and credit anchoring where exact repeatability is required.
6. **Human confirmation** — review, edit, challenge, and confirm before material outputs become inputs to later steps.

The expected result is a transparent, traceable, evidence-based portfolio assessment rather than a free-form chatbot answer.

---

# 3. Core Design Principles Learned from the Walkthrough

## 3.1 Human in the loop is mandatory

Each material stage follows this pattern:

```text
AI proposes -> analyst reviews -> analyst edits/challenges -> analyst confirms -> confirmed data moves forward
```

The system must preserve the distinction between:

- raw AI proposal;
- analyst-edited version;
- confirmed version used by downstream steps.

The AI must not silently overwrite confirmed analyst decisions.

## 3.2 Prompts are sector- and event-agnostic

The approved prompts are intended to behave like reusable functions. The sector, event, horizon, assumptions, factor taxonomy, evidence, and company data are supplied as inputs. The project should not create a separate hard-coded prompt for every sector or every event unless a methodology owner explicitly approves an exception.

## 3.3 JSON is the machine contract

The walkthrough explicitly identified Markdown output as unsuitable for reliable UI integration. Each prompt should return validated JSON matching an explicit schema. The UI renders that JSON into editable cards, tables, and commentary.

Word, PDF, or HTML documents are report artifacts generated from structured state; they should not be the primary machine-to-machine contract.

## 3.4 AI proposes methodology; deterministic code performs exact calculations

AI may propose:

- risk factors;
- qualitative importance;
- candidate metrics;
- formulas;
- threshold bands;
- rationale;
- evidence interpretation;
- recommended narrative.

Exact arithmetic should be performed in deterministic backend code, including:

- factor weighted scores;
- event-driven and sector-inherent composites;
- final company composite;
- exposure-weighted portfolio aggregation;
- approved credit-anchoring rules.

## 3.5 Model governance and consistency matter

The project owner recommended a controlled model-routing strategy:

- **Claude Opus 4.6** for scenario generation, event-driven risk-factor/metrics proposals, and sector-inherent risk-factor/metrics proposals.
- **Claude Sonnet 4.6** for the other LLM-based pipeline components.
- **No LLM** for deterministic scoring and credit anchoring.

The mapping must be centralized in configuration and versioned. Users should not arbitrarily switch models during a governed assessment because model changes can alter quality, latency, and reproducibility.

## 3.6 Agents are capabilities, not necessarily separate deployed services

The PowerPoint uses conceptual agents such as Market Event Agent, Scenario Agent, Risk Factor Agent, SEC Analysis Agent, CAM Analysis Agent, and Portfolio Analysis Agent. The MVP may implement these as task-specific methods behind one orchestrator and one model gateway. Do not create unnecessary microservices merely to imitate the diagram.

---

# 4. Authoritative Workflow Reconstructed from the Walkthrough

## 4.1 Entry points / triggers

### Trigger 1: Market scanner

A market-event capability identifies potentially material events from approved news/market sources. This is a planned or partially implemented capability and should be clearly separated from static demo logs.

### Trigger 2: User-entered risk event

The analyst enters a short event narrative. The AI enriches it into a structured risk narrative.

## 4.2 Step 1 — Risk Narrative Intake and Enrichment

**Input:** Raw event description and optional label/context.

**Expected structured output:**

- event overview;
- event history;
- direct-impact geographies;
- contagion-impact geographies;
- equity-market impact;
- credit-market impact;
- commodity-market impact;
- initial assumptions or caveats;
- scenario label and relevant metadata.

The user must be able to edit each section and confirm the final narrative.

## 4.3 Step 2.1 — Forward-Looking Scenario and Assumptions

This is not a repetition of Step 1.

- Step 1 explains **what happened**.
- Step 2.1 defines **the future environment in which companies will be assessed**.

**Inputs:**

- confirmed Step 1 narrative;
- assessment horizon, such as 12 months or 3 years;
- optional additional context typed by the analyst;
- optional uploaded assumptions/research document.

**Outputs:**

- scenario narrative;
- a structured list of assumptions, each with code, label, value/range, rationale, horizon, and where appropriate severity or confidence.

The analyst reviews, edits, and confirms the scenario and assumptions.

## 4.4 Portfolio selection

The analyst selects the relevant portfolio or population using approved dimensions such as geography, country, legal entity, and industry hierarchy. The selected company/exposure data becomes an explicit input to the name-level assessment and portfolio aggregation.

## 4.5 Event-driven risk factors and metrics

These are specific to the current event and scenario.

**Inputs:**

- confirmed event narrative;
- confirmed scenario and assumptions;
- sector and selected portfolio context.

**AI proposes:**

- a bounded set of event-driven risk factors;
- importance bands, preferably coarse and governed rather than falsely precise;
- vulnerability metrics;
- mitigant/buffer metrics;
- formulas and threshold bands;
- critical threshold combinations;
- scoring rationale.

The portfolio manager reviews whether the factors and thresholds make domain sense, edits them, and confirms them.

## 4.6 Sector-inherent risk factors and reference taxonomy

Sector-inherent factors exist independently of the current event. For Software, examples observed in the walkthrough included cybersecurity, competition, regulatory scrutiny, dependence on advertising, talent acquisition/retention, switching costs, and pace of innovation.

The walkthrough clarified a lifecycle that the PowerPoint alone may not fully show:

1. The sector factor taxonomy is relatively static.
2. A periodic process, for example quarterly, may ask AI to re-propose or refresh the factor set for each sector.
3. A human methodology owner reviews and approves it.
4. The approved version becomes reusable reference data.
5. A live RPR assessment should retrieve the approved taxonomy/version rather than blindly regenerate a different sector factor set every time.

**Important open design question to verify with the methodology owner:** Are the detailed metrics and thresholds also centrally approved and reused, or does the live Step 2b prompt expand the approved factor taxonomy into review-specific metrics and thresholds? The current implementation must not assume the answer without evidence.

## 4.7 Name-level assessment

For each company, the system evaluates the confirmed event-driven and sector-inherent framework against available evidence.

The walkthrough described at least two independent evidence modes:

### Mode A: SEC/public evidence + web

The AI retrieves or receives approved public evidence, extracts the required metric values, compares them with confirmed thresholds, and produces an evidence-based assessment.

### Mode B: CAM/internal credit memo + web

The AI uses the internal credit memo/annual review plus recent approved public information. CAM is valuable because it contains human credit analysis, conclusions, strengths, weaknesses, and decisions rather than only raw financial values.

### Potential Mode C: combined comparison

The walkthrough described a future or desired comparison of:

- external/AI reasoning;
- internal human credit reasoning;
- a combined view.

Do not conflate this source comparison with the 80/20 event-versus-sector weighting.

For every assessed metric, the system should retain:

- source type;
- source identifier and date;
- extracted value;
- unit and period;
- evidence snippet or page/section reference where permitted;
- threshold used;
- resulting level/score;
- missing-data status;
- rationale and confidence.

## 4.8 Event-versus-sector weighting

The demonstrated methodology used:

```text
Final company residual-risk score = 80% event-driven composite + 20% sector-inherent composite
```

This is a methodology parameter, not a source-quality weighting. The implementation should keep it configurable and versioned, but changes require business approval.

Factor weights inside each pool were shown as coarse importance-derived weights, for example High receiving twice the weight of Medium. Exact mapping must be confirmed against the approved prompt/methodology.

## 4.9 Credit anchoring

Credit anchoring takes the residual-risk assessment plus current client credit information and applies approved rules to recommend actions such as review, watch, maintain, classification action, or escalation.

The current code correctly keeps this deterministic. However, every threshold and action mapping must be validated with the methodology owner. A rule inferred from a slide or demo must not silently become a production credit policy.

## 4.10 Portfolio aggregation and summary

The final stage consumes confirmed name-level results and exposure data to produce:

- exposure-weighted portfolio composite;
- risk distribution by grade/classification or other approved segmentation;
- largest contributors and key drivers;
- strengths, mitigants, and concentrations;
- recommended portfolio monitoring or actions;
- portfolio narrative and report.

The observed implementation uses OSUC/exposure weighting, which is preferable to a simple average because large exposures should contribute proportionally. The exact exposure field, currency normalization, exclusions, and missing-value handling must be documented and tested.


## 4.11 Exact UI, Prompt, Model, and Data Sequence

The agent must verify the sequence below against the running code. The business sequence is authoritative; route names and file names shown as "observed/current" must be confirmed in the repository.

| Order | UI/business stage | Human or system input | Prompt/capability expected | Model strategy | Required output and gate |
|---:|---|---|---|---|---|
| 0 | Trigger | Market-scanner event or user-entered narrative | Market event identification/enrichment | Sonnet for enrichment; scanner source depends on approved integration | Selected event or raw narrative |
| 1 | Step 1 - Risk Narrative Intake | Raw event text and optional label | Narrative enrichment, currently associated with `step1.txt` | **Sonnet 4.6** | Structured narrative JSON across the approved sections; analyst edits and confirms |
| 2 | Step 2.1 - Scenario & Assumptions | Confirmed Step 1 output, horizon, typed context, and optional uploaded context | Scenario generation and assumptions. The current repository may implement this through an inline `PromptService` method rather than a dedicated prompt file; this must be audited | **Opus 4.6** | Scenario narrative plus structured assumptions; analyst edits and confirms |
| 3 | Step 2.2 - Portfolio Selection | Geography, legal entity, industry hierarchy, company/exposure population | No generative prompt required for selection | Deterministic/data query | Confirmed company and exposure set |
| 4 | Step 2.3 - Event-driven Risk Factors | Confirmed narrative, scenario, assumptions, sector, portfolio context | Event-driven factor and metrics proposal, currently associated with `step2a.txt` | **Opus 4.6** | Factors, importance, metrics, formulas, thresholds, buffers, critical rules, rationale; analyst edits and confirms |
| 5 | Step 2.4 - Sector-inherent Risk Factors | Selected sector plus approved taxonomy/version | Retrieve approved sector taxonomy; where approved, use `step2b.txt` to expand factors into metrics/scoring | **Opus 4.6** only for proposal/refresh or approved expansion | Versioned sector factors/metrics; analyst confirms. Do not silently regenerate taxonomy per run unless approved |
| 6A | Step 2.5 - SEC/Public Assessment | Confirmed methodology, company data, SEC/public evidence, approved web evidence | Company assessment, currently associated with `step3_sec.txt` | **Sonnet 4.6** | Independent SEC/public assessment JSON with evidence provenance |
| 6B | Step 2.5 - CAM/Internal Assessment | Confirmed methodology, company data, CAM/annual review, approved web evidence | Company assessment, currently associated with `step3_cam.txt` | **Sonnet 4.6** | Independent CAM/internal assessment JSON with evidence provenance |
| 7 | Credit Anchoring | Company composite, current RRR/classification and approved client information | No prompt | **Deterministic only** | Recommended action under approved rules, with rule identifier and override handling |
| 8 | Step 3 - Portfolio Level Assessment | Confirmed name-level assessments and exposure data | Portfolio narrative/aggregation prompt, currently associated with `step4.txt` | **Sonnet 4.6** for narrative; deterministic code for arithmetic | Exposure-weighted portfolio result, drivers, concentrations, mitigants, recommendations; analyst confirms |
| 9 | Export/Publish | Confirmed structured workflow state | Report renderer/publisher | No LLM required unless an approved final narrative step is explicit | HTML/Word/PDF artifact plus versions and audit metadata |

### Required prompt-chain rule

The downstream prompt must consume the **confirmed** output of the previous stage, not the initial AI proposal. The expected chain is:

```text
User/market event
  -> Step 1 narrative JSON (confirmed)
  -> Step 2.1 scenario + assumptions JSON (confirmed)
  -> portfolio selection (confirmed)
  -> event-driven framework JSON (confirmed)
  -> approved sector taxonomy/framework JSON (confirmed)
  -> SEC and/or CAM company assessments
  -> deterministic scoring and credit anchoring
  -> portfolio aggregation and narrative
  -> confirmed report artifact
```

### Prompt-file governance issue to verify

The observed project has six prompt files:

```text
step1.txt
step2a.txt
step2b.txt
step3_sec.txt
step3_cam.txt
step4.txt
```

The scenario-generation stage appears to exist as a separate runtime method/route even though a dedicated scenario prompt file was not visible in that list. The agent must determine whether the scenario prompt is hard-coded in Python, stored elsewhere, or missing from the governed prompt registry. If it is hard-coded, propose a dedicated versioned prompt file such as `step2_scenario.txt` rather than maintaining duplicate prompt sources.

## 4.12 Uploads: What the HTML User May Upload and How the Backend Must Handle It

There are two different meanings of "upload" and they must not be confused.

### A. End-user upload inside the HTML workflow

The visible upload control is in **Step 2.1 - Scenario & Assumptions**. Its intended purpose is to provide optional context that helps define the forward-looking scenario. The UI shown in the walkthrough advertises the following file types:

```text
PDF, DOC, DOCX, TXT, CSV, XLSX - maximum 20 MB each
```

The agent must verify the actual implemented allow-list, size limit, number of files, and parser support. The UI label alone is not proof that a file is parsed.

**Appropriate content for this upload:**

- analyst-written scenario assumptions;
- a scenario narrative or research note;
- constraints, focus areas, management assumptions, or horizon details;
- an approved table of assumptions, ranges, or macro variables;
- approved internal or public context that the user is authorized to supply.

**This upload is not intended for:**

- credentials, certificates, access tokens, secrets, or configuration files;
- prompt source files or model-routing configuration;
- arbitrary executable files or archives;
- unauthorized CAMs, client data, or confidential material;
- the application deployment package.

**Required processing contract:**

1. User clicks the upload area or drags and drops a supported file.
2. Frontend validates extension, file count, and size before sending.
3. Backend validates MIME/type and size again; frontend validation is not sufficient.
4. File content is extracted using an approved parser:
   - PDF -> text and page references;
   - DOC/DOCX -> paragraphs and tables;
   - TXT -> normalized text;
   - CSV/XLSX -> bounded table extraction with sheet/column metadata.
5. Extracted context is normalized into a typed object with file name, type, size, hash, extraction status, warnings, and extracted content/reference.
6. The user can see which files are attached and remove a file before generation.
7. The confirmed horizon, typed context, and extracted file context are sent to the scenario prompt.
8. The response records which uploaded files were used, without embedding confidential contents in logs.
9. Unsupported, corrupt, encrypted, oversized, or empty files fail clearly and do not silently disappear.

The agent must prove through a test that changing the uploaded assumptions changes the scenario request context and, where the model is live, meaningfully affects the generated assumptions.

### B. System/admin evidence used for name-level assessment

The demo also uses files that are **not necessarily uploaded by a portfolio manager during the live workflow**:

- portfolio/client information CSV;
- CAM or annual-review PDF;
- sector risk-factor taxonomy document;
- prompt files;
- test fixtures and expected outputs.

These are currently loaded from controlled project folders or repositories. The agent must document whether each source is preloaded, selected, retrieved from an internal repository, or available through a separate upload/admin function. Do not add a user-facing CAM upload merely because the PoC reads a local PDF.

### C. Optional future Step 1 upload

The current Step 1 screen clearly supports typed user narrative and a market-scanner trigger. A general Step 1 event-document upload was not established by the walkthrough. The agent must report it as `Missing/Not required/Proposed` rather than inventing it. If requested by the owner, it can reuse the same safe extraction pipeline and feed the extracted event narrative to Step 1.

## 4.13 Demo Artifact Sequence and Production Mapping

The SharePoint demo folder illustrates the hand-off sequence through files. The agent should use it to understand the business chain, but production should pass structured JSON/state rather than repeatedly parsing Word output.

```text
1. Step 1 Input - User Input.txt
2. Step 1 Output / Step 2.1 Input - Risk Narrative.docx
3. Step 2.1 Output - Scenarios.docx
4. Step 2.3 Output / Step 2.5 Input - Event-Driven Risk Factors.docx
5. Step 2.4 Input - Risk Factor Taxonomy - Software.docx
6. Step 2.4 Output / Step 2.5 Input - Sector-Inherent Risk Factors - Software.docx
7. Step 2.5 SEC input - Client Information - Software.csv plus SEC/public evidence
8. Step 2.5 CAM input - Annual Review/CAM Memo.pdf
9. Step 2.5 outputs / Portfolio input - company assessment documents or JSON
10. Final output - Sector/Portfolio Impact Assessment.html or approved report format
```

For each artifact, the audit must identify:

- who creates or approves it;
- whether it is input, intermediate state, reference data, or report output;
- the production JSON/schema equivalent;
- the storage location and version;
- whether downstream code reads structured state or reparses the document;
- retention and access-control requirements.

## 4.14 What to Upload to Market Dev for Deployment

This is separate from end-user upload in the HTML page.

**Upload the minimum deployable package:**

```text
backend/
UI Design/ (or the approved frontend directory and main HTML file)
Prompt/ (approved, versioned prompt files)
tests/
requirements.txt
pytest.ini or equivalent test configuration
approved non-sensitive demo/reference fixtures required for the PoC
start/check scripts and deployment documentation, once created
```

**Do not upload or commit:**

```text
Windows .venv or venv folders
__pycache__ and local caches
local output/report folders unless specifically required
passwords, tokens, client secrets, certificate contents
hard-coded internal endpoints or user-specific paths
unapproved CAMs, client CSVs, or confidential documents
large duplicate OneDrive folders and unrelated presentations
```

After upload, create or use the approved Linux environment on Market Dev, install dependencies, run tests, configure environment variables through the approved mechanism, and verify the application through the Market Dev preflight endpoint. Shared user access requires the approved internal publishing/proxy route; copying files alone does not make the app available to other users.

## 4.15 Detailed Test Strategy and End-to-End Acceptance Script

Testing must cover functionality, business alignment, failure handling, and deployment. Code generation without an exercised workflow is not acceptance.

### Test data pack

Use only approved synthetic or sanitized data. The minimum reproducible pack should contain:

- a short event narrative, such as the approved SaaS disruption example;
- a known horizon, such as 12+ months;
- one typed context value;
- one small supported assumptions file for upload;
- one approved sector taxonomy fixture;
- a portfolio CSV with known companies and exposure amounts;
- one CAM/annual-review fixture where authorized;
- expected JSON fixtures for each step;
- expected deterministic scoring, anchoring, and portfolio calculations.

### Layer 1 - Repository and configuration audit

- verify all prompt files and their versions;
- verify one authoritative prompt source per task;
- verify task-to-model routing;
- scan for secrets and hard-coded Windows/localhost paths;
- verify supported file types, limits, and parser dependencies;
- verify no governed route silently falls back to mock/demo data.

### Layer 2 - Unit tests

At minimum:

- each Pydantic/JSON schema accepts valid output and rejects missing/invalid fields;
- scoring formulas and 80/20 event-versus-sector weighting;
- importance-to-weight normalization;
- exposure-weighted portfolio aggregation;
- deterministic credit-anchoring fixtures;
- file type/size validation;
- PDF/DOCX/TXT/CSV/XLSX extraction using small fixtures;
- missing, corrupt, encrypted, empty, and oversized files;
- malformed model JSON repair and final failure behavior;
- model-routing function selects Opus/Sonnet/no-LLM correctly.

### Layer 3 - API contract tests

Exercise each route with known payloads and verify:

- status code and typed response;
- prompt/model/schema/version metadata;
- correlation/session identifiers;
- no leakage of file contents or secrets in errors;
- confirmed state is accepted and used downstream;
- SEC and CAM outputs remain distinct;
- missing evidence is explicit.

### Layer 4 - Exact end-to-end UI test

1. Start the FastAPI backend and HTML frontend in the approved development environment.
2. Call health and preflight; confirm the intended provider/model is ready and `blocking_errors` is empty.
3. Open the HTML page from its served URL, not as an unserved local file.
4. In Step 1, enter the approved test event narrative.
5. Run AI enrichment. Verify every required narrative section is populated from structured JSON.
6. Edit at least one section, click confirm, and capture the confirmed value.
7. Open Step 2.1, set a 12+ month horizon, enter typed context, and upload a small approved assumptions file.
8. Verify the UI lists the file, the backend reports successful extraction, and the request contains the extracted context.
9. Generate scenario and assumptions. Verify the confirmed Step 1 edit, horizon, typed context, and uploaded context are represented in the request/result.
10. Edit one assumption and confirm it.
11. Select the Software test portfolio and verify company/exposure totals against the CSV fixture.
12. Generate event-driven factors. Verify factors, importance, vulnerability metrics, buffer metrics, formulas, thresholds, critical rules, and rationale.
13. Edit one threshold or factor where the UI permits, confirm it, and verify the edited value is used later.
14. Load sector-inherent factors. Verify the approved taxonomy version is displayed and that a new taxonomy was not silently generated unless the test explicitly targets refresh.
15. Run SEC/public assessment for at least one company. Verify evidence value, date, unit, source, threshold, score, and rationale.
16. Run CAM/internal assessment for at least one company where an approved CAM fixture exists. Verify it is a separate result from SEC/public.
17. Run name-level assessment for the full test portfolio. Verify deterministic 80/20 calculation and company results.
18. Run credit anchoring. Verify the exact approved rule identifier and expected action.
19. Run portfolio aggregation. Recalculate the exposure-weighted score independently and compare.
20. Verify portfolio drivers, concentrations, mitigants, classifications, and narrative render correctly.
21. Export the report. Verify the artifact contains the confirmed values and version metadata.
22. Refresh the page. Record whether state is intentionally lost in the PoC or restored from persistence; do not hide this behavior.
23. Review logs for correlation IDs, timings, model names, and errors, while confirming secrets and document contents are redacted.

### Layer 5 - Negative and resilience tests

- unsupported extension;
- file larger than the configured limit;
- corrupt or password-protected document;
- empty document;
- malicious filename/path traversal;
- prompt-injection text inside an uploaded document;
- model timeout, rate limit, invalid JSON, and unavailable provider;
- one company assessment failure while others succeed;
- duplicate submission/double-click;
- browser refresh during a running assessment;
- portfolio with missing/zero/negative exposure;
- stale CAM or public evidence;
- no evidence for a required metric;
- unauthorized user or inaccessible evidence source in the shared environment.

### Layer 6 - Market Dev smoke and shared-access test

- run the test suite in the Market Dev Linux environment;
- start the app using the approved process mechanism;
- verify project-relative Linux paths;
- verify health/preflight from the server;
- verify the HTML uses a configurable/same-origin API base rather than another user's `127.0.0.1`;
- access the application from an approved non-local internal URL;
- ask a second authorized user to open the URL and run a bounded smoke test;
- verify access control, session isolation, logs, and process persistence;
- do not claim shared deployment until the second-user test succeeds.

---

# 5. Current Implementation Observed

The implementation reviewed from screenshots and project knowledge documentation includes:

- one self-contained HTML/JavaScript MVP surface;
- FastAPI routes under an RPR API family;
- an `RPRService` workflow orchestrator;
- a model-gateway abstraction with mock and internal R2D2 implementations;
- prompt loading from step-specific text files;
- JSON fence stripping, parsing, validation, and repair retries;
- deterministic `scoring_service.py`;
- deterministic `credit_anchoring.py`;
- local evidence loading from portfolio CSV and CAM PDFs;
- backend preflight/readiness reporting;
- a provider-status badge in the UI;
- no silent mock fallback on MVP routes;
- end-to-end local execution of Step 1 through portfolio assessment;
- Market Dev access intended for the shared test deployment.

This is a strong MVP foundation. The audit should preserve working features and avoid an unnecessary rewrite.

---

# 6. Alignment Matrix the Agent Must Verify

The agent must inspect the actual repository and produce an evidence-based status for every requirement below. Use exactly one of: `Aligned`, `Partial`, `Missing`, or `Unclear`. For each item, cite the relevant route, prompt, schema, UI handler, service, test, or deployment file.

1. **Step 1 structured narrative:** full approved sections are returned and rendered.
2. **Step 2.1 distinction:** the scenario is forward-looking and not a repeat of event history.
3. **Scenario upload parsing:** uploaded content is genuinely extracted and injected into the scenario request.
4. **Upload controls:** allow-list, size limit, multi-file behavior, removal, and errors are implemented in frontend and backend.
5. **Upload provenance:** file metadata is captured without logging confidential content.
6. **Scenario prompt governance:** Step 2.1 has one versioned source of truth.
7. **Prompt sequence:** confirmed outputs move through the required steps in order.
8. **Event-driven methodology:** factors, metrics, thresholds, buffers, importance, and confirmation are represented.
9. **Sector taxonomy lifecycle:** approved/versioned reference data is reused rather than silently regenerated per run.
10. **SEC and CAM separation:** SEC/public and CAM/internal assessments remain independent result objects.
11. **Combined view:** a combination method is approved and explicit, or clearly deferred.
12. **80/20 meaning:** event-versus-sector weighting is not confused with evidence-source weighting.
13. **Deterministic calculations:** all exact arithmetic is outside the LLM.
14. **Credit anchoring:** deterministic rules exist and have a business approval/source marker.
15. **Model routing:** Opus/Sonnet/no-LLM strategy is centralized and observable.
16. **Prompt source of truth:** no active duplicate hard-coded prompt definitions drift from approved files.
17. **Version metadata:** prompt, model, schema, methodology, and taxonomy versions are returned or logged.
18. **Human edits downstream:** confirmed user changes, not original AI values, feed later stages.
19. **State distinction:** AI proposal, user edit, and confirmed value are distinguishable.
20. **Evidence provenance:** source, date, value, unit, and citation/page metadata are retained.
21. **Missing evidence:** absent data is explicit and never fabricated.
22. **Portfolio weighting:** approved exposure weighting and normalization are implemented and tested.
23. **No silent fallback:** the frontend and governed routes do not switch to demo/mock data without disclosure.
24. **Market Dev configuration:** Linux paths, API base, start scripts, and publishing assumptions are not tied to localhost.
25. **Deployment package:** local virtual environments, secrets, and unauthorized data are excluded.
26. **Security:** secrets/internal endpoints are not committed or printed in logs.

The audit report should present these items in a matrix or table of its own, but this knowledge-transfer document uses a checklist to remain readable across Word pages.

---

# 7. Likely Gaps or Risks to Investigate First

These are hypotheses based on the reviewed MVP. The agent must verify them rather than assume them.

## 7.1 Duplicate prompt sources

A screenshot showed short prompt strings in `prompt_service.py`, while project documentation described long approved `.txt` prompt files loaded by `prompt_loader.py`. Determine the runtime source of truth. Duplicate prompt definitions create drift and governance risk.

## 7.2 Sector taxonomy lifecycle

The current route may regenerate sector factors in every assessment. The walkthrough indicated that the sector factor set should be periodically refreshed, human-approved, versioned, and reused. Split the periodic reference-data process from the interactive RPR run if needed.

## 7.3 Evidence retrieval is currently PoC-level

Local CSV and local CAM/PDF loading are suitable for a demo but are not equivalent to real SEC, web, Helios financials, CAM repository, or client/portfolio integrations. The code and UI must make source capability honest and must not label static/local inputs as live retrieval.

## 7.4 Source-mode confusion

Ensure the code does not treat SEC versus CAM as the 80/20 weighting. Event-versus-sector weighting, factor weighting, and evidence-source comparison are separate concepts.

## 7.5 Business rules inferred from slides

Credit anchoring thresholds or factor-weight mappings may have been inferred from the deck. Mark unapproved rules as configurable draft methodology and obtain explicit sign-off before production use.

## 7.6 Persistence and audit

The current frontend state is in memory. This is acceptable for an initial demonstration but not for multi-user testing that requires save/resume, audit, approvals, or reproducibility. Define a phased persistence design rather than prematurely adding an oversized database architecture.

## 7.7 Model routing

Verify that the gateway can route each task to the intended model and that the model name/version is recorded. Do not rely on a single global model environment variable if different steps require different models.

## 7.8 Prompt-output schema strength

The JSON schemas should represent nested metrics, threshold bands, evidence, source metadata, user edits, confirmation status, and versions. Avoid passing large untyped dictionaries between steps.

## 7.9 Long-running name-level calls

Assessing multiple companies and two source modes may require concurrency, job status, retry controls, rate-limit handling, and cancellation. Do not block the browser indefinitely or run uncontrolled parallel calls.

## 7.10 Deployment and security

Market Dev can host the MVP, but shared access depends on the approved internal publishing/proxy mechanism. The agent must not expose arbitrary ports, use an unapproved public tunnel, hard-code tokens, or claim the app is shared until verified from an approved non-local URL.

---

# 8. Recommended Target Architecture

```text
Approved internal UI / Helios surface
        |
        v
RPR API and workflow orchestrator
        |
        +--> Prompt registry + model-routing configuration
        |
        +--> Internal LLM gateway
        |       - Opus for scenario and methodology proposals
        |       - Sonnet for other LLM tasks
        |
        +--> Evidence adapters
        |       - SEC/public filings
        |       - approved web/news/search
        |       - CAM repository
        |       - Helios financials
        |       - client/portfolio data
        |
        +--> Deterministic services
        |       - scoring
        |       - weighting
        |       - credit anchoring
        |       - portfolio aggregation
        |
        +--> Workflow/reference store
        |       - sessions and step state
        |       - AI proposal, edits, confirmations
        |       - prompt/model/schema versions
        |       - approved sector taxonomy versions
        |       - audit events
        |
        +--> Artifact/report publisher
                - HTML/Word/PDF as approved
```

For the MVP, these can remain modules in one FastAPI deployment. The architecture should define clean interfaces without forcing premature microservices.

---

# 9. Prioritized Change Plan

## Priority 0 — Verify before changing

1. Produce the alignment matrix in Section 6.
2. Trace every UI button to route, service, prompt, gateway task, schema, and state update.
3. Identify the authoritative prompt files and remove or deprecate duplicate prompt definitions.
4. Verify the model used by each workflow step.
5. Verify all scoring and credit-anchoring formulas against the approved methodology source.
6. Verify whether the sector factor set, metrics, and thresholds are generated per run or retrieved from approved reference data.
7. Verify how SEC, CAM, web, and local demo sources are actually represented.
8. Run the full automated test suite and a real end-to-end test in the approved development environment.

## Priority 1 — Safe MVP corrections

1. Centralize `step -> model` routing in configuration.
2. Add prompt, model, schema, methodology, and sector-taxonomy version metadata to responses.
3. Strengthen Pydantic/JSON schemas for each step.
4. Ensure confirmed UI values, not initial AI values, are sent downstream.
5. Separate independent SEC/public and CAM/internal result objects.
6. Add explicit missing-evidence and source-freshness states.
7. Add honest source labels so local files cannot appear to be live enterprise retrieval.
8. Add deployment configuration for Market Dev without hard-coded localhost or Windows paths.
9. Add tests for malformed JSON, missing evidence, model-routing, factor weighting, exposure weighting, and no silent mock fallback.

## Priority 2 — Controlled user testing

1. Add minimal persistence for sessions, step states, AI proposals, user edits, confirmations, and versions.
2. Add an approved sector-taxonomy/reference-data store and periodic refresh workflow.
3. Add evidence citations and provenance.
4. Add background-job/status handling for multi-company assessments.
5. Add role/entitlement integration through the approved host platform.
6. Add save/resume, export, audit history, and reproducibility controls.

## Priority 3 — Enterprise integration

1. Replace local evidence files with approved SEC, CAM, Helios, portfolio, and web/news adapters.
2. Add centralized monitoring, cost/latency metrics, model-call traceability, and operational alerts.
3. Add formal methodology approval and change-control workflow.
4. Add controlled prompt evaluation, regression datasets, and output-quality monitoring.
5. Publish through the approved Helios/Market Dev/Arc application mechanism.

---

# 10. Acceptance Criteria

A change is not complete merely because code was generated. The agent must demonstrate:

- tests pass;
- the actual route is exercised;
- real JSON maps correctly into the existing UI;
- confirmed edits flow to the next step;
- deterministic calculations reproduce expected fixtures;
- missing evidence does not become invented evidence;
- model routing is visible in response metadata/logging without leaking secrets;
- no silent mock or demo-data fallback occurs on the governed MVP path;
- Market Dev deployment works through the approved internal route, not only `127.0.0.1`;
- documentation is updated with files changed, decisions, blockers, and manual approvals required.

---

# 11. Open Questions for Leslie / Methodology Owners

The agent must stop and request business confirmation rather than invent answers for these items:

1. Is the sector factor taxonomy only refreshed quarterly, or can a portfolio manager trigger an ad hoc refresh?
2. Are sector metrics/thresholds also approved reference data, or are they generated within each event review from the approved factor set?
3. What is the official importance-to-weight mapping?
4. Is the 80/20 event-versus-sector weighting fixed or configurable by use case?
5. What are the official residual-risk score bands and labels?
6. What are the approved credit-anchoring rules and actions?
7. How should SEC/public and CAM/internal assessments be compared or combined?
8. What evidence sources are approved in the first live test?
9. What citation/provenance detail is mandatory in analyst-facing output?
10. Which fields may an analyst edit, and which are methodology-controlled?
11. What is the approved model identifier and reasoning configuration for Opus and Sonnet tasks?
12. What are the maximum company count, timeout, concurrency, and cost limits for one assessment?
13. What persistence/audit requirements apply to August user testing?
14. What is the approved Market Dev publishing and process-management mechanism?

---

# 12. Master Prompt for an Internal Coding/Architecture Agent

Copy the prompt below into the internal coding agent that has repository and terminal access.

---

## BEGIN MASTER PROMPT

You are the senior architecture and implementation agent for the **AI-Assisted Rapid Portfolio Review (RPR)** project. You have access to the existing repository, current documentation, PowerPoint workflow, test data, and development terminal.

Your first responsibility is **not to rewrite the application**. Your first responsibility is to audit whether the existing implementation faithfully represents the business workflow learned from the project walkthrough and summarized below.

### A. Project purpose

RPR is an AI-assisted, human-in-the-loop credit-risk workflow. It enriches a material event, defines a forward-looking scenario, proposes event-driven and sector-inherent risk methodology, assesses companies using approved external and internal evidence, applies deterministic scoring and credit anchoring, and aggregates the results into a portfolio assessment.

AI proposes and explains. Human analysts review, edit, and confirm. Deterministic code performs exact calculations. The system is decision support, not autonomous credit approval.

### B. Business workflow you must validate

1. Entry point is either a market-scanner event or a user-entered event narrative.
2. Step 1 enriches the event into structured sections: overview, history, direct geographies, contagion geographies, equity impact, credit impact, commodity impact, and assumptions/caveats.
3. Step 2.1 uses the confirmed event plus horizon and optional uploaded/typed context to define the forward-looking scenario and structured assumptions.
4. The analyst selects the portfolio.
5. AI proposes event-driven risk factors, importance, vulnerability metrics, buffer/mitigant metrics, formulas, threshold bands, critical combinations, and rationale. The analyst reviews/edits/confirms.
6. Sector-inherent factors are based on a sector taxonomy that is relatively static, periodically refreshed, human-approved, versioned, and reused. Verify whether detailed metrics/thresholds are also reference data or are generated from the approved factor set during a review; do not assume.
7. Name-level assessment supports independent SEC/public+web and CAM/internal+web evidence paths. A combined comparison may exist or be planned. Do not confuse evidence source with event-versus-sector weighting.
8. Company final score uses approved event-driven and sector-inherent composites; the demonstrated methodology is 80% event-driven and 20% sector-inherent.
9. Exact scoring, weighting, exposure aggregation, and approved credit anchoring are deterministic, not LLM calculations.
10. Portfolio aggregation is exposure-weighted and produces drivers, concentrations, mitigants, recommended monitoring/actions, and narrative.
11. Every material step is human-in-the-loop and downstream calls must use confirmed values.
12. LLM outputs are structured JSON validated against explicit schemas; the UI renders JSON.
13. Prompts are sector- and event-agnostic; inputs vary.
14. Model routing recommended by the project owner:
    - Claude Opus 4.6: scenario generation, event-driven factors/metrics proposal, sector-inherent factors/metrics proposal.
    - Claude Sonnet 4.6: other LLM components.
    - No LLM: deterministic scoring and credit anchoring.
15. Exact prompt chain must be verified as: Step 1 narrative -> Step 2.1 scenario/assumptions -> portfolio selection -> Step 2.3 event factors -> Step 2.4 approved sector factors -> Step 2.5 SEC and/or CAM company assessment -> deterministic anchoring -> Step 3 portfolio aggregation.
16. The Step 2.1 HTML upload is for optional scenario context/assumptions. The visible UI claims PDF, DOC, DOCX, TXT, CSV, and XLSX up to 20 MB each. Verify, do not assume. Content must be parsed and injected, not merely attached.
17. Portfolio CSVs, CAM PDFs, sector taxonomy documents, prompts, and deployment files are different controlled inputs; do not expose them all through one user upload control.
18. Market Dev deployment must transfer only the deployable application/test package, not Windows virtual environments, secrets, unrelated folders, or unauthorized client data.

### C. Current implementation believed to exist

The repository appears to include a single-page HTML/JavaScript UI, FastAPI backend, RPR orchestration service, internal R2D2 gateway, step prompt files, JSON validation/repair, deterministic scoring, deterministic credit anchoring, local CSV/CAM evidence loading, preflight checks, and an end-to-end local workflow. Treat this as a hypothesis and verify it in code.

### D. Mandatory Phase 0 - Verify Prior Agents' Understanding

Before inspecting or changing code, verify what prior agents believed they implemented.

1. Read prior agent summaries, continuation prompts, project knowledge files, commit messages, and test reports.
2. If the environment supports multi-agent communication, ask the prior agents to answer, with file evidence:
   - What exact UI/business workflow did you implement?
   - What prompt or prompt file is used at every stage?
   - Is the Step 2.1 scenario prompt governed as a file or hard-coded?
   - Which model is routed to each stage and where is routing configured?
   - What does the HTML upload control accept, how is each type parsed, and how is extracted content injected?
   - Are event-driven and sector-inherent factors both generated per run, or is sector taxonomy retrieved as approved reference data?
   - Are SEC/public and CAM/internal assessments independent?
   - Which calculations and credit actions are deterministic?
   - Which tests were actually run and what failed or remains mocked?
   - What deviations, assumptions, shortcuts, or unresolved business questions remain?
3. If direct agent communication is unavailable, state that limitation and reconstruct the answers from their artifacts rather than pretending they were consulted.
4. Compare their answers against Sections A-C and the exact sequence/upload/test requirements below.
5. Produce a short `Prior Agent Alignment Summary` before the repository audit, using `Aligned / Partial / Missing / Unclear`.

### E. Mandatory Phase 1 - Read-only audit

Do not modify code in Phase 1.

1. Map the repository structure.
2. Identify all runtime entry points, routes, services, prompts, schemas, evidence adapters, state variables, and tests.
3. Trace each UI action end-to-end:
   `button -> JavaScript handler -> HTTP route -> request model -> orchestrator method -> prompt source -> model routing -> response schema -> deterministic enrichment -> UI state/rendering`.
4. Determine whether `prompt_service.py` and `.txt` prompt files duplicate each other. Identify the actual runtime source of truth.
5. Determine the model used by each step and whether routing is centralized.
6. Determine exactly what Step 2a and Step 2b generate and whether sector factors are regenerated per run.
7. Determine whether uploaded files are truly parsed and injected or only displayed.
8. Determine whether SEC and CAM analyses are independent result objects and whether web evidence is real, mocked, static, or absent.
9. Identify every deterministic formula and its test coverage.
10. Identify every business rule that lacks an explicit approval/source marker.
11. Identify whether analyst edits and confirmations are sent to later steps.
12. Identify whether AI proposal, edited state, and confirmed state are distinguishable.
13. Identify persistence, audit, versioning, and provenance capabilities.
14. Scan for secrets, hard-coded internal endpoints, Windows paths, localhost dependencies, and unsafe logging. Do not print secret values.
15. Run the existing tests without changing code.
16. Produce the exact prompt execution map from Step 1 through Step 4, including prompt file/method, model, input schema, output schema, confirmation gate, and downstream consumer.
17. Audit the Step 2.1 HTML upload control end-to-end: allow-list, 20 MB UI claim, backend size/MIME checks, multi-file behavior, parsers, extraction metadata, removal, errors, and prompt injection.
18. Determine what the user is expected to upload in the HTML versus what is system/admin evidence loaded from CSV/CAM/taxonomy repositories.
19. Trace the demo artifact chain and map every Word/CSV/PDF/HTML file to its production structured-data equivalent.
20. Inspect the Market Dev deployment package and identify files that must or must not be transferred.
21. Verify local, API, upload, model-routing, end-to-end, negative, and Market Dev tests against the detailed script in this knowledge-transfer document.
22. Do not call an upload feature complete unless a test proves the extracted content reaches the intended prompt request.

### F. Phase 1 deliverable

Produce an **Alignment Audit Report** with:

- executive conclusion;
- repository map;
- workflow call graph;
- requirement-by-requirement matrix using `Aligned / Partial / Missing / Unclear`;
- file and line evidence for every conclusion;
- list of business assumptions that require owner confirmation;
- list of technical defects, ordered by severity;
- test results;
- no code changes.

### G. Mandatory Phase 2 - Proposed change plan

After the audit, propose the smallest safe set of changes. Separate them into:

- P0 correctness/governance;
- P1 MVP hardening;
- P2 controlled user testing;
- P3 enterprise integration.

For every proposed change, state:

- problem;
- evidence;
- user/business impact;
- files likely affected;
- schema/API compatibility impact;
- tests required;
- business approval required, if any;
- rollback approach.

Do not propose microservices, a vector database, or a large persistence platform unless the requirement justifies them.

### H. Phase 3 - Implementation rules

Implement only changes that are technically safe and do not invent business methodology.

1. Preserve the existing working HTML surface unless explicitly asked to redesign it.
2. Keep backward compatibility where practical.
3. Use approved prompt files as the single source of truth.
4. Centralize step-to-model routing in configuration.
5. Return prompt/model/schema/methodology/version metadata.
6. Use strongly typed schemas; avoid untyped dictionaries between stages.
7. Use confirmed user-edited data downstream.
8. Keep all exact math and credit anchoring deterministic.
9. Make missing evidence explicit; never fabricate values or citations.
10. Keep SEC/public and CAM/internal assessments separate until an approved combination rule exists.
11. If sector taxonomy lifecycle is not implemented, create an interface and clear temporary fallback, not a falsely governed solution.
12. Do not add a silent mock fallback to the governed MVP path.
13. Do not hard-code secrets, internal hostnames, certificate paths, user IDs, or service tokens.
14. Do not expose unapproved network ports or use a public tunnel.
15. Do not claim deployment is shared until verified through an approved non-local internal URL.
16. Create or update tests for every changed behavior.
17. Run unit, API, and end-to-end tests.

### I. Required verification tests

At minimum, add or verify tests for:

- Step 1 JSON schema completeness;
- exact prompt sequence and confirmed-output propagation from Step 1 through Step 4;
- Step 2.1 horizon, typed context, file-list metadata, extracted uploaded-context propagation, and removal behavior;
- supported/unsupported file types, declared size limit, corrupt/encrypted/empty files, and prompt injection inside an upload;
- Opus/Sonnet routing by task;
- malformed JSON repair and final failure behavior;
- no silent mock fallback;
- confirmed edits used downstream;
- event-versus-sector 80/20 formula;
- importance-to-weight normalization;
- exposure-weighted portfolio aggregation;
- missing evidence and stale evidence;
- SEC and CAM independent outputs;
- deterministic credit anchoring fixtures;
- prompt/model/schema version metadata;
- Linux/project-relative paths;
- Market Dev preflight/readiness;
- one full UI test using the approved event, 12+ month horizon, an uploaded assumptions fixture, Software portfolio, event and sector factors, SEC and CAM paths, deterministic anchoring, portfolio aggregation, and report export;
- one second-authorized-user smoke test through the approved non-local Market Dev URL before shared deployment is declared successful.

### J. Stop conditions

Stop and ask for methodology-owner confirmation before implementing:

- new credit-action rules;
- new residual-risk bands;
- changed 80/20 weighting;
- changed importance-to-weight mapping;
- automatic combination of SEC and CAM opinions;
- editable methodology-controlled fields;
- unapproved evidence sources;
- new model or reasoning parameters;
- a sector-taxonomy refresh policy.

### K. Final report format

At completion, report:

1. Audit conclusion.
2. Files inspected.
3. Files changed.
4. Business alignment corrections.
5. API/schema changes.
6. Model-routing changes.
7. Tests run and exact results.
8. End-to-end scenario tested.
9. Deployment/readiness status.
10. Remaining business questions.
11. Remaining manual infrastructure actions.
12. Security scan summary with secrets redacted.

Never report success based only on code generation. Demonstrate the behavior through tests and an exercised end-to-end workflow.

## END MASTER PROMPT

---

# 13. Suggested First Agent Response

The agent’s first response should look approximately like this:

> I will begin with a read-only alignment audit. I will not modify code until I have mapped the UI-to-backend call flow, identified the authoritative prompts, confirmed model routing, traced sector taxonomy behavior, separated SEC/CAM evidence paths, and verified deterministic scoring and credit anchoring. I will return an evidence-based alignment matrix and a prioritized change plan. Any business-rule ambiguity will be listed for methodology-owner confirmation rather than guessed.

---

# 14. Security and Sharing Rules

Before sharing this document or any agent output:

- remove screenshots containing internal URLs, hostnames, client IDs, scope IDs, email addresses, user IDs, certificate paths, or token endpoints;
- never include certificate contents, passwords, access tokens, client secrets, or temporary credentials;
- do not upload CAMs, annual reviews, client CSVs, or confidential financial data to an external model;
- use only approved internal agents and repositories;
- keep environment-specific values in approved secret/configuration mechanisms;
- ensure logs redact sensitive request headers and document content.

---

# 15. Final Guidance

The present MVP should be treated as a strong, working orchestration prototype. The correct next step is an alignment-and-hardening exercise, not a wholesale rewrite. Preserve what works, correct the business distinctions revealed by the walkthrough, centralize governance, strengthen schemas and provenance, and move toward controlled Market Dev user testing through the approved internal publishing mechanism.
