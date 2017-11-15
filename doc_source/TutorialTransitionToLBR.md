# Transitioning to Latency\-Based Routing in Amazon Route 53<a name="TutorialTransitionToLBR"></a>

With latency\-based routing, Amazon Route 53 can direct your users to the lowest\-latency AWS endpoint available\. For example, you might associate a DNS name like `www.example.com` with an ELB Classic, Application, or Network Load Balancer, or with Amazon EC2 instances or Elastic IP addresses that are hosted in the US East \(Ohio\) and EU \(Ireland\) regions\. The Amazon Route 53 DNS servers decide, based on network conditions of the past couple of weeks, which instances in which regions should serve particular users\. A user in London will likely be directed to the EU \(Ireland\) instance, a user in Chicago will likely be directed to the US East \(Ohio\) instance, and so on\. Amazon Route 53 supports latency\-based routing for A, AAAA, TXT, and CNAME resource record sets, as well as aliases to A and AAAA resource record sets\.

For a smooth, low\-risk transition, you can combine weighted and latency resource record sets to gradually migrate from standard routing to latency\-based routing with full control and rollback capability at each stage\. Let's consider an example in which `www.example.com` is currently hosted on an Amazon EC2 instance in the US East \(Ohio\) region\. The instance has the Elastic IP address `W.W.W.W`\. Suppose you want to continue routing traffic to the US East \(Ohio\) region when applicable while also beginning to direct users to additional Amazon EC2 instances in the US West \(N\. California\) region \(Elastic IP `X.X.X.X`\) and in the EU \(Ireland\) region \(Elastic IP `Y.Y.Y.Y`\)\. The Amazon Route 53 hosted zone for `example.com` already has a resource record set for `www.example.com` that has a **Type** of A and a **Value** \(an IP address\) of `W.W.W.W`\.

When you're finished with the following example, you'll have two weighted alias resource record sets:

+ You'll convert your existing resource record set for `www.example.com` into a weighted alias resource record set that continues to direct the majority of your traffic to your existing Amazon EC2 instance in the US East \(Ohio\) region\.

+ You'll create another weighted alias resource record set that initially directs only a small portion of your traffic to your latency resource record sets, which route traffic to all three regions\. 

By updating the weights in these weighted alias resource record sets, you can gradually shift from routing traffic only to the US East \(Ohio\) region to routing traffic to all three regions in which you have Amazon EC2 instances\.

**To Transition to Latency\-Based Routing**

1. Make a copy of the resource record set for `www.example.com`, but use a new domain name, for example, `copy-www.example.com`\. Give the new resource record set the same **Type** \(A\) and **Value** \(`W.W.W.W`\) as the resource record set for `www.example.com`\.

1. Update the existing A record for `www.example.com` to make it a weighted alias resource record set:

   + For the value of **Alias Target**, specify `copy-www.example.com`\.

   + For the value of **Weight**, specify 100\.

   When you're finished with the update, Amazon Route 53 will continue to use this resource record set to route all traffic to the resource that has an IP address of `W.W.W.W`\.

1. Create a latency resource record set for each of your Amazon EC2 instances, for example:

   + US East \(Ohio\), Elastic IP address `W.W.W.W`

   + US West \(N\. California\), Elastic IP address `X.X.X.X`

   + EU \(Ireland\), Elastic IP address `Y.Y.Y.Y` 

   Give all of the latency resource record sets the same domain name, for example, `www-lbr.example.com` and the same type, A\.

   When you're finished creating the latency resource record sets, Amazon Route 53 will continue to route traffic using the resource record set that you updated in Step 2\.

   You can use `www-lbr.example.com` for validation testing, for example, to ensure that each endpoint can accept requests\.

1. Let's now add the `www-lbr.example.com` latency resource record set into the `www.example.com` weighted resource record set and begin routing limited traffic to the corresponding Amazon EC2 instances\. This means that the Amazon EC2 instance in the US East \(Ohio\) region will be getting traffic from both weighted resource record sets\.

   Create another weighted alias resource record set for `www.example.com`:

   + For the value of **Alias Target**, specify `www-lbr.example.com.`

   + For the value of **Weight**, specify 1\.

   When you finish and your changes are synchronized to Amazon Route 53 servers, Amazon Route 53 will begin to route a tiny fraction of your traffic \(1/101\) to the Amazon EC2 instances for which you created latency resource record sets in Step 3\.

1. As you develop confidence that your endpoints are adequately scaled for the incoming traffic, adjust the weights accordingly\. For example, if you want 10% of your requests to be based on latency\-based routing, change the weights to 90 and 10, respectively\.

For more information about creating latency resource record sets, see [Creating Resource Record Sets by Using the Amazon Route 53 Console](resource-record-sets-creating.md)\.