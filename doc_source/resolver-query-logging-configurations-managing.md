# Managing Resolver query logging configurations<a name="resolver-query-logging-configurations-managing"></a>

## Configuring \(Resolver query logging\)<a name="resolver-query-logs-configuring"></a>

To start logging DNS queries that originate in your VPCs, you perform the following tasks in the Amazon Route 53 console:<a name="resolver-query-logs-configuring-procedure"></a>

**To configure Resolver query logging**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. Expand the Route 53 console menu\. In the upper left corner of the console, choose the three horizontal bars \(![\[Menu icon\]](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/images/menu-icon.png)\) icon\.

1. Within the Resolver menu, choose **Query logging**\.

1. In the Region selector, choose the AWS Region where you want to create the query logging configuration\. This must be the same Region where you created the VPCs that you want to log DNS queries for\. If you have VPCs in multiple regions, you must create at least one query logging configuration for each region\.

1. Choose **Configure query logging**\.

1. Specify the following values:  
**Query logging configuration name**  
Enter a name for your query logging configuration\. The name appears in the console in the list of query logging configurations\. Enter a name that will help you find this configuration later\.  
**Query logs destination**  
Choose the type of AWS resource that you want Resolver to send query logs to\. For information about how to choose among the options \(CloudWatch Logs log group, S3 bucket, and Kinesis Data Firehose delivery stream\), see [AWS resources that you can send Resolver query logs to](resolver-query-logs-choosing-target-resource.md)\.  
After you choose the type of resource, you can either create another resource of that type or choose an existing resource that was created by the current AWS account\.  
You can choose only resources that were created in the AWS Region that you chose in step 4, the Region where you're creating the query logging configuration\. If you choose to create a new resource, that resource will be created in the same Region\.  
**VPCs to log queries for**  
This query logging configuration will log DNS queries that originate in the VPCs that you choose\. Check the check box for each VPC in the current Region that you want Resolver to log queries for, then choose **Choose**\.

1. Choose **Configure query logging**\.

**Note**  
You should start to see DNS queries made by resources in your VPC in the logs within a few minutes of successfully creating the query logging configuration\.