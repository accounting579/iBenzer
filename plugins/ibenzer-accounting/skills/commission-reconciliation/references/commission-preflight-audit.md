# Commission preflight audit

Use this full checklist for every Kevin/Jordan Commission or `未付` change. It exists because individual cell fixes have repeatedly concealed linked source, ownership, formula, and presentation failures.

## 1. Establish the review set

- Identify active `未付` invoice groups and every month/Commission tab whose payout can still affect the requested period.
- Re-read the actual header row and sheet IDs before any batch write. Never rely on a previous column map after a sort, copy, or layout change.
- Compare the immediately preceding approved month before changing layout, row grouping, borders, colors, number formats, totals, or signature/payment blocks.

## 2. Reconcile every active invoice group

For each Invoice#, create a source trail before it becomes payout-ready:

1. Offline Report: invoice, salesperson, customer/state, SKU/quantity, and sales amount.
2. CRM and historical Commission records: established customer owner where territory and source salesperson conflict.
3. QuickBooks: invoice/customer amount and settled evidence when the sheet/payment evidence is inconsistent.
4. ShipStation/transport ledger: actual company-paid freight; distinguish carrier-account, Third Party `$0.00`, domestic ledger freight, and genuinely missing evidence.
5. SPIFF tracker: exact amount plus actual paid status and payment date/reference, where applicable. A check merely issued is not paid.
6. Completed Commission payment block: actual Commission settlement evidence; it is separate from customer payment and SPIFF.

An unresolved source does not become a guessed number or owner. Mark the exact issue, next source/action, and prevent settlement.

## 3. Ownership gate

- Compare Offline Report salesperson, State territory, and established customer owner.
- A proven historical owner can override territory; an unproven conflict cannot.
- A conflict gets `归属待确认`, a concise evidence note, a next action, and no payout. Do not transfer the group without confirmation.
- The State field is the only location label. Do not repeat a bare State/`XX SALES` suffix in Notes.

## 4. Financial and formula gate

- Verify genuine date types, amount columns, price source, SPIFF placement, freight treatment, formula class, formulas, rate denominator, line total, monthly total, and payout/payment block.
- Search formula/effective-value output for errors (`#REF!`, `#VALUE!`, `#DIV/0!`, malformed dates, typed-over formula cells).
- Reconcile the list of settled groups to the paid/signed Commission block before removing them from `未付`.
- Apply the user's rolling inclusion rule: nonduplicated records paid before the sheet is prepared belong in the current run; do not use calendar month as a silent exclusion.

## 5. Presentation and data-quality gate

- Preserve protected green customer cells and their meaning. Do not infer or replace the classification.
- Use color only for defined business meanings. In particular, State cells use one neutral fill; exception/payout colors live in their dedicated status fields.
- Confirm line-group borders/merges, row heights, Notes wrapping, width, date/currency/quantity formats, totals, signature/payment block, and first/middle/exceptional rows visually match the approved month.

## 6. Delivery rule

Report: (a) corrected items, (b) held exceptions with evidence and next action, (c) formula/total validation, and (d) the scope actually audited. Never describe a workbook as fully confirmed while any material gate remains unresolved.

## Actual recurring failures and the control that prevents each one

| Failure actually observed | Required control |
| --- | --- |
| Correcting only the cell named by the user while linked rows/source checks were skipped | Run every gate in this preflight before delivery. |
| A paid Invoice group left in `未付` after the signed monthly Commission payout | Compare every active `未付` Invoice# against every paid monthly group, then delete only complete matching groups. |
| Near-duplicate rows use different Invoice#s despite the same date/SKU/quantity/amount | Canonicalize the Invoice# from the source; retain the user-confirmed group only and hold it if customer/SPIFF/QBO fields disagree. |
| Paid Date or Received Amount came from a wrong QBO invoice match | Match QBO reference, customer, amount, and date together; clear the false payment data and retain the verified QBO reference in the exception note. |
| SPIFF treated as proof that sales Commission was paid, or placed in Seller Commissions | Verify SPIFF separately; use the monthly paid/signed block as Commission-payout proof; reconcile the two fields before editing. |
| Wrong owner retained because source salesperson, territory, and customer history were not reconciled | Apply ownership triage and hold conflicts; never silently transfer or pay them. |
| Freight guessed, B&H/Third Party treated as ordinary freight, or domestic freight misapplied | Use ShipStation/ledger evidence only; record customer-carrier blank, Third Party `$0.00`, and domestic treatment exactly. |
| Incorrect Commission formula, denominator, minimum-rate treatment, or total after copying/sorting | Re-read live formulas and effective values, then independently reconcile all row and summary totals. |
| State kept only in Notes, State duplicated in Notes, or State formatting had accidental colour meaning | Populate the dedicated State field from evidence, remove redundant suffixes, and use one neutral State fill. |
| Date/quantity/currency type or display inconsistency obscured eligibility and review | Check real date types and standard number formats in first, middle, total, and exception rows. |
| Visual cleanup broke invoice grouping, protected green customer markers, or usability | Preserve green fills; verify merges/borders/row heights/wrapping against the approved prior month. |
