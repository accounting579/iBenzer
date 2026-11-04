---
name: una-daily-task-sync
description: Sync Una's Dida completed and open work with the Admin & Acct Google Sheet's Una对接 tracker, keeping completed work accurately dated and below active work. Use for requests to update today's work, Dida completions, or Una task status.
---

# Una Daily Task Sync

## 公司固定执行与错误闭环
开始此工作流前，先读取 [公司固定规则](../../references/company-operating-rules.md)。该规则适用于本 Skill 的所有步骤；如与当前用户明确指令冲突，以用户当次明确指令为准。


Maintain the user's master task tracker in **Admin & Acct → Una对接**. Treat this sheet as the source of truth for work tracking; do not create a separate Notion page or replacement tracker unless explicitly asked.

## Core rules

- Read Dida/滴答清单 first. The native Dida app or Dida webpage is authoritative when the generic TickTick connector does not return the user's tasks.
- When the user says a task is completed, or Dida shows it completed, update the corresponding tracker record in the same pass. Do not wait for a separate reminder.
- A completed record must have:
  - `状态 = 已完成`
  - `完成时间 = actual completion date` (use the Dida completion date; otherwise use the date the user confirmed completion)
  - a short factual `当前进展` note stating the source and completion
  - no future next-follow-up or active blocker, unless the user explicitly describes a separate unresolved issue.
- Preserve the original deadline. The tracker’s deadline formatting already excludes `已完成` rows from urgency highlighting.
- `更新 Return` is a continuing system, not a permanently completed project. If a Dida instance is complete, record that cycle in 当前进展 but keep the master Return task `进行中`.
- Brian’s routine daily `Bid Prime` is not Una work. Do not add or mark it as Una’s daily task unless there is an approved exception needing Una/Leon confirmation, signature, historical data, or escalation.
- Exclude personal habits/reminders from Una对接 unless the user explicitly asks to track them there.
- If the user names a different exact tracker, such as Notion → `2，工作安排 - Una` → `工作清单（可选状态与日期）`, write to that existing database only. Never create a similarly named replacement page, personal summary page, or narrative list below the database.
- Record one row per distinct task and update the existing row instead of creating repeated rows for progress updates. Include the arranged date, current status, purpose/scope, current progress, next step, expected completion date, blocker/decision owner, and whether the result is a draft awaiting review.
- When the user asks to migrate completed work from a date onward, inspect the full requested date range and move every supported completed item into the tracker table; do not leave some items only in a daily-summary section below.

## Completion-and-order workflow

1. Inspect recent Dida completed tasks since the last tracker sync, plus any completion the user directly states.
2. Match each business task to an existing Una对接 record by task meaning, not only exact punctuation. Avoid duplicate records.
3. Update all matched records, including completion time and progress note. Create a new completed record only for a business task with no matching record.
4. Keep active work at the top and completed work below it. After each synchronization, reorder the tracker so `进行中` / `待确认` / `待处理` records appear before `已完成` records. Within active work, put P0, P1, P2, then P3; use deadline to break ties when practical.
5. Do not delete past completed records. They remain as a compact history at the bottom.

## Simple daily view

Keep detailed data but show only these columns by default:

`任务名称 | 状态 | 优先级 | 完成时间 | 截止日期 | 下一步动作 | 当前进展`

Keep synchronization key, category, follow-up date, blocker, and remarks as retained hidden fields. Do not delete their data merely to simplify the view.

## Safety and verification

- Before editing, read sheet metadata and the target row(s), including validation for Status and Priority.
- Use exact allowed dropdown values: status `待处理`, `进行中`, `待确认`, `已完成`; priority `P0 紧急`, `P1 重要`, `P2 常规`, `P3 计划`.
- Preserve formatting, formulas, filters, and all unrelated rows.
- After a batch update, verify the updated cells and confirm completed rows use the green completion formatting and no longer trigger deadline urgency highlighting.
- Verify the exact destination title and parent location before writing, then read back the written rows and confirm there is no duplicate replacement tracker or stray narrative summary.
- Briefly report what was synchronized, any excluded personal/Brian items, and the tracker link.

