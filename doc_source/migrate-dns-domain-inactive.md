# Migrating DNS Service for an Inactive Domain<a name="migrate-dns-domain-inactive"></a>

If you want to migrate DNS service to Amazon Route 53 for a domain that isn't getting any traffic \(or is getting very little traffic\), perform the procedures in this section\.


+ [Step 1: Get Your Current DNS Configuration from the Current DNS Service Provider \(Inactive Domains\)](#migrate-dns-get-zone-file-domain-inactive)
+ [Step 2: Create a Hosted Zone \(Inactive Domains\)](#migrate-dns-create-hosted-zone-domain-inactive)
+ [Step 3: Create Records \(Inactive Domains\)](#migrate-dns-create-records-domain-inactive)
+ [Step 4: Update the Domain Registration to Use Amazon Route 53 Name Servers \(Inactive Domains\)](#migrate-dns-update-domain-inactive)

## Step 1: Get Your Current DNS Configuration from the Current DNS Service Provider \(Inactive Domains\)<a name="migrate-dns-get-zone-file-domain-inactive"></a>

When you migrate DNS service from another provider to Route 53, you reproduce your current DNS configuration in Route 53\. In Route 53, you create a hosted zone that has the same name as your domain, and you create records in the hosted zone\. Each record indicates how you want to route traffic for a specified domain name or subdomain name\. For example, when someone enters your domain name in a web browser, do you want traffic to be routed to a web server in your data center, to an Amazon EC2 instance, to a CloudFront distribution, or to some other location?

The process that you use depends on the complexity of your current DNS configuration:

+ **If your current DNS configuration is simple** – If you're routing internet traffic for just a few subdomains to a small number of resources, such as web servers or Amazon S3 buckets, then you can manually create a few records in the Route 53 console\.

+ **If your current DNS configuration is more complex, and you just want to reproduce your current configuration** – You can simplify the migration if you can get a zone file from the current DNS service provider, and import the zone file into Route 53\. \(Not all DNS service providers offer zone files\.\) When you import a zone file, Route 53 automatically reproduces the existing configuration by creating the corresponding records in your hosted zone\.

  Try asking customer support with your current DNS service provider how to get a *zone file* or a *records list*\. For information about the required format of the zone file, see [Creating Records By Importing a Zone File](resource-record-sets-creating-import.md)\.

+ **If your current DNS configuration is more complex, and you're interested in Route 53 routing features** – Review the following documentation to see whether you want to use Route 53 features that aren't available from other DNS service providers\. If so, you can either create records manually, or you can import a zone file and then create or update records later:

  + [Choosing Between Alias and Non\-Alias Records](resource-record-sets-choosing-alias-non-alias.md) explains the advantages of Route 53 alias records, which route traffic to some AWS resources for no charge\. Resources that you can create aliases for include CloudFront distributions, Elastic Beanstalk environments, Elastic Load Balancing load balancers, and Amazon S3 buckets\.

  + [Choosing a Routing Policy](routing-policy.md) explains the Route 53 routing options, for example, routing based on the location of your users, routing based on the latency between your users and your resources, routing based on whether your resources are healthy, and routing to resources based on weights that you specify\.
**Note**  
You can also import a zone file and later change your configuration to take advantage of alias records and complex routing policies\.

If you can't get a zone file or if you want to manually create records in Route 53, the records that you're likely to migrate include the following:

+ **A \(Address\) records** – associate a domain name or subdomain name with the IPv4 address \(for example, 192\.0\.2\.3\) of the corresponding resource

+ **AAAA \(Address\) records** – associate a domain name or subdomain name with the IPv6 address \(for example, 2001:0db8:85a3:0000:0000:abcd:0001:2345\) of the corresponding resource

+ **Mail server \(MX\) records** – route traffic to mail servers

+ **CNAME records** – reroute traffic for one domain name \(example\.net\) to another domain name \(example\.com\)

+ **Records for other supported DNS record types** – For a list of supported record types, see [Supported DNS Record Types](ResourceRecordTypes.md)\.

## Step 2: Create a Hosted Zone \(Inactive Domains\)<a name="migrate-dns-create-hosted-zone-domain-inactive"></a>

To tell Amazon Route 53 how you want to route traffic for your domain, you create a hosted zone that has the same name as your domain, and then you create records in the hosted zone\. 

**Important**  
You can create a hosted zone only for a domain that you have permission to administer\. Typically, this means that you own the domain, but you might also be developing an application for the domain registrant\.

When you create a hosted zone, Route 53 automatically creates a name server \(NS\) record and a start of authority \(SOA\) record for the zone\. The NS record identifies the four name servers that Route 53 associated with your hosted zone\. To make Route 53 the DNS service for your domain, you update the registration for the domain to use these four name servers\. 

**Important**  
Don't create additional name server \(NS\) or start of authority \(SOA\) records, and don't delete the existing NS and SOA records\. 

**To create a hosted zone**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. If you're new to Route 53, choose **Get Started Now** under **DNS Management**\.

   If you're already using Route 53, choose **Hosted Zones** in the navigation pane\.

1. Choose **Create Hosted Zone**\.

1. In the **Create Hosted Zone** pane, enter a domain name and, optionally, a comment\. For more information about a setting, pause the mouse pointer over its label to see a tool tip\.

   For information about how to specify characters other than a\-z, 0\-9, and \- \(hyphen\) and how to specify internationalized domain names, see [DNS Domain Name Format](DomainNameFormat.md)\.

1. For **Type**, accept the default value of **Public Hosted Zone**\.

1. Choose **Create**\.

## Step 3: Create Records \(Inactive Domains\)<a name="migrate-dns-create-records-domain-inactive"></a>

After you create a hosted zone, you create records in the hosted zone that define where you want to route traffic for a domain \(example\.com\) or subdomain \(www\.example\.com\)\. For example, if you want to route traffic for example\.com and www\.example\.com to a web server on an Amazon EC2 instance, you create two records, one named example\.com and the other named www\.example\.com\. In each record, you specify the IP address for your EC2 instance\.

You can create records in a variety of ways:

**Export a zone file**
If you are migrating resource records from one AWS account to another one, it is currently not possible to export them from the AWS console. Instead, using the following AWSCLI command (requires [jq](https://stedolan.github.io/jq/)) will help you prepare an importable TSV:

```bash
echo -e "\$ORIGIN\tEXAMPLE.COM." && echo -e "\$TTL\t1h" && aws route53 list-resource-record-sets --hosted-zone-id Z1EEXAMPLE9SF3 | jq -r '.ResourceRecordSets[] | [.Name, .Type, .ResourceRecords[0].Value] | join("\t")' - | grep -vE "NS|SOA"
```

Make sure to substitute the `EXAMPLE.COM` for your desired domain name. The command above will generate a TSV you can use later on the destination hosted zone:

```
$ORIGIN   EXAMPLE.COM.
$TTL      1h
EXAMPLE.COM.	MX	10 inbound-smtp.eu-west-1.amazonaws.com
EXAMPLE.COM.	TXT	"google-site-verification=foo"
(...)
```

SOA/NS records are excluded from the export since they cannot be automatically imported between accounts.

**Import a zone file**  
This is the easiest method if you got a zone file from your current DNS service in [Step 1: Get Your Current DNS Configuration from the Current DNS Service Provider \(Inactive Domains\)](#migrate-dns-get-zone-file-domain-inactive)\. Amazon Route 53 can't predict when to create alias records or to use special routing types such as weighted or failover\. As a result, if you import a zone file, Route 53 creates standard DNS records using the simple routing policy\.  
For more information, see [Creating Records By Importing a Zone File](resource-record-sets-creating-import.md)\.

**Create records individually in the console**  
If you didn't get a zone file and you just want to create a few records with a routing policy of Simple to get started, you can create the records in the Route 53 console\. You can create both alias and non\-alias records\.  
For more information, see the following topics:  

+ [Choosing a Routing Policy](routing-policy.md)

+ [Choosing Between Alias and Non\-Alias Records](resource-record-sets-choosing-alias-non-alias.md)

+ [Creating Records by Using the Amazon Route 53 Console](resource-record-sets-creating.md)

**Create records programmatically**  
You can create records by using one of the AWS SDKs, the AWS CLI, or AWS Tools for Windows PowerShell\. For more information, see [AWS Documentation](http://docs.aws.amazon.com/)\.  
If you're using a programming language that AWS doesn't provide an SDK for, you can also use the Route 53 API\. For more information, see the [Amazon Route 53 API Reference](http://docs.aws.amazon.com/Route53/latest/APIReference/)\.

## Step 4: Update the Domain Registration to Use Amazon Route 53 Name Servers \(Inactive Domains\)<a name="migrate-dns-update-domain-inactive"></a>

When you've finished creating records for the domain, you can change the DNS service for your domain to Amazon Route 53\. Perform the following procedure to update settings with the domain registrar\.

**To update the name servers for the domain**

1. In the Route 53 console, get the name servers for your Route 53 hosted zone:

   1. Open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

   1. In the navigation pane, choose **Hosted zones**\.

   1. On the **Hosted zones** page, choose the radio button \(not the name\) for the applicable hosted zone\.

   1. Make note of the four names listed for **Name Servers**\.

1. Use the method provided by the registrar for the domain to change the name servers for the domain to use the four Route 53 name servers that you got in step 1 of this procedure\.

   If the domain is registered with Route 53, see [Adding or Changing Name Servers and Glue Records for a Domain](domain-name-servers-glue-records.md)\.
