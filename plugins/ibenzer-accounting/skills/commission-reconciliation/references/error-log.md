# Commission control log

This is a living log. Add one dated entry after every use of `commission-reconciliation`.

## 2026-10-29 — State-column visual consistency correction

- **What happened:** Jordan 未付 State cells inherited a mixture of white and pale-gray backgrounds from legacy row formatting, even though State has no color semantics.
- **Correction and verification:** Reset the State field's active value cells to white only, preserving all borders, State values, protected green Notes fills, and business-status colors in their own columns. Re-read V2:V40: every populated State cell now has an identical white background.

## 2026-10-28 — State-field and third-party-freight completeness correction

- The first `未付` presentation pass left explicit state codes embedded only in Notes (including Jordan `197929` = SD and `197945-6` = KS), while the dedicated State field was blank. It also retained $374.83 Actual Shipping on Jordan `198032` despite ShipStation showing Third Party billing and no carrier cost.
- Re-scanned all active Kevin and Jordan Notes for explicit U.S. state abbreviations, populated the missing State values (17 Kevin, 9 Jordan), and verified no identifiable state remains absent from State. Corrected `198032` Actual Shipping to `$0.00`, documented the ShipStation Third Party evidence in Notes, and retained the order as unpaid rather than inventing freight.
- Prevention: every final 未付 sweep now compares Notes-derived explicit state codes against State and treats a ShipStation Third Party/no-cost result as verified zero freight, never as an estimated carrier charge.

## 2026-10-28 — 未付 presentation rebuild

- User correctly identified that the remaining `未付` tabs were not decision-ready: State/Type data had no headers, dates and quantities used inconsistent number formats, and payment progress could not be read without manually interpreting source columns.
- Rebuilt the operational presentation without changing protected green customer markings or source values. Added State, Record Type, Commission Status, and Next Action headers; normalized Invoice Date/Paid Date, quantities, and currency formats; and added status colors only in the new management-status field.
- Corrected the visible 197236 quantity display from a date-like `6/24/1901` to its unchanged numeric value 541. Verified representative rows: Kevin 198022 shows SPIFF issued/pending Commission settlement; Kevin 197236 is held by Kevin instruction; Jordan rows distinguish customer-payment pending from paid/in-review.

## 2026-10-28 — Field-mapping and completion-sweep correction

- The Kevin `未付` sheet contained a pre-existing `Seller Commissions` amount of $25.50 for Invoice 198022. It matched the SPIFF tracker exactly, proving it was a SPIFF amount held in the wrong column rather than a seller-commission value. Moved it to `SPIFF` and cleared `Seller Commissions`; Kevin 197236 had already been corrected to SPIFF $541.00.
- A narrowly scoped cleanup initially treated only the named SPIFF condition as the whole task. Prevention: every Commission update now requires a linked completion sweep across fields, invoice groups, SPIFF status, payout evidence, `未付` lifecycle, monthly-payment record, formulas, and protected green customer markings.

## 2026-10-28 — Payout-evidence correction

- Initially removed only three invoice groups by treating SPIFF paid/issued status as the Commission-settlement record. This was incorrect: SPIFF is a prerequisite, while the paid/signed monthly Commission table is the authoritative proof that the sales Commission itself was paid.
- Corrected the cleanup from the actual September payment records: Kevin $3,634.99 via W/T dated 10/26 and Jordan $2,581.46 via Zelle dated 10/26. Removed all Invoice groups listed in those paid September Commission tables from `未付` (Kevin 26 and Jordan 11, counting the prior removals).
- Restored Kevin Invoice 198022 because it had SPIFF CK#3190 but did not appear in the paid September Commission list. Prevention: use the monthly Commission paid block and its Invoice list for deletion; never infer Commission payment merely from SPIFF status.
- **2026-10-29 follow-up:** A full historical paid-block-to-`未付` comparison found four remaining paid groups missed by the earlier removal pass: Kevin `197901`, `197956`, `198030` (Kevin August paid block, W/T $5,172.77 on 9/28) and Jordan `197930` (Jordan August paid block, Zelle $7,464.85 on 9/28). Removed each complete Invoice group and re-read the active `未付` lists: there is now no overlap with either August or September paid Commission group. The original “all Invoice groups” wording was therefore too broad; the permanent control is an invoice-by-invoice overlap test, not a claimed completion count.

## 2026-10-28 — SPIFF-gated Commission cleanup

- User authorized deletion from Kevin/Jordan `未付` only for settled Commission invoice groups. Used the SPIFF tracker—not customer Paid Date—as the evidence source: Jordan 197525 (`已支付`, CK#3142), Kevin 197620 (`已发出`, CK#3187), and Kevin 198022 (`已发出`, CK#3190) were removed as complete invoice groups.
- Kept all unissued, unpaid, and evidence-pending SPIFF invoices in `未付`; populated Kevin 197236's verified SPIFF amount of $541.00. The remaining Jordan SPIFF amounts were already present and matched the tracker.
- Applied minimal cleanup to both `未付` sheets: standardized the header, column widths, and Notes wrapping without overwriting user-applied green customer markers.
- Verified that the three deleted Invoice# values no longer occur in either `未付` table and that Kevin 197236 displays SPIFF $541.00.

## 2026-10-15 — Initial retrospective controls

### Failures found

- Used incomplete or unverified freight, including assigning freight where the customer used its own carrier account; B&H freight must remain blank.
- Missed ShipStation-searchable invoices and domestic-tracking freight; some valid paid rows were omitted from the monthly Commission.
- Treated displayed paid dates as valid without checking their data type, which caused paid records to be missed in sorting/filtering.
- Misunderstood eligibility as payment occurring in September rather than the current settlement set of paid, received, freight-verified records.
- Removed or misplaced existing 未付 records instead of keeping all paid items at the top for review and unpaid items below.
- Assigned some invoices to the wrong salesperson and changed only one sheet instead of both monthly Commission and 未付.
- Applied formulas from the wrong salesperson/month, used wrong percentage denominators, and substituted fixed values or malformed formulas.
- Colored low Commission % cells without changing approved minimum-5% formulas.
- Applied domestic-freight handling incorrectly: the full Actual Shipping must stay visible; only Kevin AVG SHIPPING is halved.
- Built a visually inconsistent sheet: missing merges, uneven rows, misplaced summary/legend blocks, missing conditional formatting, weak grouping, and inconsistent date/currency formatting.
- Declared work complete before re-reading formulas, totals, dates, and formatted output; a transferred row later had column-shift and total-range mistakes.

### Controls adopted

- Follow the source order, formula map, and delivery checklist in `commission-playbook.md`.
- Treat prior approved month as the visual and formula template for that salesperson.
- Verify data types and formulas with a post-write read, including each changed row, total row, and payment summary.
- Move ownership in both sheets and search both workbooks to confirm exactly one surviving copy.
- Keep unresolved inputs visibly flagged; do not make numerical assumptions.

## 2026-10-15 — Skill created and initial correction

- Created `commission-reconciliation` as the mandatory workflow for future Kevin/Jordan Commission and 未付 work.
- Corrected a cross-salesperson invoice transfer that initially introduced column misalignment and an incomplete total range; the skill now requires post-write verification of each moved row, its total, summary amount, and ownership search in both workbooks.

## 2026-10-15 — Jordan revised customer markings

- User supplied a revised Jordan customer-color classification. Reconciled formula class to the marking: green = new-customer formula, white = ordinary formula, purple = SPIFF formula.
- A first batch write used the wrong assumed column sequence and temporarily targeted the State column. It was immediately restored; the prevention control is to re-read the actual header layout before every formula batch, especially where a hidden/blank-header State column separates Notes from Commission %.
- Jackson County Central Schools has no Database cost. It remains marked as a new customer but is temporarily calculated at the approved 5% minimum until a verified cost is available.
- Post-write verification confirmed Notes, State, Commission, Commission %, formulas, and total: $2,204.52.

## 2026-10-15 — Jordan Jackson cost and reordering correction

- User had entered Jackson County Central Schools' verified standard cost of $17.00. Removed the incorrect missing-cost/minimum-5% warning and restored the green new-customer formula: Commission $111.38, 6.64%.
- The sheet had been re-sorted between reads. A stale row-number-based total range excluded the first rows; corrected it to sum every active line. Prevention: locate and update records by Invoice#, then re-read the total formula after any sort/reorder.

## 2026-10-15 — Acer three-person Commission

- Added Invoice 197459 to both Jordan and Kevin September Commission from their existing 未付 records. Jordan uses ordinary Commission net of actual freight, then divides by 3 ($181.74); Kevin uses its ordinary 5%-of-sales formula, then divides by 3 ($197.50).
- Inserting a top-of-list row changed Kevin's total-row position and exposed a blank spacer row. Repaired the total, rate, Sales Commission, Total Paid, and Amount references. Prevention: after any row insertion, locate the actual total row by formula/value rather than assuming its old row number, then verify all linked summary cells.

## 2026-10-15 — Formula legend cleanup and Acer annotation sync

- Rebuilt Jordan September's auxiliary formula legend into one compact, bordered six-row classification table, preserving each pre-existing formula description and its white/yellow/green/purple visual category. Removed duplicated and scattered helper content only from the user-designated W:AA legend area.
- Jordan Invoice 197459 was left unchanged after the user completed it: its ordinary-customer, freight-net Commission formula remains divided by three. Copied its explicit three-person Commission annotation to Kevin Invoice 197459 only; verified both rows' formulas and amounts remained intact (Jordan $181.74; Kevin $197.50).

## 2026-10-20 — Commission automation design review

- Reviewed the 2026-10-15 Commission requirements. No financial cells were changed. The required control design is: evidence-first reconciliation, a separate exception queue, user approval for policy choices, then formula-driven monthly output with a review report. A monthly total must remain provisional until its period, payment evidence, freight source, ownership, formula class, and exception status are all verified.

## 2026-10-20 — Evidence-based rules and input inventory review

- Reviewed Kevin August and Jordan August completed sheets, both current Database tabs, and the existing monthly structure. Confirmed that the Database is salesperson-specific rather than a shared price list: e.g., DS06C-KL-01 is $15.00 in Kevin's Database and $7.50 in Jordan's. Future automation must therefore query the matching salesperson Database and flag conflicting/missing SKUs rather than overwrite either value.
- Identified blank fields that are structurally optional (Shipping Income, Discount, SPIFF, Tax) versus evidence-required before ordinary inclusion (Paid Date, Received Amount, Actual Shipping or documented B&H exception, Standard Unit Price for margin-based formulas). No sheet values were changed.

## 2026-10-20 — September clean-review copies

- Created separate `9月重做审核版` tabs for Kevin and Jordan by duplicating the entire live September sheets before any review-layer work; original September and 未付 sheets remain untouched and every original row/formula is preserved in the copies.
- Added a non-financial review-status column only. It identifies September-payment candidates, October cross-month rows, and earlier-payment items requiring a documented catch-up basis. A first status write miscounted two adjacent multi-SKU October orders; post-write verification found the mismatch immediately and the statuses were rebuilt by Invoice group and genuine paid date. Financial formulas and values were not changed.

## 2026-10-20 — Annual price sources and controlled database

- Imported the full 338-row `Reseller Price (Internal)` SKU price source and the 126-row `Price sheet & Models` cost-history source into dedicated source tabs in both Kevin and Jordan Commission workbooks. The first source reference omitted the final `M` from the supplied spreadsheet ID and caused a `#REF!`; this was corrected by re-reading the live browser URL and replacing the failed import with verified static source values.
- Added `Commission逻辑` and `SKU价格映射` control tabs. Existing Database values and Commission formulas were not overwritten: the two salespersons already have conflicting historical values for some exact SKUs (for example `DS06C-KL-01`), and the annual sources contain both SKU-level reseller prices and model-level cost history. Exact price replacement requires a verified SKU-to-model/price-source mapping; unmatched legacy values are explicitly flagged `待年度价格源匹配` rather than guessed or silently unified.

## 2026-10-21 — Annual-source standard-price completion

- Found five blank `STANDARD UNIT PRICE` lookups in Kevin September. The missing SKUs are Neon Party products. The annual model cost table lists ordinary Neon Party at $10.50; the annual Reseller source independently lists the four exact Neo SKUs at $10.50. `LC-NPT-AT13-RQ+1` is a verified naming alias of source SKU `LC-NPT-AT13-KK-RQ+1`, also $10.50.
- Added the five verified $10.50 SKU prices to both Kevin and Jordan Database tabs. Kevin September's existing VLOOKUP formulas now populate every previously blank standard-price cell without replacing formulas. Updated the SKU mapping control to show exact annual-SKU matches, the one confirmed alias, and remaining unmatched entries separately.

## 2026-10-21 — Review-copy scope clarification

- Re-checked the purpose of the `9月重做审核版` tabs against the live September tabs. They are duplicated September sheets with a non-financial review-status column; they were not a full reconciliation or a rebuilt, approval-ready Commission version.
- The status review covered Invoice-grouped paid-date timing only: September-payment candidates, October cross-month items, and earlier-payment catch-up items. It did not verify every ShipStation/运单 freight amount, B&H exception, payment/received/eligibility completeness, customer class, formula/rate, ownership, merge/layout, conditional formatting, totals, or signature block.
- Prevention: a sheet may be called a “审核版” only when its audit checklist and completed evidence checks are written in the sheet; otherwise label it explicitly as a “筛选/待核对副本”.

## 2026-10-21 — Audit-control rebuild started

- Added a separate `9月审核控制` tab to both Kevin and Jordan workbooks. It preserves the original September sheets and shows one invoice per line with the current paid/received/freight/price/Commission values, the applicable B&H or domestic-freight rule, settlement gate, and the exact next evidence source required.
- Corrected an initial audit-tab formula-layout failure before delivery: dynamic source data and audit tests must occupy separate columns; all rows now show their source value and status without `#REF!` or formula-parse errors.
- Verified Invoice 197459 in ShipStation using both Quick Search and Order# Advanced Search. No matching 2026 invoice was found; the advanced result was an unrelated 2020 Amazon order containing the same digits. Both audit tabs now explicitly require the original freight evidence for its $945.67 shipping instead of treating it as verified.

## 2026-10-21 — Scope corrected: all paid records, three material tests only

- User clarified that Commission work is a rolling settlement: start with every record that has a Paid Date, regardless of the payment month, because freight may arrive months later. Rebuilt both `9月审核控制` tabs directly from all paid Invoice rows in `未付`, rather than from the prior month-filtered review copy.
- Reduced the control tab to the only material audit fields: Actual Shipping, Standard Unit Price, AVG Shipping, existing Commission, freight evidence rule, price-source check, and the salesperson-specific formula check. Removed payment-period screening as an audit criterion.
- The Standard Unit Price column now looks up the relevant salesperson Database by SKU for review; a populated value is explicitly "待年度 SKU/型号来源核对", not claimed as independently verified.

## 2026-10-21 — Evidence audit continued

- Re-read the live domestic-shipment ledger rather than relying on colour or prior entry: Invoice 197734 is documented in 头程物流账单 at USD $136.38 and Invoice 197620 at USD $222.52. Both amounts match Kevin's 未付 Actual Shipping; Kevin's AVG SHIPPING remains the full freight per unit divided by two only.
- Re-read ShipStation for Invoice 197665: the shipped FedEx Ground record shows Total Cost $31.36 on the IBENZER shipping account, matching 未付. Also recorded the user-supplied ShipStation evidence for Jordan 197930 ($15.74) and 198054 ($23.50).
- Do not promote these rows to final settlement merely because freight was verified. Standard Unit Price source and the salesperson-specific Commission formula must each be independently reconciled first. The audit-control tabs retain those gates as unresolved until that evidence is present.

## 2026-10-21 — September concise review rebuild

- Replaced the two ChatGPT-created `9月重做审核版` tabs with new `9月佣金核对` tabs in Kevin and Jordan’s live Commission workbooks. The new tabs are direct copies of the original September sheets; existing Commission formulas and totals were preserved, while non-review calculation and auxiliary-legend columns were hidden.
- Added a clearly formatted `例外 / 待核对` helper column. It flags the Acer three-person Commission, B&H customer-paid shipping, domestic freight, missing verified freight (except B&H), missing standard cost, and a Commission rate below 5%. An initial draft incorrectly paired B&H with a missing-freight alert; that rule was corrected and re-read. Prevention: carrier-account exceptions must short-circuit any missing-actual-shipping test.
- Re-read the retained formulas and totals: Kevin $3,670.27; Jordan $2,451.40. These remain review versions, not a declaration that all underlying source evidence is final.

## 2026-10-21 — Bottom-up September reconciliation findings

- The first concise-review pass was not a source-level confirmation. Reconciled the live September tabs against `未付`, the salesperson-specific Database, the immediately prior available Commission sheet, and `头程物流账单`; removed the prior ChatGPT-created `9月审核控制` tabs.
- Kevin: Invoice 197459 has $945.67 Actual Shipping only in Commission, not `未付`; 197665 has SKU `LC-HPE2-A13T-BKI` in `未付` versus `LC-HPE2-A13T-BK` in Commission; 197901 has Received Amount $2,463.30 in `未付` versus $705.60 in Commission. Invoice 197993 is tagged domestic but has no `头程物流账单` invoice match. These items are explicitly non-confirmed, not silently accepted.
- Kevin Invoice 198022 has paid/received/freight inputs and Database cost $14.30 but is absent from September; customer formula class and ShipStation-source freight still need confirmation, so it was not added or calculated speculatively.
- Jordan: every existing September Commission invoice matches its `未付` key fields. Invoice 197969 has paid/received/freight inputs and Database cost $14.50 but is absent from September; it remains a candidate pending prior-settlement and formula-class proof. Invoice 197930 was found in 8.26 and was therefore not duplicated.
- Created compact `9月待确认` tabs for exact exceptions and candidate rows. Existing Commission formulas and totals were left unchanged; do not call either salesperson's September Commission fully confirmed until the listed evidence is resolved.

## 2026-10-21 — QuickBooks confirmation for Kevin Invoice 197901

- QuickBooks identifies the relevant customer as `Y & S Technologies Inc` and shows a single 2026 invoice for that customer: invoice date 2026-08-06, invoice total $705.60, balance $0.00, PO 26247, reference 0197890, location `Kevin`, and 42 units at $16.80. This independently confirms that $705.60 is the invoice/commission revenue basis.
- The number `197901` is not the QuickBooks document number: its document-number search returned no record. Treating it as a QuickBooks internal transaction ID returned an unrelated 2020 Amazon invoice for $15.59. Prevention: never resolve a commission invoice by bare QBO internal ID when the sheet value is an operational invoice number; anchor matching on customer/date/PO/reference as well.
- The previously listed $2,463.30 in `未付` cannot be the invoice total for this sale and must not be used as the Commission received amount. The QBO invoice is fully settled, but the available QBO response does not provide a posting/payment date; the sheet's 2026-09-17 paid date remains a separate payment-evidence field until traced to its receipt/deposit record.

## 2026-10-21 — Exception-column simplification

- Removed the repeated `B&H 自付运费` output from the Kevin September review column. B&H is a normal documented carrier-account rule, not an exception requiring action. The helper formula still excludes B&H from missing-freight alerts, while genuine action items such as three-person Commission, unverified freight, missing cost, low rate, and domestic-freight flags remain. Re-read the affected helper formulas and the total Commission formula; total remains $3,670.27.

## 2026-10-21 — Invoice 197665 SKU root-cause confirmation

- Reconciled Kevin Invoice 197665 across QuickBooks, Nutshell, 未付, and the September Commission row. QuickBooks shows Haywood County Schools, 2026-06-03, 50 × $23.20 = $1,160.00, location Kevin, item `LC-HPE2-A13T-BK`; Nutshell’s corresponding won opportunity 0197665 is `HPE at13-bk *50`. Both independent systems support `BK` without the trailing `I`.
- Corrected only 未付 row 3 SKU from `LC-HPE2-A13T-BKI` to `LC-HPE2-A13T-BK`. Commission’s matching SKU, $17.00 VLOOKUP cost, $126.09 live formula, and $3,670.27 total were re-read and remain correct. Updated the review flag and compact exception record to document the confirmed source and correction.
### 2026-10-22 — Kevin September commission: source-led payout decisions
- Rebuilt the review control tab as `9月审核结论`: original commission formulas remain untouched; the sheet now separates calculated commission, recommended payout, and held amount with the evidence and disposition for each exception.
- Verified `197993` in ShipStation against exact order `0197993`: UPS Ground company freight was `$738.16`; its two Kevin commission lines (`$1,381.88`) are payout-ready.
- Verified `198022` in QuickBooks: the `$510.00` invoice is assigned to location `Leon`, not Kevin. Although ShipStation freight `$26.68` is valid, it is excluded from Kevin’s September payout.
- Kept `197459` on hold: ShipStation searches did not locate the 2026 shipment/freight; only an unrelated 2020 order appeared. Do not pay its `$181.74` until original freight evidence exists.

### 2026-10-22 — Jordan September commission: source-led payout decisions
- Rebuilt the review control tab as `9月审核结论`, using the same payout/hold evidence gate while retaining every existing commission formula.
- Kept shared Acer invoice `197459` on hold for `$181.74`: its `$945.67` freight still has no matching 2026 ShipStation or original-freight evidence.
- Corrected `197969` under the standing inclusion rule: orders paid before the sheet is produced are included when they do not appear in any prior commission sheet. A 1–9 month duplicate audit found no prior entry, so it was added at `$130.06` using Jordan's existing NutKase net-sales 5% formula.
### 2026-10-28 — Commission recurrence controls from Kevin/Jordan September review
- A paid pre-sheet record (`197969`) was initially excluded because its payment month was August. This conflicted with the user's standing rule. Prevention: audit every prior Commission tab for duplicates; include any non-duplicated record paid before the sheet was prepared, regardless of its payment month.
- A review/exception layer was initially treated too much like the validation outcome. Prevention: reconcile source evidence, 未付, Commission formulas, totals, and payout first; review tabs only summarize the verified result.
- The overall Commission-rate KPI used a different denominator from the row-level rate basis, making the displayed rate misleading. Prevention: label the KPI basis, link shown amounts to formulas, and recompute the exact numerator/denominator pair before delivery.
# 2026-10-28 — Ownership audit omitted before settlement preparation

- **What happened:** Rows were initially retained in salesperson 未付 lists without a complete cross-check of Offline Report salesperson, customer State/territory, and established customer ownership. This left B&H invoice 198074 in Jordan despite the known Kevin B&H relationship and NJ territory; Hudson School District invoice 197834 likewise appeared in Jordan although CRM identifies the customer as NH (Kevin territory). State codes also remained missing for some rows while their evidence was available in CRM.
- **User impact:** A salesperson could see or be paid Commission for an order that may belong to another salesperson, and the review queue concealed the conflict rather than making it decision-ready.
- **Root cause:** The work treated source-column cleanup and reactive exceptions as sufficient, instead of completing ownership triage before preservation or payout eligibility.
- **Correct action taken:** Added State evidence (SC, NH, TX), removed duplicated state labels from Notes, and marked invoices 198074 and 197834 `归属待确认` with their confirmation actions. Neither was moved or settled.
- **Permanent prevention:** Every row must be reconciled against Offline Report + territory State + historical/CRM customer ownership. A conflict is a hold, not a transfer or payout.
- **Verification:** Re-read every active row's State and exception list after write; confirm each conflict has `归属待确认`, a concise evidence note, a next action, and is absent from settlement totals until confirmation.
- **2026-10-29 follow-up:** The same ownership scan also found Jordan `197905` (NY/Worth Ave.) without an evidenced Jordan customer override. It is now held as `归属待确认`; B&H `198074` and Hudson `197834` remain holds. No ownership was moved.

## 2026-10-29 — Full preflight rerun

- Re-ran the consolidated preflight across the active Kevin/Jordan `未付` queues and the populated August/September Commission tabs. Found no formula errors, no active blank State/Status/Next Action fields, and no remaining active-`未付` overlap with paid August or September Commission groups.
- SPIFF review confirmed the stored amounts for Kevin `198022` and Jordan `197834`, `197902`, `197908`, `198044` against the tracker. Marked Jordan `197902` as `异常待核对` because the tracker says QBO invoice not found; Kevin `197236` remains held and now explicitly requires a missing SPIFF-tracker record before settlement.
- **SPIFF payment-gate correction:** Kevin `198022` has `已发出` and CK#3190 but no SPIFF Payment Date. The earlier logic treated issued payment as adequate for Commission readiness; this conflicts with the user's rule that SPIFF must be paid first. It is now a `SPIFF 待支付确认` hold. Going forward, only an actual paid status plus payment date/reference can open the Commission-settlement gate.
- **Invoice-identity correction:** Jordan `197896` and `197902` carried the same date, SKU, quantity, and amount. The user confirmed that `197896` is the erroneous duplicate and `197902` is the retained Invoice#. Deleted the complete `197896` group only. The retained `197902` remains held because its current customer detail is Audio Visual Aids while the SPIFF tracker names Coirle LLC; resolve customer/QBO evidence before payment.
- **Exception-action specificity correction:** Generic labels such as `异常待核对` did not tell the user what fact conflicted or which system to open. Rewrote every active hold with the exact discrepancy and source action. For example, Kevin `198092` is retained for Kevin by user confirmation, while QBO `0198092` shows Location Leon, date 10/2 versus sheet 9/30, unpaid $592.50 balance, and no Ship Via/Tracking; its next action now names each required confirmation. The same treatment records the partial-receipt amount/freight gap for Jordan `197929`, the CRM/SPIFF ownership evidence for `197834`, and the exact evidence needed for `197902`, `197905`, and `198074`.
- **QBO-payment mapping correction:** User confirmed Jordan `197929` was not paid and that the prior QBO Invoice Number was wrong. The correct QBO invoice is `0198116` (10/12/2026, $1,125.60). Cleared the falsely imported 9/16 Paid Date and $65.82 Received Amount, restored `待客户付款`, and specified that ShipStation freight is checked only after QBO `0198116` is fully paid. Prevention: match QBO reference + customer + amount + date before importing any payment field.
- **Confirmed customer correction:** User confirmed Jordan `197902` belongs to Audio Visual Aids Corp. Corrected the SPIFF tracker customer from Coirle LLC to Audio Visual Aids Corp and cleared the now-known-wrong Coirle contact/email rather than carrying them to the new customer. The item remains held solely because QBO has not located the invoice and Audio Visual contact/payment details still need verification.
- **Estimate-stage correction:** User clarified that `197902` does exist in QBO as an Estimate but has not been sent, so it is neither a missing invoice nor a customer-payment exception. Corrected the SPIFF tracker to `暂不支付—QBO Estimate 未发送` / `Estimate 未发送`, and the Commission queue to `待 QBO Invoice 发送`. Its next action is now strictly sequenced: convert/send Invoice, wait for customer payment, then verify SPIFF contact/payment and Commission.

