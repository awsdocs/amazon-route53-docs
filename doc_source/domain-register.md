# Registering a New Domain<a name="domain-register"></a>

When you want to register a new domain using the Amazon Route 53 console, perform the following procedure\.

**Important**  
When you register a domain with Amazon Route 53, we automatically create a hosted zone for the domain to make it easier for you to use Amazon Route 53 as the DNS service provider for your new domain\. This hosted zone is where you store information about how to route traffic for your domain, for example, to an Amazon EC2 instance or a CloudFront distribution\. We charge a small monthly fee for the hosted zone in addition to the annual charge for the domain registration\. If you don't want to use your domain right now, you can delete the hosted zone; if you delete it within 12 hours of registering the domain, there won't be any charge for the hosted zone on your AWS bill\. We also charge a small fee for the DNS queries that we receive for your domain\. For more information, see [Amazon Route 53 Pricing](https://aws.amazon.com/route53/pricing/)\.

Note that you can't use AWS credits to pay the fee for registering a new domain with Amazon Route 53\.

**To register a new domain using Amazon Route 53**

1. Sign in to the AWS Management Console and open the Amazon Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. If you're new to Amazon Route 53, under **Domain Registration**, choose **Get Started Now**\.

   If you're already using Amazon Route 53, in the navigation pane, choose **Registered Domains**\.

1. Choose **Register Domain**\.

1. Enter the domain name that you want to register, and choose **Check** to find out whether the domain name is available\.

   For information about how to specify characters other than a\-z, 0\-9, and \- \(hyphen\) and how to specify internationalized domain names, see [DNS Domain Name Format](DomainNameFormat.md)\.

1. If the domain is available, choose **Add to cart**\. The domain name appears in your shopping cart\. 

   The **Related domain suggestions** list shows other domains that you might want to register instead of your first choice \(if it's not available\) or in addition to your first choice\. Choose **Add to cart** for each additional domain that you want to register, up to a maximum of five domains\.

1. In the shopping cart, choose the number of years that you want to register the domain for\.

1. To register more domains, repeat steps 4 through 6\.

1. Choose **Continue**\.

1. On the **Contact Details for Your** *n* **Domains** page, enter contact information for the domain registrant, administrator, and technical contacts\. The values that you enter here are applied to all of the domains that you're registering\. 

   By default, we use the same information for all three contacts\. If you want to enter different information for one or more contacts, change the value of **My Registrant, Administrative, and Technical Contacts are all the same** to **No**\.

   If you're registering more than one domain, we use the same contact information for all of the domains\. 

   For more information, see [Values that You Specify When You Register a Domain](domain-register-values-specify.md)\.

1. For some top\-level domains \(TLDs\), we're required to collect additional information\. For these TLDs, enter the applicable values after the **Postal/Zip Code** field\.

1. Choose whether you want to hide your contact information from WHOIS queries\. For more information, see the following topics:

   + [Enabling or Disabling Privacy Protection for Contact Information for a Domain](domain-privacy-protection.md)

   + [Domains That You Can Register with Amazon Route 53](registrar-tld-list.md)

1. Choose **Continue**\.

1. For [generic TLDs](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/registrar-tld-list.html#registrar-tld-list-generic), if you specified an email address for the registrant contact that has never been used to register a domain with Amazon Route 53, you need to verify that the address is valid\.

   If the registry requires verification and if you can verify the address during domain registration, the console displays a **Verify the Email Address for the Registrant Contact** section:

   + If the section doesn't appear, skip to step 14\.

   + If the section appears and the status is **email\-address is verified**, skip to step 14\.

   + If the section appears and the value is Registrant email not verified, continue with this step\.

   Perform the following steps:

   1. Choose **Send verification email**\. We send a verification email from one of the following email addresses:

      + **noreply@registrar\.amazon\.com** – for TLDs registered by Amazon Registrar\.

      + **noreply@domainnameverification\.net** – for TLDs registered by our registrar associate, Gandi\. To determine who the registrar is for your TLD, see [Domains That You Can Register with Amazon Route 53](registrar-tld-list.md)\.
**Important**  
The registrant contact must follow the instructions in the email to verify that the email was received, or we must suspend the domain as required by ICANN\. When a domain is suspended, it's not accessible on the internet\.

   1. When you receive the verification email, choose the link in the email that verifies that the email address is valid\. If you don't receive the email immediately, perform the following troubleshooting steps:

      + Choose **Back** and verify that the email address for the registrant contact is the correct one\.

      + Check your junk email folder\.

   1. Return to the Amazon Route 53 console\. If the status doesn't automatically update to say **email\-address is verified**, choose **Refresh status**\.

1. Review the information that you entered, read the terms of service, and select the check box to confirm that you've read the terms of service\. 

1. Choose **Complete Purchase**\.

   If the registry requires us to verify the email address for the registrant contact but doesn't allow us to verify earlier in the process, we send a verification email from one of the following email addresses: 

   + **noreply@registrar\.amazon\.com ** – for TLDs registered by Amazon Registrar\.

   + **noreply@domainnameverification\.net** – for TLDs registered by our registrar associate, Gandi\. To determine who the registrar is for your TLD, see [Domains That You Can Register with Amazon Route 53](registrar-tld-list.md)\.

   When you receive the verification email, choose the link in the email that verifies that the email address is valid\. If you don't receive the email immediately, perform the following troubleshooting steps:

   + Choose **Back** and verify that the email address for the registrant contact is the correct one\.

   + Check your junk email folder\.
**Important**  
The registrant contact must follow the instructions in the email to confirm that the email was received, or we must suspend the domain as required by ICANN\. When a domain is suspended, it's not accessible on the internet\.

   For all TLDs, you'll receive an email when your domain registration has been approved\. To determine the current status of your request, see [Viewing the Status of a Domain Registration](domain-view-status.md)\.

1. When domain registration is complete, your next step depends on whether you want to use Amazon Route 53 or another DNS service as the DNS service for the domain:

   + **Amazon Route 53** – In the hosted zone that Amazon Route 53 created when you registered the domain, create resource record sets to tell Amazon Route 53 how you want to route traffic for the domain and subdomains\. 

     For example, when someone enters your domain name in a browser and that query is forwarded to Amazon Route 53, do you want Amazon Route 53 to respond to the query with the IP address of a web server in your data center or with the name of an ELB load balancer?

     For more information, see [Working with Resource Record Sets](rrsets-working-with.md)\.
**Important**  
If you create resource record sets in a hosted zone other than the one that Amazon Route 53 creates automatically, you must update the name servers for the domain to use the name servers for the new hosted zone\.

   + **Another DNS service** – Configure your new domain to route DNS queries to the other DNS service\. Perform the procedure [To update the name servers for your domain when you want to use another DNS service](#domain-register-other-dns-service-procedure)\.

**To update the name servers for your domain when you want to use another DNS service**

1. Use the process that is provided by your DNS service to get the name servers for the domain\.

1. Sign in to the AWS Management Console and open the Amazon Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Registered Domains**\.

1. Choose the name of the domain that you want to configure to use another DNS service\.

1. Choose **Add/Edit Name Servers**\.

1. Change the names of the name servers to the name servers that you got from your DNS service in step 1\.

1. Choose **Update**\.

1. \(Optional\) Delete the hosted zone that Amazon Route 53 created automatically when you registered your domain\. This prevents you from being charged for a hosted zone that you aren't using\.

   1. In the navigation pane, choose **Hosted Zones**\.

   1. Select the radio button for the hosted zone that has the same name as your domain\.

   1. Choose **Delete Hosted Zone**\.

   1. Choose **Confirm** to confirm that you want to delete the hosted zone\.