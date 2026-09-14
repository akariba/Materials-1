# CCRIG Phase 2 — Real Data Enrichment via Web Search & LLM
## From: Ala-Eddine Karib, ICM First Line of Defense
## Date: September 14, 2026

---

## 0. Read This First — What Changed and Why

Phase 1 is done and working. The CoreAI Network has real CAM relationship data, real OSUC exposure figures, and the relationship scoring engine is live.

**Phase 2 has one clear goal: replace static and synthetic data with real publicly-available data wherever it genuinely exists — and be honest about what cannot be made real.**

Before building anything, understand the data reality:

| Data type | Publicly available? | Source | Action |
|---|---|---|---|
| Company profiles, sector, geography | Yes | Web search / Wikipedia / company sites | Replace static with live web-fetched |
| Real news about CoreAI companies | Yes | Web search (Reuters, Bloomberg, FT, CNBC) | Replace 34 synthetic news docs with real |
| SEC filings (10-K, 10-Q, S-1) | Yes, via web search through R2D2 | R2D2 web search proxy → SEC.gov | Fetch real filing excerpts per company |
| Public market prices (OHLC) | Yes for listed companies | Yahoo Finance / web | Expand from 14 to all listed CoreAI entities |
| GLEIF LEI corporate hierarchy | Yes | api.gleif.org (already partially done) | Expand to full CoreAI population |
| Real CCR counterparties (named hedge funds, banks, asset managers) | **Partially** — fund names, strategies, AUM are often public | Web search | Replace fictional names with real fund names where verifiable public info exists |
| PFE (Potential Future Exposure) | **No — never public** | Internal systems only | **Keep synthetic. Label honestly.** |
| NSE (Net Stress Exposure) | **No — never public** | Internal systems only | **Keep synthetic. Label honestly.** |
| Utilisation vs limit | **No** | Internal systems only | **Keep synthetic. Label honestly.** |
| ΔPFE (weekly PFE move) | **No** | Internal systems only | **Keep synthetic. Label honestly.** |

**The rule: real data where it exists publicly, honest synthetic where it doesn't. Never fabricate a number and present it as real.**

---

## 1. The LLM Web-Search Layer — How to Use It

The application already has an LLM provider configured (DeterministicProvider offline, OpenAI-compatible when `AI_API_KEY` is set). The LLM has web access.

**Use the LLM for web-search-backed enrichment tasks, not for generating numbers.** Specifically:

```python
# Pattern for LLM-assisted web enrichment
ENRICHMENT_PROMPT = """
Search for current, factual, publicly available information about {company_name}.
Return ONLY information you can verify from real public sources (company website, 
Reuters, Bloomberg, FT, SEC.gov, GLEIF, Wikipedia).

Return as JSON:
{
  "company_name": str,
  "sector": str,
  "headquarters_country": str,
  "business_description": str (2-3 sentences, factual),
  "key_customers": [str],          // named, publicly announced only
  "key_investors": [str],          // from public filings/announcements only
  "recent_news_headlines": [       // max 3, real headlines with dates
    {"headline": str, "date": str, "source": str, "url": str}
  ],
  "sec_filing_available": bool,
  "latest_sec_form": str,          // "10-K", "S-1", "20-F" etc or null
  "latest_sec_date": str,
  "public_ticker": str,            // null if private
  "estimated_aum_or_revenue": str, // only if publicly stated, else null
  "sources_used": [str]
}

If you cannot verify something from a real source, return null for that field.
Never estimate or infer financial figures.
"""
```

**R2D2 as web-search proxy for SEC filings:**
R2D2 has web-search capability that can reach SEC.gov. Use it specifically for:
- Fetching the full-text of a specific SEC filing URL
- Searching EDGAR for a company's filing history
- Extracting specific sections (Item 1 Business, Item 1A Risk Factors) from 10-K filings

```python
# R2D2 web search pattern for SEC filings
def search_sec_filing_via_r2d2(company_name: str, form_type: str = "10-K") -> dict:
    """
    Use R2D2's web search to find and extract SEC filing content.
    Returns filing metadata and key excerpt, not the full document.
    """
    search_query = f"SEC EDGAR {form_type} {company_name} site:sec.gov"
    # Call R2D2 web search endpoint with this query
    # Extract: filing date, CIK, accession number, key business description excerpt
    # Never return more than 500 words of filing text — this is for context only
```

---

## 2. What to Actually Build — Prioritised

### Priority 1 — Real Counterparty Names in the CCR Layer

**The problem:** The Inbox, Exposure Movers, and Counterparty 360 currently use completely fictional counterparty names (Sovereign Debt Office — Nation Alpha, Meridian Alpha Rates Fund, etc.).

**The solution:** Replace these with real, publicly known CCR-relevant counterparty types. Use the LLM with web search to find real named funds, banks, and asset managers that:
- Are publicly known to be active in rates/FX/credit derivatives markets
- Have publicly stated AUM or strategy information
- Are the *type* of entity Citi's CCR team actually monitors

**Do NOT use real Citi client names.** Use real fund/bank names that are publicly known to exist and operate in these markets — not necessarily Citi clients.

```python
# LLM prompt for counterparty research
COUNTERPARTY_RESEARCH_PROMPT = """
Find real, publicly known financial counterparties in each of these categories.
Use only public information (Bloomberg, Reuters, fund databases, public filings).

For each, provide: real name, type, domicile, publicly stated AUM or activity, 
and one public source URL confirming they exist and are active.

Categories needed:
1. Two large sovereign debt offices or central bank treasury desks (rates exposure)
2. Two macro/rates hedge funds (publicly known, $1Bn+ AUM)
3. One large structured equity fund
4. One sovereign wealth fund treasury operation
5. One regional bank treasury (EUR or GBP denominated)
6. Two fixed income asset managers
7. One triparty funding/repo specialist

Return only funds you can verify with a real public source. Return null for 
any you cannot verify. Do not invent or estimate.
"""
```

Once real counterparty names are found and verified, replace the fictional names in the data layer. Keep the same CCR workflow structure (priority tiers, driver classification, breach logic) — only the names and public profile data change.

**PFE/NSE/ΔPFE numbers stay synthetic and labelled.** The names become real; the exposure metrics remain illustrative. Every metric row carries:
```
ΔPFE +900  [Illustrative · not actual exposure]
```

### Priority 2 — Real News for Theme Radar and Entity 360

**The problem:** 34 of 48 news documents are `SYNTHETIC_NARRATIVE` tagged `is_synthetic=true`. This makes the Theme Radar and news co-occurrence signal weak and fake.

**The solution:** Use LLM web search to fetch real, recent news headlines for the CoreAI entity population. Target: 5 real headlines per major entity, properly sourced.

```python
NEWS_FETCH_PROMPT = """
Find the 5 most recent, factually significant news headlines about {company_name}
from the last 6 months. Focus on: business developments, funding, partnerships,
supply chain news, regulatory matters, financial results.

Use only real published sources: Reuters, Bloomberg, Financial Times, WSJ, 
CNBC, TechCrunch, The Information, SEC filings announcements.

Return as JSON array:
[{
  "headline": str,           // exact headline, not paraphrased
  "date": str,               // YYYY-MM-DD
  "source": str,             // publisher name
  "url": str,                // direct URL if available
  "entity_relevance": str,   // one sentence: why relevant to {company_name}
  "is_verified": true        // only true if you have actual URL/source
}]

Return empty array if you cannot find verified headlines.
"""
```

**Run this for:** NVDA, TSM, ASML, AMD, CoreWeave, Anthropic, OpenAI, Microsoft (AI infra angle), NVIDIA supply chain, Blackstone, Meta, Google Cloud, Apple, SK Hynix, Samsung, Qualcomm, ARM.

**Tag all results:** `source_type: REAL_PUBLIC_NEWS`, `is_synthetic: false`. Keep the 34 synthetic docs as fallback — don't delete them until real news coverage is confirmed for each entity.

### Priority 3 — SEC Filing Context via R2D2 Web Search

**The goal:** For each of the 3 hub entities (CoreWeave, BX Matrix II/Blackstone, Anthropic) and top 10 related entities (NVIDIA, TSMC, ASML, Microsoft, Meta, Blackstone, OpenAI, Coatue, Magnetar, Carlyle), fetch:

- Filing type and date (10-K / 10-Q / S-1 / 20-F)
- Business description excerpt (Item 1, ~100 words)
- Key risk factors mentioning counterparties, supply chain, concentration
- Revenue/AUM figure if stated in the filing

**Display in Entity 360 as a new collapsible section:**
```
SEC / PUBLIC FILINGS                              [REAL PUBLIC DATA]
CoreWeave Inc — S-1 — Filed 2026-03-28
"CoreWeave is a specialized AI infrastructure provider..."
[Concentration risk: Microsoft ~79% of revenue as of Dec 2025]
[Source: SEC EDGAR · accession 0001234567-26-000123]
```

### Priority 4 — Expand Real Price History and GLEIF

**Price history:** Currently 14/149 entities have OHLC. Expand to all publicly listed CoreAI entities using Yahoo Finance (already working — just run for more tickers):
- Add: AMD, INTC, AAPL, MSFT, GOOGL, AMZN, META, AVGO, QCOM, ARM, MU, AMAT
- Private companies (CoreWeave, Anthropic, OpenAI, Mistral): explicitly mark as "Private — no public price history" in Entity 360. Do not fabricate prices.

**GLEIF:** Currently 41/149. Run for all 74 public CoreAI entities. Priority: the 46 companies already in the CAM relationship database.

---

## 3. The Synthetic Layer — What Stays and Why

Be honest in the Data & Provenance Explorer. The following stays synthetic and is explicitly labelled:

| Data | Why it stays synthetic | Label to show |
|---|---|---|
| PFE, NSE, RC, ΔPFE, ΔNSE | Never publicly available — internal system outputs only | `Illustrative · not actual exposure` |
| Utilisation vs limit | Same reason | `Illustrative` |
| Breach records (except real breach logic) | Breach data is internal | `Synthetic POC · illustrative workflow` |
| Exposure edges (REPO, TRS, BOND, SEC_LENDING) in Exposure Movers | Product-level exposure by counterparty is internal | `Illustrative product types` |

**One honest label, everywhere, consistently.** Not hidden in footnotes — visible on every row that carries synthetic data.

The existing `is_synthetic=true` flag in the data layer is correct. Make sure the frontend surfaces this flag visibly, not just as metadata.

---

## 4. Updated Data & Provenance Page

After Phase 2, the Data & Provenance Explorer should show:

```
SOURCE                          CLASSIFICATION                    RECORDS   COVERAGE NOTE
--------------------------------------------------------------------------------------------
Real company profiles           REAL PUBLIC DATA (WEB)            74        LLM web-fetched:
(LLM web-enriched)                                                          sector, HQ, business
                                                                            description, investors,
                                                                            customers. Source URLs
                                                                            stored per record.

Real news (LLM web-fetched)     REAL PUBLIC DATA (WEB)            85+       Reuters, Bloomberg,
                                                                            FT, CNBC, WSJ.
                                                                            5 headlines per major
                                                                            entity. Verified URLs.

SEC filings (via R2D2 web       REAL PUBLIC DATA (WEB             ~13       S-1/10-K/20-F excerpts
search)                         SEARCH PROXY)                               for hub + top-10
                                                                            CoreAI entities.

Extended price history          REAL PUBLIC DATA                   60+       Yahoo Finance OHLC.
(Yahoo Finance)                                                             Private companies
                                                                            marked explicitly.

GLEIF LEI records               REAL PUBLIC DATA                   70+       Live-fetched from
                                                                            api.gleif.org.

Real CCR counterparty names     REAL PUBLIC DATA (WEB-            13        Named funds/banks from
                                VERIFIED PUBLIC INFO)                       public sources. AUM/
                                                                            strategy public only.

AI Economy Study Masterfile     REAL INTERNAL SOURCE              75        OSUC PSLE exposure
                                (SANITIZED PRESENTATION)                    figures as before.

CAM relationship network        REAL INTERNAL SOURCE              184       52 source relationships,
                                (SANITIZED PRESENTATION)                    bidirectional.

CCR exposure metrics            SYNTHETIC POC DATA                18 CPs    PFE/NSE/ΔPFE/utilisation
(PFE, NSE, RC, limits)          ⚠️ ILLUSTRATIVE ONLY                        illustrative. Not real
                                                                            exposure data.

Counterparty exposure edges     SYNTHETIC POC DATA                80        Product types (REPO,
(REPO, TRS, etc.)               ⚠️ ILLUSTRATIVE ONLY                        TRS, BOND) illustrative.
```

---

## 5. Architecture — New Module: `enrichment.py`

Create `backend/app/core/enrichment.py`:

```python
"""
enrichment.py — Real data enrichment via LLM web search and public APIs.

Fetches:
- Company profiles (LLM web search)
- Real news headlines (LLM web search)
- SEC filing context (R2D2 web search proxy → SEC.gov)
- Extended price history (Yahoo Finance)

All results are cached locally. Results are tagged with:
- source_type: REAL_PUBLIC_WEB | REAL_PUBLIC_API | REAL_INTERNAL_R2D2_WEB
- is_synthetic: false
- fetched_at: ISO timestamp
- source_url: direct URL where available

Never returns fabricated data. Returns null for fields that cannot
be verified from a real public source.
"""

import os, json, httpx, logging
from pathlib import Path
from datetime import datetime

logger = logging.getLogger(__name__)
CACHE_DIR = Path(".enrichment_cache")
CACHE_DIR.mkdir(exist_ok=True)


def enrich_entity(entity_name: str, ticker: str | None = None) -> dict:
    """
    Full enrichment pipeline for one entity.
    Returns cached result if available and fresh (< 24h).
    """
    cache_key = entity_name.lower().replace(" ", "_")
    cache_file = CACHE_DIR / f"{cache_key}.json"
    
    if cache_file.exists():
        cached = json.loads(cache_file.read_text())
        age_hours = (datetime.now().timestamp() - cached.get("fetched_at_ts", 0)) / 3600
        if age_hours < 24:
            return cached
    
    result = {
        "entity_name": entity_name,
        "fetched_at": datetime.now().isoformat(),
        "fetched_at_ts": datetime.now().timestamp(),
        "profile": fetch_company_profile(entity_name),
        "news": fetch_real_news(entity_name),
        "sec_filing": fetch_sec_context(entity_name),
        "price_history": fetch_price_history(ticker) if ticker else None,
    }
    
    cache_file.write_text(json.dumps(result, indent=2))
    return result


def fetch_company_profile(entity_name: str) -> dict | None:
    """LLM web search for company profile. Returns None on failure."""
    if not _llm_available():
        return None
    try:
        from backend.app.core.llm import call_llm
        prompt = f"""
Search for factual, publicly available information about {entity_name}.
Return only what you can verify from public sources.
Return as JSON with fields:
sector, headquarters_country, business_description (2-3 sentences),
key_customers (list, public only), key_investors (list, public only),
public_ticker (str or null), is_publicly_listed (bool),
primary_sources (list of URLs you used).
Return null for any field you cannot verify.
"""
        response = call_llm(prompt, max_tokens=800)
        parsed = _safe_parse_json(response)
        if parsed:
            parsed["source_type"] = "REAL_PUBLIC_WEB"
            parsed["is_synthetic"] = False
        return parsed
    except Exception as e:
        logger.error(f"Profile fetch failed for {entity_name}: {e}")
        return None


def fetch_real_news(entity_name: str, max_headlines: int = 5) -> list[dict]:
    """LLM web search for real news headlines."""
    if not _llm_available():
        return []
    try:
        from backend.app.core.llm import call_llm
        prompt = f"""
Find the {max_headlines} most recent significant news headlines about {entity_name}
from the last 6 months. Use only real published sources.
Return as JSON array with fields per item:
headline (str), date (YYYY-MM-DD), source (publisher), url (str or null),
is_verified (bool — true only if you have a real URL or confirmed source).
Return empty array if no verified headlines found.
"""
        response = call_llm(prompt, max_tokens=1000)
        headlines = _safe_parse_json(response) or []
        for h in headlines:
            h["source_type"] = "REAL_PUBLIC_NEWS"
            h["is_synthetic"] = False
        return [h for h in headlines if h.get("is_verified")]
    except Exception as e:
        logger.error(f"News fetch failed for {entity_name}: {e}")
        return []


def fetch_sec_context(entity_name: str) -> dict | None:
    """
    Search SEC filings via R2D2 web search proxy.
    Returns filing metadata and short excerpt only — never full document.
    """
    r2d2_url = os.environ.get("R2D2_BASE_URL")
    helix_token = os.environ.get("HELIX_TOKEN")
    
    if not (r2d2_url and helix_token):
        # Fallback: try direct LLM web search for filing info
        return _fetch_sec_via_llm(entity_name)
    
    try:
        query = f"SEC EDGAR 10-K OR S-1 OR 20-F {entity_name} site:sec.gov"
        with httpx.Client(timeout=20.0) as client:
            resp = client.post(
                f"{r2d2_url}/websearch",   # adjust to actual R2D2 web-search endpoint
                headers={
                    "Authorization": f"Bearer {helix_token}",
                    "Content-Type": "application/json",
                },
                json={"query": query, "max_results": 3},
            )
            resp.raise_for_status()
            results = resp.json().get("results", [])
            return _parse_sec_search_results(results, entity_name)
    except Exception as e:
        logger.warning(f"R2D2 SEC search failed for {entity_name}: {e} — trying LLM fallback")
        return _fetch_sec_via_llm(entity_name)


def _fetch_sec_via_llm(entity_name: str) -> dict | None:
    """LLM fallback for SEC filing context when R2D2 unavailable."""
    if not _llm_available():
        return None
    try:
        from backend.app.core.llm import call_llm
        prompt = f"""
Search SEC EDGAR for the most recent public filing by {entity_name}.
Return as JSON:
{{
  "form_type": str,       // "10-K", "S-1", "20-F", "10-Q" etc
  "filing_date": str,     // YYYY-MM-DD
  "cik": str,             // SEC CIK number if findable
  "accession_number": str, // SEC accession number if findable
  "business_excerpt": str, // 100 words max from Item 1 Business section
  "concentration_risks": [str], // specific named customer/supplier concentration mentions
  "sec_url": str,         // direct SEC.gov URL
  "is_verified": bool
}}
Return null if no verified filing found.
"""
        response = call_llm(prompt, max_tokens=600)
        parsed = _safe_parse_json(response)
        if parsed and parsed.get("is_verified"):
            parsed["source_type"] = "REAL_PUBLIC_WEB"
            parsed["is_synthetic"] = False
            return parsed
        return None
    except Exception as e:
        logger.error(f"LLM SEC fallback failed for {entity_name}: {e}")
        return None


def fetch_price_history(ticker: str, period_days: int = 365) -> list[dict] | None:
    """Fetch real OHLC from Yahoo Finance. Returns None for private companies."""
    if not ticker or ticker.upper() in ("PRIVATE", "N/A"):
        return None
    try:
        url = f"https://query1.finance.yahoo.com/v8/finance/chart/{ticker}"
        with httpx.Client(timeout=10.0) as client:
            resp = client.get(
                url,
                params={"range": "1y", "interval": "1d"},
                headers={"User-Agent": "Mozilla/5.0 (compatible; research-poc)"},
            )
            resp.raise_for_status()
            data = resp.json()
            timestamps = data["chart"]["result"][0]["timestamp"]
            closes = data["chart"]["result"][0]["indicators"]["quote"][0]["close"]
            return [
                {"date": datetime.fromtimestamp(t).strftime("%Y-%m-%d"), "close": c}
                for t, c in zip(timestamps, closes) if c is not None
            ]
    except Exception as e:
        logger.warning(f"Price history fetch failed for {ticker}: {e}")
        return None


def research_real_counterparties() -> list[dict]:
    """
    Use LLM web search to find real, publicly known CCR-relevant counterparties
    (sovereign treasuries, macro hedge funds, bank treasuries, asset managers).
    Returns verifiable public information only — no Citi client data.
    """
    if not _llm_available():
        return []
    try:
        from backend.app.core.llm import call_llm
        prompt = """
Find real, publicly known financial entities that are typical counterparties
in the rates, FX, credit derivatives, and repo markets. Use only public info.

For each entity provide:
- real_name: exact legal or commonly known name
- type: sovereign_treasury | macro_hedge_fund | asset_manager | bank_treasury | family_office
- domicile: country
- public_aum_or_activity: publicly stated AUM or activity description
- markets_active_in: ["rates", "fx", "credit", "repo", "equity"] (public info only)
- public_source_url: one URL confirming this entity is real and active
- is_verified: true only if you have a real confirming source

Find at minimum:
- 2 sovereign treasury or central bank desk entities (G10 or major EM)
- 2 well-known macro/rates hedge funds ($5Bn+ AUM, publicly referenced)
- 1 sovereign wealth fund with publicly known derivatives activity
- 2 fixed income asset managers (publicly known, $10Bn+ AUM)
- 1 bank treasury (non-US, publicly active in rates/repo)
- 1 structured credit or equity fund (publicly known)

Return as JSON array. Return only is_verified=true entries.
Do NOT include any entity that could be a Citi client without public confirmation.
"""
        response = call_llm(prompt, max_tokens=2000)
        entities = _safe_parse_json(response) or []
        verified = [e for e in entities if e.get("is_verified") and e.get("real_name")]
        for e in verified:
            e["source_type"] = "REAL_PUBLIC_WEB"
            e["is_synthetic"] = False
        logger.info(f"Found {len(verified)} verified public counterparties")
        return verified
    except Exception as e:
        logger.error(f"Counterparty research failed: {e}")
        return []


def _llm_available() -> bool:
    return bool(os.environ.get("AI_API_KEY") or os.environ.get("AI_BASE_URL"))


def _safe_parse_json(text: str) -> dict | list | None:
    """Parse JSON from LLM response safely, handling markdown code blocks."""
    try:
        import re
        cleaned = re.sub(r"```json\n?|\n?```", "", text).strip()
        return json.loads(cleaned)
    except Exception:
        return None


def _parse_sec_search_results(results: list[dict], company: str) -> dict | None:
    """Parse R2D2 web search results for SEC filing info."""
    sec_results = [r for r in results if "sec.gov" in r.get("url", "")]
    if not sec_results:
        return None
    top = sec_results[0]
    return {
        "form_type": _extract_form_type(top.get("title", "")),
        "filing_date": top.get("date"),
        "sec_url": top.get("url"),
        "excerpt": top.get("snippet", "")[:500],
        "source_type": "REAL_PUBLIC_WEB",
        "is_synthetic": False,
    }


def _extract_form_type(title: str) -> str:
    for form in ["10-K", "10-Q", "S-1", "20-F", "8-K", "SC 13G"]:
        if form in title.upper():
            return form
    return "Filing"
```

---

## 6. Counterparty Name Replacement Logic

Once `research_real_counterparties()` returns verified results:

```python
# In data.py — update the CCR counterparty list

def build_counterparty_roster(web_verified: list[dict]) -> list[dict]:
    """
    Map web-verified real counterparties to CCR display slots.
    METRICS (PFE/NSE/utilisation) remain synthetic — only names and profiles are real.
    """
    slots = [
        # slot_id matches existing routes/IDs in the frontend
        {"slot_id": "CP_PUB_ALPHA",  "priority": "CRITICAL", "required_type": "sovereign_treasury"},
        {"slot_id": "CP_SOV_BETA",   "priority": "HIGH",     "required_type": "sovereign_treasury"},
        {"slot_id": "CP_SOV_GAMMA",  "priority": "HIGH",     "required_type": "sovereign_treasury"},
        {"slot_id": "CP_SOV_DELTA",  "priority": "HIGH",     "required_type": "sovereign_treasury"},
        {"slot_id": "CP_HF_001",     "priority": "HIGH",     "required_type": "macro_hedge_fund"},
        {"slot_id": "CP_FUND_ECR",   "priority": "HIGH",     "required_type": "macro_hedge_fund"},
        {"slot_id": "CP_SOV_EPS",    "priority": "HIGH",     "required_type": "sovereign_treasury"},
        {"slot_id": "CP_BANK_MRID",  "priority": "HIGH",     "required_type": "bank_treasury"},
        {"slot_id": "CP_BANK_002",   "priority": "MEDIUM",   "required_type": "bank_treasury"},
        {"slot_id": "CP_AM_HALC",    "priority": "MEDIUM",   "required_type": "asset_manager"},
        {"slot_id": "CP_AM_BRK",     "priority": "MEDIUM",   "required_type": "macro_hedge_fund"},
        {"slot_id": "CP_QF_KES",     "priority": "MEDIUM",   "required_type": "macro_hedge_fund"},
        {"slot_id": "CP_FO_KES",     "priority": "LOW",      "required_type": "family_office"},
    ]
    
    by_type = {}
    for cp in web_verified:
        t = cp.get("type")
        by_type.setdefault(t, []).append(cp)
    
    result = []
    for slot in slots:
        candidates = by_type.get(slot["required_type"], [])
        real_cp = candidates.pop(0) if candidates else None
        
        result.append({
            "counterparty_id": slot["slot_id"],
            "priority": slot["priority"],
            # If real counterparty found: use real name and profile
            "display_name": real_cp["real_name"] if real_cp else _fictional_name(slot["slot_id"]),
            "type": slot["required_type"],
            "domicile": real_cp.get("domicile") if real_cp else None,
            "public_aum": real_cp.get("public_aum_or_activity") if real_cp else None,
            "markets": real_cp.get("markets_active_in", []) if real_cp else [],
            "source_url": real_cp.get("public_source_url") if real_cp else None,
            "is_real_name": bool(real_cp),
            "is_synthetic_name": not bool(real_cp),
            "source_type": "REAL_PUBLIC_WEB" if real_cp else "SYNTHETIC_POC_DATA",
            # Metrics always illustrative
            "metrics_source": "SYNTHETIC_POC_DATA",
            "metrics_label": "Illustrative · not actual exposure",
        })
    return result
```

---

## 7. Frontend Display Rules

### The One Consistent Label for Synthetic Metrics

Every ΔPFE, NSE, PFE, utilisation, ΔNSE number in the UI must carry this label, consistently:

```tsx
// MetricBadge component — use everywhere a synthetic exposure metric appears
const MetricBadge = ({ value, label }: { value: string, label: string }) => (
  <span className="metric-with-badge">
    {value}
    <span className="illustrative-badge" title="Illustrative figure — not actual exposure data">
      Illustrative
    </span>
  </span>
)
```

Style: small, amber-coloured, non-intrusive. Present on every metric — not buried in a footnote.

### Real vs Synthetic Counterparty Name Display

When a counterparty has a real verified name from web search:
```
J.P. Morgan Asset Management  [Public profile · web-verified]
ΔPFE +900  [Illustrative · not actual exposure]
```

When still using fictional name (fallback):
```
Meridian Alpha Rates Fund  [Illustrative name]
ΔPFE +900  [Illustrative · not actual exposure]
```

The name badge and the metric badge are always shown separately — a real name does not imply real metrics.

---

## 8. Enrichment Run Schedule

The enrichment pipeline is batch, not real-time:

```
On startup (or manual trigger from Data Sources page):
  1. research_real_counterparties() → update counterparty roster
  2. For each CoreAI entity in COREAI_ENTITY_LIST:
     a. fetch_company_profile(entity_name)
     b. fetch_real_news(entity_name, max=5)
     c. fetch_sec_context(entity_name)  [for hub entities + top 10 only]
     d. fetch_price_history(ticker)  [if public ticker known]
  3. Expand GLEIF LEI for all 74 public entities
  4. Regenerate coreai_snapshot.json

Cache: 24h for company profiles and news, 7 days for SEC filings, 1h for prices.
Add "Refresh enrichment data" button to Data Sources page.
```

---

## 9. What Does NOT Change

- `scoring.py` — untouched. The relationship scoring engine is not modified.
- The three-layer architecture (Layer A facts / Layer B derived / Layer C synthetic CCR) — preserved.
- The 166 existing backend tests — must all still pass after this phase.
- CoreAI Network page — already working well, only minor additions (SEC filing context in Entity 360 sidebar).
- The `is_synthetic=true` flag convention — extended, not replaced. New real data is tagged `is_synthetic=false` consistently.

---

## 10. .gitignore Additions

```
.enrichment_cache/
.counterparty_roster_cache.json
```

These contain web-fetched data that should not be committed — regenerated on each run.

---

## 11. Definition of Done

Phase 2 is complete when:

1. At least 8 of 13 CCR counterparty display names are real, web-verified public entities (not fictional). Each has a `[Public profile · web-verified]` badge and a source URL.
2. At least 50 real, verified news headlines exist in the corpus (up from 14), tagged `is_synthetic=false`, with source URLs.
3. SEC filing context (form type, date, business excerpt, key risks) is shown in Entity 360 for CoreWeave, Anthropic, NVIDIA, TSMC, ASML, Microsoft, Blackstone, Coatue, OpenAI, Meta.
4. Price history exists for all 12 listed CoreAI entities with public tickers. Private companies (CoreWeave, Anthropic, OpenAI, Mistral) are explicitly marked "Private — no public price history."
5. GLEIF LEI data covers all 74 public CoreAI entities.
6. Every synthetic metric (PFE, NSE, utilisation, ΔPFE) carries a visible "Illustrative" badge — not just a footnote.
7. Data & Provenance Explorer shows the new classification table as specified in Section 4.
8. All 166 existing backend tests still pass.
9. The application runs correctly with no AI API key set (enrichment disabled, falls back cleanly to existing data).
10. `.enrichment_cache/` is in `.gitignore` and no web-fetched data is committed to the repo.
