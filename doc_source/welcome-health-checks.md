# How Amazon Route 53 checks the health of your resources<a name="welcome-health-checks"></a>

Amazon Route 53 health checks monitor the health of your resources such as web servers and email servers\. You can optionally configure Amazon CloudWatch alarms for your health checks, so that you receive notification when a resource becomes unavailable\. 

Here's an overview of how health checking works if you want to be notified when a resource becomes unavailable:

![\[Conceptual graphic that shows how you configure Route 53 to monitor the health of specified endpoints.\]](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/images/how-health-checks-work.png)

1. You create a health check and specify values that define how you want the health check to work, such as the following:
   + The IP address or domain name of the endpoint, such as a web server, that you want Route 53 to monitor\. \(You can also monitor the status of other health checks, or the state of a CloudWatch alarm\.\)
   + The protocol that you want Amazon Route 53 to use to perform the check: HTTP, HTTPS, or TCP\.
   + How often you want Route 53 to send a request to the endpoint\. This is the *request interval*\.
   + How many consecutive times the endpoint must fail to respond to requests before Route 53 considers it unhealthy\. This is the *failure threshold*\.
   + Optionally, how you want to be notified when Route 53 detects that the endpoint is unhealthy\. When you configure notification, Route 53 automatically sets a CloudWatch alarm\. CloudWatch uses Amazon SNS to notify users that an endpoint is unhealthy\.

1. Route 53 starts to send requests to the endpoint at the interval that you specified in the health check\. 

   If the endpoint responds to the requests, Route 53 considers the endpoint to be healthy and takes no action\. 

1. If the endpoint doesn't respond to a request, Route 53 starts to count the number of consecutive requests that the endpoint doesn't respond to:
   + If the count reaches the value that you specified for the failure threshold, Route 53 considers the endpoint unhealthy\. 
   + If the endpoint starts to respond again before the count reaches the failure threshold, Route 53 resets the count to 0, and CloudWatch doesn't contact you\.

1. If Route 53 considers the endpoint unhealthy and if you configured notification for the health check, Route 53 notifies CloudWatch\.

   If you didn't configure notification, you can still see the status of your Route 53 health checks in the Route 53 console\. For more information, see [Monitoring health check status and getting notifications](health-checks-monitor-view-status.md)\.

1. If you configured notification for the health check, CloudWatch triggers an alarm and uses Amazon SNS to send notification to the specified recipients\.

In addition to checking the health of a specified endpoint, you can configure a health check to check the health of one or more other health checks so that you can be notified when a specified number of resources, such as two web servers out of five, are unavailable\. You can also configure a health check to check the status of a CloudWatch alarm so that you can be notified on the basis of a broad range of criteria, not just whether a resource is responding to requests\.

If you have multiple resources that perform the same function, for example, web servers or database servers, and you want Route 53 to route traffic only to the resources that are healthy, you can configure DNS failover by associating a health check with each record for that resource\. If a health check determines that the underlying resource is unhealthy, Route 53 routes traffic away from the associated record\.

For more information about using Route 53 to monitor the health of your resources, see [Creating Amazon Route 53 health checks and configuring DNS failover](dns-failover.md)\.