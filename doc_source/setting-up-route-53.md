# Setting up Amazon Route 53<a name="setting-up-route-53"></a>

The overview and procedures in this section help you get started with AWS\.

**Topics**
+ [Sign up for AWS](#setting-up-sign-up-for-aws)
+ [Access your account](#setting-up-access-account)
+ [Create an IAM user](#setting-up-create-iam-user)
+ [Set up the AWS Command Line Interface or AWS Tools for Windows PowerShell](#setting-up-aws-cli)
+ [Download an AWS SDK](#setting-up-sdk)

## Sign up for AWS<a name="setting-up-sign-up-for-aws"></a>

When you sign up for AWS, your AWS account is automatically signed up for all services in AWS, including Amazon Route 53\. You are charged only for the services that you use\.

If you have an AWS account already, skip to [Access your account](#setting-up-access-account)\. If you don't have an AWS account, use the following procedure to create one\.<a name="setting-up-sign-up-for-aws-procedure"></a>

**To create an AWS account**

1. Open [https://portal\.aws\.amazon\.com/billing/signup](https://portal.aws.amazon.com/billing/signup)\.

1. Follow the online instructions\.

   Part of the sign\-up procedure involves receiving a phone call and entering a verification code on the phone keypad\.

   When you sign up for an AWS account, an *AWS account root user* is created\. The root user has access to all AWS services and resources in the account\. As a security best practice, [assign administrative access to an administrative user](https://docs.aws.amazon.com/singlesignon/latest/userguide/getting-started.html), and use only the root user to perform [tasks that require root user access](https://docs.aws.amazon.com/general/latest/gr/root-vs-iam.html#aws_tasks-that-require-root)\.

Note your AWS account number, because you'll need it later\.

## Access your account<a name="setting-up-access-account"></a>

You use AWS services by using any of the following options:
+ AWS Management Console
+ API for each service
+ AWS Command Line Interface \(AWS CLI\)
+ AWS Tools for Windows PowerShell
+ AWS SDKs

For each of those options, you need to access your AWS account by providing credentials that verify that you have permissions to use the services\.

### Access the console<a name="setting-up-access-account-console"></a>

To access the AWS Management Console for the first time, you provide an email address and a password\. This combination of your email address and password is called your *root identity* or *root account credentials*\. After you access your account for the first time, we strongly recommend that you don't use your root account credentials again for everyday use\. Instead, you should create new credentials by using [AWS Identity and Access Management](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html)\. To do that, you create a user account for yourself known as an *IAM user*, and then add the IAM user to an IAM group with administrative permissions or grant the IAM user administrative permissions\. You then can access AWS using a special URL and the credentials for the IAM user\. You also can add other IAM users later, and restrict their access to specified resources in the account\.

### Access the API, AWS CLI, AWS Tools for Windows PowerShell, or the AWS SDKs<a name="setting-up-access-account-api-cli"></a>

To use the API, the AWS CLI, AWS Tools for Windows PowerShell, or the AWS SDKs, you must create *access keys*\. These keys consist of an access key ID and secret access key, which are used to sign programmatic requests that you make to AWS\.

To create the keys, you sign in to the AWS Management Console\. We strongly recommend that you sign in with your IAM user credentials instead of your root credentials\. For more information, see [Managing access keys for IAM users](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html) in the *IAM User Guide*\.

## Create an IAM user<a name="setting-up-create-iam-user"></a>

Perform the following procedures to create a group for administrators, create an IAM user, and then add the IAM user to the administrators group\. If you signed up for AWS but have not created an IAM user for yourself, you can create one using the IAM console\. If you aren't familiar with using the console, see [Working with the AWS Management Console](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/getting-started.html) for an overview\. 

To create an administrator user, choose one of the following options\.


****  

| Choose one way to manage your administrator | To | By | You can also | 
| --- | --- | --- | --- | 
| In IAM Identity Center \(Recommended\) | Use short\-term credentials to access AWS\.This aligns with the security best practices\. For information about best practices, see [Security best practices in IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#bp-users-federation-idp) in the *IAM User Guide*\. | Following the instructions in [Getting started](https://docs.aws.amazon.com/singlesignon/latest/userguide/getting-started.html) in the AWS IAM Identity Center \(successor to AWS Single Sign\-On\) User Guide\. | Configure programmatic access by [Configuring the AWS CLI to use AWS IAM Identity Center \(successor to AWS Single Sign\-On\)](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-sso.html) in the AWS Command Line Interface User Guide\. | 
| In IAM \(Not recommended\) | Use long\-term credentials to access AWS\. | Following the instructions in [Creating your first IAM admin user and user group](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_create-admin-group.html) in the IAM User Guide\. | Configure programmatic access by [Managing access keys for IAM users](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html) in the IAM User Guide\. | <a name="setting-up-sign-in-iam-user-procedure"></a>

**To sign in as your new IAM user**

1. Sign out of the AWS console\.

1. Sign in by using the following URL, where *your\_aws\_account\_id* is your AWS account number without the hyphens\. For example, if your AWS account number is 1234\-5678\-9012, your AWS account ID is 123456789012:

   ```
   https://your_aws_account_id.signin.aws.amazon.com/console/
   ```

1. Enter the IAM user name \(not your email address\) and password that you just created\. When you're signed in, the navigation bar displays "*your\_user\_name* @ *your\_aws\_account\_id*"\.

If you don't want the URL for your sign\-in page to contain your AWS account ID, you can create an account alias\.<a name="setting-up-create-account-alias-procedure"></a>

**To create an account alias and conceal your account ID**

1. On the IAM console, choose **Dashboard** in the navigation pane\. 

1. On the dashboard, choose **Customize** and enter an alias such as your company name\.

1. Sign out of the AWS console\.

1. Sign in by using the following URL:

   ```
   https://your_account_alias.signin.aws.amazon.com/console/
   ```

To verify the sign\-in link for IAM users for your account, open the IAM console and check under **IAM users sign\-in link** on the dashboard\.

For more information about using IAM, see [Identity and access management in Amazon Route 53](auth-and-access-control.md)\.

## Set up the AWS Command Line Interface or AWS Tools for Windows PowerShell<a name="setting-up-aws-cli"></a>

The AWS Command Line Interface \(AWS CLI\) is a unified tool for managing AWS services\. For information about how to install and configure the AWS CLI, see [Getting set up with the AWS Command Line Interface](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-set-up.html) in the *AWS Command Line Interface User Guide*\.

If you have experience with Windows PowerShell, you might prefer to use AWS Tools for Windows PowerShell\. For more information, see [Setting up the AWS Tools for Windows PowerShell](https://docs.aws.amazon.com/powershell/latest/userguide/pstools-getting-set-up.html) in the *AWS Tools for Windows PowerShell User Guide*\.

## Download an AWS SDK<a name="setting-up-sdk"></a>

If you're using a programming language that AWS provides an SDK for, we recommend that you use an SDK instead of the Amazon Route 53 API\. The SDKs make authentication simpler, integrate easily with your development environment, and provide easy access to Route 53 commands\. For more information, see [Tools for Amazon Web Services](https://aws.amazon.com/tools/)\.