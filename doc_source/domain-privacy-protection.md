# Enabling or disabling privacy protection for contact information for a domain<a name="domain-privacy-protection"></a>

When you register a domain with Amazon Route 53 or transfer a domain to Route 53, we enable privacy protection by default for all the contacts for the domain\. This typically hides most of your contact information from WHOIS \("Who is"\) queries and reduces the amount of spam that you receive\. Your contact information is replaced either with contact information for the registrar or with the phrase "REDACTED FOR PRIVACY\."

If you choose to disable privacy protection, you must disable it for all contacts for a domain\. If you do disable privacy protection, anyone can send a WHOIS query for the domain and, for most top\-level domains \(TLDs\), might be able to get all the contact information that you provided when you registered or transferred the domain, including name, address, phone number, and email address\. The WHOIS command is widely available; it's included in many operating systems, and it's also available as a web application on many websites\.

The information that you can hide from WHOIS queries depends on two main factors:

**The registry for the top level domain**  
Most TLD registries hide all contact information automatically, some allow you to choose to hide all contact information, some allow you to hide only some information, and some do not allow you to hide any information\.  
To enable or disable privacy protection for some domains, you must open a support case and request privacy protection\. For more information, see the applicable section in [Domains that you can register with Amazon Route 53](registrar-tld-list.md):  
+ [\.co\.uk \(United Kingdom\)](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/registrar-tld-list.html#registrar-tld-list#co.uk)
+ [\.me\.uk \(United Kingdom\)](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/registrar-tld-list.html#registrar-tld-list#me.uk)
+ [\.org\.uk \(United Kingdom\)](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/registrar-tld-list.html#registrar-tld-list#org.uk)
+ [\.link](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/registrar-tld-list.html#registrar-tld-list#link)

**The registrar**  
When you register a domain with Route 53 or transfer a domain to Route 53, the registrar for the domain is either Amazon Registrar or our registrar associate, Gandi\. Amazon Registrar and Gandi hide different information by default:  
+ **Amazon Registrar** – By default, all of your contact information is hidden\. However, regulations for the TLD registry take precedence\. 
+ **Gandi** – By default, all of your contact information is hidden except organization name, if any\. However, regulations for the TLD registry take precedence\. 

  For [geographic TLDs](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/registrar-tld-list.html#registrar-tld-list-geographic) that don't allow privacy protection, your personal information will be marked as "redacted" on the [Whois Directory Search](https://v4.gandi.net/whois) page on the Gandi website\. However, your personal information might be available at the domain registry or on third\-party WHOIS websites\. 

To find out what information is hidden for the TLD for your domain, see [Domains that you can register with Amazon Route 53](registrar-tld-list.md)\.

When you want to enable or disable privacy protection for a domain that you registered using Route 53, perform the following procedure\.<a name="domain-privacy-protection-procedure"></a>

**To enable or disable privacy protection for contact information for a domain**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Registered Domains**\.

1. Choose the name of the domain that you want to enable or disable privacy protection for\.

1. Choose **Edit Contacts**\.

1. Choose whether to hide contact information\. You must specify the same privacy setting for all three contacts: administrative, registrant, and technical\.

1. Choose **Save**\.

1. If you encounter issues while enabling or disabling privacy protection, you can contact AWS Support for free\. For more information, see [Contacting AWS Support about domain registration issues](domain-contact-support.md)\.