# Use an Amazon CloudFront distribution to serve a static website<a name="getting-started-cloudfront-overview"></a>

This getting started tutorial shows you how to perform the following tasks:
+ Register a domain name, such as example\.com\.
+ Create a certificate for your domain\.
+ Create two Amazon S3 buckets and configure one to host a website and the other one to redirect to the subdomain\.
+ Create a sample website and save the file in your S3 bucket\.
+ Create CloudFront distributions for both S3 buckets\.
+ Configure Amazon Route 53 to route traffic to the CloudFront distributions\.

When you're finished, you'll be able to open a browser, enter the name of your domain, and view your website securely\.

**Topics**
+ [Prerequisites](#getting-started-prerequisites-cloudfront)
+ [Step 1: Register a domain](#getting-started-cloudfront-domain-name)
+ [Step 2: Request a public certificate](#getting-started-cloudfront-request-certificate)
+ [Step 3: Create an S3 bucket to host your subdomain](#getting-started-cloudformation-create-s3-www-bucket)
+ [Step 4 : Create another S3 bucket, for your root domain](#getting-started-cloudfront-s3-bucket)
+ [Step 5: Upload website files to your subdomain bucket](#getting-started-cloudformation-www-for-website)
+ [Step 6: Set up your root domain bucket for website redirect](#getting-started-cloudfront-bucket-redirect)
+ [Step 7: Create an Amazon CloudFront distribution for your subdomain](#getting-started-cloudfront-distribution)
+ [Step 8: Create an Amazon CloudFront distribution for your root domain](#getting-started-cloudfront-distribution-root)
+ [Step 9: Route DNS traffic for your domain to your CloudFront distribution](#getting-started-cloudfront-create-alias)
+ [Step 10 : Test your website](#getting-started-cloudfront-test)

## Prerequisites<a name="getting-started-prerequisites-cloudfront"></a>

Before you begin, be sure that you've completed the steps in [Setting up Amazon Route 53](setting-up-route-53.md)\.

## Step 1: Register a domain<a name="getting-started-cloudfront-domain-name"></a>

To use a domain name \(such as example\.com\), you must find a domain name that isn't already in use and register it\. When you register a domain name, you reserve it for your exclusive use everywhere on the internet, typically for one year\. By default, we automatically renew your domain name at the end of each year, but you can turn off automatic renewal\.<a name="getting-started-domain-register-procedure"></a>

**To register a new domain using Amazon Route 53**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. If you're new to Route 53, choose **Get started**\.

   If you're already using Route 53, in the navigation pane, choose **Registered domains**\.

1. Choose **Register Domain**\.

1. Enter the domain name that you want to register, and choose **Check** to find out whether the domain name is available\.

   For information about how to specify characters other than a\-z, 0\-9, and \- \(hyphen\), and how to specify internationalized domain names, see [DNS domain name format](DomainNameFormat.md)\.

1. If the domain is available, choose **Add to cart**\. The domain name appears in your shopping cart\. 

   The **Related domain suggestions** list shows other domains that you might want to register instead of your first choice \(if it's not available\), or in addition to your first choice\. Choose **Add to cart** for each additional domain that you want to register, up to a maximum of five domains\.

   If the domain name isn't available and you don't want one of the suggested domain names, repeat step 4 until you find an available domain name that you like\.
**Note**  
If you also want your users to be able to use www\.*your\-domain\-name*, such as www\.example\.com, to access your sample website, you don't need to register a second domain\. Later in this topic, we explain how to route traffic for www\.*your\-domain\-name* to your website\.

1. In the shopping cart, choose the number of years that you want to register the domain for\.

1. To register more domains, repeat steps 4 through 6\.

1. Choose **Continue**\.

1. On the **Contact Details for Your** *n* **Domains** page, enter contact information for the domain registrant, administrator, and technical contacts\. 

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

By default, you register a domain for one year\. If you won't want to keep the domain, you can deactivate automatic renewal, so the domain expires at the end of a year\. <a name="getting-started-disable-renewal-procedure"></a>

***\(Optional\)* To turn off automatic renewal for a domain**

1. In the navigation pane, choose **Registered domains**\.

1. In the list of domains, select the linked name of your domain\.

1. If the value of the **Auto renew** field is **Enabled \(disable\)**, choose **disable** to turn off automatic renewal\. The change takes effect immediately\.

   If the value of the field is **Disabled \(enable\)**, don't change the setting\.

## Step 2: Request a public certificate<a name="getting-started-cloudfront-request-certificate"></a>

A public certificate is required for your Amazon CloudFront distributions to configure CloudFront to require that viewers use HTTPS so that connections are encrypted when CloudFront communicates with viewers\.

**To request an AWS Certificate Manager\(ACM\) public certificate \(console\)**

1. Sign in to the AWS Management Console and open the ACM console at [https://console\.aws\.amazon\.com/acm/home](https://console.aws.amazon.com/acm/home)\.
**Note**  
Make sure you create the certificate in the US East \(N\. Virginia\) Region\. This is required for Amazon CloudFront\.

   Choose **Request a public certificate** and then **Request a certificate**\.

1. Under **Domain name**, enter your domain, such as **example\.com**\.

   Under **Add another name to this certificate**, enter an asterisk in front of the domain name to request a wildcard certificate for all subdomains, such as **\*\.example\.com**\.

1. Choose **Next**\.

1. On the **Select validation method page**, choose **DNS validation** and then **Next**\.

1. On the **Add tags** page, you can optionally tag your certificate\. Tags are key\-value pairs that serve as metadata for identifying and organizing AWS resources\. 

   When you finish adding tags, choose **Review**\.

1. On the **Review** page, make sure the information you entered is correct, and then choose **Confirm and request**\.

1. On the **Validation** page, expand both domains and choose **Create record in Route 53** to automatically add the CNAME records for your domains, and then choose **Create**\.

   After **Success** is displayed for both domains, choose **Continue** on the bottom of the page\.

## Step 3: Create an S3 bucket to host your subdomain<a name="getting-started-cloudformation-create-s3-www-bucket"></a><a name="getting-started-cloudformation-s3-www-bucket-procedure"></a>

**To create an S3 bucket for www\.*your\-domain\-name***

Amazon S3 lets you store and retrieve your data from anywhere on the internet\. In this step you create an S3 bucket to store all the files for your website\.

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. Choose **Create bucket**\.

1. Enter the following values:  
**Bucket name**  
Enter **www\.*your\-domain\-name***\. For example, if you registered the domain name example\.com, enter **www\.example\.com**\.  
**Region**  
Choose a Region for your bucket\.

1. To accept the default settings and create the bucket, choose **Create bucket**\.

   For more information about the S3 bucket settings, see [View bucket properties](https://docs.aws.amazon.com/AmazonS3/latest/userguide/view-bucket-properties.html) in the *Amazon S3 user guide*\.

## Step 4 : Create another S3 bucket, for your root domain<a name="getting-started-cloudfront-s3-bucket"></a>

If you also want your users to be able to use the root domain, \.*your\-domain\-name* \(such as example\.com\) to access your sample website, create a second S3 bucket\. You then configure the second bucket to route traffic to the first bucket\.<a name="getting-started-cloudfront-s3-bucket-procedure"></a>

**To create an S3 bucket for *your\-domain\-name***

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. Choose **Create bucket**\.

1. Enter the following values:  
**Bucket name**  
Enter ***your\-domain\-name***\. For example, if you registered the domain name example\.com, enter **example\.com**\.  
**Region**  
Choose the same Region that you created the first bucket in\.

1. To accept the default settings and create the bucket, choose **Create bucket**\.

## Step 5: Upload website files to your subdomain bucket<a name="getting-started-cloudformation-www-for-website"></a>

Now that you have an S3 bucket, you can upload your website files\. In this tutorial you will just upload a simple index\.html file that displays text on a page\.\.<a name="getting-started-cloudformation-www-for-website-procedure"></a>

**To enable your S3 bucket for website hosting**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. In the **Buckets** list, choose the linked name of the bucket you want to upload the website files to, such as **www\.example\.com**\.

1. Copy the example text that creates a simple one\-page webstie, paste it into a text editor, and save it as index\.html:

   ```
   <html>
   <head>
   <title>Amazon Route 53 Getting Started</title>	
   </head>
   
   <body>
   
   <h1>Routing Internet traffic to Cloudfront distributions for your website stored in an S3 bucket</h1>
   
   <p>For more information, see 
   <a href="https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/getting-started.html">Getting Started with Amazon Route 53</a> 
   in the <emphasis>Amazon Route 53 Developer Guide</emphasis>.</p>
   
   </body>
   
   </html>
   ```

1. In the **Objects** tab choose **Upload**\.

1. Under **Files and folders**, choose **Add files** and upload your website files\. For this tutorial, upload the index\.html file you saved in step 3\.

## Step 6: Set up your root domain bucket for website redirect<a name="getting-started-cloudfront-bucket-redirect"></a>

After you configure your root domain bucket for website hosting, you can optionally configure your subdomain bucket to redirect all requests to the domain\. For example, you can configure all requests for `example.com` to be redirected to `www.example.com`\.<a name="getting-started-cloudfront-bucket-redirect-procedure"></a>

**To configure a redirect**

1. On the Amazon S3 console, in the **Buckets** list, choose your bucket name \(for example, `example.com`\)\.

1. Choose **Properties**\.

1. Under **Static website hosting**, choose **Edit**\.

1. Under **Static website hosting**, select **Enable**\.

1. Choose **Redirect requests for an object**\.

1. In the **Host name** box, enter your subdomain, for example, **www\.example\.com**\.

1. For **Protocol**, choose **https**\.

1. Choose **Save changes**\.

1. Under **Static website hosting**, note the **Endpoint**\.

   The **Endpoint** is the Amazon S3 website endpoint for your bucket\. You will use this endpoint to set up an Amazon CloudFront distribution\.

## Step 7: Create an Amazon CloudFront distribution for your subdomain<a name="getting-started-cloudfront-distribution"></a>

In this step you create a CloudFront distribution for your subdomain, such as www\.example\.com, to enable your website to use HTTPS so people can view it securely\.<a name="getting-started-cloudfront-distribution-procedure"></a>

**To create a CloudFront distribution**

1. Open the CloudFront console at [https://console.aws.amazon.com/cloudfront/v3/home](https://console.aws.amazon.com/cloudfront/v3/home)\.

1. Choose **Create Distribution**\.

1. Under **Origin Settings**, for **Origin Domain Name**, choose the Amazon S3 bucket that you [created previously](#getting-started-cloudformation-create-s3-www-bucket)\.

   For **S3 bucket access**, select **Yes, use OAI \(bucket can restrict access to only CloudFront\)**\. For the **Origin access identity**, you can choose from the list, or choose **Create new OAI** \(both will work\)\.

   For **Bucket policy**, select **Yes, update the bucket policy**\.

1. For the settings under **Default Cache Behavior Settings**, under **Viewer**, set **Viewer protocol policy**to **Redirect HTTP to HTTPS** and accept the default values for the rest\.

   For more information about cache behavior options, see [Cache behavior settings](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/distribution-web-values-specify.html#DownloadDistValuesCacheBehavior) in the *Amazon CloudFront developer guide*\.

1. For the fields under **Settings**, do the following:
   + Choose **Add item** for **Alternate domain name \(CNAME\) \- optional**, and enter your subdomain, such as **www\.example\.com**\.
   + For **Custom SSL Certificate**, choose the certificate you [created previously](#getting-started-cloudfront-request-certificate)\.
   + In the **Default root object** text box, type in **index\.html**\.
   + For the rest, accept the default values\.

     For more information about distribution options, see [Distribution settings](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/distribution-web-values-specify.html#DownloadDistValuesGeneral)\. 

   

1. At the bottom of the page, choose **Create Distribution**\.

1. After CloudFront creates your distribution, the value of the **Status** column for your distribution changes from **In Progress** to **Deployed**\. This typically takes a few minutes\.

   Record the domain name that CloudFront assigns to your distribution, which appears in the list of distributions\. You can use this domain name to test the distribution\. 

## Step 8: Create an Amazon CloudFront distribution for your root domain<a name="getting-started-cloudfront-distribution-root"></a>

In this step you create a CloudFront distribution for your root domain to have it use HTTPS when its URL is redirected to the subdomain\.<a name="getting-started-cloudfront-distribution-root-procedure"></a>

**To create a CloudFront distribution**

1. Open the CloudFront console at [https://console.aws.amazon.com/cloudfront/v3/home](https://console.aws.amazon.com/cloudfront/v3/home)\.

1. Choose **Create Distribution**\.

1. Under **Origin Settings**, for **Origin Domain Name**, enter the bucket website endpoint\. You get this from the **Static website hosting** section of **Properties** for the Amazon S3 bucket that you [created previously](#getting-started-cloudformation-create-s3-www-bucket)\.

   For the rest, accept the default values\.

1. For the fields under **Default Cache Behavior Settings**, do the following:
   + Under **Viewer**, set **Viewer protocol policy** to **Redirect HTTP to HTTPS**\. 
   + Set **Cache settings** to **CachingDisabled**\. 
   + Accept the default values for the rest\.

   For more information about cache behavior options, see [Cache behavior settings](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/distribution-web-values-specify.html#DownloadDistValuesCacheBehavior) in the *Amazon CloudFront developer guide*\.

1. For the fields under **Settings**, do the following:
   + Choose **Add item** for **Alternate domain name \(CNAME\) \- optional**, and enter your root domain, such as **example\.com**\.
   + For **Custom SSL Certificate**, choose the certificate you [created previously](#getting-started-cloudfront-request-certificate)\.
   + For the rest, accept the default values\.

   

   For more information about distribution options, see [Distribution settings](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/distribution-web-values-specify.html#DownloadDistValuesGeneral)\.

1. At the bottom of the page, choose **Create Distribution**\.

1. After CloudFront creates your distribution, the value of the **Status** column for your distribution changes from **In Progress** to **Deployed**\. This typically takes a few minutes\.

   Record the domain name that CloudFront assigns to your distribution, which appears in the list of distributions\. You can use this domain name to test the distribution, 

## Step 9: Route DNS traffic for your domain to your CloudFront distribution<a name="getting-started-cloudfront-create-alias"></a>

You now have a one\-page website in your S3 bucket that uses a CloudFront distribution\. To start routing internet traffic for your domain to the CloudFront distribution, perform the following procedure\. 

For more information about routing traffic to CloudFront distriibutions, see [Routing traffic to an Amazon CloudFront distribution by using your domain name](routing-to-cloudfront-distribution.md)\.<a name="getting-started-cloudfront-create-alias-procedure"></a>

**To route traffic to your website**

1. Open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Hosted zones**\.
**Note**  
When you registered your domain, Amazon Route 53 automatically created a hosted zone with the same name\. A hosted zone contains information about how you want Route 53 to route traffic for the domain\.

1. In the list of hosted zones, choose the name of your domain\. 

1. Choose **Create record**\.

   If you are in the **Quick create record** view, choose **Switch to wizard**\.
**Note**  
Each record contains information about how you want to route traffic for one domain \(such as example\.com\) or subdomain \(such as www\.example\.com or test\.example\.com\)\. Records are stored in the hosted zone for your domain\.

1. Choose **Simple routing** and choose **Next**\.

1. Choose **Define simple record**\.

1. In **Record name**, type in **www** in front of the default value, which is the name of your hosted zone and your domain\.

1. In **Record type**, choose **A ‐ Routes traffic to an IPv4 address and some AWS resources**\.

1. In **Value/Route traffic to**, choose **Alias to CloudFront distribution**\.

1. Choose the distribution\.

   The distribution name should match the name that appears in the **Domain name** box in the **Distributions** list, for example, `dddjjjkkk.cloudfront.net`\.

1. For **Evaluate target health**, choose **No**\.

1. Choose **Define simple record**\.

**To add an alias record for your root domain \(`example.com`\)**

Add an alias record for your root domain also, so it points to the S3 bucket that redirects traffic to `www.example.com`\. For more information about routing traffic to CloudFront distributions, see [Routing traffic to an Amazon CloudFront distribution by using your domain name](routing-to-cloudfront-distribution.md)\. 

1. Under **Configure records**, choose **Define simple record**\.

1. In **Record name**, accept the default value\.

1. In **Record type**, choose **A ‐ Routes traffic to an IPv4 address and some AWS resources**\.

1. In **Value/Route traffic to**, choose **Alias to CloudFront distribution**\.

1. Choose the distribution\.

   The distribution name should match the name that appears in the **Domain name** box in the **Distributions** list, for example, `dddjjjkkk.cloudfront.net`\.

1. For **Evaluate target health**, choose **No**\.

1. Choose **Define simple record**\.

1. On the **Configure records** page, choose **Create records**\.

## Step 10 : Test your website<a name="getting-started-cloudfront-test"></a>

To verify that the website is working correctly, open a web browser and browse to the following URLs:
+ https://www\.*your\-domain\-name*, for example, `www.example.com` – Displays the index document in the *www\.your\-domain\-name* bucket
+ https://*your\-domain\-name* for example, `example.com` – Redirects your request to the *www\.your\-domain\-name* bucket

In some cases, you might need to clear the cache to see the expected behavior\.

For more advanced information about routing your internet traffic, see [Configuring Amazon Route 53 as your DNS service](dns-configuring.md)\. For information about routing your internet traffic to AWS resources, see [Routing internet traffic to your AWS resources](routing-to-aws-resources.md)\.