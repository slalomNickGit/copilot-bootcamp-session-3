# Epics and Stories - Todo App Enhancements

> Generated based on requirements in docs/prd-todo.md and following the structure of docs/templates/epic-and-stories-template.md.

## MVP Epics and Stories

- Epic: Add Due Dates to Tasks
  - Story: Add due date field to task data model
    - Acceptance Criteria:
      - Each task record includes an optional dueDate field.
      - When present, dueDate is stored as an ISO YYYY-MM-DD string.
      - Tasks without a due date are treated as having no due date in all views and logic.
  - Story: Add due date input to task creation form
    - Acceptance Criteria:
      - Users can optionally specify a due date when creating a new task.
      - The due date input accepts a calendar/date control constrained to valid calendar dates.
      - If the user provides no due date, the task is saved without a dueDate value.
  - Story: Add due date editing to existing tasks
    - Acceptance Criteria:
      - Users can add, change, or clear the due date on an existing task.
      - Updated due dates are persisted and reflected in all relevant views.
      - Clearing the due date removes the stored dueDate value from the task.
  - Story: Ignore and sanitize invalid due date values
    - Acceptance Criteria:
      - Inputs that are not valid ISO YYYY-MM-DD dates are treated as if no due date was provided.
      - Tasks with invalid dueDate values do not cause errors in list or filter views.
      - Any previously stored invalid dueDate values are effectively ignored by filtering and sorting logic.

- Epic: Add Task Priority Levels
  - Story: Add priority field to task data model
    - Acceptance Criteria:
      - Each task includes a priority field with allowed values "P1", "P2", or "P3".
      - Existing tasks without an explicit priority are updated or interpreted with a valid priority value.
  - Story: Default task priority to P3 when unspecified
    - Acceptance Criteria:
      - New tasks created without a chosen priority are saved with priority "P3".
      - The default priority is visible in the UI when the user does not change it.
  - Story: Add priority selection to task creation form
    - Acceptance Criteria:
      - Users can choose between P1, P2, and P3 when creating a task.
      - The selected priority is persisted on save and shown correctly in task lists.
  - Story: Add priority editing to existing tasks
    - Acceptance Criteria:
      - Users can change the priority of any existing task to P1, P2, or P3.
      - Updated priority values are persisted and reflected in all views that show tasks.
  - Story: Display priority as color-coded badges
    - Acceptance Criteria:
      - Each task displays a priority badge with the correct label (P1, P2, or P3).
      - P1 badges appear in red, P2 badges in orange, and P3 badges in gray.
      - Priority badges are visible in the main task list views.

- Epic: Add Date-Based Task Filters
  - Story: Implement All tab to show all tasks
    - Acceptance Criteria:
      - An All tab is available in the UI alongside other filter tabs.
      - The All tab displays all tasks regardless of completion state, due date, or priority.
      - Switching to the All tab updates the list immediately without requiring a page reload.
  - Story: Implement Today tab to show today’s incomplete tasks
    - Acceptance Criteria:
      - A Today tab is available in the UI.
      - The Today tab displays only tasks that are not completed and have a dueDate equal to the current calendar date.
      - Tasks without a dueDate or with a non-today dueDate do not appear in the Today tab.
  - Story: Implement Overdue tab to show overdue incomplete tasks
    - Acceptance Criteria:
      - An Overdue tab is available in the UI.
      - The Overdue tab displays only tasks that are not completed and have a dueDate earlier than the current date.
      - Tasks without a dueDate or with due dates today or in the future do not appear in the Overdue tab.

- Epic: Preserve Local-Only Storage
  - Story: Confirm enhancements work with existing local storage
    - Acceptance Criteria:
      - All new task fields (dueDate and priority) are persisted using the existing local storage mechanism.
      - Previously saved tasks remain accessible and continue to function after the enhancements.
      - No user data loss occurs when updating from the basic version to the enhanced version.
  - Story: Ensure no backend or external storage is introduced
    - Acceptance Criteria:
      - The app continues to function without requiring any server or network connectivity.
      - No new API calls or external storage services are used for saving or loading tasks.

## Post-MVP Epics and Stories

- Epic: Highlight Overdue Tasks
  - Story: Visually emphasize overdue tasks in task list
    - Acceptance Criteria:
      - Overdue tasks are visually distinct from non-overdue tasks in all list views where they appear.
      - The chosen visual style clearly communicates that a task is overdue (for example, using red text or background consistent with the design).
      - Completed tasks do not appear as overdue in Today or Overdue tabs.

- Epic: Advanced Task Sorting
  - Story: Sort tasks with overdue tasks first
    - Acceptance Criteria:
      - In supported views, overdue tasks appear before all non-overdue tasks.
      - Changing a task from non-overdue to overdue (or vice versa) updates its relative position in the list.
  - Story: Sort tasks by priority P1 to P3 within groups
    - Acceptance Criteria:
      - Within the overdue group and within the non-overdue group, tasks are ordered by priority from P1 to P3.
      - Tasks with the same priority remain grouped together before lower-priority tasks.
  - Story: Sort tasks by due date ascending within priority
    - Acceptance Criteria:
      - For tasks sharing the same overdue status and priority, tasks with earlier due dates appear before later due dates.
      - Tasks with identical due dates are allowed in any order relative to each other.
  - Story: Place tasks without due dates at the end of lists
    - Acceptance Criteria:
      - Tasks without a dueDate appear after all tasks with a dueDate when lists are sorted.
      - Undated tasks still respect the priority ordering relative to each other if applicable.
