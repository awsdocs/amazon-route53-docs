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
Not supported\. To prevent unauthorized transfers, restrict access to the registrant email address and to the Route 53 APIs that could allow ownership change, for example, [UpdateDomainContact](https://docs.aws.amazon.com/Route53/latest/APIReference/API_domains_UpdateDomainContact.html)\. For more information, see [Actions, resources, and condition keys for Route 53 Domains](https://docs.aws.amazon.com/service-authorization/latest/reference/list_amazonroute53domains.html) in the *Service Authorization Reference* and [Example permissions for a domain record owner](access-control-managing-permissions.md#example-permissions-record-owner)\.

**Internationalized domain names**  
Supported for Japanese\.

**Authorization code not required for transfer to Route 53**  
If you're transferring a \.jp domain to Route 53, under most circumstances you don't need to get an authorization code\. Instead, initiate the transfer either programmatically or by using the Route 53 console \(see [Transferring registration for a domain to Amazon Route 53](domain-transfer-to-route-53.md)\), and then follow the procedure set by your current domain registrar\. If they ask you for value of the AGNT code for your new registrar, provide them **AGNT\-1744**, all uppercase\.  
In the rare event that your transfer fails and the error message indicates that you need an authorization code, open a support request to provide the authorization code\. For more information, see [Contacting AWS Support about domain registration issues](domain-contact-support.md)\.

**Authorization code required for transfer from Route 53**  
If you're transferring a \.jp domain from Route 53 to another registrar, initiate the transfer at your new registrar\. There is no need for an auth code at this point\. You will receive a confirmation email from address *noreply@gandi\.net* that will ask you to choose a link to confirm or reject the transfer\. To confirm the transfer, retrieve an auth code for your domain by using Route 53 console or API, then choose the link in the email, and provide the code\. For more information, see [Transferring a domain from Amazon Route 53 to another registrar](domain-transfer-from-route-53.md)\.

**DNSSEC**  
Not supported\.

**Deadlines for renewing and restoring domains**  
+ Renewal is possible: Between 30 days and 6 days before the expiration date
+ Late renewal with Route 53 is possible: No
+ Domain is deleted from Route 53: 6 days before expiration
+ Restoration with the registry is possible: Contact [AWS Support](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/domain-contact-support.html)\.
+ Domain is deleted from the registry: Contact [AWS Support](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/domain-contact-support.html)\.

**Note**  
Registering non\-general\-purpose JP domains such as \.co\.jp and \.or\.jp is currently not possible\.