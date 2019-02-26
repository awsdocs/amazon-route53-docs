# How Amazon Route 53 Determines Whether a Health Check Is Healthy<a name="dns-failover-determining-health-of-endpoints"></a>

The method that Amazon Route 53 uses to determine whether a health check is healthy depends on the type of health check\.

**Topics**
+ [Health Checks That Monitor an Endpoint](#dns-failover-determining-health-of-endpoints-monitor-endpoint)
+ [Health Checks That Monitor Other Health Checks](#dns-failover-determining-health-of-endpoints-calculated)
+ [Health Checks That Monitor CloudWatch Alarms](#dns-failover-determining-health-of-endpoints-cloudwatch)

## Health Checks That Monitor an Endpoint<a name="dns-failover-determining-health-of-endpoints-monitor-endpoint"></a>

Route 53 has health checkers in locations around the world\. When you create a health check that monitors an endpoint, health checkers start to send requests to the endpoint that you specify to determine whether the endpoint is healthy\. You can choose which locations you want Route 53 to use, and you can specify the interval between checks: every 10 seconds or every 30 seconds\. Note that Route 53 health checkers in different data centers don't coordinate with one another, so you'll sometimes see several requests per second regardless of the interval you chose, followed by a few seconds with no health checks at all\. 

Each health checker evaluates the health of the endpoint based on two values:
+ Response time
+ Whether the endpoint responds to a number of consecutive health checks that you specify \(the failure threshold\)

Route 53 aggregates the data from the health checkers and determines whether the endpoint is healthy:
+ If more than 18% of health checkers report that an endpoint is healthy, Route 53 considers it healthy\.
+ If 18% of health checkers or fewer report that an endpoint is healthy, Route 53 considers it unhealthy\.

The 18% value was chosen to ensure that health checkers in multiple regions consider the endpoint healthy\. This prevents an endpoint from being considered unhealthy only because network conditions have isolated the endpoint from some health\-checking locations\. This value might change in a future release\.

The response time that an individual health checker uses to determine whether an endpoint is healthy depends on the type of health check:
+ **HTTP and HTTPS health checks** – Route 53 must be able to establish a TCP connection with the endpoint within four seconds\. In addition, the endpoint must respond with an HTTP status code of 2xx or 3xx within two seconds after connecting\.
+ **TCP health checks** – Route 53 must be able to establish a TCP connection with the endpoint within ten seconds\.
+ **HTTP and HTTPS health checks with string matching** – As with HTTP and HTTPS health checks, Route 53 must be able to establish a TCP connection with the endpoint within four seconds, and the endpoint must respond with an HTTP status code of 2xx or 3xx within two seconds after connecting\. 

  After a Route 53 health checker receives the HTTP status code, it must receive the response body from the endpoint within the next two seconds\. Route 53 searches the response body for a string that you specify\. The string must appear entirely in the first 5,120 bytes of the response body or the endpoint fails the health check\. If you're using the Route 53 console, you specify the string in the **Search String** field\. If you're using the Route 53 API, you specify the string in the `SearchString` element when you create the health check\. 

For health checks that monitor an endpoint \(except TCP health checks\), if the response from the endpoint includes any headers, the headers must be in the format that is defined in RFC7230, Hypertext Transfer Protocol \(HTTP/1\.1\): Message Syntax and Routing, [section 3\.2, "Header Fields\."](https://tools.ietf.org/html/rfc7230#section-3.2)

## Health Checks That Monitor Other Health Checks<a name="dns-failover-determining-health-of-endpoints-calculated"></a>

A health check can monitor the status of other health checks; this type of health check is known as a *calculated health check*\. The health check that does the monitoring is the *parent health check*, and the health checks that are monitored are *child health checks*\. One parent health check can monitor the health of up to 255 child health checks\. Here's how the monitoring works:
+ Route 53 adds up the number of child health checks that are considered to be healthy\.
+ Route 53 compares that number with the number of child health checks that must be healthy for the status of the parent health check to be considered healthy\.

For more information, see [Monitoring Other Health Checks \(Calculated Health Checks\)](health-checks-creating-values.md#health-checks-creating-values-calculated) in [Values That You Specify When You Create or Update Health Checks](health-checks-creating-values.md)\.

## Health Checks That Monitor CloudWatch Alarms<a name="dns-failover-determining-health-of-endpoints-cloudwatch"></a>

When you create a health check that is based on a CloudWatch alarm, Route 53 monitors the data stream for the corresponding alarm instead of monitoring the alarm state\. If the data stream indicates that the state of the alarm is **OK**, the health check is considered healthy\. If the data stream indicates that the state is **Alarm**, the health check is considered unhealthy\. If the data stream doesn't provide enough information to determine the state of the alarm, the health check status depends on the setting for **Health check status**: healthy, unhealthy, or last known status\. \(In the Route 53 API, this setting is `InsufficientDataHealthStatus`\.\)

**Note**  
Because Route 53 health checks monitor CloudWatch data streams instead of the state of CloudWatch alarms, you can't force the status of a health check to change by using the CloudWatch [SetAlarmState](https://docs.aws.amazon.com/AmazonCloudWatch/latest/APIReference/API_SetAlarmState.html) API operation\.