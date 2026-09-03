The best solution is not to replace CIK with one other identifier. Use an identity-resolution hierarchy and only use SEC when the company can be proven to be an SEC registrant.

For your RPR, I would use:

Ticker + exchange — strongest practical alternative. Resolve AAPL + NASDAQ, for example, to the SEC registrant and then obtain the CIK internally.
Exact legal entity name + country — normalize suffixes such as Inc./Ltd./PLC, then search SEC registrant names and historical names. Accept only a strong/exact match.
LEI / ISIN / CUSIP if Step 2.2 has them — use them as identity anchors through an internal/reference mapping to the public issuer, then resolve the SEC registrant.
Parent/public issuer mapping — if Step 2.2 contains a subsidiary but the SEC filer is its listed parent, only map it when the relationship is explicitly evidenced. Never guess from similar names.
If none resolves: classify the company as NON_SEC_OR_UNRESOLVED and stop SEC searching. Use Web Search / company website / rating-agency or other approved evidence instead.

The key design should therefore be:

Step 2.2 identity → ticker/LEI/ISIN/legal-name resolution → confirmed SEC registrant → internally resolve CIK → SEC filings

rather than:

no CIK → keep asking SEC repeatedly.

For a company like Carry1st, if it is genuinely private and not a periodic SEC filer, there is nothing useful to “fix” in SEC. Step 2.5 should recognize that quickly, record “No confirmed SEC periodic-reporting registrant”, and switch to the Web evidence path.

I would also tell Claude to create an explicit identity status such as:

SEC_CONFIRMED
SEC_PARENT_CONFIRMED
NON_SEC_CONFIRMED
SEC_IDENTITY_UNRESOLVED

That would prevent the 18-search / 40-minute behavior you just saw.
