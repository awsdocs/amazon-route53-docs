# Values specific for simple records<a name="resource-record-sets-values-basic"></a>

When you create simple records, you specify the following values\.

**Topics**
+ [Routing policy](#rrsets-values-basic-routing-policy)
+ [Record name](#rrsets-values-basic-name)
+ [Value/Route traffic to](#rrsets-values-basic-value)
+ [Record type](#rrsets-values-basic-type)
+ [TTL \(seconds\)](#rrsets-values-basic-ttl)

## Routing policy<a name="rrsets-values-basic-routing-policy"></a>

Choose **Simple routing**\.

## Record name<a name="rrsets-values-basic-name"></a>

Enter the name of the domain or subdomain that you want to route traffic for\. The default value is the name of the hosted zone\. 

**Note**  
If you're creating a record that has the same name as the hosted zone, don't enter a value \(for example, an @ symbol\) in the **Name** field\. 

For more information about record names, see [Record name](resource-record-sets-values-shared.md#rrsets-values-common-name)\.

## Value/Route traffic to<a name="rrsets-values-basic-value"></a>

Choose **IP address or another value depending on the record type**\. Enter a value that is appropriate for the value of **Record type**\. For all types except **CNAME**, you can enter more than one value\. Enter each value on a separate line\.

You can route traffic to, or specify the following values:
+ **A — IPv4 address**
+ **AAAA — IPv6 address**
+ **CAA — Certificate Authority Authorization**
+ **CNAME — Canonical name**
+ **MX — Mail exchange**
+ **NAPTR — Name Authority Pointer**
+ **NS — Name server**

  The domain name of a name server, for example, **ns1\.example\.com**\.
**Note**  
You can specify an NS record with only simple routing policy\.
+ **PTR — Pointer**
+ **SPF — Sender Policy Framework**
+ **SRV — Service locator**
+ **TXT — Text**

For more information about the above values, see [Value/Route traffic to](resource-record-sets-values-shared.md#rrsets-values-common-value)\.

## Record type<a name="rrsets-values-basic-type"></a>

The DNS record type\. For more information, see [Supported DNS record types](ResourceRecordTypes.md)\.

Select the value for **Record type** based on how you want Route 53 to respond to DNS queries\. 

## TTL \(seconds\)<a name="rrsets-values-basic-ttl"></a>

The amount of time, in seconds, that you want DNS recursive resolvers to cache information about this record\. If you specify a longer value \(for example, 172800 seconds, or two days\), you reduce the number of calls that DNS recursive resolvers must make to Route 53 to get the latest information in this record\. This has the effect of reducing latency and reducing your bill for Route 53 service\. For more information, see [How Amazon Route 53 routes traffic for your domain](welcome-dns-service.md#welcome-dns-service-how-route-53-routes-traffic)\.

However, if you specify a longer value for TTL, it takes longer for changes to the record \(for example, a new IP address\) to take effect because recursive resolvers use the values in their cache for longer periods before they ask Route 53 for the latest information\. If you're changing settings for a domain or subdomain that's already in use, we recommend that you initially specify a shorter value, such as 300 seconds, and increase the value after you confirm that the new settings are correct\.