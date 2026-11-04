---
name: accounting-delivery-integrity
description: Protect user-authored accounting reports, report-source integrity, and established placement when updating Aging Report or Daily Report drafts.
---

# Accounting Delivery Integrity

## 公司固定执行与错误闭环
开始此工作流前，先读取 [公司固定规则](../../references/company-operating-rules.md)。该规则适用于本 Skill 的所有步骤；如与当前用户明确指令冲突，以用户当次明确指令为准。


Use for iBenzer Aging Report, collections follow-up, QuickBooks report attachments, and Daily Report draft updates.

## Fixed execution rules

1. **Preserve user-authored content.** When editing an existing draft, treat all pre-existing user text, sections, and attachments as immutable unless the user explicitly asks to remove or replace that exact item. Make a targeted in-place amendment, never rebuild the whole draft from memory. Re-read the edited section and confirm unrelated content remains.

2. **Update at the requested location.** When a user asks to update an existing Aging Report item, amend that item in the original Aging Report section. Do not append a separate “更新” or duplicate summary below unless the user explicitly requests a changelog.

3. **QuickBooks reports must be originals.** If a Daily Report is asked to include an Aging Report or Estimate Report, attach the current native QuickBooks export—not an AI-created recap or substitute PDF. Export after the latest user-supplied payment/Estimate update, replace only the corresponding prior attachment, retain other attachments, and verify filename, source, date, and attachment count.

4. **Draft-only by default.** Save and verify drafts; do not send unless the user explicitly says send/发送/确认. Before reporting completion, reopen or read back the draft and verify recipient, subject, body placement, retained user content, and attachments.

5. **Reply drafts must retain email formatting.** For a Gmail reply with more than one paragraph, do not use a plain value replacement that collapses line breaks. Insert structured HTML paragraphs (or type paragraph-by-paragraph) and visually verify that the salutation, each body paragraph, and signature appear on separate lines before reporting completion.

6. **Use the existing human collection thread.** When a prior human collection conversation exists, reply in that exact thread (Reply All when the customer has added the responsible Accounting contacts). Do not create a separate follow-up subject unless no suitable human thread exists.

7. **Daily Report statuses mirror actual sends.** Once the user states that follow-up emails were sent, amend the matching bullets in the existing Aging Report section in place to say “已发送.” Do not alter unrelated bullets or replace the current native QuickBooks attachments.

## Regression check

For every Daily Report draft update, record this quick check before declaring completion:

- Target section was edited in place.
- Existing user text and non-target attachments are still present.
- Each report attachment is the latest QuickBooks export for the requested report.
- Draft remains unsent and is readable from Drafts.
- Multiline customer-email drafts display distinct paragraph and signature lines in Gmail, rather than one run-on line.
- If the user confirms emails were sent, the Daily Report’s corresponding bullets say “已发送” and its QuickBooks attachments remain unchanged.

