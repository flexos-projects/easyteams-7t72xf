---
id: "dashboard-page-spec"
title: "Dashboard"
type: "page"
status: "draft"
description: "Personal home screen showing tasks due today, overdue count, active projects grid with progress bars, and recent activity feed."
tags: ["page-spec", "dashboard", "home", "overview", "personal"]
createdAt: "2026-03-05"
updatedAt: "2026-03-05"
---

---
id: dashboard-page-spec
title: Dashboard
type: page
status: active
description: The personal home screen providing an overview of user-specific tasks, project progress, and recent activity within EasyTeams.
route: /dashboard
tags:
  - dashboard
  - home
  - overview
  - tasks
  - projects
createdAt: 2023-10-27T10:00:00Z
updatedAt: 2023-10-27T10:00:00Z
---

## Overview
The Dashboard serves as the primary landing page for authenticated users, offering a personalized overview of their most critical information. It's designed to help users quickly grasp their immediate priorities, monitor project progress, and stay informed about recent team activities. This page consolidates key data points to ensure users can start their workday efficiently.

## Requirements
*   Display tasks due today, specific to the logged-in user.
*   Show a prominent count of overdue tasks for the user.
*   Present a grid of active projects relevant to the user, including progress bars.
*   Feature a chronological feed of recent activities related to the user's projects and tasks.
*   All displayed items should be clickable, leading to their respective detail pages.
*   The page must load quickly and display up-to-date information.

## User Stories
*   **As a user, I want to see my tasks due today** so I can prioritize my immediate work.
*   **As a user, I want to know how many tasks are overdue** so I can address critical items quickly.
*   **As a user, I want to view the progress of my active projects** so I can stay informed about team goals.
*   **As a user, I want to see a feed of recent activities** so I can understand what's happening across my teams and projects.
*   **As a user, I want to click on any task, project, or activity item** to navigate to its details for more information.

## Acceptance Criteria
*   **AC1: Tasks Due Today**
    *   The 