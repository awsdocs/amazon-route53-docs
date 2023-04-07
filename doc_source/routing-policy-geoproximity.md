# Geoproximity routing \(traffic flow only\)<a name="routing-policy-geoproximity"></a>

Geoproximity routing lets Amazon Route 53 route traffic to your resources based on the geographic location of your users and your resources\. You can also optionally choose to route more traffic or less to a given resource by specifying a value, known as a *bias*\. A bias expands or shrinks the size of the geographic region from which traffic is routed to a resource\.

To use geoproximity routing, you must use Route 53 [traffic flow](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/traffic-flow.html)\. You create geoproximity rules for your resources and specify one of the following values for each rule:
+ If you're using AWS resources, the AWS Region that you created the resource in
+ If you're using non\-AWS resources, the latitude and longitude of the resource

To optionally change the size of the geographic region from which Route 53 routes traffic to a resource, specify the applicable value for the bias:
+ To expand the size of the geographic region from which Route 53 routes traffic to a resource, specify a positive integer from 1 to 99 for the bias\. Route 53 shrinks the size of adjacent regions\. 
+ To shrink the size of the geographic region from which Route 53 routes traffic to a resource, specify a negative bias of \-1 to \-99\. Route 53 expands the size of adjacent regions\. 

You cannot use geoproximity routing policy for records in a private hosted zone\.

The following map shows four AWS Regions \(numbered 1 through 4\) and a location in Johannesburg, South Africa that is specified by latitude and longitude \(5\)\.

![\[A map of the world that shows how traffic is routed when you have geoproximity records for resources in the AWS Regions in US West (Oregon), US East (Northern Virginia), EU West (Paris), and Asia Pacific (Tokyo), and you have a record for a non-AWS resource in Johannesburg, South Africa.\]](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/images/traffic-flow-geoproximity-map-example-no-bias.png)

The following map shows what happens if you add a bias of \+25 for the US East \(Northern Virginia\) Region \(number **2** on the map\)\. Traffic is routed to the resource in that Region from a larger portion of North America than previously, and from all of South America\.

![\[A map of the world that shows how traffic is routed when you add a bias of +25 in the US East (Northern Virginia) Region.\]](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/images/traffic-flow-geoproximity-map-example-bias-plus-25.png)

The following map shows what happens if you change the bias to \-25 for the US East \(Northern Virginia\) Region\. Traffic is routed to the resource in that Region from smaller portions of North and South America than previously, and more traffic is routed to resources in the adjacent regions **1**, **3**, and **5**\. 

![\[A map of the world that shows how traffic is routed when you add a bias of -25 in the US East (Northern Virginia) Region.\]](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/images/traffic-flow-geoproximity-map-example-bias-minus-25.png)

The effect of changing the bias for your resources depends on a number of factors, including the following:
+ The number of resources that you have\.
+ How close the resources are to one another\.
+ The number of users that you have near the border area between geographic regions\. For example, suppose you have resources in the AWS Regions US East \(Northern Virginia\) and US West \(Oregon\) and you have a lot of users in Dallas, Austin, and San Antonio, Texas, USA\. Those cities are roughly equidistant between your resources, so a small change in bias could result in a large swing in traffic from resources in one AWS Region to the other\.

We recommend that you change the bias in small increments to prevent overwhelming your resources due to an unanticipated swing in traffic\.

For more information, see [How Amazon Route 53 uses EDNS0 to estimate the location of a user](routing-policy-edns0.md)\.

## How Amazon Route 53 uses bias to route traffic<a name="routing-policy-geoproximity-bias"></a>

Here's the formula that Amazon Route 53 uses to determine how to route traffic:

**Positive bias**  
`Biased distance = actual distance * [1 - (bias/100)]`

**Negative bias**  
`Biased distance = actual distance / [1 + (bias/100)]`

When the value of the bias is positive, Route 53 treats the source of a DNS query and the resource that you specify in a geoproximity record \(such as an EC2 instance in an AWS Region\) as if they were closer together than they really are\. For example, suppose you have the following geoproximity records:
+ A record for web server A, which has a positive bias of 50
+ A record for web server B, which has no bias

When a geoproximity record has a positive bias of 50, Route 53 halves the distance between the source of a query and the resource for that record\. Then Route 53 calculates which resource is closer to the source of the query\. Suppose web server A is 150 kilometers from the source of a query and web server B is 100 kilometers from the source of the query\. If neither record had a bias, Route 53 would route the query to web server B because it's closer\. However, because the record for web server A has a positive bias of 50, Route 53 treats web server A as if it's 75 kilometers from the source of the query\. As a result, Route 53 routes the query to web server A\. 

Here's the calculation for a positive bias of 50:

```
Bias = 50
Biased distance = actual distance * [1 - (bias/100)]

Biased distance = 150 kilometers * [1 - (50/100)]
Biased distance = 150 kilometers * (1 - .50)
Biased distance = 150 kilometers * (.50)
Biased distance = 75 kilometers
```