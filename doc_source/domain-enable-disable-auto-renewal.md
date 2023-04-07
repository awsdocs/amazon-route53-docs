# Enabling or disabling automatic renewal for a domain<a name="domain-enable-disable-auto-renewal"></a>

When you want to change whether Amazon Route 53 automatically renews registration for a domain shortly before the expiration date, or you want to see the current setting for automatic renewal, perform the following procedure\.

Note that you can't use AWS credits to pay the fee for renewing registration for a domain\.

**Note**  
Make sure you turn off automatic renewal if you intend to cancel your AWS account\. Otherwise, your domain registration will be renewed even if you have cancelled your account\.

**Note**  
We're updating the domains console for Route 53\. During the transition period, you can continue to use the old console\.

Choose the tab for the console that you are using\.
+ [New console](#domain-enable-disable-auto-renewal-new)
+ [Old console](#domain-enable-disable-auto-renewal-old)

------
#### [ New console ]<a name="domain-enable-disable-auto-renewal-procedure"></a>

**To enable or disable automatic renewal for a domain**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Registered domains**\.

1. Choose the name of the domain that you want to update\.

1. On the **Details** section, in the **Actions** dropdown, choose **Turn on auto\-renew** 

   In the **Turn on auto\-renew for <domain name>?** agree to pay the yearly rate, and choose **Turn on**\.
**Note**  
The price listed is for the current registration period, and can change\. For more information, see [Amazon Route 53 Pricing for Domain Registration](https://d32ze2gidvkk54.cloudfront.net/Amazon_Route_53_Domain_Registration_Pricing_20140731.pdf)\.

1. To turn off auto\-renew, select **Turn off auto\-renew** in the **Actions** dropdown\.

1. If you encounter issues while enabling or disabling automatic renewal, you can contact AWS Support for free\. For more information, see [Contacting AWS Support about domain registration issues](domain-contact-support.md)\.

------
#### [ Old console ]<a name="domain-enable-disable-auto-renewal-procedure-old"></a>

**To enable or disable automatic renewal for a domain**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Registered Domains**\.

1. Choose the name of the domain that you want to update\.

1. On the **Details** section, in the **Actions** dropdown, choose **Turn on transfer lock**\. 

   You can navigate to the **Requests** page to see the progress of your request\.
**Note**  
The price listed is for the current registration period, and can change\. For more information, see [Amazon Route 53 Pricing for Domain Registration](https://d32ze2gidvkk54.cloudfront.net/Amazon_Route_53_Domain_Registration_Pricing_20140731.pdf)\.

1. If you encounter issues while enabling or disabling automatic renewal, you can contact AWS Support for free\. For more information, see [Contacting AWS Support about domain registration issues](domain-contact-support.md)\.

------