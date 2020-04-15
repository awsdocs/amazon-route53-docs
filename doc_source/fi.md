# \.fi \(Finland\)<a name="fi"></a>

[Return to index](registrar-tld-list.md#index)

**Registration and renewal period**  
One to five years\.

**Restrictions**  
Open to the public, with some restrictions:  
+ The \.fi extension is available to individuals who have a domicile in Finland and have a Finnish identity number, and legal persons or private entrepreneurs registered in Finland\. 
+ You must provide the following information during registration:
  + Whether or not the contact is based on a physical or moral person in Finland\.
  + The identifier of the register where the name is recorded, if based on a moral person's name\.
  + The number of the record in the register where the name is recorded, if based on a moral person's name\.
  + The identification number for a moral person in Finland\.
  + The identification number for a physical person in Finland\.

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
+ Late renewal with Route 53 is possible: Until 29 days after expiration
+ Domain is deleted from Route 53: 30 days after expiration
+ Restoration with the registry is possible: No
+ Domain is deleted from the registry: No

**Registrar**  
The registrar for this TLD is our registrar associate, Gandi\.

**Deletion of domain registration**  
The registry for \.fi domains doesn't allow you to delete domain registrations\. Instead, you must disable automatic renewal and wait for the domain to expire\. For more information, see [Deleting a domain name registration](domain-delete.md)\.