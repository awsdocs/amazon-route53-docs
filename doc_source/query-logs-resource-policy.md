# Edit or delete a CloudWatch Logs resource policy<a name="query-logs-resource-policy"></a>

Route 53 needs permission to save DNS query logs in the CloudWatch Logs log group that you specified in **Log group**\. A CloudWatch Logs resource policy gives Route 53 the required permissions\. 

If an existing resource policy grants the required permissions, you can continue with configuring query logging\.

If there is no existing resource policy, or if no existing resource policy grants the required permissions, and if you are below the maximum of 10 resource policies, a **Missing permission** message appears\. Choose **Grant permissions**, and Route 53 automatically creates a resource policy that grants Route 53 permission to save logs in any CloudWatch Logs log group\. 

If you already have the maximum number of 10 resource policies, you have two options:
+ You can delete an existing resource policy, and then choose **Grant permission**\. Route 53 automatically creates a resource policy that grants Route 53 permission to save logs in any CloudWatch Logs log group\.
+ You can edit an existing resource policy\. Route 53 replaces the existing resource policy with a resource policy that grants Route 53 permission to save logs in any CloudWatch Logs log group\. 

**Important**  
If you delete or edit an existing resource policy, you might prevent other services from performing other operations on other AWS resources\.

The table includes the following values:
+ **Policy name**: The name of the resource policy\.
+ **Last updated time**: The date and time that the resource policy was last updated\.
+ **Matches log group**: Indicates whether the resource specified in the resource policy matches the name of the CloudWatch Logs log group that you specified in **Log group**\.
+ **Grants permission**: Indicates whether the permissions in the resource policy grant Route 53 permission to save logs in the CloudWatch Logs log group that you specified in **Log group**\.

## Learn more<a name="query-logs-resource-policy-learn-more"></a>
+ [Logging DNS queries](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/query-logs.html)