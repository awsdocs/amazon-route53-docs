# \.au \(Australia\)<a name="au"></a>

[Return to index](registrar-tld-list.md#index)

**Confirmation email from the TLD registry**  
Our registrar associate, Gandi, resells \.au domains through DomainDirectors\. When you transfer a domain name to Route 53, DomainDirectors sends an email to the registrant contact for the domain to verify contact information or to authorize transfer requests\.

**Registration and renewal period**  
One year\.

**Restrictions**  
Open to the public, with some restrictions:  
+ The \.au domains are open to legal persons, trading, partnerships, or sole traders registered in Australia; to foreign companies licensed to trade in Australia; and to owners or applicants of an Australian\-registered trademark\. Individuals cannot register \.au domains\. The registrant contact must be a company\.
+ Your domain name must be identical to your name, as registered with the relevant Australian authorities or to your trademark \(or to the abbreviation or acronym\)\. 
+ The domain name should indicate your activity\. For example, it should indicate a product that you sell or a service that you provide\.
+ During the registration process, you must indicate the following:
  + Your registration type: ABN \(Australian Business Number\), ACN \(Australian Company Number\), or TM \(Trademark\) if the domain name corresponds to your trademark\.
  + Your ID number, which can be a Medicare card number, a tax file number \(TFN\), a state driver's license number, or an Australian Business Number \(ABN\)\.
  + Your state or province\.
+ Incorrect or mismatched contact information, including name, ABN, or Trademark \(TM\) number will result in registration, trade, and renewals failures\. An ownership change might be required to correct information for existing domains\.

**Privacy protection**  
Not supported\.

**Domain locking to prevent unauthorized transfers**  
Not supported\. We recommend that you prevent unauthorized transfers by restricting access to the [RetrieveDomainAuthCode](https://docs.aws.amazon.com/Route53/latest/APIReference/API_domains_RetrieveDomainAuthCode.html) API action\. \(When you restrict access to this Route 53 API, you also restrict who can generate an authorization code using the Route 53 console, AWS SDKs, and other programmatic methods\.\) For more information, see [Identity and access management in Amazon Route 53](auth-and-access-control.md)\.

**Internationalized domain names**  
Not supported\.

**Authorization code required for transfer to Route 53**  
Yes

**DNSSEC**  
Supported for domain registration\. When you set the key, you must choose DNS security algorithm 2 \(DH\)\. For more information, see [Configuring DNSSEC for a domain](domain-configure-dnssec.md)\.

**Deadlines for renewing and restoring domains**  
+ Renewal is possible: Between 60 days before expiration and the expiration date
+ Late renewal with Route 53 is possible: Until 29 days after expiration
+ Domain is deleted from Route 53: 29 days after expiration
+ Restoration with the registry is possible: No
+ Domain is deleted from the registry: 30 days after expiration

**Deletion of domain registration**  
The registry for \.au domains doesn't allow you to delete domain registrations\. Instead, you must disable automatic renewal and wait for the domain to expire\. For more information, see [Deleting a domain name registration](domain-delete.md)\.

**Changing ownership**  
Change the owner by using the Route 53 console\. See [Updating contact information for a domain](domain-update-contacts.md#domain-update-contacts-basic)\. Then complete the following process to complete the ownership change:  

1. Both the old and new registrants must click the link they receive in an email from *noreply@emailverification\.info* to their listed email addresses\. If this isn't completed within 14 days, you have to start the process again\.

   

1. After the responses are confirmed, the owner change in the registry will be processed in a short time without any further confirmation\.