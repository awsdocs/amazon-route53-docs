# Monitoring the latency between health checkers and your endpoint<a name="monitoring-health-check-latency"></a>

When you create a health check, if you choose to monitor the status of an endpoint \(not the status of other health checks\) and you choose the **Latency graphs** option, you can view the following values on CloudWatch graphs on the Route 53 console:
+ The average time, in milliseconds, that it took Route 53 health checkers to establish a TCP connection with the endpoint
+ The average time, in milliseconds, that it took Route 53 health checkers to receive the first byte of the response to an HTTP or HTTPS request
+ The average time, in milliseconds, that it took Route 53 health checkers to complete the SSL/TLS handshake

**Note**  
You can't enable latency monitoring for existing health checks\.<a name="monitoring-latency-procedure"></a>

**To view the latency between Route 53 health checkers and your endpoint \(console\)**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Health Checks**\. 

1. Select the rows for the applicable health checks\. You can view latency data only for health checks that monitor the status of an endpoint and for which the **Latency graphs** option is enabled\.

1. In the bottom pane, choose the **Latency** tab\.

1. Choose the time range and the geographic region that you want to display latency graphs for\.

   The graphs display the status for the specified time range:  
**TCP connection time \(HTTP and TCP only\)**  
The average time, in milliseconds, that it took Route 53 health checkers in the selected geographic region to establish a TCP connection with the endpoint\.  
**Time to first byte \(HTTP and HTTPS only\)**  
The average time, in milliseconds, that it took Route 53 health checkers in the selected geographic region to receive the first byte of the response to an HTTP or HTTPS request\.  
**Time to complete SSL handshake \(HTTPS only\)**  
The average time, in milliseconds, that it took Route 53 health checkers in the selected geographic region to complete the SSL/TLS handshake\.
**Note**  
If you select more than one health check, the graph displays a separate color\-coded line for each health check\.

1. To view a larger graph and specify different settings, click the graph\. You can change the following settings:  
**Statistic**  
Changes the calculation that CloudWatch performs on the data\.  
**Time range**  
Displays the status of a health check over a different period, for example, overnight or last week\.  
**Period**  
Changes the interval between data points in the graph\.

   Note the following:
   + If you just created a health check, you might need to wait for a few minutes for data to appear in the graph and for the health check metric to appear in the list of available metrics\.
   + The graph doesn't refresh itself automatically\. To update the display, choose the refresh \(![\[Icon to refresh the CloudWatch graph\]](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/images/cloudwatch-refresh-icon.png)\) icon\.
   + If health checks are failing for some reason, such as a connection timeout, Route 53 can't measure latency, and latency data will be missing from the graph for the affected period\.