# Amazon Route 53 Metrics and Dimensions<a name="metrics_dimensions"></a>

When you create a health check, Amazon Route 53 starts to send metrics and dimensions once a minute to CloudWatch about the resource that you specify\. The Route 53 console lets you view the status of your health checks\. You can also use the following procedures to view the metrics in the CloudWatch console or view them by using the AWS Command Line Interface \(AWS CLI\)\.

**To view metrics using the CloudWatch console**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. In the navigation pane, choose **Metrics**\.

1. On the **All Metrics** tab, choose **Route 53**\.

1. Choose **Health Check Metrics**\.

**To view metrics using the AWS CLI**

+ At a command prompt, use the following command:

  ```
  1. aws cloudwatch list-metrics --namespace "AWS/Route53"
  ```


+ [Route 53 Metrics](#route-53-metrics-list)
+ [Dimensions for Route 53 Metrics](#route-53-metrics-dimensions)

## Route 53 Metrics<a name="route-53-metrics-list"></a>

The `AWS/Route53` namespace includes the following metrics\.


| Metric | Description | 
| --- | --- | 
|  `ChildHealthCheckHealthyCount`  |  For a calculated health check, the number of health checks that are healthy among the health checks that Route 53 is monitoring\. Valid statistics: Average \(recommended\), Minimum, Maximum Units: Healthy health checks  | 
|  `ConnectionTime`  |  The average time, in milliseconds, that it took Route 53 health checkers to establish a TCP connection with the endpoint\. You can view `ConnectionTime` for a health check either across all regions or for a selected geographic region\. Valid statistics: Average \(recommended\), Minimum, Maximum Units: Milliseconds  | 
|  `HealthCheckPercentageHealthy`  |  The percentage of Route 53 health checkers that consider the selected endpoint to be healthy\. You can view `HealthCheckPercentageHealthy` only across all regions; data is not available for a selected region\. Valid statistics: Average, Minimum, Maximum Units: Percent  | 
|  `HealthCheckStatus`  |  The status of the health check endpoint that CloudWatch is checking\. **1** indicates healthy, and **0** indicates unhealthy\. You can view `HealthCheckStatus` only across all regions; data is not available for a selected region\. Valid statistics: Minimum Units: none  | 
|  `SSLHandshakeTime`  |  The average time, in milliseconds, that it took Route 53 health checkers to complete the SSL handshake\. You can view `SSLHandshakeTime` for a health check either across all regions or for a selected geographic region\. Valid statistics: Average \(recommended\), Minimum, Maximum Units: Milliseconds  | 
|  `TimeToFirstByte`  |  The average time, in milliseconds, that it took Route 53 health checkers to receive the first byte of the response to an HTTP or HTTPS request\. You can view `TimeToFirstByte` for a health check either across all regions or for a selected geographic region\. Valid statistics: Average \(recommended\), Minimum, Maximum Units: Milliseconds  | 

## Dimensions for Route 53 Metrics<a name="route-53-metrics-dimensions"></a>

Route 53 metrics use the `AWS/Route53` namespace and provide metrics for `HealthCheckId`\. When retrieving metrics, you must supply the `HealthCheckId` dimension\.

In addition, for `ConnectionTime`, `SSLHandshakeTime`, and `TimeToFirstByte`, you can optionally specify `Region`\. If you omit `Region`, CloudWatch returns metrics across all regions\. If you include `Region`, CloudWatch returns metrics only for the specified region\.

For more information, see [Monitoring Health Checks Using CloudWatch](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/monitoring-health-checks.html) in the *Amazon Route 53 Developer Guide*\.