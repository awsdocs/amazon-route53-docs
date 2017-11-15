# Values for Weighted Resource Record Sets<a name="resource-record-sets-values-weighted"></a>

When you create weighted resource record sets, you specify the following values:


+ [Name](#rrsets-values-weighted-name)
+ [Type](#rrsets-values-weighted-type)
+ [Alias](#rrsets-values-weighted-alias)
+ [TTL \(Time to Live\)](#rrsets-values-weighted-ttl)
+ [Value](#rrsets-values-weighted-value)
+ [Routing Policy](#rrsets-values-weighted-routing-policy)
+ [Weight](#rrsets-values-weighted-weight)
+ [Set ID](#rrsets-values-weighted-set-identifier)
+ [Associate with Health Check/Health Check to Associate](#rrsets-values-weighted-associate-with-health-check)

## Name<a name="rrsets-values-weighted-name"></a>

Enter the name of the domain or subdomain that you want to route traffic for\. The default value is the name of the hosted zone\. 

**Note**  
If you're creating a resource record set that has the same name as the hosted zone, don't enter a value \(for example, an @ symbol\) in the **Name** field\. 

Enter the same name for all of the resource record sets in the group of weighted resource record sets\. 

**CNAME resource record sets**  
If you're creating a resource record set that has a value of **CNAME** for **Type**, the name of the resource record set can't be the same as the name of the hosted zone\.

**Special characters**  
For information about how to specify characters other than a\-z, 0\-9, and \- \(hyphen\) and how to specify internationalized domain names, see [DNS Domain Name Format](DomainNameFormat.md)\.

**Wildcard characters**  
You can use an asterisk \(\*\) character in the name\. DNS treats the \* character either as a wildcard or as the \* character \(ASCII 42\), depending on where it appears in the name\. For more information, see [Using an Asterisk \(\*\) in the Names of Hosted Zones and Resource Record Sets](DomainNameFormat.md#domain-name-format-asterisk)\.

## Type<a name="rrsets-values-weighted-type"></a>

The DNS record type\. For more information, see [Supported DNS Record Types](ResourceRecordTypes.md)\.

Select the same value for all of the resource record sets in the group of weighted resource record sets\.

## Alias<a name="rrsets-values-weighted-alias"></a>

Select **No**\. 

## TTL \(Time to Live\)<a name="rrsets-values-weighted-ttl"></a>

The amount of time, in seconds, that you want DNS recursive resolvers to cache information about this resource record set\. If you specify a longer value \(for example, 172800 seconds, or two days\), you pay less for Amazon Route 53 service because recursive resolvers send requests to Amazon Route 53 less often\. However, it takes longer for changes to the resource record set \(for example, a new IP address\) to take effect because recursive resolvers use the values in their cache for longer periods instead of asking Amazon Route 53 for the latest information\. 

If you're associating this resource record set with a health check, we recommend that you specify a TTL of 60 seconds or less so clients respond quickly to changes in health status\.

You must specify the same value for **TTL** for all of the resource record sets in this group of weighted resource record sets\.

If a group of weighted resource record sets includes one or more weighted alias resource record sets that are routing traffic to an ELB load balancer, we recommend that you specify a TTL of 60 seconds for all of the non\-alias weighted resource record sets that have the same name and type\. Values other than 60 seconds \(the TTL for load balancers\) will change the effect of the values that you specify for **Weight**\.

## Value<a name="rrsets-values-weighted-value"></a>

Enter a value that is appropriate for the value of **Type**\. For all types except **CNAME**, you can enter more than one value\. Enter each value on a separate line\.

**A — IPv4 address**  
An IP address in IPv4 format, for example, **192\.0\.2\.235**\.

**AAAA — IPv6 address**  
An IP address in IPv6 format, for example, **2001:0db8:85a3:0:0:8a2e:0370:7334**\.

**CAA — Certificate Authority Authorization**  
Three space\-separated values that control which certificate authorities are allowed to issue certificates or wildcard certificates for the domain or subdomain that is specified by **Name**\. You can use CAA records to specify the following:  

+ Which certificate authorities \(CAs\) can issue SSL/TLS certificates, if any

+ The email address or URL to contact when a CA issues a certificate for the domain or subdomain

**CNAME — Canonical name**  
The fully qualified domain name \(for example, *www\.example\.com*\) that you want Amazon Route 53 to return in response to DNS queries for this resource record set\. A trailing dot is optional; Amazon Route 53 assumes that the domain name is fully qualified\. This means that Amazon Route 53 treats *www\.example\.com* \(without a trailing dot\) and *www\.example\.com\.* \(with a trailing dot\) as identical\.

**MX — Mail exchange**  
A priority and a domain name that specifies a mail server, for example, **10 mailserver\.example\.com**\.

**NAPTR — Name Authority Pointer**  
Six space\-separated settings that are used by Dynamic Delegation Discovery System \(DDDS\) applications to convert one value to another or to replace one value with another\. For more information, see [NAPTR Format](ResourceRecordTypes.md#NAPTRFormat)\.

**PTR — Pointer**  
The domain name that you want Amazon Route 53 to return\.

**SPF — Sender Policy Framework**  
An SPF record enclosed in quotation marks, for example, **"v=spf1 ip4:192\.168\.0\.1/16\-all"**\. SPF records are not recommended\. For more information, see [Supported DNS Record Types](ResourceRecordTypes.md)\.

**SRV — Service locator**  
An SRV record\. For information about SRV record format, refer to the applicable documentation\. The format of an SRV record is:  
**\[priority\] \[weight\] \[port\] \[server host name\]**  
For example:  
**1 10 5269 xmpp\-server\.example\.com\.**

**TXT — Text**  
A text record\. Enclose text in quotation marks, for example, **"Sample Text Entry"**\. 

## Routing Policy<a name="rrsets-values-weighted-routing-policy"></a>

Select **Weighted**\.

## Weight<a name="rrsets-values-weighted-weight"></a>

A value that determines the proportion of DNS queries that Amazon Route 53 responds to using the current resource record set\. Amazon Route 53 calculates the sum of the weights for the resource record sets that have the same combination of DNS name and type\. Amazon Route 53 then responds to queries based on the ratio of a resource's weight to the total\. 

You can't create non\-weighted resource record sets that have the same values for **Name** and **Type** as weighted resource record sets\.

Enter an integer between 0 and 255\. To disable routing to a resource, set **Weight** to 0\. If you set **Weight** to 0 for all of the resource record sets in the group, traffic is routed to all resources with equal probability\. This ensures that you don't accidentally disable routing for a group of weighted resource record sets\.

The effect of setting **Weight** to 0 is different when you associate health checks with weighted resource record sets\. For more information, see [Configuring Active\-Active or Active\-Passive Failover by Using Amazon Route 53 Weighted and Weighted Alias Records](dns-failover-configuring-options.md#dns-failover-weighted-rrsets)\.

## Set ID<a name="rrsets-values-weighted-set-identifier"></a>

Enter a value that uniquely identifies this resource record set in the group of weighted resource record sets\.

## Associate with Health Check/Health Check to Associate<a name="rrsets-values-weighted-associate-with-health-check"></a>

Select **Yes** if you want Amazon Route 53 to check the health of a specified endpoint and to respond to DNS queries using this resource record set only when the endpoint is healthy\. Then select the health check that you want Amazon Route 53 to perform for this resource record set\. 

Amazon Route 53 doesn't check the health of the endpoint specified in the resource record set, for example, the endpoint specified by the IP address in the **Value** field\. When you select a health check for a resource record set, Amazon Route 53 checks the health of the endpoint that you specified in the health check\. For information about how Amazon Route 53 determines whether an endpoint is healthy, see [How Amazon Route 53 Determines Whether an Endpoint Is Healthy](dns-failover-determining-health-of-endpoints.md)\.

Associating a health check with a resource record set is useful only when Amazon Route 53 is choosing between two or more resource record sets to respond to a DNS query, and you want Amazon Route 53 to base the choice in part on the status of a health check\. Use health checks only in the following configurations:

+ You're checking the health of all of the resource record sets in a group of failover, geolocation, latency, multivalue, or weighted resource record sets, and you specify health check IDs for all the resource record sets\. If the health check for a resource record set specifies an endpoint that is not healthy, Amazon Route 53 stops responding to queries using the value for that resource record set\.

+ You select **Yes** for **Evaluate Target Health** for an alias resource record set or the resource record sets in a group of failover alias, geolocation alias, latency alias, or weighted alias resource record set\. If the alias resource record sets reference non\-alias resource record sets in the same hosted zone, you must also specify health checks for the referenced resource record sets\. 

For geolocation resource record sets, if an endpoint is unhealthy, Amazon Route 53 looks for a resource record set for the larger, associated geographic region\. For example, suppose you have resource record sets for a state in the United States, for the United States, for North America, and for all locations \(**Location** is **Default**\)\. If the endpoint for the state resource record set is unhealthy, Amazon Route 53 checks the resource record sets for the United States, for North America, and for all locations, in that order, until it finds a resource record set that has a healthy endpoint\.

If your health checks specify the endpoint only by domain name, we recommend that you create a separate health check for each endpoint\. For example, create a health check for each HTTP server that is serving content for www\.example\.com\. For the value of **Domain Name**, specify the domain name of the server \(such as us\-east\-2\-www\.example\.com\), not the name of the resource record sets \(example\.com\)\.

**Important**  
In this configuration, if you create a health check for which the value of **Domain Name** matches the name of the resource record sets and then associate the health check with those resource record sets, health check results will be unpredictable\.

For more information about checking the health of endpoints, see [Creating Amazon Route 53 Health Checks and Configuring DNS Failover](dns-failover.md)\.