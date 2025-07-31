Project -- # whatnext-vision-motors-salesforce
Salesforce CRM project for streamlining vehicle orders, stock validation, and dealer assignment.

USE CASE 
WhatsNext Vision Motors is revolutionizing its customer experience and operational efficiency with a cutting-edge Salesforce CRM implementation. The project streamlines the vehicle ordering process by auto-assigning orders to the nearest dealer based on customer location and preventing orders for out-of-stock vehicles. Automated workflows update order statuses dynamically and send scheduled email reminders for test drives. Key technical implementations include Apex triggers for stock validation, batch jobs for stock updates, and scheduled Apex for automated order processing. This initiative enhances customer satisfaction, improves order accuracy, and boosts overall operational efficiency.

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
## 📄 Project Documentation

📥 [Download Full Documentation – Whatnext Vision Motors](./Documentation_Whatnext_VisionMotors_project.pdf)

## 📽️ Project Demo Video

You can watch the demo of the project here: [Click to Watch Demo](https://drive.google.com/file/d/1_D_nf-DVATTtDLoOhZtSLycny4EmwtzV/view?usp=sharing)


The documentation includes:
- Project objectives and architecture
- Phase-wise development details
- Object model and relationships
- Automation, Apex, testing, deployment
- Screenshots and flow logic

Design Data Model and Security Model

A custom data model was designed using six main custom objects:
Vehicle__c 
Vehicle_Dealer__c
Vehicle_Customer__c
Vehicle_Order__c
Vehicle_Test_Drive__c
Vehicle_Service_Request__c


Apex Development
  
Custom Apex logic was implemented to support business rules around vehicle ordering, stock validation, and scheduled updates. The following classes and triggers were created:

📌 VehicleOrderTriggerHandler.cls
A trigger handler class that modularizes logic for Vehicle_Order__c triggers.
Prevents order creation if the selected vehicle is out of stock.
Updates vehicle stock by reducing quantity when an order is confirmed.

📌 VehicleOrderTrigger.trigger
Calls the VehicleOrderTriggerHandler class on insert and update.
Executes logic in both before and after contexts.

📌 VehicleOrderBatch.cls
Batch Apex job that scans for orders with status 'Pending'.
If stock becomes available, it sets the order status to 'Confirmed' and reduces vehicle stock accordingly.

📌 VehicleOrderBatchScheduler.cls
Scheduled Apex class that invokes VehicleOrderBatch daily.
Ensures pending orders are regularly checked and updated based on stock.

🔄 Flows

### 📌 AutoAssignDealer (Flow)
- Triggered on `Vehicle_Order__c` create/update
- Gets nearest `Vehicle_Dealer__c` based on customer location
- Assigns it to the order
  
### 📌 TestDriveReminder (Scheduled Flow)
- Scheduled 1 day before `Test_Drive_Date__c`
- Fetches customer email
- Sends a reminder email

Debug / Manual Test Execution
To test the batch job from Developer Console:

### Execute this in Anonymous Window:
```apex
VehicleOrderBatch job = new VehicleOrderBatch();
Database.executeBatch(job, 50);
