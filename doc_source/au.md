# \.au \(Australia\)<a name="au"></a>

[Return to index](registrar-tld-list.md#index)

**Note**  
Registration for \.au domains is available through Route 53, starting March 31, 2022\. The registration process for \.au domains is same as for other domains, unless another party owns the corresponding second\-level domain \(SLD\) of the \.au domain \(for example, \.com\.au or net\.au\)\. For the owners of those \.au SLD domains, a priority registration period is open from March 24,2022 until September 20, 2022\. For more information, see [The Priority Allocation Process](https://www.auda.org.au/au-domain-names/au-direct/priority-allocation-process) and the [FAQ for \.au domains](#au-priority-allocation-faq)\. 

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

**Registrar**  
Our registrar associate, Gandi, uses DomainDirectors as the registrar for this TLD\.

**Deletion of domain registration**  
The registry for \.au domains doesn't allow you to delete domain registrations\. Instead, you must disable automatic renewal and wait for the domain to expire\. For more information, see [Deleting a domain name registration](domain-delete.md)\.

**Changing ownership**  
Change the owner by using the Route 53 console\. See [Updating contact information for a domain](domain-update-contacts.md#domain-update-contacts-basic)\. Then complete the following process to complete the ownership change:  

1. Both the old and new registrants must click the link they receive in an email from *noreply@emailverification\.info* to their listed email addresses\. If this isn't completed within 14 days, you have to start the process again\.

   

1. After the responses are confirmed, the owner change in the registry will be processed in a short time without any further confirmation\.

## FAQ for \.au domains<a name="au-priority-allocation-faq"></a>

**How do I register \.au domains?**  
The registration for \.au domains is the same as for other domains, as long as the domain that you want to register isn't reserved as part of the Priority Allocation Process\.

**What are the requirements for registering \.au domains?**  
For the general requirements of \.au domain registration, see [\.au direct](https://www.auda.org.au/au-domain-names/au-domain-names/au-direct) by auDA\.

**How can I check if I can participate in the Priority Allocation Process?**  
You can check the priorities and status for your domain name by using the [priority status tool](https://www.auda.org.au/tools/priority-status-tool) provided by auDA\.

**How do I participate in the Priority Allocation Process?**  
To participate in the Priority Allocation Process, you register your \.au domain as you would other domains\. We automatically process the domain as participating in the Priority Allocation Process if the domain and contact information that you apply with are eligible\. Otherwise, you can provide an AU priority token when you register your domain, if you've obtained a token, and we will process your domain in the Priority Allocation Process\.  
Due to the Priority Allocation Process, your domain registration can end up in a pending status\. Make sure that the contact information for your existing domain is up\-to\-date\. Stale or invalid contact information can lead to delays in processing your application\. For more information, see [The Priority Allocation Process](https://www.auda.org.au/au-domain-names/au-direct/priority-allocation-process)\.

**How can I get an AU priority token?**  
You can get an AU priority token from auDA by using their [priority token tool](https://priority.auda.org.au/)\. For more information, see [The Priority Allocation Process](https://www.auda.org.au/au-domain-names/au-direct/priority-allocation-process)\. The token you will receive consists of the **priority contact ID** and **priority authinfo** strings\. Enter them into the AU priority token field separated by a dash, for example, *m01XXXXXXXXX\-Au2XXXXXXXXX*\.

**Do I need to register a \.au domain on March 24, 2022 to be able to participate in the Priority Allocation Process?**  
No\. The \.au domain launched on March 24, 2022 but registrants of eligible \.au domain names \(such as \.com\.au and \.net\.au\) have until September 20, 2022 to indicate whether they intend to apply for the exact match of their names in the \.au domain using the Priority Allocation Process\. Participating in the Priority Allocation Process earlier doesn’t mean you have priority over other participants\. For more information, see [The Priority Allocation Process](https://www.auda.org.au/au-domain-names/au-direct/priority-allocation-process)\.

**Do I need to participate in the Priority Allocation Process if I own a second level \.au domain?**  
No\. If you don’t want to apply for a \.au direct domain for your equivalent second\-level \.au domain, there is no action required\. Your existing domains will not be affected\.

**Can I still register a second\-level domain for \.au \(such as \.com\.au or \.net\.au\)?**  
Yes\. The original second\-level domains remain in operation\. The registration rules for these haven't changed\.