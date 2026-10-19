# Data Guide

`data.json` is the shared source of truth for the parking roster. Keep valid JSON syntax; JSON does not support comments, so use this guide for field explanations.

## `settings`
- `weekStartsOn`: first day of the roster week (`Monday`).
- `workingDays`: working days included in the roster.
- `parkingBays`: parking bay labels, the display does not assign fixed physical parking bays.
- `planningWeeks`: number of weeks shown in the schedule.
- `firstWeekStart`: fixed Monday anchor for rotation. Keep this stable to prevent the rotation restarting every week.
- `rotationOffset`: optional starting position in the employee queue.
- `startingBayDirection`: which employee in each weekly pair starts in Bay A (`AB` or `BA`).
- `lastUpdated`: timestamp of the last saved update.

## `employees`
Each employee has a stable `id`, display `name`, numeric `rotationOrder`, and `active` flag. Set `active` to `false` to deactivate an employee without deleting their record.

## `leavePeriods`
Annual leave records. Each record uses `employeeId`, `startDate`, `endDate`, and an optional non-sensitive `note`. Only the affected dates are skipped; the fixed rotation queue is not changed.

## `officeClosures`
Office-wide closure periods. Each record has `startDate`, `endDate`, and an optional `note`. During a full closed week the rotation does not advance; the schedule resumes after reopening.

## Other fields
- `manualOverrides`: optional day-specific bay assignments managed in the JSON.
- `weeklyAssignments`: saved historical week snapshots. Each record stores `weekStart`, `savedAt`, the weekly rotation pair, bay direction, and each weekday's saved Bay A/B assignment (including the employee ID and name at the time). Once a week is saved, the website reads that snapshot instead of recalculating it.
- `changeLog`: records changes made through the page.
- `_description`: explanatory metadata included in this starter JSON.

## Privacy
Do not store private leave reasons or other sensitive personal information in a public repository. Anyone can view files in a public GitHub repository.
