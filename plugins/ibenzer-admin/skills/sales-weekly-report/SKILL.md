---
name: sales-weekly-report
description: Complete iBenzer's weekly Sales Report by reconciling offline sales, Nutshell Leads and Activities, updating the established weekly workbook detail pages, and optionally preparing an unsent Gmail draft.
---

# Sales Weekly Report

## 公司固定执行与错误闭环
开始此工作流前，先读取 [公司固定规则](../../references/company-operating-rules.md)。该规则适用于本 Skill 的所有步骤；如与当前用户明确指令冲突，以用户当次明确指令为准。

Use this skill when Una asks to complete a weekly Sales Report, update the `2026周报` workbook, or prepare the associated weekly-report email. It is for sales-team reporting (normally Kevin, Jordan, and Leon), not the Sales VA/Hubstaff report.

## Scope and period

- Default to the current Monday–Friday reporting period; use an explicitly supplied period instead.
- Confirm the report is based on completed/available data as of the run time. Do not invent a missing order, customer, owner, activity, or amount.
- Keep sales, samples, replacements, Create Leads, Phone Calls, Emails, and Meetings as distinct metrics.

## Evidence and calculation

1. Read the current `4 iBenzer - Offline Sales Report 2026-2027.xlsm` source, using the relevant month tab. Group multi-SKU invoice lines into their single PO/order.
2. Count sales orders and quantities from non-zero sales; calculate sales amount from the invoice total. Treat zero-value sample and replacement records separately.
3. In Nutshell, filter **Leads** by Open date for the same period and report Create Lead by assignee. Filter the **Activity** report by the same period, segmented by user, and capture Phone Call, `2E - Follow Email`, and Meeting.
4. Use the actual CRM owner names: Kevin Chiu, Jordan Tseng, and Leon YU. Do not attribute records belonging to other users.
5. If the sales source provides a PO but no customer name, write `待确认` in the detail, rather than guessing from SKU or value.

## Workbook update

Update the existing `2026周报` workbook rather than creating a new report file.

- Update `Summary` for Kevin, Jordan, and Leon: sales order count, quantity, sales amount, sample count, replacement quantity, Create Lead, Phone Call, Email, and Meeting.
- Update the relevant month detail tab with invoice/PO, date, SKU lines, per-person totals, and separate Sample/Replacement sections. A multi-SKU PO counts once in the order total but every SKU line must remain visible.
- Update Kevin's individual tab for the current period with the summary, sales detail, and a short factual analysis plus measurable follow-up target.
- Copy the closest completed weekly block before filling new rows, so existing formats, currency display, borders, and formulas remain consistent. Read the target cells before editing and read them back after editing.
- When a live Sheets tab could have stale content, avoid applying old UI edits after an API update; re-read the workbook as the source of truth.

### Kevin detail layout

Use the following approved layout for newly added Kevin weekly blocks:

- Keep the yellow weekly-summary row, followed by a compact Sales table, then Sample and Replacement sections only when each has relevant records.
- Do not leave a full bordered placeholder table merely because Sales or Replacement is zero. A single `Total 0` line is sufficient for a verified zero-sales section.
- Use the right-hand panel for a compact management summary rather than loose narrative text: three factual lines headed by sales, activity, and required improvement; then a visually separated three-item next-week action list.
- Keep spacer rows minimal. The panel is for the current weekly block only, with aligned text, wrapped content, and clear header styling.
- In `Summary`, retain the established three-person weekly group. Use a visible top and bottom group separator for the newest week, and display verified zero sales as `$0.00`, not a dash.

## Weekly email draft

Only perform this part when the user asks for an email or a Gmail draft.

- Find the prior `Sales Weekly Report` sent email in the Accounting Gmail account and reuse its recipient, tone, signature, and concise structure.
- Use the exact reporting period in the subject: `YYYY.M.D–M.D Sales Weekly Report`.
- Include a brief sales section, Nutshell activity section, factual performance notes for each owner, and the existing `2026周报` link.
- Create an unsent Gmail draft only. Never send it unless the user separately asks to send it.

### Table layout

When the email uses the established three-table format, keep the layout deliberately uniform rather than sizing columns to the data.

- Give the three tables the same overall width and use one consistent header color, border treatment, padding, and centered numeric alignment.
- In the sales table, use six equal-width columns for Sales, Orders, Qty, Sales Amount, Sample, and Replacement. Do not let a long field make its column wider than the others.
- Use intentional line breaks in long headers (for example, `Sales` / `Amount`) instead of an accidental word split. Keep short headers such as `Orders` on one line.
- Keep narrative content in a separate two-column follow-up table, with a narrow person column and a wide text column. This avoids making quantitative columns uneven.

## Completion check

- Sales total and per-person figures match the source detail.
- Activity and Lead counts are from the same date range as sales.
- Zero is explicit when verified; otherwise state that data is unavailable.
- Report which workbook pages and whether an email draft were updated; include the draft subject but never claim it was sent.


