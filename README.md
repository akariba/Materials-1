Focused live-access check — Olympus / OOD only.
We have access to a database/platform called Olympus, through OOD (Olympus On Demand).
Determine whether Olympus/OOD contains or exposes the internal LEI/GLEIF data corresponding to:
- AMCDATA.LEI_GENERAL_INFO
- AMCDATA.LEI_LEI_REL
- the governed gfcid entity dataset
- the governed p2p hierarchy/relationship dataset
Do not perform another broad documentation review.
I need to know whether these data are actually queryable through Olympus/OOD.
Check specifically for datasets/tables/views containing:
- GFCID
- LEI
- legal name
- entity status
- DIRECTPARENT
- ULTIMATEPARENT
- direct parent LEI
- ultimate parent LEI
If accessible, return:
1. exact Olympus database/catalog/schema/table or view name
2. whether it is live/current data or a replicated snapshot
3. refresh frequency/as-of field if available
4. exact join key to GFCID
5. whether both entity identity and parent hierarchy are available
6. whether I have read access through OOD
Then perform one read-only lookup only for:
GFCID = 0000426083
Return actual retrieved values only:
- GFCID
- LEI
- legal name
- direct parent LEI/name if present
- ultimate parent LEI/name if present
- dataset/table/view used
- as-of/update timestamp if present
Do not infer missing values from documentation.
Do not query Oracle/AMCDATA directly.
Do not request new access.
Do not modify anything.
Finish with exactly:
OLYMPUS/OOD LEI ACCESS: AVAILABLE / NOT AVAILABLE
OLYMPUS/OOD LEVEL-2 HIERARCHY: AVAILABLE / NOT AVAILABLE
3M LIVE LOOKUP: SUCCESS / FAILED
