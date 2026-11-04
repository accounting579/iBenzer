---
name: ibenzer-monthly-report-accuracy
description: Update or review iBenzer channel monthly reports, Casing Bee weekly sales data, and related annual-account inputs with source-traceable SKU detail, historical-format parity, and verified formulas.
---

# iBenzer Monthly Report Accuracy

## 公司固定执行与错误闭环
开始此工作流前，先读取 [公司固定规则](../../references/company-operating-rules.md)。该规则适用于本 Skill 的所有步骤；如与当前用户明确指令冲突，以用户当次明确指令为准。


Use for iBenzer marketplace monthly reports, Casing Bee weekly sales/purchase-forecast updates, shipment/fee imports, and any channel data feeding annual accounts.

## Non-negotiable workflow

1. Inspect the matching completed historical period before writing. Preserve its tab structure, monthly split, detail level, formulas, number formats, colors, and completion-status wording.
2. Build a source-detail table first. Each included quantity or amount must retain the source platform, reporting/ship date, order or shipment number, SKU, quantity, amount, and a source link or export reference. Do not publish a Summary-only result when the established workbook contains Detail.
3. Aggregate only from the retained detail. Map source SKUs to master SKUs using an evidenced mapping or an existing master-SKU relationship. Keep unmapped, combined, missing-order-number, and ambiguous records in a visible exception list; exclude them from totals until confirmed.
4. Use the reporting period encoded by the source record, not download date. Treat spreadsheet date values as dates and apply the historical date format; never leave date serials visible.
5. Before declaring a period complete, verify: source row/unit count; detail-to-summary aggregation; formula coverage and values (not merely formulas present); numeric sign and currency; date format; and visual format parity with the reference period. Re-read at least one non-zero SKU/transaction and one expected-zero record after any formula rollout.
6. Never mark a task or tracker item complete while source exceptions, missing Detail, formula errors, inconsistent format, or unresolved reconciliation differences remain. Record the exact exception and next evidence needed.

## Formula and bulk-write safeguards

- Test a formula on a known non-zero row and a known zero row before filling it down.
- For weekly sales columns, confirm the aggregation key is the same SKU field used by the master table. If a mapping formula is involved, verify the mapped output rather than assuming a visually matching formula will aggregate.
- After inserting columns or copying a reference period, verify headers, formulas, cell formats, and existing period references on both adjacent columns.

## Completion evidence

The delivery note must state the source date range, included count/amount, excluded exception count, and remaining confirmations. If the request asks only for an update, do the work before reporting; do not substitute progress commentary for the completed Detail and Summary updates.

