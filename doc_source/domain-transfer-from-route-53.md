# Transferring a Domain from Amazon Route 53 to Another Registrar<a name="domain-transfer-from-route-53"></a>

When you transfer a domain from Amazon Route 53 to another registrar, you get some information from Route 53 and provide it to the new registrar\. The new registrar will do the rest\.

**Important**  
If you're currently using Route 53 as your DNS service provider and you also want to transfer DNS service to another provider, be aware that the following Route 53 features don't have direct parallels with features provided by other DNS service providers\. You'll need to work with the new DNS service provider to determine how to achieve comparable functionality:  
Alias records\. For more information, see [Choosing Between Alias and Non\-Alias Records](resource-record-sets-choosing-alias-non-alias.md)\.
Routing policies other than the simple routing policy\. For more information, see [Choosing a Routing Policy](routing-policy.md)\.
Health checks that are associated with records\. For more information, see [Configuring DNS Failover](dns-failover-configuring.md)\.

Usually, you can transfer registration of a domain name to another registrar without much trouble\. Requirements vary among TLDs, but the following requirements are typical:

+ You must have registered the domain with the current registrar at least 60 days ago\.

+ If the registration for a domain name expired and had to be restored, it must have been restored at least 60 days ago\.

+ You must have transferred registration for the domain to the current registrar at least 60 days ago\.

+ The domain cannot have any of the following domain name status codes:

  + pendingDelete

  + pendingTransfer

  + redemptionPeriod

  + clientTransferProhibited

For a current list of domain name status codes and an explanation of what each code means, go to the [ICANN website](https://www.icann.org/) and search for **epp status codes**\. \(Search on the ICANN website; web searches sometimes return an old version of the document\.\)

**To transfer a domain from Route 53 to another registrar**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Registered Domains**\.

1. Choose the name of the domain that you want to transfer to another registrar\.

1. On the **Registered domains > ** *domain name* page, check the value of **Domain name status code**\. If it is one of the following values, you can't currently transfer the domain: 

   + pendingDelete

   + pendingTransfer

   + redemptionPeriod

   + clientTransferProhibited

   For a current list of domain name status codes and an explanation of what each code means, go to the [ICANN website](https://www.icann.org/) and search for **epp status codes**\. \(Search on the ICANN website; web searches sometimes return an old version of the document\.\)

1. If the value of **Transfer lock** is **Enabled**, choose **Disable\.**

1. Choose **Edit contacts**\.

1. On the **Registered Domain** *domain name* **Edit Contacts** page, for **Privacy Protection**, select **Disable** for all contacts\.

   In addition, update the contact information so the new registrar can contact you\.

1. Choose **Save**\.

1. *All domains except \.uk, \.co\.uk, \.me\.uk, and \.org\.uk domains* – On the **Registered Domains >** *domain name* page, at **Authorization Code**, choose **Get code** and make note of the authorization code\. You'll provide this value to your registrar later in this procedure\.

   *\.uk, \.co\.uk, \.me\.uk, and \.org\.uk domains* – Change the IPS tag to the value for the new registrar:

   1. Go to the [Find a Registrar](http://www.nominet.uk/registrar-list/) page on the Nominet website, and find the IPS tag for the new registrar\. \(Nominet is the registry for \.uk, \.co\.uk, \.me\.uk, and \.org\.uk domains\.\)

   1. On the **Registered Domains >** *domain name* page, at **IPS Tag**, choose **Change IPS Tag**, and specify the value that you got in step a\.

   1. Choose **Update**\.

1. If you're not currently using Route 53 as the DNS service provider for your domain, skip to step 12\.

   If you are currently using Route 53 as the DNS service provider for the domain, perform the following steps:

   1. Choose **Hosted Zones\.**

   1. Choose the name of the hosted zone for your domain\. The domain and the hosted zone have the same name\.

   1. *If you want to continue using Route 53 as the DNS service provider for the domain:* Find the NS record for the hosted zone, and make note of the names of the four name servers\. These names all begin with **ns\-**\.

      *If you do not want to continue using Route 53 as the DNS service provider for the domain:* Make note of the settings for all of your records except the NS and SOA records\. For Route 53–specific features such as alias records, you'll need to work with your new DNS service provider to determine how to achieve comparable functionality\.

1. If you're transferring DNS service to another provider, use the methods that are provided by the new DNS service to create a hosted zone and records to reproduce the functionality of your Route 53 records\.

1. Use the process that is provided by the new registrar to request a transfer of the domain\.

   *All domains except \.uk, \.co\.uk, \.me\.uk, and \.org\.uk domains* – You'll be prompted to enter the authorization code that you got from the Route 53 console in step 9 of this procedure\.

   If you still want to use Route 53 as your DNS service provider, use the process that is provided by the new registrar to specify the names of the Route 53 name servers that you got in step 10\. If you want to use another DNS service provider, specify the names of the name servers that the new provider gave you when you created a new hosted zone in step 11\.

   Route 53 sends a confirmation email to the email address for the registrant contact for the domain:

   + If you don't respond to the email, the transfer happens automatically on the specified date\.

   + If you want the transfer to happen sooner or you want to cancel the transfer, choose the link in the email to go to the Route 53 website, and choose the applicable option\.

1. If you transferred DNS service to another DNS service provider, you can delete the records in the hosted zone and delete the hosted zone after DNS resolvers stop responding to DNS queries with the names of Route 53 name servers\. This typically takes two days, the amount of time that DNS resolvers commonly cache the names of name servers for a domain\.
**Important**  
If you delete the hosted zone while DNS resolvers are still responding to DNS queries with the names of Route 53 name servers, your domain will become unavailable on the internet\.

   After you delete the hosted zone, Route 53 will stop billing you the monthly charge for a hosted zone\. For more information, see the following documentation:

   + [Deleting Records](resource-record-sets-deleting.md)

   + [Deleting a Public Hosted Zone](DeleteHostedZone.md)

   + [Route 53 Pricing](https://aws.amazon.com/route53/pricing)