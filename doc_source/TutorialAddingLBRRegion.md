# Adding Another Region to Your Latency\-Based Routing in Amazon Route 53<a name="TutorialAddingLBRRegion"></a>

If you're using latency based routing and you want to add an instance in a new region, you can gradually shift traffic to the new region in the same way that you gradually shifted traffic to latency\-based routing in [Transitioning to Latency\-Based Routing in Amazon Route 53](TutorialTransitionToLBR.md)\. 

For example, suppose you're using latency\-based routing to route traffic for `www.example.com`, and you want to add an Amazon EC2 instance in Asia Pacific \(Tokyo\) to your instances in US East \(Ohio\), US West \(N\. California\), and EU \(Ireland\)\. The following example procedure explains one way that you could add an instance in another region\.

For this example, the Amazon Route 53 hosted zone for `example.com` already has a weighted alias resource record set for `www.example.com` that is routing traffic to the latency\-based resource record sets for `www-lbr.example.com`:

+ US East \(Ohio\), Elastic IP address `W.W.W.W`

+ US West \(N\. California\), Elastic IP address `X.X.X.X`

+ EU \(Ireland\), Elastic IP address `Y.Y.Y.Y` 

The weighted alias resource record set has a weight of 100\. After you transitioned to latency\-based routing, assume that you deleted the other weighted resource record set that you used for the transition\. 

**To Add Another Region to Your Latency\-Based Routing in Amazon Route 53**

1. Create four new latency\-based resource record sets that include the three original regions as well as the new region to which you want to start routing traffic\.

   + US East \(Ohio\), Elastic IP address `W.W.W.W`

   + US West \(N\. California\), Elastic IP address `X.X.X.X`

   + EU \(Ireland\), Elastic IP address `Y.Y.Y.Y` 

   + Asia Pacific \(Tokyo\), Elastic IP address `Z.Z.Z.Z` 

   Give all of the latency resource record sets the same new domain name, for example, `www-lbr-2012-04-30.example.com`, and the same type, A\.

   When you're finished creating the latency resource record sets, Amazon Route 53 will continue to route traffic using the original weighted alias resource record set \(`www.example.com`\) and latency resource record sets \(`www-lbr.example.com`\)\.

   You can use the `www-lbr-2012-04-30.example.com` resource record sets for validation testing, for example, to ensure that each endpoint can accept requests\.

1. Create a weighted alias resource record set for the new latency resource record sets:

   + For the domain name, specify the name for the existing weighted alias resource record set, `www.example.com`\.

   + For the value of **Alias Target**, specify `www-lbr-2012-04-30.example.com`\.

   + For the value of **Weight**, specify 1\.

   When you finish, Amazon Route 53 will begin to route a tiny fraction of your traffic \(1/101\) to the Amazon EC2 instances for which you created the `www-lbr-2012-04-30.example.com` latency resource record sets in Step 1\. The remainder of the traffic will continue to be routed to the `www-lbr.example.com` latency resource record sets, which do not include the Amazon EC2 instance in the Asia Pacific \(Tokyo\) region\. 

1. As you develop confidence that your endpoints are adequately scaled for the incoming traffic, adjust the weights accordingly\. For example, if you want 10% of your requests to be routed to the latency resource record sets that include the Tokyo region, change the weight for `www-lbr.example.com` from 100 to 90 and the weight for `www-lbr-2012-04-30.example.com` from 1 to 10\.

For more information about creating resource record sets, see [Creating Resource Record Sets by Using the Amazon Route 53 Console](resource-record-sets-creating.md)\.