# CCRIG — Project Handover & Execution Brief for Luna
## From: Ala-Eddine Karib, ICM First Line of Defense, Citi
## Date: September 14, 2026

---

## 0. Before You Read Anything Else

This is a **running local application**, not a spec for something to build from scratch. Your job is **data integration and feature addition** on top of an existing, working codebase. Do not redesign the architecture, do not change the frontend visual language, do not rebuild modules that already work. Extend what exists.

Everything synthetic in the tool needs to be replaced or augmented with **real data from the files in this folder**. Where real exposure figures cannot be used (governance/data sensitivity), the structure should be derived from the real population of names and relationships, with figures clearly labelled as illustrative. More on this below.

---

## 1. What This Project Is

**CCRIG** (Counterparty Risk Information Graph) is an internal AI analyst platform, POC stage, built for Citi's Institutional Credit Management (ICM) / Portfolio Credit Risk Management team — specifically the underwriting and CCR monitoring functions.

It is a **local web application** running at `127.0.0.1:5173` (frontend) with a backend API. The codebase is in the folder you have access to:

```
ccrig-master/
├── frontend/          ← React/Vite frontend, do not touch visual design
├── backend/           ← FastAPI or similar Python backend
├── docs/
├── screenshots/
├── README.md
├── BUILD_REPORT.md
├── render.yaml
├── .env.example       ← configure your environment here
└── AI Economy Study_Masterfile.xlsx   ← THE PRIMARY DATA SOURCE (see Section 3)
```

The tool has **12 working modules**, all running in offline deterministic mode (no API key required for the POC data layer):

| Module | URL | What it does |
|---|---|---|
| Relationships | `/` | Entity/counterparty/theme/risk-factor search. "The graph nominates what's connected — exposure is a separate question, asked after." |
| Events | `/events` | Event-driven analysis, event → entity propagation |
| Counterparties | `/counterparty?id=...` | Counterparty 360 — three tabs: Relationships, Exposure & Controls, Decision. Counterparties prioritised CRITICAL → HIGH → MEDIUM → LOW → INFORMATIONAL |
| Controls | `/breaches` | Control Exceptions — active limit breaches, age-sorted |
| Inbox | `/inbox` | The ranked investigation queue — "the 5 things worth a look today" with driver classification and ΔPFE |
| Entity Explorer | `/entity` | Composite relatedness scores with full explainability — Layer A fact relations (SUPPLIES, SUPPLIED_BY, etc.), Layer B derived similarity (sector, news, geography, semantic, market correlation), typed path display |
| Exposure Movers | `/exposure-movers` | PFE Movers / Stress-NSE Movers / RC-MTM Movers / Sensitivity Movers tabs, ranked by ΔPFE |
| Graph Explorer | `/graph` | Bounded ego-graph — fact (solid/directional), derived (dashed/symmetric), exposure (dotted) |
| Theme Radar | `/theme-radar` | Dynamic scatter: X=attention velocity, Y=entity coverage. 47-item curated taxonomy + TF-IDF discovered themes |
| Model Lab | `/model-lab` | Weight tuning sliders for the relationship vector (Sector, Geography, Supply chain, Ownership, Semantic, News co-mention, Market corr+, Market corr−). Presets. Experimental anchor calibration |
| Backtest Lab | `/backtest-lab` | Scenario replay — Taiwan earthquake scenario built, Precision@5=0.6, Recall@5=0.375. Look-ahead prevented by design (model computed as-of T0 using only fact-graph + pre-event correlation) |
| Data Sources | `/data-sources` | Data source configuration |

**Offline deterministic mode** means: the tool runs fully without an AI API key. All relationship scoring is deterministic (weighted formula). The AI layer (if `AI_API_KEY` is set) adds LLM-generated narrative explanation on top of scores that are already computed — it never generates the scores.

---

## 2. The Business Context and What the Team Actually Needs

This tool was built to support two overlapping use cases:

**Use Case A — CCR Monitoring (existing, working in synthetic form):**
The Inbox, Exposure Movers, Controls, and Counterparty 360 modules support daily CCR portfolio monitoring. An analyst opens the Inbox and sees the top-priority counterparties ranked by a combination of ΔPFE magnitude, limit utilisation, breach age, and driver classification (NEW_TRADE, MARKET_MOVE, WWR_RELATED, NON_NETTED_EXPOSURE, UNKNOWN_PENDING_INVESTIGATION). They drill into a counterparty and see Relationships → Exposure & Controls → Decision in three tabs.

**Use Case B — AI Ecosystem / Underwriting Intelligence (the new work, partially built):**
A separate tool exists (the `AI_Infrastructure_Counterparty_Network` HTML file — also in this folder) that shows a relationship database of 46 companies, 104 records, sourced from three credit memos (BX Matrix II Funding LLC Annual Review CAM, CoreWeave Inc Quarterly Review CAM, Anthropic PBC Annual Review CAM). This tool has the relationship data; CCRIG has the monitoring infrastructure. **The team wants these merged.**

**What MJ (Kim, Moo-Jin, the sponsor) specifically asked for (from email chain, Sept 9-10, 2026):**
1. **GFCID/CAGID mapping** — given a company name from a CAM (e.g. "OpenAI"), show Citi's total combined exposure across all facilities for that CAGID grouping. The Masterfile has this data.
2. **Better groupings and filter logic** — as more CAMs are added, the network map becomes hard to read. Smarter clustering by relationship type, hub facility, sector.
3. **Export functionality** — a UW reviewing a CoreAI name should be able to export a filtered report (relationships + exposure summary) that can be added to their CAM workflow.
4. **"Indirect exposure" surfacing** — two examples of where indirect exposure is mentioned in CAM text (this is what the Entity Explorer and Graph Explorer already do; needs to be connected to real names).

**Leslie Zhang's direction (same email chain):**
*"Ala-Eddine has already built a prototype of client correlations, let's build on top of that capability and avoid reinventing the wheel."*

**MJ's phrasing of the goal:**
*"Intention is not to reinvent the wheel but visualize my idea. Please walk us through the correlation work."*
*"Citi's exposure if a company mentioned is Citi's clients — we should be able to see all the combined exposures for a grouping — how much is Citi's exposure related to OpenAI for example."*

---

## 3. The Data You Have — Read This Section Carefully

### 3A. AI Economy Study_Masterfile.xlsx

This is the **primary data source**. It has six tabs:

**Master file tab:**
- CAGID (Relationship) — Citi's internal client identifier
- CAGID (Relationship) Name — company name
- Total OSUC PSLE Net of Hedges Jul'26 ME — net exposure in USD (the headline exposure figure)
- Pillar (CLFU, RESCU, F&S)
- Vertical (TMT, SAII, RE, LFU, etc.)
- UW Portfolio Head, UW Underwriter, UW Analyst — the coverage team
- We have CAM? (Yes/No) — 3 of 75 CoreAI names currently have CAMs
- Latest CAM Date — date of most recent CAM
- Population Source — "CoreAI" for all rows in this workbook

Key names visible (all publicly known companies, their CAGIDs are internal):
- BX Matrix II Funding LLC (CAM: Yes, 2/21/2025)
- Anthropic PBC (CAM: Yes, 10/24/2025)
- CoreWeave Inc (CAM: Yes, 6/12/2026)
- OpenAI OPCO LLC, Crusoe Inc, QualityTech LP, QTS Good News Facility, Digital Realty Trust, Equinix Inc, Project Delta, Project Tidal, and ~65 more CoreAI names

**Pivot - Core AI tab:**
Pivot table showing CoreAI exposure by name, useful for the "total exposure per grouping" view MJ asked for.

**Core AI - Raw data tab:**
Facility-level detail: GFBN codes, facility long descriptions (Loan-Delayed Draw Construction, Loan-Revolving, Standby Letters of Credit, Traded Products/Derivatives, Loan-Term Loan, etc.), PSLE Amt, Direct Amt, Contingent Amt, PSE Amt, CVA Dynamic, Hedge Amt, Limit-Facility, Outstanding, Exclude flags.

**CAM Data tab:**
The relationship intelligence extracted from the three CAMs — this is the data that feeds the AI Infrastructure Network tool. Company relationships, types, amounts, sources, confidence.

### 3B. AI_Infrastructure_Counterparty_Network HTML file

The working relationship database tool, showing:
- 46 unique companies across BX Matrix II / CoreWeave / Anthropic CAMs
- 52 unique relationships, 104 records (bidirectional)
- Categories: Hub Facility (Citi Subject), Big Tech/Hyperscaler, Silicon/Hardware Supply Chain, Financial Investor/Lender, AI Lab/Model Developer, Enterprise Customer, Regulator/Legal, Advisory/Rating Agency, M&A Target, Competing Infrastructure
- Key relationships with amounts and confidence ratings (Very High / High / Medium-High / Medium / Low)
- Confidence methodology: CAM is primary; SEC + news are supplementary corroboration

### 3C. CAM Priority Population_Batch 1.xlsx

The batch population list used to identify which CoreAI names to prioritise for CAM extraction. Use this as the population reference alongside the Masterfile.

### 3D. CCRIG's existing synthetic data

The tool currently runs on **fictional/synthetic counterparties** (Sovereign Debt Office Nation Alpha, Meridian Alpha Rates Fund, Kestrel Family Office, etc.). These are illustrative. Your job is to **layer in the real CoreAI population** from the Masterfile alongside or replacing the synthetic data, while keeping the synthetic CCR counterparties as illustrative examples for any module that needs them for demo purposes.

---

## 4. What You Need to Build — Prioritised

### Priority 1 — GFCID/CAGID Exposure Aggregation Layer (MJ's #1 ask)

**What:** Given any company name that appears in the relationship graph (e.g. "OpenAI", "CoreWeave", "Microsoft"), show Citi's total OSUC PSLE exposure for that company's CAGID grouping, drawn from the Masterfile.

**How:**
1. Build a lookup table: `company_name_normalized → CAGID → total_exposure + facility_breakdown`
2. The normalization matters — CAM text says "OpenAI" but the Masterfile says "OPENAI OPCO LLC" — you need fuzzy matching on company name, not exact string match.
3. Surface this in:
   - **Counterparty 360, Exposure & Controls tab**: show the OSUC PSLE figure, facility breakdown (revolving, term loan, DDTL, derivatives, standby LCs), utilisation vs limit where available
   - **Entity Explorer**: when a company is loaded, show a small "Citi Exposure" sidebar panel with the matched CAGID and total net exposure
   - **Relationships search**: when search results include a company with a known CAGID, show a small exposure badge next to the name

**Key logic:**
```
For a company_name from CAM/relationship data:
  1. Normalize name (lowercase, strip legal suffixes like LLC/Inc/Corp/Ltd)
  2. Fuzzy match against Masterfile CAGID Name column (threshold: 0.85 similarity)
  3. Return: matched_CAGID, total_PSLE_net_of_hedges, facility_count, CAM_available (Y/N), latest_CAM_date, UW_underwriter
  4. If no match found: show "Not in OSUC population" (this is expected for supply-chain entities like TSMC, ASML that are not Citi clients)
```

**Do not hard-code CAGID mappings.** Build the lookup dynamically from the Masterfile so it updates when the file updates.

### Priority 2 — Real CoreAI Entity Population in Entity Explorer and Graph Explorer

**What:** Populate the Entity Explorer and Graph Explorer with the real 75 CoreAI company names from the Masterfile, using the relationship data from the AI Infrastructure Network (the CAM Data tab / the HTML tool's dataset) as the fact-layer input.

**How:**
1. Parse the CAM Data tab (or the HTML tool's embedded JSON/data) to extract: Company A, Company B, Relationship Type, Amount, Confidence, Source
2. Load these as **Layer A (Fact) edges** in CCRIG's graph — typed: GUARANTOR/BACKLEVERAGE, SUPPLIER/INVESTOR/CUSTOMER, SUPPLY_CHAIN, CONTRACTED_CUSTOMER, EQUITY_INVESTOR, COMPETITOR, PEER/CUSTOMER/PARTNER, FAILED_M&A_TARGET, COMPLETED_ACQUISITION, CUSTOMER+EQUITY_HOLDER, etc.
3. The Entity Explorer's composite relatedness score already works — it just needs real entities to score. Feed the 46 CAM companies + the broader 75 CoreAI names as the entity universe.
4. The Graph Explorer already renders fact/derived/exposure edges correctly — connect it to this real data.

**Entity universe for the CoreAI population (source: Masterfile + CAM companies):**
- Hub entities (Citi subjects): BX Matrix II Funding LLC, CoreWeave Inc, Anthropic PBC
- Hyperscalers: Microsoft, Google/Alphabet, Amazon/AWS, Meta Platforms, Apple
- Semiconductor supply chain: NVIDIA, TSMC, ASML, SK Hynix, Samsung Electronics, Super Micro, Dell, Gigabyte
- AI labs: OpenAI, Mistral AI, Cognition, Weights & Biases (acquired by CoreWeave)
- Financial investors: Blackstone, Coatue, Magnetar Financial, Carlyle Group, Fidelity, J.P. Morgan, Jane Street
- Enterprise customers: Microsoft (contracted), Meta (contracted), Google Cloud (peer/partner), Replicate, Chai, Mistral AI (select customer), OpenAI (customer+equity holder)
- Competing infrastructure: Core Scientific, AWS, Google Cloud

### Priority 3 — Export Functionality

**What:** From three views, an analyst should be able to export a structured report.

**Export 1 — Counterparty 360 export:**
When viewing a counterparty (e.g. CoreWeave), a button "Export to CAM Report" produces a PDF or structured HTML containing:
- Counterparty name, CAGID, exposure summary (PSLE net, facility breakdown)
- Key Risk Clusters (the relationship clusters shown in the Relationships tab)
- Top related entities with relatedness scores and typed paths
- Active controls/breaches
- Decision recommendation

**Export 2 — Relationships filter export:**
From the AI Infrastructure Network's filterable database view, a "Export filtered view" button downloads the currently-filtered records as CSV with: Company A, Company B, Type, Relationship (A's perspective), Amount, Source, Confidence.

**Export 3 — Entity Explorer export:**
"Export entity report" from Entity Explorer produces a one-page summary: entity name, CAGID + exposure if matched, top 10 related entities with scores and explain text, Layer A fact relations, typed paths.

### Priority 4 — CAGID Grouping in the Network Map

**What:** The network map (the AI Infrastructure Network view) should support grouping by CAGID/facility — when multiple entities roll up to the same economic exposure (e.g. "CoreWeave Inc" and "CoreWeave Operating LLC" might have separate CAGIDs but are the same economic entity), they should be visually groupable.

**How:**
- Add a "Group by: Hub Facility / Sector / Exposure tier" toggle above the network map
- "Hub Facility" grouping colours nodes by which CAM they came from (BX Matrix II / CoreWeave / Anthropic / Not in CAM) — this is already partially done via the category colours
- "Exposure tier" grouping sizes nodes proportional to Citi's PSLE exposure for that company (from the Masterfile lookup in Priority 1) — zero exposure = small dot; large exposure = large node. This makes concentration immediately visible.

---

## 5. What NOT to Do

- **Do not rebuild the frontend visual language.** The existing CCRIG UI (sidebar nav, clean typography, teal/dark palette, offline deterministic mode badge) must be preserved exactly.
- **Do not replace the synthetic CCR counterparty data entirely.** The Inbox, Exposure Movers, and Controls modules using fictional sovereign/fund counterparties are useful demos. Keep them, and add the real CoreAI layer as a separate or merged data source.
- **Do not attempt to compute PFE from scratch.** CCRIG does not reprice trades or simulate exposure. Where PFE/ΔPFE figures are shown, they come from the data layer (currently synthetic). For the CoreAI population, use the OSUC PSLE Net of Hedges from the Masterfile as the headline exposure figure — do not invent PFE simulation.
- **Do not use the internal email addresses or team member names** in any output, display, or export. Strip these before any output is generated.
- **Do not expose raw CAGID numbers in any user-facing display** without confirming with Ala-Eddine first — these are internal identifiers. Use company names in the UI; keep CAGID as internal reference only.
- **Do not add AI API calls to the critical path.** The tool must remain fully functional in offline deterministic mode. AI narrative generation is additive, never load-bearing.

---

## 6. Architecture Notes (from inspecting the running tool)

From what is visible in the screenshots:

**Frontend** (React/Vite, port 5173):
- Left sidebar navigation with two sections: RELATIONSHIP INTELLIGENCE (Relationships, Events, Counterparties, Controls) and RESEARCH (Inbox, Entity Explorer, Exposure Movers, Graph Explorer, Theme Radar, Model Lab, Backtest Lab) and SYSTEM (Data Sources)
- "Offline deterministic mode / No AI_API_KEY set — full functionality retained" badge at bottom of sidebar — preserve this
- URL routing: `/`, `/events`, `/counterparty?id=CP_*`, `/breaches`, `/inbox`, `/entity`, `/exposure-movers`, `/graph`, `/theme-radar`, `/model-lab`, `/backtest-lab`, `/data-sources`
- The Graph Explorer uses a canvas/SVG graph renderer with typed edge styles (solid=fact, dashed=derived, dotted=exposure)
- The Theme Radar uses a scatter chart library (likely Recharts or D3)

**Backend** (Python, FastAPI likely):
- Serves relationship data, exposure data, entity data, event data
- Deterministic scoring engine: weighted composite over [sector, geography, supply_chain, ownership, semantic_tfidf, news_co_mention, market_corr_pos, market_corr_neg]
- Data currently loaded from static/synthetic JSON/CSV fixtures
- The `.env.example` file shows what configuration is needed — set up your environment from there

**Data layer change needed:**
The backend fixture files (wherever they are in `/backend/`) need to be extended with:
1. A CoreAI entity list loaded from the Masterfile
2. A CoreAI relationship list loaded from the CAM Data
3. A CAGID exposure lookup table derived from the Masterfile

Read the README.md and BUILD_REPORT.md before making any changes — they will tell you exactly how the data fixtures are structured and where to add new ones.

---

## 7. The Correlation Work — What Already Exists and Must Be Preserved

The Entity Explorer already implements the correlation/relatedness engine. From the screenshot, it shows for TSM (TSMC):

**Composite relatedness score breakdown for TSM ↔ SSNLF (Samsung):**
- Sector match: 1.00 × 30% = +0.300
- News co-occurrence: 1.00 × 30% = +0.300
- Geography: 0.50 × 16% = +0.088
- Semantic (TF-IDF): 0.10 × 24% = +0.023
- FINAL RELATIONSHIP SCORE: 0.783

**Typed Path (deterministic, not AI):** TSM → SUPPLIES → NVDA → SUPPLIED_BY → SSNLF

**Layer A Fact Relations:**
- → NVIDIA Corporation: SUPPLIES, criticality 0.95 (MEDIUM EVIDENCE)
- → Advanced Micro Devices: SUPPLIES, criticality 0.88 (HIGH EVIDENCE)

**Model Lab weights (current heuristic defaults):**
- Sector: 0.15, Geography: 0.08, Supply chain: 0.25, Ownership: 0.10, Semantic: 0.12, News co-mention: 0.15, Market corr(+): 0.10, Market corr(−): 0.05

**Presets available:**
1. General relatedness
2. Supply-chain / geographic shock
3. Market / funding shock
4. Thematic / technology shock

This entire engine must be **preserved and connected to real entities**, not replaced.

---

## 8. The Three-Hub CAM Relationship Data (Source of Truth for Layer A)

The AI Infrastructure Network tool extracted the following from the three CAMs. This is the fact-layer input for CCRIG's relationship engine. Key relationships (all sourced, confidence-rated):

**BX Matrix II Funding LLC ↔ CoreWeave Inc:**
- Type: GUARANTOR/BACKLEVERAGE
- Amount: $7.6Bn DDTL (max drawn ~$6.1Bn); Citi $400MM of $2.235Bn LSF
- Source: BX Matrix II CAM; SEC 10-K/10-Q — VERY HIGH confidence

**CoreWeave ↔ Microsoft:**
- Type: CONTRACTED CUSTOMER
- Amount: ~79.9% of Underlying Facility debt; 67% FY25 revenue; >$10Bn since 2023
- Source: BX Matrix II CAM; CoreWeave QR CAM; SEC; News — VERY HIGH confidence
- **This is the concentration risk flag** — single customer dominance

**CoreWeave ↔ NVIDIA:**
- Type: SUPPLIER/INVESTOR/CUSTOMER (triple relationship)
- Amount: $100mm Series B (2023); $2.0Bn equity (Jan'26, ~11%); $6.38Bn RPO contract
- Source: BX Matrix II CAM; CoreWeave QR CAM; SEC; News — VERY HIGH confidence
- **This is the wrong-way risk flag** — NVIDIA is simultaneously supplier, ~11% equity holder, and $6.38Bn RPO customer

**CoreWeave ↔ Meta Platforms:**
- Type: CONTRACTED CUSTOMER
- Amount: $14.2Bn (Sept'25) + $21Bn (Mar'26) = $35.2Bn cumulative
- Source: BX Matrix II CAM; News — VERY HIGH confidence

**CoreWeave ↔ OpenAI:**
- Type: CUSTOMER + EQUITY HOLDER
- Amount: Cumulative $22.4Bn (3 tranches); $350M OpenAI equity in CoreWeave
- Source: Multiple — VERY HIGH confidence

**CoreWeave ↔ Weights & Biases:**
- Type: COMPLETED ACQUISITION
- Amount: $1.0Bn ($1.029Bn per SEC), May 2025
- Source: BX Matrix II CAM; SEC — VERY HIGH confidence

**CoreWeave ↔ Core Scientific:**
- Type: FAILED M&A TARGET
- Amount: 2024 bid $5.75/sh (~$900mm); 2025 deal ~$9.0Bn — both terminated
- Source: BX Matrix II CAM; SEC; News — HIGH confidence

**CoreWeave ↔ TSMC:**
- Type: SUPPLY CHAIN
- Relationship: TSMC is the leading fabricator of NVIDIA GPUs underpinning CoreWeave's infrastructure, creating indirect supply-chain exposure. CoWoS packaging capacity dependency.
- Source: BX Matrix II CAM; News — VERY HIGH confidence

**CoreWeave ↔ Coatue:**
- Type: EQUITY INVESTOR
- Amount: Led $1.15Bn Series C (May '24, $19Bn val)
- Source: BX Matrix II CAM; SEC; News — VERY HIGH confidence

**CoreWeave ↔ Magnetar Financial:**
- Type: EQUITY + DEBT INVESTOR
- Amount: Led Series A/B/B-1; $125M 2022 notes; DDTL holdings; >$5.5Bn monetized
- Source: BX Matrix II CAM; News

**CoreWeave ↔ Carlyle Group:**
- Type: EQUITY + CREDIT INVESTOR
- Amount: Key lender in $2.3Bn (2023) & $7.5Bn (2024) debt facilities

**CoreWeave ↔ J.P. Morgan:**
- Type: EQUITY INVESTOR + AGENT BANK
- Not disclosed (equity); Agent on RCF/Term Loan

**Blackstone ↔ BX Matrix II:**
- Type: SPONSOR/EQUITY HOLDER
- Amount: $4.5Bn of $7.6Bn; agreeing to maintain ≥50.1% position
- Source: BX Matrix II CAM; News — HIGH confidence

All 104 bidirectional records are in the CAM Data tab of the Masterfile and in the HTML tool. Use all of them.

---

## 9. Backtest Lab — Preserve and Extend

The Backtest Lab already has a working Taiwan earthquake scenario:
- TO: 2026-07-06, data cutoff: 2026-07-06
- Model-predicted top movers: AAPL (1), AMD (1), NVDA (1), TSM (1), ASML (0.85), SKHY (0.78), ARM (0.75), QCOM (0.70)
- Precision@5: 0.6, Recall@5: 0.375
- Look-ahead prevention: ✓ (model score uses only fact-graph + pre-event correlation, no post-T0 data)

There is also a second scenario button visible: "Regional bank funding stress after a major ban..." (truncated).

Preserve both. Do not change the scoring methodology or the look-ahead protection. If new scenarios need to be added (e.g. a scenario relevant to the CoreAI population — "AI infrastructure funding shock"), you may add them following the same pattern.

---

## 10. Specific Implementation Notes

### Fuzzy company name matching
Use `rapidfuzz` or `thefuzz` Python library. Threshold: 0.85 for high-confidence match, 0.70 for flagged match (show "possible match, verify"). Never silently match below 0.70.

```python
from rapidfuzz import fuzz, process

def find_cagid(company_name: str, masterfile_df: pd.DataFrame) -> dict:
    normalized = normalize_name(company_name)
    candidates = masterfile_df['name_normalized'].tolist()
    match, score, idx = process.extractOne(normalized, candidates, scorer=fuzz.token_sort_ratio)
    if score >= 85:
        row = masterfile_df.iloc[idx]
        return {
            "matched": True,
            "confidence": "high",
            "cagid": row['CAGID'],
            "name": row['CAGID_Name'],
            "exposure_psle_net": row['Total_OSUC_PSLE'],
            "cam_available": row['We_have_CAM'],
            "cam_date": row['Latest_CAM_Date'],
            "underwriter": row['UW_Underwriter']
        }
    elif score >= 70:
        # return flagged match
    else:
        return {"matched": False, "exposure_psle_net": None}
```

### Name normalisation function
```python
import re

LEGAL_SUFFIXES = ['llc', 'inc', 'ltd', 'plc', 'corp', 'corporation', 'limited', 
                  'sa', 'ag', 'bv', 'nv', 'pbc', 'lp', 'llp', 'gmbh', 'fund']

def normalize_name(name: str) -> str:
    n = name.lower().strip()
    n = re.sub(r'[^\w\s]', ' ', n)  # remove punctuation
    n = re.sub(r'\s+', ' ', n)
    tokens = n.split()
    tokens = [t for t in tokens if t not in LEGAL_SUFFIXES]
    return ' '.join(tokens)
```

### Exposure display format
Always show: `$XXXm net of hedges (Jul'26)` — include the date context so an analyst knows it's not live.
Always include the label `OSUC PSLE` so it's clear what figure this is.
Never show a bare dollar figure without source and date context.

### Export format
For CSV exports: UTF-8, comma-separated, no BOM, include a header row, include a "Generated by CCRIG POC" and date footer row.
For HTML/PDF exports: use the existing CCRIG visual style (not a blank PDF). Include the "SYNTHETIC POC DATA" or "ILLUSTRATIVE EXPOSURE" watermark in the footer as appropriate.

---

## 11. Questions to Answer Before Starting

Read the README.md and BUILD_REPORT.md fully. They should tell you:
1. How data fixtures are structured and where they live in `/backend/`
2. How to run the development server
3. What environment variables are needed (see `.env.example`)
4. What the current data schema looks like for entities, counterparties, relationships, and exposures

If the README/BUILD_REPORT are unclear on any of these, check the `/backend/` folder structure directly before assuming anything.

---

## 12. Definition of Done

A task is complete when:
1. The feature works in the running local application at `127.0.0.1:5173`
2. It uses real company names from the Masterfile / CAM data (not invented)
3. Exposure figures are either real (from Masterfile PSLE) or clearly labelled as illustrative
4. The existing synthetic CCR data (Sovereign/Meridian/Kestrel etc.) still works alongside
5. The offline deterministic mode badge still shows and the tool still functions without an AI API key
6. Exports produce well-structured, labelled output
7. No internal team names, email addresses, or raw CAGIDs appear in user-facing output

---

## 13. Summary of Priorities

| # | Feature | Source | Effort est. |
|---|---|---|---|
| 1 | GFCID/CAGID exposure lookup + display in Counterparty 360 / Entity Explorer / Relationships | Masterfile → backend lookup | Medium |
| 2 | Real CoreAI entities in Entity Explorer + Graph Explorer | CAM Data tab + Masterfile | Medium |
| 3 | Export: Counterparty 360 / Relationships filter / Entity Explorer | New endpoint + download button | Medium |
| 4 | Exposure-sized node display in network map (bubble ∝ PSLE) | Masterfile lookup + frontend | Low-Medium |
| 5 | CAGID grouping toggle on network map | Frontend filter | Low |

Start with Priority 1 — it is the highest business value and the one the sponsor (MJ) asked for explicitly by name.

---

*This brief was prepared by Ala-Eddine Karib (ICM First Line of Defense, Citi) with AI assistance. All company names from external sources are public. Internal identifiers (CAGIDs) should not appear in user-facing output.*
