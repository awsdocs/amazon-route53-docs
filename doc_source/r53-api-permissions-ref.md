# Amazon Route 53 API permissions: Actions, resources, and conditions reference<a name="r53-api-permissions-ref"></a>

When you set up [Access control](auth-and-access-control.md#access-control) and write a permissions policy that you can attach to an IAM identity \(identity\-based policies\), you can use the lists of [Actions, resources, and condition keys for Route 53](https://docs.aws.amazon.com/service-authorization/latest/reference/list_amazonroute53.html), [Actions, resources, and condition keys for Route 53 Domains](https://docs.aws.amazon.com/service-authorization/latest/reference/list_amazonroute53domains.html), and [Actions, resources, and condition keys for Route 53 Resolver](https://docs.aws.amazon.com/service-authorization/latest/reference/list_amazonroute53resolver.html) in the *Service Authorization Reference*\. The pages include each Amazon Route 53 API action, the actions that you must grant permissions access to, and the AWS resource that you must grant access to\. You specify the actions in the policy's `Action` field, and you specify the resource value in the policy's `Resource` field\. 

You can use AWS\-wide condition keys in your Route 53 policies to express conditions\. For a complete list of AWS\-wide keys, see [Available keys](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html#AvailableKeys) in the *IAM User Guide*\. 

**Note**  
When granting access, the hosted zone and the Amazon VPC must belong to the same partition\. A partition is a group of AWS Regions\. Each AWS account is scoped to one partition\.  
The following are the supported partitions:  
`aws` \- AWS Regions
`aws-cn` \- China Regions
`aws-us-gov` \- AWS GovCloud \(US\) Region
For more information, see [Access Management](https://docs.aws.amazon.com/general/latest/gr/aws-arns-and-namespaces.html) in the *AWS General Reference*\.

**Note**  
To specify an action, use the applicable prefix \(`route53`, `route53domains`, or `route53resolver`\) followed by the API operation name, for example:  
`route53:CreateHostedZone`
`route53domains:RegisterDomain`
`route53resolver:CreateResolverEndpoint`