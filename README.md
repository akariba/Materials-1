FEATURE 2 — AI Analyst
Add a right-side AI Analyst panel to the existing CoreAI workspace.
Reuse the existing CoreAI/R2D2 LLM path.
Context sent to AI must come only from the currently selected entity and existing trusted CoreAI data:
- REL
- counterparties
- relationship descriptions
- exposure
- source
- excerpt
- confidence
- identifiers
First version needs only:
- Summarize this entity
- Explain key relationships
- free-text question box
Every factual answer must reference the existing source/excerpt where available.
No SEC/Web research yet.
No map.
No stress testing.
No backend redesign.
Do not touch Feature 1.
Implement directly in the CoreAI template and regenerated CoreAI HTML.
Return when I can select CyrusOne, open AI Analyst, ask “What are CyrusOne’s key relationships?” and get a grounded answer from the existing CoreAI data.
