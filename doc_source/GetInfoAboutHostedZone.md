# Getting the name servers for a public hosted zone<a name="GetInfoAboutHostedZone"></a>

You get the name servers for a public hosted zone if you want to change the DNS service for your domain registration\. For information about how to change your DNS service, see [Making Amazon Route 53 the DNS service for an existing domainMaking Route 53 the DNS service for an existing domain](MigratingDNS.md)\.

**Note**  
Some registrars only allow you to specify name servers using IP addresses; they don't allow you to specify fully qualified domain names\. If your registrar requires using IP addresses, you can get the IP addresses for your name servers using the dig utility \(for Mac, Unix, or Linux\) or the nslookup utility \(for Windows\)\. We rarely change the IP addresses of name servers; if we need to change IP addresses, we'll notify you in advance\. 

**To get the name servers for a hosted zone using the Route 53 console**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, click **Hosted Zones**\.

1. On the **Hosted Zones** page, choose the radio button \(not the name\) for the hosted zone\.

1. In the right pane, make note of the four servers listed for **Name Servers**\.