# Deleting a domain name registration<a name="domain-delete"></a>

For most top\-level domains \(TLDs\), you can delete the registration if you no longer want it\. If the registry allows you to delete the registration, perform the procedure in this topic\.

Note the following:

**The registration fee is not refundable**  
If you delete a domain name registration before the registration is scheduled to expire, AWS does not refund the registration fee\. 

**TLDs that allow you to delete a domain registration**  
To determine whether you can delete the registration for your domain, see [Domains that you can register with Amazon Route 53](registrar-tld-list.md)\. If the section for your TLD doesn't include a "Deletion of domain registration" subsection, you can delete the domain\.

**What if you can't delete a domain registration?**  
If the registry for your domain doesn't allow you to delete a domain name registration, you must wait for the domain to expire\. To ensure that the domain isn't automatically renewed, disable automatic renewal for the domain\. When the **Expires on** date passes, Route 53 automatically deletes the registration for the domain\. For information about how to change the automatic renewal setting, see [Enabling or disabling automatic renewal for a domain](domain-enable-disable-auto-renewal.md)\.

**Delay before a domain is deleted and available to register again**  
Almost all registries prevent anyone from immediately registering a domain that has just expired\. The typical delay is one to three months, depending on the TLD\. For more information, see the "Deadlines for renewing and restoring domains" section for your TLD in [Domains that you can register with Amazon Route 53](registrar-tld-list.md)\.   
Don't delete a domain and expect to reregister it if you just want to transfer the domain between AWS accounts or transfer the domain to another registrar\. See the applicable documentation instead:  
+ [Transferring a domain to a different AWS account](domain-transfer-between-aws-accounts.md)
+ [Transferring a domain from Amazon Route 53 to another registrar](domain-transfer-from-route-53.md)<a name="domain-delete-procedure"></a>

**To delete a domain name registration**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Registered Domains**\.

1. Choose the name of your domain\.

   If you want to delete a \.com\.uk, \.me\.uk, \.org\.uk, or \.uk domain, see [To delete \.com\.uk, \.me\.uk, \.org\.uk, and \.uk domain name registrations](#domain-delete-uk-procedure)\. 

1. Choose **Delete Domain**\.

1. If the registry for your TLD allows deleting a domain name registration, choose **Delete Domain**\.

   We send an email to the registrant for the domain to verify that the registrant wants to delete the domain\. \(This is an ICANN requirement\.\) The email comes from one of the following email addresses:
   + noreply@registrar\.amazon\.com – for TLDs registered by Amazon Registrar\.
   + noreply@domainnameverification\.net – for TLDs registered by our registrar associate, Gandi\.

   To determine who the registrar is for your TLD, see [Domains that you can register with Amazon Route 53](registrar-tld-list.md)\.

1. When you receive the verification email, choose the link in the email, and either approve or reject the request to delete the domain\. 
**Important**  
The registrant contact must follow the instructions in the email, or we must cancel the deletion request after five days as required by ICANN\.

   You'll receive another email when your domain has been deleted\. To determine the current status of your request, see [Viewing the status of a domain registration](domain-view-status.md)\.

1. Delete the records in the hosted zone for the deleted domain, and then delete the hosted zone\. After you delete the hosted zone, Route 53 stops billing you the monthly charge for a hosted zone\. For more information, see the following documentation:
   + [Deleting records](resource-record-sets-deleting.md)
   + [Deleting a public hosted zone](DeleteHostedZone.md)
   + [Route 53 Pricing](https://aws.amazon.com/route53/pricing)

1. If you encounter issues while deleting a domain name registration, you can contact AWS Support for free\. For more information, see [Contacting AWS Support about domain registration issues](domain-contact-support.md)\.<a name="domain-delete-uk-procedure"></a>

**To delete \.com\.uk, \.me\.uk, \.org\.uk, and \.uk domain name registrations**

If you want to delete a \.com\.uk, \.me\.uk, \.org\.uk, or \.uk domain, you create an account with Nominet, the registry for \.uk domains\. For more information, see "Cancelling your domain name" on the Nominet website, [https://www\.nominet\.uk/domain\-support/](https://www.nominet.uk/domain-support/)\.
**Important**  
If you delete \(cancel\) a \.uk domain name, it's deleted by the end of the day and becomes available for anyone to register\. If you just want to transfer the domain, do not delete it\.

Here's an overview of the process:

1. On the Nominet website, follow the instructions for logging in for the first time\. See [https://secure\.nominet\.org\.uk/auth/login\.html](https://secure.nominet.org.uk/auth/login.html)\. Nominet sends you an email with instructions for creating a password\.

1. Follow the instructions in the email that you receive from Nominet\.

1. Log in to the Nominet website, and follow the instructions for canceling \(deleting\) a domain name\.