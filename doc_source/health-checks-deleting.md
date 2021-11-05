# Deleting health checks<a name="health-checks-deleting"></a>

To delete health checks, perform the following procedure\.

**Note**  
If you're using AWS Cloud Map and you configured AWS Cloud Map to create a Route 53 health check when you register an instance, you can't use the Route 53 console to delete the health check\. The health check is deleted automatically when you deregister the instance\. There can be a delay of several hours before the health check no longer appears in the Route 53 console\. <a name="health-checks-deleting-console-proc"></a>

**To delete a health check \(console\)**

1. If you're deleting health checks that are associated with records, perform the recommended tasks in [Updating or deleting health checks when DNS failover is configured](health-checks-updating-deleting-tasks.md)\.

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Health Checks**\.

1. In the right pane, select the health check that you want to delete\.

1. Choose **Delete Health Check**\.

1. Choose **Yes, Delete** to confirm\.