3. Replace the old large prompt in Stylus. The current one still contains the old CAM authority language. Use the new V1 prompt that VS Code created.
Ask VS Code:
Show me the COMPLETE contents of the final deployment-ready Stylus prompt from:

backend/config/relationship_discovery/stylus_deployment/
LENDING_RELATIONSHIP_RESEARCH_V1_PROMPT.txt

Do not summarize it.
Do not modify it.
Output the exact full text so I can manually copy it into Stylus.

Then copy that entire output into the Prompt box in Stylus.
4. Replace the knowledge files manually.
Ask VS Code:
List the exact deployment-ready V1 Stylus knowledge files under:

backend/config/relationship_discovery/stylus_deployment/knowledge/

Give me:
- exact filename
- exact path
- purpose
- upload order

Do not modify any file.

You should end up uploading the V1 versions of roughly:
00_READINESS_POLICY.md
01_LENDING_RELATIONSHIP_POLICY.md
02_EVIDENCE_CONFIDENCE_MATERIALITY.md
03_STRUCTURED_OUTPUT_AND_RUNTIME_INPUTS.md
04_EXAMPLES_GUARDRAILS.md

If Stylus has a knowledge-file limit and only allows four, tell me before uploading. We can decide which content should be folded into the main prompt.
5. Delete the old knowledge attachments from this preset after you have the new files ready. Do not keep old + new together, because Stylus could receive contradictory CAM and Client-Universe rules simultaneously.
6. For the first test, use:
SubjectEntity:
NVIDIA CORPORATION

RelatedEntity:
[leave empty]

RelationshipScope:
MAXIMUM_RELATIONSHIP_DISCOVERY

SourceChannels:
SEC_FILING,R2D2_WEB,GLEIF

ResearchInstruction:
Discover the maximum defensible material credit-relevant relationships around
the subject. Search broadly but return only policy-compliant findings supported
by explicit evidence. Prioritize ownership, suppliers, customers, financing,
investors, strategic partners, technology dependencies, infrastructure
dependencies and significant contractual relationships. Investigate useful
hidden or indirect paths only where every hop is independently evidenced.

AsOfDate:
2026-09-25

But do not execute that test yet.
First update the prompt + knowledge files. Then send me a screenshot of the updated Stylus configuration. I want to verify that the old CAM wording is gone and the new source channels and hidden-path rules are correctly represented before we spend a run.
