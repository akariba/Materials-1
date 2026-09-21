CCR RELATIONSHIP CORRELATION — PHASE 3A
EXTERNAL CONNECTIVITY REMEDIATION + PROVIDER ACTIVATION

You are working inside the CURRENT CCR repository in VSCode on Windows.

CCR ONLY.

This is a focused remediation pass.

DO NOT proceed to Phase 4.
DO NOT implement AI Create Relationship yet.
DO NOT build relationship scoring.
DO NOT build the graph.
DO NOT modify Stylus.
DO NOT create synthetic evidence.
DO NOT weaken TLS/security controls.

Read first:

backend/data/CCR_RELATIONSHIP_PHASE3_EXTERNAL_RESEARCH_REPORT.md

Inspect all Phase-3 implementation files, especially:

backend/scripts/migrate_ccr_phase3.py
backend/scripts/run_ccr_phase3_research.py
backend/scripts/report_ccr_phase3.py
backend/tests/test_ccr_phase3_external_foundation.py

and all provider/config files added in Phase 3.

==================================================
1. OBJECTIVE
==================================================

Phase 3 architecture passed.

However the live bounded pilot failed because:

GLEIF:
- 10 network attempts
- 0 verified
- every attempt returned URLERROR

SEC:
- network requests occurred
- no identity/reference data successfully retrieved

WEB:
- provider not configured

The objective of this pass is:

A. determine the exact root cause of GLEIF/SEC URL failures;

B. repair external connectivity WITHOUT weakening security;

C. prove official GLEIF and SEC retrieval works;

D. rerun the bounded Phase-3 pilot;

E. determine the correct path for high-quality Web research;

F. make Phase 4 ready only if external evidence acquisition is genuinely usable.

==================================================
2. PRESERVE EVERYTHING THAT ALREADY PASSED
==================================================

Do not redesign Phase 3.

Preserve:

- 19 additive Phase-3 tables
- source_policy_registry
- research_runs
- provider_cache
- external_identity
- sec_entity_map
- sec_submission_records
- sec_filing_metadata
- gleif_entity_map
- gleif_relationship_observations
- gleif_reporting_exceptions
- source_documents
- evidence_snippets
- all cache semantics
- all safety rules
- explicit-run requirement
- Phase-2 immutability

Do not drop or rebuild these tables unless a migration defect is actually proven.

==================================================
3. FIRST: CAPTURE THE EXACT ERROR
==================================================

The current report only says:

URLERROR

That is insufficient.

Run ONE diagnostic request to GLEIF and ONE diagnostic request to SEC.

Capture the complete exception chain safely.

For each failure report:

provider
URL host
exception class
exception message
nested reason class
nested reason message
errno if available
HTTP status if available
TLS/SSL error if available
DNS error if available
proxy error if available
timeout flag

Do NOT expose:
- credentials
- proxy passwords
- email addresses unnecessarily
- tokens
- secrets

Persist normalized error diagnostics.

Examples of possible classes that must be distinguished:

socket.gaierror
ConnectionRefusedError
TimeoutError
ssl.SSLCertVerificationError
urllib.error.URLError
urllib.error.HTTPError
ProxyError
certificate chain error

Do not treat all of these as URLERROR.

==================================================
4. VERIFY OFFICIAL BASE ENDPOINTS
==================================================

Use only official endpoints.

GLEIF base:

https://api.gleif.org

SEC API base:

https://data.sec.gov

SEC archive/reference host where needed:

https://www.sec.gov

Do NOT substitute third-party mirrors.

For SEC submissions the official pattern is:

https://data.sec.gov/submissions/CIK##########.json

with a zero-padded 10-digit CIK.

Do not test random invalid CIKs merely to make connectivity look successful.

For GLEIF use:

https://api.gleif.org/api/v1/lei-records/<VALID_LOCAL_LEI>

using one of the existing 8,009 valid local LEIs.

==================================================
5. OPERATING-SYSTEM NETWORK DIAGNOSTICS
==================================================

Determine whether failure exists at:

DNS
TCP
TLS
HTTP
Python runtime
application/provider layer

Run bounded diagnostics.

On Windows, where available:

Resolve-DnsName api.gleif.org
Resolve-DnsName data.sec.gov

Test-NetConnection api.gleif.org -Port 443
Test-NetConnection data.sec.gov -Port 443

Then perform simple HTTPS HEAD/GET tests with PowerShell where appropriate.

Do not flood endpoints.

Maximum:
1–2 requests per host for diagnostics.

Record whether:

DNS PASS/FAIL
TCP 443 PASS/FAIL
OS HTTPS PASS/FAIL

==================================================
6. PYTHON NETWORK DIAGNOSTICS
==================================================

Using the SAME Python interpreter/venv as the application, test:

A. socket DNS resolution
B. TLS connection
C. urllib request
D. requests/httpx request ONLY if already installed/used

Determine:

Python version
OpenSSL version
certificate paths
default verify paths

Report:

ssl.get_default_verify_paths()

Also inspect package versions where relevant:

certifi
requests
urllib3
httpx

Do NOT install arbitrary packages unless necessary.

==================================================
7. PROXY / CORPORATE NETWORK DETECTION
==================================================

This machine may be behind a managed corporate network.

Inspect safely whether the environment defines:

HTTP_PROXY
HTTPS_PROXY
NO_PROXY
ALL_PROXY

Also inspect standard Windows proxy configuration where safely possible.

DO NOT print credentials contained in proxy URLs.

Mask sensitive portions.

Report only:

HTTP_PROXY configured: YES/NO
HTTPS_PROXY configured: YES/NO
NO_PROXY configured: YES/NO
system proxy detected: YES/NO

Determine whether:

PowerShell succeeds but Python fails

or:

both fail

This distinction is critical.

==================================================
8. CERTIFICATE TRUST DIAGNOSTICS
==================================================

If the failure is SSL certificate verification:

DO NOT use:

verify=False
ssl._create_unverified_context()
PYTHONHTTPSVERIFY=0
disabled certificate checks

These are forbidden.

Instead determine whether the environment needs:

- normal OS certificate trust
- certifi refresh
- corporate root CA bundle
- SSL_CERT_FILE
- REQUESTS_CA_BUNDLE

If a corporate CA is required but not available in the repository:

do not fabricate it.

Return:

CORPORATE_CA_REQUIRED

and document the required user/environment action.

Never commit private corporate CA files unless explicitly approved.

==================================================
9. SEC USER AGENT
==================================================

Verify that all SEC requests include an appropriate declared User-Agent.

Do not reveal personal contact details in the report.

Configuration may contain environment-variable references such as:

SEC_USER_AGENT
SEC_CONTACT_EMAIL

but never commit real sensitive values.

SEC provider must fail clearly with:

SEC_CONFIGURATION_INCOMPLETE

if mandatory identification configuration is absent.

Do not silently substitute:

Mozilla/5.0

or a fake identity.

==================================================
10. SEC RATE LIMIT
==================================================

Preserve:

default = 5 requests/second

and hard maximum:

10 requests/second

Do not increase this during diagnostics.

Official SEC APIs are public and do not require API keys, but automated access
must follow SEC fair-access requirements.

==================================================
11. DIAGNOSTIC MATRIX
==================================================

Generate a matrix:

                    GLEIF       SEC
DNS                 PASS/FAIL   PASS/FAIL
TCP 443             PASS/FAIL   PASS/FAIL
OS HTTPS            PASS/FAIL   PASS/FAIL
Python TLS          PASS/FAIL   PASS/FAIL
urllib              PASS/FAIL   PASS/FAIL
application client  PASS/FAIL   PASS/FAIL
cache               PASS/FAIL   PASS/FAIL

For each FAIL provide:

ROOT CAUSE
FIX APPLIED
or
EXTERNAL ACTION REQUIRED

==================================================
12. FIX APPLICATION NETWORKING ONLY IF JUSTIFIED
==================================================

If the defect is inside the application/provider code:

fix it.

Examples:

malformed URL
bad URL joining
incorrect headers
bad timeout handling
proxy not inherited
wrong SSL context construction
bad content negotiation
incorrect encoding
incorrect GLEIF path
incorrect SEC path

Do not rewrite working architecture.

Add regression test for each real defect found.

==================================================
13. GLEIF PROVIDER VERIFICATION
==================================================

After connectivity works, perform a tiny acceptance test first.

Use ONE actual existing valid LEI from canonical CCR data.

Retrieve:

legal entity record

Confirm:

HTTP success
JSON parsed
returned LEI equals requested LEI
legal name present where source supplies it

Then test Level-2 retrieval according to actual current GLEIF API capabilities.

Do not assume every LEI has a parent.

Distinguish:

PARENT_FOUND
NO_PARENT_REPORTED
REPORTING_EXCEPTION
NOT_APPLICABLE
API_ERROR

Never report NO_PARENT_REPORTED as an error.

Never create a fake parent.

==================================================
14. GLEIF PILOT RERUN
==================================================

Only after the single-record test passes:

rerun the existing deterministic 10-client GLEIF pilot.

Do not expand it.

Report:

attempted
HTTP successful
identity verified
identity conflicts
direct parent found
ultimate parent found
reporting exceptions
no-parent cases
errors
cache hits

Persist retrieved authoritative data using the existing Phase-3 tables.

==================================================
15. SEC CONNECTIVITY VERIFICATION
==================================================

Do not begin with fuzzy CCR identity matching.

First verify the SEC platform itself works.

Use an official SEC reference resource suitable for CIK/entity mapping.

Confirm:

HTTP success
User-Agent present
content returned
cache write successful
second call served from cache where appropriate

Then test one known valid record FROM THE OFFICIAL SEC REFERENCE DATA.

Do not hardcode a famous company merely as business data.

It may be used as a technical fixture only if obtained from the SEC mapping
itself during the test.

==================================================
16. SEC DISCOVERY DESIGN REVIEW
==================================================

The previous pilot executed only 4 of 10 planned SEC discovery cases.

Determine WHY.

Classify the six not attempted as:

INSUFFICIENT_LOCAL_IDENTITY
NO_US_JURISDICTION_SIGNAL
PILOT_SELECTION_RULE
UPSTREAM_CONNECTIVITY_STOP
OTHER

Do not call this a failed match if it was never attempted.

Fix reporting so:

ATTEMPTED
NOT_ATTEMPTED
FAILED
NOT_FOUND

are distinct.

==================================================
17. SEC PILOT RERUN
==================================================

After connectivity is proven:

rerun the deterministic Phase-3 SEC pilot.

Maximum 10 clients.

Use official SEC reference data and local matching first.

Report separately:

selected
eligible
attempted
verified CIK
candidate CIK
ambiguous
not found
not attempted
errors

For VERIFIED CIKs only:

retrieve submissions metadata.

Do not retrieve large numbers of filings.

For acceptance:

maximum 1–2 recent relevant filing metadata records per verified pilot entity.

Metadata only is sufficient at this point unless one bounded filing is needed
to prove the document acquisition path.

==================================================
18. WEB PROVIDER — DO NOT FAKE THIS
==================================================

Current status:

WEB_PROVIDER_CONFIGURED = NO

Do not hide this.

Inspect CURRENT CCR repository/environment for an APPROVED existing Web
research runtime.

Search for configuration only in this current repository/environment:

R2D2
WEB_PROVIDER
WEB_SEARCH
SEARCH_API
BING
GOOGLE
SERP
OPENAI_WEB
EXTERNAL_RESEARCH

Do not inspect Lending or other repositories.

If an approved provider is already available:
wire it through the Phase-3 WebResearchProvider abstraction.

If none exists:
leave provider unconfigured.

Do NOT add:
- random scraping
- browser automation against search-engine HTML
- unofficial Google scraping
- arbitrary free search APIs
- hardcoded search results

Return clearly:

WEB_PROVIDER_ACTIVATION_REQUIRED

==================================================
19. WEB PROVIDER CONFIG CONTRACT
==================================================

Even if unconfigured, ensure the provider interface supports environment
configuration.

Do not hardcode credentials.

Expected generic concepts:

WEB_PROVIDER
WEB_API_KEY
WEB_ENDPOINT
WEB_MODEL_OR_ENGINE if applicable
WEB_TIMEOUT_SECONDS
WEB_MAX_RESULTS

Actual variables may depend on the approved provider.

No credentials in git.

==================================================
20. WEB SOURCE POLICY REMAINS IN FORCE
==================================================

Do not weaken Phase-3 source tiers.

Tier 1:
authoritative/primary

Tier 2:
high-quality established secondary

Tier 3:
corroborative specialist

Inadmissible:
must remain inadmissible.

Search results/snippets are NOT evidence.

Underlying retrieved source required.

==================================================
21. EVIDENCE CLEANUP
==================================================

Current Phase-3 report shows:

source_documents = 4
all SOURCE_NOT_VERIFIED

Inspect these.

Do not delete them merely because retrieval failed.

Their failure state is valuable audit history.

Ensure a successful rerun creates NEW properly linked retrieval state rather
than rewriting history misleadingly.

Research runs must remain auditable.

==================================================
22. PROVIDER CACHE
==================================================

After successful connectivity test prove:

first request:
CACHE_MISS
NETWORK_REQUEST = 1

second logically identical request:
CACHE_HIT
NETWORK_REQUEST = 0

Test separately for:

GLEIF
SEC

Do not require Web while provider is unconfigured.

==================================================
23. REPORTING IMPROVEMENT
==================================================

The Phase-3 report was too coarse because all connectivity failures became
URLERROR.

Improve reporting permanently.

Provider errors should now include categories:

DNS_ERROR
TCP_ERROR
TLS_CERTIFICATE_ERROR
PROXY_ERROR
TIMEOUT
HTTP_403
HTTP_404
HTTP_429
HTTP_5XX
MALFORMED_URL
PARSE_ERROR
PROVIDER_NOT_CONFIGURED
UNKNOWN_NETWORK_ERROR

Keep original low-level exception available in technical logs, sanitized.

==================================================
24. TESTS
==================================================

Retain all 27 existing tests.

Add tests for:

1. malformed provider URL classification
2. DNS error classification
3. TLS certificate error classification
4. timeout classification
5. HTTP 429 classification
6. proxy-aware behavior where applicable
7. security verification cannot be disabled via config
8. SEC User-Agent is always present
9. SEC rate maximum remains 10
10. cache eliminates duplicate network request
11. failed research history is preserved
12. rerun creates new research run
13. NOT_ATTEMPTED != NOT_FOUND
14. GLEIF no-parent != failure
15. reporting exception != failure
16. canonical Phase-2 data remains immutable

If live integration tests are added:

mark them separately from unit tests.

They must not make the normal offline test suite fragile.

==================================================
25. CONNECTIVITY REPORT
==================================================

Create:

backend/data/CCR_PHASE3A_CONNECTIVITY_REPORT.md

Include:

ROOT CAUSE
WINDOWS NETWORK DIAGNOSTICS
PYTHON NETWORK DIAGNOSTICS
PROXY STATE
TLS STATE
GLEIF TEST
GLEIF PILOT
SEC TEST
SEC PILOT
WEB PROVIDER STATUS
CACHE VALIDATION
ERROR TAXONOMY
FILES CHANGED
TESTS
REMAINING BLOCKERS

Do not expose secrets.

==================================================
26. PHASE 4 READINESS RULE
==================================================

Set:

PHASE 4 READY = YES

only if:

A. Phase-2 regression still passes

AND

B. at least one authoritative external provider is genuinely functional

AND

C. identity/source retrieval produces verifiable records

AND

D. no synthetic evidence was used

AND

E. source policy remains enforced.

Preferred state:

GLEIF functional
SEC functional

Web may remain:

PROVIDER_NOT_CONFIGURED

provided this is explicit.

However do NOT claim full external-research readiness while Web is absent.

Use:

PHASE_4_CORE_READY

and separately:

WEB_RESEARCH_READY

==================================================
27. FINAL RESPONSE FORMAT
==================================================

Return exactly:

CCR PHASE 3A CONNECTIVITY: PASS / FAIL

ROOT CAUSE
GLEIF:
SEC:
WEB:

DIAGNOSTIC MATRIX
GLEIF DNS:
GLEIF TCP:
GLEIF TLS:
GLEIF Python:
GLEIF application:

SEC DNS:
SEC TCP:
SEC TLS:
SEC Python:
SEC application:

PROXY
System proxy:
Python proxy:
Corporate CA required:

GLEIF
Single-record test:
Pilot selected:
Pilot attempted:
HTTP success:
Verified identities:
Direct parents:
Ultimate parents:
Reporting exceptions:
No-parent cases:
Errors:
Network requests:
Cache hits:

SEC
Reference-data retrieval:
Pilot selected:
Eligible:
Attempted:
Not attempted:
Verified CIK:
Candidate:
Ambiguous:
Not found:
Errors:
Submission metadata retrieved:
Network requests:
Cache hits:

WEB
Provider configured:
Provider type:
Activation required:

CACHE
GLEIF cache test:
SEC cache test:

SAFETY
TLS verification disabled: 0 / FAIL
Synthetic evidence: 0 / FAIL
Canonical Phase-2 mutations: 0 / FAIL
Automatic GET research: 0 / FAIL
Dense pair generation: 0 / FAIL

TESTS
Existing Phase-3 tests:
New tests:
Total passed:
Failed:

REPORT:
backend/data/CCR_PHASE3A_CONNECTIVITY_REPORT.md

PHASE_4_CORE_READY:
YES / NO

WEB_RESEARCH_READY:
YES / NO

If PHASE_4_CORE_READY = NO:
list only genuine blockers.

STOP.
