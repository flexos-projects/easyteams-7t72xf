---
id: flows-005
title: "User Flows"
description: "Documents the key user journeys and interaction sequences within the easyteams application."
type: doc
subtype: core
status: draft
sequence: 5
tags:
  - flows
  - ux
  - product
createdAt: "2023-10-27T10:04:00Z"
updatedAt: "2023-10-27T10:04:00Z"
---

# User Flows

This document details the step-by-step user flows for critical processes within the easyteams platform. Understanding these flows is essential for building an intuitive and logical user experience. They illustrate how users interact with the features detailed in the [Features Document](./002-features.md) and the pages from the [Pages Document](./003-pages.md).

## 1. User Signup & Initial Onboarding

*   **Trigger:** A new user clicks 'Sign Up' on the **Landing Page** or receives an email invitation.
*   **Description:** This flow guides a new user from creating their account to completing their initial company-specific onboarding tasks, ensuring they are set up for success from day one.
*   **Steps:**
    1.  **Initiate Signup (Actor: User):** The user accesses the **Login / Sign Up** page. They enter their name, work email, a secure password, and their company name. If invited, the company name is pre-filled.
    2.  **Account Creation & Verification (Actor: System):** The system creates a new document in the `users` collection and an associated company in the `companies` collection if it's the first user. A verification email is sent via SendGrid.
    3.  **Email Verification (Actor: User):** The user clicks the link in the verification email, which activates their account and redirects them to the login page.
    4.  **First Login & Profile Setup (Actor: User):** Upon their first successful login, the user is prompted to complete their profile on the **User Settings & Profile** page (e.g., add a job title, upload an avatar).
    5.  **Onboarding Kickoff (Actor: System):** The system checks if an onboarding template is active for the company. If so, it generates the necessary `onboarding_tasks` and displays a prominent link to the **Onboarding Center** on the user's **Dashboard**.
    6.  **Complete Initial Tasks (Actor: User):** The user navigates to the **Onboarding Center** and begins working through their assigned checklist, such as 'Read Company Handbook' or 'Submit Emergency Contact Info'.

## 2. Submit & Approve Holiday Request

*   **Trigger:** An employee needs to request time off for a vacation.
*   **Description:** This flow covers the end-to-end process of an employee requesting leave and their manager approving it, including all system notifications and data updates.
*   **Steps:**
    1.  **Navigate and Request (Actor: Employee):** The user logs in and navigates to the **Leave Hub**. They view their remaining balance and click 'Request Leave'.
    2.  **Fill Form (Actor: Employee):** The user selects the start and end dates using a calendar, chooses the leave type (e.g., 'Holiday'), and adds an optional note for their manager.
    3.  **Submit Request (Actor: Employee):** Upon submission, the system creates a new document in the `leave_requests` collection with a status of `Pending`.
    4.  **Notify Manager (Actor: System):** The system identifies the user's manager (via the `managerId` field in the `users` collection) and sends them an email and an in-app notification about the new request.
    5.  **Review Request (Actor: Manager):** The manager clicks the notification or logs in to their **Dashboard**, where they see the pending request. They click to view details, including the employee's note and the team calendar to check for overlaps.
    6.  **Approve/Deny (Actor: Manager):** The manager clicks 'Approve' or 'Deny'. They can add a comment explaining their decision.
    7.  **Update & Notify Employee (Actor: System):** The system updates the `leave_requests` document's status to `Approved` or `Denied` and records the `approverId`. If approved, the leave duration is deducted from the employee's balance. The system then sends a confirmation email to the employee.
    8.  **Update Calendar (Actor: System):** If approved, the leave is visually added to the shared team calendar in the **Leave Hub**.

## 3. Submit & Approve an Expense

*   **Trigger:** An employee pays for a business-related item (e.g., a software subscription) and needs reimbursement.
*   **Description:** This flow details how an employee can easily submit a digital expense claim and how a manager reviews and processes it for payment.
*   **Steps:**
    1.  **Create New Expense (Actor: Employee):** The user navigates to the **Expenses Manager** page and clicks 'Submit New Expense'.
    2.  **Upload Receipt & Details (Actor: Employee):** The user uploads a photo of the receipt, which is sent to Cloudinary. They fill in the amount, select a category (e.g., 'Software'), set the date it was incurred, and add a description.
    3.  **Submit for Approval (Actor: Employee):** The user submits the form. A new document is created in the `expenses` collection with a status of `Pending`.
    4.  **Manager Notification (Actor: System):** The user's manager receives an email and in-app notification.
    5.  **Review & Action (Actor: Manager):** The manager goes to their approval queue in the **Expenses Manager**. They review the expense details and click to view the attached receipt. They then choose to 'Approve' or 'Reject'.
    6.  **Employee Notification (Actor: System):** The employee is notified of the outcome via email. The `expenses` document status is updated.
    7.  **Mark for Reimbursement (Actor: System):** If approved, the expense status is updated to `Approved`. It now appears in a filterable list for admins/accountants to export for payment processing.

## 4. Initiate a 360 Performance Review

*   **Trigger:** An HR admin or manager decides to start a performance review cycle for an employee.
*   **Description:** This flow outlines how a structured 360-degree feedback process is configured, launched, and managed within the platform.
*   **Steps:**
    1.  **Start New Cycle (Actor: HR Admin/Manager):** The user navigates to the **Performance Reviews** page and clicks 'Start New Review Cycle'.
    2.  **Configure Review (Actor: HR Admin/Manager):** They select the employee to be reviewed, give the cycle a name (e.g., 'Q3 2024 Performance Review'), and set the deadline for feedback submission.
    3.  **Invite Participants (Actor: HR Admin/Manager):** They invite the employee to complete a self-assessment. They then select a list of peers and other managers to provide feedback on the employee.
    4.  **Participant Notifications (Actor: System):** The system creates a `performance_reviews` document and sends email notifications to all invited participants with a direct link to the feedback form.
    5.  **Submit Feedback (Actor: Participants):** Each participant follows the link, fills out the review form, and submits their feedback before the deadline. The submissions are stored in the `feedbackSubmissions` array.
    6.  **Monitor Progress (Actor: System & HR Admin/Manager):** The initiator can track who has and has not submitted feedback. The system sends automated reminders as the deadline approaches.
    7.  **Close Cycle & Generate Report (Actor: System):** Once the deadline passes, the system closes the cycle. It then compiles all submitted feedback into a single, consolidated report accessible only to the employee's manager and HR.