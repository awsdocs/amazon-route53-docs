# Considerations when working with public hosted zones<a name="hosted-zone-public-considerations"></a>

Note the following considerations when working with public hosted zones:

**NS and SOA records**  
When you create a hosted zone, Amazon Route 53 automatically creates a name server \(NS\) record and a start of authority \(SOA\) record for the zone\. The NS record identifies the four name servers that you give to your registrar or your DNS service so that DNS queries are routed to Route 53 name servers\. For more information about NS and SOA records, see [NS and SOA records that Amazon Route 53 creates for a public hosted zone](SOA-NSrecords.md)\.

**Multiple hosted zones that have the same name**  
You can create more than one hosted zone that has the same name and add different records to each hosted zone\. Route 53 assigns four name servers to every hosted zone, and the name servers are different for each of them\. When you update your registrar's name server records, be careful to use the Route 53 name servers for the correct hosted zone—the one that contains the records that you want Route 53 to use when responding to queries for your domain\. Route 53 never returns values for records in other hosted zones that have the same name\.

**Reusable delegation sets**  
By default, Route 53 assigns a unique set of four name servers \(known collectively as a delegation set\) to each hosted zone that you create\. If you want to create a large number of hosted zones, you can create a reusable delegation set programmatically\. \(Reusable delegation sets aren't available in the Route 53 console\.\) Then you can create hosted zones programmatically and assign the same reusable delegation set—the same four name servers—to each hosted zone\.   
Reusable delegation sets simplify migrating DNS service to Route 53 because you can instruct your domain name registrar to use the same four name servers for all of the domains for which you want to use Route 53 as the DNS service\. For more information, see [CreateReusableDelegationSet](https://docs.aws.amazon.com/Route53/latest/APIReference/API_CreateReusableDelegationSet.html) in the *Amazon Route 53 API Reference*\.