---
id: flow-submit-approve-holiday
title: Submit & Approve Holiday Request User Flow
description: Detailed user flow for an employee requesting a holiday and a manager subsequently approving or denying it.
type: spec
subtype: flow
status: draft
sequence: 300
tags:
  - Workflow
  - HR
  - Leave
  - Approval
relatesTo:
  - feature-holiday-leave
  - page-leave-hub
  - collection-leave-requests
createdAt: 2024-07-30T12:00:00Z
updatedAt: 2024-07-30T12:00:00Z
---

# Submit & Approve Holiday Request User Flow

This specification details the end-to-end user flow for an employee submitting a holiday request and their manager processing that request within the easyteams platform. This flow is critical for efficient team management and a positive employee experience, directly leveraging the 'Holiday & Leave Management' feature.

## Trigger

An employee decides to request time off and initiates the process from their easyteams dashboard or the dedicated 'Leave Hub' page.

## Steps

1.  **Request Holiday (Actor: Employee)**:
    *   The employee navigates to the 'Leave Hub' (`/leave` route).
    *   They select the desired start and end dates for their leave using a calendar interface.
    *   The system displays their current remaining holiday allowance and highlights any potential conflicts with team members' approved leave.
    *   The employee selects the type of leave (e.g., Holiday, Sick, Unpaid) and adds an optional reason or note.
    *   After reviewing the details, the employee clicks 'Submit Request'.

2.  **Notification to Manager (Actor: System)**:
    *   Upon submission, the system creates a new `leave_request` record in the database with a 'Pending' status.
    *   An email notification is automatically sent to the employee's assigned manager (`managerId` from `users` collection), informing them of the new request.
    *   An in-app notification appears on the manager's Dashboard and 'Leave Hub' indicating a pending action.

3.  **Review Request (Actor: Manager)**:
    *   The manager logs into easyteams and navigates to their Dashboard or the 'Leave Hub'.
    *   They see the pending leave request listed, along with key details: employee name, dates, type, and any notes.
    *   The manager can click on the request to view more context, including the employee's leave balance, and a visual representation of their team's calendar during the requested period.

4.  **Approve/Deny Request (Actor: Manager)**:
    *   Based on the review, the manager chooses to 'Approve' or 'Deny' the request.
    *   If denying, the manager is prompted to provide a mandatory reason or comment.
    *   The manager confirms their decision.

5.  **Update & Notify Employee (Actor: System)**:
    *   The system updates the `leave_request` status to 'Approved' or 'Denied' in the database, recording the `approverId` and `approvedAt` timestamp.
    *   If approved, the employee's leave allowance is automatically deducted.
    *   An email notification is sent to the employee, informing them of the manager's decision and any comments.
    *   An in-app notification confirms the status update.

6.  **Calendar Update (Actor: System)**:
    *   If the request is approved, the employee's leave dates are automatically added to the shared team calendar view within the 'Leave Hub' and Dashboard, ensuring real-time visibility for all relevant parties.

This flow ensures a transparent, efficient, and well-documented process for managing employee time off, significantly improving HR operations.