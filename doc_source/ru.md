# \.ru \(Russian Federation\)<a name="ru"></a>

**Important**  
You can no longer use Route 53 to register new \.ru domains or transfer \.ru domains to Route 53\. We'll continue to support \.ru domains that are already registered with Route 53\.

[Return to index](registrar-tld-list.md#index)

**Registration and renewal period**  
One year\.  
The registry for \.ru domains updates the expiration date for a domain on the day that the domain expires\. WHOIS queries will show the old expiration date for the domain until that date regardless of when you renew the domain with Route 53\.

**Restrictions**  
Open to the public, with some restrictions:  
+ Individuals might need to provide a passport number or government\-issued ID number\. 
+ Foreign companies might need to provide a company ID or company registration\. 

**Privacy protection**  
Determined by the registry\.

**Domain locking to prevent unauthorized transfers**  
Not supported\. We recommend that you prevent unauthorized transfers by restricting access to the [RetrieveDomainAuthCode](https://docs.aws.amazon.com/Route53/latest/APIReference/API_domains_RetrieveDomainAuthCode.html) API action\. \(When you restrict access to this Route 53 API, you also restrict who can generate an authorization code using the Route 53 console, AWS SDKs, and other programmatic methods\.\) For more information, see [Identity and access management in Amazon Route 53](auth-and-access-control.md)\.

**Internationalized domain names**  
Not supported\.

**Authorization code required for transfer to Route 53**  
Not supported\. You can no longer transfer \.ru domains to Route 53\.

**DNSSEC**  
Not supported\.

**Deadlines for renewing and restoring domains**  
+ Renewal is possible: Until 2 days before the expiration date
+ Late renewal with Route 53 is possible: No
+ Domain is deleted from Route 53: 2 days before expiration
+ Restoration with the registry is possible: Between 2 days before and 28 days after expiration
+ Domain is deleted from the registry: 28 days after expiration

**Registrar**  
The registrar for this TLD is our registrar associate, Gandi\.

**Deletion of domain registration**  
The registry for \.ru domains doesn't allow you to delete domain registrations\. Instead, you must disable automatic renewal and wait for the domain to expire\. For more information, see [Deleting a domain name registration](domain-delete.md)\.