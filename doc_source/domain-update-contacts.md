# Updating contact information and ownership for a domain<a name="domain-update-contacts"></a>

For the administrative and technical contacts for a domain, you can change all contact information without having to authorize the changes\. For more information, see [Updating contact information for a domain](#domain-update-contacts-basic)\.

For the registrant contact, you can change most values without having to authorize the changes\. However, for some TLDs, changing the owner of a domain requires authorization\. For more information, see the applicable topic\.

**Topics**
+ [Who is the owner of a domain?](#domain-update-contacts-who-is-domain-owner)
+ [TLDs that require special processing to change the owner](#domain-update-contacts-tlds)
+ [Updating contact information for a domain](#domain-update-contacts-basic)
+ [Changing the owner of a domain when the registry requires a Change of Domain Ownership form](#domain-update-contacts-domain-ownership-form)

## Who is the owner of a domain?<a name="domain-update-contacts-who-is-domain-owner"></a>

When the contact type is **Person** and you change the **First Name** or **Last Name** fields for the registrant contact, you change the owner of the domain\.

When the contact type is any value except **Person** and you change **Organization**, you change the owner of the domain\.

Note the following about changing the owner of a domain:
+ For some TLDs, there's a fee to change the owner of a domain\. To determine whether there's a fee for the TLD for your domain, see the "Change Ownership Price" column in [Amazon Route 53 Pricing for Domain Registration](https://d32ze2gidvkk54.cloudfront.net/Amazon_Route_53_Domain_Registration_Pricing_20140731.pdf)\.
**Note**  
You can't use AWS credits to pay the fee, if any, to change the owner of a domain\.
+ For some TLDs, when you change the owner of a domain, we send an authorization email to the email address for the registrant contact\. The registrant contact must follow the instructions in the email to authorize the change\.
+ For some TLDs, you need to fill out a Change of Domain Ownership Form and provide proof of identity so that an Amazon Route 53 support engineer can update the values for you\. If the TLD for your domain requires a Change of Domain Ownership form, the console displays a message that links to a form for opening a support case\. For more information, see [Changing the owner of a domain when the registry requires a Change of Domain Ownership form](#domain-update-contacts-domain-ownership-form)\.

## TLDs that require special processing to change the owner<a name="domain-update-contacts-tlds"></a>

When you change the owner of a domain, the registries for some TLDs require special processing\. If you're changing the owner for any of the following domains, perform the applicable procedure\. If you're changing the owner for any other domain, you can change the owner yourself, either programmatically or using the Route 53 console\. See [Updating contact information for a domain](#domain-update-contacts-basic)\.

The following TLDs require special processing to change the owner of the domain:

[.be](#be-special), [.cl](#cl-special), [.com.ar](#com.ar-special), [.com.au](#com.au-special), [.com.br](#com.br-special), [.com.sg](#com.sg-special), [.es](#es-special), [.fi](#fi-special), [.im](#im-special), [.it](#it-special), [.net.au](#net.au-special), [.qa](#qa-special), [.ru](#ru-special), [.se](#se-special), [.sg](#sg-special), [.sh](#sh-special) 

**\.be**  
You must get a transfer code from the registry for \.be domains, and then open a case with AWS Support\.  
+ To get the transfer code, see [https://www\.dnsbelgium\.be/en/manage\-your\-domain\-name/change\-holder\#transfer](https://www.dnsbelgium.be/en/manage-your-domain-name/change-holder#transfer), and follow the prompts\.
+ To open a case, see [Contacting AWS Support about domain registration issues](domain-contact-support.md)\.

**\.cl**  
You must complete and submit a form to AWS Support\. See [Changing the owner of a domain when the registry requires a Change of Domain Ownership form](#domain-update-contacts-domain-ownership-form)\.

**\.com\.ar**  
You must complete and submit a form to AWS Support\. See [Changing the owner of a domain when the registry requires a Change of Domain Ownership form](#domain-update-contacts-domain-ownership-form)\.

**\.com\.au**  
Perform the following steps\. You must complete the process within 14 days, or you have to start again:  

1. Change the owner, either programmatically or using the Route 53 console\. See [Updating contact information for a domain](#domain-update-contacts-basic)\.

1. Go to [https://domainform\.net/form/au/search?view=ownerchange](https://domainform.net/form/au/search?view=ownerchange), enter the name of your domain, and follow the prompts to get a form in PDF format\.

1. Print the form, and fill it out\.

1. Do one of the following:
   + Scan the form, save the scan in a common format, and email the scan to au\_trades@ispapi\.net\.
   + Fax the form to \+49 6841 6984 299\.

**\.com\.br**  
You must complete and submit a form to AWS Support\. See [Changing the owner of a domain when the registry requires a Change of Domain Ownership form](#domain-update-contacts-domain-ownership-form)\.

**\.com\.sg**  
You must complete and submit a form to AWS Support\. See [Changing the owner of a domain when the registry requires a Change of Domain Ownership form](#domain-update-contacts-domain-ownership-form)\.

**\.es**  
You must complete and submit a form to AWS Support\. See [Changing the owner of a domain when the registry requires a Change of Domain Ownership form](#domain-update-contacts-domain-ownership-form)\.

**\.fi**  
You must complete and submit a form to AWS Support\. We arrange for Ficora, the registry for \.fi domains, to send you a code that allows a change of ownership for the domain\. You forward the code to us, and we complete the process\. See [Changing the owner of a domain when the registry requires a Change of Domain Ownership form](#domain-update-contacts-domain-ownership-form)\.

**\.im**  
You must open a case with AWS Support\. See [Contacting AWS Support about domain registration issues](domain-contact-support.md)\.

**\.it**  
You must open a case with AWS Support\. See [Contacting AWS Support about domain registration issues](domain-contact-support.md)\.

**\.net\.au**  
Perform the following steps\. You must complete the process within 14 days, or you have to start again:  

1. Change the owner, either programmatically or using the Route 53 console\. See [Updating contact information for a domain](#domain-update-contacts-basic)\.

1. Go to [https://domainform\.net/form/au/search?view=ownerchange](https://domainform.net/form/au/search?view=ownerchange), enter the name of your domain, and follow the prompts to get a form in PDF format\.

1. Print the form, and fill it out\.

1. Do one of the following:
   + Scan the form, save the scan in a common format, and email the scan to au\_trades@ispapi\.net\.
   + Fax the form to \+49 6841 6984 299\.

**\.qa**  
You must complete and submit a form to AWS Support\. See [Changing the owner of a domain when the registry requires a Change of Domain Ownership form](#domain-update-contacts-domain-ownership-form)\.

**\.ru**  
You must complete and submit a form to AWS Support\. See [Changing the owner of a domain when the registry requires a Change of Domain Ownership form](#domain-update-contacts-domain-ownership-form)\.

**\.se**  
You must complete and submit a form to AWS Support\. See [Changing the owner of a domain when the registry requires a Change of Domain Ownership form](#domain-update-contacts-domain-ownership-form)\.

**\.sg**  
You must complete and submit a form to AWS Support\. See [Changing the owner of a domain when the registry requires a Change of Domain Ownership form](#domain-update-contacts-domain-ownership-form)\.

**\.sh**  
You must complete and submit a form to AWS Support\. See [Changing the owner of a domain when the registry requires a Change of Domain Ownership form](#domain-update-contacts-domain-ownership-form)\.

## Updating contact information for a domain<a name="domain-update-contacts-basic"></a>

To update contact information for a domain, perform the following procedure\. <a name="domain-update-contacts-procedure"></a>

**To update contact information for a domain**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Registered Domains**\.

1. Choose the name of the domain that you want to update contact information for\.

1. Choose **Edit Contacts**\.

1. If you're changing the email address for the registrant contact, perform the following steps\. If you aren't changing the email address for the registrant contact, skip to step 6\.

   1. Change *only* the email address for the registrant contact\. Don't change any other values for any of the contacts for the domain\. If you also want to change other values, you change them later in the process\.

   1. Choose **Save**\.

      When the change is complete, we send email to the new email address confirming that the change is complete\. You don't need to authorize the change\.

   1. If you want to change other values for the registrant, administrative, or technical contacts for the domain, return to step 1 and repeat the procedure\.

1. Update the applicable values\. For more information, see [Values that you specify when you register or transfer a domain](domain-register-values-specify.md)\.

   Depending on the TLD for your domain and the values that you're changing, the console might display the following message:

   "To change the registrant name or organization, open a case\."

   If you see that message, skip the rest of this procedure and see [Changing the owner of a domain when the registry requires a Change of Domain Ownership form](#domain-update-contacts-domain-ownership-form) for more information\.

1. Choose **Save**\.

1. **AISPL \(India\) customers only**: If your contact address is in India, your user agreement is with Amazon Internet Services Pvt\. Ltd \(AISPL\), a local AWS seller in India\. To change the owner of a domain when the TLD registry charges a fee to change the owner, perform the following steps to pay the fee for the extension\. 

   1. Go to the [Orders and Invoices](https://console.aws.amazon.com/billing/home#/paymenthistory) page in the AWS Management Console\.

   1. In the **Payments Due** section, find the applicable invoice\.

   1. In the **Actions** column, choose **Verify and Pay**\.

      After you pay the invoice, we change the applicable settings for the registrant contact\.
**Important**  
If you don't pay the invoice within five days, the invoice is canceled\. To change settings for the registrant contact after an invoice is canceled, resubmit the request\.

   For more information, see [Managing your payments in India](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/edit-aispl-payment-method.html) in the *AWS Billing and Cost Management User Guide*\.

1. If you changed the domain owner, as described in [Who is the owner of a domain?](#domain-update-contacts-who-is-domain-owner), we send email to the registrant contact for the domain\. The email asks for authorization for the change of owner\. 

   If we don't receive authorization for the change within 3 to 15 days, depending on the top\-level domain, we must cancel the request as required by ICANN\.

   The email comes from one of the following email addresses\.  
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/domain-update-contacts.html)

1. If you encounter issues while updating contact information, you can contact AWS Support for free\. For more information, see [Contacting AWS Support about domain registration issues](domain-contact-support.md)\.

## Changing the owner of a domain when the registry requires a Change of Domain Ownership form<a name="domain-update-contacts-domain-ownership-form"></a>

If the registry for your domain requires you to complete a Change of Domain Ownership and submit the form to AWS Support, perform the following procedure\. To determine whether you need to perform this procedure, see the following topics:
+ To determine whether the value you're changing is considered a change of owner, see [Who is the owner of a domain?](#domain-update-contacts-who-is-domain-owner)\.
+ To determine whether a Change of Domain Ownership form is required for your domain, see [TLDs that require special processing to change the owner](#domain-update-contacts-tlds)\.<a name="domain-update-contacts-domain-ownership-form-procedure"></a>

**To change the owner of a domain when the registry requires a Change of Domain Ownership form**

1. See the introduction to this topic to determine whether the registry for your domain requires special processing to change the owner of the domain\. If so, and if a Change of Domain Ownership form is required, continue with this procedure\.

   If no Change of Domain Ownership form is required, perform the procedure in the applicable topic instead\.

1. Download the [Change of Domain Ownership Form](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/samples/ChangeOfOwnerForm.zip)\. The file is compressed into a \.zip file\.

1. Fill out the form\.

1. For the registrant contact for the former owner of the domain *and* for the new owner, get a copy of a signed proof of identity \(identity card, driver's license, passport, or other legal proof of identity\)\.

   In addition, if a legal entity is listed as the registrant organization, gather the following information for the former owner of the domain *and* for the new owner:
   + Proof that the organization that the domain is registered to exists\.
   + Proof that the representatives for the former owner and the new owner are authorized to act on the organization's behalf\. This document must be a certified legal document that contains both the name of the organization and the names of the representatives as signing officers \(for example, CEO, President, or Executive Director\)\.

1. Scan the Change of Domain Ownership form and the required proof\. Save the scanned documents in a common format, such as a \.pdf file or a \.png file\.

1. Using the AWS account that the domain is currently registered to, sign in to the [AWS Support Center](https://console.aws.amazon.com/support/home?region=us-east-1#/case/create?issueType=customer-service&serviceCode=billing&categoryCode=domain-name-registration-issue)\.
**Important**  
You must sign in either by using the root account or by using an IAM user that has been granted IAM permissions in one or more of the following ways:  
The user is assigned the **AdministratorAccess** managed policy\.
The user is assigned the **AmazonRoute53DomainsFullAccess** managed policy\.
The user is assigned the **AmazonRoute53FullAccess** managed policy\.
If you don't sign in either by using the root account or by using an IAM user that has the required permissions, we can't update the domain owner\. This requirement prevents unauthorized users from changing the owner of a domain\.

1. Specify the following values:  
**Regarding**  
Accept the default value of **Account and Billing Support**\.  
**Service**  
Accept the default value of **Billing**\.  
**Category**  
Accept the default value of **Domain name registration issue**\.  
**Subject**  
Specify **Change the owner of a domain**\.  
**Description**  
Provide the following information:  
   + Domain that you want to change the owner for
   + [12\-digit account ID](https://docs.aws.amazon.com/general/latest/gr/acct-identifiers.html#FindingYourAccountIdentifiers) of the AWS account that the domain is registered to  
**Add attachment**  
Upload the documents that you scanned in step 5\.  
**Contact method**  
Specify a contact method and enter the applicable values\.

1. Choose **Submit**\.

   An AWS Support engineer reviews the information that you provided and updates the settings\. The engineer will either contact you when the update is finished or contact you for more information\.