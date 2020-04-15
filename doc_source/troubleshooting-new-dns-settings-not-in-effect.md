# I changed DNS settings, but they haven't taken effect<a name="troubleshooting-new-dns-settings-not-in-effect"></a>

If you changed DNS settings, here are some common reasons that the changes haven't taken effect yet\.

**Topics**
+ [You transferred DNS service to Amazon Route 53 in the last 48 hours, so DNS is still using your previous DNS service](#troubleshooting-new-dns-settings-not-in-effect-recent-dns-transfer)
+ [You recently transferred DNS service to Amazon Route 53, but you didn't update the name servers with the domain registrar](#troubleshooting-new-dns-settings-not-in-effect-recent-transfer-wrong-name-servers)
+ [DNS resolvers still are using the old settings for the record](#troubleshooting-new-dns-settings-not-in-effect-cached-resource-record-set)
+ [You have more than one hosted zone with the same name, and you updated the one that isn't associated with the domain](#troubleshooting-new-dns-settings-not-in-effect-updated-wrong-hosted-zone)

## You transferred DNS service to Amazon Route 53 in the last 48 hours, so DNS is still using your previous DNS service<a name="troubleshooting-new-dns-settings-not-in-effect-recent-dns-transfer"></a>

When you transferred DNS service to Amazon Route 53, you used the method provided by the registrar for your domain to replace the name servers for the previous DNS service with the four name servers for Route 53\.

**Note**  
If you aren't sure you did this part, see [You recently transferred DNS service to Amazon Route 53, but you didn't update the name servers with the domain registrar](#troubleshooting-new-dns-settings-not-in-effect-recent-transfer-wrong-name-servers)\.

Domain registrars typically use a TTL \(time to live\) of 24 to 48 hours for name servers\. This means that when a DNS resolver gets the name servers for your domain, it uses that information for up to 48 hours before it submits another request for the current name servers for the domain\. If you transferred DNS service to Route 53 in the last 48 hours and then changed DNS settings, some DNS resolvers are still using your old DNS service to route traffic for the domain\.

## You recently transferred DNS service to Amazon Route 53, but you didn't update the name servers with the domain registrar<a name="troubleshooting-new-dns-settings-not-in-effect-recent-transfer-wrong-name-servers"></a>

The registrar for your domain has a variety of information about the domain, including the name servers for the DNS service for the domain\. Typically, the domain registrar is also your DNS service, so the name servers that are associated with your domain belong to the registrar\. These name servers tell DNS where to get information about how you want traffic for your domain to be routed, for example, to the IP address of a web server for your domain\.

When you transfer DNS service to Amazon Route 53, you need to use the method that is provided by your domain registrar to change the name servers that are associated with your domain\. You're usually replacing the name servers that are provided by the registrar with the four Route 53 name servers that are associated with the hosted zone that you created for the domain\.

If you created a new hosted zone and records for your domain and specified different settings than you used for the previous DNS service, and if DNS is still routing traffic to the old resources, it's possible that you didn't update the name servers with the domain registrar\. To determine whether the registrar is using the name servers for your Route 53 hosted zone and, if necessary, to update the name servers for the domain, perform the following procedure:<a name="troubleshooting-new-dns-settings-not-in-effect-recent-transfer-wrong-name-servers-procedure"></a>

**To get the name servers for your hosted zone and update the name server setting with the domain registrar**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Hosted Zones**\.

1. On the **Hosted Zones** page, choose the radio button \(not the name\) for the hosted zone\.
**Important**  
If you have more than one hosted zone with the same name, make sure you're getting the name servers for the correct hosted zone\.

1. In the right pane, make note of the four servers listed for **Name Servers**\.

1. Using the method provided by the registrar for the domain, display the list of name servers for the domain\.

1. If the name servers for the domain match the name servers that you got in step 4, then the domain configuration is correct\.

   If the name servers for the domain don't match the name servers that you got in step 4, update the domain to use the Route 53 name servers\.

**Important**  
When you change the name servers for the domain to the name servers from your Route 53 hosted zone, it can take up to two days for the change to take effect and for Route 53 to become your DNS service\. This is because DNS resolvers across the internet typically request the name servers only once every two days and cache the answer\.

## DNS resolvers still are using the old settings for the record<a name="troubleshooting-new-dns-settings-not-in-effect-cached-resource-record-set"></a>

If you changed the settings in a record but your traffic is still being routed to the old resource, such as a web server for your website, one possible cause is that DNS still has the previous settings cached\. Each record has a TTL \(time to live\) value that specifies how long, in seconds, that you want DNS resolvers to cache the information in the record, such as the IP address for a web server\. Until the amount of time that is specified by the TTL passes, DNS resolvers will continue to return the old value in response to DNS queries\. If you want to know what the TTL is for a record, perform the following procedure\.

**Note**  
For alias records, the TTL is determined by the AWS resource that the record routes traffic to\. For more information, see [Choosing between alias and non\-alias records](resource-record-sets-choosing-alias-non-alias.md)\.<a name="troubleshooting-new-dns-settings-not-in-effect-cached-resource-record-set-procedure"></a>

**To view the TTL for a record**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. On the **Hosted Zones** page, choose the name of the hosted zone that includes the record\.

1. In the list of records, find the record that you want the TTL value for, and check the value of the **TTL** column\.
**Note**  
Changing the TTL now won't make your change take effect faster\. DNS resolvers already have the value cached, and they won't get the new setting until the amount of time that was specified by the old setting passes\.

## You have more than one hosted zone with the same name, and you updated the one that isn't associated with the domain<a name="troubleshooting-new-dns-settings-not-in-effect-updated-wrong-hosted-zone"></a>

You can create more than one hosted zone that has the same name, either using the same account or using multiple accounts\. To specify the hosted zone that Route 53 uses to route internet traffic for your domain, you get the four Route 53 name servers for that hosted zone, and you update the domain registration to use those name servers\. 

If you add, change, or delete records in one hosted zone but your domain registration is using the name servers for another hosted zone, Route 53 responses to DNS queries won't reflect your changes\. To determine whether your domain registration is using the name servers for the hosted zone that you updated records in, perform the following tasks: 

1. Determine which name servers are associated with your domain registration\. See [Adding or changing name servers or glue records](domain-name-servers-glue-records.md#domain-name-servers-glue-records-adding-changing)\.

1. Compare the name servers that you got in step 1 with the name servers that Route 53 assigned to the hosted zone that you updated records in\. See [Getting the name servers for a public hosted zone](GetInfoAboutHostedZone.md)\.

If the name servers for the domain registration don't match the name servers for the hosted zone that you updated records in, you have two options:

**Change records in the hosted zone that's currently associated with the domain \(recommended\)**  
Make note of the changes that you made in the hosted zone that is not currently associated with your domain registration\. Then go to the hosted zone that is associated with the domain registration, and make the same changes\. This is the preferred method because the changes take effect almost immediately\. For more information, see [Editing records](resource-record-sets-editing.md)\.

**Update your domain registration to use different name servers**  
Change your domain registration to use the name servers in the hosted zone that you updated\.  
If you change the name servers that are associated with your domain registration, your domain will be unavailable on the internet for up to 2 days\. This is because DNS resolvers typically cache the names of name servers for 2 days\. For an overview of how DNS works, including information about resolver caching, see [How Amazon Route 53 routes traffic for your domain](welcome-dns-service.md#welcome-dns-service-how-route-53-routes-traffic)\. 
By changing the name servers that are associated with your domain registration, you're essentially changing the DNS service for the domain\. You have two options, depending on whether the domain is currently in use:  
+ **If the domain is in use**, see [Making Route 53 the DNS service for a domain that's in use](migrate-dns-domain-in-use.md)\.
+ **If the domain is currently inactive**, perform the following tasks:

  1. Get the name servers for the hosted zone that you want to use to route traffic to your domain\. See [Getting the name servers for a public hosted zone](GetInfoAboutHostedZone.md)\.

  1. In the hosted zone that you got name servers for in step 1, confirm that the NS record is using the same four name servers\. If not, update the NS record\. See [Editing records](resource-record-sets-editing.md)\.

  1. Update the domain registration to use the name servers that you got in step 1\. See [Adding or changing name servers or glue records](domain-name-servers-glue-records.md#domain-name-servers-glue-records-adding-changing)\. 