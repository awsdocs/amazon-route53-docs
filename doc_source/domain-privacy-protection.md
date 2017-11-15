# Enabling or Disabling Privacy Protection for Contact Information for a Domain<a name="domain-privacy-protection"></a>

When you register a domain with Amazon Route 53, we enable privacy protection by default for all the contacts for the domain\. This typically hides most of your contact information from WHOIS \("Who is"\) queries and reduces the amount of spam that you receive\. Your contact information is replaced either with contact information for the registrar or with the phrase "Protected by policy\."

**Important**  
You can hide contact information only when the domain is locked to prevent transfers\. If you're transferring the domain to or from Amazon Route 53, you must disable privacy protection, so your contact information is visible in WHOIS queries\. You can re\-enable privacy protection when the transfer is complete\.

You can choose to disable privacy protection for some or all contacts for a domain\. If you do, anyone can send a WHOIS query for the domain and, for most top\-level domains \(TLDs\), get all the contact information that you provided when you registered the domain, including name, address, phone number, and email address\. The WHOIS command is widely available; it's included in many operating systems, and it's also available as a web application on many websites\.

The information that you can hide from WHOIS queries depends on two main factors:

**The registry for the top level domain**  
Some TLD registries hide all contact information automatically, some allow you to choose to hide all contact information, some allow you to hide only some information, and some do not allow you to hide any information\. For example, most registries allow you to hide your address, phone number, and email address\. Only a few also allow you to hide your name\. 

**The registrar**  
When you register a domain with Amazon Route 53 or transfer a domain to Amazon Route 53, the registrar for the domain is either Amazon Registrar or our registrar associate, Gandi\. Amazon Registrar and Gandi hide different information by default:  

+ **Amazon Registrar** – By default, all of your contact information is hidden\. 

+ **Gandi** – By default, all of your contact information is hidden except first and last name, and organization name\. However, regulations for the TLD registry take precedence\. 

To find out what information is hidden for the TLD for your domain, see [Domains That You Can Register with Amazon Route 53](registrar-tld-list.md)\.

When you want to enable or disable privacy protection for a domain that you registered using Amazon Route 53, perform the following procedure\.

**To enable or disable privacy protection for contact information for domain**

1. Sign in to the AWS Management Console and open the Amazon Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Registered Domains**\.

1. Choose the name of the domain that you want to enable or disable privacy protection for\.

1. Choose **Edit Contacts**\.

1. For each type of contact, choose whether to hide contact information\. 

1. Choose **Save**\.