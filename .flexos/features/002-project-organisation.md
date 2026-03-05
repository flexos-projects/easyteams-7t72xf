---
id: "project-organisation"
title: "Project Organisation"
type: "feature"
status: "draft"
priority: "P1"
description: "Enables users to group tasks into projects with customisable attributes and progress tracking."
tags: ["project-management", "task-management", "team-collaboration"]
createdAt: "2026-03-05"
updatedAt: "2026-03-05"
---

---
id: project-organisation
title: Project Organisation
type: feature
status: draft
description: Enables users to group tasks into projects with customisable attributes and progress tracking.
tags:
  - project-management
  - task-management
  - team-collaboration
relatesTo: []
createdAt: 2023-10-27T10:00:00Z
updatedAt: 2023-10-27T10:00:00Z
---

# Project Organisation

## Overview

This feature introduces a robust project management layer to easyteams, allowing users to organise tasks into distinct projects. Each project will have definable attributes such as a name, description, status, and a unique colour identifier. A key component of this feature is the automatic calculation of project progress, derived from the completion status of its associated tasks. This will provide team leads and members with a high-level view of project health and advancement.

## User Stories

*   **As a team lead**, I want to create a new project so that I can group related tasks together.
*   **As a team lead**, I want to define a project's name, description, status (e.g., 'Not Started', 'In Progress', 'Completed'), and assign a colour to it, so that projects are clearly identifiable and well-defined.
*   **As a team lead**, I want to assign specific team members to a project, so that only relevant individuals see and interact with project-related tasks.
*   **As a team member**, I want to view all projects I am assigned to, so that I can easily find and focus on my work.
*   **As a team lead**, I want to see the progress of a project as a percentage, calculated from its completed tasks, so that I can quickly assess its overall health.
*   **As a team lead**, I want to update the status of a project manually, independent of task progress, to reflect broader project milestones or decisions.
*   **As a team lead**, I want to add existing tasks to a project and create new tasks directly within a project, ensuring all related work is organised.

## Requirements

<flex_block type="requirements">
*   **FR1: Project Creation**: Users must be able to create new projects.
*   **FR2: Project Attributes**: Each project must support the following attributes:
    *   `name` (string, required, unique)
    *   `description` (string, optional)
    *   `status` (enum: 'Not Started', 'In Progress', 'On Hold', 'Completed', 'Archived')
    *   `colour` (hex code or predefined palette, required)
*   **FR3: Team Member Assignment**: Users must be able to assign one or more existing team members to a project.
*   **FR4: Task Association**: Tasks must be associable with a single project.
*   **FR5: Project Progress Calculation**: The system must automatically calculate project progress as a percentage based on the count of completed tasks divided by the total count of tasks within that project.
*   **FR6: Project Display**: Projects must be displayed in a dedicated view, showing their name, description, status, colour, assigned members, and progress percentage.
*   **FR7: Project Status Update**: Users must be able to manually update a project's status.
*   **FR8: Task Management within Project**: Users must be able to add new tasks directly within a project context and move existing tasks into a project.
*   **FR9: Permissions**: Only users with 'Team Lead' or 'Admin' roles can create, edit, or delete projects.
</flex_block>

## Acceptance Criteria

*   **AC1: Project Creation Form**
    *   A 'Create Project' button is available in the project dashboard.
    *   Clicking the button opens a modal/page with fields for Project Name, Description, Status, Colour Picker, and Team Member multi-select.
    *   Project Name field is required and has a character limit (e.g., 100 chars).
    *   Project Name must be unique within the user's team/organisation.
    *   Colour picker allows selection from a predefined palette or custom hex input.
    *   Upon successful creation, the new project appears in the project list.
*   **AC2: Team Member Assignment**
    *   The team member multi-select displays all active members of the team.
    *   Selected members are linked to the project and can be viewed in the project details.
    *   Only assigned members can view tasks belonging to that project (unless they have admin/global permissions).
*   **AC3: Task Association**
    *   When creating a new task, there is an option to assign it to an existing project.
    *   Existing tasks can be edited to be associated with a project.
    *   Tasks must belong to a project or be unassigned; they cannot belong to multiple projects.
*   **AC4: Project Progress Calculation**
    *   Given a project with 10 tasks, where 5 are marked 'Completed' and 5 are 'In Progress', the project's progress should display as 50%.
    *   If a project has no tasks, its progress should display as 0%.
    *   If all tasks in a project are 'Completed', its progress should display as 100%.
    *   Progress percentage updates in real-time or near real-time as task statuses change.
*   **AC5: Project Display**
    *   The project dashboard lists all projects accessible to the user.
    *   Each list item/card displays the project name, current status, assigned colour, and progress percentage.
    *   Clicking on a project item navigates to a detailed project view showing all attributes, assigned members, and a list of associated tasks.
*   **AC6: Project Status Update**
    *   Project status can be changed manually via a dropdown or dedicated button in the project details view.
    *   Changing the project status does not automatically change the status of its associated tasks.
*   **AC7: Permissions**
    *   Users with 'Team Lead' or 'Admin' roles can access and use project creation/editing functionalities.
    *   'Team Member' roles can view project details and tasks assigned to them, but cannot create, edit, or delete projects.

## Edge Cases

*   **Project with no tasks**: The project progress calculation should gracefully handle zero tasks (display 0%).
*   **Project with no assigned members**: Project can exist without assigned members, useful for planning phases.
*   **Archived/Deleted tasks**: Ensure that archived or deleted tasks do not contribute to the project progress calculation or task count.
*   **Deleting a project**: Prompt user for confirmation. Options could include: unassigning all associated tasks, deleting all associated tasks (with warnings), or only allowing deletion if no tasks are assigned.
*   **Renaming a project**: Ensure uniqueness validation still applies.
*   **Duplicate Project Names**: Prevent creation of projects with identical names within the same team/organisation.
*   **Visibility for unassigned users**: If a user is not assigned to a project, they should not see its details or tasks, unless they have admin permissions.

## Dependencies

*   **Task Management System**: Relies on the existing task creation, editing, status management, and deletion functionalities.
*   **User & Team Management System**: Relies on the ability to retrieve lists of active team members and their roles for assignment and permission checks.
*   **UI Component Library**: Requires a colour picker component and a multi-select component for team members.