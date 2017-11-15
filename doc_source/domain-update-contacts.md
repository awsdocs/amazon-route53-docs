# Updating Contact Information and Ownership for a Domain<a name="domain-update-contacts"></a>

For the administrative and technical contacts for a domain, you can change all contact information without having to authorize the changes\. For more information, see [Updating Contact Information for a Domain](#domain-update-contacts-basic)\.

For the registrant contact, you can change most values without having to authorize the changes\. However, for some TLDs, changing the owner of a domain or changing the email address of the registrant contact requires authorization\. For more information, see the applicable topic\.


+ [Who Is the Owner of a Domain?](#domain-update-contacts-who-is-domain-owner)
+ [Updating Contact Information for a Domain](#domain-update-contacts-basic)
+ [Changing the Owner of a Domain When the Registry Requires a Change of Domain Ownership Form](#domain-update-contacts-domain-owership-form)
+ [Updating the Email Address for a Domain When You Can't Access Email at the Old Address](#domain-update-contacts-change-email-form)

## Who Is the Owner of a Domain?<a name="domain-update-contacts-who-is-domain-owner"></a>

When the contact type is **Person** and you change the **First Name** or **Last Name** fields for the registrant contact, you change the owner of the domain\.

When the contact type is any value except **Person** and you change **Organization**, you change the owner of the domain\.

Note the following about changing the owner of a domain:

+ For some TLDs, when you change the owner of a domain, we send an authorization email to the email address for the registrant contact\. The registrant contact must follow the instructions in the email to authorize the change\.

+ For some TLDs, you need to fill out a Change of Domain Ownership Form and provide proof of identity so that an Amazon Route 53 support engineer can update the values for you\. If the TLD for your domain requires a Change of Domain Ownership form, the console displays a message that links to a form for opening a support case\. For more information, see [Changing the Owner of a Domain When the Registry Requires a Change of Domain Ownership Form](#domain-update-contacts-domain-owership-form)\.

## Updating Contact Information for a Domain<a name="domain-update-contacts-basic"></a>

To update contact information for a domain, perform the following procedure\. 

**To update contact information for a domain**

1. Sign in to the AWS Management Console and open the Amazon Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Registered Domains**\.

1. Choose the name of the domain that you want to update contact information for\.

1. Choose **Edit Contacts**\.

1. Update the applicable values\. For more information, see [Values that You Specify When You Register a Domain](domain-register-values-specify.md)\.

   Depending on the TLD for your domain and the values that you're changing, the console might display the following message:

   "To change the registrant name or organization, open a case\."

   If you see that message, skip the rest of this procedure and see [Changing the Owner of a Domain When the Registry Requires a Change of Domain Ownership Form](#domain-update-contacts-domain-owership-form) for more information\.

1. Choose **Save**\.

1. If you changed the following values, we send you an email that asks for your authorization:  
**Domain owner**  
If you change the owner of the domain, as described in [Who Is the Owner of a Domain?](#domain-update-contacts-who-is-domain-owner), we send email to the registrant contact for the domain\.  
**Email address for the registrant contact \(only for some TLDs\)**  
For some TLDs, if you change the email address for the registrant contact, we send an email to the old and the new email address for the registrant contact\. Someone at both email addresses must follow the instructions in the email to authorize the change\.  
If you get an authorization email at your new email address and you don't have access to the old email address, open a support case\. For more information, see [Updating the Email Address for a Domain When You Can't Access Email at the Old Address](#domain-update-contacts-change-email-form)\.

   If we don't receive authorization for the change within 3 to 15 days, depending on the top\-level domain, we must cancel the request as required by ICANN\.

   The email comes from one of the following email addresses\.  
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/domain-update-contacts.html)

## Changing the Owner of a Domain When the Registry Requires a Change of Domain Ownership Form<a name="domain-update-contacts-domain-owership-form"></a>

If the Amazon Route 53 console displays the following message when you try to change contact information, the registry for your TLD requires that you fill out a Change of Domain Ownership form:

"To change the registrant name or organization, open a case\."

Perform the following procedure to request the ownership change\. When your ownership has been verified, an AWS customer support engineer will change contact information for you\.

**To change the owner of a domain when the registry requires a Change of Domain Ownership form**

1. Download the [Change of Domain Ownership Form](https://s3.amazonaws.com/AWSCS_CustomerForms/AmazonRegistrarChangeOfDomainOwnershipForm.pdf)\.

1. Fill out the form\.

1. If a legal entity is listed as the registrant name or organization, gather the following information:

   + Proof that the organization that the domain is registered to exists\.

   + Proof that you're authorized to act on the organization's behalf\. This document must be a certified legal document that contains both the name of the organization and your name as a signing officer \(for example, CEO, President, or Executive Director\)\.

1. Scan the Change of Domain Ownership form and the required proof, if applicable\. Save the scanned documents in a common format, such as a \.pdf file or a \.png file\.

1. Using the AWS account that the domain is currently registered to, sign in to the [AWS Support Center](https://console.aws.amazon.com/support/home?region=us-east-1#/case/create?issueType=customer-service&serviceCode=billing&categoryCode=domain-name-registration-issue)\.
**Important**  
You must sign in by using the root account that the domain is currently registered to\. If you sign in by using an IAM user or any other account, we can't update the domain owner\. This requirement prevents unauthorized users from changing the owner of a domain\.

1. Specify the following values:  
**Regarding**  
Accept the default value of **Account and Billing Support**\.  
**Service**  
Accept the default value of **Billing**\.  
**Category**  
Accept the default value of **Domain name registration issue**\.  
**Subject**  
Specify **Change the owner of a domain**  
**Description**  
Provide the following information:  

   + Domain that you want to change the owner for

   + Account ID of the AWS account that the domain is registered to  
**Add attachment**  
Upload the documents that you scanned in step 4\.  
**Contact method**  
Specify a contact method and enter the applicable values\.

1. Choose **Submit**\.

   A customer support engineer reviews the information that you provided and updates the settings\. The engineer will either contact you when the update is finished or contact you for more information\.

## Updating the Email Address for a Domain When You Can't Access Email at the Old Address<a name="domain-update-contacts-change-email-form"></a>

When you change the email address for the registrant contact for a domain, the registries for some TLDs require us to get authorization from the registrant contact at the old email address and at the new email address\. If you receive an authorization email at the new email address, your TLD requires us to get authorization from both email addresses\. If you no longer have access to the old email address, perform the following procedure\.

**Note**  
You can use this procedure only if the domain is already registered with Amazon Route 53\. If you're transferring a domain to Amazon Route 53 and you can't access email at the email address for the registrant contact, you must work with the current registrar to update the email address\.

****

1. Download the [Change of Registrant Email Form](https://s3.amazonaws.com/AWSCS_CustomerForms/AmazonRegistrarChangeOfRegistrantEmailForm.pdf)\.

1. Fill out the form\.

1. If a legal entity is listed as the registrant name or organization, gather the following information:

   + Proof that the organization that the domain is registered to exists\.

   + Proof that you're authorized to act on the organization's behalf\. This document must be a certified legal document that contains both the name of the organization and your name as a signing officer \(for example, CEO, President, or Executive Director\)\.

1. Scan the Change of Registrant Email form and the required proof, if applicable\. Save the scanned documents in a common format, such as a \.pdf file or a \.png file\.

1. Using the AWS account that the domain is currently registered to, sign in to the [AWS Support Center](https://console.aws.amazon.com/support/home?region=us-east-1#/case/create?issueType=customer-service&serviceCode=billing&categoryCode=domain-name-registration-issue)\.
**Important**  
You must sign in by using the root account that the domain is currently registered to\. If you sign in by using an IAM user or any other account, we can't update the email address\. This requirement prevents unauthorized users from changing the contact information for a domain\.

1. Specify the following values:  
**Regarding**  
Accept the default value of **Account and Billing Support**\.  
**Service**  
Accept the default value of **Billing**\.  
**Category**  
Accept the default value of **Domain name registration issue**\.  
**Subject**  
Specify **Change the email address for a domain**  
**Description**  
Provide the following information:  

   + Domain that you want to change the email address for

   + Account ID of the AWS account that the domain is registered to  
**Add attachment**  
Upload the documents that you scanned in step 4\.  
**Contact method**  
Specify a contact method and enter the applicable values\.

1. Choose **Submit**\.

   A customer support engineer reviews the information that you provided and updates the settings\. The engineer will either contact you when the update is finished or contact you for more information\.