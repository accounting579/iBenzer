---
name: ibenzer-attendance-payroll
description: "Update iBenzer weekly or bi-weekly attendance, employee Detail sheets, Monthly payroll tables, and summaries from punch records. Use for attendance, lateness, early leave, overtime, vacation/paid leave, show travel, payroll-detail, Weekly Summary, Bi-Weekly Summary, or salary-confirmation updates."
---

# iBenzer Attendance and Payroll

## 公司固定执行与错误闭环
开始此工作流前，先读取 [公司固定规则](../../references/company-operating-rules.md)。该规则适用于本 Skill 的所有步骤；如与当前用户明确指令冲突，以用户当次明确指令为准。

Use this workflow for every iBenzer attendance period. The goal is a traceable, formula-driven record: source attendance, employee Detail, monthly payroll table, and summary must agree.

Before editing any file, read [attendance-rules.md](references/attendance-rules.md) and [failure-controls.md](references/failure-controls.md), then use the closest **user-reviewed complete period** as the structural template. Do not use a partially completed or AI-created period as a template.

## How to invoke this skill

It is available automatically when a request is clearly about iBenzer attendance/payroll. To require it explicitly, start the request with `$ibenzer-attendance-payroll`, for example:

> `$ibenzer-attendance-payroll 请按 2026/10/16–10/31 的考勤记录完成 Howard、Kevin、Una、Ivy、Jordan 的 Detail、Summary 和 Monthly，同步保留公式并完成核对。`

State the period, source attendance workbook, affected people, and required downstream outputs. If the user has already corrected a period, explicitly say “以我修改后的考勤记录为准”.

## Non-negotiable principles

1. The current period's manually corrected `考勤记录` is the authoritative record. User corrections and written instructions override old periods or inferred rules.
2. Preserve formulas. Extend formulas and references from the comparable completed period; never replace a formula with a pasted result unless the user explicitly asks.
3. Never copy a prior period's hours, balance, pay date, source link, or leave result as a value. Recompute it from the current period.
4. Yellow cells represent weekends only. A yellow blank is not an absence.
5. A missing punch on a scheduled non-weekend/non-holiday day requires classification: approved leave, business travel/show, holiday, or unapproved absence. Do not guess.
6. Changes are incomplete until every required downstream sheet is reconciled.

## Required workflow

### 1. Establish the period and authoritative sources

- Identify whether the request is Weekly, Bi-Weekly, monthly, or another payroll cycle. Do not assume the date span.
- Open the period workbook's `考勤记录`, `考勤汇总`, and relevant employee tabs. Read existing formula patterns and formulas before changing anything.
- Open each affected employee's personal attendance workbook, including the relevant month Detail and `Summary` tab.
- Open the master `1 Attendance Monthly 2026` workbook and identify the corresponding Detail, Weekly/Bi-Weekly, and Summary blocks.
- For sales/show personnel, check the Show/Travel source and any notes before classifying an empty attendance day.

### 2. Build a source-of-truth review table before writing

For each employee/day, record: date, weekday/weekend/holiday, raw arrival, raw departure, work/show/leave classification, late minutes, early-leave minutes, leave hours, overtime hours, and the destination cells.

Use the current manually corrected attendance record as the review baseline. If punch data, a prior Detail, and the corrected attendance record conflict, stop and identify the conflict rather than silently selecting one.

### 3. Enter the attendance record correctly

- Keep arrival and departure in the same daily cell on two lines when the template uses that presentation.
- Format late arrivals in **red** and overtime in **blue**. Retain existing borders, dates, yellow weekend fill, row layout, and summary column placement.
- Do not mark a normal post-17:00 departure as late. Only count an early departure when it is at least 30 minutes before 17:00.
- Exclude the 12:00–12:30 lunch break from work/leave calculations when the absence interval crosses it.
- Use 15-minute increments as 0.25 hour; do not round 15 minutes to 0.5.
- Keep before-9:00 and 9:00-or-later lateness in their separate columns (`9前` / `9后`) and do not merge their count/minute/leave results.
- If a person attends a confirmed show or business trip, enter the show/event name in the period record rather than treating the day as absence.

### 4. Handle leave, vacation, holidays, and overtime

- Approved vacation/paid leave reduces the appropriate leave balance; it is not an absence value copied as a static number.
- Vacation covers the scheduled absence and must not automatically reduce paid standard hours. Follow the employee's established Detail/payroll pattern. For an employee whose approved vacation is paid against standard hours, retain standard paid hours and reduce only the Vacation balance.
- Company holidays count as attendance even without a punch, when the employee is eligible and the template/policy calls for it.
- Record unapproved absence/deduction in the correct `AB` field and preserve the table's formulas/totals.
- Record OT separately; it is not late time or leave time.
- Do not infer a vacation balance or entitlement. Verify it from the employee's Detail and policy table.

### 5. Update employee Detail and Summary

- Use the month Detail layout already present in the employee workbook.
- Add the current dates, punches, AB, OT, actual/standard-hour formulas, and leave table updates while retaining formulas, formatting, and totals.
- Ensure Detail totals flow into the employee `Summary` through formulas/references. Do not type an aggregate value into a Summary cell when a corresponding formula pattern exists.
- Verify each employee-specific rate and hour model from the nearest completed period; do not apply one employee's pay logic to every employee.

### 6. Update the master Monthly workbook

For each completed period, update every applicable destination:

1. The current-period employee Detail block, preserving its full layout.
2. The corresponding Weekly or Bi-Weekly payroll block.
3. Weekly Summary or Bi-Weekly Summary (late counts/minutes, OT, AB, vacation add/remain, cash/base pay fields as appropriate).
4. The monthly payment/attendance table with the correct current-period hour/rate formula and the **link to the source attendance workbook**.
5. Any employee-specific monthly row or summary that pulls from the Detail block.
6. The salary-confirmation document when the user asks for it.

Copy the entire structural template for a new block (headers, formulas, formatting, employee rows, links, and confirmation area), then replace only current-period content and references. A partial lower block is not acceptable.

### 7. Formula and visual QA

Before declaring completion:

- Inspect formulas—not just displayed values—in new Detail, Summary, and payroll cells.
- Confirm total work hours, AB, OT, late counts/minutes, vacation balance, rate split, and salary agree across source, personal Detail, master monthly table, and relevant summary.
- Verify new period dates, source workbook hyperlink, employee name hyperlink, pay date, and source link point to the current period.
- Check that late text is red, overtime text is blue, weekends are yellow, and labels align with the prior reviewed layout.
- Compare the new block side-by-side with the complete template block to confirm headers, merged cells, borders, and formula coverage match.
- Report exceptions or unresolved classifications to the user; never hide them with zeros.
- Before completion, perform the `Failure-prevention sign-off` in [failure-controls.md](references/failure-controls.md). Completion is blocked if any listed required destination is missing, any formula has been replaced with a static value, or a current-period source link has not been verified.

## Scope and approval boundaries

- The agent may calculate, prepare, and update requested attendance spreadsheets and documents after checking formula patterns.
- Ask the user/management before assigning an unconfirmed absence as vacation, changing an entitlement, creating a payroll payment, changing pay rate, or deciding whether ambiguous travel/show time is paid.
- Do not submit payroll, issue payment, or alter bank/Zelle data unless explicitly instructed.

## Error-library and regression-control rules

These controls apply whenever a user corrects a prior attendance or payroll result.

1. Before editing, read the relevant entries in **Admin & Acct → AI 错误库** and the company **AI 错误库与改进规则** document. Treat already-verified rules as mandatory, not optional reminders.
2. Choose the structural template only from a complete period the user has reviewed and accepted. Never use an AI-created, partially completed, or merely most-recent block as the formatting/formula source. Copy its full structure; replace every date, source link, formula reference, balance, hour, rate tier, and payment-status field that belongs to the current period.
3. For every new or changed period, complete the propagation matrix as one closed task: source attendance → employee month Detail → employee Summary → master payroll block → Weekly/Bi-Weekly Summary → monthly payment/attendance table and source link → confirmation document when required. A blank or partially copied downstream block is a failure, even if the attendance grid itself looks complete.
4. Formula audit is mandatory: inspect the formula bar for each current-period totals/hour/rate/salary/balance field and Summary reference. A copied displayed number is not evidence of a preserved formula. Only fixed policy constants may remain literal values.
5. When the user identifies one calculation, color, layout, formula, link, or propagation error, run a same-scope regression sweep across every affected employee, period, and downstream destination before reporting completion. Record the outcome in the AI error library; update an existing matching entry instead of creating a duplicate.
6. Before final delivery, visually compare the current block with the approved template: merged headers, row heights, column widths, borders, weekend fill, two-line punches, red late, blue OT, source hyperlink, and formula-bearing cells must match. Report any unresolved classification or payroll decision instead of inserting a default.

## Cross-period balance and monthly-confirmation controls

These controls apply when any employee has Vacation Add, Vacation Remain, AB, OT, or a monthly payroll confirmation.

1. Use the employee's own reviewed `Summary` as the authoritative balance ledger. Reconcile the entire chain for the affected month—not only the newest row: prior-period ending balance → each period's Vacation Add → OT → AB → each next-period opening balance. Do not derive a balance from an unrelated master cell, an old template, or a displayed value alone.
2. Build and retain a per-employee reconciliation line before writing: `period | opening balance | Vacation Add | OT | AB | ending balance | Detail cell | Summary cell | master Bi-Weekly cell`. Each ending balance must equal the next period's opening balance exactly. If it does not, stop and correct the first divergence before editing downstream records.
3. When one employee's balance/AB/leave chain is wrong, sweep the same balance chain for every affected employee and all adjacent pay periods. Do not report a single-cell correction as complete.
4. A salary-confirmation document is monthly unless the user explicitly requests a weekly or bi-weekly confirmation. For a monthly confirmation, aggregate October 1–31 (or the stated calendar month) from all payroll periods in that month; do not carry a half-month date range, half-month late/AB totals, or half-month vacation values into the document.
5. Confirmation values must be copied only after the monthly ledger is reconciled. Verify the confirmation's dates, employee, late totals, AB, OT, Vacation opening/add/end, salary/cash, and show/travel note against the final source Summary. Keep unknown payment status blank; never invent or infer a payment.

## Layout, color, and template-integrity controls

These controls apply to every attendance grid, Detail block, Summary block, master payroll block, and confirmation output.

1. **Do not redesign the workbook.** Select the nearest user-reviewed block for the same employee/workflow and copy its complete structure before entering values: merged cells, row/column dimensions, borders, headers, formulas, number formats, hyperlinks, conditional formatting, fills, and print layout. Never create an improvised lower block or leave a partial template beneath a completed block.
2. **Use the approved visual grammar exactly.** Yellow = weekend only; red = late arrival and late/leave summary fields only; blue = OT and confirmed show/travel name only; black = all departure times, including early-departure punches. A post-17:00 departure is black and is never classified or colored as late. Do not recolor any user-entered cell, show label, or manual annotation.
3. **Protect human edits.** Before editing, snapshot the target range's values, formulas, font colors, fills, hyperlinks, and notes. Change only cells required by the current period. If a target differs from the template because of a user edit, retain the user's version unless the user explicitly asks to change it.
4. **Date-boundary control.** Enter only dates within the requested payroll period. Do not pull forward next-period punches or dates; do not leave prior-period rows below the total; do not use an old period title/pay date/source link. Verify first date, last date, weekday/weekend pattern, and total-row range.
5. **Detail and Summary distinction.** A Detail sheet records daily punches/AB/OT/actual hours; a Summary records only the employee categories authorized for that employee. Do not populate Ivy's payroll/vacation Summary merely because a generic template has fields. Preserve authorized blanks.
6. **Show/travel presentation.** For Kevin/Jordan and other sales staff, use the confirmed Show sheet wording and user's existing color. Put the show name in the attendance/daily Detail cell; do not overwrite it with punch data, red late text, or AB. Do not treat confirmed travel as absence.
7. **Two-pass visual validation.** After formula reconciliation, compare the edited block side-by-side with the approved reference at 100% zoom. Then re-read the exact edited ranges: dates/title, employee highlights, headers, borders/merged cells, row heights, source links, colors, and totals. A format mismatch blocks completion even if totals are correct.

### Mandatory layout-and-format sign-off checklist

Complete this checklist for **each employee and each new period block**. A “not applicable” item must state why; a blank checklist item is not a pass.

**A. Scope and source locking**

- [ ] Record requested payroll type, exact start date, exact end date, employees in scope, and every required downstream destination.
- [ ] Locate the closest **user-reviewed complete** reference block for the same workflow and confirm its period is not AI-created/partial.
- [ ] Read the current manually corrected attendance grid before copying any formatting; do not take a screenshot or prior AI output as authority.
- [ ] For Kevin/Jordan or any sales employee, read Show/Travel source and retain its exact event wording and user-set color.
- [ ] Identify user-edited cells in the target period (value, formula, font color, fill, hyperlink, note, merged range). Mark them protected before any bulk fill/copy operation.

**B. Structure replication**

- [ ] Copy the entire approved block, not isolated value cells: title, date row, employee header, Detail table, totals, leave ledger, confirmation area, source link, hidden/formula-bearing cells, and print layout.
- [ ] Preserve merged ranges; do not create unmatched lower blocks, leftover header-only areas, duplicate summary blocks, or rows from the preceding period below the new total.
- [ ] Match row heights, column widths, borders, font family/size/alignment, date/number/currency/time formats, yellow weekend fill, and any existing conditional formatting.
- [ ] Replace all copied period-specific fields: title, dates, pay date, attendance source hyperlink, employee/name hyperlink, source labels, formulas and references, vacation opening balance, rate tiers, payment status, and confirmation period.
- [ ] Confirm the new date list includes only requested dates and that weekends/holidays occupy the same positions as the calendar requires.

**C. Daily punch presentation and classification**

- [ ] Put arrival and departure on separate lines within the same daily attendance cell only when the approved attendance grid uses this design.
- [ ] Arrival later than 08:30 is red; every departure remains black, including early departure and departure after 17:00.
- [ ] Yellow means weekend only. Do not color weekday absence, leave, show/travel, or a selected employee yellow unless the approved template explicitly requires it.
- [ ] Normal departure after 17:00 is neither late nor red. Early departure enters calculations only at the policy threshold; exclude 12:00–12:30 lunch when the missed interval crosses lunch.
- [ ] Keep 9前 and 9后 count/minute/leave fields separate. A 09:55 arrival contributes 25 minutes to 9前 and 60 minutes/1 count to 9后 under the user-established rule; it must not be collapsed into one field.
- [ ] Use 15 minutes = 0.25 hour; never silently round it to 0.5 hour.
- [ ] Mark OT in blue only where it is eligible and verified; do not use blue for unconfirmed data.
- [ ] Confirmed show/travel replaces absence/AB with the exact show name, retaining the user’s existing show color; do not overwrite it with punch, formula, or generic text.

**D. Detail, Summary, and formula integrity**

- [ ] Detail contains current-period daily data only: no previous-period rows after total and no next-period dates/punches inside the block.
- [ ] Use formulas for actual hours, totals, AB, OT, late totals, vacation balance, rate splits, salary and carry-forward fields wherever the accepted reference uses formulas.
- [ ] Inspect formulas, not only their displayed result, for all total/carry-forward/salary/summary fields. No `#REF!`, formula replaced by a pasted value, or copied reference to another period is permitted.
- [ ] Keep employee-specific distinctions: Ivy is attendance-only (do not add payroll/vacation Summary data); Howard’s approved vacation follows his established paid-hours pattern; never apply one employee's formula/leave logic to another.
- [ ] For every balance chain, verify: `opening + Vacation Add + OT − AB = ending`, and current ending equals next period opening.

**E. Downstream propagation and links**

- [ ] Update every required downstream location: personal Detail, personal Summary (if applicable), master Detail, Weekly/Bi-Weekly block, Weekly/Bi-Weekly Summary, Monthly payroll/payment table, current attendance-source link, and confirmation document when requested.
- [ ] Verify the linked source is the current period's source attendance workbook, not a prior week's/bimonthly file, a generic link, or a blank link.
- [ ] Detail, Summary, master payroll block, and Bi-Weekly/Weekly Summary must agree on late count/minutes, AB, OT, Vacation Add/Remain, hours/rates and salary. If they differ, correct the first source-of-truth divergence before continuing.
- [ ] Confirmation document must be a calendar-month aggregation unless the user explicitly specifies a different period; it must not inherit half-month dates, figures or labels.

**F. Final two-pass QA and delivery gate**

- [ ] Pass 1—data/formula: re-read all changed cells and formulas, all balance-chain cells, current-period links, and downstream totals.
- [ ] Pass 2—visual: side-by-side against approved reference at 100% zoom; check title/date boundary, headers, merged cells, row/column dimensions, borders, fonts, formula cells, weekends, red late, blue OT/show, black departures, protected user edits and source links.
- [ ] Sweep all employees with the same class of change/error and all adjacent periods; do not correct only the employee/cell the user happened to identify.
- [ ] Report completion only with a concise evidence list of blocks and documents actually re-read. If any item is unresolved, state it as an exception; never report a partially copied or visually inconsistent block as complete.


