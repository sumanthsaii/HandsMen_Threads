# Phase 5: Apex Programming (Developer)
## 1. Classes & Objects

- LeaveRequestController: Handles leave application logic (submit, update, approve, reject).
- EmailNotificationService: Sends approval/rejection notifications.
- Utility Classes: For reusable logic like date validation, string formatting, and error handling.

## 2. Apex Triggers

### Before Insert/Update:

- Validate leave dates (From_Date ≤ To_Date).
- Prevent overlapping leave requests.

### After Insert:
- Notify manager of new leave request submission.

### After Update:

- If Status = Approved → Send Approved Email
- If Status = Rejected → Send rejection email.
- If Status = Cancelled → Restore leave balance.

## 3. Trigger Design Pattern

### Handler Class Pattern followed:

- One trigger per object (e.g., LeaveRequestTrigger).
- Delegates logic to LeaveRequestHandler class.
- Improves readability, reusability, and testability.

## 4. SOQL & SOSL Usage

### SOQL:

- Fetch leave requests of current user
  -     List<LeaveRequest__c> leaveList = 
        [SELECT Id, From_Date__c, To_Date__c, Status__c 
        FROM LeaveRequest__c 
         WHERE Employee__c = :UserInfo.getUserId()];

- Fetch manager details for email notifications.
- Aggregate queries for reports (e.g., total leaves per type).

### SOSL:

- Used for searching leave requests by employee name or reason.
- Collections (List, Set, Map)
- List: Store multiple leave requests fetched from SOQL.
- Set: Avoid duplicate leave request IDs during processing.

### Control Statements

- If-Else: Approve vs Reject logic.
  -     if (newStatus == 'Approved' || newStatus == 'Rejected') {
            sendStatusEmail(leave, newStatus);
        }
- For Loops: Bulk processing of leave requests.
- Switch (with enums): Handle leave types (Sick Leave, Casual Leave, Earned Leave).
  -     public enum LeaveType {
          Sick, Casual, Earned, Maternity, Paternity
        }
        public class LeaveTypeHandler {
        public static String handleLeaveType(String leaveType) {
            String policyNote;
        switch on leaveType {
            when 'Sick' {
                policyNote = 'Sick leave requires a medical certificate if more than 2 days.';
            }
            when 'Casual' {
                policyNote = 'Casual leave limited to 5 days per quarter.';
            }
            when 'Earned' {
                policyNote = 'Earned leave can be carried forward to next year.';
            }
            when 'Maternity' {
                policyNote = 'Maternity leave policy as per HR guidelines.';
            }
            when 'Paternity' {
                policyNote = 'Paternity leave limited to 10 days.';
            }
            when else {
                policyNote = 'Unknown leave type. Please contact HR.';
            }
        }

        return policyNote;
        }
        }


## 5. Asynchronous Apex

### Future Methods:

- Asynchronous processing for long-running tasks:
- Sending email alerts to employees and managers.
- Logging cancellation/approval data for audits.

-     @AuraEnabled
        public static void sendNotification(String email, String subject, String body) {
        Messaging.SingleEmailMessage mail = new Messaging.SingleEmailMessage();
        mail.setToAddresses(new String[] { email });
        mail.setSubject(subject);
        mail.setPlainTextBody(body);
        Messaging.sendEmail(new Messaging.SingleEmailMessage[] { mail });
      }
  

## 6.Exception Handling

- Try-Catch Blocks: Handle DML and SOQL exceptions.
-     try {
        update leaveRecord;
      } catch(DmlException e) {
          System.debug('Error: ' + e.getMessage());
      }
- Custom Exceptions: For business rules like “Insufficient Leave Balance.”
- Error Logging: Store errors in a custom object Error_Log__c for admin review.

## 7. Test Classes

- Achieve > 85% coverage.
  
### Scenarios covered:

- Leave request submission (valid & invalid).
- Overlapping leave requests.
- Approval & Rejection flow.
- Cancellation update.
- Email sending functionality.

## ✅ Phase 5 Outcome:

- Robust Apex code with reusable classes and triggers.
- Asynchronous processing ensures performance.
- Proper exception handling + test coverage makes the system reliable and deployment-ready.
