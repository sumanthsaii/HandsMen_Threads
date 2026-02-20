# Phase 9: Reporting, Dashboards & Security Review

## Goal
- Track leave requests and approvals with reports & dashboards
- Protect sensitive employee leave data from unauthorized access
- Ensure managers, HR, and employees see the right information in real time
  
## 1. Reports

- Created different report formats to track leave usage:
- Tabular Report → Simple list of all leave requests (used for quick exports).
- Summary Report → Grouped by Employee Name → shows how many leaves each employee has taken.
- Matrix Report → Cross-tab view → Leave Type vs Month (helps HR see seasonal leave trends).
- Joined Report → Combined Leave Requests + Approval History → helps managers check approval timelines.

  <img width="1909" height="919" alt="image" src="https://github.com/user-attachments/assets/e97568a8-719a-4a1d-ae33-c194d7d77230" />

  
## 2. Report Types

- Created a Custom Report Type:
- Primary Object: LeaveRequest__c
- Related Object: User (Employee)
- Allows advanced reporting like: Leaves by Department or Leaves by Manager.


## 3. Dashboards

Dashboards visually display leave metrics.

A. Create Dashboard
- Go to App Launcher → Dashboards → New
- Add components from leave reports:
  - Metric: Count of Pending Leaves
  - Pie Chart: Leaves by Type
  - Bar Chart: Leaves by Status
  - Line Chart: Leaves Over Time

B. Dynamic Dashboards

Managers → See only their team’s data.
HR/Admins → See complete organization-level data.

<img width="1910" height="926" alt="Screenshot 2025-09-25 151018" src="https://github.com/user-attachments/assets/143b88cf-9711-447d-9c2b-4345f24ff05e" />

## Security
### A. Sharing Settings

- Org-Wide Defaults (OWD): Leave Requests = Private (only owner, manager, HR can see).
- Sharing Rules: Managers can access their team’s requests.
- Role Hierarchy: Employee → Manager → HR → Admin.

<img width="1892" height="903" alt="image" src="https://github.com/user-attachments/assets/87ece880-4595-410a-8bbd-cecaba878dfd" />
<img width="1905" height="912" alt="image" src="https://github.com/user-attachments/assets/68d3bb26-3741-446c-bfe3-11ba33707b7c" />



### B. Field Level Security (FLS)

- Employees: Can see only their leave details.
- Managers: Can see team leaves + approval fields.
- Sensitive fields (like Manager Comments) hidden from employees.


### C. Audit Trail

- Setup --> Audit Trail enabled.
- Tracks last 20 configuration changes (e.g., new validation rule, updated profile).
<img width="1895" height="903" alt="image" src="https://github.com/user-attachments/assets/766498e0-fc54-4c39-8ef0-f4d7f341cd67" />



## ✅ Final Outcome of Phase 9

- Reports + Dashboards = Clear visibility of leave data.
- Dynamic dashboards = Role-based insights.

Sharing + FLS + IP + Session settings = Strong data security.

Audit Trail = Full tracking of system changes.
