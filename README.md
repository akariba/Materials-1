EXECUTE NOW — WORKING CCR SOLUTION + TESTABLE UI
Stop architecture work. Implement the working flow in CCR.
1. Reuse only the proven Stylus access mechanism from RPR
Inspect the existing RPR POC and reuse its already-working:
- Stylus authentication/session handling
- Stylus invocation/API method
- request/response transport
- required configuration
Do not integrate the RPR application itself.
Do not copy RPR business logic, UI, data model, or research rules.
CCR should call Stylus directly using the proven RPR access mechanism.
2. Use the existing Stylus preset
Use:
Lending Relationship Research - Web + SEC
Research behavior:
SEC first → if SEC unavailable/not applicable/insufficient → Web
Use the existing Stylus knowledge/prompt.
No GLEIF requirement for this research execution.
No Olympus work.
No new provider architecture.
3. Add one simple UI action
In the existing selected-client CCR workspace add:
Research Relationships
When clicked:
1. use the currently selected client
2. show the company/GFCID being researched
3. call the backend CCR research endpoint
4. backend invokes Stylus using the reused RPR mechanism
5. show progress/status:
   - Authenticating
   - Researching SEC
   - Researching Web if needed
   - Processing evidence
   - Complete / Failed
Do not build a new screen.
Do not redesign the workspace.
4. Result in the existing UI
When research completes, refresh the current client workspace and display:
- newly accepted factual relationships
- candidate/context findings separately
- source/evidence
- exact passage/excerpt
- source URL/document metadata
- relationship type
- qualifier if present
- coverage/research status
- updated factual network
- updated existing six correlation results
If nothing is accepted, show:
Research completed — no new evidence-backed relationships found.
Do not invent relationships.
5. First working test
Use:
3M Company
GFCID 0000426083
Execute a real end-to-end test:
CCR UI → CCR backend → reused RPR Stylus access → Web+SEC preset → result → CCR ingestion → UI refresh
6. Keep current governance
Do not change:
- Client Universe
- VERIFIED+EXACT identity gate
- relationship ontology
- evidence acceptance rules
- six correlation definitions
- two-hop limit
- existing factual graph semantics
7. Do not stop for normal implementation choices
Make the smallest implementation choice and continue.
Stop only for a genuine blocker:
- Stylus authentication cannot work using the existing RPR method
- Stylus invocation fails
- required source result cannot be returned/retained
- ingestion fails
If blocked, report only:
BLOCKER: <exact issue>
FIX REQUIRED: <smallest fix>
Otherwise continue until I can open CCR, select 3M, click Research Relationships, and see the results.
8. Final report
Report only:
- Stylus access reused from RPR: YES/NO
- backend endpoint implemented
- UI button implemented
- 3M end-to-end execution result
- relationships accepted
- correlations found
- tests passed
- READY FOR USER TESTING: YES/NO
Do not start another architecture review.

Also reuse the proven authentication/token-refresh process from the RPR POC.
Specifically, inspect RPR and reuse the exact existing mechanism for:
- authenticating to Stylus
- obtaining the R2D2 access token
- refreshing/renewing the R2D2 token when expired
- reusing the authenticated session where appropriate
- handling expiry/retry without asking the user to manually copy tokens
Do not invent a new auth flow.
Do not:
- extract browser JWTs manually
- ask me to paste tokens
- hardcode tokens
- save credentials/tokens in source code
- create a second token-refresh implementation
The CCR backend should reuse the same proven RPR auth/session/token-refresh process so that Research Relationships can run repeatedly from the UI without manual token handling.
Verify specifically:
1. exact RPR module/function used for Stylus authentication
2. exact RPR module/function used for R2D2 token acquisition
3. exact RPR module/function used for token refresh
4. token expiry detection behavior
5. retry behavior after refresh
6. how credentials/session state are kept securely
Then wire that existing mechanism into the CCR backend research call.
Expected working flow:
CCR UI → Research Relationships → CCR backend → RPR auth/session mechanism → refresh R2D2 token if needed → invoke Stylus Web+SEC preset → receive results → ingest → refresh UI
Do not stop to redesign authentication if the RPR mechanism already works. Reuse it exactly unless there is a concrete incompatibility.
