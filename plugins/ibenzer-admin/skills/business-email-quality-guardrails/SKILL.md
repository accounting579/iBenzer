---
name: business-email-quality-guardrails
description: Draft accurate, formal iBenzer business emails and make precise tracker updates after validating the exact request, facts, row, and columns.
---

# Business Email & Tracker Quality Guardrails

## 公司固定执行与错误闭环
开始此工作流前，先读取 [公司固定规则](../../references/company-operating-rules.md)。该规则适用于本 Skill 的所有步骤；如与当前用户明确指令冲突，以用户当次明确指令为准。


Use this skill for iBenzer customer/vendor email drafting, translation, and closely related tracker updates.

## Default writing standard

- Unless the user explicitly requests otherwise, write in formal, natural business English.
- Match the user's established business-email format: clear greeting, concise paragraphs, courteous request or update, and a professional closing.
- Do not provide a casual literal translation, a terse chat-style reply, or extra analysis when the user asks only for an email draft.

## Fact fidelity check before drafting

- Include every explicit fact the user supplied that is material to the request: names, addresses, dates, PO/invoice numbers, tracking numbers, amounts, and requested next step.
- Do not claim a shipment, attachment, payment, confirmation, or action occurred unless the user explicitly supplied that fact or asked you to verify it.
- When revising a draft after feedback, revise the whole draft against the requested tone and format rather than changing only a phrase.

## Direct-instruction calibration

- When the user asks for instructions or a prompt for another operator/agent, provide a directly executable, simple version first.
- Include detail only when it is necessary for execution or the user asks for it; avoid turning a straightforward command into a technical plan.

## Spreadsheet / tracker updates

- Before writing, inspect the sheet headers and the entire target row.
- Identify the target by a unique organization, PO, bid, or other unique identifier—not visual proximity or date alone.
- Write only to the confirmed intended columns.
- Immediately re-read the edited cells and neighboring row context; verify that no other row or column was changed.

## Required verification

- For emails: perform a final check for formal business tone and exact user-provided facts.
- For trackers: report completion only after the exact target row and columns have been read back successfully.

