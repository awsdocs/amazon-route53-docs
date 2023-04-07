# Viewing the status of a domain registration<a name="domain-view-status"></a>

ICANN, the organization that maintains a central database of domain names, has developed a set of domain name status codes \(also known as EPP status codes\) that tell you the status of a variety of operations, for example, registering a domain name, transferring a domain name to another registrar, renewing the registration for a domain name, and so on\. All registrars use this same set of status codes\.

To view the status code for your domains, perform the following procedure\. 

**Note**  
We're updating the domains console for Route 53\. During the transition period, you can continue to use the old console\.

Choose the tab for the console that you are using\.
+ [New console](#view_status_new_console)
+ [Old console](#view_status_old_console)

------
#### [ New console ]<a name="domain-view-status-procedure-new"></a>

**To view the ICANN status code of a domain**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, expand **Domains** and choose **Registered Domains**\.

1. Select the linked name of your domain\.

1. If you need to take an action, such as resending the verification email to the registrant contact, a banner on top of the page will indicate the action you need to take\. 

1. For the current status of your domain, see the value of the **Domain status code** field\. 

   For a current list of domain name status codes and an explanation of what each code means, go to the [ICANN website](https://www.icann.org/) and search for **epp status codes**\. \(Search on the ICANN website; web searches sometimes return an old version of the document\.\)

You can also view the status of the registration on the **Requests** page\.<a name="domain-requests-view"></a>

**To view the registration status**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, expand **Domains** and choose **Requests**\.

1. On the **Requests** page, you can view the registration status, and additionally the status of any other actions, such as deleting domains, ,locking domain transfers, adding or deleting DNSSEC keys, you have taken on domains,

   Any action you might have to take to complete a process, such as verifying your email, is also listed\.

   1. To respond to an action request, select the radio\-button next to the domain name and then select the action from the **Action** drop\-down\.

------
#### [ Old console ]<a name="domain-view-status-procedure"></a>

**To view the ICANN status code of a domain**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Registered Domains**\.

1. Select the linked name of your domain\.

1. For the current status of your domain, see the value of the **Domain name status** field\. 

   For a current list of domain name status codes and an explanation of what each code means, go to the [ICANN website](https://www.icann.org/) and search for **epp status codes**\. \(Search on the ICANN website; web searches sometimes return an old version of the document\.\)

------