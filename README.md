## Evidence Retrieval Strategy — STRICT BOUNDED EXECUTION

The confirmed ScenarioContextJSON, EventDrivenFactorsJSON and SectorInherentFactorsJSON already define the analytical framework. SEC Filings and Web Search are used only to obtain company-specific evidence needed to apply that framework.

### Company Identity Gate

First read CompanyContextJSON and use all supplied identity information.

If a confirmed CIK or confirmed SEC registrant is supplied:
SEC_PATH = ENABLED.

If the company is confirmed private/non-SEC:
SEC_PATH = SKIP.
Do not call SEC Filings.

If SEC status is unresolved:
make at most ONE reasonable SEC identity/registrant attempt.
If no reliable registrant is resolved, record the evidence gap and STOP using SEC Filings.

Never repeatedly retry SEC after identity resolution has failed.

### SEC Retrieval Budget

When SEC_PATH = ENABLED, normally use only:

- latest relevant 10-K before AssessmentAsOfDATE;
- latest relevant 10-Q before AssessmentAsOfDATE;
- one additional 8-K/filing only when directly material.

If SEC Filings returns no usable result after the initial direct attempt:
record the limitation and stop SEC retrieval.

Do not repeatedly search SEC.

### Web Search Budget

Use a maximum of FOUR purposeful Web Search actions for the entire company assessment.

Do NOT perform one search per Event-Driven or Sector-Inherent factor.

Search by evidence theme:

1. company identity, business model and financial condition;
2. liquidity, leverage, refinancing and capital structure;
3. scenario exposure and relevant industry/geographic sensitivity;
4. counter-thesis / disconfirming evidence only if still needed.

One source may support multiple factors.

If sufficient evidence is obtained after 2 or 3 searches, STOP.

Do not repeat substantially equivalent searches with slightly different wording.

### Evidence Reuse

Create one company-level evidence pool and reuse it across all relevant factors.

Do not search again when existing evidence already supports the factor.

### Assessment

Assess every supplied EventDrivenFactorsJSON factor exactly once.

Assess every supplied SectorInherentFactorsJSON factor exactly once.

For every factor:
- test company evidence against the supplied vulnerability metrics;
- test evidence against the supplied buffer metrics;
- apply the supplied Step 3a 1–5 scoring methodology;
- identify supporting and disconfirming evidence;
- record genuine evidence gaps without inventing values.

### Mandatory Stop Rule

STOP searching as soon as enough reliable information exists to assess:

- company identity/business model;
- principal financial vulnerabilities;
- liquidity/leverage/refinancing where relevant;
- scenario exposure;
- material buffers;
- reasonable counter-evidence or evidence limitations.

More searches are not automatically higher quality.

When evidence is sufficient, immediately complete scoring and return the final schema-compliant JSON.

Do not generate additional markdown or narrative artifacts.
