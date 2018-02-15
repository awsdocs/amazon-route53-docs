# Monitoring Health Check Status and Getting Notifications<a name="health-checks-monitor-view-status"></a>

You monitor the status of your health checks on the Amazon Route 53 console\. You can also set CloudWatch alarms and get automated notifications when the status of your health check status changes\. 


+ [Viewing Health Check Status and the Reason for Health Check Failures](#health-checks-view-status)
+ [Monitoring the Latency Between Health Checkers and Your Endpoint](#monitoring-health-check-latency)
+ [Monitoring Health Checks Using CloudWatch](#monitoring-health-checks)

## Viewing Health Check Status and the Reason for Health Check Failures<a name="health-checks-view-status"></a>

On the Route 53 console, you can view the status \(healthy or unhealthy\) of your health checks as reported by Route 53 health checkers\. For all health checks except calculated health checks, you can also view the reason for the last health check failure, for example, health checkers were unable to establish a connection with the endpoint\. 

**To view the status and last failure reason for a health check \(console\)**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Health Checks**\.

1. For an overview of the status of all of your health checks—healthy or unhealthy—view the **Status** column\. For more information, see [How Amazon Route 53 Determines Whether an Endpoint Is Healthy](dns-failover-determining-health-of-endpoints.md)\.

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

## Monitoring the Latency Between Health Checkers and Your Endpoint<a name="monitoring-health-check-latency"></a>

When you create a health check, if you choose to monitor the status of an endpoint \(not the status of other health checks\) and you choose the **Latency graphs** option, you can view the following values on CloudWatch graphs on the Amazon Route 53 console:

+ The average time, in milliseconds, that it took Route 53 health checkers to establish a TCP connection with the endpoint

+ The average time, in milliseconds, that it took Route 53 health checkers to receive the first byte of the response to an HTTP or HTTPS request

+ The average time, in milliseconds, that it took Route 53 health checkers to complete the SSL handshake 

**Note**  
You can't enable latency monitoring for existing health checks\.

**To view the latency between Route 53 health checkers and your endpoint \(console\)**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Health Checks**\. 

1. Select the rows for the applicable health checks\. You can view latency data only for health checks that monitor the status of an endpoint and for which the **Latency graphs** option is enabled\.

1. In the bottom pane, choose the **Latency** tab\.

1. Choose the time range and the geographic region for which you want to display latency graphs\.

   The graphs display the status for the specified time range:  
**TCP connection time \(HTTP and TCP only\)**  
The average time, in milliseconds, that it took Route 53 health checkers in the selected geographic region to establish a TCP connection with the endpoint\.  
**Time to first byte \(HTTP and HTTPS only\)**  
The average time, in milliseconds, that it took Route 53 health checkers in the selected geographic region to receive the first byte of the response to an HTTP or HTTPS request\.  
**Time to complete SSL handshake \(HTTPS only\)**  
The average time, in milliseconds, that it took Route 53 health checkers in the selected geographic region to complete the SSL handshake\.
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

## Monitoring Health Checks Using CloudWatch<a name="monitoring-health-checks"></a>

Amazon Route 53 health checks integrate with CloudWatch metrics so that you can do the following:

+ Verify that a health check is properly configured\.

+ Review the status of a health check over a specified period of time\.

+ Configure CloudWatch to send an Amazon Simple Notification Service \(Amazon SNS\) alert when the status of a health check is unhealthy\. Note that several minutes might elapse between the time that a health check fails and the time that you receive the associated Amazon SNS notification\. 

CloudWatch metrics are retained for two weeks\. 

For more information, see [How Amazon Route 53 Determines Whether an Endpoint Is Healthy](dns-failover-determining-health-of-endpoints.md)\.

+ [To view the status of a health check \(console\)](#monitoring-status-procedure)

+ [To receive an Amazon SNS notification when a health check status is unhealthy \(console\)](#monitoring-sns-notification-procedure)

+ [To view CloudWatch alarm status and edit alarms for Amazon Route 53 \(console\)](#monitoring-alarm-status-procedure)

+ [To view Route 53 metrics on the CloudWatch console](#monitoring-metrics-in-cloudwatch-console-procedure)

**To view the status of a health check \(console\)**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Health Checks**\. 

1. Choose the rows for the applicable health checks\. 

1. In the bottom pane, choose the **Monitoring** tab\.

   The two graphs display the status for the last hour in one\-minute intervals:  
**Health check status**  
The graph shows the Route 53 assessment of endpoint health\. **1** indicates healthy and **0** indicates unhealthy\.  
**Health checkers that report the endpoint healthy \(%\)**  
For health checks that monitor an endpoint only, the graph shows the percentage of Route 53 health checkers that consider the selected endpoint to be healthy\.  
**Number of healthy child health checks**  
For calculated health checks only, the graph shows the number of child health checks for which the status is healthy\. 
**Note**  
If you selected more than one health check, the graph displays a separate color\-coded line for each health check\.

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

**To receive an Amazon SNS notification when a health check status is unhealthy \(console\)**

1. In the navigation pane of the Amazon Route 53 console, choose **Health Checks**\.

1. Choose the row for the applicable health check\.

1. In the bottom pane, choose the **Alarms** tab\.

   The table lists the alarms that you've already created for this health check\.

1. Choose **Create Alarm**\.

1. Specify the following values:  
**Alarm name**  
Type the name that you want to see in the **Name** column in the table\.  
**Alarm description**  
\(Optional\) Type a description of the alarm\.  
**Send notification**  
Choose whether you want Route 53 to send you notification if the status of this health check triggers an alarm\.  
**Notification target \(Only when "Send notification" is "Yes"\)**  
If you want CloudWatch to send notification to an existing Amazon SNS topic, choose the topic from the list\.  
If you want CloudWatch to send notification but not to an existing Amazon SNS topic, do one of the following:  

   + **If you want CloudWatch to send email notification** – Choose **New SNS topic** and continue with this procedure\.

   + **If you want CloudWatch to send notification by another method** – Open a new browser tab, go to the Amazon SNS console, and create the new topic\. Then return to the Route 53 console, choose the name of the new topic from the **Notification target** list, and continue with this procedure\.  
**Topic name \(Only when you choose to create a new Amazon SNS topic\)**  
Type a name for the new Amazon SNS topic\.  
**Recipient email addresses \(Only when you choose to create a new Amazon SNS topic\)**  
Type the email address that you want Route 53 to send an Amazon SNS notification to when a health check triggers an alarm\.  
**Alarm target**  
Choose the value that you want Route 53 to evaluate for this health check:  

   + **Health check status** – Route 53 health checkers report that the health check is healthy or unhealthy

   + **Health checkers that report the endpoint healthy \(%\)** \(health checks that monitor an endpoint only\) – The percentage of Route 53 health checkers that report that the status of the health check is healthy

   + **Number of healthy child health checks** \(calculated health checks only\) – The number of child health checks in a calculated health check that report that the status of the health check is healthy

   + **TCP connection time** \(HTTP and TCP health checks only\) – The time in milliseconds that it took Route 53 health checkers to establish a TCP connection with the endpoint

   + **Time to complete SSL handshake** \(HTTPS health checks only\) – The time in milliseconds that it took Route 53 health checkers to complete the SSL handshake

   + **Time to first byte** \(HTTP and HTTPS health checks only\) – The time in milliseconds that it took Route 53 health checkers to receive the first byte of the response to an HTTP or HTTPS request  
**Alarm target**  
For the alarm targets that are based on latency \(**TCP connection time**, **Time to complete SSL handshake**, **Time to first byte**\), choose whether you want CloudWatch to calculate latency for Route 53 health checkers in a specific region or for all regions \(**Global**\)\.  
Note that if you choose a region, Route 53 measures latency only twice per minute, and the number of samples will be smaller than if you choose all regions\. As a result, outlying values are more likely\. To prevent spurious alarm notifications, we recommend that you specify a larger number of consecutive periods that the health check must fail before CloudWatch sends you a notification\.   
**Fulfill condition**  
Use the following settings to determine when CloudWatch should trigger an alarm:    
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/health-checks-monitor-view-status.html)  
**For at least *x* consecutive periods of *y* minutes/hours/day**  
Specify how many consecutive time periods that the specified value must meet the criteria before Route 53 sends notification\. Then specify the length of the time period\.

1. When you choose **Create**, Amazon SNS sends you an email with information about the new Amazon SNS topic\.

1. In the email, choose **Confirm subscription**\. You must confirm your subscription to begin receiving CloudWatch notifications\. 

**To view CloudWatch alarm status and edit alarms for Amazon Route 53 \(console\)**

1. In the navigation pane of the Amazon Route 53 console, choose **Health Checks**\.

1. Choose the row for any health check\.

1. In the details pane \(following *x* **Health Checks Selected**\), choose the right caret \(![\[Icon to expand the list of CloudWatch alarms\]](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/images/cloudwatch-expand-alarms-list.png)\) icon\.

   The **CloudWatch Alarms** list contains all of the Route 53 alarms that you have created using the current AWS account\.

   The **State** column shows the current status of each alarm:  
**OK**  
CloudWatch has accumulated enough statistics from Route 53 health checks to determine that the endpoint doesn't meet the alarm threshold\.  
**INSUFFICIENT DATA**  
CloudWatch hasn't accumulated enough statistics to determine whether the endpoint meets the alarm threshold\. This is the initial state of a new alarm\.  
**ALARM**  
CloudWatch has accumulated enough statistics from Route 53 health checks to determine that the endpoint meets the alarm threshold and to send notification to the specified email address\.

1. To view or edit settings for an alarm, choose the name of the alarm\.

1. To view an alarm in the CloudWatch console, which provides more detailed information about the alarm \(for example, a history of updates to the alarm and changes in status\), choose **View** in the **More Options** column for the alarm\.

1. To view all of the CloudWatch alarms that you have created using the current AWS account, including alarms for other AWS services, choose **View All CloudWatch Alarms**\.

1. To view all of the available CloudWatch metrics, including metrics that aren't currently being used by the current AWS account, choose **View All CloudWatch Metrics**\.

**To view Route 53 metrics on the CloudWatch console**

1. Sign in to the AWS Management Console and open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. Change the current region to **US East \(N\. Virginia\)**\. Route 53 metrics are not available if you select any other region as the current region\.

1. In the navigation pane, choose **Metrics**\.

1. On the **All metrics** tab, choose **Route 53**\.

1. Choose **Health Check Metrics**\.