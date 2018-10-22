# Registering a New Domain<a name="domain-register"></a>

When you want to register a new domain using the Amazon Route 53 console, perform the following procedure\.

Note the following:

**Domain registration pricing**  
For information about the cost to register domains, see [Amazon Route 53 Pricing for Domain Registration](https://d32ze2gidvkk54.cloudfront.net/Amazon_Route_53_Domain_Registration_Pricing_20140731.pdf)\.

**Supported domains**  
For a list of supported TLDs, see [Domains That You Can Register with Amazon Route 53](registrar-tld-list.md)\.

**AWS credits**  
You can't use AWS credits to pay the fee for registering a new domain with Route 53\.

**Special or premium prices**  
TLD registries have assigned special or premium prices to some domain names\. You can't use Route 53 to register a domain that has a special or premium price\.

**Charges for hosted zones**  
When you register a domain with Route 53, we automatically create a hosted zone for the domain and charge a small monthly fee for the hosted zone in addition to the annual charge for the domain registration\. This hosted zone is where you store information about how to route traffic for your domain, for example, to an Amazon EC2 instance or a CloudFront distribution\. If you don't want to use your domain right now, you can delete the hosted zone; if you delete it within 12 hours of registering the domain, there won't be any charge for the hosted zone on your AWS bill\. We also charge a small fee for the DNS queries that we receive for your domain\. For more information, see [Amazon Route 53 Pricing](https://aws.amazon.com/route53/pricing/)\.

**To register a new domain using Route 53**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. If you're new to Route 53, under **Domain Registration**, choose **Get Started Now**\.

   If you're already using Route 53, in the navigation pane, choose **Registered Domains**\.

1. Choose **Register Domain**, and specify the domain that you want to register:

   1. Enter the domain name that you want to register, and choose **Check** to find out whether the domain name is available\.

      For information about how to specify characters other than a\-z, 0\-9, and \- \(hyphen\) and how to specify internationalized domain names, see [DNS Domain Name Format](DomainNameFormat.md)\.

   1. If the domain is available, choose **Add to cart**\. The domain name appears in your shopping cart\. 

      The **Related domain suggestions** list shows other domains that you might want to register instead of your first choice \(if it's not available\) or in addition to your first choice\. Choose **Add to cart** for each additional domain that you want to register, up to a maximum of five domains\.

   1. In the shopping cart, choose the number of years that you want to register the domain for\.

   1. To register more domains, repeat steps 3a through 3c\.

1. Choose **Continue**\.

1. On the **Contact Details for Your** *n* **Domains** page, enter contact information for the domain registrant, administrator, and technical contacts\. The values that you enter here are applied to all of the domains that you're registering\. For more information, see [Values that You Specify When You Register or Transfer a Domain](domain-register-values-specify.md)\.

   Note the following considerations:  
**First Name and Last Name**  
For **First Name** and **Last Name**, we recommend that you specify the name on your official ID\. For some changes to domain settings, some domain registries require that you provide proof of identity\. The name on your ID must match the name of the registrant contact for the domain\.  
**Different Contacts**  
By default, we use the same information for all three contacts\. If you want to enter different information for one or more contacts, change the value of **My Registrant, Administrative, and Technical Contacts are all the same** to **No**\.  
For \.it domains, the registrant and administrative contacts must be the same\.  
**Multiple Domains**  
If you're registering more than one domain, we use the same contact information for all of the domains\.   
**Additional Required Information**  
For some top\-level domains \(TLDs\), we're required to collect additional information\. For these TLDs, enter the applicable values after the **Postal/Zip Code** field\.  
**Privacy Protection**  
Choose whether you want to hide your contact information from WHOIS queries\. For more information, see the following topics:  

   + [Enabling or Disabling Privacy Protection for Contact Information for a Domain](domain-privacy-protection.md)

   + [Domains That You Can Register with Amazon Route 53](registrar-tld-list.md)
To enable privacy protection for \.co\.uk, \.me\.uk, and \.org\.uk domains, you must open a support case and request privacy protection\. For more information, see [\.co\.uk \(United Kingdom\)](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/registrar-tld-list.html#registrar-tld-list-geographic) in [Domains That You Can Register with Amazon Route 53](registrar-tld-list.md)\.

1. Choose **Continue**\.

1. **Generic TLDs only** – If you're registering a domain that has a [generic TLD](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/registrar-tld-list.html#registrar-tld-list-generic), such as \.com, \.org, or \.net, and you specified an email address for the registrant contact that has never been used to register a domain with Route 53, you need to verify that the address is valid\.
**Note**  
Verification isn't required for domains that have a [geographic TLD](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/registrar-tld-list.html#registrar-tld-list-geographic), such as \.ca, \.com\.au, \.co\.uk, or \.jp\.

   If the registry requires verification and if you can verify the address during domain registration, the console displays a **Verify the Email Address for the Registrant Contact** section:

   + If the section doesn't appear, skip to step 8\.

   + If the section appears and the status is **email\-address is verified**, skip to step 8\.

   + If the section appears and the value is **Registrant email not verified**, continue with this step\.

   Perform the following steps:

   1. Choose **Send verification email**\. We send a verification email from one of the following email addresses:

      + **noreply@registrar\.amazon\.com** – for TLDs registered by Amazon Registrar\.

      + **noreply@domainnameverification\.net** – for TLDs registered by our registrar associate, Gandi\. To determine who the registrar is for your TLD, see [Domains That You Can Register with Amazon Route 53](registrar-tld-list.md)\.
**Important**  
The registrant contact must follow the instructions in the email to verify that the email was received, or we must suspend the domain as required by ICANN\. When a domain is suspended, it's not accessible on the internet\.

   1. When you receive the verification email, choose the link in the email that verifies that the email address is valid\. If you don't receive the email immediately, check your junk email folder\.

   1. Return to the Route 53 console\. If the status doesn't automatically update to say **email\-address is verified**, choose **Refresh status**\.

1. Review the information that you entered, read the terms of service, and select the check box to confirm that you've read the terms of service\. 

1. Choose **Complete Purchase**\.

1. **Generic TLDs only** – Verify that the email address for the registrant contact is valid\.
**Note**  
If you were able to verify your email address in step 7, skip to step 11\.

   If the registry requires us to verify the email address for the registrant contact but doesn't allow us to verify earlier in the process, we send a verification email from one of the following email addresses: 

   + **noreply@registrar\.amazon\.com ** – for TLDs registered by Amazon Registrar\.

   + **noreply@domainnameverification\.net** – for TLDs registered by our registrar associate, Gandi\. To determine who the registrar is for your TLD, see [Domains That You Can Register with Amazon Route 53](registrar-tld-list.md)\.

   When you receive the verification email, choose the link in the email that verifies that the email address is valid\. If you don't receive the email immediately:

   + Check the settings for the domain to verify that you specified the correct email address for the registrant contact\.

   + Check your junk email folder\.
**Important**  
The registrant contact must follow the instructions in the email to confirm that the email was received, or we must suspend the domain as required by ICANN\. When a domain is suspended, it's not accessible on the internet\.

1. For all TLDs, you'll receive an email when your domain registration has been approved\.

   To determine the current status of your request, see [Viewing the Status of a Domain Registration](domain-view-status.md)\.

1. \(Optional\) We configure the domain to automatically renew as the expiration date approaches\. If you want to change this setting, see [Enabling or Disabling Automatic Renewal for a Domain](domain-enable-disable-auto-renewal.md)\. 

1. When domain registration is complete, your next step depends on whether you want to use Route 53 or another DNS service as the DNS service for the domain:

   + **Route 53** – In the hosted zone that Route 53 created when you registered the domain, create records to tell Route 53 how you want to route traffic for the domain and subdomains\. 

     For example, when someone enters your domain name in a browser and that query is forwarded to Route 53, do you want Route 53 to respond to the query with the IP address of a web server in your data center or with the name of an ELB load balancer?

     For more information, see [Working with Records](rrsets-working-with.md)\.
**Important**  
If you create records in a hosted zone other than the one that Route 53 creates automatically, you must update the name servers for the domain to use the name servers for the new hosted zone\.

   + **Another DNS service** – Configure your new domain to route DNS queries to the other DNS service\. Perform the procedure [To update the name servers for your domain when you want to use another DNS service](#domain-register-other-dns-service-procedure)\.

**To update the name servers for your domain when you want to use another DNS service**

1. Use the process that is provided by your DNS service to get the name servers for the domain\.

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Registered Domains**\.

1. Choose the name of the domain that you want to configure to use another DNS service\.

1. Choose **Add/Edit Name Servers**\.

1. Change the names of the name servers to the name servers that you got from your DNS service in step 1\.

1. Choose **Update**\.

1. \(Optional\) Delete the hosted zone that Route 53 created automatically when you registered your domain\. This prevents you from being charged for a hosted zone that you aren't using\.

   1. In the navigation pane, choose **Hosted Zones**\.

   1. Select the radio button for the hosted zone that has the same name as your domain\.

   1. Choose **Delete Hosted Zone**\.

   1. Choose **Confirm** to confirm that you want to delete the hosted zone\.