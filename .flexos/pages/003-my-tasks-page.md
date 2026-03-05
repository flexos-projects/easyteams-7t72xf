---
id: "my-tasks-page"
title: "My Tasks Page"
type: "page"
status: "draft"
description: "Personal task inbox filtered to tasks assigned to the current user, grouped by project, with quick status toggle and due date picker."
tags: ["tasks", "inbox", "personal", "page-spec"]
createdAt: "2026-03-05"
updatedAt: "2026-03-05"
---

---
id: my-tasks-page
title: My Tasks Page
type: page
status: draft
route: /my-tasks
description: Personal task inbox filtered to tasks assigned to the current user, grouped by project, with quick status toggle and due date picker.
createdAt: 2023-10-27T10:00:00Z
updatedAt: 2023-10-27T10:00:00Z
---

## Overview

The "My Tasks" page serves as a personal task inbox for the current user. It consolidates all tasks assigned to them across various projects, providing a centralized view to manage their workload. The page emphasizes quick actions for status updates and due date modifications to enhance user efficiency.

## Requirements

1.  **Personalized View**: Only display tasks assigned to the currently logged-in user.
2.  **Project Grouping**: Tasks must be grouped logically by the project they belong to.
3.  **Quick Actions**: Provide intuitive controls for changing task status and adjusting due dates directly within the task list.
4.  **Clear Status Indication**: Visually distinguish task statuses (e.g., To Do, In Progress, Done).
5.  **Due Date Visibility**: Clearly show the due date for each task, with overdue tasks highlighted.

## User Stories

*   **As a user**, I want to see all tasks assigned to me in one place so I can easily understand my current workload.
*   **As a user**, I want my tasks grouped by project so I can context-switch efficiently and see project-specific priorities.
*   **As a user**, I want to quickly mark a task as 'done' without navigating to a separate task detail page to save time.
*   **As a user**, I want to easily change a task's due date if plans change so I can keep my deadlines accurate.
*   **As a user**, I want to identify overdue tasks at a glance so I can prioritize urgent items.

## Acceptance Criteria

*   The page loads within 2 seconds for a user with up to 100 assigned tasks.
*   All tasks displayed are explicitly assigned to the logged-in user.
*   Tasks are visually grouped under collapsible project headers.
*   Each task item includes: task title, associated project name, current status, and due date.
*   Clicking a status indicator (e.g., a checkbox or dropdown) immediately updates the task status.
*   Clicking the due date opens a date picker, and selecting a new date updates the task's due date.
*   Overdue tasks are styled differently (e.g., red text, warning icon).
*   An empty state is displayed when no tasks are assigned to the user.

## Edge Cases

*   **No assigned tasks**: The page should display a friendly message indicating no tasks and possibly suggest how to get started or link to a project view.
*   **Task with no due date**: Due date field should be empty or indicate 'No Due Date', allowing one to be set.
*   **Task with deleted project**: The project name should display as '[Deleted Project]' or be omitted gracefully, and the task should still be accessible.
*   **Long project/task names**: Names should truncate with ellipses and a tooltip on hover.
*   **Many tasks in one project**: The project group should remain performant and scrollable, possibly with pagination or virtualized lists if performance becomes an issue.

## Route

`/my-tasks`

## Layout

This page utilizes the standard `AppLayout` which includes:

*   A persistent header with the application logo and global navigation/user profile controls.
*   A left-hand sidebar for primary navigation (e.g., Dashboard, Projects, Teams).
*   The main content area will house the 'My Tasks' specific elements.

## Sections

<flex_block type="sections">

### 1. Page Header (`.my-tasks-header`)

*   **Title**: "My Tasks"
*   **Description**: "Your personal task inbox."
*   **(Optional)** Right-aligned filter/sort controls (e.g., dropdown for sorting by due date, priority, or project; quick filter for 'Due Today', 'Overdue').

### 2. Task List Area (`.my-tasks-list-container`)

*   **Grouping**: Tasks are grouped by Project. Each project group starts with a `Project Header`.
    *   `Project Header`: Displays the project name, possibly a task count for that project, and could be collapsible.
*   **Task Item (`.task-item`)**: For each task within a project group:
    *   **Status Toggle**: A checkbox or a small dropdown component on the left to quickly change task status (e.g., To Do, In Progress, Done).
    *   **Task Title**: The main title of the task.
    *   **Due Date Picker**: A clickable element displaying the current due date. Clicking it opens a date picker to modify the due date. Overdue dates are highlighted.
    *   **(Optional)** Priority indicator (e.g., small flag icon).
    *   **(Optional)** Link to open task details page.

### 3. Empty State (`.my-tasks-empty-state`)

*   Displayed when `my-tasks-list-container` has no tasks.
*   **Message**: "You're all caught up! No tasks assigned to you."
*   **(Optional)** Call to action: "Explore Projects" button linking to the projects list.

</flex_block>

## Interactions

<flex_block type="interactions">

1.  **Toggle Task Status**: Clicking the status toggle (e.g., checkbox) for a task instantly updates its status in the backend and reflects the change visually. For dropdowns, selecting a new status from the menu updates.
2.  **Edit Due Date**: Clicking on the due date text for a task reveals a date picker. Selecting a new date from the picker updates the task's due date in the backend and on the UI.
3.  **Sort/Filter Tasks**: If filter/sort controls are present in the header, interacting with them will re-render the task list based on the selected criteria.
4.  **Navigate to Task Details**: Clicking the task title (if it's a link) or a dedicated 'details' icon/button will navigate the user to the `Task Details Page` (e.g., `/tasks/:taskId`).
5.  **Collapse/Expand Project Group**: Clicking the project header toggles the visibility of tasks within that project group.

</flex_block>

## Data Requirements

*   **`GET /api/v1/users/me/tasks`**: Fetches all tasks assigned to the current user.
    *   **Request parameters**: (Optional) `status`, `projectId`, `sortBy`, `sortOrder` for initial filtering/sorting.
    *   **Response data structure**:
        ```json
        [
          {
            "id": "string",
            "title": "string",
            "description": "string",
            "status": "enum (todo|in_progress|done)",
            "due_date": "datetime | null",
            "project_id": "string",
            "project_name": "string",
            "assigned_to_user_id": "string" // Should always match current user
          }
        ]
        ```
*   **`PATCH /api/v1/tasks/:taskId`**: Updates a specific task's properties.
    *   **Request body**:
        ```json
        {
          "status": "enum (todo|in_progress|done)",
          "due_date": "datetime | null"
        }
        ```

## Related Features

*   **Task Details Page**: For viewing and editing all details of a single task.
*   **Project Details Page**: For viewing all tasks and information related to a specific project.
*   **Global Search**: Tasks should be discoverable via global search.
*   **Notifications**: Users should receive notifications for newly assigned tasks or upcoming due dates for their tasks.