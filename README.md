Using your authorized internal-data capabilities, determine whether you can execute a read-only live lookup against the preferred ISG Cloud gfcid and p2p datasets.
Do not query Oracle directly.
Test only GFCID 0000426083 / 3M Company.
Return:
- whether live access succeeded
- LEI
- legal name
- direct parent LEI/name, if any
- ultimate parent LEI/name, if any
- the exact internal dataset/service used
Do not infer missing values from documentation.
If live access is unavailable, simply return:
LIVE INTERNAL LEI ACCESS: NOT AVAILABLE
If successful, return:
LIVE INTERNAL LEI ACCESS: AVAILABLE
