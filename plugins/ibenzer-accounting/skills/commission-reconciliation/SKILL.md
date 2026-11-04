---
name: commission-reconciliation
description: Reconcile and prepare iBenzer monthly Kevin or Jordan sales Commission in Google Sheets, including ShipStation freight, domestic-shipment freight, payment eligibility, prior-month formulas, and review-ready formatting. Use for any request to update, verify, or prepare Commission or 未付 records.
---

# Commission Reconciliation

## 公司固定执行与错误闭环
开始此工作流前，先读取 [公司固定规则](../../references/company-operating-rules.md)。该规则适用于本 Skill 的所有步骤；如与当前用户明确指令冲突，以用户当次明确指令为准。

Prepare a reviewable monthly Commission sheet that is accurate before it is described as complete. This skill is for the recurring Kevin/Jordan Commission and 未付 workflow; it is not general accounting or generic spreadsheet cleanup.

## Start every run

### Monthly cadence

- Begin the Kevin and Jordan Commission reconciliation on the 10th of every month. Run the complete preflight before changing either worksheet; this is a start date, not permission to settle an invoice without its payment, SPIFF, ownership, and source-evidence gates.

1. Read `references/commission-playbook.md`, `references/commission-preflight-audit.md`, and `references/error-log.md` completely before editing.
2. Inspect the immediately preceding approved month for the salesperson being processed. Treat it as the source of truth for formulas, grouping, merging, fills, borders, row heights, conditional formats, totals, and signature block.
3. State briefly which live sources will be checked. Do not claim completion until the final formulas, totals, date types, shipping values, and formatting have been re-read from the sheet.

## Operating invariants

- Never invent a freight amount, cost, payment date, received amount, customer classification, or formula result. Mark a genuinely missing value clearly instead.
- Determine actual freight only from ShipStation by Invoice#. If the shipment uses the customer's carrier account (including B&H), leave Actual Shipping blank; this does not block payment/Commission eligibility where the order, payment, and other required data are valid.
- Only freight found in the 运单跟踪记录 domestic-shipment sheet is domestic freight and is colored yellow. Do not infer domestic status from a customer name or location.
- For Kevin domestic orders, preserve full Actual Shipping and divide only AVG SHIPPING by two.
- Build the month from all eligible paid records, not merely those paid during the calendar month: eligibility is paid date + received amount + verified company-paid shipping, with the documented B&H exception.
- Apply the user's established cut-off rule exactly: every record paid before this Commission sheet is prepared belongs in the current run if a duplicate audit across all earlier Commission tabs for that salesperson finds no prior occurrence. The calendar month of payment is not an exclusion rule. Record the duplicate-audit result before excluding a paid record.
- Keep all paid records in 未付 at the top until the user has reviewed and explicitly authorized deletion. Keep unpaid records below.
- Preserve every user-applied green customer marking and its existing fill: it is the authoritative visual classifier for a new customer. Never clear, recolor, or infer a replacement classification during cleanup.
- When a related SPIFF program applies, read the SPIFF tracker by Invoice# before settling Commission. Populate the verified SPIFF amount in the workbook's SPIFF field and retain its tracker status/evidence. An invoice is not eligible for Commission settlement until SPIFF has actual payment evidence: a paid status and payment date/reference. `已发出`/a check number alone is a payment-pending hold, not proof of payment; customer Paid Date alone is also not sufficient.
- Treat `Seller Commissions` and `SPIFF` as distinct fields. Before any cleanup, reconcile every nonblank value in either field to its authoritative source. If a legacy `Seller Commissions` value equals the verified SPIFF tracker amount, move it to the SPIFF field after readback; never use the Seller Commissions column as temporary SPIFF storage.
- When the user authorizes removal of settled records from 未付, delete only complete Invoice groups that have a verified Commission-settlement basis. A completed monthly Commission tab's signed/paid block (amount, paid date, and payment reference) is the authoritative payout evidence; its listed Invoice groups control deletion. SPIFF paid/issued evidence is a prerequisite only, never a substitute for actual Commission payout evidence.
- A row belongs to exactly one salesperson's 未付 and Commission sheet. When correcting ownership, move it in both places, recompute totals, and verify neither copy remains.
- Before retaining, assigning, or settling any row, perform an ownership triage: (1) the current Offline Report salesperson, (2) the customer State against the approved territory map, and (3) the established customer owner in historical Commission records and CRM. A documented customer-owner history may override a territory only when the evidence is explicit. If the three signals conflict, do not move the row or pay it: add a concise Notes exception, set `Commission Status` to `归属待确认`, state the next confirmation action, and exclude it from settlement. Once State is populated, Notes must not duplicate the bare state code or `XX SALES` label.
- Before payout or SPIFF reconciliation, canonicalize the Invoice# against its source record. If two rows share the same SKU, quantity, amount, and date but use different Invoice#s, never assume two sales: preserve the user-confirmed canonical Invoice#, remove only the confirmed duplicate group, and hold the retained row if customer/SPIFF/QBO evidence conflicts.
- Do not populate Paid Date or Received Amount from a merely similar QBO result. Match the correct QBO Invoice Number/reference, customer, invoice amount, and date first. If the mapping is wrong, clear the imported payment fields, record the correct QBO reference in Notes, and keep the row unpaid until the correct QBO invoice shows payment.
- Preserve formulas. A displayed number is not an adequate substitute for a formula.
- Standard Unit Price is a Commission cost input, not automatically the Reseller selling price. Use the matching salesperson's Database plus the approved annual SKU/model source; where the sources do not establish the cost, flag it and do not substitute MSRP, Base Price, or a guessed historical value.
- Invoice 197459 (Acer) is a three-person Commission: retain the normal applicable customer formula and divide its resulting Commission by 3 on both Kevin and Jordan sheets. The row must be present for both people and visibly annotated as three-person Commission.
- Do not treat an exception/audit tab as a substitute for reconciliation. Before declaring a run complete, trace every disposition through source evidence, the relevant 未付 row, the Commission row and formula, the total, and the recommended payout; an audit tab may summarize this result only after those elements agree.
- For every manually shown Commission amount, link to the underlying Commission formula whenever possible. Never report or persist a hand-calculated rounded amount without matching it to the live formula result.

## Formula and layout requirements

Use the matching salesperson's approved prior-month formulas and the column positions in that workbook. Read the detailed formula map in `references/commission-playbook.md`; do not transpose Kevin formulas to Jordan or vice versa.

- Apply the active low-rate conditional-format rule so a Commission percentage below 5% is red.
- For any customer where the approved minimum-5% policy applies, change the Commission formula to the minimum-5% formula; do not merely color the cell red. Add the approved explanatory note.
- Group rows in review order: ordinary/established customers first, green new customers grouped by customer, then purple SPIFF/special rows. Keep same-customer rows adjacent.
- Customer colour/category and the associated formula must come from that salesperson's immediately preceding approved sheet or an explicit user marking; never infer a new-customer, SPIFF, or special category from a customer name.
- Restore the complete prior-month visual system: header, line borders, merged multi-SKU cells where needed, correct row heights, colored Notes cell, total row, percentage total, legend, signature/payment block, and currency/date formats.
- Treat `未付` as a decision-ready management queue, not a raw ledger. Its active rows must have uniform Invoice Date/Paid Date formats, integer quantity, currency amount columns, named State and Record Type fields, and visible Commission Status plus Next Action. Use the approved monthly Commission tab as the visual reference for field order and readability, while retaining only the operational fields needed before payout. Headers must never inherit a date or currency format.
- Before delivery, scan every active Notes cell for an unambiguous U.S. state abbreviation and compare it with the State field. Fill State only when exactly one explicit state code is present; otherwise flag it rather than guessing. Re-read the complete exception list after the write. When ShipStation shows `Third Party` with no cost, record Actual Shipping as `$0.00`, note the carrier-billing evidence, and recheck the linked Commission formula.
- If a Date cell is a text look-alike, convert it to a genuine date serial and recheck filtering/eligibility.
- An aggregate Commission-rate KPI must name its denominator and use one consistent basis. Do not compare a cash-basis aggregate (Commission ÷ received amount) with row rates computed on net eligible revenue. Before delivery, re-read the KPI formula and independently recompute numerator ÷ denominator from the live totals; if it is merely informational, label the basis or omit it.
- After any edit that adds, moves, or replaces a Commission summary/review formula, re-read every summary cell in that panel using its effective value. Do not deliver or use the panel as a record while any `#REF!`, `#VALUE!`, `#DIV/0!`, or formula error remains. Verify that summary totals equal the itemized decision rows.
- A Commission task is not complete merely because the named cell was changed. Before delivery, perform the linked completion sweep: source/field mapping, Invoice-group completeness, SPIFF prerequisite, payout evidence, active `未付` cleanup, historical-month preservation, formula/totals, and user-defined colour semantics. Report any true exception rather than waiting for a follow-up prompt.
- Include display QA in that completion sweep: check a representative first, middle, and exceptional row for readable dates, quantity, currency, State/Type labels, Commission Status, and next action; compare the visual hierarchy with the completed monthly Commission tab.
- Do not treat a correction named by the user as the scope boundary. Before returning a changed Commission workbook, execute the whole preflight audit and surface every material exception that remains; only make financial/ownership changes when the evidence is unambiguous or the user has authorized the decision.

## Completion and upkeep

Before finishing, run the checklist in `references/commission-playbook.md`, then append a short dated entry to `references/error-log.md` describing any discovered failure, root cause, correction, and prevention. If no failure is discovered, log a successful verification instead.

The log is a living control record: update it after every use of this skill. Keep it factual and concise.


