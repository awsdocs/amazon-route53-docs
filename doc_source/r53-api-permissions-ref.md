# Amazon Route 53 API Permissions: Actions, Resources, and Conditions Reference<a name="r53-api-permissions-ref"></a>

When you set up [Access Control](auth-and-access-control.md#access-control) and write a permissions policy that you can attach to an IAM identity \(identity\-based policies\), you can use the following lists as a reference\. The lists include each Amazon Route 53 API action, the actions that you must grant permissions access to, and the AWS resource that you must grant access to\. You specify the actions in the policy's `Action` field, and you specify the resource value in the policy's `Resource` field\. 

You can use AWS\-wide condition keys in your Route 53 policies to express conditions\. For a complete list of AWS\-wide keys, see [Available Keys](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html#AvailableKeys) in the *IAM User Guide*\. 

**Note**  
To specify an action, use the applicable prefix \(`route53`, `route53domains`, or `route53resolver`\) followed by the API operation name, for example:  
`route53:CreateHostedZone`
`route53domains:RegisterDomain`
`route53resolver:CreateResolverEndpoint`

**Topics**
+ [Required Permissions for Actions on Public Hosted Zones](#required-permissions-public-hosted-zones)
+ [Required Permissions for Actions on Private Hosted Zones](#required-permissions-private-hosted-zones)
+ [Required Permissions for Actions on Reusable Delegation Sets](#required-permissions-reusable-delegation-sets)
+ [Required Permissions for Actions on Records](#required-permissions-resource-record-sets)
+ [Required Permissions for Actions on Traffic Policies](#required-permissions-traffic-policies)
+ [Required Permissions for Actions on Traffic Policy Instances](#required-permissions-traffic-policy-instances)
+ [Required Permissions for Actions on Health Checks](#required-permissions-health-checks)
+ [Required Permissions for Actions on Domain Registrations](#required-permissions-domain-registrations)
+ [Required Permissions for Route 53 Resolver Actions](#required-permissions-resolver)
+ [Required Permissions for Actions to Get Limits for Accounts, Hosted Zones, and Reusable Delegation Sets](#required-permissions-get-limits)
+ [Required Permissions for Actions on Tags for Hosted Zones and Health Checks](#required-permissions-tags-hosted-zones)
+ [Required Permissions for Actions on Tags for Domains](#required-permissions-tags-domains)

## Required Permissions for Actions on Public Hosted Zones<a name="required-permissions-public-hosted-zones"></a><a name="public-hosted-zones-table"></a>

[CreateHostedZone](https://docs.aws.amazon.com/Route53/latest/APIReference/API_CreateHostedZone.html)  
Required Permissions \(API Action\): `route53:CreateHostedZone`  
Resources: `*`

[DeleteHostedZone](https://docs.aws.amazon.com/Route53/latest/APIReference/API_DeleteHostedZone.html)  
Required Permissions \(API Action\): `route53:DeleteHostedZone`  
Resources: `*`

[GetHostedZone](https://docs.aws.amazon.com/Route53/latest/APIReference/API_GetHostedZone.html)  
Required Permissions \(API Action\): `route53:GetHostedZone`  
Resources: `*`

[GetHostedZoneCount](https://docs.aws.amazon.com/Route53/latest/APIReference/API_GetHostedZoneCount.html)  
Required Permissions \(API Action\): `route53:GetHostedZoneCount`  
Resources: `*`

[ListHostedZones](https://docs.aws.amazon.com/Route53/latest/APIReference/API_ListHostedZones.html)  
Required Permissions \(API Action\): `route53:ListHostedZones`  
Resources: `*`

[ListHostedZonesByName](https://docs.aws.amazon.com/Route53/latest/APIReference/API_ListHostedZonesByName.html)  
Required Permissions \(API Action\): `route53:ListHostedZonesByName`  
Resources: `*`

[UpdateHostedZoneComment](https://docs.aws.amazon.com/Route53/latest/APIReference/API_UpdateHostedZoneComment.html)  
Required Permissions \(API Action\): `route53:UpdateHostedZoneComment`  
Resources: `*`

## Required Permissions for Actions on Private Hosted Zones<a name="required-permissions-private-hosted-zones"></a><a name="private-hosted-zones-table"></a>

[CreateHostedZone](https://docs.aws.amazon.com/Route53/latest/APIReference/API_CreateHostedZone.html)  
Required Permissions \(API Action\): `route53:CreateHostedZone`, `ec2:DescribeVpcs`, `ec2:DescribeRegions`  
Resources: `*`, `arn:aws:ec2::optional account id:*`

[DeleteHostedZone](https://docs.aws.amazon.com/Route53/latest/APIReference/API_DeleteHostedZone.html)  
Required Permissions \(API Action\): `route53:DeleteHostedZone`  
Resources: `*`

[AssociateVPCWithHostedZone](https://docs.aws.amazon.com/Route53/latest/APIReference/API_AssociateVPCWithHostedZone.html)  
Required Permissions \(API Action\): `route53:AssociateVPCWithHostedZone`, `ec2:DescribeVpcs`  
Resources: `*`, `arn:aws:ec2::optional account id:*`

[DisassociateVPCFromHostedZone](https://docs.aws.amazon.com/Route53/latest/APIReference/API_DisassociateVPCFromHostedZone.html)  
Required Permissions \(API Action\): `route53:DisassociateVPCFromHostedZone`, `ec2:DescribeVpcs`  
Resources: `*`, `arn:aws:ec2::optional account id:*`

[GetHostedZone](https://docs.aws.amazon.com/Route53/latest/APIReference/API_GetHostedZone.html)  
Required Permissions \(API Action\): `route53:GetHostedZone`  
Resources: `*`

[GetHostedZoneCount](https://docs.aws.amazon.com/Route53/latest/APIReference/API_GetHostedZoneCount.html)  
Required Permissions \(API Action\): `route53:GetHostedZoneCount`  
Resources: `*`

[ListHostedZones](https://docs.aws.amazon.com/Route53/latest/APIReference/API_ListHostedZones.html)  
Required Permissions \(API Action\): `route53:ListHostedZones`  
Resources: `*`

[ListHostedZonesByName](https://docs.aws.amazon.com/Route53/latest/APIReference/API_ListHostedZonesByName.html)  
Required Permissions \(API Action\): `route53:ListHostedZonesByName`  
Resources: `*`

[UpdateHostedZoneComment](https://docs.aws.amazon.com/Route53/latest/APIReference/API_UpdateHostedZoneComment.html)  
Required Permissions \(API Action\): `route53:UpdateHostedZoneComment`  
Resources: `*`

## Required Permissions for Actions on Reusable Delegation Sets<a name="required-permissions-reusable-delegation-sets"></a><a name="reusable-delegation-sets-table"></a>

[CreateReusableDelegationSet](https://docs.aws.amazon.com/Route53/latest/APIReference/API_CreateReusableDelegationSet.html)  
Required Permissions \(API Action\): `route53:CreateReusableDelegationSet`  
Resources: `*`

[DeleteReusableDelegationSet](https://docs.aws.amazon.com/Route53/latest/APIReference/API_DeleteReusableDelegationSet.html)  
Required Permissions \(API Action\): `route53:DeleteReusableDelegationSet`  
Resources: `*`

[GetReusableDelegationSet](https://docs.aws.amazon.com/Route53/latest/APIReference/API_GetReusableDelegationSet.html)  
Required Permissions \(API Action\): `route53:GetReusableDelegationSet`  
Resources: `*`

[ListReusableDelegationSets](https://docs.aws.amazon.com/Route53/latest/APIReference/API_ListReusableDelegationSets.html)  
Required Permissions \(API Action\): `route53:ListReusableDelegationSets`  
Resources: `*`

## Required Permissions for Actions on Records<a name="required-permissions-resource-record-sets"></a><a name="resource-record-sets-table"></a>

[ChangeResourceRecordSets](https://docs.aws.amazon.com/Route53/latest/APIReference/API_ChangeResourceRecordSets.html)  
Required Permissions \(API Action\): `route53:ChangeResourceRecordSets`  
Resources: `arn:aws:route53:::hostedzone/hosted zone ID`

[GetChange](https://docs.aws.amazon.com/Route53/latest/APIReference/API_GetChange.html)  
Required Permissions \(API Action\): `route53:GetChange`  
Resources: `*`

[GetGeoLocation](https://docs.aws.amazon.com/Route53/latest/APIReference/API_GetGeoLocation.html)  
Required Permissions \(API Action\): None  
Resources: None

[ListGeoLocations](https://docs.aws.amazon.com/Route53/latest/APIReference/API_ListGeoLocations.html)  
Required Permissions \(API Action\): None  
Resources: None

[ListResourceRecordSets](https://docs.aws.amazon.com/Route53/latest/APIReference/API_ListResourceRecordSets.html)  
Required Permissions \(API Action\): `route53:ListResourceRecordSets`  
Resources: `arn:aws:route53:::hostedzone/hosted zone ID`

## Required Permissions for Actions on Traffic Policies<a name="required-permissions-traffic-policies"></a><a name="traffic-policies-table"></a>

[CreateTrafficPolicy](https://docs.aws.amazon.com/Route53/latest/APIReference/API_CreateTrafficPolicy.html)  
Required Permissions \(API Action\): `route53:CreateTrafficPolicy`  
Resources: `*`

[CreateTrafficPolicyVersion](https://docs.aws.amazon.com/Route53/latest/APIReference/API_CreateTrafficPolicyVersion.html)  
Required Permissions \(API Action\): `route53:CreateTrafficPolicyVersion`  
Resources: `*`

[DeleteTrafficPolicy](https://docs.aws.amazon.com/Route53/latest/APIReference/API_DeleteTrafficPolicy.html)  
Required Permissions \(API Action\): `route53:DeleteTrafficPolicy`  
Resources: `*`

[GetTrafficPolicy](https://docs.aws.amazon.com/Route53/latest/APIReference/API_GetTrafficPolicy.html)  
Required Permissions \(API Action\): `route53:GetTrafficPolicy`  
Resources: `*`

[ListTrafficPolicies](https://docs.aws.amazon.com/Route53/latest/APIReference/API_ListTrafficPolicies.html)  
Required Permissions \(API Action\): `route53:ListTrafficPolicies`  
Resources: `*`

[ListTrafficPolicyVersions](https://docs.aws.amazon.com/Route53/latest/APIReference/API_ListTrafficPolicyVersions.html)  
Required Permissions \(API Action\): `route53:ListTrafficPolicyVersions`  
Resources: `*`

[UpdateTrafficPolicyComment](https://docs.aws.amazon.com/Route53/latest/APIReference/API_UpdateTrafficPolicyComment.html)  
Required Permissions \(API Action\): `route53:UpdateTrafficPolicyComment`  
Resources: `*`

## Required Permissions for Actions on Traffic Policy Instances<a name="required-permissions-traffic-policy-instances"></a><a name="traffic-policy-instances-table"></a>

[CreateTrafficPolicyInstance](https://docs.aws.amazon.com/Route53/latest/APIReference/API_CreateTrafficPolicyInstance.html)  
Required Permissions \(API Action\): `route53:CreateTrafficPolicyInstance`  
Resources: `*`

[DeleteTrafficPolicyInstance](https://docs.aws.amazon.com/Route53/latest/APIReference/API_DeleteTrafficPolicyInstance.html)  
Required Permissions \(API Action\): `route53:DeleteTrafficPolicyInstance`  
Resources: `*`

[GetTrafficPolicyInstance](https://docs.aws.amazon.com/Route53/latest/APIReference/API_GetTrafficPolicyInstance.html)  
Required Permissions \(API Action\): `route53:GetTrafficPolicyInstance`  
Resources: `*`

[GetTrafficPolicyInstanceCount](https://docs.aws.amazon.com/Route53/latest/APIReference/API_GetTrafficPolicyInstanceCount.html)  
Required Permissions \(API Action\): `route53:GetTrafficPolicyInstanceCount`  
Resources: `*`

[ListTrafficPolicyInstances](https://docs.aws.amazon.com/Route53/latest/APIReference/API_ListTrafficPolicyInstances.html)  
Required Permissions \(API Action\): `route53:ListTrafficPolicyInstances`  
Resources: `*`

[ListTrafficPolicyInstancesByHostedZone](https://docs.aws.amazon.com/Route53/latest/APIReference/API_ListTrafficPolicyInstancesByHostedZone.html)  
Required Permissions \(API Action\): `route53:ListTrafficPolicyInstancesByHostedZone`  
Resources: `*`

[ListTrafficPolicyInstancesByPolicy](https://docs.aws.amazon.com/Route53/latest/APIReference/API_ListTrafficPolicyInstancesByPolicy.html)  
Required Permissions \(API Action\): `route53:ListTrafficPolicyInstancesByPolicy`  
Resources: `*`

[UpdateTrafficPolicyInstance](https://docs.aws.amazon.com/Route53/latest/APIReference/API_UpdateTrafficPolicyInstance.html)  
Required Permissions \(API Action\): `route53:UpdateTrafficPolicyInstance`  
Resources: `*`

## Required Permissions for Actions on Health Checks<a name="required-permissions-health-checks"></a><a name="health-checks-table"></a>

[CreateHealthCheck](https://docs.aws.amazon.com/Route53/latest/APIReference/API_CreateHealthCheck.html)  
Required Permissions \(API Action\): `route53:CreateHealthCheck`  
Resources: `*`, `arn:aws:route53:::healthcheck/`

[DeleteHealthCheck](https://docs.aws.amazon.com/Route53/latest/APIReference/API_DeleteHealthCheck.html)  
Required Permissions \(API Action\): `route53:DeleteHealthCheck`  
Resources: `*`, `arn:aws:route53:::healthcheck/health check ID`

[GetCheckerIpRanges](https://docs.aws.amazon.com/Route53/latest/APIReference/API_GetCheckerIpRanges.html)  
Required Permissions \(API Action\): `route53:GetCheckerIpRanges`  
Resources: `*`

[GetHealthCheck](https://docs.aws.amazon.com/Route53/latest/APIReference/API_GetHealthCheck.html)  
Required Permissions \(API Action\): `route53:GetHealthCheck`  
Resources: `*`, `arn:aws:route53:::healthcheck/health check ID`

[GetHealthCheckCount](https://docs.aws.amazon.com/Route53/latest/APIReference/API_GetHealthCheckCount.html)  
Required Permissions \(API Action\): `route53:GetHealthCheckCount`  
Resources: `*`

[GetHealthCheckLastFailureReason](https://docs.aws.amazon.com/Route53/latest/APIReference/API_GetHealthCheckLastFailureReason.html)  
Required Permissions \(API Action\): `route53:GetHealthCheckLastFailureReason`  
Resources: `*`, `arn:aws:route53:::healthcheck/health check ID`

[GetHealthCheckStatus](https://docs.aws.amazon.com/Route53/latest/APIReference/API_GetHealthCheckStatus.html)  
Required Permissions \(API Action\): `route53:GetHealthCheckStatus`  
Resources: `*`, `arn:aws:route53:::healthcheck/health check ID`

[ListHealthChecks](https://docs.aws.amazon.com/Route53/latest/APIReference/API_ListHealthChecks.html)  
Required Permissions \(API Action\): `route53:ListHealthChecks`  
Resources: `*`

[UpdateHealthCheck](https://docs.aws.amazon.com/Route53/latest/APIReference/API_UpdateHealthCheck.html)  
Required Permissions \(API Action\): `route53:UpdateHealthCheck`  
Resources: `*`, `arn:aws:route53:::healthcheck/health check ID`

## Required Permissions for Actions on Domain Registrations<a name="required-permissions-domain-registrations"></a><a name="domain-registrations-table"></a>

[AddDnssec](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/domain-configure-dnssec.html) \(console only\)  
Required Permissions \(API Action\): `route53domains:AddDnssec`  
Resources: `*`

[CheckDomainAvailability](https://docs.aws.amazon.com/Route53/latest/APIReference/API_domains_CheckDomainAvailability.html)  
Required Permissions \(API Action\): `route53domains:CheckDomainAvailability`  
Resources: `*`

[DeleteDomain](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/domain-delete.html) \(console only\)  
Required Permissions \(API Action\): `route53domains:DeleteDomain`  
Resources: `*`

[DisableDomainAutoRenew](https://docs.aws.amazon.com/Route53/latest/APIReference/API_domains_DisableDomainAutoRenew.html)  
Required Permissions \(API Action\): `route53domains:ChangeAutoRenew`  
Resources: `*`

[DisableDomainTransferLock](https://docs.aws.amazon.com/Route53/latest/APIReference/API_domains_DisableDomainTransferLock.html)  
Required Permissions \(API Action\): `route53domains:DisableDomainTransferLock`  
Resources: `*`

[EnableDomainAutoRenew](https://docs.aws.amazon.com/Route53/latest/APIReference/API_domains_EnableDomainAutoRenew.html)  
Required Permissions \(API Action\): `route53domains:ChangeAutoRenew`  
Resources: `*`

[EnableDomainTransferLock](https://docs.aws.amazon.com/Route53/latest/APIReference/API_domains_EnableDomainTransferLock.html)  
Required Permissions \(API Action\): `route53domains:EnableDomainTransferLock`  
Resources: `*`

[GetContactReachabilityStatus](https://docs.aws.amazon.com/Route53/latest/APIReference/API_domains_GetContactReachabilityStatus.html)  
Required Permissions \(API Action\): `route53domains:ListDomains`  
Resources: `*`

[GetDomainDetail](https://docs.aws.amazon.com/Route53/latest/APIReference/API_domains_GetDomainDetail.html)  
Required Permissions \(API Action\): `route53domains:GetDomainDetail`  
Resources: `*`

[GetDomainSuggestions](https://docs.aws.amazon.com/Route53/latest/APIReference/API_domains_GetDomainSuggestions.html)  
Required Permissions \(API Action\): `route53domains:ListDomains`  
Resources: `*`

[GetOperationDetail](https://docs.aws.amazon.com/Route53/latest/APIReference/API_domains_GetOperationDetail.html)  
Required Permissions \(API Action\): `route53domains:GetOperationDetail`  
Resources: `*`

[ListDnssec](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/domain-configure-dnssec.html) \(console only\)  
Required Permissions \(API Action\): `route53domains:ListDnssec`  
Resources: `*`

[ListDomains](https://docs.aws.amazon.com/Route53/latest/APIReference/API_domains_ListDomains.html)  
Required Permissions \(API Action\): `route53domains:ListDomains`  
Resources: `*`

[ListOperations](https://docs.aws.amazon.com/Route53/latest/APIReference/API_domains_ListOperations.html)  
Required Permissions \(API Action\): `route53domains:ListOperations`  
Resources: `*`

[RegisterDomain](https://docs.aws.amazon.com/Route53/latest/APIReference/API_domains_RegisterDomain.html)  
Required Permissions \(API Action\): `route53domains:RegisterDomain`  
Resources: `*`

[RemoveDnssec](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/domain-configure-dnssec.html) \(console only\)  
Required Permissions \(API Action\): `route53domains:RemoveDnssec`  
Resources: `*`

[RenewDomain](https://docs.aws.amazon.com/Route53/latest/APIReference/API_domains_RenewDomain.html)  
Required Permissions \(API Action\): `route53domains:RegisterDomain`  
Resources: `*`

[ResendContactReachabilityEmail](https://docs.aws.amazon.com/Route53/latest/APIReference/API_domains_ResendContactReachabilityEmail.html)  
Required Permissions \(API Action\): `route53domains:ListDomains`  
Resources: `*`

[RetrieveDomainAuthCode](https://docs.aws.amazon.com/Route53/latest/APIReference/API_domains_RetrieveDomainAuthCode.html)  
Required Permissions \(API Action\): `route53domains:RetrieveDomainAuthCode`  
Resources: `*`

[TransferDomain](https://docs.aws.amazon.com/Route53/latest/APIReference/API_domains_TransferDomain.html)  
Required Permissions \(API Action\): `route53domains:TransferDomain`  
Resources: `*`

[UpdateDomainContact](https://docs.aws.amazon.com/Route53/latest/APIReference/API_domains_UpdateDomainContact.html)  
Required Permissions \(API Action\): `route53domains:UpdateDomainContact`  
Resources: `*`

[UpdateDomainContactPrivacy](https://docs.aws.amazon.com/Route53/latest/APIReference/API_domains_UpdateDomainContactPrivacy.html)  
Required Permissions \(API Action\): `route53domains:UpdateDomainContactPrivacy`  
Resources: `*`

[UpdateDomainNameservers](https://docs.aws.amazon.com/Route53/latest/APIReference/API_domains_UpdateDomainNameservers.html)  
Required Permissions \(API Action\): `route53domains:UpdateDomainNameservers`  
Resources: `*`

[ViewBilling](https://docs.aws.amazon.com/Route53/latest/APIReference/API_domains_ViewBilling.html)  
Required Permissions \(API Action\): `route53domains:ViewBilling`  
Resources: `*`

## Required Permissions for Route 53 Resolver Actions<a name="required-permissions-resolver"></a><a name="resolver-table"></a>

[AssociateResolverEndpointIpAddress](https://docs.aws.amazon.com/Route53/latest/APIReference/API_route53resolver_AssociateResolverEndpointIpAddress.html)  
Required Permissions \(API Action\): `route53resolver:AssociateResolverEndpointIpAddress`, `ec2:DescribeSubnets`, `ec2:DescribeNetworkInterfaces`, `ec2:CreateNetworkInterfacePermission`  
Resources: `*`

[AssociateResolverRule](https://docs.aws.amazon.com/Route53/latest/APIReference/API_route53resolver_AssociateResolverRule.html)  
Required Permissions \(API Action\): `route53resolver:AssociateResolverRule`, `ec2:DescribeVpcs`  
Resources: `*`

[CreateResolverEndpoint](https://docs.aws.amazon.com/Route53/latest/APIReference/API_route53resolver_CreateResolverEndpoint.html)  
Required Permissions \(API Action\): `route53resolver:CreateResolverEndpoint`, `ec2:DescribeSubnets`, `ec2:CreateNetworkInterface`, `ec2:DescribeNetworkInterfaces`, `ec2:CreateNetworkInterfacePermission`, `ec2:DescribeSecurityGroups`  
Resources: `*`

[CreateResolverRule](https://docs.aws.amazon.com/Route53/latest/APIReference/API_route53resolver_CreateResolverRule.html)  
Required Permissions \(API Action\): `route53resolver:CreateResolverRule`  
Resources: `*`

[DeleteResolverEndpoint](https://docs.aws.amazon.com/Route53/latest/APIReference/API_route53resolver_DeleteResolverEndpoint.html)  
Required Permissions \(API Action\): `route53resolver:DeleteResolverEndpoint`, `ec2:DeleteNetworkInterface`  
Resources: `*`

[DeleteResolverRule](https://docs.aws.amazon.com/Route53/latest/APIReference/API_route53resolver_DeleteResolverRule.html)  
Required Permissions \(API Action\): `route53resolver:DeleteResolverRule`  
Resources: `*`

[DisassociateResolverEndpointIpAddress](https://docs.aws.amazon.com/Route53/latest/APIReference/API_route53resolver_DisassociateResolverEndpointIpAddress.html)  
Required Permissions \(API Action\): `route53resolver:DisassociateResolverEndpointIpAddress`, `ec2:DeleteNetworkInterface`  
Resources: `*`

[DisassociateResolverRule](https://docs.aws.amazon.com/Route53/latest/APIReference/API_route53resolver_DisassociateResolverRule.html)  
Required Permissions \(API Action\): `route53resolver:DisassociateResolverRule`  
Resources: `*`

[GetResolverEndpoint](https://docs.aws.amazon.com/Route53/latest/APIReference/API_route53resolver_GetResolverEndpoint.html)  
Required Permissions \(API Action\): `route53resolver:GetResolverEndpoint`  
Resources: `*`

[GetResolverRule](https://docs.aws.amazon.com/Route53/latest/APIReference/API_route53resolver_GetResolverRule.html)  
Required Permissions \(API Action\): `route53resolver:GetResolverRule`  
Resources: `*`

[GetResolverRuleAssociation](https://docs.aws.amazon.com/Route53/latest/APIReference/API_route53resolver_GetResolverRuleAssociation.html)  
Required Permissions \(API Action\): `route53resolver:GetResolverRuleAssociation`, `ec2:DescribeVpcs`  
Resources: `*`

[GetResolverRulePolicy](https://docs.aws.amazon.com/Route53/latest/APIReference/API_route53resolver_GetResolverRulePolicy.html)  
Required Permissions \(API Action\): `route53resolver:GetResolverRulePolicy`  
Resources: `*`

[ListResolverEndpointIpAddresses](https://docs.aws.amazon.com/Route53/latest/APIReference/API_route53resolver_ListResolverEndpointIpAddresses.html)  
Required Permissions \(API Action\): `route53resolver:ListResolverEndpointIpAddresses`  
Resources: `*`

[ListResolverEndpoints](https://docs.aws.amazon.com/Route53/latest/APIReference/API_route53resolver_ListResolverEndpoints.html)  
Required Permissions \(API Action\): `route53resolver:ListResolverEndpoints`  
Resources: `*`

[ListResolverRuleAssociations](https://docs.aws.amazon.com/Route53/latest/APIReference/API_route53resolver_ListResolverRuleAssociations.html)  
Required Permissions \(API Action\): `route53resolver:ListResolverRuleAssociations`, `ec2:DescribeVpcs`  
Resources: `*`

[ListResolverRules](https://docs.aws.amazon.com/Route53/latest/APIReference/API_route53resolver_ListResolverRules.html)  
Required Permissions \(API Action\): `route53resolver:ListResolverRules`  
Resources: `*`

[ListTagsForResource](https://docs.aws.amazon.com/Route53/latest/APIReference/API_route53resolver_ListTagsForResource.html)  
Required Permissions \(API Action\): `route53resolver:ListTagsForResource`  
Resources: `arn:aws:route53resolver:::resolver-endpoint/*`, `arn:aws:route53resolver:::resolver-rule/`

[PutResolverRulePolicy](https://docs.aws.amazon.com/Route53/latest/APIReference/API_route53resolver_PutResolverRulePolicy.html)  
Required Permissions \(API Action\): `route53resolver:PutResolverRulePolicy`  
Resources: `*`

[TagResource](https://docs.aws.amazon.com/Route53/latest/APIReference/API_route53resolver_TagResource.html)  
Required Permissions \(API Action\): `route53resolver:TagResource`  
Resources: `arn:aws:route53resolver:::resolver-endpoint/*`, `arn:aws:route53resolver:::resolver-rule/*`

[UntagResource](https://docs.aws.amazon.com/Route53/latest/APIReference/API_route53resolver_UntagResource.html)  
Required Permissions \(API Action\): `route53resolver:UntagResource`  
Resources: `arn:aws:route53resolver:::resolver-endpoint/*`, `arn:aws:route53resolver:::resolver-rule/*`

[UpdateResolverEndpoint](https://docs.aws.amazon.com/Route53/latest/APIReference/API_route53resolver_UpdateResolverEndpoint.html)  
Required Permissions \(API Action\): `route53resolver:UpdateResolverEndpoint`  
Resources: `*`

[UpdateResolverRule](https://docs.aws.amazon.com/Route53/latest/APIReference/API_route53resolver_UpdateResolverRule.html)  
Required Permissions \(API Action\): `route53resolver:UpdateResolverRule`  
Resources: `*`

## Required Permissions for Actions to Get Limits for Accounts, Hosted Zones, and Reusable Delegation Sets<a name="required-permissions-get-limits"></a><a name="tags-hosted-zones-table"></a>

[GetAccountLimit](https://docs.aws.amazon.com/Route53/latest/APIReference/API_GetAccountLimit.html)  
Required Permissions \(API Action\): `route53:GetAccountLimit`  
Resources: `*`

[GetHostedZoneLimit](https://docs.aws.amazon.com/Route53/latest/APIReference/API_GetHostedZoneLimit.html)  
Required Permissions \(API Action\): `route53:GetHostedZoneLimit`  
Resources: `*`

[GetReusableDelegationSetLimit](https://docs.aws.amazon.com/Route53/latest/APIReference/API_GetReusableDelegationSetLimit.html)  
Required Permissions \(API Action\): `route53:GetReusableDelegationSetLimit`  
Resources: `*`

## Required Permissions for Actions on Tags for Hosted Zones and Health Checks<a name="required-permissions-tags-hosted-zones"></a><a name="tags-hosted-zones-table"></a>

[ChangeTagsForResource](https://docs.aws.amazon.com/Route53/latest/APIReference/API_ChangeTagsForResource.html)  
Required Permissions \(API Action\): `route53:ChangeTagsForResource`  
Resources:  
+ `arn:aws:route53:::healthcheck/*`
+ `arn:aws:route53:::hostedzone/*`

[ListTagsForResource](https://docs.aws.amazon.com/Route53/latest/APIReference/API_ListTagsForResource.html)  
Required Permissions \(API Action\): `route53:ListTagsForResource`  
Resources:  
+ `arn:aws:route53:::healthcheck/*`
+ `arn:aws:route53:::hostedzone/*`

[ListTagsForResources](https://docs.aws.amazon.com/Route53/latest/APIReference/API_ListTagsForResources.html)  
Required Permissions \(API Action\): `route53:ListTagsForResources`  
Resources:  
+ `arn:aws:route53:::healthcheck/*`
+ `arn:aws:route53:::hostedzone/*`

## Required Permissions for Actions on Tags for Domains<a name="required-permissions-tags-domains"></a><a name="tags-domains-table"></a>

[DeleteTagsForDomain](https://docs.aws.amazon.com/Route53/latest/APIReference/API_domains_DeleteTagsForDomain.html)  
Required Permissions \(API Action\): `route53domains:DeleteTagsForDomain`  
Resources: `*`

[ListTagsForDomain](https://docs.aws.amazon.com/Route53/latest/APIReference/API_domains_ListTagsForDomain.html)  
Required Permissions \(API Action\): `route53domains:ListTagsForDomain`  
Resources: `*`

[UpdateTagsForDomain](https://docs.aws.amazon.com/Route53/latest/APIReference/API_domains_UpdateTagsForDomain.html)  
Required Permissions \(API Action\): `route53domains:UpdateTagsForDomain`  
Resources: `*`
