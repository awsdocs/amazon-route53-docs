# Adding another Region to your latency\-based routing in Amazon Route 53<a name="TutorialAddingLBRRegion"></a>

If you're using latency based routing and you want to add an instance in a new region, you can gradually shift traffic to the new region in the same way that you gradually shifted traffic to latency\-based routing in [Transitioning to latency\-based routing in Amazon Route 53](TutorialTransitionToLBR.md)\. 

For example, suppose you're using latency\-based routing to route traffic for `www.example.com`, and you want to add an Amazon EC2 instance in Asia Pacific \(Tokyo\) to your instances in US East \(Ohio\), US West \(N\. California\), and Europe \(Ireland\)\. The following example procedure explains one way that you could add an instance in another region\.

For this example, the Amazon Route 53 hosted zone for `example.com` already has a weighted alias record for `www.example.com` that is routing traffic to the latency\-based records for `www-lbr.example.com`:
+ US East \(Ohio\), Elastic IP address `W.W.W.W`
+ US West \(N\. California\), Elastic IP address `X.X.X.X`
+ Europe \(Ireland\), Elastic IP address `Y.Y.Y.Y` 

The weighted alias record has a weight of 100\. After you transitioned to latency\-based routing, assume that you deleted the other weighted record that you used for the transition\. <a name="TutorialAddingLBRRegionProcedure"></a>

**To add another Region to your latency\-based routing in Route 53**

1. Create four new latency\-based records that include the three original regions as well as the new region to which you want to start routing traffic\.
   + US East \(Ohio\), Elastic IP address `W.W.W.W`
   + US West \(N\. California\), Elastic IP address `X.X.X.X`
   + Europe \(Ireland\), Elastic IP address `Y.Y.Y.Y` 
   + Asia Pacific \(Tokyo\), Elastic IP address `Z.Z.Z.Z` 

   Give all of the latency records the same new domain name, for example, `www-lbr-2012-04-30.example.com`, and the same type, A\.

   When you're finished creating the latency records, Route 53 will continue to route traffic using the original weighted alias record \(`www.example.com`\) and latency records \(`www-lbr.example.com`\)\.

   You can use the `www-lbr-2012-04-30.example.com` records for validation testing, for example, to ensure that each endpoint can accept requests\.

1. Create a weighted alias record for the new latency records:
   + For the domain name, specify the name for the existing weighted alias record, `www.example.com`\.
   + For the value of **Alias Target**, specify `www-lbr-2012-04-30.example.com`\.
   + For the value of **Weight**, specify 1\.

   When you finish, Route 53 will begin to route a tiny fraction of your traffic \(1/101\) to the Amazon EC2 instances for which you created the `www-lbr-2012-04-30.example.com` latency records in Step 1\. The remainder of the traffic will continue to be routed to the `www-lbr.example.com` latency records, which do not include the Amazon EC2 instance in the Asia Pacific \(Tokyo\) region\. 

1. As you develop confidence that your endpoints are adequately scaled for the incoming traffic, adjust the weights accordingly\. For example, if you want 10% of your requests to be routed to the latency records that include the Tokyo region, change the weight for `www-lbr.example.com` from 100 to 90 and the weight for `www-lbr-2012-04-30.example.com` from 1 to 10\.

For more information about creating records, see [Creating records by using the Amazon Route 53 console](resource-record-sets-creating.md)\.