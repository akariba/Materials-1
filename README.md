Stop the manual Stylus handoff workflow. We want to test the actual Stylus preset automatically with minimal human interaction.
Goal: one command should execute the frozen Stage 7 Stylus pilot for all eligible entities and collect/validate the outputs.
First, do discovery only
Inspect the existing Stylus integration/assets/configuration and determine whether the actual preset:
Lending Relationship Research - Web + SEC + GLEIF
can be invoked programmatically through, in priority order:
1. official API
2. CLI/internal service endpoint
3. authenticated HTTP endpoint already used by the Stylus UI
4. supported browser automation
Do not create a fake local implementation that merely runs the prompt text. We want to test the real preset/runtime, including its configured knowledge, tools and source-channel behavior.
If an authenticated session/token is required, allow me to provide/login once locally. Never store credentials in Git, source code, reports, fixtures, or logs.
If a supported automation route exists, implement a Stage 7 batch runner
Suggested entry point:
backend/scripts/run_stage7_stylus_batch.py
It must use the existing frozen Stage 7 selection manifest and execute exactly these seven jobs:
- ROOT_3M
- KNOWN_3M_INDIA
- KNOWN_SOLVENTUM
- KNOWN_CABOT
- UNRESOLVED_AEARO
- UNRESOLVED_3M_BELGIUM
- UNRESOLVED_BNY_TRUSTEE
EPA remains excluded according to the existing frozen policy.
For every job, supply the existing six governed runtime inputs:
- SubjectEntity
- RelatedEntity
- RelationshipScope
- SourceChannels
- ResearchInstruction
- AsOfDate
These inputs must come from the existing frozen request matrix. Do not reconstruct them manually or change their semantics.
Automation requirements
One command should:
1. validate the frozen selection fingerprint
2. validate the preset/version being invoked
3. submit all seven jobs
4. wait/poll for completion where required
5. capture the raw Stylus JSON response for each job
6. validate the expected Stylus output structure
7. preserve underlying source URLs/document identifiers/excerpts returned by Stylus
8. record failures/retries without silently converting them into zero-result research
9. save the seven raw outputs under a deterministic Stage 7 results directory
10. generate a run manifest containing job status, timestamps, hashes and preset/runtime metadata
11. package the results into:
CCR_V1_STAGE_7_STYLUS_RESULTS_FROZEN_FB4CBB2017875A2D.zip
12. optionally invoke the existing controlled ingestion/validation step after all required jobs succeed.
Do not treat Stylus itself as the evidence source. The underlying SEC filing, approved Web source or GLEIF record remains the evidence source.
Safety constraints
- same frozen eight-entity pilot
- same seven Stylus jobs
- no Stage 8
- no new correlation definitions
- no ontology changes
- no loosened identity/evidence gates
- no synthetic relationships
- no automatic promotion of ambiguous Client Record matches
- do not modify the Client Universe
- preserve query-time correlation evaluation
If automation of the actual preset is not technically available
Stop. Do not revert immediately to seven manual runs.
Report exactly:
- what interface Stylus exposes
- what you inspected
- why programmatic invocation is unavailable
- whether authenticated browser automation is possible
- the minimum one-time human action required to enable automation
Then wait for me.
Do not give me another manual seven-job procedure.
