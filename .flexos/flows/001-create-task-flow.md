---
id: "create-task-flow"
title: "Create New Task Flow"
type: "flow"
status: "draft"
description: "Describes the user flow for creating a new task within a project board."
tags: ["task", "create", "flow", "project-management", "easyteams"]
createdAt: "2026-03-05"
updatedAt: "2026-03-05"
relatesTo: ["./page/project-board.md", "./component/new-task-form.md"]
---

---
id: create-task-flow
title: Create New Task Flow
type: flow
status: active
description: Describes the user flow for creating a new task within a project board.
tags:
  - task
  - create
  - flow
  - project-management
  - easyteams
relatesTo:
  - ./page/project-board.md
  - ./component/new-task-form.md
createdAt: 2023-10-27T10:00:00Z
updatedAt: 2023-10-27T10:00:00Z
---

# Create New Task Flow

## Overview
This flow details the process a user follows to create a new task within an easyteams project. The focus is on a quick, intuitive task creation experience where the task appears instantly on the project board after submission.

## Trigger
The user initiates the flow by clicking a `+ New Task` button on the project board or a similar dedicated action.

<flex_block type="flow">
### Steps

1.  **Actor:** User
    **Action:** Clicks the `+ New Task` button, typically located in the project header, a column header, or a floating action button.
    **Outcome:** The system displays the "Create New Task" modal or a sidebar form.

2.  **Actor:** System
    **Action:** Presents the "Create New Task" form to the user.
    **Outcome:** The form includes:
        -   `Title` field (text input, required, max 255 characters).
        -   `Description` field (textarea, optional).
        -   `Assignee` dropdown/selector (optional, pre-populated with project members; defaults to 'Unassigned' if not selected).
        -   `Due Date` picker (optional).
        -   `Priority` dropdown (optional, e.g., Low, Medium, High; defaults to 'Medium').
        -   `Create Task` button (initially disabled until `Title` is provided).
        -   `Cancel` button or an "X" icon to close the form.

3.  **Actor:** User
    **Action:** Fills in the `Title` field. Optionally, they can add a `Description`, select an `Assignee`, choose a `Due Date`, and set a `Priority`.
    **Outcome:** The input fields are populated with user data. The `Create Task` button becomes enabled once the `Title` field contains text.

4.  **Actor:** User
    **Action:** Clicks the `Create Task` button.
    **Outcome:** The system receives the task creation request.

5.  **Actor:** System
    **Action:** Performs client-side and server-side validation on the submitted task data.
    **Outcome:**
        -   If validation passes: The system proceeds to create the task in the backend.
        -   If validation fails (e.g., missing required fields, invalid date format): The form remains open, and specific inline error messages are displayed next to the invalid fields.

6.  **Actor:** System
    **Action:** Creates a new task record in the database, associating it with the current project and the provided details.
    **Outcome:** The task is successfully persisted in the backend.

7.  **Actor:** System
    **Action:** Publishes the newly created task data to the frontend in real-time (e.g., via websockets or a polling mechanism).
    **Outcome:** The "Create New Task" modal/sidebar closes. The new task card instantly appears on the project board, typically in a default column (e.g., "To Do") or as specified by project settings. A transient success toast notification ("Task created successfully!") may be displayed.
</flex_block>

## Happy Path
1.  User clicks `+ New Task`.
2.  User fills in "Title: Implement login screen", leaves other fields optional.
3.  User clicks `Create Task`.
4.  System validates and creates the task.
5.  System closes the modal and the "Implement login screen" task card appears instantly on the project board in the "To Do" column.

## Error Paths

### 1. Missing Required Field
*   **Scenario:** User clicks `Create Task` without providing a `Title`.
*   **Actor:** System
*   **Action:** Displays an inline error message "Title is required" below the `Title` field.
*   **Outcome:** The `Create Task` button remains disabled or the form does not submit, and the user cannot proceed until a title is provided.

### 2. Invalid Date Format
*   **Scenario:** User manually types an invalid date (e.g., "31/31/2023") into the `Due Date` field (if direct input is allowed) or an API validation error occurs.
*   **Actor:** System
*   **Action:** Displays an inline error message "Invalid date format" or "Please select a valid date" below the `Due Date` field.
*   **Outcome:** The `Create Task` button remains enabled but submission fails, allowing the user to correct the date.

### 3. Backend/Network Error During Submission
*   **Scenario:** A network interruption occurs, or the backend service is temporarily unavailable when the user clicks `Create Task`.
*   **Actor:** System
*   **Action:** Displays a transient error toast notification (e.g., "Could not create task. Please try again later." or "Network error. Please check your connection.").
*   **Outcome:** The form remains open with the user's input, allowing them to retry the submission or cancel.

## Edge Cases

### 1. User Cancels Task Creation
*   **Scenario:** User opens the "Create New Task" form but decides not to create a task.
*   **Actor:** User
*   **Action:** Clicks the `Cancel` button or the "X" icon to close the modal/sidebar, or clicks outside the modal.
*   **Outcome:** The form closes without creating any task, and the project board remains unchanged.

### 2. Very Long Title or Description
*   **Scenario:** User enters a `Title` or `Description` that exceeds typical display limits.
*   **Actor:** System
*   **Action:** The UI should handle long text gracefully, typically by text wrapping for descriptions and potentially truncating with an ellipsis for titles on the task card, revealing full text on hover or in task details view.
*   **Outcome:** The task is created with the full text, and the UI adapts to display it effectively without breaking the layout.

### 3. Simultaneous Task Creation by Multiple Users
*   **Scenario:** Two or more users are creating tasks for the same project at roughly the same time.
*   **Actor:** System
*   **Action:** Each task creation request is processed independently.
*   **Outcome:** All successfully created tasks appear on the project board for all active users in real-time, maintaining data consistency.
