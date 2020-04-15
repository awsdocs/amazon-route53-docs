# My domain is unavailable on the internet<a name="troubleshooting-domain-unavailable"></a>

Here are the most common reasons that your domain is not available on the internet\.

**Topics**
+ [You registered a new domain, but you didn't click the link in the confirmation email](#troubleshooting-domain-unavailable-didnt-click-link)
+ [You transferred domain registration to Amazon Route 53, but you didn't transfer DNS service](#troubleshooting-domain-unavailable-transferred-domain-not-dns)
+ [You transferred domain registration and specified the wrong name servers in the domain settings](#troubleshooting-domain-unavailable-transferred-domain-wrong-name-servers)
+ [You transferred DNS service first, but you didn't wait long enough before transferring domain registration](#troubleshooting-domain-unavailable-transferred-domain-too-soon-after-dns-transfer)
+ [You deleted the hosted zone that Route 53 is using to route internet traffic for the domain](#troubleshooting-domain-unavailable-deleted-hosted-zone)
+ [Your domain has been suspended](#troubleshooting-domain-unavailable-suspended)

## You registered a new domain, but you didn't click the link in the confirmation email<a name="troubleshooting-domain-unavailable-didnt-click-link"></a>

When you register a new domain, ICANN requires that we get confirmation that the email address for the registrant contact is valid\. To get confirmation, we send an email that contains a link\. \(If you don't respond to the first email, we resend the same email up to two more times\.\) You have between 3 and 15 days to click the link, depending on the top\-level domain\. After that time, the link stops working\.

If you don't click the link in the email in the allotted amount of time, ICANN requires that we suspend the domain\. For information about how to resend the confirmation email to the registrant contact, see [Resending authorization and confirmation emails](domain-click-email-link.md)\.

## You transferred domain registration to Amazon Route 53, but you didn't transfer DNS service<a name="troubleshooting-domain-unavailable-transferred-domain-not-dns"></a>

If your previous registrar offered free DNS service with domain registration, the registrar might have stopped providing DNS service when you transferred domain registration to Route 53\. Perform the following procedure to determine whether this is the problem and, if so, to resolve it\.<a name="troubleshooting-domain-unavailable-transferred-domain-not-dns-procedure"></a>

**To restore DNS service if your previous registrar canceled it after you transferred domain registration to Route 53**

1. Contact your previous registrar and confirm that they canceled DNS service for your domain\. If so, here are the three quickest ways to restore DNS service for the domain, in order of desirability:
   + If the previous registrar provides paid DNS service, ask them to restore DNS service using the old DNS records and name servers for your domain\. 
   + If the previous registrar doesn't provide paid DNS service without domain registration, ask whether you can transfer domain registration back to them and have them restore DNS service using the old DNS records and name servers for your domain\. 
   + If you can transfer domain registration back to the previous registrar but they don't have your DNS records any longer, ask whether you can transfer domain registration back to them and get the same set of name servers that were formerly assigned to the domain\. If this is possible, you'll have to recreate your old DNS records yourself\. However, as soon as you do that, your domain will become available again\.

   If your previous registrar can't help with any of these options, continue with step 2\.
**Important**  
If you can't restore DNS service using the name servers that you specified when you transferred your domain to Route 53, it can take up to two days after you complete the remaining steps in this procedure for your domain to become available again on the internet\. DNS resolvers typically cache the names of the name servers for a domain for 24 to 48 hours, and it will take that long before all DNS resolvers get the names of the new name servers\.

1. Choose a new DNS service, for example, Route 53\.

1. Using the method provided by the new DNS service, create a hosted zone and records:

   1. Create a hosted zone that has the same name as your domain, such as example\.com\.

   1. Use the zone file that you got from the previous registrar to create records\.

   If you chose Route 53 as your new DNS service, you can create records by importing the zone file\. For more information, see [Creating records by importing a zone file](resource-record-sets-creating-import.md)\.

1. Get the name servers for the new hosted zone\. If you chose Route 53 as the DNS service, see [Getting the name servers for a public hosted zone](GetInfoAboutHostedZone.md)\.

1. Change the name servers for your domain to the name servers that you got in step 4\. For more information, see [Adding or changing name servers and glue records for a domain](domain-name-servers-glue-records.md)\.

## You transferred domain registration and specified the wrong name servers in the domain settings<a name="troubleshooting-domain-unavailable-transferred-domain-wrong-name-servers"></a>

When you transfer domain registration to Amazon Route 53, one of the settings that you specify for the domain is the set of name servers that will respond to DNS queries for the domain\. These name servers come from the hosted zone that has the same name as the domain\. The hosted zone contains information about how you want to route traffic for the domain, such as the IP address of a web server for www\.example\.com\.

You might have accidentally specified the name servers for the wrong hosted zone, which is especially easy if you have more than one hosted zone that has the same name as the domain\. To confirm that the domain is using the name servers for the correct hosted zone and, if necessary, update the name servers for the domain, perform the following procedures\.

**Important**  
If you specified the wrong name server records when you transferred the domain to Route 53, it can take up to two days after you correct the name servers for the domain before DNS service is fully restored\. This is because DNS resolvers across the internet typically request the name servers only once every two days and cache the answer\.<a name="troubleshooting-domain-unavailable-transferred-domain-wrong-name-servers-procedure-1"></a>

**To get the name servers for your hosted zone**

1. If you're using another DNS service for the domain, use the method provided by the DNS service to get the name servers for the hosted zone\. Then skip to the next procedure\.

   If you're using Route 53 as the DNS service for the domain, sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Hosted Zones**\.

1. On the **Hosted Zones** page, choose the radio button \(not the name\) for the hosted zone\.
**Important**  
If you have more than one hosted zone with the same name, make sure you're getting the name servers for the correct hosted zone\.

1. In the right pane, make note of the four servers listed for **Name Servers**\.<a name="troubleshooting-domain-unavailable-transferred-domain-wrong-name-servers-procedure-2"></a>

**To confirm that the domain is using the correct name servers**

1. If you're using another DNS service for the domain, sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)

   If you're using Route 53, skip to the next step\.

1. In the navigation pane, choose **Registered Domains**\.

1. Choose the name of the domain for which you want to edit settings\.

1. Choose **Add or Edit Name Servers**\.

1. Compare the list of name servers that you got in the previous procedure with the name servers that are listed in the **Edit Name Servers for** *domain name* dialog box\.

1. If the name servers listed here don't match the name servers that you got in the previous procedure, change the name servers here, and then choose **Update**\.

## You transferred DNS service first, but you didn't wait long enough before transferring domain registration<a name="troubleshooting-domain-unavailable-transferred-domain-too-soon-after-dns-transfer"></a>

When you transferred DNS service to Amazon Route 53 or another DNS service, you updated the configuration for your domain with the domain registrar to use the name servers for the new DNS service\.

DNS resolvers, which respond to requests for your domain, commonly cache the names of name servers for 24 to 48 hours\. If you change the DNS service for a domain and replace the name servers from one DNS service with the name servers for another DNS service, it can take up to 48 hours before DNS resolvers start using the new name servers and, therefore, the new DNS service\.

Here's how transferring your DNS service and then transferring your domain too soon after can cause your domain to become unavailable on the internet:

1. You transferred DNS service for your domain\.

1. You transferred your domain to Route 53 before DNS resolvers started to use the name servers for your new DNS service\.

1. Your previous registrar canceled DNS service for your domain as soon as the domain was transferred to Route 53\.

1. DNS resolvers are still routing queries to your old DNS service, but there are no longer any records that tell how to route your traffic\.

When caching expires for the name servers for the old DNS service, DNS will start to use your new DNS service\. Unfortunately, there is no way to accelerate this process\.

## You deleted the hosted zone that Route 53 is using to route internet traffic for the domain<a name="troubleshooting-domain-unavailable-deleted-hosted-zone"></a>

If Route 53 is the DNS service for your domain and if you delete the hosted zone that is used to route internet traffic for the domain, the domain will become unavailable on the internet\. This is true regardless of whether the domain is registered with Route 53\.

**Important**  
Restoring internet service for the domain can take up to 48 hours\.<a name="troubleshooting-domain-unavailable-deleted-hosted-zone-procedure"></a>

**To restore internet service if you delete a hosted zone that Route 53 is using to route internet traffic for a domain**

1. Create another hosted zone that has the same name as the domain\. For more information, see [Creating a public hosted zone](CreatingHostedZone.md)\.

1. Recreate the records that were in the hosted zone that you deleted\. For more information, see [Working with records](rrsets-working-with.md)\.

1. Get the names of the name servers that Route 53 assigned to the new hosted zone\. For more information, see [Getting the name servers for a public hosted zone](GetInfoAboutHostedZone.md)\.

1. Update the domain registration to use the name servers that you got in step 3:
   + If the domain is registered with Route 53, see [Adding or changing name servers and glue records for a domain](domain-name-servers-glue-records.md)\.
   + If the domain is registered with another domain registrar, use the method provided by the registrar to update the domain registration to use the new name servers\.

1. Wait for the TTL for the name servers to pass for recursive resolvers that have cached the names of the name servers for the deleted hosted zone\. After the TTL has passed, when a browser or application submits a DNS query for the domain or one of its subdomains, a recursive resolver forwards the query to the Route 53 name servers for the new hosted zone\. For more information, see [How Amazon Route 53 routes traffic for your domain](welcome-dns-service.md#welcome-dns-service-how-route-53-routes-traffic)\.

   The TTL for name servers can be as long as 48 hours, depending on the TLD of the domain\.

## Your domain has been suspended<a name="troubleshooting-domain-unavailable-suspended"></a>

Your domain might be unavailable on the internet because we had to suspend it\. For more information, see [My domain is suspended \(status is ClientHold\)](troubleshooting-domain-suspended.md)\.