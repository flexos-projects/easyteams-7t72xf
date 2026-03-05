---
id: "invite-team-member"
title: "Invite Team Member Flow"
type: "flow"
status: "draft"
description: "User flow for a project owner to invite a new team member to an EasyTeams project."
tags: ["team", "invite", "onboarding", "user-management", "flow"]
createdAt: "2026-03-05"
updatedAt: "2026-03-05"
---

---
id: invite-team-member
title: Invite Team Member Flow
type: flow
status: active
slug: invite-team-member
description: User flow for a project owner to invite a new team member to an EasyTeams project.
tags:
  - team
  - invite
  - onboarding
  - user-management
  - flow
relatesTo: []
---

# Invite Team Member Flow

## Overview
This flow describes the process by which an EasyTeams project owner invites a new member to their project, from the initial invitation to the new member successfully joining the team. It covers both new users and existing EasyTeams users.

## User Stories
*   As a Project Owner, I want to easily invite team members to my project so we can collaborate effectively.
*   As a potential Team Member, I want to seamlessly accept an invitation and join an EasyTeams project, whether I have an account or need to create one.

## Acceptance Criteria
*   The Project Owner can specify the recipient's email address and assign a specific role (e.g., Viewer, Editor, Admin) during the invitation process.
*   The system generates a unique, secure, and time-sensitive invitation link for each invite.
*   The recipient receives an email containing the invitation link and relevant project details.
*   Upon clicking the link, a new user can register for an EasyTeams account and join the project.
*   Upon clicking the link, an existing EasyTeams user can log in to their account and join the project.
*   Once joined, the new member appears in the project roster with the role assigned by the owner.
*   The Project Owner receives confirmation when an invite has been sent and when a recipient accepts the invite.

## Trigger
An authenticated Project Owner navigates to the "Members" or "Team Settings" section within their project dashboard and clicks an "Invite Member" or similar call-to-action button.

## Steps
<flex_block type="flow">
    ### Step 1: Owner Initiates Invite
    *   **Actor:** User (Project Owner)
    *   **Action:** The owner clicks "Invite Member", enters the recipient's email address into the input field, selects a desired role for the new member (e.g., Viewer, Editor, Admin) from a dropdown menu, and clicks the "Send Invite" button.
    *   **Outcome:** The system validates the email format. A unique invite token is generated and associated with the project, owner, recipient email, and selected role. The invite status is recorded as "Pending". The owner sees a confirmation message, e.g., "Invitation sent to [recipient's email address]".

    ### Step 2: System Sends Invitation Email
    *   **Actor:** System
    *   **Action:** The system composes an email containing a personalized message, the project name, the inviting owner's name, and the unique invitation link. This email is then sent to the specified recipient's email address.
    *   **Outcome:** The recipient receives the invitation email. The system logs the email send attempt and its success/failure. The invite remains in "Pending" status.

    ### Step 3: Recipient Accepts Invitation
    *   **Actor:** User (Recipient)
    *   **Action:** The recipient opens the invitation email and clicks on the unique invitation link provided.
    *   **Outcome:** The recipient's web browser navigates to the EasyTeams platform. The system intercepts the request, validates the invitation token (checking for authenticity, expiration, and prior acceptance).

    ### Step 4: Recipient Account Creation/Login
    *   **Actor:** User (Recipient)
    *   **Action:**
        *   **If Recipient is a New User:** The recipient is presented with a registration form (e.g., Name, Password, Confirm Password). They fill in their details and submit the form.
        *   **If Recipient is an Existing User:** The recipient is prompted to log in using their existing EasyTeams credentials. They enter their email and password and submit.
    *   **Outcome:** The recipient is successfully authenticated. If a new user, a new EasyTeams account is created and linked to their email address. The system associates the authenticated user with the pending invitation.

    ### Step 5: System Adds Member to Project
    *   **Actor:** System
    *   **Action:** The system updates the invite status from "Pending" to "Accepted". The authenticated user is officially added to the project, and the pre-selected role is assigned to them. The system redirects the user to the project dashboard or a welcome page.
    *   **Outcome:** The recipient is now an active member of the EasyTeams project with the assigned role. The project owner's project roster is updated to display the new member. The recipient can now access project resources according to their role.
</flex_block>

## Error Paths
*   **Invalid Email Format:** If the owner enters an email address that doesn't conform to standard email syntax, the system should prevent submission and display an inline error message.
*   **Invite to Self:** The owner attempts to invite the same email address as their own account. The system should notify the owner that they are already a member.
*   **Already a Member:** The owner tries to invite an email address that is already an active member of the specific project. The system should inform the owner that the user is already a member.
*   **Invite Link Expired:** The recipient clicks an invitation link that has passed its expiration time. The system should display an error page indicating the link is expired and offer options to request a new invite (if applicable).
*   **Invite Link Invalid/Tampered:** The recipient clicks a malformed or non-existent invitation link. The system should display a generic error page (e.g., 404 Not Found or Invalid Link).
*   **Email Send Failure:** If the system encounters an error sending the invitation email (e.g., temporary mail server outage, recipient email bounce), the owner should be notified, and the invite status should reflect the failure (e.g., "Send Failed"). The owner should have an option to re-send.
*   **Registration/Login Failure:** The recipient fails to create an account (e.g., invalid password criteria) or log in (e.g., incorrect credentials). Standard error messages for account operations should be displayed, allowing the user to correct the issue and retry.

## Edge Cases
*   **Invite Revocation:** The Project Owner revokes a pending invitation before the recipient accepts it. The invitation link should be immediately invalidated. If the recipient clicks the link after revocation, they should see an error indicating the invite was revoked.
*   **Role Change Before Acceptance:** The Project Owner changes the role associated with a pending invite before the recipient accepts. The new role should be applied when the recipient accepts the invite.
*   **Project Deletion Before Acceptance:** If the project associated with a pending invite is deleted before the recipient accepts, the invitation link should become invalid, and the recipient should see an appropriate error message.
*   **Multiple Invites for Same User/Project:** If a user receives multiple invitations for the same project (either from the same or different owners, or at different times), the system should ensure that only one successful acceptance process occurs, and subsequent attempts with other links for the same project should gracefully redirect to the already-joined project or notify them they are already a member.
*   **User Exists, Not in Project:** The invited email address belongs to an existing EasyTeams user who is not currently a member of the inviting project. The flow should seamlessly guide this user to log in and then join the project without requiring new account creation.