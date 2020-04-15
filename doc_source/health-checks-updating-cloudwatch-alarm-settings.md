# Updating health checks when you change CloudWatch alarm settings \(health checks that monitor a CloudWatch alarm only\)<a name="health-checks-updating-cloudwatch-alarm-settings"></a>

If you create a Route 53 health check that monitors the data stream for a CloudWatch alarm and then you update the settings in the CloudWatch alarm, Route 53 doesn't automatically update the alarm settings in the health check\. If you want the health check to start using the new alarm settings, you need to update the health check\.

**Note**  
To update a health check programmatically, you can use the `UpdateHealthCheck` API\. Just specify the current values for `AlarmIdentifier` and `Region`, and Route 53 will get the latest settings from CloudWatch\. For more information, see [UpdateHealthCheck](https://docs.aws.amazon.com/Route53/latest/APIReference/API_UpdateHealthCheck.html) in the *Amazon Route 53 API Reference*\.<a name="health-checks-updating-cloudwatch-alarm-settings-procedure"></a>

**To update a health check with new CloudWatch alarm settings \(console\)**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Health Checks**\.

1. Select the check box for the health check that you want to update\.

1. Choose **Edit health check**\.

   A note explains that the CloudWatch alarm for the health check has changed\. The **Details** field shows the new alarm settings\.

1. Choose **Save**\.