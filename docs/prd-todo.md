# Product Requirements Document (PRD) - Todo App Enhancements (Due Dates, Priorities, Filters)

## 1. Overview

We are upgrading the existing basic Todo app (currently supporting only title and completion state) to add due dates, task priorities, and simple date-based filters. The goal is to make the app more practical for everyday task management while keeping it lightweight and easy to teach, with all data stored locally and no backend changes.

---

## 2. MVP Scope

- Add a `dueDate` field to each task:
  - Optional field.
  - Stored as an ISO `YYYY-MM-DD` string when present.
  - Invalid date values are ignored and treated as if no due date was set.
- Add a `priority` field to each task:
  - Enum: `"P1" | "P2" | "P3"`.
  - Default value is `"P3"` when the user does not choose a priority.
  - Display priority visually using color-coded badges:
    - `P1`: red.
    - `P2`: orange.
    - `P3`: gray.
- Maintain the existing `title` field as required.
- Keep storage local only:
  - No backend API or external storage changes.
  - All enhancements operate on the current local data model/storage approach.
- Add date-based filter views as tabs:
  - **All** tab:
    - Shows all tasks, including completed tasks.
  - **Today** tab:
    - Shows only incomplete tasks whose due date is today.
  - **Overdue** tab:
    - Shows only incomplete tasks whose due date is before today.

---

## 3. Post-MVP Scope

- Overdue task highlighting:
  - Visually emphasize overdue tasks (e.g., using red styling) so they stand out.
- Enhanced sorting rules for task lists:
  - Order tasks in the following priority:
    1. Overdue tasks first.
    2. Then by priority level (`P1` → `P2` → `P3`).
    3. Then by due date ascending (earlier dates first).
    4. Tasks without a due date appear last.

---

## 4. Out of Scope

- Notifications (email, push, or in-app alerts).
- Recurring or repeating tasks.
- Multi-user or shared task lists.
- Keyboard navigation and additional accessibility features beyond the current baseline.
- Any external or server-side storage; the app remains local-only.
