# \.net\.au \(Australia\)<a name="net.au"></a>

[Return to index](registrar-tld-list.md#index)

**Confirmation email from the TLD registry**  
Our registrar associate, Gandi, resells \.net\.au domains through Tucows\. When you transfer a domain name to Route 53, Tucows sends an email to the registrant contact for the domain to verify contact information or to authorize transfer requests\.

**Registration and renewal period**  
One to five years\.

**Restrictions**  
Only second\-level domains are available\. Route 53 supports the second\-level domains \.com\.au and net\.au\.   
Open to the public, with some restrictions:  
+ The \.com\.au and \.net\.au domains are open to legal persons, trading, partnerships, or sole traders registered in Australia; to foreign companies licensed to trade in Australia; and to owners or applicants of an Australian\-registered trademark\. 
+ Your domain name must be identical to your name, as registered with the relevant Australian authorities or to your trademark \(or to the abbreviation or acronym\)\. 
+ The domain name should indicate your activity\. For example, it should indicate a product that you sell or a service that you provide\.
+ During the registration process, you must indicate the following:
  + Your registration type: ABN \(Australian Business Number\), ACN \(Australian Company Number\), or TM \(Trademark\) if the domain name corresponds to your trademark\.
  + Your ID number, which can be a Medicare card number, a tax file number \(TFN\), a state driver's license number, or an Australian Business Number \(ABN\)\.
  + Your state or province\.

**Privacy protection**  
All information is hidden except the name of the registrant contact\.

**Domain locking to prevent unauthorized transfers**  
Not supported\. We recommend that you prevent unauthorized transfers by restricting access to the [RetrieveDomainAuthCode](https://docs.aws.amazon.com/Route53/latest/APIReference/API_domains_RetrieveDomainAuthCode.html) API action\. \(When you restrict access to this Route 53 API, you also restrict who can generate an authorization code using the Route 53 console, AWS SDKs, and other programmatic methods\.\) For more information, see [Identity and access management in Amazon Route 53](auth-and-access-control.md)\.

**Internationalized domain names**  
Not supported\.

**Authorization code required for transfer to Route 53**  
Yes

**DNSSEC**  
Not supported\.

**Deadlines for renewing and restoring domains**  
+ Renewal is possible: Between 60 days before expiration and the expiration date
+ Late renewal with Route 53 is possible: Until 29 days after expiration
+ Domain is deleted from Route 53: 29 days after expiration
+ Restoration with the registry is possible: No
+ Domain is deleted from the registry: 30 days after expiration

**Registrar**  
Our registrar associate, Gandi, uses Tucows as the registrar for this TLD\.

**Deletion of domain registration**  
The registry for \.net\.au domains doesn't allow you to delete domain registrations\. Instead, you must disable automatic renewal and wait for the domain to expire\. For more information, see [Deleting a domain name registration](domain-delete.md)\.