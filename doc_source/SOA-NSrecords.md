# NS and SOA Records that Amazon Route 53 Creates for a Public Hosted Zone<a name="SOA-NSrecords"></a>

For each public hosted zone that you create, Amazon Route 53 automatically creates a name server \(NS\) record and a start of authority \(SOA\) record\. Don't change these records\. 


+ [The Name Server \(NS\) record](#NSrecords)
+ [The Start of Authority \(SOA\) Record](#SOArecords)

## The Name Server \(NS\) record<a name="NSrecords"></a>

Amazon Route 53 automatically creates a name server \(NS\) record that has the same name as your hosted zone\. It lists the four name servers that are the authoritative name servers for your hosted zone\. Do not add, change, or delete name servers in this record\.

The following examples show the format for the names of Route 53 name servers \(these are examples only; don't use them when you're updating your registrar's name server records\):

+ *ns\-2048\.awsdns\-64\.com*

+ *ns\-2049\.awsdns\-65\.net*

+ *ns\-2050\.awsdns\-66\.org*

+ *ns\-2051\.awsdns\-67\.co\.uk*

To get the list of name servers for your hosted zone:

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, click **Hosted Zones**\.

1. On the **Hosted Zones** page, choose the radio button \(not the name\) for the hosted zone\.

1. In the right pane, make note of the four servers listed for **Name Servers**\.

For information about migrating DNS service from another DNS service provider to Route 53, see [Making Amazon Route 53 the DNS Service for an Existing DomainMaking Route 53 the DNS Service for an Existing Domain](MigratingDNS.md)\.

## The Start of Authority \(SOA\) Record<a name="SOArecords"></a>

The start of authority \(SOA\) record identifies the base DNS information about the domain, for example:

```
1. ns-2048.awsdns-64.net. hostmaster.example.com. 1 7200 900 1209600 86400
```

A SOA record includes the following elements:

+ The Route 53 name server that created the SOA record, for example, `ns-2048.awsdns-64.net`\.

+ The email address of the administrator\. The `@` symbol is replaced by a period, for example, `hostmaster.example.com`\. The default value is an amazon\.com email address that is not monitored\.

+ A serial number that you can optionally increment whenever you update a record in the hosted zone\. Route 53 doesn't increment the number automatically\. \(The serial number is used by DNS services that support secondary DNS\.\) In the example, this value is `1`\.

+ A refresh time in seconds that secondary DNS servers wait before querying the primary DNS server's SOA record to check for changes\. In the example, this value is `7200`\.

+ The retry interval in seconds that a secondary server waits before retrying a failed zone transfer\. Normally, the retry time is less than the refresh time\. In the example, this value is `900` \(15 minutes\)\. 

+ The time in seconds that a secondary server will keep trying to complete a zone transfer\. If this time elapses before a successful zone transfer, the secondary server will stop answering queries because it considers its data too old to be reliable\. In the example, this value is `1209600` \(two weeks\)\.

+ The minimum time to live \(TTL\)\. This value helps define the length of time that an NXDOMAIN result, which indicates that a domain does not exist, should be cached by a DNS resolver\. When a DNS resolver caches an NXDOMAIN result, this is referred to as *negative caching*\. 

  The duration of negative caching is the lesser of the following values:

  + This value—the minimum TTL in the SOA record\. In the example, the value is `86400` \(one day\)\.

  + The value of the minimum TTL for the SOA record\. The default value is 900 seconds\. For information about changing this value, see [Editing Records](resource-record-sets-editing.md)\.