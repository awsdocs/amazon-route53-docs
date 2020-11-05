# VPC association<a name="hz-type-private-associate-vpc"></a>

When you associate one or more VPCs with a hosted zone, Route 53 uses the records in the hosted zone to route traffic within and among the VPCs\.

You can use the console to associate VPCs with a hosted zone only if the VPCs and the hosted zone were created by the same AWS account\. If they were created using different AWS accounts, you must use a programmatic method, such as the AWS CLI, to associate the VPCs with the hosted zone\. 

To associate multiple VPCs with a hosted zone, choose the Region and VPC ID\. Then choose **Add**, and choose the next Region and VPC ID\. 

## Learn more<a name="hz-type-private-associate-vpc-learn-more"></a>
+ [Considerations when working with a private hosted zone](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/hosted-zone-private-considerations.html)
+ [associate\-vpc\-with\-hosted\-zone \(AWS CLI Command Reference\)](https://docs.aws.amazon.com/cli/latest/reference/route53/associate-vpc-with-hosted-zone.html)