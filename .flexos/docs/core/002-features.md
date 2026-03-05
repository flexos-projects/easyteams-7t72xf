---
id: features-002
title: "Core Features"
description: "A detailed breakdown of the core features and functionalities of the easyteams platform."
type: doc
subtype: core
status: draft
sequence: 2
tags:
  - features
  - product
  - scope
createdAt: "2023-10-27T10:01:00Z"
updatedAt: "2023-10-27T10:01:00Z"
---

# Core Features

This document outlines the primary features of the easyteams platform. Each feature is designed to solve a specific set of problems related to team management, and they work together to create a cohesive experience. All features listed are considered P0 (critical for launch) unless otherwise noted.

## 1. Holiday & Leave Management

This module is the cornerstone for planning and tracking all types of employee time off.

*   **Description:** It provides a comprehensive system for employees to request leave and for managers to approve it. The system maintains an accurate, real-time record of leave balances and team availability. All data is stored in the `leave_requests` collection, as detailed in the [Database Document](./004-database.md).
*   **Key Functionality:**
    *   **Employee Self-Service:** Users can view their remaining holiday allowance, see a history of their past requests, and submit new requests for various leave types (Holiday, Sick, etc.) through the **Leave Hub** page.
    *   **Manager Approval Workflow:** Managers receive notifications for new requests and can approve or deny them from their **Dashboard** or the **Leave Hub**. They have access to a team calendar to check for potential scheduling conflicts before making a decision.
    *   **Customizable Policies:** Admins can configure company-wide leave policies in the **Company Admin Settings**, including annual allowance, carry-over rules, and different leave types.
*   **User Stories:**
    *   As an employee, I want to see my remaining holiday allowance so I can plan my vacations accurately.
    *   As a manager, I want to view my team's upcoming leave on a shared calendar to avoid staffing conflicts.

## 2. Expense Tracking & Approval

This feature streamlines the entire expense claim and reimbursement process.

*   **Description:** It enables employees to digitally submit expenses with receipts, which are then routed to their managers for approval. This eliminates paper forms and manual tracking. All expense data is stored in the `expenses` collection.
*   **Key Functionality:**
    *   **Receipt Upload:** Employees can quickly submit an expense via the **Expenses Manager** page by uploading a photo or file of their receipt. The system uses Cloudinary for robust image handling, as noted in the [Technical Document](./007-technical.md).
    *   **Categorization:** Expenses can be categorized (e.g., 'Travel', 'Meals', 'Software') based on a list defined by the company admin.
    *   **Approval Queue:** Managers see a clear queue of pending expenses. They can view all details, including the attached receipt, before approving or rejecting a claim.
    *   **Export for Accounting:** Approved expenses can be easily exported by an admin or accountant for processing in external accounting software.
*   **User Stories:**
    *   As an employee, I want to quickly upload a photo of a receipt and submit it as an expense.
    *   As a manager, I want to review submitted expenses with all details and receipts clearly visible before approving.

## 3. Onboarding Workflow Automation

This module ensures a consistent, organized, and welcoming experience for new hires.

*   **Description:** It allows HR managers to create standardized onboarding checklists and assign tasks to relevant people (the new hire, their manager, IT, etc.). Progress is tracked centrally, ensuring nothing is missed. This is managed through the `onboarding_tasks` collection.
*   **Key Functionality:**
    *   **Customizable Templates:** Admins can build onboarding templates for different roles or departments in the **Company Admin Settings**.
    *   **New Hire Portal:** New hires get access to the **Onboarding Center**, a dedicated page showing their personalized checklist, links to important documents, and introductions to the team.
    *   **Task Assignment & Notifications:** Tasks are automatically assigned to the correct individuals, who receive notifications when a task is due. This ensures accountability and timely completion.
    *   **Progress Tracking:** HR and managers can monitor the onboarding progress for all new hires from a central dashboard.
*   **User Stories:**
    *   As an HR manager, I want to create a standardized onboarding checklist for different roles.
    *   As a new hire, I want a clear list of tasks to complete during my first weeks.

## 4. 360 Performance Review System

This feature facilitates structured, comprehensive, and fair performance reviews.

*   **Description:** It supports 360-degree feedback cycles where input is gathered from the employee (self-assessment), their peers, and their manager. The goal is to foster a culture of continuous growth and development. Review data is stored in the `performance_reviews` collection.
*   **Key Functionality:**
    *   **Cycle Management:** HR admins can set up, schedule, and manage review cycles from the **Performance Reviews** page. This includes setting timelines and selecting participants.
    *   **Feedback Submission:** Participants receive notifications and can easily submit their feedback through a structured form. Anonymity can be configured on a per-cycle basis.
    *   **Consolidated Reports:** Once a cycle is complete, the system generates a consolidated report for the manager, presenting all feedback in an organized and easy-to-digest format.
    *   **Goal Setting:** The module includes functionality for employees and managers to set and track performance goals throughout the year.
*   **User Stories:**
    *   As a manager, I want to initiate a 360-degree review for a team member and invite specific colleagues to contribute.
    *   As an employee, I want to easily submit self-assessments and provide peer feedback during a review cycle.

## 5. User Authentication & Authorization (P0)

This is a foundational feature ensuring secure access to the platform. It leverages Firebase Authentication for reliability.

*   **Description:** Provides secure user signup, login, password management, and role-based access control (RBAC). Roles (e.g., employee, manager, admin) dictate what features and data a user can access.

## 6. Company Settings & Policy Configuration (P1)

This admin-focused feature allows each company to tailor the platform to its specific needs.

*   **Description:** A dedicated section where administrators can configure company-wide settings, such as holiday policies, expense categories, and onboarding templates. This ensures the platform aligns with the company's internal processes and culture.