# Opening Connections to an Amazon RDS Database Instance Using Your Domain Name<a name="routing-to-rds-db"></a>

If you use an Amazon RDS database instance for data storage for your web application, the domain name that is assigned to your DB instance is a long, partially random, alphanumeric string, for example:

`myexampledb.a1b2c3d4wxyz.us-west-2.rds.amazonaws.com`

Whenever you open a connection to your Amazon RDS DB instance, you must specify the domain name in your application code\. 

If you want to use a domain name that's easier to remember, you can use your own domain name instead\. To do this, you can use Amazon Route 53 to create a [CNAME record](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resource-record-sets-choosing-alias-non-alias.html) that associates your domain name with the domain name of your DB instance\.

For example, you could create a CNAME record to map `productdata.example.com` to the domain name `myexampledb.a1b2c3d4wxyz.us-west-2.rds.amazonaws.com`\. After you create the CNAME record, you can use `productdata.example.com` in your application code whenever you open a connection to your Amazon RDS DB instance\.

In addition to letting you use a name that's easier to remember, the CNAME record makes it easier for you to replace one DB instance with another\. Instead of updating all of your code with the domain name of a new DB instance, you can just change the domain name of the DB instance in the CNAME record\.

**Note**  
You must use a CNAME record to associate a domain name with an Amazon RDS DB instance\. Route 53 doesn't support using other types of records for this purpose\. For more information, see [Working with Records](rrsets-working-with.md)\.

## Prerequisites<a name="routing-to-rds-db-prerequisites"></a>

Before you get started, you need the following:

+ An Amazon RDS DB instance\.

+ A registered domain name\. \(You don't need to use Route 53 as the domain registrar\.\)

+ Route 53 as the DNS service for the domain\. To use the procedures in this topic, Route 53 must be your DNS service provider, but you can also create a CNAME record with another DNS service provider\.

  For more information, see [Using Amazon Route 53 as the DNS Service for Subdomains Without Migrating the Parent Domain](creating-migrating.md)\.

## Configuring Amazon Route 53 So You Can Use Your Domain Name to Open Connections<a name="routing-to-rds-db-procedures"></a>

To configure Amazon Route 53 so you can use your domain name to open connections to an Amazon RDS database instance, perform the following procedures\. First you get the domain name that is associated with your DB instance, and then you create a CNAME record that maps your domain name to the domain name of your DB instance\.

**To get the domain name for your Amazon RDS DB instance**

1. Sign in to the AWS Management Console and open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. In the regions list in the upper\-right corner of the console, change to the region where you created the DB instance that you want to open connections to\.

1. In the navigation pane, choose **Instances**\.

1. In the table, expand the DB instance that you want to open connections to\.

1. Get the value of **Endpoint**\.

**To create a CNAME record**

1. Open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Hosted Zones**\.

1. Choose the name of the hosted zone that has the domain name that you want to use to open connections to your DB instance\.

1. Choose **Create Record Set**\.

1. Specify the following values:  
**Name**  
Type the domain name that you want to use to open connections to your DB instance\. The default value is the name of the hosted zone\.  
For example, if the name of the hosted zone is example\.com and you want to use acme\.example\.com to open connections to your DB instance, type **acme**\.  
You can't create a CNAME record that has the same name as the hosted zone\.  
**Type**  
Choose **CNAME – Canonical name**\.  
**Alias**  
Choose **No**\.  
**TTL \(Seconds\)**  
Accept the default value of **300**\.  
**Value**  
Type the domain name of the DB instance that you want to open connections to\. This is the value that you got when you performed the procedure [To get the domain name for your Amazon RDS DB instance](#routing-to-rds-db-get-instance-domain-name-procedure)\.  
**Routing Policy**  
Accept the default value of **Simple**\.

1. Choose **Create**\.

   Changes generally propagate to all Route 53 servers within 60 seconds\. When propagation is complete, you'll be able to open connections to your DB instance by using the name of the CNAME record that you created in this procedure\.