# Creating Amazon Route 53 Health Checks and Configuring DNS Failover<a name="dns-failover"></a>

Amazon Route 53 health checks monitor the health and performance of your web applications, web servers, and other resources\. Each health check that you create can monitor one of the following:

+ The health of a specified resource, such as a web server

+ The status of other health checks

+ The status of an Amazon CloudWatch alarm

For an overview of the three types of health checks, see [Types of Amazon Route 53 Health ChecksTypes of Health Checks](health-checks-types.md)\. For information about creating health checks, see [Creating and Updating Health Checks](health-checks-creating.md)\.

After you create a health check, you can get the status of the health check, get notifications when the status changes, and configure DNS failover:

**Getting health check status and notifications**  
You can view the current and recent status of your health checks on the Route 53 console\. You can also work with health checks programmatically through one of the AWS SDKs, the AWS Command Line Interface, AWS Tools for Windows PowerShell, or the Route 53 API\.   
If you want to receive a notification when the status of a health check changes, you can configure an Amazon CloudWatch alarm for each health check\.  
For information about viewing health check status and receiving notifications, see [Monitoring Health Check Status and Getting Notifications](health-checks-monitor-view-status.md)\.

**Configuring DNS failover**  
If you have multiple resources that perform the same function, you can configure DNS failover so that Route 53 will route your traffic from an unhealthy resource to a healthy resource\. For example, if you have two web servers and one web server becomes unhealthy, Route 53 can route traffic to the other web server\. For more information, see [Configuring DNS Failover](dns-failover-configuring.md)\.


+ [Types of Amazon Route 53 Health Checks](health-checks-types.md)
+ [How Amazon Route 53 Determines Whether a Health Check Is Healthy](dns-failover-determining-health-of-endpoints.md)
+ [Creating, Updating, and Deleting Health Checks](health-checks-creating-deleting.md)
+ [Monitoring Health Check Status and Getting Notifications](health-checks-monitor-view-status.md)
+ [Configuring DNS Failover](dns-failover-configuring.md)
+ [Naming and Tagging Health Checks](health-checks-tagging.md)
+ [Using Health Checks with Amazon Route 53 API Versions Earlier than 2012\-12\-12](dns-failover-using-old-apis.md)