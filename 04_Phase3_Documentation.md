# Phase 3: Data Modeling & Relationships
## 1. Standard & Custom Objects
### Standard Objects Used:
- LeaveRequest__c – The main object that stores all employee leave applications.
### Custom Objects Created:

- Leave Request → Stores each leave application.
- Holiday Calendar → Stores organization-wide holidays.
- Approval History → Records manager approvals/rejections for audit purposes.

## 2. Fields

### Leave Request Object Fields:

- Employee (Lookup to User)
- Leave Type (Picklist: Sick, Casual, Earned, Maternity, etc.)
- From Date (Date)
- To Date (Date)
- Total Days (Formula: To Date – From Date – Holidays)
- Reason (Text Area)
- Status (Picklist: Draft, Submitted, Approved, Rejected, Cancelled)
- Manager Comments (Long Text)


- <img width="1886" height="920" alt="image" src="https://github.com/user-attachments/assets/de925a3a-77d6-4750-ac47-6e71675c96cf" />
  
## 3. Record Types

### Leave Request Record Types:

- Sick Leave Request
- Casual Leave Request
- Earned Leave Request
- Special Leave Request (e.g., Maternity, Paternity)
- Each record type has different page layouts and approval rules.

-  <img width="1892" height="804" alt="image" src="https://github.com/user-attachments/assets/92383ebb-4f63-4d9c-b225-d0b14378d3d2" />


## 4. Page Layouts

- Employee Layout (Leave Request): Fields: From Date, To Date, Reason, Leave Type.
- Manager Layout (Leave Request): Includes additional fields: Status, Manager Comments.

- 
  <img width="1920" height="1080" alt="Screenshot 2025-09-13 155110" src="https://github.com/user-attachments/assets/a49549cb-fc3f-46a0-9cae-f6ca2b926ffb" />


### Compact Layouts

   - For Leave Request, compact layout shows: Leave Type, Dates, Status.

## 5. Relationships

### Lookup Relationship:

- Leave Request → User (Employee).
- Leave Balance → User.

### Master-Detail Relationship:

- Approval History → Leave Request (deletes when parent request is deleted).


## ✅ Phase 3 Outcome:

- Data model created with required custom objects and fields.
- Relationships established between employees, leave requests.
- Record types, page layouts, and compact layouts designed for different users.
