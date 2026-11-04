# Attendance Rules and Review Checklist

## Baseline schedule and display

- Normal workday: 08:30–17:00.
- Lunch: 12:00–12:30. Do not count the lunch interval as work time or leave when an interval crosses it.
- Daily time cells normally place clock-in and clock-out on separate lines in the same cell.
- Yellow dates/cells are weekends. Their blanks are not leave.
- Late-related entries are red. Overtime entries are blue.

## Lateness and early leave

- Keep pre-09:00 and 09:00-or-later records distinct in the designated count, minute, and leave columns.
- Record 09:00 as a 0.5-hour late event in the post-09:00 category; do not combine it with the pre-09:00 accumulation.
- Use quarter-hour increments: 15 min = 0.25 h, 30 min = 0.5 h.
- Do not treat any departure after 17:00 as lateness. Early leave begins only when the employee leaves at least 30 minutes before 17:00.
- Follow the workbook's existing policy formula for how minute totals translate to leave/deduction; preserve it instead of re-implementing it as static values.

## Leave, holidays, shows, and vacation

- Blank normally scheduled days must be classified—approved leave, company holiday, show/business travel, or absence—before totals are changed.
- Confirmed exhibition/show participation or travel is entered as the show/event name, not absence.
- Company policy currently recorded:
  - Paid sick day: one day after every two worked months, maximum five days per year.
  - Vacation: five days after one year, eight after two years, ten after five years.
  - Holidays: New Year's Day; Chinese New Year's Day (2–6 PM half day); Memorial Day; Independence Day; Labor Day; Thanksgiving Day; Christmas Day.
- Holidays count as attendance without punches when applicable.
- Vacation reduces remaining vacation. It does not, by itself, reduce paid standard work hours for an employee whose established payroll pattern treats approved vacation as paid time.

## Cross-sheet propagation matrix

| Source change | Must be checked downstream |
| --- | --- |
| Punch / late / early leave / OT | Period `考勤记录`, employee month Detail, employee Summary, master Detail block, period summary |
| Vacation / paid leave / holiday | Employee leave table, Detail balance, master Summary vacation add/remain, paid-hour model |
| Show / travel | Period record name/notes, employee Detail, related master block; ensure it is not counted as AB |
| New weekly/bi-weekly period | Full master payroll block, source workbook hyperlink, Weekly/Bi-Weekly Summary, payment table, salary confirmation when requested |
| Rate or salary split | Employee Detail formula, master payroll calculation, Summary, confirmation document |

## Period-close checklist

1. Start from a user-reviewed complete period’s structure, not its values.
2. Validate every current-period date, worker, formula reference, hyperlink, rate, and leave balance.
3. Reconcile source totals to employee Detail and master Summary.
4. Check red late formatting and blue OT formatting visibly.
5. Confirm all required monthly/weekly/bi-weekly blocks exist in full and source links are present.
6. Escalate ambiguities; never fill unknown days, leave, rates, or payment decisions by inference.
