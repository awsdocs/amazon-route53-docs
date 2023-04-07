# Setting up Amazon Route 53<a name="setting-up-route-53"></a>

The overview and procedures in this section help you get started with AWS\.

**Topics**
+ [Sign up for an AWS account](#sign-up-for-aws)
+ [Create an administrative user](#create-an-admin)
+ [Download tools](#setting-up-sdk)

## Sign up for an AWS account<a name="sign-up-for-aws"></a>

If you do not have an AWS account, complete the following steps to create one\.

**To sign up for an AWS account**

1. Open [https://portal\.aws\.amazon\.com/billing/signup](https://portal.aws.amazon.com/billing/signup)\.

1. Follow the online instructions\.

   Part of the sign\-up procedure involves receiving a phone call and entering a verification code on the phone keypad\.

   When you sign up for an AWS account, an *AWS account root user* is created\. The root user has access to all AWS services and resources in the account\. As a security best practice, [assign administrative access to an administrative user](https://docs.aws.amazon.com/singlesignon/latest/userguide/getting-started.html), and use only the root user to perform [tasks that require root user access](https://docs.aws.amazon.com/accounts/latest/reference/root-user-tasks.html)\.

AWS sends you a confirmation email after the sign\-up process is complete\. At any time, you can view your current account activity and manage your account by going to [https://aws\.amazon\.com/](https://aws.amazon.com/) and choosing **My Account**\.

## Create an administrative user<a name="create-an-admin"></a>

After you sign up for an AWS account, create an administrative user so that you don't use the root user for everyday tasks\.

**Secure your AWS account root user**

1.  Sign in to the [AWS Management Console](https://console.aws.amazon.com/) as the account owner by choosing **Root user** and entering your AWS account email address\. On the next page, enter your password\.

   For help signing in by using root user, see [Signing in as the root user](https://docs.aws.amazon.com/signin/latest/userguide/console-sign-in-tutorials.html#introduction-to-root-user-sign-in-tutorial) in the *AWS Sign\-In User Guide*\.

1. Turn on multi\-factor authentication \(MFA\) for your root user\.

   For instructions, see [Enable a virtual MFA device for your AWS account root user \(console\)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa_enable_virtual.html#enable-virt-mfa-for-root) in the *IAM User Guide*\.

**Create an administrative user**
+ For your daily administrative tasks, grant administrative access to an administrative user in AWS IAM Identity Center \(successor to AWS Single Sign\-On\)\.

  For instructions, see [Getting started](https://docs.aws.amazon.com/singlesignon/latest/userguide/getting-started.html) in the *AWS IAM Identity Center \(successor to AWS Single Sign\-On\) User Guide*\.

**Sign in as the administrative user**
+ To sign in with your IAM Identity Center user, use the sign\-in URL that was sent to your email address when you created the IAM Identity Center user\.

  For help signing in using an IAM Identity Center user, see [Signing in to the AWS access portal](https://docs.aws.amazon.com/signin/latest/userguide/iam-id-center-sign-in-tutorial.html) in the *AWS Sign\-In User Guide*\.

## Download tools<a name="setting-up-sdk"></a>

The AWS Management Console includes a console for Amazon Route 53, but if you want to access the services programmatically, see the following:
+ The API guide document the operations that the services support and provide links to the related SDK and CLI documentation:
  + [Amazon Route 53 API Reference](https://docs.aws.amazon.com/Route53/latest/APIReference/Welcome.html)
+ To call an API without having to handle low\-level details like assembling raw HTTP requests, you can use an AWS SDK\. The AWS SDKs provide functions and data types that encapsulate the functionality of AWS services\. To download an AWS SDK and access installation instructions, see the applicable page: 
  + [Java](https://aws.amazon.com/sdk-for-java/)
  + [JavaScript](http://aws.amazon.com/sdkforbrowser/)
  + [\.NET](https://aws.amazon.com/sdk-for-net/)
  + [Node\.js](https://aws.amazon.com/sdk-for-node-js/)
  + [PHP](https://aws.amazon.com/sdk-for-php/)
  + [Python](https://github.com/boto/boto)
  + [Ruby](https://aws.amazon.com/sdk-for-ruby/)

  For a complete list of AWS SDKs, see [Tools for Amazon Web Services](http://aws.amazon.com/tools/)\.
+ You can use the AWS Command Line Interface \(AWS CLI\) to control multiple AWS services from the command line\. You can also automate your commands using scripts\. For more information, see [AWS Command Line Interface](https://aws.amazon.com/cli/)\.
+ AWS Tools for Windows PowerShell supports these AWS services\. For more information, see [AWS Tools for PowerShell Cmdlet Reference](http://aws.amazon.com/documentation/powershell/)\.