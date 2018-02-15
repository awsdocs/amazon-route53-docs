# Getting the Name Servers for a Public Hosted Zone<a name="GetInfoAboutHostedZone"></a>

If you're currently using another DNS service and you want to migrate to Amazon Route 53, you begin by creating a hosted zone\. Route 53 automatically assigns four name servers to your hosted zone\. To ensure that the Domain Name System routes queries for your domain to the Route 53 name servers, update your registrar's or your DNS service's NS records for the domain to replace the current name servers with the names of the four Route 53 name servers for your hosted zone\. The method that you use to update the NS records depends on which registrar or DNS service you're using\. For more information about migrating your DNS service to Route 53, see [Using Amazon Route 53 as the DNS Service for Subdomains Without Migrating the Parent Domain](creating-migrating.md)\.

**Note**  
Some registrars only allow you to specify name servers using IP addresses; they don't allow you to specify fully qualified domain names\. If your registrar requires using IP addresses, you can get the IP addresses for your name servers using the dig utility \(for Mac, Unix, or Linux\) or the nslookup utility \(for Windows\)\. We rarely change the IP addresses of name servers; if we need to change IP addresses, we'll notify you in advance\.

The following procedure explains how to get the name servers for a hosted zone using the Route 53 console\. For information about how to get name servers using the Route 53 API, see [GetHostedZone](http://docs.aws.amazon.com/Route53/latest/APIReference/API_GetHostedZone.html) in the *Amazon Route 53 API Reference*\. 

**To get the name servers for a hosted zone using the Route 53 console**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, click **Hosted Zones**\.

1. On the **Hosted Zones** page, choose the radio button \(not the name\) for the hosted zone\.

1. In the right pane, make note of the four servers listed for **Name Servers**\.