Do one very small Lending geography cleanup only.

Identify the ONE unmatched portfolio country label from the completed world-map reconciliation.

1. Report:
   - exact portfolio country label
   - closest GeoJSON country name
   - GeoJSON ISO_A2
   - GeoJSON ISO_A3

2. If the match is unambiguous, add ONE explicit normalization alias.

3. Re-run country reconciliation.

Acceptance:
- Portfolio country labels = 88
- Matched = 88
- Unmatched = 0
- OSUC reconciliation still PASS
- world map still renders
- no external map calls
- no other UI changes
- V1/V2/V3 unchanged
- backend unchanged
- CCR untouched

Then STOP.
