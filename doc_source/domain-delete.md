# Deleting a Domain Name Registration<a name="domain-delete"></a>

For most top\-level domains \(TLDs\), you can delete the registration if you no longer want it\. Registries for some TLDs don't allow you to delete a domain name registration; instead, you must wait for it to expire\. To determine whether you can delete the registration for your domain, see [Domains That You Can Register with Amazon Route 53](registrar-tld-list.md)\.

If the registry allows you to delete the registration, perform the procedure in this topic\. If the registry doesn't allow you to delete a domain name registration, disable automatic renewal of domain registration for this domain\. When the **Expires on** date passes, Amazon Route 53 will automatically delete the registration for the domain\. For information about how to change the automatic renewal setting, see [Enabling or Disabling Automatic Renewal for a Domain](domain-enable-disable-auto-renewal.md)\.

**Important**  
If you delete a domain name registration before the registration was scheduled to expire, we will not refund the registration fee\. 

**To delete a domain name registration**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Registered Domains**\.

1. Choose the name of your domain\.

1. Choose **Delete Domain**\.

1. If the registry for your TLD allows deleting a domain name registration, choose **Delete Domain**\.

   We send an email to the registrant for the domain to verify that the registrant wants to delete the domain\. \(This is an ICANN requirement\.\) The email comes from one of the following email addresses:

   + noreply@registrar\.amazon\.com – for TLDs registered by Amazon Registrar\.

   + noreply@domainnameverification\.net – for TLDs registered by our registrar associate, Gandi\.

   To determine who the registrar is for your TLD, see [Domains That You Can Register with Amazon Route 53](registrar-tld-list.md)\.
**Important**  
The registrant contact must follow the instructions in the email, or we must cancel the deletion request as required by ICANN\.

   You'll receive another email when your domain has been deleted\. To determine the current status of your request, see [Viewing the Status of a Domain Registration](domain-view-status.md)\.

1. Delete the records in the hosted zone for the deleted domain, and then delete the hosted zone\. After you delete the hosted zone, Route 53 will stop billing you the monthly charge for a hosted zone\. For more information, see the following documentation:

   + [Deleting Records](resource-record-sets-deleting.md)

   + [Deleting a Public Hosted Zone](DeleteHostedZone.md)

   + [Route 53 Pricing](https://aws.amazon.com/route53/pricing)