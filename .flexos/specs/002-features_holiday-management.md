---
type: spec
subtype: features
title: Holiday Management System
description: Comprehensive system for employees to request and managers to approve holidays, adhering to French labor laws.
sequence: 2
status: active
tags: [holiday, leave, compliance, france-specific, hr]
relatesTo:
  - /.flexos/specs/001-vision_easyteams.md
createdAt: 2023-10-27T10:05:00Z
updatedAt: 2023-10-27T10:05:00Z
---

# Holiday Management System

## Overview
This feature provides a robust system for managing employee holidays, including request submission, approval workflows, and automated leave balance tracking, with specific emphasis on compliance with French labor regulations (Code du Travail).

## Core Functionality
1.  **Employee Holiday Requests:** Employees can submit requests for various types of leave (e.g., paid leave, RTT, unpaid leave) for specific dates or periods.
2.  **Leave Balance Tracking:** Automated calculation and display of available leave days for each employee, considering different leave types.
3.  **Manager Approval Workflow:** Managers can view, approve, deny, or request modifications to submitted holiday requests.
4.  **Public Holiday Integration:** Automatic recognition and marking of French national and regional public holidays.
5.  **Reporting & Audit Trail:** Generation of reports on leave usage and a complete audit trail of all holiday requests and approvals for compliance purposes.

## French-Specific Logic & Rules
This section details the critical French labor law rules that the system must enforce. These rules are non-negotiable for compliance.

### 1. **Acquisition of Paid Leave (Congés Payés)**
*   **Rule:** Employees typically accrue 2.5 working days of paid leave per month of actual work, up to a maximum of 30 working days per year (equivalent to 5 weeks).
*   **Logic:** The system must calculate and display accrual rates based on employment start date and monthly activity. For part-time employees, accrual is proportional.
*   **Context:** The reference period for leave acquisition is generally from June 1st of the previous year to May 31st of the current year.

### 2. **Main Leave Period (Période Principale de Prise des Congés)**
*   **Rule:** Employees are generally required to take their main block of at least 12 continuous working days of paid leave between May 1st and October 31st each year.
*   **Logic:** The system should flag or warn if an employee attempts to book less than 12 continuous days as their *first* main leave block, or if the main leave period falls outside the permitted dates.

### 3. **Fractionnement (Splitting of Leave)**
*   **Rule:** If an employee splits their main block of leave (i.e., takes less than 12 continuous working days outside the main period, or takes more than 24 working days in total), additional leave days (jours de fractionnement) might be due.
    *   2 days if remaining leave > 8 working days.
    *   1 day if remaining leave between 3 and 5 working days.
*   **Logic:** The system must automatically calculate and add `jours de fractionnement` based on the timing and duration of leave taken, and update the employee's leave balance accordingly.

### 4. **Pre-notification for Employers (Délai de Prévenance)**
*   **Rule:** The employer must inform employees of their main leave dates at least one month in advance.
*   **Logic:** While not directly enforcing employee requests, the system can provide tools for managers to proactively schedule and notify, and flag short-notice changes.

### 5. **Maximum Continuous Leave:**
*   **Rule:** Paid leave cannot exceed 24 continuous working days, except in specific justified cases (e.g., employees with geographical constraints or family obligations).
*   **Logic:** The system should prevent booking more than 24 continuous working days unless explicitly overridden by a manager with a recorded justification.

### 6. **Other Leave Types (e.g., RTT, Congés Sans Solde)**
*   **Rule:** Integration and tracking of RTT (Réduction du Temps de Travail) days and unpaid leave (congés sans solde) should be supported, with their own specific balances and rules.
*   **Logic:** Separate tracking mechanisms for RTT and unpaid leave, not impacting paid leave balances.

## User Roles & Permissions
*   **Employee:** Can view their own leave balances, submit new requests, view the status of their requests, and cancel pending requests.
*   **Manager:** All employee permissions, plus: view all team members' leave balances and requests, approve/deny requests, modify approved requests (with audit trail), access compliance reports.
*   **Admin:** All manager permissions, plus: configure global holiday rules, adjust individual employee leave balances (with justification), manage public holidays.

## Integrations (Future Scope)
-   Integration with payroll systems for automated leave deductions.
-   Calendar integration (Outlook, Google Calendar) for team availability.
