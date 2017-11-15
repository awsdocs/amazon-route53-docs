# Migrating DNS Service for an Existing Domain to Amazon Route 53<a name="MigratingDNS"></a>

You can migrate an existing domain from another DNS service to Amazon Route 53 as the DNS service\.


+ [Step 1: Create a Hosted Zone](#Step_CreateHostedZone)
+ [Step 2: Get Your Current DNS Configuration from Your DNS Service Provider](#Step_GetZoneFile)
+ [Step 3: Create Resource Record Sets](#Step_MakeChangeBatch)
+ [Step 4: Check the Status of Your Changes \(API Only\)](#MigratingDNSCheckStatusChange)
+ [Step 5: Update Your Registrar's Name Servers](#Step_UpdateRegistrar)
+ [Step 6: Wait 48 Hours for Your Changes to Take Effect](#migrating-domain-wait-for-ttl)

## Step 1: Create a Hosted Zone<a name="Step_CreateHostedZone"></a>

To migrate a domain from your existing DNS service, start by creating an Amazon Route 53 hosted zone\. Amazon Route 53 stores information about your domain in the hosted zone\.

**Important**  
You can create a hosted zone only for a domain that you have permission to administer\. Typically, this means that you own the domain, but you may also be developing an application for the domain registrant\.

When you create a hosted zone, Amazon Route 53 automatically creates four name server \(NS\) records and a start of authority \(SOA\) record for the zone\. The NS records identify the name servers that you give to your registrar or your DNS service so that queries are routed to Amazon Route 53 name servers\. For more information about NS and SOA records, see [NS and SOA Resource Record Sets that Amazon Route 53 Creates for a Public Hosted Zone](SOA-NSrecords.md)\.

To create a hosted zone using the Amazon Route 53 console, perform the following procedure\. To create a hosted zone using the Amazon Route 53 API, use the `CreateHostedZone` action\. For more information, see [CreateHostedZone](http://docs.aws.amazon.com/Route53/latest/APIReference/API_CreateHostedZone.html) in the *Amazon Route 53 API Reference*\.

**To create a hosted zone using the Amazon Route 53 console**

1. Sign in to the AWS Management Console and open the Amazon Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. If you're new to Amazon Route 53, choose **Get Started Now** under **DNS Management**\.

   If you're already using Amazon Route 53, choose **Hosted Zones** in the **navigation** pane\.

1. Choose **Create Hosted Zone**\.

1. In the **Create Hosted Zone** pane, enter a domain name and, optionally, a comment\. For more information about a setting, pause the mouse pointer over its label to see a tool tip\.

   For information about how to specify characters other than a\-z, 0\-9, and \- \(hyphen\) and how to specify internationalized domain names, see [DNS Domain Name Format](DomainNameFormat.md)\.

1. Choose **Create**\.

## Step 2: Get Your Current DNS Configuration from Your DNS Service Provider<a name="Step_GetZoneFile"></a>

To simplify the process of migrating an existing domain to Amazon Route 53, get the current DNS configuration for the domain from the DNS service provider that is currently servicing the domain\. You can use this information as a basis for configuring Amazon Route 53 as your DNS service\. 

What you ask for and the format that it comes in depends on which company you're currently using as your DNS service provider\. Ideally, they'll give you a zone file, which contains information about all of the resource record sets in your current configuration\. \(Resource record sets tell DNS how you want traffic to be routed for your domains and subdomains\. For example, when someone enters your domain name in a web browser, do you want traffic to be routed to a web server in your data center, to an Amazon EC2 instance, to a CloudFront distribution, or to some other location?\) If you can get a zone file from your current DNS service provider, you can import your existing DNS configuration into your Amazon Route 53 hosted zone, which greatly simplifies the process of creating resource record sets\. Try asking customer support for your current DNS service provider how to get a *zone file* or a *records list*\.

Records that you are likely to migrate include:

+ A \(Address\) records, which associate a domain name \(example\.com\) with the IP address of the home page for the domain \(192\.0\.2\.3\)

+ Mail server \(MX\) records

+ CNAME records, which reroute queries for one domain name \(www\.example\.com\) to another domain name \(example\.com\)

+ Other A records, CNAME records, or other supported DNS record types\. For a list of supported record types, see [Supported DNS Record Types](ResourceRecordTypes.md)\.

## Step 3: Create Resource Record Sets<a name="Step_MakeChangeBatch"></a>

Using the resource record sets that you got from your current DNS service provider as a starting point, create corresponding resource record sets in the Amazon Route 53 hosted zone\. The resource record sets that you create in Amazon Route 53 will become the resource record sets that DNS uses after you update your current DNS service's name server records, as explained in [Step 5: Update Your Registrar's Name Servers](#Step_UpdateRegistrar), later in the process\.

**Important**  
Do not create additional name server \(NS\) or start of authority \(SOA\) records in the Amazon Route 53 hosted zone, and do not delete the existing NS and SOA records\. 

To create resource record sets using the Amazon Route 53 console, see [Working with Resource Record Sets](rrsets-working-with.md)\. To create resource record sets using the Amazon Route 53 API, use `ChangeResourceRecordSets`\. For more information, see [ChangeResourceRecordSets](http://docs.aws.amazon.com/Route53/latest/APIReference/API_ChangeResourceRecordSets.html) in the *[Amazon Route 53 API Reference](http://docs.aws.amazon.com/Route53/latest/APIReference/)*\.

## Step 4: Check the Status of Your Changes \(API Only\)<a name="MigratingDNSCheckStatusChange"></a>

Creating a new hosted zone and changing resource record sets take time to propagate to the Amazon Route 53 DNS servers\. If you used [ChangeResourceRecordSets](http://docs.aws.amazon.com/Route53/latest/APIReference/API_ChangeResourceRecordSets.html) to create your resource record sets, you can use the `GetChange` action to determine whether your changes have propagated\. \(`ChangeResourceRecordSets` returns a value for `ChangeId`, which you can include in a subsequent `GetChange` request\. `ChangeId` is not available if you created the resource record sets by using the console\.\) For more information, see [GET GetChange](http://docs.aws.amazon.com/Route53/latest/APIReference/API_GetChange.html) in the *Amazon Route 53 API Reference*\.

**Note**  
Changes generally propagate to all Amazon Route 53 name servers within 60 seconds\.

## Step 5: Update Your Registrar's Name Servers<a name="Step_UpdateRegistrar"></a>

After your changes to Amazon Route 53 resource record sets have propagated to Amazon Route 53 DNS servers \(see [Step 4: Check the Status of Your Changes \(API Only\)](#MigratingDNSCheckStatusChange)\), update your registrar's name server \(NS\) records to refer to the Amazon Route 53 name servers\. Perform the following procedure\.

1. If the registrar has a method to change the TTL settings for their name servers, we recommend that you reset the settings to 900 seconds\. This limits the time during which client requests will try to resolve domain names using obsolete name servers\. You'll need to wait for the duration of the previous TTL for resolvers and clients to stop caching the DNS records with their previous values\. A common default setting is 172800 seconds \(two days\)\. After the TTL settings expire, you can safely delete the records that are stored at the previous provider and make changes only to Amazon Route 53\.

1. In the Amazon Route 53 console, get the name servers for your Amazon Route 53 hosted zone:

   1. Sign in to the AWS Management Console and open the Amazon Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

   1. In the navigation pane, click **Hosted Zones**\.

   1. On the **Hosted Zones** page, choose the radio button \(not the name\) for the hosted zone\.

   1. In the right pane, make note of the four servers listed for **Name Servers**\.

   Alternatively, you can use the `GetHostedZone` action\. For more information, see [GetHostedZone](http://docs.aws.amazon.com/Route53/latest/APIReference/API_GetHostedZone.html) in the *Amazon Route 53 API Reference*\.

1. Using the method provided by the registrar for the domain, replace the name servers in the registrar's NS records with the four Amazon Route 53 name servers that you got in step 2\.
**Note**  
Some registrars only allow you to specify name servers using IP addresses; they don't allow you to specify fully qualified domain names\. If your registrar requires using IP addresses, you can get the IP addresses for your name servers using the dig utility \(for Mac, Unix, or Linux\) or the nslookup utility \(for Windows\)\. We rarely change the IP addresses of name servers; if we need to change IP addresses, we'll notify you in advance\.

   Depending on the TTL settings for the name servers for the parent domain, the propagation of your changes to DNS resolvers can take 48 hours or more\. During this time, DNS resolvers might still answer requests with the name servers for the registrar\. In addition, client computers might continue to have the previous name servers for the domain in their cache\.

To learn more about working with your hosted zone, see the following related topics\.

**Related Topics**

+ [Getting the Name Servers for a Public Hosted Zone](GetInfoAboutHostedZone.md)

+ [Listing Public Hosted Zones](ListInfoOnHostedZone.md)

+ [Deleting a Public Hosted Zone](DeleteHostedZone.md)

+ [Listing Resource Record Sets](resource-record-sets-listing.md)

## Step 6: Wait 48 Hours for Your Changes to Take Effect<a name="migrating-domain-wait-for-ttl"></a>

You might have to wait a day or two before Amazon Route 53 becomes the DNS service for your domain name\. If you've been using the domain name, DNS resolvers have cached the registrar's NS records for your domain\. NS records are cached for the period specified by the TTL \(time to live\) in the records, which commonly is 86400 to 172800 seconds \(one to two days\)\. Until the TTL expires, DNS resolvers that have cached the registrar's NS records will continue to respond to queries for your domain with the name servers in those NS records\. After the TTL expires for a resolver, the resolver submits another query for the NS records for your domain, and your registrar responds with your Amazon Route 53 NS records\.

**Note**  
If you don't remember the TTL for your registrar's NS records, you can still find it until the TTL expires\. Use a tool like `dig` or `nslookup` to query DNS for the NS records of your domain\.