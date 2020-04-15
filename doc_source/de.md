# \.de \(Germany\)<a name="de"></a>

[Return to index](registrar-tld-list.md#index)

**Registration and renewal period**  
One year\.

**Restrictions**  
Open to the public, with some restrictions:  
+ You must reside in Germany or have an administrative contact \(physical person\) who resides in Germany and has an address other than a P\.O\. box\.
+ During registration, the DNS \(A, MX, and CNAME\) of the domain name must be correctly configured so that it can pass the registry's zone check\. Three servers of two different C classes are required\.

**Privacy protection**  
Not supported\.

**Domain locking to prevent unauthorized transfers**  
Not supported\. We recommend that you prevent unauthorized transfers by restricting access to the [RetrieveDomainAuthCode](https://docs.aws.amazon.com/Route53/latest/APIReference/API_domains_RetrieveDomainAuthCode.html) API action\. \(When you restrict access to this Route 53 API, you also restrict who can generate an authorization code using the Route 53 console, AWS SDKs, and other programmatic methods\.\) For more information, see [Identity and access management in Amazon Route 53](auth-and-access-control.md)\.

**Internationalized domain names**  
Supported\.

**Authorization code required for transfer to Route 53**  
Yes

**DNSSEC**  
Supported for domain registration\. For more information, see [Configuring DNSSEC for a domain](domain-configure-dnssec.md)\.

**Deadlines for renewing and restoring domains**  
+ Renewal is possible: Until the expiration date
+ Late renewal with Route 53 is possible: No
+ Domain is deleted from Route 53: On the expiration date
+ Restoration with the registry is possible: Contact [AWS Support](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/domain-contact-support.html)\.
+ Domain is deleted from the registry: Contact [AWS Support](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/domain-contact-support.html)\.

**Registrar**  
The registrar for this TLD is our registrar associate, Gandi\.