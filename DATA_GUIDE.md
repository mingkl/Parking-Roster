# Parking Roster — Data Guide

This guide describes the data file used by the static Parking Roster website.

## Settings
- `weekStartsOn`: the roster week starts on Monday.
- `workingDays`: Monday to Friday.
- `firstWeekStart`: fixed Monday anchor for the rotation. Keep this stable so the rotation does not restart each week.
- `rotationOffset`: optional starting position in the fixed employee queue.
- `planningWeeks`: legacy display setting; the current page shows the current week and three upcoming weeks.

The site allocates two shared parking permits. It does not display or rotate physical parking-bay labels.

## Employees
Each employee has a stable `id`, display `name`, numeric `rotationOrder`, and `active` flag. Set `active` to `false` to deactivate an employee without deleting their record. New employees should be added at the end of the queue.

## Annual leave (`leavePeriods`)
Each record uses `employeeId`, `startDate`, `endDate`, and an optional non-sensitive `note`.
- Leave is assessed separately for each Monday–Friday roster week.
- If an employee has leave recorded on 1–4 weekdays in that week, keep the employee in their normal assignment and display their name faded with a `Leave` label on the affected dates. Do not substitute.
- If an employee has leave recorded on all 5 weekdays in that roster week, skip the employee for that week and fill from the fixed queue.
- A skipped employee returns to their original queue position after leave and does not receive missed turns back.

## Office closures (`officeClosures`)
Each record has `startDate`, `endDate`, and an optional `note`. A fully closed Monday–Friday week pauses the rotation and does not consume a turn. Rotation resumes after reopening. Partial-week closures do not pause the whole week's turn.

## Legacy / compatibility fields
- `availabilityPeriods`: legacy data retained for compatibility. The current interface does not provide a Temporary Unavailability control.
- `manualOverrides`: legacy day-specific assignments. The current weekly allocation is calculated from the fixed rotation, leave, and closure rules; do not rely on old overrides to express the rotation policy.
- `weeklyAssignments`: legacy snapshots retained for compatibility. The current site recalculates schedules from the current rotation rules, leave and closures rather than using snapshots. Calculated past weeks may therefore change if the queue or leave records are edited.
- `changeLog`: browser-side change notes; this static site does not provide authenticated audit logging.

## Allocation priority
1. Keep the fixed employee order; do not permanently move employees because of leave or substitution.
2. Skip inactive employees and employees with 5 leave weekdays in the roster week.
3. Prefer employees who were not allocated in the previous open roster week, avoiding consecutive-week use when possible.
4. If there are not two distinct eligible employees, allow a repeat to keep both permits allocated. If only one employee is available, that person is shown as using both permits.
5. A person allocated as a substitute is covered by the same next-week skip rule as any person allocated in the prior week.
6. A short-leave employee still counts as allocated for the week, even when their name is marked `Leave` on the relevant dates.

## Privacy
Do not store private leave reasons, contact details, or other sensitive information in a public repository. Anyone can view files in a public GitHub repository.
