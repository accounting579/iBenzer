# iBenzer Commission Playbook

## Source order

1. The salesperson's latest approved month: exact formulas, placements, format, merges and colors.
2. ShipStation: actual company-paid shipping by Invoice#.
3. 运单跟踪记录: domestic freight only. Yellow indicates this exact source, not merely a domestic destination.
4. 未付: payment, received amount, customer notes, and the working record.
5. Database / approved salesperson records: standard unit price or other cost data.

## Eligibility and freight

Include an order in the working monthly Commission only when it has a genuine paid date, received amount, and verified company-paid freight. B&H is the documented exception: it can be included when paid/received because the customer pays shipping with its own account; Actual Shipping remains blank and is not yellow.

Do not delete the paid item from 未付 until user approval. Sort paid work rows first, unpaid rows afterward.

## Formula maps

Always check the previous approved month because columns can change. The established 2026–27 maps are:

### Jordan

- Ordinary/white: `=(E-Q)*0.05*D`; rate `=R/(F-Q*D)`.
- Green self-developed customer: `=$P*0.05*$D+($E-$P-$Q)*0.3*$D`; rate `=R/F`.
- SPIFF: `=(E-1-Q)*D*0.05`; rate `=R/{(E-1-Q)*D}`.
- Total rate: `=R_total/L_total`.

### Kevin

- Green self-developed customer: `=$P*0.05*$D+($E-$P-$Q)*0.3*$D`; rate `=R/F`.
- Approved minimum-5% row: `=E*0.05*D`; rate `=R/F`; add `未满足5%，按照5%计算`.
- Domestic: Actual Shipping stays full; AVG SHIPPING is the normal freight-per-unit result divided by 2.

Use the actual sheet's columns and references, not these literals blindly.

## Before delivery checklist

- [ ] Every freight amount is sourced from ShipStation or documented domestic tracking; nothing is guessed.
- [ ] Domestic freight is yellow and only domestic freight is yellow.
- [ ] B&H freight is blank, unyellowed, and Commission treatment is correct.
- [ ] All paid/received/eligible rows were considered, including payments outside the month when that is the active policy.
- [ ] Each row is assigned to the correct salesperson in both monthly Commission and 未付.
- [ ] Paid dates are true dates, not text.
- [ ] Cost/standard price is sourced; unresolved data is flagged rather than calculated speculatively.
- [ ] Formulas, rates, total, and summary values are live formulas and have been re-read after edits.
- [ ] Low percentage rule is installed and minimum-5% cases use the approved formula, not just a red fill.
- [ ] Grouping, merged cells, borders, currency/date formats, color, signature block and totals match the approved prior month.
