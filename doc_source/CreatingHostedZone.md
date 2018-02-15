# Creating a Public Hosted Zone<a name="CreatingHostedZone"></a>

A hosted zone is a collection of records for a specified domain\. You create a hosted zone for a domain \(such as example\.com\), and then you create records to tell the Domain Name System how you want traffic to be routed for that domain\.

When you create a hosted zone, Amazon Route 53 automatically creates a name server \(NS\) record and a start of authority \(SOA\) record for the zone\. The NS record identifies the four name servers that you give to your registrar or your DNS service so that DNS queries are routed to Route 53 name servers\. For more information about NS and SOA records, see [NS and SOA Records that Amazon Route 53 Creates for a Public Hosted Zone](SOA-NSrecords.md)\.

After you update the settings with your domain registrar to include the Route 53 name servers, Route 53 responds to DNS queries for the hosted zone even if you don't have a functioning website\. For example, Route 53 responds with information about your hosted zone whenever someone enters your domain name in a web browser\.

By default, Route 53 assigns a unique set of four name servers \(known collectively as a delegation set\) to each hosted zone that you create\. If you want to create a large number of hosted zones, you can use the Route 53 API to create a reusable delegation set\. Then when you create hosted zones by using the Route 53 API, you can assign the same reusable delegation set—the same four name servers—to each hosted zone\. \(You can't specify a reusable delegation set when you created a hosted zone by using the Route 53 console\.\) Reusable delegation sets simplify migrating DNS service to Route 53 because you can instruct your domain name registrar to use the same four name servers for all of the domains for which you want Route 53 to be the DNS service\. For more information about reusable delegation sets, see [Route 53 API Actions by Function](http://docs.aws.amazon.com/Route53/latest/APIReference/API-actions-by-function.html) in the *Amazon Route 53 API Reference*\. For information about creating hosted zones by using the Route 53 API, see [CreateHostedZone](http://docs.aws.amazon.com/Route53/latest/APIReference/API_CreateHostedZone.html)\.

You can create more than one hosted zone with the same name and add different records to each hosted zone\. Route 53 assigns four name servers to every hosted zone, and the name servers are different for each of them\. When you update your registrar's name server records, be careful to use the Route 53 name servers for the correct hosted zone—the one that contains the records that you want Route 53 to use when responding to queries for your domain\. Route 53 never returns values for records in other hosted zones that have the same name\.

**To create a hosted zone using the Route 53 console**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. If you're new to Route 53, choose **Get Started Now** under **DNS Management**\.

   If you're already using Route 53, choose **Hosted Zones** in the navigation pane\.

1. Choose **Create Hosted Zone**\.

1. In the **Create Hosted Zone** pane, enter a domain name and, optionally, a comment\. For more information about a setting, pause the mouse pointer over its label to see a tool tip\.

   For information about how to specify characters other than a\-z, 0\-9, and \- \(hyphen\) and how to specify internationalized domain names, see [DNS Domain Name Format](DomainNameFormat.md)\.

1. For **Type**, accept the default value of **Public Hosted Zone**\.

1. Choose **Create**\.