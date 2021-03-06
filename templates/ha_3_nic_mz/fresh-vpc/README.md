## CloudFormation Template description
> If VPC, subnets, iGateway already exists and ADCs are to be provisioned on these resources, refer [ha_3nic_mz on existing-vpc](../existing-vpc)

This template deploys a VPC, with 3 subnets (Management, client, server) for 2 Availability Zones.
  It deploys an Internet Gateway, with a default  route on the public subnets.
  This template also creates a HA pair across Availability Zones with two instance of Citrix ADC:
  3 ENIs associated to 3 VPC subnets (Management, Client, Server) on primary and 3 ENIs associated
  to 3 VPC subnets (Management, Client, Server) on secondary.
  All the resource names created by this CFT will be prefixed with a tagName of the stackname.

  The output of the CloudFormation template includes:

- `PrimaryCitrixADCManagementURL`: HTTPS URL to the Management GUI of Primary VPX (uses self-signed cert)
- `PrimaryCitrixADCManagementURL2`: HTTP URL to the Management GUI of Primary VPX
- `PrimaryCitrixADCInstanceID`: Instance Id of newly created Primary VPX instance
- `PrimaryCitrixADCPublicVIP`:  Elastic IP address of the Primary VPX instance associated with the VIP
- `PrimaryCitrixADCPrivateNSIP`:  Private IP (NS IP) used for management of Primary VPX
- `PrimaryCitrixADCPublicNSIP`:  Public IP (NS IP) used for management of Primary VPX
- `PrimaryCitrixADCPrivateVIP`:  Private IP address of the Primary VPX instance associated with the VIP
- `PrimaryCitrixADCSNIP`:  Private IP address of the Primary VPX instance associated with the SNIP
- `SecondaryCitrixADCManagementURL`:  HTTPS URL to the Management GUI of Secondary VPX (uses self-signed cert)
- `SecondaryCitrixADCManagementURL2`:  HTTP URL to the Management GUI of Secondary VPX
- `SecodnaryCitrixADCInstanceID`:  Instance Id of newly created Secondary VPX instance
- `SecondaryCitrixADCPrivateNSIP`:  Private IP (NS IP) used for management of Secondary VPX
- `SecondaryCitrixADCPublicNSIP`:  Public IP (NS IP) used for management of Secondary VPX
- `SecondaryCitrixADCPrivateVIP`:  Private IP address of the Secondary VPX instance associated with the VIP
- `SecondaryCitrixADCSNIP`:  Private IP address of the Secondary VPX instance associated with the SNIP
- `SecurityGroup`:  Security group id that the VPX belongs to

## Input
The `*` against any parameter in the CFT implies it as a mandatory field.
For eg., `VPC ID*` is a mandatory field

## Pre-requisites
The CloudFormation template requires sufficient permissions to create IAM roles, beyond normal EC2 full privileges. The user of this template also needs to [accept the terms and subscribe to the AWS Marketplace product](https://aws.amazon.com/marketplace/pp/B00AA01BOE/) before using this CloudFormation template.
<p>The following should be present</p>

- Key Pair
- 3 unallocated EIPs
	- Primary Management
	- Client VIP
	- Secondary Management

## Network architecture
![Citrix HA Across AZ](https://docs.citrix.com/en-us/netscaler/media/aws-hainc.png)


## Quick Launch Links

- **US East (Ohio)** (us-east-2): [![This template creates a HA pair with two instance of Netscaler with 3 ENIs associated to 3 VPC subnets (Management, Client, Server) on primary and 3 ENIs associated to 3 VPC subnets (Management, Client, Server) on secondary](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=us-east-2#/stacks/new?templateURL=https://s3.amazonaws.com/netscaler-cft-templates/cft-freshvpc-ha-3-nic-mz.template)
- **US East (N. Virginia)** (us-east-1): [![This template creates a HA pair with two instance of Netscaler with 3 ENIs associated to 3 VPC subnets (Management, Client, Server) on primary and 3 ENIs associated to 3 VPC subnets (Management, Client, Server) on secondary](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?templateURL=https://s3.amazonaws.com/netscaler-cft-templates/cft-freshvpc-ha-3-nic-mz.template)
- **US West (N. California)** (us-west-1): [![This template creates a HA pair with two instance of Netscaler with 3 ENIs associated to 3 VPC subnets (Management, Client, Server) on primary and 3 ENIs associated to 3 VPC subnets (Management, Client, Server) on secondary](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=us-west-1#/stacks/new?templateURL=https://s3.amazonaws.com/netscaler-cft-templates/cft-freshvpc-ha-3-nic-mz.template)
- **US West (Oregon)** (us-west-2): [![This template creates a HA pair with two instance of Netscaler with 3 ENIs associated to 3 VPC subnets (Management, Client, Server) on primary and 3 ENIs associated to 3 VPC subnets (Management, Client, Server) on secondary](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks/new?templateURL=https://s3.amazonaws.com/netscaler-cft-templates/cft-freshvpc-ha-3-nic-mz.template)
- **Asia Pacific (Mumbai)** (ap-south-1): [![This template creates a HA pair with two instance of Netscaler with 3 ENIs associated to 3 VPC subnets (Management, Client, Server) on primary and 3 ENIs associated to 3 VPC subnets (Management, Client, Server) on secondary](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=ap-south-1#/stacks/new?templateURL=https://s3.amazonaws.com/netscaler-cft-templates/cft-freshvpc-ha-3-nic-mz.template)
- **Asia Pacific (Seoul)** (ap-northeast-2): [![This template creates a HA pair with two instance of Netscaler with 3 ENIs associated to 3 VPC subnets (Management, Client, Server) on primary and 3 ENIs associated to 3 VPC subnets (Management, Client, Server) on secondary](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=ap-northeast-2#/stacks/new?templateURL=https://s3.amazonaws.com/netscaler-cft-templates/cft-freshvpc-ha-3-nic-mz.template)
- **Asia Pacific (Singapore)** (ap-southeast-1): [![This template creates a HA pair with two instance of Netscaler with 3 ENIs associated to 3 VPC subnets (Management, Client, Server) on primary and 3 ENIs associated to 3 VPC subnets (Management, Client, Server) on secondary](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-1#/stacks/new?templateURL=https://s3.amazonaws.com/netscaler-cft-templates/cft-freshvpc-ha-3-nic-mz.template)
- **Asia Pacific (Sydney)** (ap-southeast-2): [![This template creates a HA pair with two instance of Netscaler with 3 ENIs associated to 3 VPC subnets (Management, Client, Server) on primary and 3 ENIs associated to 3 VPC subnets (Management, Client, Server) on secondary](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-2#/stacks/new?templateURL=https://s3.amazonaws.com/netscaler-cft-templates/cft-freshvpc-ha-3-nic-mz.template)
- **Asia Pacific (Tokyo)** (ap-northeast-1): [![This template creates a HA pair with two instance of Netscaler with 3 ENIs associated to 3 VPC subnets (Management, Client, Server) on primary and 3 ENIs associated to 3 VPC subnets (Management, Client, Server) on secondary](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=ap-northeast-1#/stacks/new?templateURL=https://s3.amazonaws.com/netscaler-cft-templates/cft-freshvpc-ha-3-nic-mz.template)
- **Canada (Central)** (ca-central-1): [![This template creates a HA pair with two instance of Netscaler with 3 ENIs associated to 3 VPC subnets (Management, Client, Server) on primary and 3 ENIs associated to 3 VPC subnets (Management, Client, Server) on secondary](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=ca-central-1#/stacks/new?templateURL=https://s3.amazonaws.com/netscaler-cft-templates/cft-freshvpc-ha-3-nic-mz.template)
- **EU (Frankfurt)** (eu-central-1): [![This template creates a HA pair with two instance of Netscaler with 3 ENIs associated to 3 VPC subnets (Management, Client, Server) on primary and 3 ENIs associated to 3 VPC subnets (Management, Client, Server) on secondary](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=eu-central-1#/stacks/new?templateURL=https://s3.amazonaws.com/netscaler-cft-templates/cft-freshvpc-ha-3-nic-mz.template)
- **EU (Ireland)** (eu-west-1): [![This template creates a HA pair with two instance of Netscaler with 3 ENIs associated to 3 VPC subnets (Management, Client, Server) on primary and 3 ENIs associated to 3 VPC subnets (Management, Client, Server) on secondary](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=eu-west-1#/stacks/new?templateURL=https://s3.amazonaws.com/netscaler-cft-templates/cft-freshvpc-ha-3-nic-mz.template)
- **EU (London)** (eu-west-2): [![This template creates a HA pair with two instance of Netscaler with 3 ENIs associated to 3 VPC subnets (Management, Client, Server) on primary and 3 ENIs associated to 3 VPC subnets (Management, Client, Server) on secondary](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=eu-west-2#/stacks/new?templateURL=https://s3.amazonaws.com/netscaler-cft-templates/cft-freshvpc-ha-3-nic-mz.template)
- **South America (Sao Paulo)** (sa-east-1): [![This template creates a HA pair with two instance of Netscaler with 3 ENIs associated to 3 VPC subnets (Management, Client, Server) on primary and 3 ENIs associated to 3 VPC subnets (Management, Client, Server) on secondary](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=sa-east-1#/stacks/new?templateURL=https://s3.amazonaws.com/netscaler-cft-templates/cft-freshvpc-ha-3-nic-mz.template)




## Additional Links:

- **HA Across AZs**: https://docs.citrix.com/en-us/citrix-adc/13/deploying-vpx/deploy-aws/high-availability-different-zones.html
- **VPX installation in AWS** : https://docs.citrix.com/en-us/citrix-adc/13/deploying-vpx/deploy-aws.html
- **Citrix ADC Overview** : https://www.citrix.com/products/citrix-adc/
