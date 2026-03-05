---
id: database-004
title: "Database Schema"
description: "Defines the data models and collections for the easyteams application using Firestore."
type: doc
subtype: core
status: draft
sequence: 4
tags:
  - database
  - firestore
  - backend
createdAt: "2023-10-27T10:03:00Z"
updatedAt: "2023-10-27T10:03:00Z"
---

# Database Schema

This document outlines the database schema for easyteams. We will be using Google Firestore, a NoSQL, document-based database. This choice aligns with our technical stack (see [Technical Document](./007-technical.md)), offering seamless integration with Firebase Authentication, real-time data synchronization, and excellent scalability for our target SMB audience.

## Data Modeling Philosophy

Our schema is designed to be denormalized where appropriate to optimize for common read operations, reducing the need for complex queries. For example, we may store a user's `displayName` on a `leave_request` to avoid fetching the user document every time we display the request.

--- 

## Collection: `users`

Stores all user account information.

*   **Description:** This collection is the central repository for user data. The document ID will be the UID provided by Firebase Authentication.
*   **Fields:**
    *   `id` (string, required): Unique user ID from Firebase Auth.
    *   `email` (email, required): User's login email.
    *   `displayName` (string): User's full name.
    *   `avatarUrl` (url): URL to the user's profile picture.
    *   `companyId` (reference, required): A reference to the `companies` document the user belongs to.
    *   `role` (enum, required): User's role (`employee`, `manager`, `admin`).
    *   `managerId` (reference): A reference to another `users` document for their direct manager.
    *   `createdAt` (timestamp, required): Timestamp of account creation.
*   **Relationships:** Belongs to one `company`. Can have one `manager` (another user).

## Collection: `companies`

Stores settings and configurations for each client company.

*   **Description:** Each document represents a single company using easyteams. This is the root for most company-specific data.
*   **Fields:**
    *   `id` (string, required): Unique company ID.
    *   `name` (string, required): The legal name of the company.
    *   `logoUrl` (url): URL for the company's logo for branding.
    *   `subscriptionStatus` (enum, required): e.g., `active`, `trial`, `past_due`.
    *   `leavePolicies` (object): Contains leave rules, e.g., `{ annualAllowance: 25, carryOverDays: 5, yearStartMonth: 1 }`.
    *   `expenseCategories` (array of strings): A list of valid expense categories, e.g., `["Travel", "Software", "Meals"]`.
*   **Relationships:** Has many `users`, `leave_requests`, `expenses`, etc.

## Collection: `leave_requests`

Records all employee time-off requests.

*   **Description:** Each document is a single request for leave made by an employee.
*   **Fields:**
    *   `id` (string, required): Unique ID for the request.
    *   `userId` (reference, required): Reference to the `users` document of the requester.
    *   `companyId` (reference, required): Reference to the company.
    *   `startDate` (date, required): The first day of leave.
    *   `endDate` (date, required): The last day of leave.
    *   `type` (enum, required): Type of leave (`Holiday`, `Sick`, `Unpaid`).
    *   `status` (enum, required): Current status (`Pending`, `Approved`, `Denied`).
    *   `reason` (string): Optional note from the employee.
    *   `approverId` (reference): Reference to the `users` document of the manager who actioned the request.
    *   `createdAt` (timestamp, required): Timestamp of submission.
*   **Relationships:** Belongs to one `user` and one `company`.

## Collection: `expenses`

Stores all employee expense claims.

*   **Description:** Each document represents a single expense claim submitted for reimbursement.
*   **Fields:**
    *   `id` (string, required): Unique ID for the expense.
    *   `userId` (reference, required): Reference to the submitting user.
    *   `companyId` (reference, required): Reference to the company.
    *   `amount` (number, required): The monetary value of the expense (in cents).
    *   `currency` (string, required): 3-letter currency code (e.g., `GBP`).
    *   `category` (string, required): The expense category.
    *   `receiptUrl` (image, required): URL to the uploaded receipt file in Cloudinary.
    *   `dateIncurred` (date, required): The date the expense occurred.
    *   `status` (enum, required): Current status (`Pending`, `Approved`, `Rejected`, `Reimbursed`).
    *   `approverId` (reference): Reference to the approving manager.
    *   `createdAt` (timestamp, required): Timestamp of submission.
*   **Relationships:** Belongs to one `user` and one `company`.

## Collection: `onboarding_tasks`

Tracks individual tasks within an onboarding workflow.

*   **Description:** A list of all tasks assigned during the onboarding process for new hires.
*   **Fields:**
    *   `id` (string, required): Unique task ID.
    *   `companyId` (reference, required): Reference to the company.
    *   `newHireId` (reference, required): Reference to the new user being onboarded.
    *   `title` (string, required): The name of the task.
    *   `description` (string): More detailed instructions for the task.
    *   `assignedTo` (reference, required): User responsible for the task (can be the new hire or someone else).
    *   `dueDate` (date): Optional due date.
    *   `status` (enum, required): `Pending`, `Completed`.
*   **Relationships:** Belongs to one `newHireId` (a user) and one `company`.

## Collection: `performance_reviews`

Manages performance review cycles and associated feedback.

*   **Description:** Each document represents a single performance review cycle for an employee.
*   **Fields:**
    *   `id` (string, required): Unique ID for the review cycle.
    *   `companyId` (reference, required): Reference to the company.
    *   `reviewedUserId` (reference, required): The employee being reviewed.
    *   `cycleName` (string, required): Name of the cycle (e.g., 'Q4 2024 Review').
    *   `status` (enum, required): `Open`, `Collecting Feedback`, `Closed`.
    *   `endDate` (date, required): The deadline for submitting feedback.
    *   `feedbackSubmissions` (array of objects): Stores feedback, e.g., `[{ reviewerId: '...', role: 'peer', content: '...' }]`.
*   **Relationships:** Belongs to one `reviewedUserId` (a user) and one `company`.