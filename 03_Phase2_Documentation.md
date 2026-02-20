## Phase 2: Org Setup & Configuration
## 1. Salesforce Editions

For the Leave Tracker Project, the chosen edition is Salesforce Enterprise Edition, as it provides:
- Support for complex business processes like approval workflows and automation.
- Ability to create custom objects (Leave Request, Leave Balance).
- Role hierarchy and advanced sharing settings.

## Company Profile Setup

- Organization Name: Leave Tracker (example for your project).
- Default Time Zone: IST (India Standard Time) to match employee location.
- Default Currency: INR (₹) for leave-related reporting (if linked with payroll).
- Language Settings: English (default), with multilingual support possible if required.


## User Setup & Licenses

### 1. Users Created:

- Employees (end users submitting leave requests).
- Managers (approvers).
- HR/Admin (monitoring, reporting).




### 2. Licenses Assigned:

- Salesforce Platform License → For Employees.
- Salesforce License → For Managers & Admins (to enable reporting and advanced features).
## Profiles, Roles, Permission Sets

### 1. Profiles:

- Employee Profile → Access to submit leave requests only.
- Manager Profile → Approve/reject requests, view team records.
- HR/Admin Profile → Full access, reporting, system configurations.

### 2. Roles:

- Employee Role → Reports to Manager Role.
- Manager Role → Reports to HR Role.
- HR Role → Top-level role with organization-wide visibility.

### 3. Permission Sets:

- Notification Access (Email/SMS integration).
- Report & Dashboard Access.

<img width="1894" height="909" alt="image" src="https://github.com/user-attachments/assets/1c5650ba-fb21-4263-9f79-564a838606eb" />

### 4. Users:

- Used to test the profiles, Roles, permission sets.
- The user is used to edit the leave request to accepted , Rejected.

  <img width="1887" height="898" alt="image" src="https://github.com/user-attachments/assets/bf930aa8-2296-44c2-9ac7-d892ef56a307" />



## OWD & Sharing Rules

###  1. Object-Level Security (OWD):
- Leave Requests → Private (employees see only their own requests).
- Leave Balance → Private.
- Reports/Dashboards → Controlled by HR.

### 2. Sharing Rules:

- Manager can see leave requests of their direct reports.
- HR/Admin has access to all employee records.

## Deployment Basics

- Change Sets: Used to deploy metadata (custom objects, fields, flows, reports) from Sandbox to Production.
- Version Control (GitHub): Repository maintained for tracking changes.
- Deployment Checklist:
- Validate test classes (minimum 75% coverage).
- Backup existing metadata.
- Deploy in non-peak hours.

## ✅ Phase 2 Outcome:

- Org environment is fully set up with business hours, users, roles, and permissions.
- Security policies, login access, and data visibility configured.
- Deployment process established for smooth release cycles.
