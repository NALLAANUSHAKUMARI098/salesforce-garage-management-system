# salesforce-garage-management-system
> A CRM project to manage customer details, appointments, service records, billing, and feedback for automotive garages, built using Salesforce Developer tools.

---

## 🧾 Project Overview

The Garage Management System is designed to:
- Optimize customer service and vehicle tracking
- Automate appointments and reminders
- Enable real-time repair tracking
- Manage parts inventory and billing
- Improve customer satisfaction and business insights

---

## 🧩 Key Features

- Customer Detail Management  
- Appointment Scheduling & Notifications  
- Service Record Tracking  
- Billing & Invoicing  
- Feedback Collection  
- Reports and Dashboards  
- Automation with Flows, Triggers, and Validation

---

## 💻 APEX CODE

### 1. AmountDistribution.apxt (Trigger)

apex
trigger AmountDistribution on Service_Records__c (before insert, before update) {
    for(Service_Records__c sr : Trigger.new) {
        if(sr.Appointment__r != null && sr.Appointment__r.Service_Amount__c != null) {
            sr.Payment_Paid__c = sr.Appointment__r.Service_Amount__c;
        }
    }
}


---

### 2. AmountDistributionHandler.apxc (Apex Class)

apex
public class AmountDistributionHandler {
    public static void updateAmount(List<Service_Records__c> serviceRecords) {
        for(Service_Records__c sr : serviceRecords) {
            if(sr.Appointment__r != null && sr.Appointment__r.Service_Amount__c != null) {
                sr.Payment_Paid__c = sr.Appointment__r.Service_Amount__c;
            }
        }
    }
}


---

## 🔁 FLOW FORMULAS

### 1. Payment Auto Update Flow

*Target Field*: Payment_Paid__c

text
{!$Record.Service_records__r.Appointment__r.Service_Amount__c}


---

### 2. Email Notification Flow

*Recipient Email Field*:

text
{!$Record.Service_records__r.Appointment__r.Customer_Name__r.Gmail__c}


---

## ✅ VALIDATION RULES

### 1. Appointment Date Cannot Be in the Past

text
Appointment_Date__c < TODAY()


*Error Message*: Appointment date cannot be before today.

---

### 2. Billing Amount Must Be Greater Than Zero

text
Billing_Amount__c <= 0


*Error Message*: Billing amount must be more than zero.

---

## ❌ DUPLICATE RULES

### Matching Rule for Customer Gmail

- Field: Gmail__c
- Matching Method: Exact

### Duplicate Rule

- Allow Duplicates: ❌ No  
- Show Alert: ✅ Yes  
- Applies On: Create & Edit

---

## 📊 REPORTS

*Sample Report: New Services Report*

- Fields:
  - Customer Name
  - Appointment Date
  - Service Amount
  - Feedback Rating
- Filter: CreatedDate = THIS_MONTH

---

## 📈 DASHBOARD COMPONENTS

- 💰 Total Revenue (Sum of Service_Amount__c)
- 👨‍🔧 Services Per Technician
- ⭐ Average Feedback Rating

---

## 🧪 TESTING STRATEGY

- Positive, Negative, and Bulk Tests for Triggers & Classes
- UAT (User Acceptance Testing)
- Performance Testing for large records

---



   vedio Demo:
   https://drive.google.com/file/d/1_Y_nGA88X87HscBkSGl6cT4fkCnCdSYd/view?usp=drivesdk


   ## 🙋‍♀ Author

*Nalla Anusha Kumari*  
Bonam Venkata Chalamayya Institute of Technology & Science  
📧 22h41a04a2anusha.n@gmail.com


   
