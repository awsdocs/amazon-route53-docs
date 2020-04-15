# Values that you specify when you create or update health checks<a name="health-checks-creating-values"></a>

When you create or update health checks, you specify the applicable values\. Note that you can't change some values after you create a health check\. 

**Topics**
+ [Monitoring an endpoint](#health-checks-creating-values-endpoint)
+ [Monitoring other health checks \(calculated health checks\)](#health-checks-creating-values-calculated)
+ [Monitoring a CloudWatch alarm](#health-checks-creating-values-cloudwatch)
+ [Advanced configuration \("Monitor an Endpoint" only\)](#health-checks-creating-values-advanced)
+ [Get notified when a health check fails](#health-checks-creating-values-alarm)

**Name**  
Optional, but recommended: The name that you want to assign to the health check\. If you specify a value for **Name**, Route 53 adds a tag to the health check, assigns the value **Name** to the tag key, and assigns the value that you specify to the tag value\. The value of the **Name** tag appears in the list of health checks in the Route 53 console, which lets you easily distinguish health checks from one another\.  
For more information about tagging and health checks, see [Naming and tagging health checks](health-checks-tagging.md)\.

**What to monitor**  
Whether you want this health check to monitor an endpoint or the status of other health checks:  
+ **Endpoint** – Route 53 monitors the health of an endpoint that you specify\. You can specify the endpoint by providing either a domain name or an IP address and a port\.
**Note**  
If you specify a non\-AWS endpoint, an additional charge applies\. For more information, including a definition of AWS endpoints, see "Health Checks" on the [Route 53 Pricing](https://aws.amazon.com/route53/pricing/) page\.
+ **Status of other health checks \(calculated health check\)** – Route 53 determines whether this health check is healthy based on the status of other health checks that you specify\. You also specify how many of the health checks need to be healthy for this health check to be considered healthy\.
+ **State of CloudWatch alarm** – Route 53 determines whether this health check is healthy by monitoring the data stream for a CloudWatch alarm\. 

## Monitoring an endpoint<a name="health-checks-creating-values-endpoint"></a>

If you want this health check to monitor an endpoint, specify the following values:
+ [Specify endpoint by](#health-checks-creating-values-specify-endpoint-by)
+ [Protocol](#health-checks-creating-values-protocol)
+ [IP address](#health-checks-creating-values-ip-address)
+ [Host name](#health-checks-creating-values-host-name)
+ [Port](#health-checks-creating-values-port)
+ [Domain name](#health-checks-creating-values-domain-name)
+ [Path](#health-checks-creating-values-path)

**Specify endpoint by**  
Whether you want to specify the endpoint using an IP address or using a domain name\.  
After you create a health check, you can't change the value of **Specify endpoint by**\. 

**Protocol**  
The method that you want Route 53 to use to check the health of your endpoint:  
+ **HTTP** – Route 53 tries to establish a TCP connection\. If successful, Route 53 submits an HTTP request and waits for an HTTP status code of 2xx or 3xx\.
+ **HTTPS** – Route 53 tries to establish a TCP connection\. If successful, Route 53 submits an HTTPS request and waits for an HTTP status code of 2xx or 3xx\.
**Important**  
If you choose **HTTPS**, the endpoint must support TLS v1\.0 or later\. 

  If you choose **HTTPS** for the value of **Protocol**, an additional charge applies\. For more information, see [Route 53 Pricing](https://aws.amazon.com/route53/pricing/)\.
+ **TCP** – Route 53 tries to establish a TCP connection\.
For more information, see [How Amazon Route 53 determines whether a health check is healthyHow Route 53 determines whether a health check is healthy](dns-failover-determining-health-of-endpoints.md)\.  
After you create a health check, you can't change the value of **Protocol**\. 

**IP address \("Specify endpoint by IP address" Only\)**  
The IPv4 or IPv6 address of the endpoint on which you want Route 53 to perform health checks, if you chose **Specify endpoint by IP address**\.  
Route 53 cannot check the health of endpoints for which the IP address is in local, private, nonroutable, or multicast ranges\. For more information about IP addresses that you can't create health checks for, see the following documents:  
+ [RFC 5735, Special Use IPv4 Addresses](http://tools.ietf.org/html/rfc5735)
+ [RFC 6598, IANA\-Reserved IPv4 Prefix for Shared Address Space](http://tools.ietf.org/html/rfc6598)\.
+ [RFC 5156, Special\-Use IPv6 Addresses](https://tools.ietf.org/html/rfc5156)
If the endpoint is an Amazon EC2 instance, we recommend that you create an Elastic IP address, associate it with your EC2 instance, and specify the Elastic IP address\. This ensures that the IP address of your instance will never change\. For more information, see [Elastic IP addresses \(EIP\)](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html) in the *Amazon EC2 User Guide for Linux Instances*\.  
If you specify a non\-AWS endpoint, an additional charge applies\. For more information, including a definition of AWS endpoints, see "Health Checks" on the [Route 53 Pricing](https://aws.amazon.com/route53/pricing/) page\.

**Host name \("Specify endpoint by IP address" Only, HTTP and HTTPS Protocols Only\)**  
The value that you want Route 53 to pass in the `Host` header in HTTP and HTTPS health checks\. This is typically the fully qualified DNS name of the website on which you want Route 53 to perform health checks\. When Route 53 checks the health of an endpoint, here is how it constructs the `Host` header:  
+ If you specify a value of **80** for **Port** and **HTTP** for **Protocol**, Route 53 passes to the endpoint a `Host` header that contains the value of **Host name**\. 
+ If you specify a value of **443** for **Port** and **HTTPS** for **Protocol**, Route 53 passes to the endpoint a `Host` header that contains the value of **Host name**\.
+ If you specify another value for **Port** and either **HTTP** or **HTTPS** for **Protocol**, Route 53 passes to the endpoint a `Host` header that contains the value *Host name***:***Port*\.
If you choose to specify the endpoint by IP address and you don't specify a value for **Host name**, Route 53 substitutes the value of **IP address** in the `Host` header in each of the preceding cases\.

**Port**  
The port on the endpoint on which you want Route 53 to perform health checks\.

**Domain name \("Specify endpoint by domain name" Only, All Protocols\)**  
The domain name \(example\.com\) or subdomain name \(backend\.example\.com\) of the endpoint that you want Route 53 to perform health checks on, if you choose **Specify endpoint by domain name**\.   
If you choose to specify the endpoint by domain name, Route 53 sends a DNS query to resolve the domain name that you specify in **Domain name** at the interval that you specify in **Request interval**\. Using an IP address that DNS returns, Route 53 then checks the health of the endpoint\.  
If you specify the endpoint by domain name, Route 53 uses only IPv4 to send health checks to the endpoint\. If there's no record with a type of A for the name that you specify for **Domain name**, the health check fails with a "DNS resolution failed" error\. 
If you want to check the health of failover, geolocation, geoproximity, latency, multivalue, or weighted records, and you choose to specify the endpoint by domain name, we recommend that you create a separate health check for each endpoint\. For example, create a health check for each HTTP server that is serving content for www\.example\.com\. For the value of **Domain name**, specify the domain name of the server \(such as us\-east\-2\-www\.example\.com\), not the name of the records \(www\.example\.com\)\.  
In this configuration, if you create a health check for which the value of **Domain name** matches the name of the records and then associate the health check with those records, health check results will be unpredictable\.
In addition, if the value of **Protocol** is **HTTP** or **HTTPS**, Route 53 passes the value of **Domain name** in the `Host` header as described in **Host name**, earlier in this list\. If the value of **Protocol** is **TCP**, Route 53 doesn't pass a `Host` header\.  
If you specify a non\-AWS endpoint, an additional charge applies\. For more information, including a definition of AWS endpoints, see "Health Checks" on the [Route 53 Pricing](https://aws.amazon.com/route53/pricing/) page\.

**Path \(HTTP and HTTPS Protocols Only\)**  
The path that you want Route 53 to request when performing health checks\. The path can be any value for which your endpoint will return an HTTP status code of `2xx` or `3xx` when the endpoint is healthy, such as the file `/docs/route53-health-check.html`\. You can also include query string parameters, for example, `/welcome.html?language=jp&login=y`\. If you don't include a leading slash \(`/`\) character, Route 53 automatically adds one\.

## Monitoring other health checks \(calculated health checks\)<a name="health-checks-creating-values-calculated"></a>

If you want this health check to monitor the status of other health checks, specify the following values:
+ [Health checks to monitor](#health-checks-creating-values-health-checks-to-monitor)
+ [Report healthy when](#health-checks-creating-values-report-healthy-when)
+ [Invert health check status](#health-checks-creating-values-invert-health-check-status)
+ [Disabled](#health-checks-creating-values-disabled)

**  Health checks to monitor **  
The health checks that you want Route 53 to monitor to determine the health of this health check\.   
You can add up to 256 health checks to **Health checks to monitor**\. To remove a health check from the list, choose the **x** at the right of the highlight for that health check\.  
You can't configure a calculated health check to monitor the health of other calculated health checks\.
If you disable a health check that a calculated health check is monitoring, Route 53 considers the disabled health check to be healthy as it calculates whether the calculated health check is healthy\. If you want the disabled health check to be considered unhealthy, choose the **Invert health check status** check box\.

**  Report healthy when **  
The calculation that you want Route 53 to perform to determine whether this health check is healthy:  
+ **Report healthy when at least x of y selected health checks are healthy** – Route 53 considers this health check to be healthy when the specified number of health checks that you added to **Health checks to monitor** are healthy\. Note the following:
  + If you specify a number greater than the number of health checks in **Health checks to monitor**, Route 53 always considers this health check to be unhealthy\.
  + If you specify **0**, Route 53 always considers this health check to be healthy\.
+ **Report healthy when all health checks are healthy \(AND\)** – Route 53 considers this health check to be healthy only when all the health checks that you added to **Health checks to monitor** are healthy\.
+ **Report healthy when one or more health checks are healthy \(OR\)** – Route 53 considers this health check to be healthy when at least one of the health checks that you added to **Health checks to monitor** is healthy\.

**  Invert health check status **  
Choose whether you want Route 53 to invert the status of a health check\. If you choose this option, Route 53 considers health checks to be unhealthy when the status is healthy and vice versa\.

**  Disabled **  
Stops Route 53 from performing health checks\. When you disable a health check, Route 53 stops aggregating the status of the referenced health checks\.  
After you disable a health check, Route 53 considers the status of the health check to always be healthy\. If you configured DNS failover, Route 53 continues to route traffic to the corresponding resources\. If you want to stop routing traffic to a resource, change the value of [Invert health check status](#health-checks-creating-values-invert-health-check-status)\.  
Charges for a health check still apply when the health check is disabled\.

## Monitoring a CloudWatch alarm<a name="health-checks-creating-values-cloudwatch"></a>

If you want this health check to monitor the alarm state of a CloudWatch alarm, specify the following values:
+ [CloudWatch alarm](#health-checks-creating-values-cloudwatch-alarm)
+ [Health check status](#health-checks-creating-values-health-check-status)
+ [Invert health check status](#health-checks-creating-values-invert-health-check-status-cloudwatch)
+ [Disabled](#health-checks-creating-values-disabled-cloudwatch)

**CloudWatch alarm**  
Choose the CloudWatch alarm that you want Route 53 to use to determine whether this health check is healthy\.  
Route 53 supports CloudWatch alarms with the following features:  
+ Standard\-resolution metrics\. High\-resolution metrics aren't supported\. For more information, see [High\-resolution metrics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/publishingMetrics.html#high-resolution-metrics) in the *Amazon CloudWatch User Guide*\.
+ Statistics: `Average`, `Minimum`, `Maximum`, `Sum`, and `SampleCount`\. Extended statistics aren't supported\.
Route 53 does not support alarms that use [metric math](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/using-metric-math.html) to query multiple CloudWatch metrics\. 
If you want to create an alarm, perform the following steps:  

1. Choose **create**\. The CloudWatch console appears in a new browser tab\.

1. Enter the applicable values\. For more information, see [Create or edit a CloudWatch alarm](https://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/ConsoleAlarms.html) in the *Amazon CloudWatch User Guide*\.

1. Return to the browser tab that the Route 53 console appears in\.

1. Choose the refresh button next to the **CloudWatch alarm** list\.

1. Choose the new alarm from the list\.
If you change settings for the CloudWatch alarm after you create a health check, you must update the health check\. For more information, see [Updating health checks when you change CloudWatch alarm settings \(health checks that monitor a CloudWatch alarm only\)Updating health checks when you change CloudWatch alarm settings](health-checks-updating-cloudwatch-alarm-settings.md)\.

**Health check status**  
Choose the status of the health check \(healthy, unhealthy, or last known status\) when CloudWatch has insufficient data to determine the state of the alarm that you chose for **CloudWatch alarm**\. If you choose to use the last known status, Route 53 uses the status of the health check from the last time that CloudWatch had sufficient data to determine the alarm state\. For new health checks that have no last known status, the default status for the health check is healthy\.   
The value of **Health check status** provides a temporary status when the data stream for a CloudWatch metric is briefly unavailable\. \(Route 53 monitors data streams for CloudWatch metrics, not the state of the corresponding alarm\.\) If the metric will be unavailable frequently or for long periods \(longer than a few hours\), we recommend that you not use the last known status\.

**Invert health check status**  
Choose whether you want Route 53 to invert the status of a health check\. If you choose this option, Route 53 considers health checks to be unhealthy when the status is healthy and vice versa\.

**  Disabled **  
Stops Route 53 from performing health checks\. When you disable a health check, Route 53 stops monitoring the corresponding CloudWatch metrics\.  
After you disable a health check, Route 53 considers the status of the health check to always be healthy\. If you configured DNS failover, Route 53 continues to route traffic to the corresponding resources\. If you want to stop routing traffic to a resource, change the value of [Invert health check status](#health-checks-creating-values-invert-health-check-status-cloudwatch)\.  
Charges for a health check still apply when the health check is disabled\.

## Advanced configuration \("Monitor an Endpoint" only\)<a name="health-checks-creating-values-advanced"></a>

If you choose the option to monitor an endpoint, you can also specify the following settings:
+ [Request interval](#health-checks-creating-values-request-interval)
+ [Failure threshold](#health-checks-creating-values-failure-threshold)
+ [String matching](#health-checks-creating-values-string-matching)
+ [Search string](#health-checks-creating-values-search-string)
+ [Latency graphs](#health-checks-creating-values-latency-graphs)
+ [Enable SNI](#health-checks-creating-values-enable-sni)
+ [Health checker regions](#health-checks-creating-values-health-checker-regions)
+ [Invert health check status](#health-checks-creating-values-invert-health-check-status-advanced)
+ [Disabled](#health-checks-creating-values-disabled-advanced)

**Request interval**  
The number of seconds between the time that each Route 53 health checker gets a response from your endpoint and the time that it sends the next health check request\. If you choose an interval of 30 seconds, each of the Route 53 health checkers in data centers around the world will send your endpoint a health check request every 30 seconds\. On average, your endpoint will receive a health check request about every two seconds\. If you choose an interval of 10 seconds, the endpoint will receive a request more than once per second\.  
Note that Route 53 health checkers in different data centers don't coordinate with one another, so you'll sometimes see several requests per second regardless of the interval you chose, followed by a few seconds with no health checks at all\.  
After you create a health check, you can't change the value of **Request interval**\.   
If you choose **Fast \(10 seconds\)** for the value of **Request interval**, an additional charge applies\. For more information, see [Route 53 Pricing](https://aws.amazon.com/route53/pricing/)\.

**Failure threshold**  
The number of consecutive health checks that an endpoint must pass or fail for Route 53 to change the current status of the endpoint from unhealthy to healthy or vice versa\. For more information, see [How Amazon Route 53 determines whether a health check is healthyHow Route 53 determines whether a health check is healthy](dns-failover-determining-health-of-endpoints.md)\.

**String matching \(HTTP and HTTPS Only\)**  
Whether you want Route 53 to determine the health of an endpoint by submitting an HTTP or HTTPS request to the endpoint and searching the response body for a specified string\. If the response body contains the value that you specify in **Search string**, Route 53 considers the endpoint healthy\. If not, or if the endpoint doesn't respond, Route 53 considers the endpoint unhealthy\. The search string must appear entirely within the first 5,120 bytes of the response body\.  
After you create a health check, you can't change the value of **String matching**\.   
If you choose **Yes** for the value of **String matching**, an additional charge applies\. For more information, see [Route 53 Pricing](https://aws.amazon.com/route53/pricing/)\.

**Search string \(Only When "String matching" Is Enabled\)**  
The string that you want Route 53 to search for in the body of the response from your endpoint\. The maximum length is 255 characters\.  
Route 53 considers case when searching for **Search string** in the response body\.

**Latency graphs**  
Choose whether you want Route 53 to measure the latency between health checkers in multiple AWS Regions and your endpoint\. If you choose this option, CloudWatch latency graphs appear on the **Latency** tab on the **Health checks** page in the Route 53 console\. If Route 53 health checkers can't connect to the endpoint, Route 53 can't display latency graphs for that endpoint\.   
After you create a health check, you can't change the value of **Latency measurements**\.   
If you configure Route 53 to measure the latency between health checkers and your endpoint, an additional charge applies\. For more information, see [Route 53 Pricing](https://aws.amazon.com/route53/pricing/)\.

**Enable SNI \(HTTPS Only\)**  
Specify whether you want Route 53 to send the host name to the endpoint in the `client_hello` message during TLS negotiation\. This allows the endpoint to respond to the HTTPS request with the applicable SSL/TLS certificate\.  
Some endpoints require that HTTPS requests include the host name in the `client_hello` message\. If you don't enable SNI, the status of the health check will be `SSL alert handshake_failure`\. A health check can also have that status for other reasons\. If SNI is enabled and you're still getting the error, check the SSL/TLS configuration on your endpoint and confirm that your certificate is valid\.  
Note the following requirements:  
+ The endpoint must support SNI\.
+ The SSL/TLS certificate on your endpoint includes a domain name in the `Common Name` field and possibly several more in the `Subject Alternative Names` field\. One of the domain names in the certificate must match the value that you specify for **Host name**\.  

**Health checker regions**  
Choose whether you want Route 53 to check the health of the endpoint by using health checkers in the recommended regions or by using health checkers in regions that you specify\.  
If you update a health check to remove a region that has been performing health checks, Route 53 continues to perform checks from that region for up to an hour\. This ensures that some health checkers are always checking the endpoint \(for example, if you replace three regions with four different regions\)\.   
If you choose **Customize**, choose the **x** for a region to remove it\. Click the space at the bottom of the list to add a region back to the list\. You must specify at least three regions\.

**Invert health check status**  
Choose whether you want Route 53 to invert the status of a health check\. If you choose this option, Route 53 considers health checks to be unhealthy when the status is healthy and vice versa\. For example, you might want Route 53 to consider a health check *unhealthy* if you configure string matching and the endpoint returns a specified value\. For more information about health checks that perform string matching, see [String matching](#health-checks-creating-values-string-matching)\.

**  Disabled **  
Stops Route 53 from performing health checks\. When you disable a health check, Route 53 stops trying to establish a TCP connection with the endpoint\.  
After you disable a health check, Route 53 considers the status of the health check to always be healthy\. If you configured DNS failover, Route 53 continues to route traffic to the corresponding resources\. If you want to stop routing traffic to a resource, change the value of [Invert health check status](#health-checks-creating-values-invert-health-check-status-advanced)\.  
Charges for a health check still apply when the health check is disabled\.

## Get notified when a health check fails<a name="health-checks-creating-values-alarm"></a>

Use the following options to configure email notification when a health check fails:
+ [Create alarm](#health-checks-creating-values-create-alarm)
+ [Send notification to](#health-checks-creating-values-send-notification-to)
+ [Topic name](#health-checks-creating-values-topic-name)
+ [Recipient email addresses](#health-checks-creating-values-recipient-email-addresses)

**Create alarm \(Only When Creating Health Checks\)**  
Specify whether you want to create a default CloudWatch alarm\. If you choose **Yes**, CloudWatch sends you an Amazon SNS notification when the status of this endpoint changes to unhealthy and Route 53 considers the endpoint unhealthy for one minute\.  
If you want CloudWatch to send you another Amazon SNS notification when the status changes back to healthy, you can create another alarm after you create the health check\. For more information, see [Creating Amazon CloudWatch alarms](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html) in the *Amazon CloudWatch User Guide*\.
If you want to create an alarm for an existing health check or you want to receive notifications when Route 53 considers the endpoint unhealthy for more or less than one minute \(the default value\), select **No**, and add an alarm after you create the health check\. For more information, see [Monitoring health checks using CloudWatch](monitoring-health-checks.md)\.

**Send notification to \(Only When Creating an Alarm\)**  
Specify whether you want CloudWatch to send notifications to an existing Amazon SNS topic or to a new one:  
+ **Existing SNS topic** – Select the name of the topic from the list\. The topic must be in the US East \(N\. Virginia\) Region\.
+ **New SNS topic** – Enter a name for the topic in **Topic name**, and enter the email addresses that you want to send notifications to in **Recipients**\. Separate multiple addresses with commas \(,\), semicolons \(;\), or spaces\. 

  Route 53 will create the topic in the US East \(N\. Virginia\) Region\.

**Topic name \(Only When Creating a New SNS Topic\)**  
If you specified **New SNS Topic**, enter the name of the new topic\. 

**Recipient email addresses \(Only When Creating a New SNS Topic\)**  
If you specified **New SNS topic**, enter the email addresses that you want to send notifications to\. Separate multiple names with commas \(,\), semicolons \(;\), or spaces\.