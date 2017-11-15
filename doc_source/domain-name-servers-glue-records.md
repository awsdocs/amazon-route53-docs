# Adding or Changing Name Servers and Glue Records for a Domain<a name="domain-name-servers-glue-records"></a>

In general, you don't need to change the name servers that Amazon Route 53 assigned to your domain and to the corresponding hosted zone when you registered the domain\. If you do need to add or change name servers, perform the following procedure\. You can also use this procedure to specify glue records \(IP addresses\) when you're configuring white label name servers—name servers that have the same domain name as the hosted zone\. For more information about configuring white label name servers \(also known as vanity name servers or private name servers\), see [Configuring White Label Name Servers](white-label-name-servers.md)\.

**Important**  
If you change name servers to the wrong values, specify the wrong IP addresses in glue records, or delete one or more name servers without specifying new ones, your website or application might become unavailable on the internet\.

**To add or change name servers and glue records for a domain**

1. *\.fi domains only* – Order an authorization key from the Finnish Communications Regulatory Authority, the registry for \.fi domains\. You use the authorization key later in this process\. For more information, see [Ordering of authorization key](https://domain.fi/info/en/index/yllapito/valtuutusavain/valtuutusavaimentilaus.html) on the Finnish Communications Regulatory Authority website\.
**Important**  
The Finnish Communications Regulatory Authority mails the authorization key to you, which can take two weeks or more\. Do not continue with this procedure until you have the key\.

1. Sign in to the AWS Management Console and open the Amazon Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Registered Domains**\.

1. Choose the name of the domain for which you want to edit settings\.

1. Choose **Add/Edit Name Servers**\.

1. *\.fi domains only* – In the **Authorization Key** field, type the authorization key that you got in step 1\.

1. In the **Edit Name Servers** dialog box, you can do the following:

   + Add one or more name servers\.

   + Replace the name of an existing name server\.

   + Add glue records or change the IP addresses in glue records\. If you add a name server or change the name of a name server and specify a name that is a subdomain of the domain that you're updating \(for example, ns1\.example\.com in the domain example\.com\), Amazon Route 53 prompts you to specify one or more IP addresses for the name server\. These IP addresses are known as glue records\.

     You can enter addresses in IPv4 or IPv6 format\. If a name server has multiple IP addresses, type each address on a separate line\.

   + Delete a name server\. Choose the x icon on the right side of the field for that name server\.

1. Choose **Update**\.