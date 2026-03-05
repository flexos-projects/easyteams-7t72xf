---
id: pages-003
title: "Application Pages"
description: "An overview of the key pages and views within the easyteams application, their purpose, and their structure."
type: doc
subtype: core
status: draft
sequence: 3
tags:
  - ux
  - ui
  - frontend
createdAt: "2023-10-27T10:02:00Z"
updatedAt: "2023-10-27T10:02:00Z"
---

# Application Pages

This document describes the primary pages that constitute the easyteams user interface. Each page is designed to serve a specific purpose and user role, contributing to a clear and intuitive navigation structure. The overall navigation pattern will be a persistent sidebar for authenticated users, as specified in the [Design Document](./006-design.md).

## Public Pages (Authentication Not Required)

### 1. Landing Page (`/`)
*   **Description:** This is the main public-facing marketing page. Its goal is to communicate the value proposition of easyteams and convert visitors into signups or demo requests.
*   **Sections:**
    *   **Hero Section:** A compelling headline, the tagline, and primary call-to-action buttons ("Start Free Trial", "Request a Demo").
    *   **Feature Highlights:** A visually engaging overview of the core features: Holiday Management, Expense Tracking, Onboarding, and Performance Reviews.
    *   **Social Proof:** Testimonials from early adopters or representative customer quotes.
    *   **Pricing:** A clear breakdown of the subscription plans.
    *   **Footer:** Standard links to about, contact, privacy policy, etc.

### 2. Login / Sign Up Page (`/auth`)
*   **Description:** The entry point for new and returning users. It provides forms for authentication and account creation.
*   **Sections:**
    *   **Login Form:** Fields for email and password.
    *   **Sign Up Form:** Fields for name, work email, password, and company name.
    *   **Password Reset Link:** A link to a flow for users who have forgotten their password.
    *   **Social Login:** Buttons for Google and Microsoft authentication to speed up the process.
*   **Related Features:** `user-authentication`.

## Authenticated Pages (Login Required)

### 3. Dashboard (`/dashboard`)
*   **Description:** The personalized home base for every logged-in user. It provides a high-level summary and quick access to pending tasks and important information.
*   **Sections:**
    *   **Welcome & Quick Stats:** A personalized greeting and key metrics (e.g., "You have 15 days of leave remaining").
    *   **Pending Actions (for Managers):** A prominent list of items requiring approval, such as leave requests and expense claims.
    *   **Upcoming Leave:** A calendar or list view of the user's upcoming approved time off and company holidays.
    *   **Recent Expense Status:** A summary of the user's most recently submitted expenses and their current status.
    *   **Onboarding Progress (for New Hires):** A checklist showing the new hire's progress through their onboarding plan.
*   **Related Features:** `holiday-leave-management`, `expense-tracking-approval`, `onboarding-workflow-automation`, `performance-review-360`.

### 4. Leave Hub (`/leave`)
*   **Description:** The dedicated center for all leave-related activities.
*   **Sections:**
    *   **Leave Balance Summary:** A clear visual breakdown of leave allowance, taken leave, and remaining balance.
    *   **Request New Leave Form:** An intuitive form to select dates, leave type, and add notes.
    *   **My Leave Requests:** A table or list showing the history of all submitted requests with their status (Pending, Approved, Denied).
    *   **Team Calendar View (Manager/Admin):** A calendar showing the approved leave for the manager's team members to help with planning.
*   **Related Features:** `holiday-leave-management`.

### 5. Expenses Manager (`/expenses`)
*   **Description:** The central hub for managing expense claims.
*   **Sections:**
    *   **Submit New Expense Form:** A simple form with fields for amount, category, date, and a prominent receipt upload component.
    *   **My Submitted Expenses:** A historical log of all expenses submitted by the user, showing their status.
    *   **Pending Expense Approvals (for Managers):** A queue of expense claims from their team awaiting review.
*   **Related Features:** `expense-tracking-approval`.

### 6. Onboarding Center (`/onboarding`)
*   **Description:** A portal for managing and participating in the new hire onboarding process.
*   **Sections:**
    *   **My Onboarding Checklist (for New Hires):** A step-by-step list of tasks the new hire needs to complete.
    *   **Company Resources:** A section with links to important documents, handbooks, and guides.
    *   **New Hire Progress Tracker (for HR/Admin):** A dashboard to monitor the progress of all current new hires.
*   **Related Features:** `onboarding-workflow-automation`.

### 7. Performance Reviews (`/performance`)
*   **Description:** The interface for all performance review activities, from setup to feedback submission.
*   **Sections:**
    *   **My Review Cycles:** A view for employees to access their self-assessment and requests for peer feedback.
    *   **Team Member Reviews (for Managers):** A dashboard for managers to track the review cycles of their direct reports and view consolidated reports.
    *   **Review Cycle Setup (for HR/Admin):** A wizard-like interface to create and launch new review cycles.
*   **Related Features:** `performance-review-360`.

### 8. Company Admin Settings (`/admin/settings`)
*   **Description:** A secure, admin-only area for configuring the entire easyteams account for the company.
*   **Sections:**
    *   **User & Role Management:** Invite new users and assign roles (employee, manager, admin).
    *   **Leave Policies:** Define annual allowance, carry-over rules, and custom leave types.
    *   **Expense Categories & Approval Flows:** Customize expense categories and set approval limits.
    *   **Onboarding Templates Management:** Create and edit reusable onboarding checklists.
*   **Related Features:** `company-settings-policies`, `user-authentication`.