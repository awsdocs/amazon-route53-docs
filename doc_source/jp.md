# \.jp \(Japan\)<a name="jp"></a>

[Return to index](registrar-tld-list.md#index)

**Registration and renewal period**  
One year\.

**Restrictions**  
Open to the public, with one restriction:  
+ Only individuals or companies in Japan can register a \.jp domain name\.

**Privacy protection**  
Not supported\.

**Domain locking to prevent unauthorized transfers**  
Not supported\. We recommend that you prevent unauthorized transfers by restricting access to the [RetrieveDomainAuthCode](https://docs.aws.amazon.com/Route53/latest/APIReference/API_domains_RetrieveDomainAuthCode.html) API action\. \(When you restrict access to this Route 53 API, you also restrict who can generate an authorization code using the Route 53 console, AWS SDKs, and other programmatic methods\.\) For more information, see [Identity and access management in Amazon Route 53](auth-and-access-control.md)\.

**Internationalized domain names**  
Supported for Japanese\.

**Authorization code required for transfer to Route 53**  
If you're transferring a \.jp domain to Route 53, you don't need to get an authorization code\. Instead, use the method provided by your current domain registrar to update the value of the AGNT code to **AGNT\-1744**, all uppercase\. 

**DNSSEC**  
Not supported\.

**Deadlines for renewing and restoring domains**  
+ Renewal is possible: Between 30 days and 6 days before the expiration date
+ Late renewal with Route 53 is possible: No
+ Domain is deleted from Route 53: 6 days before expiration
+ Restoration with the registry is possible: Contact [AWS Support](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/domain-contact-support.html)\.
+ Domain is deleted from the registry: Contact [AWS Support](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/domain-contact-support.html)\.

**Registrar**  
The registrar for this TLD is our registrar associate, Gandi\.