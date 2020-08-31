# Transferring registration for a domain to Amazon Route 53<a name="domain-transfer-to-route-53"></a>

To transfer the registration for a domain to Amazon Route 53, carefully follow the procedures in this topic\. 

**Important**  
If you skip a step, your domain might become unavailable on the internet\.

Note the following:

**Contacting AWS Support**  
If you encounter issues while transferring a domain, you can contact AWS Support for free\. For more information, see [Contacting AWS Support about domain registration issues](domain-contact-support.md)\.

**Expiration date**  
For information about how transferring your domain affects the current expiration date, see [How transferring a domain to Amazon Route 53 affects the expiration date for your domain registration](domain-transfer-to-route-53-expiration.md)\.

**Transfer fee**  
When you transfer a domain to Route 53, the transfer fee that we apply to your AWS account depends on the top\-level domain, such as \.com or \.org\. For more information, see [Route 53 Pricing](https://aws.amazon.com/route53/pricing/)\.   
You can't use AWS credits to pay the fee, if any, for transferring a domain to Route 53\.  
Route 53 charges the fee for transferring your domain before we start the transfer process\. If a transfer fails for some reason, we immediately credit your account for the cost of the transfer\.

**Special and premium domain names**  
TLD registries have assigned special or premium prices to some domain names\. You can't transfer a domain to Route 53 if the domain has a special or premium price\.

**Topics**
+ [Transfer requirements for top\-level domains](#domain-transfer-to-route-53-requirements)
+ [Step 1: Confirm that Amazon Route 53 supports the top\-level domain](#domain-transfer-to-route-53-confirm-tld)
+ [Step 2: Transfer your DNS service to Amazon Route 53 or another DNS service provider](#domain-transfer-to-route-53-transfer-dns)
+ [Step 3: Change settings with the current registrar](#domain-transfer-to-route-53-change-registrar-settings)
+ [Step 4: Get the names of your name servers](#domain-transfer-to-route-53-get-name-servers)
+ [Step 5: Request the transfer](#domain-transfer-to-route-53-request-transfer)
+ [Step 6: AISPL \(India\) customers only: Pay the transfer fee](#domain-transfer-to-route-53-aispl)
+ [Step 7: Click the link in the confirmation and authorization emails](#domain-transfer-to-route-53-authorize-transfer)
+ [Step 8: Update the domain configuration](#domain-transfer-to-route-53-change-configuration)

## Transfer requirements for top\-level domains<a name="domain-transfer-to-route-53-requirements"></a>

Most domain registrars enforce requirements on transferring a domain to another registrar\. The primary purpose of these requirements is to prevent the owners of fraudulent domains from repeatedly transferring the domains to different registrars\. Requirements vary, but the following requirements are typical: 
+ You must have either registered the domain with the current registrar or transferred registration for the domain to the current registrar at least 60 days ago\.
+ If the registration for a domain name expired and had to be restored, it must have been restored at least 60 days ago\.
+ The domain cannot have any of the following domain name status codes:
  + clientTransferProhibited
  + pendingDelete
  + pendingTransfer
  + redemptionPeriod
  + serverTransferProhibited
+ The registries for some top\-level domains don't allow transfers until changes are complete, such as changes to the domain owner\.

For a current list of domain name status codes and an explanation of what each code means, go to the [website for ICANN](https://www.icann.org/), and search for "EPP status codes"\. \(Search on the ICANN website; web searches sometimes return an old version of the document\.\)

**Note**  
ICANN is the organization that establishes policies governing registration and transfer of domain names\.

## Step 1: Confirm that Amazon Route 53 supports the top\-level domain<a name="domain-transfer-to-route-53-confirm-tld"></a>

See [Domains that you can register with Amazon Route 53](registrar-tld-list.md)\. If the top\-level domain for the domain that you want to transfer is on the list, you can transfer the domain to Amazon Route 53\. 

If a TLD is not on the list, you can't currently transfer the domain registration to Route 53\. We occasionally add support more TLDs to the list, so check back to see if we've added support for your domain\. You can also submit a request for support for your TLD on the [Route 53 Domain Registration](https://forums.aws.amazon.com/forum.jspa?forumID=214) forum\.

## Step 2: Transfer your DNS service to Amazon Route 53 or another DNS service provider<a name="domain-transfer-to-route-53-transfer-dns"></a>

If the registrar for your domain is also the DNS service provider for the domain, transfer your DNS service to Amazon Route 53 or another DNS service provider *before* you continue with the process to transfer the domain registration\.

**Why transfer DNS first?**

Some registrars provide free DNS service when you purchase a domain registration\. When you transfer the registration, the previous registrar will not renew your domain registration and might disable DNS service for the domain as soon as they receive a request from Route 53 to transfer the domain\. For more information, see [Making Amazon Route 53 the DNS service for an existing domainMaking Route 53 the DNS service for an existing domain](MigratingDNS.md)\.

**Important**  
If the registrar for your domain is also the DNS service provider for the domain and you don't transfer DNS service to another provider, your website, email, and the web applications associated with the domain might become unavailable\. 

**Transferring DNS service when you're using DNSSEC**

Route 53 supports DNSSEC for domain registration but does not support DNSSEC for DNS service\. If you want to continue using DNSSEC for the domain that you're transferring, you need to either choose a DNS service provider that does support DNSSEC or set up your own DNS server\. You can't transfer a domain registration while DNSSEC is configured, so don't configure DNSSEC with the new DNS service provider until after the transfer is complete\.

## Step 3: Change settings with the current registrar<a name="domain-transfer-to-route-53-change-registrar-settings"></a>

Using the method provided by your current registrar, perform the following tasks for each domain that you want to transfer\.
+ [Confirm that the email for the registrant contact for your domain is up to date](#domain-transfer-to-route-53-change-registrar-settings-email)
+ [Unlock the domain so it can be transferred](#domain-transfer-to-route-53-change-registrar-settings-unlock)
+ [Confirm that the domain status allows you to transfer the domain](#domain-transfer-to-route-53-change-registrar-settings-status)
+ [Disable DNSSEC for the domain](#domain-transfer-to-route-53-change-registrar-settings-dnssec)
+ [Get an authorization code](#domain-transfer-to-route-53-change-registrar-settings-code)
+ [Renew your domain registration before you transfer the domain (selected geographic TLDs)](#domain-transfer-to-route-53-change-registrar-settings-renew)

**Confirm that the email for the registrant contact for your domain is up to date**  
We'll send email to that email address to request authorization for the transfer\. You need to click a link in the email to authorize the transfer\. If you don't click the link, we must cancel the transfer\.

**Unlock the domain so it can be transferred**  
ICANN, the governing body for domain registrations, requires that you unlock your domain before you transfer it\.

**Confirm that the domain status allows you to transfer the domain**  
For more information, see [Transfer requirements for top\-level domains](#domain-transfer-to-route-53-requirements)\.

** Disable DNSSEC for the domain **  
Route 53 supports DNSSEC for domain registration, but not for DNS\. If you're using DNSSEC for the domain that you're transferring to Route 53, do one of the following:  
+ **If you're transferring DNS service to Route 53 or another provider that does not support DNSSEC** – Delete public keys for the domain\.
**Important**  
If you transfer a domain registration to Route 53 while DNSSEC is configured, the DNSSEC public keys are transferred, too\. If you transfer DNS service to Route 53 or another a provider that doesn't support DNSSEC, DNS resolution fails intermittently until you delete the DNSSEC keys from the domain\. For more information, see the troubleshooting topic [DNS resolution fails intermittently](troubleshooting-intermittent-dns-resolution-failure.md)\.
+ **If you're transferring DNS service to a provider that supports DNSSEC** – Configure DNSSEC with the new DNS service provider\. You don't need to delete public keys for the domain\.
+ **If you aren't transferring DNS service** – You don't need to delete public keys for the domain\.

**Get an authorization code**  
An authorization code from the current registrar authorizes us to request that registration for the domain be transferred to Route 53\. You'll enter this code in the Route 53 console later in the process\.  
Some top\-level domains have additional requirements:    
**\.co\.za domains**  
You don't need to get an authorization code to transfer a \.co\.za domain to Route 53\.  
**\.es domains**  
If you're transferring a \.es domain to Route 53, you don't need to get an authorization code\.  
**\.jp domains**  
If you're transferring a \.jp domain to Route 53, you don't need to get an authorization code\.  
**\.uk, \.co\.uk, \.me\.uk, and \.org\.uk domains**  
If you're transferring a \.uk, \.co\.uk, \.me\.uk, or \.org\.uk domain to Route 53, you don't need to get an authorization code\. Instead, use the method provided by your current domain registrar to update the value of the IPS tag for the domain to **GANDI**, all uppercase\. \(An IPS tag is required by Nominet, the registry for \.uk domain names\.\) If your registrar doesn't provide a way to change the value of the IPS tag, [contact Nominet](http://www.nominet.org.uk/uk-domain-names/manage-your-domain/change-registrar)\.  
Note the following about changing the IPS tag:    
**You must request the transfer within five days**  
If you don't request the transfer within five days after you change the IPS tag, the tag changes back to the previous value\. You must change the value of the IPS tag again, or the transfer request will fail\.   
**Viewing the IPS tag in WHOIS queries**  
The change to the IPS tag doesn't appear in WHOIS queries until after the transfer to Route 53 has completed\.   
**Email from Gandi**  
You might receive an email from our registrar associate, Gandi, about the transfer process\. If you receive an email from Gandi \(transfer\-auth@gandi\.net\) about transferring your domain, ignore the instructions in the email because they aren't relevant to Route 53\. Follow the instructions in this topic instead\.

**Renew your domain registration before you transfer the domain \(selected geographic TLDs\)**  
For most TLDs, when you transfer a domain, the registration is automatically extended by one year\. However, for some geographic TLDs, registration is not extended when you transfer the domain\. If you're transferring a domain to Route 53 that has one of these TLDs, we recommend that you renew the domain registration before you transfer the domain, especially if the expiration date is approaching\.  
If you don't renew the domain before you transfer it, the registration could expire before the transfer is complete\. If this happens, the domain becomes unavailable on the internet, and the domain name could become available for others to purchase\.
Registration is not automatically extended when you transfer the following domains to another registrar:  
+ \.ac \(Ascension Island\)
+ \.ch \(Switzerland\)
+ \.co\.uk \(United Kingdom\)
+ \.co\.za \(South Africa\)
+ \.com\.au \(Australia\)
+ \.es \(Spain\)
+ \.fi \(Finland\)
+ \.im \(Isle of Man\)
+ \.jp \(Japan\)
+ \.me\.uk \(United Kingdom\)
+ \.net\.au \(Australia\)
+ \.org\.uk \(United Kingdom\)
+ \.se \(Sweden\)
+ \.sh \(Saint Helena\)
+ \.uk \(United Kingdom\)

## Step 4: Get the names of your name servers<a name="domain-transfer-to-route-53-get-name-servers"></a>

If you're using Amazon Route 53 as your DNS service or you're continuing to use the existing DNS service, we'll get the names of the name servers for you automatically later in the process\. Skip to [Step 5: Request the transfer](#domain-transfer-to-route-53-request-transfer)\.

If you want to change the DNS service to a provider other than Route 53 at the same time that you're transferring the domain to Route 53, use the procedure provided by the DNS service provider to get the names of the name servers for each domain that you want to transfer\.

**Important**  
If the registrar for your domain is also the DNS service provider for the domain, transfer your DNS service to Route 53 or another DNS service provider *before* you continue with the process to transfer the domain registration\.   
If you transfer DNS service at the same time that you transfer domain registration, your website, email, and the web applications associated with the domain might become unavailable\. For more information, see [Step 2: Transfer your DNS service to Amazon Route 53 or another DNS service provider](#domain-transfer-to-route-53-transfer-dns)\.

## Step 5: Request the transfer<a name="domain-transfer-to-route-53-request-transfer"></a>

To transfer domain registration from the current registrar to Amazon Route 53, use the Route 53 console to request the transfer\. Route 53 handles the communication with the current registrar for the domain\.

The procedure that you use depends on whether you want to transfer up to five domains or more than five domains:
+ [To transfer domain registration to Route 53 for up to five domains](#domain-transfer-to-route-53-up-to-five-procedure)
+ [To transfer domain registration to Route 53 for more than five domains](#domain-transfer-to-route-53-more-than-five-procedure)

**Important**  
If you use the procedure to transfer more than five domains, Route 53 automatically configures the transferred domains to use the current DNS service for all the domains that you're transferring\. If the registrar for your domain is also the DNS service provider for the domain and you don't transfer DNS service to another provider, your website, email, and the web applications associated with the domain might become unavailable\. For more information, see [Step 2: Transfer your DNS service to Amazon Route 53 or another DNS service provider](#domain-transfer-to-route-53-transfer-dns)\.<a name="domain-transfer-to-route-53-up-to-five-procedure"></a>

**To transfer domain registration to Route 53 for up to five domains**

1. Open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Registered Domains**\.

1. Choose **Transfer Domain**\.

1. Enter the name of the domain for which you want to transfer registration to Route 53, and choose **Check**\.

1. If the domain registration is available for transfer, choose **Add to cart**\.

   If the domain registration is not available for transfer, the Route 53 console lists the reasons\. Contact your registrar for information about how to resolve the issues that prevent you from transferring the registration\.

1. If you want to transfer other domain registrations, repeat steps 4 and 5\. 

1. When you've added all the domain registrations that you want to transfer, choose **Continue**\.

1. For each domain name that you want to transfer, enter the applicable values:  
**Authorization code**  
Enter the authorization code that you got from your current registrar in [Step 3: Change settings with the current registrar](#domain-transfer-to-route-53-change-registrar-settings)\.  
You don't need to enter an authorization code to transfer a \.co\.za, \.es, \.jp, \.uk, \.co\.uk, \.me\.uk, or \.org\.uk domain to Route 53\.  
**Name server options**  
Choose the applicable option:  
   + **Continue to use the name servers provided by the current registrar or DNS service** – If the current registrar for the domain is currently providing DNS service, we recommend that you transfer DNS service to another DNS service provider before you transfer the domain\. 
**Important**  
Some registrars stop providing DNS service as soon as you request a transfer to another registrar\. If the current registrar disables DNS service, your domain will become unavailable on the internet\.
   + **Import name servers from a Route 53 hosted zone that has the same name as the domain** – When you select this option, the console displays a list of the hosted zones that have the same name as the domain\. Choose the hosted zone that you want to use for routing traffic for the domain\.
   + **Specify new name servers to replace the current registrar's name servers \(not recommended\)** – If you're using a DNS service other than Route 53 for this domain, enter the names of the name servers that you got in [Step 4: Get the names of your name servers](#domain-transfer-to-route-53-get-name-servers)\. 
**Important**  
We don't recommend choosing this option because transferring DNS service from one DNS service provider to another can take up to two days\. The current registrar might stop providing DNS service as soon as you request a transfer to another registrar\. If the current registrar disables DNS service, your domain will become unavailable on the internet until the change to another DNS service provider takes effect\.  
**Name servers**  
If you chose the option **Specify new name servers to replace the current registrar's name servers**, enter the names of the name servers that you got from the DNS service for the domain in [Step 4: Get the names of your name servers](#domain-transfer-to-route-53-get-name-servers)\. By default, the **Name server** fields display the names of the current name servers for the domain\.  
**Glue records**  
If the name of a name server is a subdomain of the domain that you're transferring \(such as ns1\.example\.com in the domain example\.com\), enter one or more IP addresses for each name server\. You can enter addresses in IPv4 or IPv6 format\. If a name server has multiple IP addresses, enter each address on a separate line\.

1. On the **Contact Details for Your** *n* **Domains** page, enter contact information for the domain registrant, administrator, and technical contact\. The values that you enter here are applied to all the domains that you're transferring\. 
**Important**  
We recommend that you specify the following values for the registrant contact \(the domain owner\):  
**First and last name**: We recommend that you specify the name that appears on your official ID\. For some changes to domain settings, some domain registries require that you provide proof of identity\. The name on your ID must match the name of the registrant contact for the domain\.
**Contact details**: During the domain transfer, we recommend that you specify the same values as are specified with the current registrar\. When you change contact details for the registrant contact, you change the domain owner, and some TLD registries don't allow you to change the domain owner during a domain transfer\. If you change contact details for the registrant contact, the transfer might fail\. You can change contact details for the registrant contact after you transfer the domain\.

   By default, we use the same information for all three contacts\. If you want to enter different information for one or more contacts, change the value of **My Registrant, Administrative, and Technical contacts are all the same** to **No**\.
**Note**  
For \.it domains, the registrant and administrative contacts must be the same\.

   For more information, see [Values that you specify when you register or transfer a domain](domain-register-values-specify.md)\.

1. For some TLDs, we're required to collect additional information\. For these TLDs, enter the applicable values after the **Postal/Zip Code** field\.

1. If the value of **Contact Type** is **Person**, choose whether you want to hide your contact information from WHOIS queries\. For more information, see [Enabling or disabling privacy protection for contact information for a domain](domain-privacy-protection.md)\.

1. Choose **Continue**\.

1. Choose whether you want us to automatically renew your domain registration before the expiration date\.
**Note**  
Domain name registrations and renewals are not refundable\. If you enable automatic domain renewal and you decide that you don't want the domain name after we renew the registration, you can't get a refund for the cost of the renewal\.

1. Review the information you entered, read the terms of service, and select the check box to confirm that you've read the terms of service\. 

1. Choose **Complete Purchase**\. 

   We confirm that the domain is eligible for transfer, and we send an email to the registrant contact for the domain to request authorization to transfer the domain\. <a name="domain-transfer-to-route-53-more-than-five-procedure"></a>

**To transfer domain registration to Route 53 for more than five domains**

1. Open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Registered Domains**\.

1. Choose **Transfer Domain**\.

1. On the **Transfer domain to Route 53** page, choose **Transfer multiple domains to Route 53**\.

1. For each domain that you want to transfer, enter the domain name and the authorization code in the following format\. Note the comma between the domain name and the authorization code:

   ```
   domain-name-1,authorization-code-1
   domain-name-2,authorization-code-2
   ```

   If an authorization code isn't required for a domain, omit the comma, too:

   ```
   domain-name-3
   ```
**Note**  
You don't need to enter an authorization code to transfer a \.co\.za, \.es, \.jp, \.uk, \.co\.uk, \.me\.uk, or \.org\.ukdomain to Route 53\.

1. When you've entered all the domains that you want to transfer, choose **Continue**\.

1. The **Check domain transferability** page lists the domains that you entered on the previous page and whether each domain can be transferred\. You have the following options:  
**If all domains are transferable**  
Choose **Add transferable domains to cart**\.  
**If one or more domains are untransferable and you want to transfer them**  
Review [Transfer requirements for top\-level domains](#domain-transfer-to-route-53-requirements) to confirm that each untransferable domain meets the transfer requirements\. If you don't find any obvious problems, contact the current registrar to determine why the domain can't be transferred to Route 53\.  
After you make any changes so that domains are transferable \(for example, disabling the transfer lock\), choose **Check transferability**, and Route 53 will repeat the transferability check\.  
**If one or more domains are untransferable and you don't want to transfer them**  
Choose **Add transferable domains to cart**\.

1. Choose **Continue**\.

1. On the **Contact Details for Your** *n* **Domains** page, enter contact information for the domain registrant, administrator, and technical contact\. The values that you enter here are applied to all the domains that you're transferring\. 
**Important**  
We recommend that you specify the following values for the registrant contact \(the domain owner\):  
**First and last name**: We recommend that you specify the name that appears on your official ID\. For some changes to domain settings, some domain registries require that you provide proof of identity\. The name on your ID must match the name of the registrant contact for the domain\.
**Contact details**: During the domain transfer, we recommend that you specify the same values as are specified with the current registrar\. When you change contact details for the registrant contact, you change the domain owner, and some TLD registries don't allow you to change the domain owner during a domain transfer\. If you change contact details for the registrant contact, the transfer might fail\. You can change contact details for the registrant contact after you transfer the domain\.

   By default, we use the same information for all three contacts\. If you want to enter different information for one or more contacts, change the value of **My Registrant, Administrative, and Technical contacts are all the same** to **No**\.

   For more information, see [Values that you specify when you register or transfer a domain](domain-register-values-specify.md)\.

1. For some TLDs, we're required to collect additional information\. For these TLDs, enter the applicable values after the **Postal/Zip Code** field\.

1. If the value of **Contact Type** is **Person**, choose whether you want to hide your contact information from WHOIS queries\. For more information, see [Enabling or disabling privacy protection for contact information for a domain](domain-privacy-protection.md)\.

1. Choose **Continue**\.

1. Choose whether you want us to automatically renew your domain registration before the expiration date\.
**Note**  
Domain name registrations and renewals are not refundable\. If you enable automatic domain renewal and you decide that you don't want the domain name after we renew the registration, you can't get a refund for the cost of the renewal\.

1. Review the information you entered, read the terms of service, and select the check box to confirm that you've read the terms of service\. 

1. Choose **Complete Purchase**\. 

   We confirm that the domain is eligible for transfer, and we send an email to the registrant contact for the domain to request authorization to transfer the domain\. 

## Step 6: AISPL \(India\) customers only: Pay the transfer fee<a name="domain-transfer-to-route-53-aispl"></a>

If your contact address is in India, your user agreement is with Amazon Internet Services Pvt\. Ltd \(AISPL\), a local AWS seller in India\. To transfer a domain to Route 53, perform the following procedure to pay the fee for transferring your domain\. <a name="domain-transfer-to-route-53-aispl-procedure"></a>

**To pay the transfer fee**

1. Go to the [Orders and Invoices](https://console.aws.amazon.com/billing/home#/paymenthistory) page in the AWS Management Console\.

1. In the **Payments Due** section, find the applicable invoice\.

1. In the **Actions** column, choose **Verify and Pay**\.

   After you pay the invoice, we complete the domain transfer and send the applicable emails\.

**Important**  
If you don't pay the invoice within five days, the invoice is canceled\. To transfer a domain after an invoice is canceled, resubmit the request\.

For more information, see [Managing your payments in India](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/edit-aispl-payment-method.html) in the *AWS Billing and Cost Management User Guide*\.

## Step 7: Click the link in the confirmation and authorization emails<a name="domain-transfer-to-route-53-authorize-transfer"></a>

Soon after you request the transfer, we might send one or more emails to the registrant contact for the domain:

**Email to confirm that the registrant contact is reachable**  
If you've never registered a domain with Route 53 or transferred a domain to Route 53, we send you an email that asks you to confirm that the email address is valid\. We retain this information so we don't have to send this confirmation email again\.

**Email to get authorization to transfer the domain**  
For some TLDs, you need to respond to an email to authorize transfer of the domain\.    
**Generic TLDs such as \.com, \.net, and \.org**  
Authorization isn't required for domains that have a [generic TLD](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/registrar-tld-list.html#registrar-tld-list-generic), such as \.com, \.net, or \.org\.  
**Geographic TLDs such as \.co\.uk and \.jp**  
For domains that have a [geographic TLD](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/registrar-tld-list.html#registrar-tld-list-geographic), we're required to get your authorization to transfer the domain\. If you transfer 10 domains, we have to send you 10 emails, and you have to click the authorization link in each one\.

The emails all go to the registrant contact for the domain:
+ If you're the registrant contact for the domain, follow the instructions in the email to authorize the transfer\.
+ If someone else is the registrant contact, ask that person to follow the instructions in the email to authorize the transfer\.

**Important**  
If you're transferring a domain that has a geographic TLD, we wait up to five days for the registrant contact to authorize the transfer\. If the registrant contact doesn't respond within five days, we cancel the transfer operation and send an email to the registrant contact about the cancellation\. 

**Topics**
+ [Authorization email for a new owner or email address](#domain-transfer-to-route-53-authorize-transfer-additional-email)
+ [Email addresses that authorization emails come from](#domain-transfer-to-route-53-authorize-transfer-email-addresses)
+ [Approval from the current registrar](#domain-transfer-to-route-53-authorize-transfer-registrar-approval)
+ [What happens next](#domain-transfer-to-route-53-authorize-transfer-what-next)

### Authorization email for a new owner or email address<a name="domain-transfer-to-route-53-authorize-transfer-additional-email"></a>

If you changed the following values, we send you a separate email that asks for your authorization:

**Domain owner**  
If you change the owner of the domain, as described in [Who is the owner of a domain?](domain-update-contacts.md#domain-update-contacts-who-is-domain-owner), we send email to the registrant contact for the domain\.

**Email address for the registrant contact \(only for some TLDs\)**  
For some TLDs, if you change the email address for the registrant contact, we send an email to the old and the new email address for the registrant contact\. Someone at both email addresses must follow the instructions in the email to authorize the change\.

For changes to the domain owner or the email address for the registrant contact, if we don't receive authorization for the change within 3 to 15 days, depending on the top\-level domain, we must cancel the request as required by ICANN\.

### Email addresses that authorization emails come from<a name="domain-transfer-to-route-53-authorize-transfer-email-addresses"></a>

All email comes from one of the following email addresses\.


****  

| TLDs | Email address that authorization email comes from | 
| --- | --- | 
| \.com\.au and \.net\.au |  no\-reply@ispapi\.net The email contains a link to http://transfers\.ispapi\.net\.  | 
| \.fr |  nic@nic\.fr, if you're changing the registrant contact for a \.fr domain name at the same time that you're transferring the domain\. \(The email is sent both to the current registrant contact and the new registrant contact\.\)  | 
| All others |  One of the following email addresses: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/domain-transfer-to-route-53.html)  | 

To determine who the registrar is for your TLD, see [Domains that you can register with Amazon Route 53](registrar-tld-list.md)\.

### Approval from the current registrar<a name="domain-transfer-to-route-53-authorize-transfer-registrar-approval"></a>

If the registrant contact authorizes the transfer, we start to work with your current registrar to transfer your domain\. This step might take up to ten days, depending on the TLD for your domain:
+ [Generic top\-level domains](registrar-tld-list-generic.md) – take up to seven days
+ [Geographic top\-level domains](registrar-tld-list-geographic.md) \(also known as country code top\-level domains\) – take up to ten days

If your current registrar doesn't reply to our transfer request, which is common among registrars, the transfer happens automatically\. If your current registrar rejects the transfer request, we send an email notification to the current registrant contact\. The registrant needs to contact the current registrar and resolve the issues with the transfer\.

### What happens next<a name="domain-transfer-to-route-53-authorize-transfer-what-next"></a>

When your domain transfer has been approved, we send another email to the registrant contact\. For more information about the process, see [Viewing the status of a domain transfer](domain-transfer-to-route-53-status.md)\.

We charge your AWS account for the domain transfer as soon as the transfer is complete\. For a list of charges by TLD, see [Amazon Route 53 Pricing for Domain Registration](https://d32ze2gidvkk54.cloudfront.net/Amazon_Route_53_Domain_Registration_Pricing_20140731.pdf)\.

**Note**  
This is a one\-time charge, so the charge doesn't appear in your CloudWatch billing metrics\. For more information about CloudWatch metrics, see [Using Amazon CloudWatch metrics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/working_with_metrics.html) in the *Amazon CloudWatch User Guide*\.

## Step 8: Update the domain configuration<a name="domain-transfer-to-route-53-change-configuration"></a>

After the transfer is complete, you can optionally change the following settings:

**Transfer lock**  
To transfer the domain to Route 53, you had to disable the transfer lock\. If you want to re\-enable the lock to prevent unauthorized transfers, see [Locking a domain to prevent unauthorized transfer to another registrar](domain-lock.md)\.

**Automatic renewal**  
We configure the transferred domain to automatically renew as the expiration date approaches\. For information about how to change this setting, see [Enabling or disabling automatic renewal for a domain](domain-enable-disable-auto-renewal.md)\.

**Extended registration period**  
By default, Route 53 renews the domain annually\. If you want to register the domain for a longer period, see [Extending the registration period for a domain](domain-extend.md)\.

**DNSSEC**  
For information about configuring DNSSEC for the domain, see [Configuring DNSSEC for a domain](domain-configure-dnssec.md)\.