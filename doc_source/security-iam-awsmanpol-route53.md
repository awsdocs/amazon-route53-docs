# AWS managed policies for Amazon Route 53<a name="security-iam-awsmanpol-route53"></a>

To add permissions to users, groups, and roles, it is easier to use AWS managed policies than to write policies yourself\. It takes time and expertise to [create IAM customer managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_create-console.html) that provide your team with only the permissions they need\. To get started quickly, you can use our AWS managed policies\. These policies cover common use cases and are available in your AWS account\. For more information about AWS managed policies, see [AWS managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *IAM User Guide*\.

AWS services maintain and update AWS managed policies\. You can't change the permissions in AWS managed policies\. Services occasionally add additional permissions to an AWS managed policy to support new features\. This type of update affects all identities \(users, groups, and roles\) where the policy is attached\. Services are most likely to update an AWS managed policy when a new feature is launched or when new operations become available\. Services do not remove permissions from an AWS managed policy, so policy updates won't break your existing permissions\.

Additionally, AWS supports managed policies for job functions that span multiple services\. For example, the **ViewOnlyAccess** AWS managed policy provides read\-only access to many AWS services and resources\. When a service launches a new feature, AWS adds read\-only permissions for new operations and resources\. For a list and descriptions of job function policies, see [AWS managed policies for job functions](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_job-functions.html) in the *IAM User Guide*\.

## AWS managed policy: AmazonRoute53FullAccess<a name="security-iam-awsmanpol-AmazonRoute53FullAccess"></a>

You can attach the `AmazonRoute53FullAccess` policy to your IAM identities\.

This policy grants full access to Route 53 resources, including domain registration and health checking, but excluding Resolver\.

**Permissions details**

This policy includes the following permissions\.
+ `route53:*` – Lets you perform all Route 53 actions *except* the following:
  + Create and update alias records for which the value of **Alias Target** is a CloudFront distribution, an Elastic Load Balancing load balancer, an Elastic Beanstalk environment, or an Amazon S3 bucket\. \(With these permissions, you can create alias records for which the value of **Alias Target** is another record in the same hosted zone\.\)
  + Work with private hosted zones\.
  + Work with domains\.
  + Create, delete, and view CloudWatch alarms\.
  + Render CloudWatch metrics in the Route 53 console\.
+ `route53domains:*`– Lets you work with domains\.
+ `cloudfront:ListDistributions` – Lets you create and update alias records for which the value of **Alias Target** is a CloudFront distribution\.

  This permission isn't required if you aren't using the Route 53 console\. Route 53 uses it only to get a list of distributions to display in the console\.
+ `elasticloadbalancing:DescribeLoadBalancers` – Lets you create and update alias records for which the value of **Alias Target** is an Elastic Load Balancing load balancer\.

  These permissions aren't required if you aren't using the Route 53 console\. Route 53 uses it only to get a list of load balancers to display in the console\.
+ `elasticbeanstalk:DescribeEnvironments` – Lets you create and update alias records for which the value of **Alias Target** is an Elastic Beanstalk environment\.

  These permissions aren't required if you aren't using the Route 53 console\. Route 53 uses it only to get a list of environments to display in the console\.
+ `s3:ListBucket`, `s3:GetBucketLocation`, and `s3:GetBucketWebsite` – Let you create and update alias records for which the value of **Alias Target** is an Amazon S3 bucket\. \(You can create an alias to an Amazon S3 bucket only if the bucket is configured as a website endpoint; `s3:GetBucketWebsite` gets the required configuration information\.\)

  These permissions aren't required if you aren't using the Route 53 console\. Route 53 uses these only to get a list of buckets to display in the console\.
+  `ec2:DescribeVpcs` – Lets you display a list of VPCs\.
+  `ec2:DescribeVpcEndpoints` – Lets you display a list of VPC endpoints\.
+  `ec2:DescribeRegions` – Lets you display a list of Availability Zones\.
+ `sns:ListTopics`, `sns:ListSubscriptionsByTopic`, `cloudwatch:DescribeAlarms` – Let you create, delete, and view CloudWatch alarms\.
+ `cloudwatch:GetMetricStatistics` – Lets you create CloudWatch metric health checks\.

  These permissions aren't required if you aren't using the Route 53 console\. Route 53 uses it only to get statistics to display in the console\.
+ `apigateway:GET` – Lets you create and update alias records for which the value of **Alias Target** is an Amazon API Gateway API\.

  This permission isn't required if you aren't using the Route 53 console\. Route 53 uses it only to get a list of APIs to display in the console\.

 For more information about the permissions, see [Amazon Route 53 API permissions: Actions, resources, and conditions reference](r53-api-permissions-ref.md), 

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "route53:*",
                "route53domains:*",
                "cloudfront:ListDistributions",
                "elasticloadbalancing:DescribeLoadBalancers",
                "elasticbeanstalk:DescribeEnvironments",
                "s3:ListBucket",
                "s3:GetBucketLocation",
                "s3:GetBucketWebsite",
                "ec2:DescribeVpcs",
                "ec2:DescribeVpcEndpoints",
                "ec2:DescribeRegions",
                "sns:ListTopics",
                "sns:ListSubscriptionsByTopic",
                "cloudwatch:DescribeAlarms",
                "cloudwatch:GetMetricStatistics"
            ],
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": "apigateway:GET",
            "Resource": "arn:aws:apigateway:*::/domainnames"
        }
    ]
}
```

## AWS managed policy: AmazonRoute53ReadOnlyAccess<a name="security-iam-awsmanpol-AmazonRoute53ReadOnlyAccess"></a>

You can attach the `AmazonRoute53ReadOnlyAccess` policy to your IAM identities\.

This policy grants read\-only access to Route 53 resources, including domain registration and health checking, but excluding Resolver\.

**Permissions details**

This policy includes the following permissions\. 
+ `route53:Get*` – Gets the Route 53 resources\.
+ `route53:List*` – Lists the Route 53 resources\.
+ `route53:TestDNSAnswer` – Gets the value that Route 53 returns in response to a DNS request\.

 For more information about the permissions, see [Amazon Route 53 API permissions: Actions, resources, and conditions reference](r53-api-permissions-ref.md), 

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "route53:Get*",
                "route53:List*",
                "route53:TestDNSAnswer"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```

## AWS managed policy: AmazonRoute53DomainsFullAccess<a name="security-iam-awsmanpol-AmazonRoute53DomainsFullAccess"></a>

You can attach the `AmazonRoute53DomainsFullAccess` policy to your IAM identities\.

This policy grants full access to Route 53 domain registration resources\.

**Permissions details**

This policy includes the following permissions\. 
+ `route53:CreateHostedZone` – Lets you create a Route 53 hosted zone\.
+ `route53domains:*` – Lets you register domain names and perform related operations\.

 For more information about the permissions, see [Amazon Route 53 API permissions: Actions, resources, and conditions reference](r53-api-permissions-ref.md), 

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "route53:CreateHostedZone",
                "route53domains:*"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```

## AWS managed policy: AmazonRoute53DomainsReadOnlyAccess<a name="security-iam-awsmanpol-AmazonRoute53DomainsReadOnlyAccess"></a>

You can attach the `AmazonRoute53DomainsReadOnlyAccess` policy to your IAM identities\.

This policy grants read\-only access to Route 53 domain registration resources\.

**Permissions details**

This policy includes the following permissions\. 
+ `route53domains:Get*` – Lets you retrieve a list of domains from Route 53\.
+ `route53domains:List*` – Lets you display a list of Route 53 domains\.

 For more information about the permissions, see [Amazon Route 53 API permissions: Actions, resources, and conditions reference](r53-api-permissions-ref.md), 

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "route53domains:Get*",
                "route53domains:List*"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```

## AWS managed policy: AmazonRoute53ResolverFullAccess<a name="security-iam-awsmanpol-AmazonRoute53ResolverFullAccess"></a>

You can attach the `AmazonRoute53ResolverFullAccess` policy to your IAM identities\.

This policy grants full access to Route 53 Resolver resources\.

**Permissions details**

This policy includes the following permissions\. 
+ `route53resolver:*` – Lets you create and manage Resolver resources on the Route 53 console\.
+ `ec2:DescribeSubnets` – Lets you list your Amazon VPC subnets\.
+ `ec2:CreateNetworkInterface`, `ec2:DeleteNetworkInterface`, and `ec2:ModifyNetworkInterfaceAttribute` – Let you create, modify, and delete network interfaces\.
+ `ec2:DescribeNetworkInterfaces` – Lets you display a list of network interfaces\.
+ `ec2:DescribeSecurityGroups` – Lets you display a list of all of your security groups\.
+  `ec2:DescribeVpcs` – Lets you display a list of VPCs\.
+ `ec2:DescribeAvailabilityZones` – Lets you list the zones that are available to you\.

 For more information about the permissions, see [Amazon Route 53 API permissions: Actions, resources, and conditions reference](r53-api-permissions-ref.md), 

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "route53resolver:*",
                "ec2:DescribeSubnets",
                "ec2:CreateNetworkInterface",
                "ec2:DeleteNetworkInterface",
                "ec2:ModifyNetworkInterfaceAttribute",
                "ec2:DescribeNetworkInterfaces",
                "ec2:CreateNetworkInterfacePermission",
                "ec2:DescribeSecurityGroups",
                "ec2:DescribeVpcs",
                "ec2:DescribeAvailabilityZones"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```

## AWS managed policy: AmazonRoute53ResolverReadOnlyAccess<a name="security-iam-awsmanpol-AmazonRoute53ResolverReadOnlyAccess"></a>

You can attach the `AmazonRoute53ResolverReadOnlyAccess` policy to your IAM identities\.

This policy grants read\-only access to Route 53 Resolver resources\.

**Permissions details**

This policy includes the following permissions\. 
+ `route53resolver:Get*` – Lets you retrieve list of Resolver resources\.
+ `route53resolver:List*` – Lets you display a list of Resolver resources\.
+ `ec2:DescribeNetworkInterfaces` – Lets you display a list of network interfaces\.
+ `ec2:DescribeSecurityGroups` – Lets you display a list of all of your security groups\.

 For more information about the permissions, see [Amazon Route 53 API permissions: Actions, resources, and conditions reference](r53-api-permissions-ref.md), 

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "route53resolver:Get*",
                "route53resolver:List*",
                "ec2:DescribeNetworkInterfaces",
                "ec2:DescribeSecurityGroups",
                "ec2:DescribeVpcs",
                "ec2:DescribeSubnets"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```

## AWS managed policy: Route53ResolverServiceRolePolicy<a name="security-iam-awsmanpol-Route53ResolverServiceRolePolicy"></a>

You can't attach `Route53ResolverServiceRolePolicy` to your IAM entities\. This policy is attached to a service\-linked role that allows Route 53 Resolver to access AWS services and resources that are used or managed by Resolver\. For more information, see [Using Service\-Linked Roles for Amazon Route 53 Resolver](using-service-linked-roles.md)\.

## Route 53 updates to AWS managed policies<a name="security-iam-awsmanpol-route53-updates"></a>

View details about updates to AWS managed policies for Route 53 since this service began tracking these changes\. For automatic alerts about changes to this page, subscribe to the RSS feed on the Route 53 [Document history page](History.md)\.




| Change | Description | Date | 
| --- | --- | --- | 
|  Route 53 started tracking changes  |  Route 53 started tracking changes for its AWS managed policies\.  | July 14, 2021 | 