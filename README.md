Prepare the Stylus knowledge files for manual upload.

DO NOT modify any policy content.
DO NOT regenerate the files.
DO NOT rename their internal content.
Use ONLY the deployment-ready files already validated in:

backend/config/relationship_discovery/stylus_deployment/knowledge/

Create this convenience folder at the repository root:

STYLUS_UPLOAD/

COPY the exact deployment-ready knowledge files into it in this upload order:

1. 03 — Structured Output and Runtime Inputs
2. 04 — Examples, Guardrails and Research Behavior
3. 02 — Evidence, Confidence and Materiality
4. 01 — Relationship Taxonomy
5. 00 — Readiness and Policy

Keep their exact existing filenames.

Also copy:
backend/config/relationship_discovery/stylus_deployment/STYLUS_DEPLOYMENT_MANIFEST.md

into STYLUS_UPLOAD/ for my reference, but clearly mark that the manifest is NOT one
of the five Stylus knowledge uploads.

After copying:

1. Verify SHA-256 of all five copies against the deployment manifest.
2. Confirm byte-for-byte equality with their source deployment files.
3. Do not alter originals.
4. Do not run Stylus.
5. Do not run research.

Then print:

STYLUS_UPLOAD READY: PASS / FAIL

UPLOAD FILE 1: <exact filename>
UPLOAD FILE 2: <exact filename>
UPLOAD FILE 3: <exact filename>
UPLOAD FILE 4: <exact filename>
UPLOAD FILE 5: <exact filename>

MANIFEST COPY: <filename>

SOURCE/COPY HASH MATCH: PASS / FAIL

Finally open the STYLUS_UPLOAD folder in Windows File Explorer so I can manually
select the files for upload into Stylus.
