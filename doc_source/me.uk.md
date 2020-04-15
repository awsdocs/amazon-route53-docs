# \.me\.uk \(United Kingdom\)<a name="me.uk"></a>

[Return to index](registrar-tld-list.md#index)

**Registration and renewal period**  
One to ten years\.

**Restrictions**  
Open to the public, with no restrictions\. 

**Privacy protection**  
All information is hidden\.

**Domain locking to prevent unauthorized transfers**  
Not supported\. We recommend that you prevent unauthorized transfers by restricting access to the [RetrieveDomainAuthCode](https://docs.aws.amazon.com/Route53/latest/APIReference/API_domains_RetrieveDomainAuthCode.html) API action\. \(When you restrict access to this Route 53 API, you also restrict who can generate an authorization code using the Route 53 console, AWS SDKs, and other programmatic methods\.\) For more information, see [Identity and access management in Amazon Route 53](auth-and-access-control.md)\.

**Internationalized domain names**  
Not supported\.

**Authorization code required for transfer to Route 53**  
If you're transferring a \.me\.uk domain to Route 53, you don't need to get an authorization code\. Instead, use the method provided by your current domain registrar to update the value of the IPS tag for the domain to **GANDI**, all uppercase\. \(An IPS tag is required by Nominet, the registry for \.uk domain names\.\) If your registrar will not change the value of the IPS tag, [contact Nominet](http://www.nominet.org.uk/uk-domain-names/manage-your-domain/change-registrar)\.  
When you register a \.me\.uk domain, Route 53 automatically sets the IPS tag for the domain to **GANDI**\.

**DNSSEC**  
Supported for domain registration\. For more information, see [Configuring DNSSEC for a domain](domain-configure-dnssec.md)\.

**Deadlines for renewing and restoring domains**  
+ Renewal is possible: Between 180 days before and 30 days after the expiration date
+ Late renewal with Route 53 is possible: Between 30 days and 90 days after expiration
+ Domain is deleted from Route 53: 90 days after expiration
+ Restoration with the registry is possible: No
+ Domain is deleted from the registry: 92 days after expiration

**Registrar**  
The registrar for this TLD is our registrar associate, Gandi\.

**Deletion of domain registration**  
The registry for \.me\.uk domains doesn't allow you to delete domain registrations\. Instead, you must disable automatic renewal and wait for the domain to expire\. For more information, see [Deleting a domain name registration](domain-delete.md)\.