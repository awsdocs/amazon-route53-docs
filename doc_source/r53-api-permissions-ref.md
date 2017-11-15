# Amazon Route 53 API Permissions: Actions, Resources, and Conditions Reference<a name="r53-api-permissions-ref"></a>

When you are setting up [Access Control](auth-and-access-control.md#access-control) and writing a permissions policy that you can attach to an IAM identity \(identity\-based policies\), you can use the following as a reference\. The each Amazon Route 53 API operation, the corresponding actions for which you can grant permissions to perform the action, and the AWS resource for which you can grant the permissions\. You specify the actions in the policy's `Action` field, and you specify the resource value in the policy's `Resource` field\. 

You can use AWS wide condition keys in your Amazon Route 53 policies to express conditions\. For a complete list of AWS wide keys, see [Available Keys](http://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html#AvailableKeys) in the *IAM User Guide*\. 

**Note**  
To specify an action, use the applicable prefix \(`route53:` or `route53domains`\) followed by the API operation name \(for example, `route53:CreateHostedZone` or `route53domains:RegisterDomain`\)\.


+ [Required Permissions for Actions on Public Hosted Zones](#required-permissions-public-hosted-zones)
+ [Required Permissions for Actions on Private Hosted Zones](#required-permissions-private-hosted-zones)
+ [Required Permissions for Actions on Reusable Delegation Sets](#required-permissions-reusable-delegation-sets)
+ [Required Permissions for Actions on Resource Record Sets](#required-permissions-resource-record-sets)
+ [Required Permissions for Actions on Traffic Policies](#required-permissions-traffic-policies)
+ [Required Permissions for Actions on Traffic Policy Instances](#required-permissions-traffic-policy-instances)
+ [Required Permissions for Actions on Health Checks](#required-permissions-health-checks)
+ [Required Permissions for Actions on Domain Registrations](#required-permissions-domain-registrations)
+ [Required Permissions for Actions on Tags for Hosted Zones and Health Checks](#required-permissions-tags-hosted-zones)
+ [Required Permissions for Actions on Tags for Domains](#required-permissions-tags-domains)

## Required Permissions for Actions on Public Hosted Zones<a name="required-permissions-public-hosted-zones"></a>

[CreateHostedZone](http://docs.aws.amazon.com/Route53/latest/APIReference/API_CreateHostedZone.html)  
Required Permissions \(API Action\): `route53:CreateHostedZone`  
Resources: `*`

[DeleteHostedZone](http://docs.aws.amazon.com/Route53/latest/APIReference/API_DeleteHostedZone.html)  
Required Permissions \(API Action\): `route53:DeleteHostedZone`  
Resources: `*`

[GetHostedZone](http://docs.aws.amazon.com/Route53/latest/APIReference/API_GetHostedZone.html)  
Required Permissions \(API Action\): `route53:GetHostedZone`  
Resources: `*`

[GetHostedZoneCount](http://docs.aws.amazon.com/Route53/latest/APIReference/API_GetHostedZoneCount.html)  
Required Permissions \(API Action\): `route53:GetHostedZoneCount`  
Resources: `*`

[ListHostedZones](http://docs.aws.amazon.com/Route53/latest/APIReference/API_ListHostedZones.html)  
Required Permissions \(API Action\): `route53:ListHostedZones`  
Resources: `*`

[ListHostedZonesByName](http://docs.aws.amazon.com/Route53/latest/APIReference/API_ListHostedZonesByName.html)  
Required Permissions \(API Action\): `route53:ListHostedZonesByName`  
Resources: `*`

[UpdateHostedZoneComment](http://docs.aws.amazon.com/Route53/latest/APIReference/API_UpdateHostedZoneComment.html)  
Required Permissions \(API Action\): `route53:UpdateHostedZoneComment`  
Resources: `*`

## Required Permissions for Actions on Private Hosted Zones<a name="required-permissions-private-hosted-zones"></a>

[CreateHostedZone](http://docs.aws.amazon.com/Route53/latest/APIReference/API_CreateHostedZone.html)  
Required Permissions \(API Action\): `route53:CreateHostedZone`, `ec2:DescribeVpcs`, `ec2:DescribeRegions`  
Resources: `*`, `arn:aws:ec2::optional account id:*`

[DeleteHostedZone](http://docs.aws.amazon.com/Route53/latest/APIReference/API_DeleteHostedZone.html)  
Required Permissions \(API Action\): `route53:DeleteHostedZone`  
Resources: `*`

[AssociateVPCWithHostedZone](http://docs.aws.amazon.com/Route53/latest/APIReference/API_AssociateVPCWithHostedZone.html)  
Required Permissions \(API Action\): `route53:AssociateVPCWithHostedZone`, `ec2:DescribeVpcs`  
Resources: `*`, `arn:aws:ec2::optional account id:*`

[DisassociateVPCFromHostedZone](http://docs.aws.amazon.com/Route53/latest/APIReference/API_DisassociateVPCFromHostedZone.html)  
Required Permissions \(API Action\): `route53:DisassociateVPCFromHostedZone`, `ec2:DescribeVpcs`  
Resources: `*`, `arn:aws:ec2::optional account id:*`

[GetHostedZone](http://docs.aws.amazon.com/Route53/latest/APIReference/API_GetHostedZone.html)  
Required Permissions \(API Action\): `route53:GetHostedZone`  
Resources: `*`

[GetHostedZoneCount](http://docs.aws.amazon.com/Route53/latest/APIReference/API_GetHostedZoneCount.html)  
Required Permissions \(API Action\): `route53:GetHostedZoneCount`  
Resources: `*`

[ListHostedZones](http://docs.aws.amazon.com/Route53/latest/APIReference/API_ListHostedZones.html)  
Required Permissions \(API Action\): `route53:ListHostedZones`  
Resources: `*`

[ListHostedZonesByName](http://docs.aws.amazon.com/Route53/latest/APIReference/API_ListHostedZonesByName.html)  
Required Permissions \(API Action\): `route53:ListHostedZonesByName`  
Resources: `*`

[UpdateHostedZoneComment](http://docs.aws.amazon.com/Route53/latest/APIReference/API_UpdateHostedZoneComment.html)  
Required Permissions \(API Action\): `route53:UpdateHostedZoneComment`  
Resources: `*`

## Required Permissions for Actions on Reusable Delegation Sets<a name="required-permissions-reusable-delegation-sets"></a>

[CreateReusableDelegationSet](http://docs.aws.amazon.com/Route53/latest/APIReference/API_CreateReusableDelegationSet.html)  
Required Permissions \(API Action\): `route53:CreateReusableDelegationSet`  
Resources: `*`

[DeleteReusableDelegationSet](http://docs.aws.amazon.com/Route53/latest/APIReference/API_DeleteReusableDelegationSet.html)  
Required Permissions \(API Action\): `route53:DeleteReusableDelegationSet`  
Resources: `*`

[GetReusableDelegationSet](http://docs.aws.amazon.com/Route53/latest/APIReference/API_GetReusableDelegationSet.html)  
Required Permissions \(API Action\): `route53:GetReusableDelegationSet`  
Resources: `*`

[ListReusableDelegationSets](http://docs.aws.amazon.com/Route53/latest/APIReference/API_ListReusableDelegationSets.html)  
Required Permissions \(API Action\): `route53:ListReusableDelegationSets`  
Resources: `*`

## Required Permissions for Actions on Resource Record Sets<a name="required-permissions-resource-record-sets"></a>

[ChangeResourceRecordSets](http://docs.aws.amazon.com/Route53/latest/APIReference/API_ChangeResourceRecordSets.html)  
Required Permissions \(API Action\): `route53:ChangeResourceRecordSets`  
Resources: `arn:aws:route53:::hostedzone/hosted zone ID/rrset`

[GetChange](http://docs.aws.amazon.com/Route53/latest/APIReference/API_GetChange.html)  
Required Permissions \(API Action\): `route53:GetChange`  
Resources: `*`

[GetGeoLocation](http://docs.aws.amazon.com/Route53/latest/APIReference/API_GetGeoLocation.html)  
Required Permissions \(API Action\): None  
Resources: None

[ListGeoLocations](http://docs.aws.amazon.com/Route53/latest/APIReference/API_ListGeoLocations.html)  
Required Permissions \(API Action\): None  
Resources: None

[ListResourceRecordSets](http://docs.aws.amazon.com/Route53/latest/APIReference/API_ListResourceRecordSets.html)  
Required Permissions \(API Action\): `route53:ListResourceRecordSets`  
Resources: `*`

## Required Permissions for Actions on Traffic Policies<a name="required-permissions-traffic-policies"></a>

[CreateTrafficPolicy](http://docs.aws.amazon.com/Route53/latest/APIReference/API_CreateTrafficPolicy.html)  
Required Permissions \(API Action\): `route53:CreateTrafficPolicy`  
Resources: `*`

[CreateTrafficPolicyVersion](http://docs.aws.amazon.com/Route53/latest/APIReference/API_CreateTrafficPolicyVersion.html)  
Required Permissions \(API Action\): `route53:CreateTrafficPolicyVersion`  
Resources: `*`

[DeleteTrafficPolicy](http://docs.aws.amazon.com/Route53/latest/APIReference/API_DeleteTrafficPolicy.html)  
Required Permissions \(API Action\): `route53:DeleteTrafficPolicy`  
Resources: `*`

[GetTrafficPolicy](http://docs.aws.amazon.com/Route53/latest/APIReference/API_GetTrafficPolicy.html)  
Required Permissions \(API Action\): `route53:GetTrafficPolicy`  
Resources: `*`

[ListTrafficPolicies](http://docs.aws.amazon.com/Route53/latest/APIReference/API_ListTrafficPolicyPolicies.html)  
Required Permissions \(API Action\): `route53:ListTrafficPolicies`  
Resources: `*`

[ListTrafficPolicyVersions](http://docs.aws.amazon.com/Route53/latest/APIReference/API_ListTrafficPolicyVersions.html)  
Required Permissions \(API Action\): `route53:ListTrafficPolicyVersions`  
Resources: `*`

[UpdateTrafficPolicyComment](http://docs.aws.amazon.com/Route53/latest/APIReference/API_UpdateTrafficPolicyComment.html)  
Required Permissions \(API Action\): `route53:UpdateTrafficPolicyComment`  
Resources: `*`

## Required Permissions for Actions on Traffic Policy Instances<a name="required-permissions-traffic-policy-instances"></a>

[CreateTrafficPolicyInstance](http://docs.aws.amazon.com/Route53/latest/APIReference/API_CreateTrafficPolicyInstance.html)  
Required Permissions \(API Action\): `route53:CreateTrafficPolicyInstance`  
Resources: `*`

[DeleteTrafficPolicyInstance](http://docs.aws.amazon.com/Route53/latest/APIReference/API_DeleteTrafficPolicyInstance.html)  
Required Permissions \(API Action\): `route53:DeleteTrafficPolicyInstance`  
Resources: `*`

[GetTrafficPolicyInstance](http://docs.aws.amazon.com/Route53/latest/APIReference/API_GetTrafficPolicyInstance.html)  
Required Permissions \(API Action\): `route53:GetTrafficPolicyInstance`  
Resources: `*`

[GetTrafficPolicyInstanceCount](http://docs.aws.amazon.com/Route53/latest/APIReference/API_GetTrafficPolicyInstanceCount.html)  
Required Permissions \(API Action\): `route53:GetTrafficPolicyInstanceCount`  
Resources: `*`

[ListTrafficPolicyInstances](http://docs.aws.amazon.com/Route53/latest/APIReference/API_ListTrafficPolicyInstances.html)  
Required Permissions \(API Action\): `route53:ListTrafficPolicyInstances`  
Resources: `*`

[ListTrafficPolicyInstancesByHostedZone](http://docs.aws.amazon.com/Route53/latest/APIReference/API_ListTrafficPolicyInstancesByHostedZone.html)  
Required Permissions \(API Action\): `route53:ListTrafficPolicyInstancesByHostedZone`  
Resources: `*`

[ListTrafficPolicyInstancesByPolicy](http://docs.aws.amazon.com/Route53/latest/APIReference/API_ListTrafficPolicyInstancesByPolicy.html)  
Required Permissions \(API Action\): `route53:ListTrafficPolicyInstancesByPolicy`  
Resources: `*`

[UpdateTrafficPolicyInstance](http://docs.aws.amazon.com/Route53/latest/APIReference/API_UpdateTrafficPolicyInstance.html)  
Required Permissions \(API Action\): `route53:UpdateTrafficPolicyInstance`  
Resources: `*`

## Required Permissions for Actions on Health Checks<a name="required-permissions-health-checks"></a>

[CreateHealthCheck](http://docs.aws.amazon.com/Route53/latest/APIReference/API_CreateHealthCheck.html)  
Required Permissions \(API Action\): `route53:CreateHealthCheck`  
Resources: `*`

[DeleteHealthCheck](http://docs.aws.amazon.com/Route53/latest/APIReference/API_DeleteHealthCheck.html)  
Required Permissions \(API Action\): `route53:DeleteHealthCheck`  
Resources: `*`

[GetCheckerIpRanges](http://docs.aws.amazon.com/Route53/latest/APIReference/API_GetCheckerIpRanges.html)  
Required Permissions \(API Action\): `route53:GetCheckerIpRanges`  
Resources: `*`

[GetHealthCheck](http://docs.aws.amazon.com/Route53/latest/APIReference/API_GetHealthCheck.html)  
Required Permissions \(API Action\): `route53:GetHealthCheck`  
Resources: `*`

[GetHealthCheckCount](http://docs.aws.amazon.com/Route53/latest/APIReference/API_GetHealthCheckCount.html)  
Required Permissions \(API Action\): `route53:GetHealthCheckCount`  
Resources: `*`

[GetHealthCheckLastFailureReason](http://docs.aws.amazon.com/Route53/latest/APIReference/API_GetHealthCheckLastFailureReason.html)  
Required Permissions \(API Action\): `route53:GetHealthCheckLastFailureReason`  
Resources: `*`

[GetHealthCheckStatus](http://docs.aws.amazon.com/Route53/latest/APIReference/API_GetHealthCheckStatus.html)  
Required Permissions \(API Action\): `route53:GetHealthCheckStatus`  
Resources: `*`

[ListHealthChecks](http://docs.aws.amazon.com/Route53/latest/APIReference/API_ListHealthChecks.html)  
Required Permissions \(API Action\): `route53:ListHealthChecks`  
Resources: `*`

[UpdateHealthCheck](http://docs.aws.amazon.com/Route53/latest/APIReference/API_UpdateHealthCheck.html)  
Required Permissions \(API Action\): `route53:UpdateHealthCheck`  
Resources: `*`

## Required Permissions for Actions on Domain Registrations<a name="required-permissions-domain-registrations"></a>

[AddDnssec](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/domain-configure-dnssec.html) \(console only\)  
Required Permissions \(API Action\): `route53domains:AddDnssec`  
Resources: `*`

[CheckDomainAvailability](http://docs.aws.amazon.com/Route53/latest/APIReference/API_CheckDomainAvailability.html)  
Required Permissions \(API Action\): `route53domains:CheckDomainAvailability`  
Resources: `*`

[DeleteDomain](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/domain-delete.html) \(console only\)  
Required Permissions \(API Action\): `route53domains:DeleteDomain`  
Resources: `*`

[DisableDomainAutoRenew](http://docs.aws.amazon.com/Route53/latest/APIReference/API_DisableDomainAutoRenew.html)  
Required Permissions \(API Action\): `route53domains:ChangeAutoRenew`  
Resources: `*`

[DisableDomainTransferLock](http://docs.aws.amazon.com/Route53/latest/APIReference/API_DisableDomainTransferLock.html)  
Required Permissions \(API Action\): `route53domains:DisableDomainTransferLock`  
Resources: `*`

[EnableDomainAutoRenew](http://docs.aws.amazon.com/Route53/latest/APIReference/API_EnableDomainAutoRenew.html)  
Required Permissions \(API Action\): `route53domains:ChangeAutoRenew`  
Resources: `*`

[EnableDomainTransferLock](http://docs.aws.amazon.com/Route53/latest/APIReference/API_EnableDomainTransferLock.html)  
Required Permissions \(API Action\): `route53domains:EnableDomainTransferLock`  
Resources: `*`

[GetContactReachabilityStatus](http://docs.aws.amazon.com/Route53/latest/APIReference/API_GetContactReachabilityStatus.html)  
Required Permissions \(API Action\): `route53domains:ListDomains`  
Resources: `*`

[GetDomainDetail](http://docs.aws.amazon.com/Route53/latest/APIReference/API_GetDomainDetail.html)  
Required Permissions \(API Action\): `route53domains:GetDomainDetail`  
Resources: `*`

[GetDomainSuggestions](http://docs.aws.amazon.com/Route53/latest/APIReference/API_GetDomainSuggestions.html)  
Required Permissions \(API Action\): `route53domains:ListDomains`  
Resources: `*`

[GetOperationDetail](http://docs.aws.amazon.com/Route53/latest/APIReference/API_GetOperationDetail.html)  
Required Permissions \(API Action\): `route53domains:GetOperationDetail`  
Resources: `*`

[ListDnssec](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/domain-configure-dnssec.html) \(console only\)  
Required Permissions \(API Action\): `route53domains:ListDnssec`  
Resources: `*`

[ListDomains](http://docs.aws.amazon.com/Route53/latest/APIReference/API_ListDomains.html)  
Required Permissions \(API Action\): `route53domains:ListDomains`  
Resources: `*`

[ListOperations](http://docs.aws.amazon.com/Route53/latest/APIReference/API_ListOperations.html)  
Required Permissions \(API Action\): `route53domains:ListOperations`  
Resources: `*`

[RegisterDomain](http://docs.aws.amazon.com/Route53/latest/APIReference/API_RegisterDomain.html)  
Required Permissions \(API Action\): `route53domains:RegisterDomain`  
Resources: `*`

[RemoveDnssec](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/domain-configure-dnssec.html) \(console only\)  
Required Permissions \(API Action\): `route53domains:RemoveDnssec`  
Resources: `*`

[RenewDomain](http://docs.aws.amazon.com/Route53/latest/APIReference/API_RenewDomain.html)  
Required Permissions \(API Action\): `route53domains:RegisterDomain`  
Resources: `*`

[ResendContactReachabilityEmail](http://docs.aws.amazon.com/Route53/latest/APIReference/API_ResendContactReachabilityEmail.html)  
Required Permissions \(API Action\): `route53domains:ListDomains`  
Resources: `*`

[RetrieveDomainAuthCode](http://docs.aws.amazon.com/Route53/latest/APIReference/API_RetrieveDomainAuthCode.html)  
Required Permissions \(API Action\): `route53domains:RetrieveDomainAuthCode`  
Resources: `*`

[TransferDomain](http://docs.aws.amazon.com/Route53/latest/APIReference/API_TransferDomain.html)  
Required Permissions \(API Action\): `route53domains:TransferDomain`  
Resources: `*`

[UpdateDomainContact](http://docs.aws.amazon.com/Route53/latest/APIReference/API_UpdateDomainContact.html)  
Required Permissions \(API Action\): `route53domains:UpdateDomainContact`  
Resources: `*`

[UpdateDomainContactPrivacy](http://docs.aws.amazon.com/Route53/latest/APIReference/API_UpdateDomainContactPrivacy.html)  
Required Permissions \(API Action\): `route53domains:UpdateDomainContactPrivacy`  
Resources: `*`

[UpdateDomainNameservers](http://docs.aws.amazon.com/Route53/latest/APIReference/API_UpdateDomainNameservers.html)  
Required Permissions \(API Action\): `route53domains:UpdateDomainNameservers`  
Resources: `*`

[ViewBilling](http://docs.aws.amazon.com/Route53/latest/APIReference/API_ViewBilling.html)  
Required Permissions \(API Action\): `route53domains:ViewBilling`  
Resources: `*`

## Required Permissions for Actions on Tags for Hosted Zones and Health Checks<a name="required-permissions-tags-hosted-zones"></a>

[ChangeTagsForResource](http://docs.aws.amazon.com/Route53/latest/APIReference/API_ChangeTagsForResource.html)  
Required Permissions \(API Action\): `route53:ChangeTagsForResource`  
Resources:  

+ `arn:aws:route53:::healthcheck/*`

+ `arn:aws:route53:::hostedzone/*`

[ListTagsForResource](http://docs.aws.amazon.com/Route53/latest/APIReference/API_ListTagsForResource.html)  
Required Permissions \(API Action\): `route53:ListTagsForResource`  
Resources:  

+ `arn:aws:route53:::healthcheck/*`

+ `arn:aws:route53:::hostedzone/*`

[ListTagsForResources](http://docs.aws.amazon.com/Route53/latest/APIReference/API_ListTagsForResources.html)  
Required Permissions \(API Action\): `route53:ListTagsForResources`  
Resources:  

+ `arn:aws:route53:::healthcheck/*`

+ `arn:aws:route53:::hostedzone/*`

## Required Permissions for Actions on Tags for Domains<a name="required-permissions-tags-domains"></a>

[DeleteTagsForDomain](http://docs.aws.amazon.com/Route53/latest/APIReference/API_DeleteTagsForDomain.html)  
Required Permissions \(API Action\): `route53domains:DeleteTagsForDomain`  
Resources: `*`

[ListTagsForDomain](http://docs.aws.amazon.com/Route53/latest/APIReference/API_ListTagsForDomain.html)  
Required Permissions \(API Action\): `route53domains:ListTagsForDomain`  
Resources: `*`

[UpdateTagsForDomain](http://docs.aws.amazon.com/Route53/latest/APIReference/API_UpdateTagsForDomain.html)  
Required Permissions \(API Action\): `route53domains:UpdateTagsForDomain`  
Resources: `*`