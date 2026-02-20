# Phase 4: Process Automation (Admin)
## 1. Validation Rules

- Ensures data quality and prevents invalid submissions.
- End Date must be greater than Start Date
-     End_Date__c < Start_Date__c
- → Displays error message: "End Date must be later than Start Date."

Reason Required for Submitted Requests
Ensures employees provide a reason before submitting.

## 2. Workflow Rules

- Auto-update Status: When a leave request is submitted, set status to “Pending Approval.”

  <img width="1897" height="917" alt="image" src="https://github.com/user-attachments/assets/d6bf4d1a-a741-4d01-92c4-a9d61140d0c4" />

Actions:

  - Send email notification to the Manager.
  - Update Status field to "Submitted".
    
Deletion:

  - Top pop warning will be avaliable to delete the request to Employee.

  - 
    <img width="1876" height="895" alt="image" src="https://github.com/user-attachments/assets/39809e74-3a6b-45f8-b095-cf51f4713296" />

## 3. Process Builder 

### On Leave Request Submission:

- Process Builder is used for conditional automation that cannot be handled by simple workflow rules.
Example:
- If Status = Approved → Trigger email to employee confirming approval.
- If Status = Rejected → Trigger email with rejection reason.

## 4. Flow Builder

### Screen Flows (for employees):

Guided process to apply for leave.
- Step 1: Select Leave Type.
- Step 2: Pick Dates.
- Step 3: Provide Reason.
- Step 4: Review & Submit.

  <img width="1893" height="892" alt="image" src="https://github.com/user-attachments/assets/6dde9cf4-70ee-49db-bcc3-b51c3f1f2275" />

## 5. Approval Process

- Step 1: Employee submits request → Status = Pending.
- Step 2: Manager receives approval request.
- Step 3: Manager approves or rejects.
- Step 4: If approved → Send email to employee.
- Step 5: If rejected → Send email to employee.

    <img width="1897" height="908" alt="image" src="https://github.com/user-attachments/assets/f4aff111-c9de-4f6c-9b74-b81e1c03ae22" />

## 6. Email Flows & Alerts
### A. Email Flow
- 1. Click Setup ()→ Quick Find→ Flows New Flow.

- 2. Select Record-Triggered Flow.

- 3. Choose Object: Leave_Request_Status_Notification → Trigger: When record is created→ After Save.

- 4. Add Action Send Email Select Welcome Email Template.

- 5. Save and Activate.
     
<img width="1895" height="905" alt="image" src="https://github.com/user-attachments/assets/61015d39-e949-456c-ac54-af79de9dd6b9" />
 
### B. Email Alerts

- Leave Request Submitted: Sent to Manager.
- Leave Request Approved: Sent to Employee.

  <img width="1908" height="907" alt="image" src="https://github.com/user-attachments/assets/cd58125b-028d-47bd-9af0-7aea2e56db8d" />

- Leave Request Rejected: Sent to Employee.

   <img width="1906" height="888" alt="image" src="https://github.com/user-attachments/assets/cf66f180-2a75-44ec-92dc-03ced73061bd" />

- Leave Balance Reminder: Monthly email to Employee.

## 7. Field Updates

- On Approval: Status → Approved.
- On Rejection: Status → Rejected.
- On Cancellation: Status → Cancelled.

## 8. Tasks & Custom Notifications

- Task: Auto-created for managers to review requests.
- Custom Notification (via Salesforce App): Push notification sent when a new leave request is assigned to a manager.

## ✅ Phase 4 Outcome:

- All leave management workflows automated (submission, approval, rejection, cancellation).
- Employees & managers receive real-time notifications.
- HR/Admin has complete visibility with fewer manual interventions.
