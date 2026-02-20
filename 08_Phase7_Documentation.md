# Phase 7: Integration & External Access
## 🔹 1. Named Credentials Setup

- Define Named Credentials in Salesforce to securely store external service URLs + authentication.

- Example use case: Connecting Salesforce to an HR system API for employee details.


## 🔹 2. External Services & Callouts

Demonstrate Apex HTTP Callout to fetch leave balance from an external HR system.

Sample Code (HTTP Callout):

    public with sharing class LeaveIntegrationService {
        public static void getLeaveBalance(String employeeId) {
            Http http = new Http();
            HttpRequest req = new HttpRequest();
            req.setEndpoint('callout:HR_System/leavebalance/' + employeeId);
            req.setMethod('GET');
            
            HttpResponse res = http.send(req);
            if(res.getStatusCode() == 200){
                System.debug('Leave Balance: ' + res.getBody());
            } else {
                System.debug('Error: ' + res.getStatus());
            }
        }
    }

## 🔹 3. Email Service Integration

- Salesforce sends email notifications when leave is approved/rejected.
- Can also integrate with Gmail/Outlook API for two-way sync.

    <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/f89dd384-7a2f-4c23-b0dc-6db7bdfe4647" />



## 🔹 4. Platform Events for Real-time Updates

Use Platform Events to notify external systems (like HR Payroll) when leave status changes.

Sample Platform Event Trigger:

    trigger LeaveEventTrigger on LeaveRequest__c (after update) {
        for(LeaveRequest__c lr : Trigger.new){
            if(lr.Status__c == 'Approved'){
                Leave_Status_Event__e eventMsg = new Leave_Status_Event__e(
                    LeaveId__c = lr.Id,
                    Status__c = 'Approved',
                    EmployeeEmail__c = lr.User__r.Email
                );
                Database.SaveResult result = EventBus.publish(eventMsg);
            }
        }
    }



## 🔹 5. Remote Site Settings

- Before callouts, add endpoints under Setup → Remote Site Settings.
  - Example: https://api.hr-system.com

    <img width="1880" height="892" alt="image" src="https://github.com/user-attachments/assets/1511fc64-5b59-48f0-a474-42edf2e60905" />


## 🔹 6. OAuth & Authentication

- If external API requires OAuth 2.0, connect via Named Credentials → OAuth.
- Secure token handling ensures safe communication.

## 🔹 7. Phase 7 Outcomes

- Secure external integration setup.
- Real-time event-driven communication.
- Email notifications for leave updates.
- Extended CRM capability with external HR/Payroll systems.
