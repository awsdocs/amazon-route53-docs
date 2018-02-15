# Configuring Failover in a Private Hosted Zone<a name="dns-failover-private-hosted-zones"></a>

If you're creating failover records in a private hosted zone, note the following:

+ Amazon Route 53 health checkers are outside the VPC\. To check the health of an endpoint within a VPC by IP address, you must assign a public IP address to the instance in the VPC\.

+ You can configure a health checker to check the health of an external resource that the instance relies on, such as a database server\.

+ You can create a CloudWatch metric, associate an alarm with the metric, and then create a health check that is based on the state of the alarm\. For example, you might create a CloudWatch metric that checks the status of the EC2 `StatusCheckFailed` metric, add an alarm to the metric, and then create a health check that is based on the state of the alarm\. For information about creating CloudWatch metrics and alarms by using the CloudWatch console, see the [Amazon CloudWatch User Guide](http://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/)\.

For more information, see the following topics:

+ [Working with Private Hosted Zones](hosted-zones-private.md)

+ [Creating and Updating Health Checks](health-checks-creating.md)

+ [Working with Records](rrsets-working-with.md)