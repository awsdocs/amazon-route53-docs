# Values for Multivalue Answer Resource Record Sets<a name="resource-record-sets-values-multivalue"></a>

When you create multivalue answer resource record sets, you specify the following values:

**Note**  
Creating multivalue answer alias resource record sets is not supported\.


+ [Name](#rrsets-values-multivalue-name)
+ [Type](#rrsets-values-multivalue-type)
+ [Alias](#rrsets-values-multivalue-alias)
+ [TTL \(Time to Live\)](#rrsets-values-multivalue-ttl)
+ [Value](#rrsets-values-multivalue-value)
+ [Routing Policy](#rrsets-values-multivalue-routing-policy)
+ [Set ID](#rrsets-values-multivalue-set-identifier)
+ [Associate with Health Check/Health Check to Associate](#rrsets-values-multivalue-associate-with-health-check)

## Name<a name="rrsets-values-multivalue-name"></a>

Enter the name of the domain or subdomain that you want to route traffic for\. The default value is the name of the hosted zone\. 

**Note**  
If you're creating a resource record set that has the same name as the hosted zone, don't enter a value \(for example, an @ symbol\) in the **Name** field\. 

**Special characters**  
For information about how to specify characters other than a\-z, 0\-9, and \- \(hyphen\) and how to specify internationalized domain names, see [DNS Domain Name Format](DomainNameFormat.md)\.

**Wildcard characters**  
You can use an asterisk \(\*\) character in the name\. DNS treats the \* character either as a wildcard or as the \* character \(ASCII 42\), depending on where it appears in the name\. For more information, see [Using an Asterisk \(\*\) in the Names of Hosted Zones and Resource Record Sets](DomainNameFormat.md#domain-name-format-asterisk)\.

## Type<a name="rrsets-values-multivalue-type"></a>

The DNS record type\. For more information, see [Supported DNS Record Types](ResourceRecordTypes.md)\.

Select any value except **NS** or **CNAME**\.

Select the same value for all of the resource record sets in the group of multivalue answer resource record sets\.

## Alias<a name="rrsets-values-multivalue-alias"></a>

Select **No**\. 

## TTL \(Time to Live\)<a name="rrsets-values-multivalue-ttl"></a>

The amount of time, in seconds, that you want DNS recursive resolvers to cache information about this resource record set\. If you specify a longer value \(for example, 172800 seconds, or two days\), you pay less for Amazon Route 53 service because recursive resolvers send requests to Amazon Route 53 less often\. However, it takes longer for changes to the resource record set \(for example, a new IP address\) to take effect because recursive resolvers use the values in their cache for longer periods instead of asking Amazon Route 53 for the latest information\. 

If you're associating this resource record set with a health check, we recommend that you specify a TTL of 60 seconds or less so clients respond quickly to changes in health status\.

## Value<a name="rrsets-values-multivalue-value"></a>

Enter a value that is appropriate for the value of **Type**\. If you enter more than one value, enter each value on a separate line\.

**A — IPv4 address**  
An IP address in IPv4 format, for example, **192\.0\.2\.235**\.

**AAAA — IPv6 address**  
An IP address in IPv6 format, for example, **2001:0db8:85a3:0:0:8a2e:0370:7334**\.

**MX — Mail exchange**  
A priority and a domain name that specifies a mail server, for example, **10 mailserver\.example\.com**\.

**NAPTR — Name Authority Pointer**  
Six space\-separated settings that are used by Dynamic Delegation Discovery System \(DDDS\) applications to convert one value to another or to replace one value with another\. For more information, see [NAPTR Format](ResourceRecordTypes.md#NAPTRFormat)\.

**NS — Name server**  
The domain name of a name server, for example, **ns1\.example\.com**\.

**PTR — Pointer**  
The domain name that you want Amazon Route 53 to return\.

**SOA — Start of Authority**  
Basic DNS information about the domain\. For more information, see [The Start of Authority \(SOA\) Resource Record Set](SOA-NSrecords.md#SOArecords)\.

**SPF — Sender Policy Framework**  
An SPF record enclosed in quotation marks, for example, **"v=spf1 ip4:192\.168\.0\.1/16\-all"**\. SPF records are not recommended\. For more information, see [Supported DNS Record Types](ResourceRecordTypes.md)\.

**SRV — Service locator**  
An SRV record\. For information about SRV record format, refer to the applicable documentation\. The format of an SRV record is:  
**\[priority\] \[weight\] \[port\] \[server host name\]**  
For example:  
**1 10 5269 xmpp\-server\.example\.com\.**

**TXT — Text**  
A text record\. Enclose text in quotation marks, for example, **"Sample Text Entry"**\. 

## Routing Policy<a name="rrsets-values-multivalue-routing-policy"></a>

Select **Multivalue answer**\.

## Set ID<a name="rrsets-values-multivalue-set-identifier"></a>

Enter a value that uniquely identifies this resource record set in the group of multivalue answer resource record sets\. 

## Associate with Health Check/Health Check to Associate<a name="rrsets-values-multivalue-associate-with-health-check"></a>

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