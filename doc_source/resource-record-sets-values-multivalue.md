# Values for multivalue answer records<a name="resource-record-sets-values-multivalue"></a>

When you create multivalue answer records, you specify the following values\.

**Note**  
Creating multivalue answer alias records is not supported\.

**Topics**
+ [Name](#rrsets-values-multivalue-name)
+ [Type](#rrsets-values-multivalue-type)
+ [Alias](#rrsets-values-multivalue-alias)
+ [TTL \(time to live\)](#rrsets-values-multivalue-ttl)
+ [Value](#rrsets-values-multivalue-value)
+ [Routing policy](#rrsets-values-multivalue-routing-policy)
+ [Set ID](#rrsets-values-multivalue-set-identifier)
+ [Associate with health check/Health check to associate](#rrsets-values-multivalue-associate-with-health-check)

## Name<a name="rrsets-values-multivalue-name"></a>

Enter the name of the domain or subdomain that you want to route traffic for\. The default value is the name of the hosted zone\. 

**Note**  
If you're creating a record that has the same name as the hosted zone, don't enter a value \(for example, an @ symbol\) in the **Name** field\. 

**Special characters**  
For information about how to specify characters other than a\-z, 0\-9, and \- \(hyphen\) and how to specify internationalized domain names, see [DNS domain name format](DomainNameFormat.md)\.

**Wildcard characters**  
You can use an asterisk \(\*\) character in the name\. DNS treats the \* character either as a wildcard or as the \* character \(ASCII 42\), depending on where it appears in the name\. For more information, see [Using an asterisk \(\*\) in the names of hosted zones and records](DomainNameFormat.md#domain-name-format-asterisk)\.

## Type<a name="rrsets-values-multivalue-type"></a>

The DNS record type\. For more information, see [Supported DNS record types](ResourceRecordTypes.md)\.

Select any value except **NS** or **CNAME**\.

Select the same value for all of the records in the group of multivalue answer records\.

## Alias<a name="rrsets-values-multivalue-alias"></a>

Select **No**\. 

## TTL \(time to live\)<a name="rrsets-values-multivalue-ttl"></a>

The amount of time, in seconds, that you want DNS recursive resolvers to cache information about this record\. If you specify a longer value \(for example, 172800 seconds, or two days\), you reduce the number of calls that DNS recursive resolvers must make to Route 53 to get the latest information in this record\. This has the effect of reducing latency and reducing your bill for Route 53 service\. For more information, see [How Amazon Route 53 routes traffic for your domain](welcome-dns-service.md#welcome-dns-service-how-route-53-routes-traffic)\.

However, if you specify a longer value for TTL, it takes longer for changes to the record \(for example, a new IP address\) to take effect because recursive resolvers use the values in their cache for longer periods before they ask Route 53 for the latest information\. If you're changing settings for a domain or subdomain that's already in use, we recommend that you initially specify a shorter value, such as 300 seconds, and increase the value after you confirm that the new settings are correct\.

If you're associating this record with a health check, we recommend that you specify a TTL of 60 seconds or less so clients respond quickly to changes in health status\.

**Note**  
If you create two or more multivalue answer records that have the same name and type, and you specify different values for **TTL**, Route 53 changes the value of **TTL** for all of the records to the last value that you specified\.

## Value<a name="rrsets-values-multivalue-value"></a>

Enter a value that is appropriate for the value of **Type**\. If you enter more than one value, enter each value on a separate line\.

**A — IPv4 address**  
An IP address in IPv4 format, for example, **192\.0\.2\.235**\.

**AAAA — IPv6 address**  
An IP address in IPv6 format, for example, **2001:0db8:85a3:0:0:8a2e:0370:7334**\.

**MX — Mail exchange**  
A priority and a domain name that specifies a mail server, for example, **10 mailserver\.example\.com**\.

**NAPTR — Name Authority Pointer**  
Six space\-separated settings that are used by Dynamic Delegation Discovery System \(DDDS\) applications to convert one value to another or to replace one value with another\. For more information, see [NAPTR record type](ResourceRecordTypes.md#NAPTRFormat)\.

**NS — Name server**  
The domain name of a name server, for example, **ns1\.example\.com**\.

**PTR — Pointer**  
The domain name that you want Route 53 to return\.

**SOA — Start of Authority**  
Basic DNS information about the domain\. For more information, see [The start of authority \(SOA\) record](SOA-NSrecords.md#SOArecords)\.

**SPF — Sender Policy Framework**  
An SPF record enclosed in quotation marks, for example, **"v=spf1 ip4:192\.168\.0\.1/16\-all"**\. SPF records are not recommended\. For more information, see [Supported DNS record types](ResourceRecordTypes.md)\.

**SRV — Service locator**  
An SRV record\. For information about SRV record format, refer to the applicable documentation\. The format of an SRV record is:  
**\[priority\] \[weight\] \[port\] \[server host name\]**  
For example:  
**1 10 5269 xmpp\-server\.example\.com\.**

**TXT — Text**  
A text record\. Enclose text in quotation marks, for example, **"Sample Text Entry"**\. 

## Routing policy<a name="rrsets-values-multivalue-routing-policy"></a>

Select **Multivalue answer**\.

## Set ID<a name="rrsets-values-multivalue-set-identifier"></a>

Enter a value that uniquely identifies this record in the group of multivalue answer records\. 

## Associate with health check/Health check to associate<a name="rrsets-values-multivalue-associate-with-health-check"></a>

Select **Yes** if you want Route 53 to check the health of a specified endpoint and to respond to DNS queries using this record only when the endpoint is healthy\. Then select the health check that you want Route 53 to perform for this record\. 

Route 53 doesn't check the health of the endpoint specified in the record, for example, the endpoint specified by the IP address in the **Value** field\. When you select a health check for a record, Route 53 checks the health of the endpoint that you specified in the health check\. For information about how Route 53 determines whether an endpoint is healthy, see [How Amazon Route 53 determines whether a health check is healthyHow Route 53 determines whether a health check is healthy](dns-failover-determining-health-of-endpoints.md)\.

Associating a health check with a record is useful only when Route 53 is choosing between two or more records to respond to a DNS query, and you want Route 53 to base the choice in part on the status of a health check\. Use health checks only in the following configurations:
+ You're checking the health of all of the records in a group of records that have the same name, type, and routing policy \(such as failover or weighted records\), and you specify health check IDs for all the records\. If the health check for a record specifies an endpoint that is not healthy, Route 53 stops responding to queries using the value for that record\.
+ You select **Yes** for **Evaluate Target Health** for an alias record or the records in a group of failover alias, geolocation alias, latency alias, or weighted alias record\. If the alias records reference non\-alias records in the same hosted zone, you must also specify health checks for the referenced records\. 

If your health checks specify the endpoint only by domain name, we recommend that you create a separate health check for each endpoint\. For example, create a health check for each HTTP server that is serving content for www\.example\.com\. For the value of **Domain Name**, specify the domain name of the server \(such as us\-east\-2\-www\.example\.com\), not the name of the records \(example\.com\)\.

**Important**  
In this configuration, if you create a health check for which the value of **Domain Name** matches the name of the records and then associate the health check with those records, health check results will be unpredictable\.