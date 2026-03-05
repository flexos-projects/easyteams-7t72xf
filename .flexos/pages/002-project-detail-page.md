---
id: "project-detail-page"
title: "Project Detail Page"
type: "page"
status: "draft"
description: "Displays a project's full task list with multiple views, filters, bulk actions, and project settings."
tags: ["project", "tasks", "kanban", "list-view", "settings", "page-spec"]
createdAt: "2026-03-05"
updatedAt: "2026-03-05"
---

---
id: project-detail-page
title: Project Detail Page
type: page
status: active
route: /projects/:projectId
---

## Overview
This page provides a comprehensive view of a specific project within easyteams. It allows users, primarily project managers and team members, to manage all associated tasks, monitor progress through different views, apply filters, perform bulk actions, and configure project-level settings.

## Requirements
*   Display all tasks belonging to a specific project.
*   Allow users to toggle between Kanban and List views for tasks.
*   Provide filtering capabilities by assignee, task status, and priority.
*   Enable users to perform bulk actions on selected tasks.
*   Offer a dedicated sidebar for managing project settings.
*   Ensure responsive design for various screen sizes.

## User Stories
*   As a Project Manager, I want to see all tasks for my project in one consolidated view so I can easily track overall progress.
*   As a Team Member, I want to quickly filter tasks by my name so I can focus on my assigned work items.
*   As a Project Manager, I want to switch between Kanban and List views so I can choose the best visualization method for different planning or reporting needs.
*   As a Team Lead, I want to update the status of multiple tasks at once so I can efficiently manage team workflow after a sprint review.
*   As a Project Owner, I want to access and modify project settings (e.g., name, description, members) directly from the project page so I can easily maintain project configurations.
*   As a Project Manager, I want to add a new task quickly from the project detail page.

## Acceptance Criteria
*   The page must successfully load and display all tasks associated with the `:projectId` in the URL.
*   A toggle (e.g., buttons or tabs) labeled "Kanban" and "List" must be present and functional.
*   Selecting "Kanban" must render tasks as cards arranged in columns corresponding to task statuses.
*   Selecting "List" must render tasks as rows in a sortable table.
*   Filter controls for "Assignee", "Status", and "Priority" must be clearly visible and allow selection of multiple options.
*   Applying a filter must instantly update the displayed task list without a full page refresh.
*   Each task item (card or row) must include a selectable checkbox for bulk actions.
*   A "Bulk Actions" menu/bar must appear only when one or more tasks are selected, offering options like "Change Status", "Assign", "Delete", "Set Priority".
*   A dedicated sidebar for "Project Settings" must be accessible, either always visible or toggleable.
*   Clicking on any task (card in Kanban, row in List) must navigate to the detailed Task View page or open a task detail modal.
*   Clicking an "Add Task" button must open a modal for new task creation, pre-filled with the current project ID.

## Edge Cases
*   **No tasks in the project**: The task display area should show a clear message like "No tasks found. Click 'Add Task' to get started." instead of an empty view.
*   **Project not found**: If `:projectId` does not exist, the user should be redirected to a projects list page or a 404 error page.
*   **User permissions**: Actions like "Delete Project" or modifying certain project settings should be disabled or hidden if the user lacks the necessary permissions. Bulk actions should also respect user permissions for task modification.
*   **Large number of tasks**: For projects with hundreds or thousands of tasks, the page should implement pagination, infinite scroll, or virtualization to maintain performance and responsiveness.
*   **No assignees/statuses/priorities configured**: Filter dropdowns should clearly indicate if no options are available or provide defaults.
*   **Empty search results**: Display a message indicating no tasks match the search query.

## Route
`/projects/:projectId`

## Layout
The page will utilize the standard application layout, including a global header with navigation and a main content area. The project details and tasks will occupy the primary content space, with an optional or persistent sidebar for project settings.

## Sections
<flex_block type="sections">
### 1. Project Header
*   **Project Title**: Displays the name of the current project (e.g., "easyteams Backend Development").
*   **Add Task Button**: A primary call-to-action button (e.g., "+ Add Task") to quickly create a new task within the project.
*   **View Toggle**: A component allowing users to switch between "Kanban" and "List" views.

### 2. Filters & Search Bar
*   **Assignee Filter**: A dropdown or multi-select component to filter tasks by one or more assigned users.
*   **Status Filter**: A dropdown or multi-select component to filter tasks by their current status (e.g., To Do, In Progress, Done).
*   **Priority Filter**: A dropdown or multi-select component to filter tasks by their priority level (e.g., High, Medium, Low).
*   **Search Input**: A text input field to search tasks by title or description.

### 3. Bulk Actions Bar
*   **Visibility**: This bar appears only when one or more tasks are selected via their checkboxes.
*   **Selected Count**: Displays the number of tasks currently selected (e.g., "3 tasks selected").
*   **Actions Dropdown**: A dropdown menu offering actions applicable to all selected tasks (e.g., "Change Status", "Assign", "Delete Selected", "Set Priority").

### 4. Task Display Area (Dynamic)
#### 4.1. Kanban View
*   **Columns**: Each column represents a task status (e.g., "To Do", "In Progress", "Done", "Blocked"). These columns should be configurable in project settings.
*   **Task Cards**: Within each column, tasks are displayed as cards. Each card shows: Task Name, Assignee (avatar & name), Due Date, Priority indicator, and a checkbox for selection.
*   **Drag-and-Drop**: Tasks should be draggable between columns to change their status.

#### 4.2. List View
*   **Table Structure**: A table with sortable columns.
*   **Columns**: Checkbox, Task Name, Assignee, Due Date, Status, Priority, Tags, and a context menu for individual task actions (e.g., Edit, Delete, Duplicate).
*   **Task Rows**: Each row represents a task with its details.

### 5. Project Settings Sidebar
*   **Toggle/Visibility**: Can be toggled open/closed or remain persistently open depending on layout context (e.g., desktop vs. mobile).
*   **Sections**: A list of clickable sections for project configuration:
    *   **General**: Project Name, Description, Owner.
    *   **Members**: Manage project team members and their roles.
    *   **Statuses**: Configure custom task statuses and their order (which dictates Kanban columns).
    *   **Labels/Tags**: Manage project-specific tags for tasks.
    *   **Permissions**: Define access levels for project actions.
    *   **Integrations**: Link to external services.
    *   **Advanced**: Options like archiving or deleting the project.
</flex_block>

## Interactions
<flex_block type="interactions">
*   **View Toggle Click**: Clicking "Kanban" or "List" switches the `Task Display Area` content.
*   **Filter Selection**: Selecting an option from any filter dropdown (`Assignee`, `Status`, `Priority`) immediately updates the tasks shown in the `Task Display Area`.
*   **Search Input**: Typing in the search bar filters tasks in real-time by title or description.
*   **Task Checkbox Click**: Toggles the selection state of an individual task. If any task is selected, the `Bulk Actions Bar` becomes visible. If no tasks are selected, it hides.
*   **Bulk Actions Dropdown Selection**: Choosing an action from the dropdown in the `Bulk Actions Bar` (e.g., "Change Status") triggers a modal or a prompt to confirm or provide further input, then applies the action to all selected tasks.
*   **Task Card/Row Click**: Clicking on a task card (Kanban) or row (List) navigates to the `Task Detail Page` (e.g., `/tasks/:taskId`) or opens a detailed task modal.
*   **Kanban Drag-and-Drop**: Dragging a task card from one status column to another updates the task's status in the backend and reflects it in the UI.
*   **Add Task Button Click**: Opens a modal for creating a new task, pre-populating the project ID.
*   **Project Settings Sidebar Toggle**: Clicking an icon or button toggles the visibility of the `Project Settings Sidebar`.
*   **Project Settings Section Click**: Clicking a section in the `Project Settings Sidebar` displays its corresponding configuration options within the sidebar or a dedicated area.
*   **Table Header Click (List View)**: Sorts the task list by the clicked column (e.g., by Due Date, Assignee).
</flex_block>

## Data Requirements
*   **Project Data**: `id`, `name`, `description`, `ownerId`, `createdAt`, `updatedAt`, `statusWorkflow` (list of configurable statuses for Kanban columns), `memberIds`, `isArchived`.
*   **Task Data**: `id`, `projectId`, `title`, `description`, `assigneeId`, `status`, `priority`, `dueDate`, `createdAt`, `updatedAt`, `tags`.
*   **User Data**: `id`, `firstName`, `lastName`, `email`, `avatarUrl` (for assignees).
*   **Permissions Data**: User roles and associated permissions for project and task actions.

## Related Features
*   **Task Detail Page**: `/tasks/:taskId`
*   **Create Task Modal**: Triggered from "Add Task" button.
*   **Project List Page**: `/projects`
*   **User Profile Page**: `/users/:userId` (for assignee clicks)
*   **Global Search**: Integration with project-specific search functionality.