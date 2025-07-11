Project -- # whatnext-vision-motors-salesforce
Salesforce CRM project for streamlining vehicle orders, stock validation, and dealer assignment.

This project implements a Salesforce CRM solution to manage vehicle orders, stock validation, test drives, and dealer assignments.

Features
- Auto-assign dealer based on customer location
- Stock check before placing order (trigger logic)
- Batch job for updating order status when stock is replenished
- Scheduled job runs daily
- Email reminder for test drives

Tech Stack
- Salesforce Lightning Experience
- Apex Triggers, Classes, and Batch Apex
- Record-Triggered Flows & Scheduled Flows
- Salesforce Setup (Roles, Profiles, Sharing Rules)
- Lightning App Builder & Dynamic Forms
- 
📄 [Open Documentation PDF](./WhatsNext_VisionMotors_Project_Documentation.pdf)
The documentation includes:
- Project objectives and architecture
- Phase-wise development details
- Object model and relationships
- Automation, Apex, testing, deployment
- Screenshots and flow logic

🔄 Flows

### 📌 AutoAssignDealer (Flow)
- Triggered on `Vehicle_Order__c` create/update
- Gets nearest `Vehicle_Dealer__c` based on customer location
- Assigns it to the order
  📸 Screenshot:  
  ![Auto Assign Dealer Flow](./flows/AutoAssignDealer_Flow.jpeg)

### 📌 TestDriveReminder (Scheduled Flow)
- Scheduled 1 day before `Test_Drive_Date__c`
- Fetches customer email
- Sends a reminder email
  📸 Screenshot:  
  ![Test Drive Reminder Flow](./flows/TestDriveReminder_Flow.jpeg)

Debug / Manual Test Execution
To test the batch job from Developer Console:

### Execute this in Anonymous Window:
```apex
VehicleOrderBatch job = new VehicleOrderBatch();
Database.executeBatch(job, 50);
