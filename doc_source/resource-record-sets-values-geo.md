# Values for geolocation records<a name="resource-record-sets-values-geo"></a>

When you create geolocation records, you specify the following values\.

**Note**  
Although creating geolocation records in private hosted zones is allowed, it's not supported\.

**Topics**
+ [Name](#rrsets-values-geo-name)
+ [Type](#rrsets-values-geo-type)
+ [Alias](#rrsets-values-geo-alias)
+ [TTL \(time to live\)](#rrsets-values-geo-ttl)
+ [Value](#rrsets-values-geo-value)
+ [Routing policy](#rrsets-values-geo-routing-policy)
+ [Location](#rrsets-values-geo-location)
+ [Sublocation](#rrsets-values-geo-sublocation)
+ [Set ID](#rrsets-values-geo-set-id)
+ [Associate with health check/Health check to associate](#rrsets-values-geo-associate-with-health-check)

## Name<a name="rrsets-values-geo-name"></a>

Enter the name of the domain or subdomain that you want to route traffic for\. The default value is the name of the hosted zone\. 

**Note**  
If you're creating a record that has the same name as the hosted zone, don't enter a value \(for example, an @ symbol\) in the **Name** field\. 

Enter the same name for all of the records in the group of geolocation records\. 

**CNAME records**  
If you're creating a record that has a value of **CNAME** for **Type**, the name of the record can't be the same as the name of the hosted zone\.

**Special characters**  
For information about how to specify characters other than a\-z, 0\-9, and \- \(hyphen\) and how to specify internationalized domain names, see [DNS domain name format](DomainNameFormat.md)\.

**Wildcard characters**  
You can use an asterisk \(\*\) character in the name\. DNS treats the \* character either as a wildcard or as the \* character \(ASCII 42\), depending on where it appears in the name\. For more information, see [Using an asterisk \(\*\) in the names of hosted zones and records](DomainNameFormat.md#domain-name-format-asterisk)\.

## Type<a name="rrsets-values-geo-type"></a>

The DNS record type\. For more information, see [Supported DNS record types](ResourceRecordTypes.md)\.

Select the same value for all of the records in the group of geolocation records\.zzz

## Alias<a name="rrsets-values-geo-alias"></a>

Select **No**\. 

## TTL \(time to live\)<a name="rrsets-values-geo-ttl"></a>

The amount of time, in seconds, that you want DNS recursive resolvers to cache information about this record\. If you specify a longer value \(for example, 172800 seconds, or two days\), you reduce the number of calls that DNS recursive resolvers must make to Route 53 to get the latest information in this record\. This has the effect of reducing latency and reducing your bill for Route 53 service\. For more information, see [How Amazon Route 53 routes traffic for your domain](welcome-dns-service.md#welcome-dns-service-how-route-53-routes-traffic)\.

However, if you specify a longer value for TTL, it takes longer for changes to the record \(for example, a new IP address\) to take effect because recursive resolvers use the values in their cache for longer periods before they ask Route 53 for the latest information\. If you're changing settings for a domain or subdomain that's already in use, we recommend that you initially specify a shorter value, such as 300 seconds, and increase the value after you confirm that the new settings are correct\.

If you're associating this record with a health check, we recommend that you specify a TTL of 60 seconds or less so clients respond quickly to changes in health status\.

## Value<a name="rrsets-values-geo-value"></a>

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
The fully qualified domain name \(for example, *www\.example\.com*\) that you want Route 53 to return in response to DNS queries for this record\. A trailing dot is optional; Route 53 assumes that the domain name is fully qualified\. This means that Route 53 treats *www\.example\.com* \(without a trailing dot\) and *www\.example\.com\.* \(with a trailing dot\) as identical\.

**MX — Mail exchange**  
A priority and a domain name that specifies a mail server, for example, **10 mailserver\.example\.com**\.

**NAPTR — Name Authority Pointer**  
Six space\-separated settings that are used by Dynamic Delegation Discovery System \(DDDS\) applications to convert one value to another or to replace one value with another\. For more information, see [NAPTR record type](ResourceRecordTypes.md#NAPTRFormat)\.

**PTR — Pointer**  
The domain name that you want Route 53 to return\.

**SPF — Sender Policy Framework**  
An SPF record enclosed in quotation marks, for example, **"v=spf1 ip4:192\.168\.0\.1/16\-all"**\. SPF records are not recommended\. For more information, see [Supported DNS record types](ResourceRecordTypes.md)\.

**SRV — Service locator**  
An SRV record\. For information about SRV record format, refer to the applicable documentation\. The format of an SRV record is:  
**\[priority\] \[weight\] \[port\] \[server host name\]**  
For example:  
**1 10 5269 xmpp\-server\.example\.com\.**

**TXT — Text**  
A text record\. Enclose text in quotation marks, for example, **"Sample Text Entry"**\. 

## Routing policy<a name="rrsets-values-geo-routing-policy"></a>

Select **Geolocation**\. 

## Location<a name="rrsets-values-geo-location"></a>

When you configure Route 53 to respond to DNS queries based on the location that the queries originated from, select the continent or country for which you want Route 53 to respond with the settings in this record\. If you want Route 53 to respond to DNS queries for individual states in the United States, select **United States** from the **Location** list, and then select the state from the **Sublocation** list\.

**Important**  
We recommend that you create one geolocation record that has a value of **Default** for **Location**\. This covers geographic locations that you haven't created records for and IP addresses that Route 53 can't identify a location for\.

You can't create non\-geolocation records that have the same values for **Name** and **Type** as geolocation records\.

For more information, see [Geolocation routing](routing-policy.md#routing-policy-geo)\.

Here are the countries that Amazon Route 53 associates with each continent\. The country codes are from ISO 3166\. For more information, see the Wikipedia article [ISO 3166\-1 alpha\-2](http://en.wikipedia.org/wiki/ISO_3166-1_alpha-2):

**Africa \(AF\)**  
AO, BF, BI, BJ, BW, CD, CF, CG, CI, CM, CV, DJ, DZ, EG, ER, ET, GA, GH, GM, GN, GQ, GW, KE, KM, LR, LS, LY, MA, MG, ML, MR, MU, MW, MZ, NA, NE, NG, RE, RW, SC, SD, SH, SL, SN, SO, SS, ST, SZ, TD, TG, TN, TZ, UG, YT, ZA, ZM, ZW

**Antarctica \(AN\)**  
AQ, GS, TF

**Asia \(AS\)**  
AE, AF, AM, AZ, BD, BH, BN, BT, CC, CN, GE, HK, ID, IL, IN, IO, IQ, IR, JO, JP, KG, KH, KP, KR, KW, KZ, LA, LB, LK, MM, MN, MO, MV, MY, NP, OM, PH, PK, PS, QA, SA, SG, SY, TH, TJ, TM, TW, UZ, VN, YE

**Europe \(EU\)**  
AD, AL, AT, AX, BA, BE, BG, BY, CH, CY, CZ, DE, DK, EE, ES, FI, FO, FR, GB, GG, GI, GR, HR, HU, IE, IM, IS, IT, JE, LI, LT, LU, LV, MC, MD, ME, MK, MT, NL, NO, PL, PT, RO, RS, RU, SE, SI, SJ, SK, SM, TR, UA, VA, XK

**North America \(NA\)**  
AG, AI, AW, BB, BL, BM, BQ, BS, BZ, CA, CR, CU, CW, DM, DO, GD, GL, GP, GT, HN, HT, JM, KN, KY, LC, MF, MQ, MS, MX, NI, PA, PM, PR, SV, SX, TC, TT, US, VC, VG, VI

**Oceania \(OC\)**  
AS, AU, CK, FJ, FM, GU, KI, MH, MP, NC, NF, NR, NU, NZ, PF, PG, PN, PW, SB, TK, TL, TO, TV, UM, VU, WF, WS

**South America \(SA\)**  
AR, BO, BR, CL, CO, EC, FK, GF, GY, PE, PY, SR, UY, VE

**Note**  
Route 53 doesn't support creating geolocation records for the following countries: Bouvet Island \(BV\), Christmas Island \(CX\), Western Sahara \(EH\), and Heard Island and McDonald Islands \(HM\)\. No data is available about IP addresses for these countries\.

## Sublocation<a name="rrsets-values-geo-sublocation"></a>

When you configure Route 53 to respond to DNS queries based on the state of the United States that the queries originated from, select the state from the **Sublocations** list\. United States territories \(for example, Puerto Rico\) are listed as countries in the **Location** list\.

**Important**  
Some IP addresses are associated with the United States, but not with an individual state\. If you create records for all of the states in the United States, we recommend that you also create a record for the United States to route queries for these unassociated IP addresses\. If you don't create a record for the United States, Route 53 responds to DNS queries from unassociated United States IP addresses with settings from the default geolocation record \(if you created one\) or with a "no answer" response\. 

## Set ID<a name="rrsets-values-geo-set-id"></a>

Enter a value that uniquely identifies this record in the group of geolocation records\.

## Associate with health check/Health check to associate<a name="rrsets-values-geo-associate-with-health-check"></a>

Select **Yes** if you want Route 53 to check the health of a specified endpoint and to respond to DNS queries using this record only when the endpoint is healthy\. Then select the health check that you want Route 53 to perform for this record\. 

Route 53 doesn't check the health of the endpoint specified in the record, for example, the endpoint specified by the IP address in the **Value** field\. When you select a health check for a record, Route 53 checks the health of the endpoint that you specified in the health check\. For information about how Route 53 determines whether an endpoint is healthy, see [How Amazon Route 53 determines whether a health check is healthyHow Route 53 determines whether a health check is healthy](dns-failover-determining-health-of-endpoints.md)\.

Associating a health check with a record is useful only when Route 53 is choosing between two or more records to respond to a DNS query, and you want Route 53 to base the choice in part on the status of a health check\. Use health checks only in the following configurations:
+ You're checking the health of all of the records in a group of records that have the same name, type, and routing policy \(such as failover or weighted records\), and you specify health check IDs for all the records\. If the health check for a record specifies an endpoint that is not healthy, Route 53 stops responding to queries using the value for that record\.
+ You select **Yes** for **Evaluate Target Health** for an alias record or the records in a group of failover alias, geolocation alias, latency alias, or weighted alias record\. If the alias records reference non\-alias records in the same hosted zone, you must also specify health checks for the referenced records\. 

If your health checks specify the endpoint only by domain name, we recommend that you create a separate health check for each endpoint\. For example, create a health check for each HTTP server that is serving content for www\.example\.com\. For the value of **Domain Name**, specify the domain name of the server \(such as us\-east\-2\-www\.example\.com\), not the name of the records \(example\.com\)\.

**Important**  
In this configuration, if you create a health check for which the value of **Domain Name** matches the name of the records and then associate the health check with those records, health check results will be unpredictable\.

For geolocation records, if an endpoint is unhealthy, Route 53 looks for a record for the larger, associated geographic region\. For example, suppose you have records for a state in the United States, for the United States, for North America, and for all locations \(**Location** is **Default**\)\. If the endpoint for the state record is unhealthy, Route 53 checks the records for the United States, for North America, and for all locations, in that order, until it finds a record that has a healthy endpoint\. If all applicable records are unhealthy, including the record for all locations, Route 53 responds to the DNS query using the value for the record for the smallest geographic region\. 