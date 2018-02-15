# Getting Started with Amazon Route 53<a name="getting-started"></a>

This Getting Started tutorial shows you how to perform the following tasks:

+ Register a domain name, such as example\.com

+ Create an Amazon S3 bucket and configure it to host a website

+ Create a sample website and save the file in your S3 bucket

+ Configure Amazon Route 53 to route traffic to your new website

When you're finished, you'll be able to open a browser, enter the name of your domain, and view your website\.

**Note**  
You can also transfer an existing domain to Route 53, but the process is more complex and time consuming than registering a new domain\. For more information, see [Transferring Registration for a Domain to Amazon Route 53](domain-transfer-to-route-53.md)\. 

**Estimated cost**

+ There's an annual fee to register a domain, ranging from $9 to several hundred dollars, depending on the top\-level domain, such as \.com\. For more information, see [Route 53 Pricing for Domain Registration](https://d32ze2gidvkk54.cloudfront.net/Amazon_Route_53_Domain_Registration_Pricing_20140731.pdf)\. This fee is not refundable\.

+ When you register a domain, we automatically create a hosted zone that has the same name as the domain\. You use the hosted zone to specify where you want Route 53 to route traffic for your domain\. The fee for a hosted zone is $0\.50 per month\. You can delete the hosted zone if you want to avoid this charge\.

+ If you're a new AWS customer, you can get started with Amazon S3 for free\. If you're an existing AWS customer, charges are based on how much data you store, on the number of requests for your data, and on the amount of data transferred\. For more information, see [Amazon S3 Pricing](https://aws.amazon.com/s3/pricing/)\.


+ [Prerequisites](#getting-started-prerequisites)
+ [Step 1: Register a domain](#getting-started-find-domain-name)
+ [Step 2: Create an S3 Bucket and Configure It to Host a Website](#getting-started-create-s3-website-bucket)
+ [Step 3 *\(Optional\)*: Create Another S3 Bucket, for www\.*your\-domain\-name*](#getting-started-create-s3-www-bucket)
+ [Step 4: Create a Website and Upload It to Your S3 Bucket](#getting-started-create-website)
+ [Step 5: Route DNS Traffic for Your Domain to Your Website Bucket](#getting-started-create-alias)
+ [Step 6: Test Your Website](#getting-started-test)

## Prerequisites<a name="getting-started-prerequisites"></a>

Before you begin, be sure that you've completed the steps in [Setting Up Amazon Route 53](setting-up-route-53.md)\.

## Step 1: Register a domain<a name="getting-started-find-domain-name"></a>

To use a domain name such as example\.com, you need to find a domain name that isn't already in use by someone else and register it\. When you register a domain name, you reserve it for your exclusive use everywhere on the internet, typically for one year\. By default, we automatically renew your domain name at the end of each year, but you can disable automatic renewal\.

**To register a new domain using Amazon Route 53**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. If you're new to Route 53, under **Domain Registration**, choose **Get Started Now**\.

   If you're already using Route 53, in the navigation pane, choose **Registered Domains**\.

1. Choose **Register Domain**\.

1. Enter the domain name that you want to register, and choose **Check** to find out whether the domain name is available\.

   For information about how to specify characters other than a\-z, 0\-9, and \- \(hyphen\) and how to specify internationalized domain names, see [DNS Domain Name Format](DomainNameFormat.md)\.

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

   For more information, see [Values that You Specify When You Register a Domain](domain-register-values-specify.md)\.

1. For some top\-level domains \(TLDs\), we're required to collect additional information\. For these TLDs, enter the applicable values after the **Postal/Zip Code** field\.

1. Choose whether you want to hide your contact information from WHOIS queries\. For more information, see the following topics:

   + [Enabling or Disabling Privacy Protection for Contact Information for a Domain](domain-privacy-protection.md)

   + [Domains That You Can Register with Amazon Route 53](registrar-tld-list.md)

1. Choose **Continue**\.

1. Review the information that you entered, read the terms of service, and select the check box to confirm that you've read the terms of service\. 

1. Choose **Complete Purchase**\.

   We send an email to the registrant for the domain to verify that the registrant contact can be reached at the email address that you specified\. \(This is an ICANN requirement\.\) The email comes from one of the following email addresses:

   + **noreply@registrar\.amazon\.com ** – for TLDs registered by Amazon Registrar\.

   + **noreply@domainnameverification\.net** – for TLDs registered by our registrar associate, Gandi\. To determine who the registrar is for your TLD, see [Domains That You Can Register with Amazon Route 53](registrar-tld-list.md)\.
**Important**  
The registrant contact must follow the instructions in the email to confirm that the email was received, or we must suspend the domain as required by ICANN\. When a domain is suspended, it's not accessible on the internet\.

   You'll receive another email when your domain registration has been approved\. To determine the current status of your request, see [Viewing the Status of a Domain Registration](domain-view-status.md)\.

By default, you register a domain for one year\. If you won't want to keep the domain, you can disable automatic renewal, so the domain expires at the end of a year\. 

***\(Optional\)* To disable automatic renewal for a domain**

1. In the navigation pane, choose **Registered domains**\.

1. In the list of domains, choose the name of your domain\.

1. If the value of the **Auto renew** field is **Enabled \(disable\)**, choose **disable** to turn automatic renewal off\. The change takes effect immediately\.

   If the value of the field is **Disabled \(enable\)**, don't change the setting\.

## Step 2: Create an S3 Bucket and Configure It to Host a Website<a name="getting-started-create-s3-website-bucket"></a>

Amazon S3 lets you store and retrieve your data from anywhere on the internet\. To organize your data, you create buckets and upload your data to the buckets by using the AWS Management Console\. You can use S3 to host a static website in a bucket\. The following procedure explains how to create a bucket and configure it for website hosting\.

**To create an S3 bucket and configure it to host a website**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. If a **Switch to the old console** button appears in the upper\-right corner of the S3 console, choose it\.

1. Choose **Create bucket**\.

1. For **Bucket Name**, type the name of your domain, such as **example\.com**\.

1. For **Region**, choose the region closest to most of your users\.

   Make note of the region that you choose; you'll need this information later in the process\.

1. Choose **Create**\.

1. In the right pane, expand **Permissions**\.

1. Choose **Add bucket policy**\.

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

1. In the bucket policy, replace the value *your\-domain\-name* with the name of your domain, such as `example.com`\.

1. Choose **Save**\.

1. In the right pane, expand **Static website hosting**\.

1. Choose **Enable website hosting**\.

1. For **Index document**, type **index\.html**\. This is the name that you'll give the HTML file that you'll create later in this process\.

1. Choose **Save**\.

## Step 3 *\(Optional\)*: Create Another S3 Bucket, for www\.*your\-domain\-name*<a name="getting-started-create-s3-www-bucket"></a>

In the preceding procedure, you created a bucket for your domain name, such as example\.com\. This allows your users to access your website by using your domain name, such as example\.com\.

If you also want your users to be able to use **www**\.*your\-domain\-name*, such as www\.example\.com, to access your sample website, you create a second S3 bucket\. You then configure the second bucket to route traffic to the first bucket\.

**To create an S3 bucket for www\.*your\-domain\-name***

1. Choose **Create bucket**\.

1. For **Bucket Name**, type **www\.*your\-domain\-name***\. For example, if you registered the domain name example\.com, type **www\.example\.com**\.

1. For **Region**, choose the same region that you created the first bucket in\. 

1. Choose **Create**\.

1. In the right pane, expand **Static website hosting**\.

1. Choose **Redirect all requests to another host name**\.

1. For **Redirect all requests to**, type your domain name\.

1. Choose **Save**\.

## Step 4: Create a Website and Upload It to Your S3 Bucket<a name="getting-started-create-website"></a>

Now that you have an S3 bucket to save your website in, you can create the first page for your website and upload it to \(save it in\) your bucket\.

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
   <a href url="http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/getting-started.html">Getting Started with Amazon Route 53</a> 
   in the <emphasis>Amazon Route 53 Developer Guide</emphasis>.</p>
   
   </body>
   
   </html>
   ```

1. Save the file with the file name **index\.html**\.

1. In the Amazon S3 console, choose the name of the bucket that you created in the procedure [To create an S3 bucket and configure it to host a website](#getting-started-create-s3-website-bucket-procedure)\.

1. Choose **Upload**\.

1. Choose **Add files**\.

1. Follow the on\-screen prompts to select **index\.html**, and then choose **Start Upload**\.

## Step 5: Route DNS Traffic for Your Domain to Your Website Bucket<a name="getting-started-create-alias"></a>

You now have a one\-page website in your S3 bucket\. To start routing internet traffic for your domain to your S3 bucket, perform the following procedure\. 

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
For the first record that you'll create, accept the default value, which is the name of your hosted zone and your domain\. This will route internet traffic to the bucket that has the same name as your domain\.  
If you created a second S3 bucket, for www\.*your\-domain\-name*, you'll repeat this step to create a second record\. For the second record, type **www**\. This will route internet traffic to the www\.*your\-domain\-name* bucket\.  
**Type**  
Choose **A – IPv4 address**\.  
**Alias**  
Choose **Yes**\.  
**Alias Target**  
Type the name of the region that you created your S3 bucket in\. Use the applicable value from the **Website Endpoint** column in the [Amazon Simple Storage Service Website Endpoints](http://docs.aws.amazon.com/general/latest/gr/rande.html#s3_website_region_endpoints) table in the [AWS Regions and Endpoints](http://docs.aws.amazon.com/general/latest/gr/rande.html) chapter of the *Amazon Web Services General Reference*\.  
You specify the same value for **Alias Target** for both records\. Route 53 figures out which bucket to route traffic to based on the name of the record\.  
**Routing Policy**  
Accept the default value of **Simple**\.  
**Evaluate Target Health**  
Accept the default value of **No**\.

1. Choose **Create**\.

1. If you created a second S3 bucket, for www\.*your\-domain\-name*, repeat steps 4 through 6 to create a record for www\.*your\-domain\-name*\.

## Step 6: Test Your Website<a name="getting-started-test"></a>

To verify that the website is working correctly, open a web browser and browse to the following URLs:

+ http://*your\-domain\-name* – Displays the index document in the *your\-domain\-name* bucket

+ http://www\.*your\-domain\-name* – Redirects your request to the *your\-domain\-name* bucket

In some cases, you might need to clear the cache to see the expected behavior\.

For more advanced information about routing your internet traffic, see [Configuring Amazon Route 53 as Your DNS Service](dns-configuring.md)\. For information about routing your internet traffic to AWS resources, see [Routing Internet Traffic to Your AWS Resources](routing-to-aws-resources.md)\.