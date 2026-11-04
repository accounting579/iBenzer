---
name: ibenzer-execution-alignment
description: Apply iBenzer's fixed execution checks to multi-step operational work, especially trade-show, travel, Sheets, Gmail, and reimbursement tasks where the user has established exact formats, scope limits, or confirmation rules.
---

# iBenzer Execution Alignment

## 公司固定执行与错误闭环
开始此工作流前，先读取 [公司固定规则](../../references/company-operating-rules.md)。该规则适用于本 Skill 的所有步骤；如与当前用户明确指令冲突，以用户当次明确指令为准。


Use this skill whenever a request continues an iBenzer operational workflow with an established spreadsheet, prior examples, recurring status fields, travel records, registrations, or reimbursements.

## Fixed rules

1. **Preserve the agreed destination and format.** Before editing, identify the exact field the user asked to update and inspect a completed example from the same document. Do not move information to a different column, section, or artifact because it seems more convenient.
2. **Treat confirmation status as evidence-based.** Never mark a person, ticket, badge, booth, furniture package, booking, invoice, or itinerary as complete merely because a related purchase or plan exists. Mark it complete only when the relevant confirmation identifies that exact item; otherwise leave it pending and state what is missing.
3. **Do not silently alter protected context.** When a user says notes, remarks, call-to-action fields, dates, links, or previously supplied constraints must remain, leave them untouched unless the user explicitly asks to change that exact content. Before replacing long cells, compare all non-targeted text and preserve it verbatim.
4. **Use the requested scope and time period.** For expense, reimbursement, and travel work, confirm the requested year, event, person, account/card, and category before entering amounts. Do not substitute prior-year or similarly named records.
5. **Reconcile related trackers as one system.** When completing a reimbursement or show status workflow, update or verify its paired summary/status tracker using the established template. Do not create an ad-hoc layout when a user example exists.
6. **Verify generated links and itinerary assumptions.** Open or inspect final booking/search links for the requested dates, airports, sorting, and travel mode before presenting them. Validate travel feasibility against event times, travel-to-venue time, and stated attendee constraints.
7. **Filter event agendas by the attendee's role.** Include only activities that serve the stated role and goal. For exhibit planning, use *Exhibit Hall Open* hours only unless the user expressly asks to include move-in, education sessions, receptions, or other programming.
8. **Forward source materials when asked.** When the user asks to forward, or says organizer materials already exist, search for the source email first and preserve its thread and attachments. Do not replace it with a newly composed summary unless the source is unavailable or the user asks for a new draft.
9. **Make reviewer handoffs decision-ready.** Complete all source gathering, classification, formulas, matching, and itemization that AI can perform. Ask Leon or another reviewer only for a specific decision or missing fact, preferably yes/no. Include the exact transaction/date/amount/description, proposed treatment, reason, and direct source/output links. Do not assign the reviewer broad searches, reconstruction, or checks that the AI can complete.
10. **Finish the available scope in the current work cycle.** Do not split a fully available task into artificial next-day phases. Complete every item supported by current evidence, then list only genuine external blockers.
11. **Rebuild reimbursement layouts as one block, never by patching rows into a finished block.** For an expense report with merged category subtotals and a Pivot, first identify the complete source range, category order, subtotal/total rows, merge ranges, Pivot source/output range, and nearest approved same-sheet example. Rebuild or resize the whole report block from that structure; do not leave stale formatting, partial borders, colored blank cells, or disconnected Pivot fragments. Reconcile source-detail total = category subtotals = Pivot grand total before delivery.

## Preflight and verification

- Restate internally: exact artifact, target range/section, no-touch fields, status evidence required, and user-approved scope.
- Before any live write, inspect the exact cells/section and a nearest completed peer.
- After a write, re-read the changed area and visually confirm it when a live view is available.
- For reimbursement blocks, compare the complete rendered block against the approved peer: category grouping/order, continuous borders, intentional blank separators only, matching fill colors, no leftover values or formats, and matching source/Pivot/grand totals.
- If an issue is identified after delivery, update this skill only with a narrow, reusable rule; then update the company error library without duplicating an existing record.

## Boundary

These rules guide execution quality; they do not authorize purchases, ticket issuance, registrations, payments, email sending, or changes outside the user's stated request.

