# How Amazon Route 53 Determines Whether an Endpoint Is Healthy<a name="dns-failover-determining-health-of-endpoints"></a>

The method that Amazon Route 53 uses to determine whether a health check is healthy depends on the type of health check\.


+ [Health Checks That Monitor an Endpoint](#dns-failover-determining-health-of-endpoints-monitor-endpoint)
+ [Health Checks That Monitor Other Health Checks](#dns-failover-determining-health-of-endpoints-calculated)
+ [Health Checks That Monitor CloudWatch Alarms](#dns-failover-determining-health-of-endpoints-cloudwatch)

## Health Checks That Monitor an Endpoint<a name="dns-failover-determining-health-of-endpoints-monitor-endpoint"></a>

Route 53 has health checkers in locations around the world\. When you create a health check that monitors an endpoint, health checkers start to send requests to the endpoint that you specify to determine whether the endpoint is healthy\. \(You can choose which locations you want Route 53 to use, and you can specify the interval between checks: every 10 seconds or every 30 seconds\.\) Each health checker evaluates the health of the endpoint based on two values:

+ Response time

+ Whether the endpoint responds to a number of consecutive health checks that you specify \(the failure threshold\)

Route 53 aggregates the data from the health checkers and determines whether the endpoint is healthy:

+ If more than 18% of health checkers report that an endpoint is healthy, Route 53 considers it healthy\.

+ If 18% or fewer of health checkers report that an endpoint is healthy, Route 53 considers it unhealthy\.

The 18% value was chosen to ensure that health checkers in multiple regions consider the endpoint healthy\. This prevents an endpoint from being considered unhealthy only because network conditions have isolated the endpoint from some health\-checking locations\. This value might change in a future release\.

The response time that an individual health checker uses to determine whether an endpoint is healthy depends on the type of health check:

+ **HTTP and HTTPS health checks** – Route 53 must be able to establish a TCP connection with the endpoint within four seconds\. In addition, the endpoint must respond with an HTTP status code of 200 or greater and less than 400 within two seconds after connecting\.

+ **TCP health checks** – Route 53 must be able to establish a TCP connection with the endpoint within ten seconds\.

+ **HTTP and HTTPS health checks with string matching** – As with HTTP and HTTPS health checks, Route 53 must be able to establish a TCP connection with the endpoint within four seconds, and the endpoint must respond with an HTTP status code of 200 or greater and less than 400 within two seconds after connecting\. 

  After a Route 53 health checker receives the HTTP status code, it must receive the response body from the endpoint within the next two seconds\. Route 53 searches the response body for a string that you specify\. The string must appear entirely in the first 5120 bytes of the response body or the endpoint fails the health check\. If you're using the Route 53 console, you specify the string in the **Search String** field\. If you're using the Route 53 API, you specify the string in the `SearchString` element when you create the health check\. 

## Health Checks That Monitor Other Health Checks<a name="dns-failover-determining-health-of-endpoints-calculated"></a>

For health checks that monitor the status of other health checks, Route 53 adds up the number of health checks that Route 53 health checkers consider to be healthy\. Route 53 then compares that number with the number of child health checks that must be healthy for the status of the health check to be considered healthy\. 

## Health Checks That Monitor CloudWatch Alarms<a name="dns-failover-determining-health-of-endpoints-cloudwatch"></a>

If the state of a CloudWatch alarm is **OK**, the health check is considered healthy\. If the state is **Alarm**, the health check is considered unhealthy\. If CloudWatch doesn't have sufficient data to determine whether the state is **OK** or **Alarm**, the health check status depends on the setting for **Health check status**: healthy, unhealthy, or last known status\. \(In the Route 53 API, this setting is `InsufficientDataHealthStatus`\.\) 