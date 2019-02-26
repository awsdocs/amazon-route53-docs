# Redirecting Internet Traffic to Another Domain and Redirecting HTTP Requests to HTTPS<a name="tutorial-redirecting-dns-queries"></a>

You can use a combination of AWS services to redirect internet traffic from one domain \(such as example\.com\) to another domain \(such as example\.net\) and redirect HTTP request to HTTPS\. Here's how it works:

1. A viewer, such as a web browser, submits a request for a domain such as example\.com\.

1. Amazon Route 53 routes the request for example\.com to an Amazon CloudFront distribution\.

1. Amazon CloudFront forwards the request to an Amazon S3 bucket that you specified as the origin for the distribution\. The bucket doesn't contain your content; instead, when you created the bucket, you configured it to redirect requests to another domain name\.

1. Amazon S3 uses HTTPS to return an HTTP 301/302 status code to CloudFront along with the name of the domain that you want to redirect traffic to, such as example\.net\.

1. CloudFront returns the redirect to the viewer\.

   Because the response from S3 uses HTTPS, CloudFront uses HTTPS to return the response to the viewer\. AWS Certificate Manager \(ACM\) provides the SSL/TLS certificate that encrypts communication between CloudFront and the viewer\.

1. The viewer submits a request for example\.net\.

1. The DNS service for example\.net routes the request to the applicable resource, such as another S3 bucket or an EC2 instance running a web server\.

**Estimated cost**
+ There's an annual fee to register a domain, ranging from $9 to several hundred dollars, depending on the top\-level domain \(TLD\), such as \.com\. For more information, see [Route 53 Pricing for Domain Registration](https://d32ze2gidvkk54.cloudfront.net/Amazon_Route_53_Domain_Registration_Pricing_20140731.pdf)\. This fee is not refundable\.
+ When you register a domain, we automatically create a hosted zone that has the same name as the domain\. You use the hosted zone to specify where you want Route 53 to route traffic for your domain\. The fee for a hosted zone is $0\.50 per month\.
+ If you're a new AWS customer, you can get started with Amazon S3 for free\. If you're an existing AWS customer, charges are based on how much data you store, on the number of requests for your data, and on the amount of data transferred\. For more information, see [Amazon S3 Pricing](https://aws.amazon.com/s3/pricing/)\.

**Topics**
+ [Step 1: Set up Route 53](#tutorial-redirecting-dns-queries-set-up-route-53)
+ [Step 2: Register a Domain](#tutorial-redirecting-dns-queries-register-domain)
+ [Step 3: Get an SSL/TLS Certificate from ACM](#tutorial-redirecting-dns-queries-get-certificate)
+ [Step 4: Create an S3 Bucket and Configure It to Redirect Requests to Another Domain Name](#tutorial-redirecting-dns-queries-create-s3-bucket)
+ [Step 5: Create or Update a CloudFront Distribution](#tutorial-redirecting-dns-queries-cloudfront)
+ [Step 6: Create a Route 53 Record that Routes Traffic to Your CloudFront Distribution](#tutorial-redirecting-dns-queries-create-route-53-record)
+ [Step 7: Test the Configuration](#tutorial-redirecting-dns-queries-test)

## Step 1: Set up Route 53<a name="tutorial-redirecting-dns-queries-set-up-route-53"></a>

If you already have an AWS account, if you know how to access resources using the AWS console, and if you've created an IAM user, you can skip this step\. If you haven't performed those steps, see [Setting Up Amazon Route 53](setting-up-route-53.md)\.

## Step 2: Register a Domain<a name="tutorial-redirecting-dns-queries-register-domain"></a>

For information about how to register a domain, see [Registering a New Domain](domain-register.md)\.

## Step 3: Get an SSL/TLS Certificate from ACM<a name="tutorial-redirecting-dns-queries-get-certificate"></a>

You can ensure that any HTTP requests are converted to HTTPS, so traffic is encrypted between viewers and the resource that you're redirecting traffic to\. To do so, you configure S3 to redirect any HTTP requests to HTTPS\. To use HTTPS, you need an SSL/TLS certificate\.

If you already have an SSL/TLS certificate for the domain that you're redirecting traffic to, you can skip this step\.

If you don't have a certificate, perform the following steps in the [Getting Started](https://docs.aws.amazon.com/acm/latest/userguide/gs.html) topic in the *AWS Certificate Manager User Guide*:

1. Request a certificate\.

1. Validate that you own the domain using either DNS or email\.

## Step 4: Create an S3 Bucket and Configure It to Redirect Requests to Another Domain Name<a name="tutorial-redirecting-dns-queries-create-s3-bucket"></a>

In this tutorial, we're using an S3 bucket as the origin for your CloudFront distribution, but the bucket won't contain your content\. Instead, we're using the bucket only to redirect requests from one domain name to another\.<a name="tutorial-redirecting-dns-queries-create-s3-bucket-procedure"></a>

**To create an S3 bucket and configure it to redirect requests to another domain name**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. Choose **Create bucket**\.

1. For **Bucket name**, specify any value you want\. The bucket doesn't need to have the same name as the domain that you're redirecting internet traffic for or the domain that you're routing traffic to\.

1. For **Region**, choose a region that's close to a large portion of your users\.

1. Choose **Next**\.

1. On the **Set properties** page of the **Create bucket** wizard, choose **Next**\.

1. Choose **Next**\.

1. Choose **Create bucket**\.

1. In the list of buckets, choose the name of your new bucket\.

1. Choose the **Properties** tab\.

1. Choose **Static website hosting**\.

1. In the **Static website hosting** box, make note of the **Endpoint URL**, for example, **http://example\.com\.s3\-website\-us\-west\-2\.amazonaws\.com**\. You'll need this value when you create or update a CloudFront distribution in the next procedure\.

1. Choose **Redirect requests**\.

1. For **Target bucket or domain**, enter the name of the domain \(example\.com\) or subdomain \(www\.example\.com\) that you want to redirect requests to\.

1. For **Protocol**, enter **https**, all lowercase\.

1. Choose **Save**\.

## Step 5: Create or Update a CloudFront Distribution<a name="tutorial-redirecting-dns-queries-cloudfront"></a>

You can either create a new CloudFront web distribution or update an existing distribution\. Perform the applicable procedure:
+  [To create a CloudFront web distribution](#tutorial-redirecting-dns-queries-cloudfront-procedure-create) 
+  [To update an existing CloudFront web distribution](#tutorial-redirecting-dns-queries-cloudfront-procedure-update) <a name="tutorial-redirecting-dns-queries-cloudfront-procedure-create"></a>

**To create a CloudFront web distribution**

1. Open the CloudFront console at [ https://console\.aws\.amazon\.com/cloudfront/](https://console.aws.amazon.com/cloudfront/)\.

1. Choose **Create Distribution**\.

1. On the **Select a delivery method for your content** page, in the **Web** section, choose **Get Started**\.

1. On the **Create Distribution** page, for **Origin Domain Name**, enter or paste the **Endpoint URL** that you got when you created the bucket, for example:

   **http://example\.com\.s3\-website\-us\-west\-2\.amazonaws\.com**
**Note**  
Don't choose the name of the bucket from the **Origin Domain Name** list\. The format of the bucket name is different, and the redirect won't work if you choose the bucket from the list\.

1. For the other settings in the **Origin Settings** section, accept the default values\.

1. Under **Default Cache Behavior Settings**, for **Viewer Protocol Policy**, choose **HTTP and HTTPS**\.

1. For the other settings in the **Default Cache Behavior Settings** section, accept the default values\.

1. In the **Distribution Settings** section, accept the default values for all settings except the following:  
**Alternate domain names \(CNAMEs\)**  
Enter the names of the two domains that you want users to use to access your content, such as example\.com and example\.net, or www\.example\.com and example\.com\.  
**SSL Certificate**  
Choose **Custom SSL Certificate**\. Then choose the certificate that you got in [Step 3: Get an SSL/TLS Certificate from ACM](#tutorial-redirecting-dns-queries-get-certificate)\.

1. Also in the **Distribution Settings** section, for **Custom SSL Client Support**, accept the default value of **Only Clients that Support Server Name Indication \(SNI\)**\. If you choose the other option, you have to pay for dedicated IP addresses to serve HTTPS requests\. For more information, see [Choosing How CloudFront Serves HTTPS Requests](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/cnames-https-dedicated-ip-or-sni.html) in the *Amazon CloudFront Developer Guide*\.

1. Choose **Create Distribution**\.

1. On the **CloudFront Distributions** page, find the distribution that you just created, and wait for the value of the **Status** column to change from **In Progress** to **Deployed**\.<a name="tutorial-redirecting-dns-queries-cloudfront-procedure-update"></a>

**To update an existing CloudFront web distribution**

1. Open the CloudFront console at [ https://console\.aws\.amazon\.com/cloudfront/](https://console.aws.amazon.com/cloudfront/)\.

1. Choose the ID of the distribution that you want to update\.

1. On the **General** tab, choose **Edit**\.

1. Update the following values:  
**Alternate domain names \(CNAMEs\)**  
Enter the names of the two domains that you want users to use to access your content, such as example\.com and example\.net, or www\.example\.com and example\.com\.  
**SSL Certificate**  
Choose **Custom SSL Certificate**\. Then choose the certificate that you got in [Step 3: Get an SSL/TLS Certificate from ACM](#tutorial-redirecting-dns-queries-get-certificate)\.

1. Also in the **Distribution Settings** section, for **Custom SSL Client Support**, accept the default value of **Only Clients that Support Server Name Indication \(SNI\)**\. If you choose the other option, you have to pay for dedicated IP addresses to serve HTTPS requests\. For more information, see [Choosing How CloudFront Serves HTTPS Requests](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/cnames-https-dedicated-ip-or-sni.html) in the *Amazon CloudFront Developer Guide*\.

1. Choose the **Origins** tab\.

1. Choose **Create Origin**\.

1. For **Origin Domain Name**, enter or paste the **Endpoint URL** that you got when you created the bucket, for example:

   **http://example\.com\.s3\-website\-us\-west\-2\.amazonaws\.com**
**Note**  
Don't choose the name of the bucket from the **Origin Domain Name** list\. The format of the bucket name is different, and the redirect won't work if you choose the bucket from the list\.

1. Choose **Create**\.

1. Choose the **Behaviors** tab\.

1. Choose the cache behavior that has **Default \(\*\)** in the **Path Pattern** column, and choose **Edit**\.

1. In the **Origin** list, choose the origin that you created in steps 7 and 8\.

1. Change **Viewer Protocol Policy** to **HTTP and HTTPS**\.

1. Choose **Yes, Edit**\.

1. In the navigation pane, choose **Distributions**\.

1. Find the distribution that you just updated, and wait for the value of the **Status** column to change from **In Progress** to **Deployed**\.

## Step 6: Create a Route 53 Record that Routes Traffic to Your CloudFront Distribution<a name="tutorial-redirecting-dns-queries-create-route-53-record"></a>

The final step before you can test the configuration is to add a record to Route 53 that routes traffic to your CloudFront distribution\. Perform the following procedure\.<a name="tutorial-redirecting-dns-queries-create-route-53-record-procedure"></a>

**To create a Route 53 record that routes traffic to your CloudFront distribution**

1. Open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Hosted zones**\.

1. Choose the hosted zone that has the same name as the domain that you're redirecting traffic for\.

1. Choose **Create Record Set**\.

1. Specify the following values:  
**Name**  
Specify the domain or subdomain name that you want to redirect internet traffic for\. The default value is the name of the domain\.  
If you want to redirect traffic for a subdomain, enter the value that precedes the domain name\. For example, to redirect traffic for www\.example\.com, enter **www**\.  
**Type**  
Accept the default value, **A – IPv4 address**\.  
**Alias**  
Choose **Yes**\.  
**Alias Target**  
In the **CloudFront distributions** section of the list, choose the distribution that you created or updated in [Step 5: Create or Update a CloudFront Distribution](#tutorial-redirecting-dns-queries-cloudfront)\. The list of distributions includes an alternate domain name\.  
If you use one AWS account to create the current hosted zone and a different account to create a distribution, the distribution won't appear in the **Alias Targets** list\. Enter the CloudFront domain name for the distribution, such as d111111abcdef8\.cloudfront\.net\.  
**Routing Policy**  
Accept the default value of **Simple**\.  
**Evaluate Target Health**  
Accept the default value of **No**\.

1. Choose **Create**\.

## Step 7: Test the Configuration<a name="tutorial-redirecting-dns-queries-test"></a>

To verify that the website is working correctly, open a web browser and browse to the following URLs\. In both cases, you should see the content for the domain that you're redirecting DNS queries to:
+ http://domain\-name\-that\-you're\-redirecting\-from
+ https://domain\-name\-that\-you're\-redirecting\-from

In some cases, you might need to clear the cache to see the expected behavior\.