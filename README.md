FEATURE 1 ONLY — COREAI INTERACTIVE NETWORK EXPLORER
Work only on the CoreAI correlation HTML template and redesigned CoreAI report.
Do NOT work in PHR.
Do NOT change backend logic.
Do NOT change REL.
Do NOT change the trusted data.
Objective
Turn the existing CoreAI relationship map into a focused interactive Network Explorer using only the existing embedded CoreAI data.
Required behavior
1. Default network
When an entity is selected, display:
- selected entity
- its direct counterparties
- the existing REL edges connecting them
Do not display all 521 nodes by default.
Default depth = 1 hop.
2. Network depth
Add:
- 1 Hop
- 2 Hops
- Full Network
2 Hops must expand only through relationships already present in REL.
No synthetic or inferred edges.
3. Node interaction
Clicking a node must:
- make it the selected entity
- center/focus the graph on it
- update the entity inspector
- update relationship table filtering
- update evidence context
- update existing URL/selection state if already supported
Add an Expand relationships action for the selected node.
4. Edge interaction
Clicking an edge must open an evidence/detail drawer or panel showing the existing trusted fields available for that relationship:
- Company A
- Company B
- relationship type
- relationship/perspective description
- deal / commitment
- Citi indirect exposure
- source
- exact excerpt
- confidence
Do not generate or summarize evidence with AI.
5. Network toolbar
Add only:
Search | 1 Hop / 2 Hops / Full Network | Category | Community | Fit | Reset | Fullscreen
Reuse existing category and community logic.
6. Visual hierarchy
- selected entity = dominant central node
- reference/hub entities = distinguishable
- node color = existing category
- community mode = existing community assignment
- selected edge = visually emphasized
- labels readable without excessive overlap
Preserve the current CoreAI visual identity.
7. Fullscreen
Fullscreen Network must use the entire available browser viewport and retain:
- search
- depth control
- entity inspector
- edge evidence
- category/community switch
Escape/close returns to the normal CoreAI workspace without losing the selected entity.
8. Synchronization
Entity selection must remain synchronized across:
- search
- entity list
- network
- inspector
- relationship table
- evidence
Acceptance test
Use existing trusted entities such as CyrusOne and CoreWeave.
I must be able to:
1. search for CyrusOne;
2. immediately see CyrusOne and its direct relationships;
3. click KKR or another connected node and make it the new focus;
4. click an edge and see its actual CoreAI source/excerpt;
5. switch to 2-hop;
6. return to 1-hop;
7. expand the network fullscreen;
8. return without losing selection.
Preserve exactly:
- 856 canonical REL relationships
- existing entity identifiers
- source/excerpt data
- confidence
- exposures
- categories
- communities
- exports
Do not implement AI Analyst, SEC/Web research, maps, news, stress testing, or new backend APIs in this task.
Deliver the working updated CoreAI HTML so I can test this feature visually.
