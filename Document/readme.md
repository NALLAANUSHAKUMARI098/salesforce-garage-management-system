project report in pdf

trigger AmountDistribution on Service_Records__c (before insert, before update) {
    for(Service_Records__c sr : Trigger.new) {
        if(sr.Appointment_r != null && sr.Appointmentr.Service_Amount_c != null) {
            sr.Payment_Paid_c = sr.Appointmentr.Service_Amount_c;
        }
    }
}


public class AmountDistributionHandler {
    public static void updateAmount(List<Service_Records__c> serviceRecords) {
        for(Service_Records__c sr : serviceRecords) {
            if(sr.Appointment_r != null && sr.Appointmentr.Service_Amount_c != null) {
                sr.Payment_Paid_c = sr.Appointmentr.Service_Amount_c;
            }
        }
    }
}


{!$Record.Service_records_r.Appointmentr.Service_Amount_c}


{!$Record.Service_records_r.Appointmentr.Customer_Namer.Gmail_c}


Appointment_Date__c < TODAY()


Billing_Amount__c <= 0

