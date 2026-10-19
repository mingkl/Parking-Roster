# Data Guide

`data.json` is the shared source of truth for the parking roster. Keep valid JSON syntax; JSON does not support comments, so use this guide for field explanations.

## `settings`
- `weekStartsOn`: first day of the roster week (`Monday`).
- `workingDays`: working days included in the roster.
- `parkingBays`: parking bay labels, normally `A` and `B`.
- `planningWeeks`: number of weeks shown in the schedule.
- `firstWeekStart`: fixed Monday anchor for rotation. Keep this stable to prevent the rotation restarting every week.
- `rotationOffset`: optional starting position in the employee queue.
- `startingBayDirection`: which employee in each weekly pair starts in Bay A (`AB` or `BA`).
- `lastUpdated`: timestamp of the last saved update.

## `employees`
Each employee has a stable `id`, display `name`, numeric `rotationOrder`, and `active` flag. Set `active` to `false` to deactivate an employee without deleting their record.

## `leavePeriods`
Annual leave records. Each record uses `employeeId`, `startDate`, `endDate`, and an optional non-sensitive `note`. Only the affected dates are skipped; the fixed rotation queue is not changed.

## `availabilityPeriods`
Temporary unavailability records. Each record uses `employeeId`, `startDate`, optional `endDate`, and an ID. If `endDate` is `null`, the unavailability continues until the record is removed or updated.

## `officeClosures`
Office-wide closure periods. Each record has `startDate`, `endDate`, and an optional `note`. During a full closed week the rotation does not advance; the schedule resumes after reopening.

## Other fields
- `manualOverrides`: optional day-specific bay assignments managed in the JSON.
- `weeklyAssignments`: reserved for saved weekly assignments/history.
- `changeLog`: records changes made through the page.
- `_description`: explanatory metadata included in this starter JSON.

## Privacy
Do not store private leave reasons or other sensitive personal information in a public repository. Anyone can view files in a public GitHub repository.
