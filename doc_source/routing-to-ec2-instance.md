# Routing Traffic to an Amazon EC2 Instance<a name="routing-to-ec2-instance"></a>

Amazon EC2 provides scalable computing capacity in the AWS cloud\. You can launch an EC2 virtual computing environment \(an instance\) using a preconfigured template \(an Amazon Machine Image, or AMI\)\. When you launch an EC2 instance, EC2 automatically installs the operating system \(Linux or Microsoft Windows\) and additional software included in the AMI, such as web server or database software\.

If you're hosting a website or running a web application on an EC2 instance, you can route traffic for your domain, such as example\.com, to your server by using Amazon Route 53\. 

## Prerequisites<a name="routing-to-ec2-instance-prereqs"></a>

Before you get started, you need the following:

+ An Amazon EC2 instance\. For information about launching an EC2 instance, see the following documentation:

  + **Linux** – See [Getting Started with Amazon EC2 Linux Instances](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html) in the *Amazon EC2 User Guide for Linux Instances*

  + **Microsoft Windows** – See [Getting Started with Amazon EC2 Windows Instances](http://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/EC2_GetStarted.html) in the *Amazon EC2 User Guide for Windows Instances*
**Important**  
We recommend that you also create an [Elastic IP address](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html) and associate it with your EC2 instance\. An Elastic IP address ensures that the IP address of your Amazon EC2 instance will never change\.

+ A registered domain name\. You can use Amazon Route 53 as your domain registrar, or you can use a different registrar\.

+ Amazon Route 53 as the DNS service for the domain\. If you register your domain name by using Amazon Route 53, we automatically configure Amazon Route 53 as the DNS service for the domain\. 

  For information about migrating DNS service to Amazon Route 53, see [Using Amazon Route 53 as the DNS Service for Subdomains Without Migrating the Parent Domain](creating-migrating.md)\.

## Configuring Amazon Route 53 to Route Traffic to an Amazon EC2 Instance<a name="routing-to-ec2-instance-configuring"></a>

To configure Amazon Route 53 to route traffic to an EC2 instance, perform the following procedure\.

**To route traffic to an Amazon EC2 instance**

1. Get the IP address for the Amazon EC2 instance:

   1. Sign in to the AWS Management Console and open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

   1. In the regions list in the upper right corner of the console, choose the region that you launched the instance in\.

   1. In the navigation pane, choose **Instances**\.

   1. In the table, choose the instance that you want to route traffic to\.

   1. In the bottom pane, on the **Description** tab, get the value of **Elastic IPs**\. 

      If you didn't associate an Elastic IP with the instance, get the value of **Public IP**\.

1. Open the Amazon Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Hosted Zones**\.

1. Choose the name of the hosted zone for the domain name that you want to use to route traffic to your EC2 instance\.

1. Choose **Create Record Set**\.

1. Specify the following values:  
**Name**  
Type the domain name that you want to use to route traffic to your EC2 instance\. The default value is the name of the hosted zone\.  
For example, if the name of the hosted zone is example\.com and you want to use acme\.example\.com to route traffic to your EC2 instance, type **acme**\.  
**Type**  
Choose **A – IPv4 address**\.  
**Alias**  
Choose **No**\.  
**TTL \(Seconds\)**  
Accept the default value of **300**\.  
**Value**  
Type the IP address that you got in step 1\.  
**Routing Policy**  
Accept the default value, **Simple**\.

1. Choose **Create**\.

   Changes generally propagate to all Amazon Route 53 servers within 60 seconds\. When propagation is done, you'll be able to route traffic to your EC2 instance by using the name of the resource record set that you created in this procedure\. 