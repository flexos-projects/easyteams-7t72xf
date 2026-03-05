---
id: page-dashboard
title: Dashboard Page Specification
description: Specification for the main user dashboard, providing a personalized overview of pending actions, upcoming events, and key metrics.
type: spec
subtype: page
status: draft
sequence: 200
tags:
  - UI
  - UX
  - Overview
  - Home
relatesTo:
  - feature-holiday-leave-management
  - feature-expense-tracking-approval
  - feature-onboarding-workflow-automation
  - feature-performance-review-360
createdAt: 2024-07-30T12:00:00Z
updatedAt: 2024-07-30T12:00:00Z
---

# Dashboard Page

This specification outlines the **Dashboard** page, serving as the primary entry point and personalized overview for every user within the easyteams application. It is designed to provide immediate access to critical information, pending actions, and relevant updates, ensuring users can quickly grasp their current status and navigate to key functionalities.

## Purpose

The Dashboard's main purpose is to offer a concise, contextual summary tailored to the user's role (employee, manager, admin, new hire). It acts as a central hub, reducing the need to visit multiple pages for routine checks and approvals, thereby improving user efficiency and overall experience.

## Key Sections & Content

1.  **Welcome Message & Quick Stats**: A personalized greeting along with high-level statistics relevant to the user, such as total leave days remaining, number of pending expenses, or upcoming review deadlines.
2.  **Pending Actions/Approvals**: For managers and HR, this section highlights outstanding tasks like leave requests awaiting approval, expense reports to review, or onboarding tasks assigned to them. For employees, it might show pending self-assessments or unread notifications.
3.  **Upcoming Leave/Holidays**: Displays a quick glance at the user's own upcoming approved leave and, for managers, a summary of their team's upcoming time off, preventing scheduling conflicts.
4.  **Latest Expense Status**: Provides an overview of recently submitted expenses, their current status (pending, approved, rejected), and quick links to the full expense manager.
5.  **Onboarding Task Progress**: Specifically for new hires, this section tracks their progress through assigned onboarding tasks, including completion status and upcoming deadlines. For HR, it might show an overview of new hires' onboarding journeys.
6.  **Performance Review Status/Upcoming Deadlines**: Informs users about active performance review cycles, their participation status (e.g., self-assessment due), and deadlines for feedback submission. Managers will see an overview of reviews they need to conduct.

## User Experience

The Dashboard prioritizes clarity and actionability, using intuitive cards and widgets to present information. It will be responsive, adapting to various screen sizes, and offer quick navigation links to the detailed pages for each section. The design will adhere to the 'Modern, Clean, Friendly' aesthetic of easyteams, utilizing the defined color palette and Inter font family.