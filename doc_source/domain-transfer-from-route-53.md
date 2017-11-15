# Transferring a Domain from Amazon Route 53 to Another Registrar<a name="domain-transfer-from-route-53"></a>

When you transfer a domain from Amazon Route 53 to another registrar, you get some information from Amazon Route 53 and provide it to the new registrar\. The new registrar will do the rest\.

**Important**  
If you're currently using Amazon Route 53 as your DNS service provider and you also want to transfer DNS service to another provider, be aware that the following Amazon Route 53 features don't have direct parallels with features provided by other DNS service providers\. You'll need to work with the new DNS service provider to determine how to achieve comparable functionality:  
Alias resource record sets
Weighted resource record sets
Latency resource record sets
Failover resource record sets
Geo resource record sets

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

**To transfer a domain from Amazon Route 53 to another registrar**

1. *\.fi domains only* – If you're transferring a \.fi domain to another registrar, order an authorization key from the Finnish Communications Regulatory Authority, the registry for \.fi domains\. You use the authorization key later in this process\. For more information, see [Ordering of authorization key](https://domain.fi/info/en/index/yllapito/valtuutusavain/valtuutusavaimentilaus.html) on the Finnish Communications Regulatory Authority website\.
**Important**  
The Finnish Communications Regulatory Authority mails the authorization key to you, which can take two weeks or more\. Do not continue with this procedure until you have the key\.

1. Sign in to the AWS Management Console and open the Amazon Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Registered Domains**\.

1. Choose the name of the domain that you want to transfer to another registrar\.

1. On the **Your Domains > ** *domain name* page, check the value of **Domain name status**\. If it is one of the following values, you can't currently transfer the domain: 

   + pendingDelete

   + pendingTransfer

   + redemptionPeriod

   + clientTransferProhibited

   For a current list of domain name status codes and an explanation of what each code means, go to the [ICANN website](https://www.icann.org/) and search for **epp status codes**\. \(Search on the ICANN website; web searches sometimes return an old version of the document\.\)

1. If the value of **Transfer lock** is **Enabled**, choose **Disable\.**

1. Choose **Edit contacts**\.

1. On the **Edit Contact Details for ** *domain name* page, for **Privacy Protection**, select **Don't hide contact information** for all contacts\.

   In addition, update the contact information so the new registrar can contact you\.

1. Choose **Save**\.

1. *All domains except \.co\.uk, \.me\.uk, \.org\.uk, and \.fi domains* – On the **Your Domains >** *domain name* page, at **Authorization Code**, choose **Generate** and make note of the authorization code\. You'll provide this value to your registrar later in this procedure\.

   *\.co\.uk, \.me\.uk, and \.org\.uk domains* – Change the IPS tag to the value for the new registrar:

   1. Go to the [Find a Registrar](http://www.nominet.uk/registrar-list/) page on the Nominet website, and find the IPS tag for the new registrar\. \(Nominet is the registry for \.co\.uk, \.me\.uk, and \.org\.uk domains\.\)

   1. On the **Your Domains** > *domain name* page, at **IPS Tag**, choose **Change IPS Tag**, and specify the value that you got in step a\.

   1. Choose **Update**\.

   *\.fi domains* – Skip this step\.

1. If you're not currently using Amazon Route 53 as the DNS service provider for your domain, skip to step 13\.

   If you are currently using Amazon Route 53 as the DNS service provider for the domain, perform the following steps:

   1. Choose **Hosted Zones\.**

   1. Double\-click the name of the hosted zone for your domain\. The domain and the hosted zone have the same name\.

   1. *If you want to continue using Amazon Route 53 as the DNS service provider for the domain:* Find the NS record for the hosted zone, and make note of the names of the four name servers\. These names all begin with **ns\-**\.

      *If you do not want to continue using Amazon Route 53 as the DNS service provider for the domain:* Make note of the settings for all of your resource record sets except the NS and SOA records\. For Amazon Route 53–specific features such as alias resource record sets, you'll need to work with your new DNS service provider to determine how to achieve comparable functionality\.

1. If you're transferring DNS service to another provider, use the methods that are provided by the new DNS service to create a hosted zone and resource record sets to reproduce the functionality of your Amazon Route 53 resource record sets\.

1. Using the process that is provided by the new registrar, request a transfer of the domain\.

   *All domains except \.co\.uk, \.me\.uk, \.org\.uk, and \.fi domains* – You'll be prompted to enter the authorization code that you got from the Amazon Route 53 console in step 10 of this procedure\.

   If you still want to use Amazon Route 53 as your DNS service provider, specify the names of the Amazon Route 53 name servers that you got in step 11\. If you want to use another DNS service provider, specify the names of the name servers that the new provider gave you when you created a new hosted zone in step 12\.

   *\.fi domains* – Go to the Finnish Communications Regulatory Authority website and request a transfer\. For more information, see the procedure "Domain name transfer made by domain name holder" on the [Transfer of domain name to new holder](https://domain.fi/info/en/index/yllapito/siirtaminen.html) page\.