# Transferring Registration for a Domain to Amazon Route 53<a name="domain-transfer-to-route-53"></a>

To transfer the registration for a domain to Amazon Route 53, carefully follow the procedures in this topic\. 

**Important**  
If you skip a step, your domain might become unavailable on the internet\.

Note the following:

**Expiration date**  
For information about how transferring your domain affects the current expiration date, see [How Transferring a Domain to Amazon Route 53 Affects the Expiration Date for Your Domain Registration](domain-transfer-to-route-53-expiration.md)\.

**Transfer fee**  
When you transfer a domain to Route 53, the transfer fee that we apply to your AWS account depends on the top\-level domain, such as \.com or \.org\. For more information, see [Route 53 Pricing](https://aws.amazon.com/route53/pricing/)\.   
You can't use AWS credits to pay the fee, if any, for transferring a domain to Route 53\.

**Special and premium domain names**  
TLD registries have assigned special or premium prices to some domain names\. You can't use transfer a domain to Route 53 if the domain has a special or premium price\.


+ [Transfer Requirements for Top\-Level Domains](#domain-transfer-to-route-53-requirements)
+ [Step 1: Confirm that Amazon Route 53 Supports the Top\-Level Domain](#domain-transfer-to-route-53-confirm-tld)
+ [Step 2: Transfer Your DNS Service to Amazon Route 53 or Another DNS Service Provider](#domain-transfer-to-route-53-transfer-dns)
+ [Step 3: Change Settings with the Current Registrar](#domain-transfer-to-route-53-change-registrar-settings)
+ [Step 4: Get the Names of Your Name Servers](#domain-transfer-to-route-53-get-name-servers)
+ [Step 5: Request the Transfer](#domain-transfer-to-route-53-request-transfer)
+ [Step 6: Click the Link in the Confirmation and Authorization Emails](#domain-transfer-to-route-53-authorize-transfer)
+ [Step 7: Update the Domain Configuration](#domain-transfer-to-route-53-change-configuration)

## Transfer Requirements for Top\-Level Domains<a name="domain-transfer-to-route-53-requirements"></a>

Registries for top\-level domains \(TLDs\), such as \.com or \.org, have requirements for transferring domains\. Requirements vary among TLDs, but the following requirements are typical:

+ The domain must have been registered with the current registrar at least 60 days ago\.

+ If the registration for a domain name expired and had to be restored, it must have been restored at least 60 days ago\.

+ If registration for the domain was transferred, the transfer to the current registrar must have been at least 60 days ago\.

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

## Step 1: Confirm that Amazon Route 53 Supports the Top\-Level Domain<a name="domain-transfer-to-route-53-confirm-tld"></a>

See [Domains That You Can Register with Amazon Route 53](registrar-tld-list.md)\. If the top\-level domain for the domain that you want to transfer is on the list, you can transfer the domain to Amazon Route 53\. 

If a TLD is not on the list, you can't currently transfer the domain registration to Route 53\. We occasionally add support more TLDs to the list, so check back to see if we've added support for your domain\. You can also submit a request for support for your TLD on the [Route 53 Domain Registration](https://forums.aws.amazon.com/forum.jspa?forumID=214) forum\.

## Step 2: Transfer Your DNS Service to Amazon Route 53 or Another DNS Service Provider<a name="domain-transfer-to-route-53-transfer-dns"></a>

If the registrar for your domain is also the DNS service provider for the domain, transfer your DNS service to Amazon Route 53 or another DNS service provider *before* you continue with the process to transfer the domain registration\.

**Why transfer DNS first?**

Some registrars provide free DNS service when you purchase a domain registration\. When you transfer the registration, the previous registrar will not renew your domain registration and might disable DNS service for the domain as soon as they receive a request from Route 53 to transfer the domain\. For more information, see [Making Amazon Route 53 the DNS Service for an Existing DomainMaking Route 53 the DNS Service for an Existing Domain](MigratingDNS.md)\.

**Important**  
If the registrar for your domain is also the DNS service provider for the domain and you don't transfer DNS service to another provider, your website, email, and the web applications associated with the domain might become unavailable\. 

**Transferring DNS service when you're using DNSSEC**

Route 53 supports DNSSEC for domain registration but does not support DNSSEC for DNS service\. If you want to continue using DNSSEC for the domain that you're transferring, you need to choose a DNS service provider that does support DNSSEC\. You can't transfer a domain registration while DNSSEC is configured, so don't configure DNSSEC with the new DNS service provider until after the transfer is complete\.

## Step 3: Change Settings with the Current Registrar<a name="domain-transfer-to-route-53-change-registrar-settings"></a>

Using the method provided by your current registrar, perform the following tasks for each domain that you want to transfer:

**Confirm that the email for the registrant contact for your domain is up to date**  
We'll send email to that email address to request authorization for the transfer\. You need to click a link in the email to authorize the transfer\. If you don't click the link, we must cancel the transfer\.

**Unlock the domain so it can be transferred**  
ICANN, the governing body for domain registrations, requires that you unlock your domain before you transfer it\.

**Confirm that the domain status allows you to transfer the domain**  
For more information, see [Transfer Requirements for Top\-Level Domains](#domain-transfer-to-route-53-requirements)\.

**Disable DNSSEC for the domain**  
If you're transferring DNS service to another provider and you're using DNSSEC, you need to either delete public keys for the domain or configure DNSSEC with the new provider:  

+ **If you're transferring DNS service to a provider that does not support DNSSEC** – Delete public keys for the domain\.

+ **If you're transferring DNS service to a provider that supports DNSSEC** – Configure DNSSEC with the new DNS service provider\. You don't need to delete public keys for the domain\.

+ **If you aren't transferring DNS service** – You don't need to delete public keys for the domain\.

**Get an authorization code**  
An authorization code from the current registrar authorizes us to request that registration for the domain be transferred to Route 53\. You'll enter this code in the Route 53 console later in the process\.  
Some top\-level domains have additional requirements:    
**\.uk, \.co\.uk, \.me\.uk, and \.org\.uk domains**  
If you're transferring a \.uk, \.co\.uk, \.me\.uk, or \.org\.uk domain to Route 53, you don't need to get an authorization code\. Instead, use the method provided by your current domain registrar to update the value of the IPS tag for the domain to **GANDI**, all uppercase\. \(An IPS tag is required by Nominet, the registry for \.uk domain names\.\) If your registrar will not change the value of the IPS tag, [contact Nominet](http://www.nominet.org.uk/uk-domain-names/manage-your-domain/change-registrar)\.  
**\.jp domains**  
If you're transferring a \.jp domain to Route 53, you don't need to get an authorization code\. Instead, use the method provided by your current domain registrar to update the value of the AGNT code to **AGNT\-1744**, all uppercase\. 

## Step 4: Get the Names of Your Name Servers<a name="domain-transfer-to-route-53-get-name-servers"></a>

If you're using Amazon Route 53 as your DNS service or you're continuing to use the existing DNS service, we'll get the names of the name servers for you automatically later in the process\. Skip to [Step 5: Request the Transfer](#domain-transfer-to-route-53-request-transfer)\.

If you want to change the DNS service to a provider other than Route 53 at the same time that you're transferring the domain to Route 53, use the procedure provided by the DNS service provider to get the names of the name servers for each domain that you want to transfer\.

**Important**  
If the registrar for your domain is also the DNS service provider for the domain, transfer your DNS service to Route 53 or another DNS service provider *before* you continue with the process to transfer the domain registration\.   
If you transfer DNS service at the same time that you transfer domain registration, your website, email, and the web applications associated with the domain might become unavailable\. For more information, see [Step 2: Transfer Your DNS Service to Amazon Route 53 or Another DNS Service Provider](#domain-transfer-to-route-53-transfer-dns)\.

## Step 5: Request the Transfer<a name="domain-transfer-to-route-53-request-transfer"></a>

To transfer domain registration from the current registrar to Amazon Route 53, use the Route 53 console to request the transfer\. Route 53 handles the communication with the current registrar for the domain\.

The procedure that you use depends on whether you want to transfer up to five domains or more than five domains:

+ [To transfer domain registration to Route 53 for up to five domains](#domain-transfer-to-route-53-up-to-five-procedure)

+ [To transfer domain registration to Route 53 for more than five domains](#domain-transfer-to-route-53-more-than-five-procedure)

**Important**  
If you use the procedure to transfer more than five domains, Route 53 automatically configures the transferred domains to use the current DNS service for all the domains that you're transferring\. If the registrar for your domain is also the DNS service provider for the domain and you don't transfer DNS service to another provider, your website, email, and the web applications associated with the domain might become unavailable\. For more information, see [Step 2: Transfer Your DNS Service to Amazon Route 53 or Another DNS Service Provider](#domain-transfer-to-route-53-transfer-dns)\.

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
Enter the authorization code that you got from your current registrar in [Step 3: Change Settings with the Current Registrar](#domain-transfer-to-route-53-change-registrar-settings)\.  
**Name server options**  
Choose the applicable option:  

   + **Continue to use the name servers provided by the current registrar or DNS service** – If the current registrar for the domain is currently providing DNS service, we recommend that you transfer DNS service to another DNS service provider before you transfer the domain\. 
**Important**  
Some registrars stop providing DNS service as soon as you request a transfer to another registrar\. If the current registrar disables DNS service, your domain will become unavailable on the internet\.

   + **Import name servers from a Route 53 hosted zone that has the same name as the domain** – When you select this option, the console displays a list of the hosted zones that have the same name as the domain\. Choose the hosted zone that you want to use for routing traffic for the domain\.

   + **Specify new name servers to replace the current registrar's name servers \(not recommended\)** – If you're using a DNS service other than Route 53 for this domain, type the names of the name servers that you got in [Step 4: Get the Names of Your Name Servers](#domain-transfer-to-route-53-get-name-servers)\. 
**Important**  
We don't recommend choosing this option because transferring DNS service from one DNS service provider to another can take up to two days\. The current registrar might stop providing DNS service as soon as you request a transfer to another registrar\. If the current registrar disables DNS service, your domain will become unavailable on the internet until the change to another DNS service provider takes effect\.  
**Name servers**  
If you chose the option **Specify new name servers to replace the current registrar's name servers**, type the names of the name servers that you got from the DNS service for the domain in [Step 4: Get the Names of Your Name Servers](#domain-transfer-to-route-53-get-name-servers)\. By default, the **Name server** fields display the names of the current name servers for the domain\.  
**Glue records**  
If the name of a name server is a subdomain of the domain that you're transferring \(such as ns1\.example\.com in the domain example\.com\), enter one or more IP addresses for each name server\. You can enter addresses in IPv4 or IPv6 format\. If a name server has multiple IP addresses, type each address on a separate line\.

1. On the **Contact Details for Your** *n* **Domains** page, enter contact information for the domain registrant, administrator, and technical contact\. The values that you enter here are applied to all the domains that you're transferring\. 
**Important**  
For **First Name** and **Last Name**, we recommend that you specify the name on your official ID\. For some changes to domain settings, some domain registries require that you provide proof of identity\. The name on your ID must match the name of the registrant contact for the domain\.

   By default, we use the same information for all three contacts\. If you want to enter different information for one or more contacts, change the value of **My Registrant, Administrative, and Technical contacts are all the same** to **No**\.
**Note**  
For \.it domains, the registrant and administrative contacts must be the same\.

   For more information, see [Values that You Specify When You Register a Domain](domain-register-values-specify.md)\.

1. For some TLDs, we're required to collect additional information\. For these TLDs, enter the applicable values after the **Postal/Zip Code** field\.

1. If the value of **Contact Type** is **Person**, choose whether you want to hide your contact information from WHOIS queries\. For more information, see [Enabling or Disabling Privacy Protection for Contact Information for a Domain](domain-privacy-protection.md)\.

1. Choose **Continue**\.

1. Review the information you entered, read the terms of service, and select the check box to confirm that you've read the terms of service\. 

1. Choose **Complete Purchase**\. 

   We confirm that the domain is eligible for transfer, and we send an email to the registrant contact for the domain to request authorization to transfer the domain\. 

**To transfer domain registration to Route 53 for more than five domains**

1. Open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Registered Domains**\.

1. Choose **Transfer Domain**\.

1. On the **Transfer domain to Route 53** page, choose **Transfer multiple domains to Route 53**\.

1. For each domain that you want to transfer, type the domain name and the authorization code in the following format\. Note the comma between the domain name and the authorization code:

   ```
   domain-name-1,authorization-code-1
   domain-name-2,authorization-code-2
   ```

   If an authorization code isn't required for a domain, omit the comma, too:

   ```
   domain-name-3
   ```

1. When you've entered all the domains that you want to transfer, choose **Continue**\.

1. The **Check domain transferability** page lists the domains that you entered on the previous page and whether each domain can be transferred\. You have the following options:  
**If all domains are transferable**  
Choose **Add transferable domains to cart**\.  
**If one or more domains are untransferable and you want to transfer them**  
Review [Transfer Requirements for Top\-Level Domains](#domain-transfer-to-route-53-requirements) to confirm that each untransferable domain meets the transfer requirements\. If you don't find any obvious problems, contact the current registrar to determine why the domain can't be transferred to Route 53\.  
After you make any changes so that domains are transferable \(for example, disabling privacy protection\), choose **Check transferability**, and Route 53 will repeat the transferability check\.  
**If one or more domains are untransferable and you don't want to transfer them**  
Choose **Add transferable domains to cart**\.

1. Choose **Continue**\.

1. On the **Contact Details for Your** *n* **Domains** page, enter contact information for the domain registrant, administrator, and technical contact\. The values that you enter here are applied to all the domains that you're transferring\. 

   By default, we use the same information for all three contacts\. If you want to enter different information for one or more contacts, change the value of **My Registrant, Administrative, and Technical contacts are all the same** to **No**\.

   For more information, see [Values that You Specify When You Register a Domain](domain-register-values-specify.md)\.

1. For some TLDs, we're required to collect additional information\. For these TLDs, enter the applicable values after the **Postal/Zip Code** field\.

1. If the value of **Contact Type** is **Person**, choose whether you want to hide your contact information from WHOIS queries\. For more information, see [Enabling or Disabling Privacy Protection for Contact Information for a Domain](domain-privacy-protection.md)\.

1. Choose **Continue**\.

1. Review the information you entered, read the terms of service, and select the check box to confirm that you've read the terms of service\. 

1. Choose **Complete Purchase**\. 

   We confirm that the domain is eligible for transfer, and we send an email to the registrant contact for the domain to request authorization to transfer the domain\. 

## Step 6: Click the Link in the Confirmation and Authorization Emails<a name="domain-transfer-to-route-53-authorize-transfer"></a>

Soon after you request the transfer, we send one or more emails to the registrant contact for the domain:

**Email to confirm that the registrant contact is reachable**  
If you've never registered a domain with Route 53 or transferred a domain to Route 53, we send you an email that asks you to confirm that the email address is valid\. We retain this information so we don't have to send this confirmation email again\.

**Email to get authorization to transfer the domain**  
If we can access your email address in the public WHOIS database, we're required to get your authorization to transfer the domain\. If you transfer 10 domains, we have to send you 10 emails, and you have to click the authorization link in each one\. If we can't access your email address by submitting a public WHOIS query, the transfer proceeds without this authorization\.

The emails all go to the registrant contact for the domain:

+ If you're the registrant contact for the domain, follow the instructions in the email to authorize the transfer\.

+ If someone else is the registrant contact, ask that person to follow the instructions in the email to authorize the transfer\.

**Important**  
We wait up to five days for the registrant contact to authorize the transfer\. If the registrant contact doesn't respond within five days, we cancel the transfer operation and send an email to the registrant contact about the cancellation\. 


+ [Authorization Email for a New Owner or Email Address](#domain-transfer-to-route-53-authorize-transfer-additional-email)
+ [Email Addresses that Authorization Emails Come From](#domain-transfer-to-route-53-authorize-transfer-email-addresses)
+ [Approval from the Current Registrar](#domain-transfer-to-route-53-authorize-transfer-registrar-approval)
+ [What Happens Next](#domain-transfer-to-route-53-authorize-transfer-what-next)

### Authorization Email for a New Owner or Email Address<a name="domain-transfer-to-route-53-authorize-transfer-additional-email"></a>

If you changed the following values, we send you a separate email that asks for your authorization:

**Domain owner**  
If you change the owner of the domain, as described in [Who Is the Owner of a Domain?](domain-update-contacts.md#domain-update-contacts-who-is-domain-owner), we send email to the registrant contact for the domain\.

**Email address for the registrant contact \(only for some TLDs\)**  
For some TLDs, if you change the email address for the registrant contact, we send an email to the old and the new email address for the registrant contact\. Someone at both email addresses must follow the instructions in the email to authorize the change\.

**Important**  
If you get an authorization email at your new email address and you don't have access to the old email address, open a support case\. For more information, see [Updating the Email Address for a Domain When You Can't Access Email at the Old Address](domain-update-contacts.md#domain-update-contacts-change-email-form)\.

For changes to the domain owner or the email address for the registrant contact, if we don't receive authorization for the change within 3 to 15 days, depending on the top\-level domain, we must cancel the request as required by ICANN\.

### Email Addresses that Authorization Emails Come From<a name="domain-transfer-to-route-53-authorize-transfer-email-addresses"></a>

All email comes from one of the following email addresses\.


****  

| TLDs | Email Address That Authorization Email Comes From | 
| --- | --- | 
| \.com\.au and \.net\.au |  no\-reply@ispapi\.net The email contains a link to http://transfers\.ispapi\.net\.  | 
| \.fr |  nic@nic\.fr, if you're changing the registrant contact for a \.fr domain name at the same time that you're transferring the domain\. \(The email is sent both to the current registrant contact and the new registrant contact\.\)  | 
| All others |  One of the following email addresses: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/domain-transfer-to-route-53.html)  | 

To determine who the registrar is for your TLD, see [Domains That You Can Register with Amazon Route 53](registrar-tld-list.md)\.

### Approval from the Current Registrar<a name="domain-transfer-to-route-53-authorize-transfer-registrar-approval"></a>

If the registrant contact authorizes the transfer, we start to work with your current registrar to transfer your domain\. This step might take up to ten days, depending on the TLD for your domain:

+ [Generic Top\-Level Domains](registrar-tld-list.md#registrar-tld-list-generic) – take up to seven days

+ [Geographic Top\-Level Domains](registrar-tld-list.md#registrar-tld-list-geographic) \(also known as country code top\-level domains\) – take up to ten days

If your current registrar doesn't reply to our transfer request, which is common among registrars, the transfer happens automatically\. If your current registrar rejects the transfer request, we send an email notification to the current registrant contact\. The registrant needs to contact the current registrar and resolve the issues with the transfer\.

### What Happens Next<a name="domain-transfer-to-route-53-authorize-transfer-what-next"></a>

When your domain transfer has been approved, we send another email to the registrant contact\. For more information about the process, see [Viewing the Status of a Domain Transfer](domain-transfer-to-route-53-status.md)\.

We charge your AWS account for the domain transfer as soon as the transfer is complete\. For a list of charges by TLD, see [Amazon Route 53 Pricing for Domain Registration](https://d32ze2gidvkk54.cloudfront.net/Amazon_Route_53_Domain_Registration_Pricing_20140731.pdf)\.

**Note**  
This is a one\-time charge, so the charge doesn't appear in your CloudWatch billing metrics\. For more information about CloudWatch metrics, see [Using Amazon CloudWatch Metrics](http://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/working_with_metrics.html) in the *Amazon CloudWatch User Guide*\.

## Step 7: Update the Domain Configuration<a name="domain-transfer-to-route-53-change-configuration"></a>

After the transfer is complete, you can optionally change the following settings:

**Transfer lock**  
To transfer the domain to Route 53, you had to disable the transfer lock\. If you want to re\-enable the lock to prevent unauthorized transfers, see [Locking a Domain to Prevent Unauthorized Transfer to Another Registrar](domain-lock.md)\.

**Automatic renewal**  
We configure the transferred domain to automatically renew as the expiration date approaches\. For information about how to change this setting, see [Enabling or Disabling Automatic Renewal for a Domain](domain-enable-disable-auto-renewal.md)\.

**Extended registration period**  
By default, Route 53 renews the domain annually\. If you want to register the domain for a longer period, see [Extending the Registration Period for a Domain](domain-extend.md)\.

**DNSSEC**  
For information about configuring DNSSEC for the domain, see [Configuring DNSSEC for a Domain](domain-configure-dnssec.md)\.