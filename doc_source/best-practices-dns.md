# Best practices for Amazon Route 53 DNS<a name="best-practices-dns"></a>

Follow these best practices to get the best results when using Route 53 DNS service\.

**Use the data plane functions for DNS failover and app recovery**  
The data planes for Route 53, including health checks, and Amazon Route 53 Application Recovery Controller routing control are globally distributed, and are designed for 100% availability and functionality, even during severe events\. They integrate with each other and don't depend on control plane functionality\. While the control planes for these services, including their consoles, are generally very reliable, they're designed in a more centralized way and prioritize durability and consistency rather than high availability\. For scenarios such as failover during disaster recovery, we recommend that you use features like Route 53 health checks and Route 53 ARC that rely on data plane functionality to update DNS\. For more information, see [Creating Disaster Recovery Mechanisms Using Amazon Route 53](http://aws.amazon.com/blogs/networking-and-content-delivery/creating-disaster-recovery-mechanisms-using-amazon-route-53/)\.

**Choosing TTL values for DNS records**  
The DNS TTL is the numeric value \(in seconds\) that DNS resolvers use to decide how long a record may be cached for without making another query to Route 53\. All DNS records must specify a TTL\. The recommended range for TTlL values is 60 to 172,800 seconds\.  
The choice of a TTL is a trade\-off between latency and reliability, and responsiveness to change\. With shorter TTLs on a record, DNS resolvers will notice updates to the record quicker as they must query more frequently\. This will increase the query volume \(and cost\)\. As you lengthen the TTL, DNS resolvers answer queries from cache more often which is typically faster, cheaper, and in some situations more reliable because it avoids queries across the internet\. There is no correct value, but it is worthwhile to think about whether responsiveness or reliability is more important to you\.  
Things to consider while setting TTL values:  
+ Set DNS record TTLs as long as you can afford to wait for a change to take effect\. This is especially true on delegations \(NS recordsets\), or other records that rarely change, for example MX records\. For these records longer TTLs are preferred\. Between an hour \(3600s\) or a day \(86,400s\) is a common choice\.
+ For records that need to be altered as part of a rapid failover mechanism \(especially records that are health checked\), lower TTLs are appropriate\. 60 or 120 seconds are common choices\.
+ When you make changes to critical DNS entries, it is advisable to temporarily shorten the TTLs, so that you can make the change, observe and then rollback quickly if you need to\. Once the change is in place and working as expected, you can raise the TTL to a longer value\.
For more information see [TTL \(seconds\)](resource-record-sets-values-shared.md#rrsets-values-common-ttl)\.

**CNAME records**  
   
CNAME records in DNS are a way to point one domain name at another\. If a DNS resolver resolves domain\-1\.example\.com and finds a CNAME pointing at domain\-2\.example\.net, the DNS resolver must proceed to resolve domain\-2\.example\.net before it can respond\. These records are useful in many situations, for example, to ensure consistency when a website has more than one domain name\.   
However, DNS resolvers must make more queries to answer CNAMEs, which increases latency and costs\. Where possible, a faster and cheaper alternative is to use a Route 53 ALIAS record\. Aliases allow Route 53 to respond with the direct answer for AWS resources \(for example, Elastic Load Balancing\) and for other domains within the same hosted zone\.  
For more information, see [Routing internet traffic to your AWS resources](routing-to-aws-resources.md)\.

**Advanced DNS routing**  
+ When using geolocation, geoproximity or latency\-based routing, always set a default, unless you want some clients to receive *no answer* responses\.
+ To minimize application latency, use latency\-based routing\. This type of routing data can change frequently\.
+ To provide routing stability and predictability, use either geolocation or geoproximity routing\.
For more information, see [Geolocation routing](routing-policy.md#routing-policy-geo), [Geoproximity routing \(traffic flow only\)](routing-policy.md#routing-policy-geoproximity), and [Latency\-based routing](routing-policy.md#routing-policy-latency)\.

**Confirm DNS changes\.**  
When you create or update a record by using the Route 53 console or API, it takes some time for the change to be reflected across the internet\. This is called *change propagation*\. While propagation is typically under one minute globally, there're occasionally cases where a change can be delayed, for example, due to problems syncing to one location, or in rare cases, problems within the central control plane\. Use the [GetChange](https://docs.aws.amazon.com/Route53/latest/APIReference/API_GetChange.html) API to verify your DNS changes have gone into effect \(`Status =INSYNC`\) if you are building automated provisioning work flows, and it is important to wait for change propagation to complete before moving forward with the next work flow step\.

**DNS delegation**  
When you delegate multiple levels of subdomains in DNS, it is important to always delegate from the parent zone\. For example, if you are delegating www\.dept\.example\.com you should do so from the dept\.example\.com zone, not from the example\.com zone\. Delegations from a *grandparent* to a *child* zone may not work at all or work only inconsistently\. For more information, see [Routing traffic for subdomains](dns-routing-traffic-for-subdomains.md)\.

**Size of DNS response**  
Avoid creating large single responses\. Above 512 bytes, many DNS resolvers must retry over TCP instead of UDP, , which can lead to slower responses and reduced reliability\. We recommend using multi\-value answers which chooses 8 healthy, random IPs to keep responses within the 512 byte boundary\.  
For more information, see [Multivalue answer routing](routing-policy.md#routing-policy-multivalue) and [DNS Reply Size Test Server](https://www.dns-oarc.net/oarc/services/replysizetest/)\.