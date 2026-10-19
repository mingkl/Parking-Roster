# Data Guide

`data.json` is the shared source of truth for the parking roster. Keep valid JSON syntax; JSON does not support comments, so use this guide for field explanations.

## `settings`
- `weekStartsOn`: first day of the roster week (`Monday`).
- `workingDays`: working days included in the roster.
- `planningWeeks`: number of weeks shown in the schedule.
- `firstWeekStart`: fixed Monday anchor for rotation. Keep this stable to prevent the rotation restarting every week.
- `rotationOffset`: optional starting position in the employee queue.
- `lastUpdated`: timestamp of the last saved update.

## `employees`
Each employee has a stable `id`, display `name`, numeric `rotationOrder`, and `active` flag. Set `active` to `false` to deactivate an employee without deleting their record.

## `leavePeriods`
Annual leave records. Each record uses `employeeId`, `startDate`, `endDate`, and an optional non-sensitive `note`. If the record covers 1–4 Monday–Friday workdays, the employee remains listed on the roster and their name is faded with a “Leave” label on affected weekdays. If the record covers 5 or more Monday–Friday workdays, the employee is skipped for any roster week overlapping that leave period, and the next eligible employee in the fixed queue fills the slot. The employee remains in their original rotation order and returns to normal rotation after leave.

## `officeClosures`
Office-wide closure periods. Each record has `startDate`, `endDate`, and an optional `note`. During a fully closed Monday–Friday week the rotation does not advance; the schedule resumes after reopening. A week with at least one open workday consumes its normal rotation turn.

## Other fields
- `manualOverrides`: optional date-specific assignment overrides in the JSON. These are advanced settings and should be edited carefully.
- `weeklyAssignments`: legacy field retained for compatibility. The current site calculates past and future schedules from the current rotation rules and leave/closure records rather than using saved snapshots.
- `changeLog`: records changes made through the page.
- `_description`: explanatory metadata included in this starter JSON.

## Privacy
Do not store private leave reasons or other sensitive personal information in a public repository. Anyone can view files in a public GitHub repository.
