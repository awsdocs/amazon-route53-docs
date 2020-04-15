# Configuring failover in a private hosted zone<a name="dns-failover-private-hosted-zones"></a>

If you're creating failover records in a private hosted zone, note the following:
+ Route 53 health checkers are outside the VPC\. To check the health of an endpoint within a VPC by IP address, you must assign a public IP address to the instance in the VPC\.
+ You can configure a health checker to check the health of an external resource that the instance relies on, such as a database server\.
+ You can create a CloudWatch metric, associate an alarm with the metric, and then create a health check that is based on the data stream for the alarm\. For example, you might create a CloudWatch metric that checks the status of the EC2 `StatusCheckFailed` metric, add an alarm to the metric, and then create a health check that is based on the data stream for the alarm\. For information about creating CloudWatch metrics and alarms by using the CloudWatch console, see the [Amazon CloudWatch User Guide](https://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/)\.

For more information, see [Working with private hosted zones](hosted-zones-private.md)\.