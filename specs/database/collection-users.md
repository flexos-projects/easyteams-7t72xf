---
id: collection-users
title: Users Data Collection Specification
description: Specification for the 'users' Firestore collection, detailing its structure, fields, and relationships.
type: spec
subtype: database
status: draft
sequence: 400
tags:
  - Database
  - Firestore
  - User Management
  - Authentication
relatesTo:
  - feature-user-authentication
  - collection-companies
  - collection-leave-requests
  - collection-expenses
  - collection-onboarding-tasks
  - collection-performance-reviews
createdAt: 2024-07-30T12:00:00Z
updatedAt: 2024-07-30T12:00:00Z
---

# Users Data Collection (Firestore)

This specification details the `users` collection within the Firestore database for the easyteams platform. This collection is fundamental, storing all user accounts, their authentication details, roles, and personal information crucial for system operation and access control.

## Purpose

The `users` collection serves as the central repository for all individuals interacting with easyteams. It underpins authentication, authorization, personalization, and facilitates relationships across various other data collections, ensuring that every action is attributed to a specific user and their permissions.

## Fields

*   **`id`** (string, required): Unique user ID, typically derived from Firebase Authentication UID. This serves as the primary key for the user document.
*   **`email`** (email, required): The user's primary email address, used for login and notifications. Must be unique across the platform.
*   **`displayName`** (string, optional): The user's full name, displayed throughout the application (e.g., in team calendars, expense reports).
*   **`avatarUrl`** (url, optional): A URL pointing to the user's profile picture, allowing for personalization.
*   **`companyId`** (reference, required): A reference to the `companies` collection, indicating which organization the user belongs to. This is crucial for multi-tenancy.
*   **`role`** (enum: 'employee', 'manager', 'admin', 'HR', required): Defines the user's permissions and access level within their `companyId`. This dictates what features and data they can view or modify.
*   **`managerId`** (reference, optional): A self-referencing field to another user's `id` within the `users` collection, indicating the user's direct manager. Essential for approval workflows (e.g., leave, expenses).
*   **`employeeId`** (string, optional): An optional, company-specific employee identifier, if used by the organization.
*   **`createdAt`** (timestamp, required): The timestamp when the user account was created.
*   **`updatedAt`** (timestamp, required): The timestamp of the last update to the user's profile information.

## Relationships

*   **`companies`**: Each user `references` one company via `companyId`. A company `has many` users.
*   **`users` (self-referencing)**: Users can `reference` another user as their `managerId` for hierarchical structures.
*   **`leave_requests`**: Users `submit` and `approve` `leave_requests`.
*   **`expenses`**: Users `submit` and `approve` `expenses`.
*   **`onboarding_tasks`**: Users are `newHireId` or `assignedTo` for `onboarding_tasks`.
*   **`performance_reviews`**: Users can be `reviewedUserId`, `initiatorId`, or provide `feedbackSubmissions` in `performance_reviews`.

## Security & Indexing

*   Access to user data will be strictly controlled by Firestore Security Rules based on `companyId` and `role`.
*   Indexes will be created for `email`, `companyId`, `role`, and `managerId` to optimize query performance for common operations like fetching users by company or manager.