# Use your domain for a static website in an Amazon S3 bucket<a name="getting-started-s3"></a>

This getting started tutorial shows you how to perform the following tasks:
+ Register a domain name, such as example\.com
+ Create an Amazon S3 bucket and configure it to host a website
+ Create a sample website and save the file in your S3 bucket
+ Configure Amazon Route 53 to route traffic to your new website

When you're finished, you'll be able to open a browser, enter the name of your domain, and view your website\.

**Note**  
You can also transfer an existing domain to Route 53, but the process is more complex and time\-consuming than registering a new domain\. For more information, see [Transferring registration for a domain to Amazon Route 53 ](domain-transfer-to-route-53.md)\. 

**Topics**
+ [Prerequisites](#getting-started-prerequisites)
+ [Step 1: Register a domain](#getting-started-find-domain-name)
+ [Step 2: Create an S3 bucket for your root domain](#getting-started-create-s3-website-bucket)
+ [Step 3 *\(optional\)*: Create another S3 Bucket, for your subdomain](#getting-started-create-s3-www-bucket)
+ [Step 4: Set up your root domain bucket for website hosting](#getting-started-configure-root-for-website)
+ [Step 5 : *\(optional\)*: Set up your subdomain bucket for website redirect](#getting-started-subdomain-bucket-redirect)
+ [Step 6: Upload index to create website content](#getting-started-upload-content)
+ [Step 7: Edit S3 Block Public Access settings](#getting-started-block-access)
+ [Step 8: Attach a bucket policy](#getting-started-attach-policy)
+ [Step 9: Test your domain endpoint](#getting-started-test-domain-endpoint)
+ [Step 10: Route DNS traffic for your domain to your website bucket](#getting-started-create-alias)
+ [Step 11: Test your website](#getting-started-test)
+ [Step 12 \(optional\): Use Amazon CloudFront to speed up distribution of your content](#getting-started-cloudfront)

## Prerequisites<a name="getting-started-prerequisites"></a>

Before you begin, be sure that you've completed the steps in [Setting up Amazon Route 53 ](setting-up-route-53.md)\.

## Step 1: Register a domain<a name="getting-started-find-domain-name"></a>

To use a domain name \(such as example\.com\), you must find a domain name that isn't already in use and register it\. When you register a domain name, you reserve it for your exclusive use everywhere on the internet, typically for one year\. By default, we automatically renew your domain name at the end of each year, but you can turn off automatic renewal\.<a name="getting-started-domain-register-procedure"></a>

**To register a new domain using Amazon Route 53**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. If you're new to Route 53, choose **Get started**\.

   If you're already using Route 53, in the navigation pane, choose **Registered domains**\.

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
   + [Domains that you can register with Amazon Route 53 ](registrar-tld-list.md)

1. Choose **Continue**\.

1. Review the information that you entered, read the terms of service, and select the check box to confirm that you've read the terms of service\. 

1. Choose **Complete Purchase**\.

   We send an email to the registrant for the domain to verify that the registrant contact can be reached at the email address that you specified\. \(This is an ICANN requirement\.\) The email comes from one of the following email addresses:
   + **noreply@registrar\.amazon\.com ** – for TLDs registered by Amazon Registrar\.
   + **noreply@domainnameverification\.net** – for TLDs registered by our registrar associate, Gandi\. To determine who the registrar is for your TLD, see [Domains that you can register with Amazon Route 53 ](registrar-tld-list.md)\.
**Important**  
The registrant contact must follow the instructions in the email to confirm that the email was received, or we must suspend the domain as required by ICANN\. When a domain is suspended, it's not accessible on the internet\.

   You'll receive another email when your domain registration has been approved\. To determine the current status of your request, see [Viewing the status of a domain registration](domain-view-status.md)\.

By default, you register a domain for one year\. If you won't want to keep the domain, you can turn off automatic renewal, so the domain expires at the end of a year\. <a name="getting-started-disable-renewal-procedure"></a>

***\(Optional\)* To turn off automatic renewal for a domain**

1. In the navigation pane, choose **Registered domains**\.

1. In the list of domains, select the linked name of your domain\.

1. If the value of the **Auto renew** field is **Enabled \(disable\)**, choose **disable** to turn off automatic renewal\. The change takes effect immediately\.

   If the value of the field is **Disabled \(enable\)**, don't change the setting\.

## Step 2: Create an S3 bucket for your root domain<a name="getting-started-create-s3-website-bucket"></a>

Amazon S3 lets you store and retrieve your data from anywhere on the internet\. To organize your data, you create buckets and upload your data to the buckets by using the AWS Management Console\. You can use Amazon S3 to host a static website in a bucket\. The following procedure explains how to create a bucket\.<a name="getting-started-create-s3-website-bucket-procedure"></a>

**To create an S3 bucket for your root domain**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. Choose **Create bucket**\.

1. Enter the following values:  
**Bucket name**  
Enter the name of your domain, such as **example\.com**\.  
**Region**  
Choose the Region closest to most of your users\.  
Make note of the Region that you choose; you'll need this information later in the process\.

1. To accept the default settings and create the bucket, choose **Create bucket**\.

## Step 3 *\(optional\)*: Create another S3 Bucket, for your subdomain<a name="getting-started-create-s3-www-bucket"></a>

In the preceding procedure, you created a bucket for your domain name, such as example\.com\. This allows your users to access your website by using your domain name, such as example\.com\.

If you also want your users to be able to use **www**\.*your\-domain\-name*, such as www\.example\.com, to access your sample website, create a second S3 bucket\. Configure the second bucket to route traffic to the first bucket\.<a name="getting-started-create-s3-www-bucket-procedure"></a>

**To create an S3 bucket for www\.*your\-domain\-name***

1. Choose **Create bucket**\.

1. Enter the following values:  
**Bucket name**  
Enter **www\.*your\-domain\-name***\. For example, if you registered the domain name example\.com, enter **www\.example\.com**\.  
**Region**  
Choose the same Region that you created the first bucket in\.

1. To accept the default settings and create the bucket, choose **Create**\.

## Step 4: Set up your root domain bucket for website hosting<a name="getting-started-configure-root-for-website"></a>

Now that you have an S3 bucket, you can configure it for website hosting\.<a name="getting-started-configure-s3-website-bucket-procedure"></a>

**To allow website hosting on your S3 bucket**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. In the **Buckets** list, choose the name of the bucket that you want to enable for static website hosting\.

1. Choose **Properties**\.

1. Under **Static website hosting**, choose **Enable**\.

1. Choose **Use this bucket to host a website**\.

1. Under **Static website hosting**, choose **Enable**\.

1. In **Index document**, enter the file name of the index document, typically `index.html`\.

   The index document name is case sensitive and must exactly match the file name of the HTML index document that you plan to upload to your S3 bucket\. When you configure a bucket for website hosting, you must specify an index document\. Amazon S3 returns this index document when requests are made to the root domain or any of the subfolders\.

1. \(Optional\) To provide your own custom error document for 4XX class errors, in **Error document**, enter the custom error document file name\.

    If you don't specify a custom error document and an error occurs, Amazon S3 returns a default HTML error document\. 

1. \(Optional\) If you want to specify advanced redirection rules, in **Redirection** **rules**, enter XML to describe the rules\.

   For more information, see [Configuring advanced conditional redirects](https://docs.aws.amazon.com/AmazonS3/latest/userguide/how-to-page-redirect.html#advanced-conditional-redirects) in the *Amazon Simple Storage Service Console User Guide*\.

1. Choose **Save changes**\.

1. Under **Static website hosting**, note the **Endpoint**\.

   The **Endpoint** is the Amazon S3 website endpoint for your bucket\. After you finish configuring your bucket as a static website, you can use this endpoint to test your website, as shown in [Step 9: Test your domain endpoint](#getting-started-test-domain-endpoint)\.

   After you use the following steps to edit settings for public access and add a bucket policy that allows public read access,you can use the website endpoint to access your website\.

## Step 5 : *\(optional\)*: Set up your subdomain bucket for website redirect<a name="getting-started-subdomain-bucket-redirect"></a>

After you configure your root domain bucket for website hosting, you can optionally configure your subdomain bucket to redirect all requests to the domain\. For example, you can configure all requests for `www.example.com` to be redirected to `example.com`\.<a name="getting-started-configure-s3-website-redirect-procedure"></a>

**To configure a redirect**

1. On the Amazon S3 console, in the **Buckets** list, choose your subdomain bucket name \(for example, `www.example.com`\)\.

1. Choose **Properties**\.

1. Under **Static website hosting**, choose **Edit**\.

1. Choose **Redirect requests for an object**\.

1. In the **Target bucket** box, enter your root domain, for example, **example\.com**\.

1. For **Protocol**, choose **http**\.

1. Choose **Save changes**\.

## Step 6: Upload index to create website content<a name="getting-started-upload-content"></a>

When you allow static website hosting on your bucket, you enter the name of the index document \(for example, **index\.html**\)\. After you allow static website hosting for the bucket, you upload an HTML file with this index document name to your bucket\.<a name="getting-started-create-website-procedure"></a>

**To upload an index file**

1. Copy the following example text you can use as a simple one\-page website for this tutorial, paste it into a text editor, and save it as index\.html:

   ```
   <html>
   <head>
   <title>Amazon Route 53
                Getting Started</title>	
   </head>
   
   <body>
   
   <h1>Routing Internet Traffic to an Amazon S3 Bucket for Your Website</h1>
   
   <p>For more information, see 
   <a href="https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/getting-started.html">Getting Started with Amazon Route 53
               </a> 
   in the <emphasis>Amazon Route 53
                Developer Guide</emphasis>.</p>
   
   </body>
   
   </html>
   ```

1. In the **Buckets list**, choose the name of the bucket that you want to enable static website hosting for\.

1. In the Amazon S3 console, choose the name of the bucket that you created in the procedure [To allow website hosting on your S3 bucket](#getting-started-configure-s3-website-bucket-procedure)\.

1. Under **Static website hosting**, choose **Edit**\.

1. Choose **Upload**, **Add Files**, select index\.html from where you saved it, and then **Upload**\.

1. If you created and error document, for example, **404\.html**, follow steps 3 through 5 to upload it\.

## Step 7: Edit S3 Block Public Access settings<a name="getting-started-block-access"></a>

By default, Amazon S3 blocks public access to your account and buckets\. If you want to use a bucket to host a static website, use these steps to edit your public access settings\.

**Warning**  
Before you complete this step, review [Blocking public access to your Amazon S3 storage](https://docs.aws.amazon.com/AmazonS3/latest/userguide/access-control-block-public-access.html) to ensure that you understand and accept the risks involved with allowing public access\. When you turn off block public access settings to make your bucket public, anyone on the internet can access your bucket\. We recommend that you block all public access to your buckets\.<a name="getting-started-block-access-procedure"></a>

**To route traffic to your website**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. Choose the name of the bucket that you have configured as a static website\.

1. Choose **Permissions**\.

1. Under **Block public access \(bucket settings\)**, choose **Edit**\.

1. Clear **Block all public access**, and choose **Save changes**\.

Amazon S3 turns off Block Public Access settings for your bucket\. To create a public, static website, you might also have to edit the [Block Public Access settings](https://docs.aws.amazon.com/AmazonS3/latest/userguide/configuring-block-public-access-account.html) for your account before adding a bucket policy\. If account settings for Block Public Access are currently turned on, you see a note under **Block public access \(bucket settings\)**\.

## Step 8: Attach a bucket policy<a name="getting-started-attach-policy"></a>

After you edit Amazon S3 Block Public Access settings, you can add a bucket policy to grant public read access to your bucket\. When you grant public read access, anyone on the internet can access your bucket\. 

**Warning**  
Before you complete this step, review [Blocking public access to your Amazon S3 storage](https://docs.aws.amazon.com/AmazonS3/latest/userguide/access-control-block-public-access.html) to ensure that you understand and accept the risks involved with allowing public access\. When you turn off block public access settings to make your bucket public, anyone on the internet can access your bucket\. We recommend that you block all public access to your buckets\.<a name="getting-started-attach-policy-procedure"></a>

**To route traffic to your website**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. Under **Buckets**, choose the name of your bucket\.

1. Choose **Permissions**\.

1. Under **Bucket Policy**, choose **Edit**\.

1. Copy the following bucket policy and paste it into a text editor\. This policy grants everyone on the internet \(`"Principal":"*"`\) permission to get the files \(`"Action":["s3:GetObject"]`\) in the S3 bucket that is associated with your domain name \(`"arn:aws:s3:::your-domain-name/*"`\)\.

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

1. Update the value for `Resource` to *your\-domain\-name*, for example **example\.com**\.

1. Choose **Save changes**\.

## Step 9: Test your domain endpoint<a name="getting-started-test-domain-endpoint"></a>

After you configure your domain bucket to host a public website, you can test your endpoint\. You can test the endpoint only for your domain bucket because your subdomain bucket is set up for website redirect and not static website hosting\.

**Note**  
Amazon S3 does not support HTTPS access to the website\. If you want to use HTTPS, you can use Amazon CloudFront to serve a static website hosted on Amazon S3\.   
For more information, see [Requiring HTTPS for Communication Between Viewers and CloudFront](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/using-https-viewers-to-cloudfront.html)\.

1. Under **Buckets**, choose the name of your bucket\.

1. Choose **Properties**\.

1. At the bottom of the page, under **Static website hosting**, choose your **Bucket website endpoint**\.

   Your index document opens in a separate browser window\.

## Step 10: Route DNS traffic for your domain to your website bucket<a name="getting-started-create-alias"></a>

You now have a one\-page website in your S3 bucket\. To start routing internet traffic for your domain to your S3 bucket, perform the following procedure\. <a name="getting-started-create-alias-procedure"></a>

**To route traffic to your website**

1. Open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Hosted zones**\.
**Note**  
When you registered your domain, Amazon Route 53 automatically created a hosted zone with the same name\. A hosted zone contains information about how you want Route 53 to route traffic for the domain\.

1. In the list of hosted zones, choose the name of your domain\. 

1. Choose **Create record**\.
**Note**  
Each record contains information about how you want to route traffic for one domain \(such as example\.com\) or one subdomain \(such as www\.example\.com or test\.example\.com\)\. Records are stored in the hosted zone for your domain\.

1. Choose **Switch to wizard**\.

1. Choose **Simple routing** and choose **Next**\.

1. Choose **Define simple record**\.

1. In **Record name**, accept the default value, which is the name of your hosted zone and your domain\.

1. In **Value/Route traffic to**, choose **Alias to S3 website endpoint**\.

1. Choose the Region\.

1. Choose the S3 bucket\.

   The bucket name should match the name that appears in the **Name** box\. In the **Choose S3 bucket** list, the bucket name appears with the Amazon S3 website endpoint for the Region where the bucket was created, for example, `s3-website-us-west-1.amazonaws.com (example.com)`\.

   **Choose S3 bucket** lists a bucket if one of the following is true:
   + You configured the bucket as a static website\.
   + The bucket name is the same as the name of the record that you're creating\.
   + The current AWS account created the bucket\.

   If your bucket does not appear in the **Choose S3 bucket** list, enter the Amazon S3 website endpoint for the Region where the bucket was created, for example, **s3\-website\-us\-west\-2\.amazonaws\.com**\. For a complete list of Amazon S3 website endpoints, see [Amazon S3 Website endpoints](https://docs.aws.amazon.com/general/latest/gr/s3.html#s3_website_region_endpoints)\. For more information about the alias target, see "values/route traffic to" section in [Values for alias records](resource-record-sets-values-alias.md)\.

1. In **Record type**, choose **A ‐ Routes traffic to an IPv4 address and some AWS resources**\.

1. For **Evaluate target health**, choose **No**\.

1. Choose **Define simple record**\.

**\(Optional\) To add an alias record for your subdomain \(`www.example.com`\)**

If you created a bucket for your subdomain, add an alias record for it also\.

1. Under **Configure records**, choose **Define simple record**\.

1. In **Record name** for your subdomain, type `www`\.

1. In **Value/Route traffic to**, choose **Alias to S3 website endpoint**\.

1. Choose the Region\.

1. Choose the S3 bucket, for example, `s3-website-us-west-2.amazonaws.com (example.com)`\.

   If your bucket does not appear in the **Choose S3 bucket** list, enter the Amazon S3 website endpoint for the Region where the bucket was created, for example, **s3\-website\-us\-west\-2\.amazonaws\.com**\. 

1. In **Record type**, choose **A ‐ Routes traffic to an IPv4 address and some AWS resources**\.

1. For **Evaluate target health**, choose **No**\.

1. Choose **Define simple record**\.

1. On the **Configure records** page, choose **Create records**\.

## Step 11: Test your website<a name="getting-started-test"></a>

To verify that the website is working correctly, open a web browser and browse to the following URLs:
+ http://*your\-domain\-name*, for example, `example.com` – Displays the index document in the *your\-domain\-name* bucket
+ http://www\.*your\-domain\-name* for example, `www.example.com` – Redirects your request to the *your\-domain\-name* bucket

In some cases, you might need to clear the cache to see the expected behavior\.

For more advanced information about routing your internet traffic, see [Configuring Amazon Route 53 as your DNS service](dns-configuring.md)\. For information about routing your internet traffic to AWS resources, see [Routing internet traffic to your AWS resources](routing-to-aws-resources.md)\.

## Step 12 \(optional\): Use Amazon CloudFront to speed up distribution of your content<a name="getting-started-cloudfront"></a>

CloudFront is a web service that speeds up distribution of your static and dynamic web content, such as \.html, \.css, \.js, and image files, to your users\. CloudFront delivers your content through a worldwide network of data centers called edge locations\. When a user requests content that you're serving with CloudFront, the user is routed to the edge location that provides the lowest latency \(time delay\), so that content is delivered with the best possible performance\.
+ If the content is already in the edge location with the lowest latency, CloudFront delivers it immediately\.
+ If the content is not in that edge location, CloudFront retrieves it from an Amazon S3 bucket or an HTTP server \(for example, a web server\) that you have identified as the source for the definitive version of your content\.

For information about using CloudFront to distribute the content in your Amazon S3 bucket, see [Adding CloudFront when you're distributing content from Amazon S3](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/MigrateS3ToCloudFront.html#adding-cloudfront-to-s3) in the *Amazon CloudFront Developer Guide*\. 