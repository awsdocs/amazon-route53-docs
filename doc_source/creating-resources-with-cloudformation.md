# Creating Amazon Route 53 and Amazon Route 53 Resolver resources with AWS CloudFormation<a name="creating-resources-with-cloudformation"></a>

Amazon Route 53 and Amazon Route 53 Resolver are integrated with AWS CloudFormation, a service that helps you to model and set up your AWS resources so that you can spend less time creating and managing your resources and infrastructure\. You create a template that describes all the AWS resources that you want, and AWS CloudFormation provisions and configures those resources for you\. 

When you use AWS CloudFormation, you can reuse your template to set up your Route 53 and Route 53 Resolver resources consistently and repeatedly\. Describe your resources once, and then provision the same resources over and over in multiple AWS accounts and Regions\. 

## Route 53, Route 53 Resolver, and AWS CloudFormation templates<a name="working-with-templates"></a>

To provision and configure resources for Route 53, Route 53 Resolver, and related services, you must understand [AWS CloudFormation templates](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-guide.html)\. Templates are formatted text files in JSON or YAML\. These templates describe the resources that you want to provision in your AWS CloudFormation stacks\. If you're unfamiliar with JSON or YAML, you can use AWS CloudFormation Designer to help you get started with AWS CloudFormation templates\. For more information, see [What is AWS CloudFormation Designer?](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/working-with-templates-cfn-designer.html) in the *AWS CloudFormation User Guide*\.

Route 53 supports creating the following resource types in AWS CloudFormation:
+ `AWS::Route53::DNSSEC`
+ `AWS::Route53::HealthCheck`
+ `AWS::Route53::HostedZone`
+ `AWS::Route53::KeySigningKey`
+ `AWS::Route53::RecordSet`
+ `AWS::Route53::RecordSetGroup`

  For more information, including examples of JSON and YAML templates for Route 53 resources, see the [Amazon Route 53 resource type reference](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/AWS_Route53.html) in the *AWS CloudFormation User Guide*\.

Route 53 Resolver supports creating the following resource types in AWS CloudFormation:
+ `AWS::Route53Resolver::FirewallDomainList`
+ `AWS::Route53Resolver::FirewallDomainList`
+ `AWS::Route53Resolver::FirewallRuleGroupAssociation`
+ `AWS::Route53Resolver::ResolverDNSSECConfig`
+ `AWS::Route53Resolver::ResolverEndpoint`
+ `AWS::Route53Resolver::ResolverQueryLoggingConfig`
+ `AWS::Route53Resolver::ResolverQueryLoggingConfigAssociation`
+ `AWS::Route53Resolver::ResolverRule`
+ `AWS::Route53Resolver::ResolverRuleAssociation`

 For more information, including examples of JSON and YAML templates for Route 53 Resolver resources, see the [Amazon Route 53 Resolver resource type reference](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/AWS_Route53Resolver.html) in the *AWS CloudFormation User Guide*\.

## Learn more about AWS CloudFormation<a name="learn-more-cloudformation"></a>

To learn more about AWS CloudFormation, see the following resources:
+ [AWS CloudFormation](http://aws.amazon.com/cloudformation/)
+ [AWS CloudFormation User Guide](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/Welcome.html)
+ [AWS CloudFormation API Reference](https://docs.aws.amazon.com/AWSCloudFormation/latest/APIReference/Welcome.html)
+ [AWS CloudFormation Command Line Interface User Guide](https://docs.aws.amazon.com/cloudformation-cli/latest/userguide/what-is-cloudformation-cli.html)