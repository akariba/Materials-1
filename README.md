Use the same RPR method that already works in this environment. Do not invent a new Stylus authentication or execution path.
For the remaining Stage 7 SEC_FILING + R2D2_WEB research:
- Reuse the existing RPR execution method/workflow already used successfully in this workspace/project.
- Reuse its existing authentication/session handling.
- Reuse its existing research invocation pattern and output capture.
- Do not build a new browser-login mechanism.
- Do not extract or persist JWTs/browser tokens.
- Do not create another SEC helper or PowerShell credential flow.
- Do not change the frozen Stage 7 manifest, fingerprint, population, ontology, or evidence gates.
- Do not add GLEIF to Stylus/RPR; GLEIF remains with the existing audited CCR backend provider.
First inspect the repository and identify the exact existing RPR implementation/path that previously worked. Do not approximate it or replace it.
Then use that same RPR method to execute the existing Stage 7 Web + SEC research requests from the frozen request matrix.
Before running anything, report:
1. the exact RPR module/script/service you found,
2. how it authenticates,
3. how it invokes research,
4. how it captures the underlying SEC/Web source artifacts,
5. why it can be reused without changing Stage 7 governance.
If it is the same established RPR method, proceed with the first frozen Stage 7 research job only and stop after producing its raw output and retained source artifacts.
Do not start Stage 8.
