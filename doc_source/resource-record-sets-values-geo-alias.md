# Values specific for geolocation alias records<a name="resource-record-sets-values-geo-alias"></a>

When you create geolocation alias records, you specify the following values\.

**Note**  
Although creating geolocation alias records in a private hosted zone is allowed, it's not supported\.

For more information, see [Choosing between alias and non\-alias records](resource-record-sets-choosing-alias-non-alias.md)\.

**Topics**
+ [Routing policy](#rrsets-values-geo-alias-routing-policy)
+ [Record name](#rrsets-values-geo-alias-name)
+ [Record type](#rrsets-values-geo-alias-type)
+ [Value/Route traffic to](#rrsets-values-geo-alias-alias-target)
+ [Location](#rrsets-values-geo-alias-location)
+ [U\.S\. states](#rrsets-values-geo-alias-sublocation)
+ [Health check](#rrsets-values-geo-alias-associate-with-health-check)
+ [Evaluate target health](#rrsets-values-geo-alias-evaluate-target-health)
+ [Record ID](#rrsets-values-geo-alias-set-id)

## Routing policy<a name="rrsets-values-geo-alias-routing-policy"></a>

Choose **Geolocation**\. 

**Note**  
Although creating geolocation alias records in a private hosted zone is allowed, it's not supported\.

## Record name<a name="rrsets-values-geo-alias-name"></a>

Enter the name of the domain or subdomain that you want to route traffic for\. The default value is the name of the hosted zone\. 

**Note**  
If you're creating a record that has the same name as the hosted zone, don't enter a value \(for example, an @ symbol\) in the **Record name** field\. 

Enter the same name for all of the records in the group of geolocation records\. 

For more information about record names, see [Record name](resource-record-sets-values-alias-common.md#rrsets-values-common-alias-name)\.

## Record type<a name="rrsets-values-geo-alias-type"></a>

The DNS record type\. For more information, see [Supported DNS record types](ResourceRecordTypes.md)\.

Select the applicable value based on the AWS resource that you're routing traffic to\. Select the same value for all of the records in the group of geolocation records:

**API Gateway custom regional API or edge\-optimized API**  
Select **A — IPv4 address**\.

**Amazon VPC interface endpoints**  
Select **A — IPv4 address**\.

**CloudFront distribution**  
Select **A — IPv4 address**\.  
If IPv6 is enabled for the distribution, create two records, one with a value of **A — IPv4 address** for **Record type**, and one with a value of **AAAA — IPv6 address**\.

**Elastic Beanstalk environment that has regionalized subdomains**  
Select **A — IPv4 address**

**ELB load balancer**  
Select **A — IPv4 address** or **AAAA — IPv6 address**

**Amazon S3 bucket**  
Select **A — IPv4 address**

**Another record in this hosted zone**  
Select the type of the record that you're creating the alias for\. All types are supported except **NS** and **SOA**\.  
If you're creating an alias record that has the same name as the hosted zone \(known as the *zone apex*\), you can't route traffic to a record for which the value of **Record type** is **CNAME**\. This is because the alias record must have the same type as the record you're routing traffic to, and creating a CNAME record for the zone apex isn't supported even for an alias record\. 

## Value/Route traffic to<a name="rrsets-values-geo-alias-alias-target"></a>

The value that you choose from the list or that you type in the field depends on the AWS resource that you're routing traffic to\.

For information about what AWS resources you can target, see [Value/route traffic to](resource-record-sets-values-alias-common.md#rrsets-values-alias-common-target)\.

For more information about how to configure Route 53 to route traffic to specific AWS resources, see [Routing internet traffic to your AWS resources](routing-to-aws-resources.md)\.

## Location<a name="rrsets-values-geo-alias-location"></a>

When you configure Route 53 to respond to DNS queries based on the location that the queries originated from, select the continent or country for which you want Route 53 to respond with the settings in this record\. If you want Route 53 to respond to DNS queries for individual states in the United States, select **United States** from the **Location** list, and then select the state from the **U\.S\. states** list\.

**Important**  
We recommend that you create one geolocation record that has a value of **Default** for **Location**\. This covers geographic locations that you haven't created records for and IP addresses that Route 53 can't identify a location for\.

You can't create non\-geolocation records that have the same values for **Record name** and **Record type** as geolocation records\.

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

## U\.S\. states<a name="rrsets-values-geo-alias-sublocation"></a>

When you configure Route 53 to respond to DNS queries based on the state of the United States that the queries originated from, select the state from the **U\.S\. states** list\. United States territories \(for example, Puerto Rico\) are listed as countries in the **Location** list\.

**Important**  
Some IP addresses are associated with the United States, but not with an individual state\. If you create records for all of the states in the United States, we recommend that you also create a record for the United States to route queries for these unassociated IP addresses\. If you don't create a record for the United States, Route 53 responds to DNS queries from unassociated United States IP addresses with settings from the default geolocation record \(if you created one\) or with a "no answer" response\. 

## Health check<a name="rrsets-values-geo-alias-associate-with-health-check"></a>

Select a health check if you want Route 53 to check the health of a specified endpoint and to respond to DNS queries using this record only when the endpoint is healthy\. 

Route 53 doesn't check the health of the endpoint specified in the record, for example, the endpoint specified by the IP address in the **Value** field\. When you select a health check for a record, Route 53 checks the health of the endpoint that you specified in the health check\. For information about how Route 53 determines whether an endpoint is healthy, see [How Amazon Route 53 determines whether a health check is healthyHow Route 53 determines whether a health check is healthy](dns-failover-determining-health-of-endpoints.md)\.

Associating a health check with a record is useful only when Route 53 is choosing between two or more records to respond to a DNS query, and you want Route 53 to base the choice in part on the status of a health check\. Use health checks only in the following configurations:
+ You're checking the health of all of the records in a group of records that have the same name, type, and routing policy \(such as failover or weighted records\), and you specify health check IDs for all the records\. If the health check for a record specifies an endpoint that is not healthy, Route 53 stops responding to queries using the value for that record\.
+ You select **Yes** for **Evaluate target health** for an alias record or the records in a group of failover alias, geolocation alias, latency alias, or weighted alias record\. If the alias records reference non\-alias records in the same hosted zone, you must also specify health checks for the referenced records\. 

If your health checks specify the endpoint only by domain name, we recommend that you create a separate health check for each endpoint\. For example, create a health check for each HTTP server that is serving content for www\.example\.com\. For the value of **Domain name**, specify the domain name of the server \(such as us\-east\-2\-www\.example\.com\), not the name of the records \(example\.com\)\.

**Important**  
In this configuration, if you create a health check for which the value of **Domain name** matches the name of the records and then associate the health check with those records, health check results will be unpredictable\.

For geolocation records, if an endpoint is unhealthy, Route 53 looks for a record for the larger, associated geographic Region\. For example, suppose you have records for a state in the United States, for the United States, for North America, and for all locations \(**Location** is **Default**\)\. If the endpoint for the state record is unhealthy, Route 53 checks the records for the United States, for North America, and for all locations, in that order, until it finds a record that has a healthy endpoint\. If all applicable records are unhealthy, including the record for all locations, Route 53 responds to the DNS query using the value for the record for the smallest geographic region\. 

## Evaluate target health<a name="rrsets-values-geo-alias-evaluate-target-health"></a>

Select **Yes** if you want Route 53 to determine whether to respond to DNS queries using this record by checking the health of the resource specified by **Endpoint**\. 

Note the following:

**API Gateway custom regional APIs and edge\-optimized APIs**  
There are no special requirements for setting **Evaluate target health** to **Yes** when the endpoint is an API Gateway custom Regional API or an edge\-optimized API\.

**CloudFront distributions**  
You can't set **Evaluate target health** to **Yes** when the endpoint is a CloudFront distribution\.

**Elastic Beanstalk environments that have regionalized subdomains**  
If you specify an Elastic Beanstalk environment in **Endpoint** and the environment contains an ELB load balancer, Elastic Load Balancing routes queries only to the healthy Amazon EC2 instances that are registered with the load balancer\. \(An environment automatically contains an ELB load balancer if it includes more than one Amazon EC2 instance\.\) If you set **Evaluate target health** to **Yes** and either no Amazon EC2 instances are healthy or the load balancer itself is unhealthy, Route 53 routes queries to other available resources that are healthy, if any\.   
If the environment contains a single Amazon EC2 instance, there are no special requirements\.

**ELB load balancers**  
Health checking behavior depends on the type of load balancer:  
+ **Classic Load Balancers** – If you specify an ELB Classic Load Balancer in **Endpoint**, Elastic Load Balancing routes queries only to the healthy Amazon EC2 instances that are registered with the load balancer\. If you set **Evaluate target health** to **Yes** and either no EC2 instances are healthy or the load balancer itself is unhealthy, Route 53 routes queries to other resources\.
+ **Application and Network Load Balancers** – If you specify an ELB Application or Network Load Balancer and you set **Evaluate target health** to **Yes**, Route 53 routes queries to the load balancer based on the health of the target groups that are associated with the load balancer:
  + For an Application or Network Load Balancer to be considered healthy, every target group that contains targets must contain at least one healthy target\. If any target group contains only unhealthy targets, the load balancer is considered unhealthy, and Route 53 routes queries to other resources\.
  + A target group that has no registered targets is considered unhealthy\.
When you create a load balancer, you configure settings for Elastic Load Balancing health checks; they're not Route 53 health checks, but they perform a similar function\. Do not create Route 53 health checks for the EC2 instances that you register with an ELB load balancer\. 

**S3 buckets**  
There are no special requirements for setting **Evaluate target health** to **Yes** when the endpoint is an S3 bucket\.

**Amazon VPC interface endpoints**  
There are no special requirements for setting **Evaluate target health** to **Yes** when the endpoint is an Amazon VPC interface endpoint\.

**Other records in the same hosted zone**  
If the AWS resource that you specify in **Endpoint** is a record or a group of records \(for example, a group of weighted records\) but is not another alias record, we recommend that you associate a health check with all of the records in the endpoint\. For more information, see [What happens when you omit health checks?](dns-failover-complex-configs.md#dns-failover-complex-configs-hc-omitting)\.

## Record ID<a name="rrsets-values-geo-alias-set-id"></a>

Enter a value that uniquely identifies this record in the group of geolocation records\.