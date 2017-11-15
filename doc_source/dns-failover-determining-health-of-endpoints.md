# How Amazon Route 53 Determines Whether an Endpoint Is Healthy<a name="dns-failover-determining-health-of-endpoints"></a>

Amazon Route 53 determines whether the endpoint associated with a health check is healthy based on response time and on the number of failed or passed health checks:

+ **HTTP and HTTPS health checks** – Amazon Route 53 must be able to establish a TCP connection with the endpoint within four seconds\. In addition, the endpoint must respond with an HTTP status code of 200 or greater and less than 400 within two seconds after connecting\.

+ **TCP health checks** – Amazon Route 53 must be able to establish a TCP connection with the endpoint within ten seconds\.

+ **HTTP and HTTPS health checks with string matching** – As with HTTP and HTTPS health checks, Amazon Route 53 must be able to establish a TCP connection with the endpoint within four seconds, and the endpoint must respond with an HTTP status code of 200 or greater and less than 400 within two seconds after connecting\. 

  After an Amazon Route 53 health checker receives the HTTP status code, it must receive the response body from the endpoint within the next two seconds\. Amazon Route 53 searches the response body for a string that you specify\. The string must appear entirely in the first 5120 bytes of the response body or the endpoint fails the health check\. If you're using the Amazon Route 53 console, you specify the string in the **Search String** field\. If you're using the Amazon Route 53 API, you specify the string in the `SearchString` element when you create the health check\. 

+ **Calculated health checks** – For health checks that monitor the status of other health checks, Amazon Route 53 adds up the number of health checks that Amazon Route 53 health checkers consider to be healthy\. It then compares that number with the number of child health checks that must be healthy for the status of the health check to be considered healthy\. 

+ **Health checks based on the state of CloudWatch alarms** – If the state of a CloudWatch alarm is **OK**, the health check is considered healthy\. If the state is **Alarm**, the health check is considered unhealthy\. If CloudWatch doesn't have sufficient data to determine whether the state is **OK** or **Alarm**, the health check status depends on the setting for **Health check status**: healthy, unhealthy, or last known status\. \(In the Amazon Route 53 API, this setting is `InsufficientDataHealthStatus`\.\)

For more information, see [Creating, Updating, and Deleting Health Checks](health-checks-creating-deleting.md)\.

When you create a health check, here's what happens:

1. Amazon Route 53 propagates the health check configuration to the servers that perform health checks in AWS data centers around the world\. 

1. A health\-checking application \(a health checker\) in each data center sends a request to the endpoint that you specify at the request interval that you specify: every 10 seconds or every 30 seconds\. The request interval is the number of seconds between the time that Amazon Route 53 gets a response from your endpoint and the time that it sends the next health\-check request\.

1. When the endpoint either passes or fails a consecutive number of health checks that you specify \(the failure threshold\), Amazon Route 53 updates the health status of the endpoint\. Thereafter, the health status of an endpoint changes from healthy to unhealthy \(or vice versa\) after it fails \(or passes\) the same number of consecutive checks\.

1. Each Amazon Route 53 health checker propagates the results of its health checks to Amazon Route 53 DNS servers worldwide\. If more than 18% of available health checkers report that an endpoint is healthy, Amazon Route 53 responds to queries using the associated records when applicable\. If 18% of health checkers or fewer report that an endpoint is healthy, Amazon Route 53 typically does not respond to queries using the associated records\. The 18% value might change in a future release\.