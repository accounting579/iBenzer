# Documented Failure Controls

This reference records the observed failures from the 2026 attendance work. It is not a substitute for the current source data; it is a mandatory anti-regression checklist.

## Failures that occurred and their controls

| Observed failure | Required prevention control |
| --- | --- |
| A result was typed/copied as a number instead of preserving or extending the peer formula. | Inspect the nearest complete formula, copy/adjust the formula pattern, then read the new formula back. Never use displayed values as proof of correctness. |
| An old period's hour, rate, salary, leave, or balance value was reused for the new period. | Calculate from current punches/current leave records only. Verify the current dates and source reference in every new block. |
| Only a personal Detail or only an attendance record was updated; Summary, Monthly, Weekly/Bi-Weekly Summary, payment table, or confirmation document was missed. | Start with the propagation matrix and check off every applicable destination before completion. |
| A new payroll/Monthly block was only partially built and did not match the full upper block. | Copy the entire reviewed structural block: headers, rows, formulas, styles, confirmation section, and links. Then replace current-period data. |
| The master Monthly block lacked the hyperlink to the source attendance workbook. | Validate the current-period source hyperlink and open/inspect its target before finishing. |
| Rate was treated as a single flat value despite a template with a split-rate calculation. | Preserve the employee/template-specific rate formula and test that each rate-tier hours and cash total agree with the Detail. |
| Blank yellow weekend cells were interpreted as absence or leave. | Check weekday/weekend/holiday status first. Yellow means weekend; blank yellow cells do not create AB. |
| A blank scheduled weekday was silently treated as regular work, absence, or vacation without a classification. | Classify every such day as approved leave, holiday, show/travel, or unapproved absence; escalate when evidence is missing. |
| Approved vacation reduced paid work hours instead of only reducing the vacation balance for a standard-time employee. | Determine the employee's established payroll model from their reviewed Detail. For paid vacation under a standard-hours model, keep standard paid hours and decrease Vacation Remain. |
| An employee-specific Hour model was applied to everyone. | Read the relevant employee's completed Detail and formula pattern. Hour handling is person/template-specific. |
| Late, early leave, and lunch were calculated incorrectly. | Separate pre-09:00/post-09:00 results; treat 09:00 as 0.5 h in the post-09:00 category; use 15 min = 0.25 h; exclude 12:00–12:30 when applicable; do not count post-17:00 departure as late; only early leave of at least 30 minutes qualifies. |
| Late values were not red and/or overtime was not blue; time display was not in the requested two-line daily format. | Perform visual QA on each employee row: red late, blue OT, two-line punch cell, yellow weekends, and unchanged borders/layout. |
| Early departure was ignored, or departure after 17:00 was incorrectly treated as late. | Compare the departure against 17:00 only. Flag early leave at 30+ minutes early; never treat a later departure as late. |
| Leave/AB hours were absent from Detail, totals, or Summary. | Reconcile each AB/leave entry from the source attendance record to employee Detail, employee Summary, and master period summary. |
| Lunch was included in an absence/leave calculation. | When an absence spans noon, subtract the 12:00–12:30 break before recording leave hours. |
| Confirmed exhibition/travel days were counted as absence. | Check the Show/Travel source and write the event name in the attendance record/Detail as required; exclude it from AB. |
| User-corrected current-period attendance was not reviewed before downstream work. | Treat the user's corrected `考勤记录` as the final source-of-truth and compare every downstream row to it before making changes. |
| Employee Summary was not updated after Detail changed. | Verify Summary cells contain/retain references to current Detail totals and recalculate expected values. |
| Company holiday/approved paid leave was not counted as attendance when no punch existed. | Check policy and eligibility; record paid attendance through the established formula/leave pattern, not by creating a missing-punch AB. |

## Failure-prevention sign-off

Do not declare the period complete until every applicable box is true:

- [ ] The manually corrected current `考勤记录` was reviewed before any downstream calculation.
- [ ] All formula-bearing cells in new/changed Detail, Summary, and Monthly blocks retain formulas or references.
- [ ] Every worker/day has a verified classification; weekends and holidays are not treated as absence.
- [ ] Pre-09:00 and post-09:00 late results, early leave, lunch exclusion, AB, OT, and show/travel were reconciled.
- [ ] Red late and blue OT formatting are visibly present where required.
- [ ] Each affected employee's Detail and Summary match the source attendance record.
- [ ] Master Detail, Weekly/Bi-Weekly block, the relevant Summary, payment table, and source hyperlink are updated.
- [ ] Rate tiers, paid hours, vacation balance, AB, and salary totals reconcile without copied prior-period values.
- [ ] Required salary confirmation material is updated when requested.
- [ ] Unresolved classifications or management decisions are explicitly listed for the user rather than guessed.
