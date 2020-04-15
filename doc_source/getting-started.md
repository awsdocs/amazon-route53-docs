# Getting started with Amazon Route 53<a name="getting-started"></a>

This Getting Started tutorial shows you how to perform the following tasks:
+ Register a domain name, such as example\.com
+ Create an Amazon S3 bucket and configure it to host a website
+ Create a sample website and save the file in your S3 bucket
+ Configure Amazon Route 53 to route traffic to your new website

When you're finished, you'll be able to open a browser, enter the name of your domain, and view your website\.

**Note**  
You can also transfer an existing domain to Route 53, but the process is more complex and time consuming than registering a new domain\. For more information, see [Transferring registration for a domain to Amazon Route 53](domain-transfer-to-route-53.md)\. 

**Estimated cost**
+ There's an annual fee to register a domain, ranging from $9 to several hundred dollars, depending on the top\-level domain, such as \.com\. For more information, see [Route 53 Pricing for Domain Registration](https://d32ze2gidvkk54.cloudfront.net/Amazon_Route_53_Domain_Registration_Pricing_20140731.pdf)\. This fee is not refundable\.
+ When you register a domain, we automatically create a hosted zone that has the same name as the domain\. You use the hosted zone to specify where you want Route 53 to route traffic for your domain\. The fee for a hosted zone is $0\.50 per month\. 
+ During this tutorial, you create an Amazon S3 bucket and upload a sample web page\. If you're a new AWS customer, you can get started with Amazon S3 for free\. If you're an existing AWS customer, charges are based on how much data you store, on the number of requests for your data, and on the amount of data transferred\. For more information, see [Amazon S3 Pricing](https://aws.amazon.com/s3/pricing/)\.

**Topics**
+ [Prerequisites](#getting-started-prerequisites)
+ [Step 1: Register a domain](#getting-started-find-domain-name)
+ [Step 2: Create an S3 bucket and configure it to host a website](#getting-started-create-s3-website-bucket)
+ [Step 3 *\(optional\)*: Create another S3 Bucket, for www\.*your\-domain\-name*](#getting-started-create-s3-www-bucket)
+ [Step 4: Create a website and upload it to your S3 bucket](#getting-started-create-website)
+ [Step 5: Route DNS traffic for your domain to your website bucket](#getting-started-create-alias)
+ [Step 6: Test your website](#getting-started-test)
+ [Step 7 \(optional\): Use Amazon CloudFront to speed up distribution of your content](#getting-started-cloudfront)

## Prerequisites<a name="getting-started-prerequisites"></a>

Before you begin, be sure that you've completed the steps in [Setting up Amazon Route 53](setting-up-route-53.md)\.

## Step 1: Register a domain<a name="getting-started-find-domain-name"></a>

To use a domain name such as example\.com, you need to find a domain name that isn't already in use by someone else and register it\. When you register a domain name, you reserve it for your exclusive use everywhere on the internet, typically for one year\. By default, we automatically renew your domain name at the end of each year, but you can disable automatic renewal\.<a name="getting-started-domain-register-procedure"></a>

**To register a new domain using Amazon Route 53**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. If you're new to Route 53, under **Domain Registration**, choose **Get Started Now**\.

   If you're already using Route 53, in the navigation pane, choose **Registered Domains**\.

1. Choose **Register Domain**\.

1. Enter the domain name that you want to register, and choose **Check** to find out whether the domain name is available\.

   For information about how to specify characters other than a\-z, 0\-9, and \- \(hyphen\) and how to specify internationalized domain names, see [DNS domain name format](DomainNameFormat.md)\.

1. If the domain is available, choose **Add to cart**\. The domain name appears in your shopping cart\. 

   The **Related domain suggestions** list shows other domains that you might want to register instead of your first choice \(if it's not available\) or in addition to your first choice\. Choose **Add to cart** for each additional domain that you want to register, up to a maximum of five domains\.

   If the domain name isn't available and you don't want one of the suggested domain names, repeat step 4 until you find an available domain name that you like\.
**Note**  
If you also want your users to be able to use www\.*your\-domain\-name*, such as www\.example\.com, to access your sample website, you don't need to register a second domain\. Later in this Getting Started topic, we explain how to route traffic for www\.*your\-domain\-name* to your website\.

1. In the shopping cart, choose the number of years that you want to register the domain for\.

1. To register more domains, repeat steps 4 through 6\.

1. Choose **Continue**\.

1. On the **Contact Details for Your** *n* **Domains** page, enter contact information for the domain registrant, administrator, and technical contacts\. The values that you enter here are applied to all of the domains that you're registering\. 

   By default, we use the same information for all three contacts\. If you want to enter different information for one or more contacts, change the value of **My Registrant, Administrative, and Technical Contacts are all the same** to **No**\.

   If you're registering more than one domain, we use the same contact information for all of the domains\. 

   For more information, see [Values that you specify when you register or transfer a domain](domain-register-values-specify.md)\.

1. For some top\-level domains \(TLDs\), we're required to collect additional information\. For these TLDs, enter the applicable values after the **Postal/Zip Code** field\.

1. Choose whether you want to hide your contact information from WHOIS queries\. For more information, see the following topics:
   + [Enabling or disabling privacy protection for contact information for a domain](domain-privacy-protection.md)
   + [Domains that you can register with Amazon Route 53](registrar-tld-list.md)

1. Choose **Continue**\.

1. Review the information that you entered, read the terms of service, and select the check box to confirm that you've read the terms of service\. 

1. Choose **Complete Purchase**\.

   We send an email to the registrant for the domain to verify that the registrant contact can be reached at the email address that you specified\. \(This is an ICANN requirement\.\) The email comes from one of the following email addresses:
   + **noreply@registrar\.amazon\.com ** – for TLDs registered by Amazon Registrar\.
   + **noreply@domainnameverification\.net** – for TLDs registered by our registrar associate, Gandi\. To determine who the registrar is for your TLD, see [Domains that you can register with Amazon Route 53](registrar-tld-list.md)\.
**Important**  
The registrant contact must follow the instructions in the email to confirm that the email was received, or we must suspend the domain as required by ICANN\. When a domain is suspended, it's not accessible on the internet\.

   You'll receive another email when your domain registration has been approved\. To determine the current status of your request, see [Viewing the status of a domain registration](domain-view-status.md)\.

By default, you register a domain for one year\. If you won't want to keep the domain, you can disable automatic renewal, so the domain expires at the end of a year\. <a name="getting-started-disable-renewal-procedure"></a>

***\(Optional\)* To disable automatic renewal for a domain**

1. In the navigation pane, choose **Registered domains**\.

1. In the list of domains, choose the name of your domain\.

1. If the value of the **Auto renew** field is **Enabled \(disable\)**, choose **disable** to turn automatic renewal off\. The change takes effect immediately\.

   If the value of the field is **Disabled \(enable\)**, don't change the setting\.

## Step 2: Create an S3 bucket and configure it to host a website<a name="getting-started-create-s3-website-bucket"></a>

Amazon S3 lets you store and retrieve your data from anywhere on the internet\. To organize your data, you create buckets and upload your data to the buckets by using the AWS Management Console\. You can use S3 to host a static website in a bucket\. The following procedure explains how to create a bucket and configure it for website hosting\.<a name="getting-started-create-s3-website-bucket-procedure"></a>

**To create an S3 bucket and configure it to host a website**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. Choose **Create bucket**\.

1. Enter the following values:  
**Bucket name**  
Enter the name of your domain, such as **example\.com**\.  
**Region**  
Choose the region closest to most of your users\.  
Make note of the region that you choose; you'll need this information later in the process\.

1. Choose **Next**\.

1. On the **Configure options** page, choose **Next** to accept the default values\.

1. On the **Set permissions page**, uncheck the **Block all public access** check box, and choose **Next**\.
**Note**  
The console displays a message about public access to the bucket\. Later in this procedure, you add a bucket policy that limits access to the bucket\.

1. On the **Review** page, choose **Create bucket**\.

1. On the list of S3 buckets, choose the name of the bucket that you just created\.

1. Choose the **Properties** tab\.

1. Choose **Static website hosting**\.

1. Choose **Use this bucket to host a website**\.

1. For **Index document**, enter the name of the file that contains the main page for your website\. 
**Note**  
You'll create an HTML file and upload it to your bucket later in the process\.

1. Choose **Save**\.

1. Choose the **Permissions** tab\.

1. Choose **Bucket policy**\.

1. Copy the following bucket policy and paste it into a text editor\. This policy grants everyone on the internet \(`"Principal":"*"`\) permission to get the files \(`"Action":["s3:GetObject"]`\) in the S3 bucket that is associated with your domain name \(`"arn:aws:s3:::your-domain-name/*"`\):

   ```
   {
      "Version":"2012-10-17",
      "Statement":[{
         "Sid":"AddPerm",
         "Effect":"Allow",
         "Principal":"*",
         "Action":[
            "s3:GetObject"
         ],
         "Resource":[
            "arn:aws:s3:::your-domain-name/*"
         ]
       }]
   }
   ```

1. In the bucket policy, replace the value *your\-domain\-name* with the name of your domain, such as `example.com`\. This value must match the name of the bucket\.

1. Choose **Save**\.

## Step 3 *\(optional\)*: Create another S3 Bucket, for www\.*your\-domain\-name*<a name="getting-started-create-s3-www-bucket"></a>

In the preceding procedure, you created a bucket for your domain name, such as example\.com\. This allows your users to access your website by using your domain name, such as example\.com\.

If you also want your users to be able to use **www**\.*your\-domain\-name*, such as www\.example\.com, to access your sample website, you create a second S3 bucket\. You then configure the second bucket to route traffic to the first bucket\.

**Note**  
Websites typically redirect *your\-domain\-name* to **www**\.*your\-domain\-name*, for example, from example\.com to www\.example\.com\. Because of the way S3 works, you must set up the redirection in the opposite direction, from www\.example\.com to example\.com\. <a name="getting-started-create-s3-www-bucket-procedure"></a>

**To create an S3 bucket for www\.*your\-domain\-name***

1. Choose **Create bucket**\.

1. Enter the following values:  
**Bucket name**  
Enter **www\.*your\-domain\-name***\. For example, if you registered the domain name example\.com, enter **www\.example\.com**\.  
**Region**  
Choose the same region that you created the first bucket in\.

1. Choose **Next**\.

1. On the **Configure options** page, choose **Next** to accept the default values\.

1. On the **Set permissions page**, choose **Next** to accept the default values\.

1. On the **Review** page, choose **Create bucket**\.

1. On the list of S3 buckets, choose the name of the bucket that you just created\.

1. Choose the **Properties** tab\.

1. Choose **Static website hosting**\.

1. Choose **Redirect requests**\.

1. Enter the following values:  
**Target bucket or domain**  
Enter the name of the bucket that you want to redirect requests to\. This is the name of the bucket that you created in the procedure [To create an S3 bucket and configure it to host a website](#getting-started-create-s3-website-bucket-procedure)\.   
**Protocol**  
Enter **http**\. You're redirecting requests to an S3 bucket that is configured as a website endpoint, and Amazon S3 doesn't support HTTPS connections for website endpoints\.

1. Choose **Save**\.

## Step 4: Create a website and upload it to your S3 bucket<a name="getting-started-create-website"></a>

Now that you have an S3 bucket to save your website in, you can create the first page for your website and upload it to \(save it in\) your bucket\.<a name="getting-started-create-website-procedure"></a>

**To create a website and upload it to your S3 bucket**

1. Copy the following text and paste it into a text editor:

   ```
   <html>
   <head>
   <title>Amazon Route 53 Getting Started</title>	
   </head>
   
   <body>
   
   <h1>Routing Internet Traffic to an Amazon S3 Bucket for Your Website</h1>
   
   <p>For more information, see 
   <a href="https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/getting-started.html">Getting Started with Amazon Route 53</a> 
   in the <emphasis>Amazon Route 53 Developer Guide</emphasis>.</p>
   
   </body>
   
   </html>
   ```

1. Save the file with the file name **index\.html**\.

1. In the Amazon S3 console, choose the name of the bucket that you created in the procedure [To create an S3 bucket and configure it to host a website](#getting-started-create-s3-website-bucket-procedure)\.

1. Choose **Upload**\.

1. Choose **Add files**\.

1. Follow the on\-screen prompts to select **index\.html**, and then choose **Upload**\.

## Step 5: Route DNS traffic for your domain to your website bucket<a name="getting-started-create-alias"></a>

You now have a one\-page website in your S3 bucket\. To start routing internet traffic for your domain to your S3 bucket, perform the following procedure\. <a name="getting-started-create-alias-procedure"></a>

**To route traffic to your website**

1. Open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Hosted zones**\.
**Note**  
When you registered your domain, Amazon Route 53 automatically created a hosted zone with the same name\. A hosted zone contains information about how you want Route 53 to route traffic for the domain\.

1. In the list of hosted zones, choose the name of your domain\. 

1. Choose **Create Record Set**\.
**Note**  
Each record contains information about how you want to route traffic for one domain \(such as example\.com\) or subdomain \(such as www\.example\.com or test\.example\.com\)\. Records are stored in the hosted zone for your domain\.

1. Specify the following values:  
**Name**  
For the first record that you create, accept the default value, which is the name of your hosted zone and your domain\. This will route internet traffic to the bucket that has the same name as your domain\.  
If you created a second S3 bucket, for www\.*your\-domain\-name*, you repeat this step to create a second record\. For the second record, enter **www**\. This will route internet traffic to the www\.*your\-domain\-name* bucket\.  
**Type**  
Choose **A – IPv4 address**\.  
**Alias**  
Choose **Yes**\.  
**Alias Target**  
If you used the same account to create the Route 53 hosted zone and the Amazon S3 buckets, you can choose the name of the bucket from the **Alias Target** list:  
   + For the first record that you create, choose the bucket that has the same name as your hosted zone and your domain\.
   + For the second record, choose the bucket that has the name www\.*your\-domain\-name*\.
If another account created the S3 bucket, enter the name of the region that you created your S3 bucket in\. Use the applicable value from the **Website Endpoint** column in the table [Amazon S3 website endpoints](https://docs.aws.amazon.com/general/latest/gr/s3.html#s3_website_region_endpoints) in the *Amazon Web Services General Reference*\.  
If different accounts created the hosted zone and the S3 bucket, you specify the same value for **Alias Target** for both records\. Route 53 figures out which bucket to route traffic to based on the name of the record\.  
**Routing Policy**  
Accept the default value of **Simple**\.  
**Evaluate Target Health**  
Accept the default value of **No**\.

1. Choose **Create**\.

1. If you created a second S3 bucket, for www\.*your\-domain\-name*, repeat steps 4 through 6 to create a record for www\.*your\-domain\-name* in the same hosted zone\.

## Step 6: Test your website<a name="getting-started-test"></a>

To verify that the website is working correctly, open a web browser and browse to the following URLs:
+ http://*your\-domain\-name* – Displays the index document in the *your\-domain\-name* bucket
+ http://www\.*your\-domain\-name* – Redirects your request to the *your\-domain\-name* bucket

In some cases, you might need to clear the cache to see the expected behavior\.

For more advanced information about routing your internet traffic, see [Configuring Amazon Route 53 as your DNS service](dns-configuring.md)\. For information about routing your internet traffic to AWS resources, see [Routing internet traffic to your AWS resources](routing-to-aws-resources.md)\.

## Step 7 \(optional\): Use Amazon CloudFront to speed up distribution of your content<a name="getting-started-cloudfront"></a>

CloudFront is a web service that speeds up distribution of your static and dynamic web content, such as \.html, \.css, \.js, and image files, to your users\. CloudFront delivers your content through a worldwide network of data centers called edge locations\. When a user requests content that you're serving with CloudFront, the user is routed to the edge location that provides the lowest latency \(time delay\), so that content is delivered with the best possible performance\.
+ If the content is already in the edge location with the lowest latency, CloudFront delivers it immediately\.
+ If the content is not in that edge location, CloudFront retrieves it from an Amazon S3 bucket or an HTTP server \(for example, a web server\) that you have identified as the source for the definitive version of your content\.

For information about using CloudFront to distribute the content in your Amazon S3 bucket, see [Adding CloudFront when you're distributing content from Amazon S3](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/MigrateS3ToCloudFront.html#adding-cloudfront-to-s3) in the *Amazon CloudFront Developer Guide*\. 