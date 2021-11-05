# Overview of managing access permissions to your Amazon Route 53 resources<a name="access-control-overview"></a>

Every AWS resource is owned by an AWS account, and permissions to create or access a resource are governed by permissions policies\.

**Note**  
An *account administrator* \(or administrator user\) is a user that has administrator privileges\. For more information about administrators, see [IAM best practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html) in the *IAM User Guide*\.

When you grant permissions, you decide who gets the permissions, the resources they get permissions for, and the actions that they get permissions to perform\.

**Topics**
+ [ARNs for Amazon Route 53 resources](#access-control-resources)
+ [Understanding resource ownership](#access-control-owner)
+ [Managing access to resources](#access-control-manage-access-intro)
+ [Specifying policy elements: Resources, actions, effects, and principals](#access-control-specify-r53-actions)
+ [Specifying conditions in a policy](#specifying-conditions)

## ARNs for Amazon Route 53 resources<a name="access-control-resources"></a>

Amazon Route 53 supports a variety of resource types for DNS, health checking, and domain registration\. In a policy, you can grant or deny access to the following resources by using `*` for the ARN:
+ Health checks
+ Hosted zones
+ Reusable delegation sets
+ Status of a resource record set change batch \(API only\)
+ Traffic policies \(traffic flow\)
+ Traffic policy instances \(traffic flow\)

Not all Route 53 resources support permissions\. You can't grant or deny access to the following resources:
+ Domains
+ Individual records
+ Tags for domains
+ Tags for health checks
+ Tags for hosted zones

Route 53 provides API actions to work with each of these types of resources\. For more information, see the [Amazon Route 53 API Reference](https://docs.aws.amazon.com/Route53/latest/APIReference/)\. For a list of actions and the ARN that you specify to grant or deny permission to use each action, see [Amazon Route 53 API permissions: Actions, resources, and conditions reference](r53-api-permissions-ref.md)\.

## Understanding resource ownership<a name="access-control-owner"></a>

An AWS account owns the resources that are created in the account, regardless of who created the resources\. Specifically, the resource owner is the AWS account of the principal entity \(that is, the root account, an IAM user, or an IAM role\) that authenticates the resource creation request\. 

The following examples illustrate how this works:
+ If you use the root account credentials of your AWS account to create a hosted zone, your AWS account is the owner of the resource\.
+ If you create an IAM user in your AWS account and grant permissions to create a hosted zone to that user, the user can create a hosted zone\. However, your AWS account, to which the user belongs, owns the hosted zone resource\.
+ If you create an IAM role in your AWS account with permissions to create a hosted zone, anyone who can assume the role can create a hosted zone\. Your AWS account, to which the role belongs, owns the hosted zone resource\.

## Managing access to resources<a name="access-control-manage-access-intro"></a>

A *permissions policy* specifies who has access to what\. This section explains the options for creating permissions policies for Amazon Route 53\. For general information about IAM policy syntax and descriptions, see the [AWS IAM Policy Reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies.html) in the *IAM User Guide*\.

Policies attached to an IAM identity are referred to as *identity\-based* policies \(IAM policies\), and policies attached to a resource are referred to as *resource\-based* policies\. Route 53 supports only identity\-based policies \(IAM policies\)\.

**Topics**
+ [Identity\-based policies \(IAM policies\)](#access-control-manage-access-intro-iam-policies)
+ [Resource\-based policies](#access-control-manage-access-intro-resource-policies)

### Identity\-based policies \(IAM policies\)<a name="access-control-manage-access-intro-iam-policies"></a>

You can attach policies to IAM identities\. For example, you can do the following:
+ **Attach a permissions policy to a user or a group in your account** – An account administrator can use a permissions policy that is associated with a particular user to grant permissions for that user to create Amazon Route 53 resources\.
+ **Attach a permissions policy to a role \(grant cross\-account permissions\)** – You can grant permission to perform Route 53 actions to a user that was created by another AWS account\. To do so, you attach a permissions policy to an IAM role, and then you allow the user in the other account to assume the role\. The following example explains how this works for two AWS accounts, account A and account B:

  1. Account A administrator creates an IAM role and attaches to the role a permissions policy that grants permissions to create or access resources that are owned by account A\.

  1. Account A administrator attaches a trust policy to the role\. The trust policy identifies account B as the principal that can assume the role\.

  1. Account B administrator can then delegate permissions to assume the role to users or groups in Account B\. This allows users in account B to create or access resources in account A\.

  For more information about how to delegate permissions to users in another AWS account, see [Access management](https://docs.aws.amazon.com/IAM/latest/UserGuide/access.html) in the *IAM User Guide*\.

The following example policy allows a user to perform the `CreateHostedZone` action to create a public hosted zone for any AWS account:

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "route53:CreateHostedZone"
            ],
            "Resource":"*"
        }
    ]
}
```

If you want the policy to also apply to private hosted zones, you need to grant permissions to use the Route 53 `AssociateVPCWithHostedZone` action and two Amazon EC2 actions, `DescribeVpcs` and `DescribeRegion`, as shown in the following example:

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "route53:CreateHostedZone",
                "route53:AssociateVPCWithHostedZone"
            ],
            "Resource":"*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "ec2:DescribeVpcs",
                "ec2:DescribeRegion"
            ],
            "Resource":"*"
        },
    ]
}
```

For more information about attaching policies to identities for Route 53, see [Using identity\-based policies \(IAM policies\) for Amazon Route 53](access-control-managing-permissions.md)\. For more information about users, groups, roles, and permissions, see [Identities \(users, groups, and roles\)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id.html) in the *IAM User Guide*\.

### Resource\-based policies<a name="access-control-manage-access-intro-resource-policies"></a>

Other services, such as Amazon S3, also support attaching permissions policies to resources\. For example, you can attach a policy to an S3 bucket to manage access permissions to that bucket\. Amazon Route 53 doesn't support attaching policies to resources\. 

## Specifying policy elements: Resources, actions, effects, and principals<a name="access-control-specify-r53-actions"></a>

Amazon Route 53 includes API actions \(see the [Amazon Route 53 API Reference](https://docs.aws.amazon.com/Route53/latest/APIReference/)\) that you can use on each Route 53 resource \(see [ARNs for Amazon Route 53 resources](#access-control-resources)\)\. You can grant a user or a federated user permissions to perform any or all of these actions\. Note that some API actions, such as registering a domain, require permissions to perform more than one action\.

The following are the basic policy elements:
+ **Resource** – You use an Amazon Resource Name \(ARN\) to identify the resource that the policy applies to\. For more information, see [ARNs for Amazon Route 53 resources](#access-control-resources)\.
+ **Action** – You use action keywords to identify resource operations that you want to allow or deny\. For example, depending on the specified `Effect`, the `route53:CreateHostedZone` permission allows or denies a user the ability to perform the Route 53 `CreateHostedZone` action\.
+ **Effect** – You specify the effect, either allow or deny, when a user tries to perform the action on the specified resource\. If you don't explicitly grant access to an action, access is implicitly denied\. You can also explicitly deny access to a resource, which you might do to make sure that a user cannot access it, even if a different policy grants access\.
+ **Principal** – In identity\-based policies \(IAM policies\), the user that the policy is attached to is the implicit principal\. For resource\-based policies, you specify the user, account, service, or other entity that you want to receive permissions \(applies to resource\-based policies only\)\. Route 53 doesn't support resource\-based policies\.

For more information about IAM policy syntax and descriptions, see the [AWS IAM Policy Reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies.html) in the *IAM User Guide*\.

For a table showing all of the Route 53 API operations and the resources that they apply to, see [Amazon Route 53 API permissions: Actions, resources, and conditions reference](r53-api-permissions-ref.md)\.

## Specifying conditions in a policy<a name="specifying-conditions"></a>

When you grant permissions, you can use the IAM policy language to specify when a policy should take effect\. For example, you might want a policy to be applied only after a specific date\. For more information about specifying conditions in a policy language, see [IAM JSON policy elements: Condition](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_condition.html) in the *IAM User Guide*\. 

To express conditions, you use predefined condition keys\. There are no condition keys specific to Route 53\. However, there are AWS wide condition keys that you can use as needed\. For a complete list of AWS wide keys, see [Available keys for conditions](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html#AvailableKeys) in the *IAM User Guide*\. 