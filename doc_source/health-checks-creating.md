# Creating and Updating Health Checks<a name="health-checks-creating"></a>

The following procedure describes how to create and update health checks using the Route 53 console\.

**To create or update a health check \(console\)**

1. If you're updating health checks that are already associated with records, perform the recommended tasks in [Updating or Deleting Health Checks When DNS Failover Is Configured](health-checks-updating-deleting-tasks.md)\.

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Health Checks**\.

1. If you want to update an existing health check, select the health check, and then choose **Edit Health Check**\.

   If you want to create a health check, choose **Create Health Check**\. For more information about each setting, move the mouse pointer over a label to see its tooltip\.

1. Enter the applicable values\. Note that some values can't be changed after you create a health check\. For more information, see [Values That You Specify When You Create or Update Health Checks](health-checks-creating-values.md)\.

1. Choose **Create Health Check**\.

1. Associate the health check with one or more Route 53 records\. For information about creating and updating records, see [Working with Records](rrsets-working-with.md)\.