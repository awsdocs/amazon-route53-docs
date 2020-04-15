# Viewing health check status and the reason for health check failures<a name="health-checks-view-status"></a>

On the Route 53 console, you can view the status \(healthy or unhealthy\) of your health checks as reported by Route 53 health checkers\. For all health checks except calculated health checks, you can also view the reason for the last health check failure, for example, health checkers were unable to establish a connection with the endpoint\. <a name="health-checks-view-status-console-proc"></a>

**To view the status and last failure reason for a health check \(console\)**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Health Checks**\.

1. For an overview of the status of all of your health checks—healthy or unhealthy—view the **Status** column\. For more information, see [How Amazon Route 53 determines whether a health check is healthyHow Route 53 determines whether a health check is healthy](dns-failover-determining-health-of-endpoints.md)\.

1. For all health checks except calculated health checks, you can view the status of the Route 53 health checkers that are checking the health of a specified endpoint\. Select the health check\.

1. In the bottom pane, choose the **Health Checkers** tab\.
**Note**  
New health checks must propagate to Route 53 health checkers before the health check status and last failure reason appear in the **Status** column\. Until propagation has finished, the message in that column explains that no status is available\.

1. Choose whether you want to view the current status of the health check, or view the date and time of the last failure and the reason for the failure\. The table on the **Status** tab includes the following values:  
**Health checker IP**  
The IP address of the Route 53 health checker that performed the health check\.  
**Last checked**  
The date and time of the health check or the date and time of the last failure, depending on the option that you select at the top of the **Status** tab\.  
**Status**  
Either the current status of the health check or the reason for the last health check failure, depending on the option that you select at the top of the **Status** tab\.