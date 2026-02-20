# Phase 6: User Interface Development
## 1. Lightning App Builder

- Designed a custom Leave Management App in Salesforce.

- App includes navigation tabs:
  - Home (dashboard & announcements)
  - My Leaves (employee leave records)
  - Leave Requests (manager view)
  - Reports & Dashboards
 
    <img width="1882" height="882" alt="image" src="https://github.com/user-attachments/assets/f46e75c9-f480-4708-9e8b-d3192c71c4b0" />


## 2. Record Pages

- Customized LeaveRequest__c Record Page to show:

  - Employee details
  - Leave type, dates, and reason
  - Manager comments
  - Approval/Rejection buttons (Quick Actions)

- Compact layouts added for quick visibility of status.

## 3. Tabs

- Created custom tabs for:
  - Leave Request (object tab)
 
     <img width="1892" height="756" alt="image" src="https://github.com/user-attachments/assets/6c3afa13-e72f-4ec4-8831-5ffd7a9e9749" />
     
  - Leave Dashboard (Lightning app page with reports & charts)

## 4. Home Page Layouts

- Customized with:
  - Employee Leave Summary Chart
  - Quick Action: Apply for Leave
  - Recent Leave Requests list view
 
    <img width="1915" height="986" alt="image" src="https://github.com/user-attachments/assets/2045b1f1-a6f4-43f1-b248-6976e9abe6de" />


## 5. Utility Bar

- Added Quick Actions:

  - Apply Leave
  - Contact HR (case creation)

## 6.Lightning Web Components (LWC)

### Built multiple LWCs to handle leave functionality:

- applyLeave

  - Form for employees to apply for leave.
  - Fields: Leave Type, From Date, To Date, Reason.
  - Client-side validation before submission.
 
        // applyLeave.js
        import { LightningElement, track } from 'lwc';
        import createLeaveRequest from '@salesforce/apex/LeaveRequestController.createLeaveRequest';
        
        export default class ApplyLeave extends LightningElement {
            @track leaveType;
            @track fromDate;
            @track toDate;
            @track reason;
    
        handleSubmit() {
            if(!this.leaveType || !this.fromDate || !this.toDate) {
                alert('All fields are required');
                return;
            }
            createLeaveRequest({
                leaveType: this.leaveType,
                fromDate: this.fromDate,
                toDate: this.toDate,
                reason: this.reason
            })
            .then(() => {
                alert('Leave request submitted successfully');
            })
            .catch(error => {
                console.error(error);
            });
        }
        }


- myLeaves
  - Displays logged-in employee’s leave history.
  -  Uses @wire to fetch data from LeaveRequestController.getMyLeaves().
    - Color-coded statuses:
    -     Approved ✅ = Green
    -     Pending ⏳ = Yellow
    -     Rejected ❌ = Red
- leaveRequest (Manager View)
  - Managers can view and act on leave requests.
  - Buttons for Approve / Reject directly from the LWC.
  - Sends updates via Apex controller + email notifications.

            // leaveRequest.js
        import { LightningElement, track, wire } from 'lwc';
        import getPendingRequests from '@salesforce/apex/LeaveRequestController.getPendingRequests';
        import updateLeaveStatus from '@salesforce/apex/LeaveRequestController.updateLeaveStatus';
        
        export default class LeaveRequest extends LightningElement {
            @wire(getPendingRequests) requests;
        
            handleAction(event) {
                const leaveId = event.target.dataset.id;
                const status = event.target.dataset.status;
        
                updateLeaveStatus({ leaveId: leaveId, newStatus: status })
                    .then(() => {
                        alert('Leave ' + status);
                    })
                    .catch(error => {
                        console.error(error);
                    });
            }
        }


## 7. Apex with LWC

- Imperative Apex Calls: Used in applyLeave and leaveRequest for record insert/update.
- Wire Adapters: Used in myLeaves to fetch employee’s leaves dynamically.


## 8. Navigation Service

- Used in LWC to navigate between:

  - Leave request record page
  - Leave dashboard reports
  - Apply Leave form

## ✅ Phase 6 Outcome:

- Built a modern, responsive UI using LWC.
- Enhanced user experience with real-time updates & quick actions.
- Managers and employees interact seamlessly with leave records.
- User interface is aligned with Salesforce Lightning design standards.
