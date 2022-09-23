# Identity and access management in Amazon Route 53<a name="auth-and-access-control"></a>

To perform any operation on Amazon Route 53 resources, such as registering a domain or updating a record, AWS Identity and Access Management \(IAM\) requires you to authenticate that you're an approved AWS user\. If you're using the Route 53 console, you authenticate your identity by providing your AWS user name and a password\. If you're accessing Route 53 programmatically, your application authenticates your identity for you by using access keys or by signing requests\.

After you authenticate your identity, IAM controls your access to AWS by verifying that you have permissions to perform operations and to access resources\. If you are an account administrator, you can use IAM to control the access of other users to the resources that are associated with your account\.

This chapter explains how to use [IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html) and Route 53 to help secure your resources\.

**Topics**
+ [Authentication](#authentication)
+ [Access control](#access-control)

## Authentication<a name="authentication"></a>

You can access AWS as any of the following types of identities:
+ **AWS account root user**

    When you create an AWS account, you begin with one sign\-in identity that has complete access to all AWS services and resources in the account\. This identity is called the AWS account *root user* and is accessed by signing in with the email address and password that you used to create the account\. We strongly recommend that you do not use the root user for your everyday tasks\. Safeguard your root user credentials and use them to perform the tasks that only the root user can perform\. For the complete list of tasks that require you to sign in as the root user, see [Tasks that require root user credentials](https://docs.aws.amazon.com/general/latest/gr/root-vs-iam.html#aws_tasks-that-require-root) in the *AWS General Reference*\. 
+ **IAM users and groups**  

  An *[IAM user](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users.html)* is an identity within your AWS account that has specific permissions for a single person or application\. Where possible, we recommend relying on temporary credentials instead of creating IAM users who have long\-term credentials such as passwords and access keys\. However, if you have specific use cases that require long\-term credentials with IAM users, we recommend that you rotate access keys\. For more information, see [Rotate access keys regularly for use cases that require long\-term credentials](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#rotate-credentials) in the *IAM User Guide*\.

  An [https://docs.aws.amazon.com/IAM/latest/UserGuide/id_groups.html](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_groups.html) is an identity that specifies a collection of IAM users\. You can't sign in as a group\. You can use groups to specify permissions for multiple users at a time\. Groups make permissions easier to manage for large sets of users\. For example, you could have a group named *IAMAdmins* and give that group permissions to administer IAM resources\.

  Users are different from roles\. A user is uniquely associated with one person or application, but a role is intended to be assumable by anyone who needs it\. Users have permanent long\-term credentials, but roles provide temporary credentials\. To learn more, see [When to create an IAM user \(instead of a role\)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id.html#id_which-to-choose) in the *IAM User Guide*\.
+ **IAM role**

    An [IAM role](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html) is an IAM identity that you can create in your account that has specific permissions\. An IAM role is similar to an IAM user in that it is an AWS identity with permissions policies that determine what the identity can and cannot do in AWS\. However, instead of being uniquely associated with one person, a role is intended to be assumable by anyone who needs it\. Also, a role does not have standard long\-term credentials such as a password or access keys associated with it\. Instead, when you assume a role, it provides you with temporary security credentials for your role session\. IAM roles with temporary credentials are useful in the following situations:
  + **Federated user access** –  To assign permissions to a federated identity, you create a role and define permissions for the role\. When a federated identity authenticates, the identity is associated with the role and is granted the permissions that are defined by the role\. For information about roles for federation, see [ Creating a role for a third\-party Identity Provider](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-idp.html) in the *IAM User Guide*\. 

    If you use IAM Identity Center, you configure a permission set\. To control what your identities can access after they authenticate, IAM Identity Center correlates the permission set to a role in IAM\. For information about permissions sets, see [ Permission sets](https://docs.aws.amazon.com/singlesignon/latest/userguide/permissionsetsconcept.html) in the *AWS IAM Identity Center \(successor to AWS Single Sign\-On\) User Guide*\.
  + **AWS service access** –  A service role is an [IAM role](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html) that a service assumes to perform actions on your behalf\. An IAM administrator can create, modify, and delete a service role from within IAM\. For more information, see [Creating a role to delegate permissions to an AWS service](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-service.html) in the *IAM User Guide*\. 
  + **Applications running on Amazon EC2** –  You can use an IAM role to manage temporary credentials for applications that are running on an EC2 instance and making AWS CLI or AWS API requests\. This is preferable to storing access keys within the EC2 instance\. To assign an AWS role to an EC2 instance and make it available to all of its applications, you create an instance profile that is attached to the instance\. An instance profile contains the role and enables programs that are running on the EC2 instance to get temporary credentials\. For more information, see [Using an IAM role to grant permissions to applications running on Amazon EC2 instances](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-ec2.html) in the *IAM User Guide*\. 

## Access control<a name="access-control"></a>

To create, update, delete, or list Amazon Route 53 resources, you need permissions to perform the operation, and you need permission to access the corresponding resources\. In addition, to perform the operation programmatically, you need valid access keys\. 

The following sections describe how to manage permissions for Route 53\. We recommend that you read the overview first\.
+ [Overview of managing access permissions to your Amazon Route 53 resources](access-control-overview.md)
+ [Using identity\-based policies \(IAM policies\) for Amazon Route 53](access-control-managing-permissions.md)
+ [Amazon Route 53 API permissions: Actions, resources, and conditions reference](r53-api-permissions-ref.md)