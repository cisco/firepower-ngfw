# Cisco Firepower NGFW Virtual (NGFWv) Appliances  

## Security for virtual and hybrid cloud environments  

The Cisco Firepower® NGFW (next-generation firewall) is the industry’s first fully integrated, threat-focused next-gen firewall with 
unified management. It uniquely provides advanced threat protection before, during, and after attacks.

The Firepower Threat Defense Virtual (FTDv) is the virtualized component of the Cisco NGFW solution. Organizations employing SDN can 
rapidly provision and orchestrate flexible network protection with Firepower NGFWv. As well, organizations using NFV can further 
lower costs utilizing Firepower FTDv.

## Supported Platforms

The FTDv is supported on the following platforms:

* VMware ESXi  
* KVM  
* AWS  
* Azure

## Management Options  
Cisco Firepower NGFWs may be managed in a variety of ways depending on the way you work, your environment, and your needs.  
* **The Cisco Firepower Management Center (FMC)** — Provides centralized management of the Cisco Firepower NGFW, the 
Cisco Firepower NGIPS, and Cisco AMP for Networks. It also provides threat correlation for network sensors and Advanced Malware 
Protection (AMP) for Endpoints.  

* **The Cisco Firepower Device Manager (FDM)** — Provides an integrated, web-based configuration interface especially designed for 
networks that include a single device or just a few. FDM lets you configure the basic features of the software that are most 
commonly used for small networks. The option is currently supported on VMware and KVM.

If you are managing large numbers of devices, or if you want to use the more complex features and configurations that Firepower 
Threat Defense allows, use the Firepower Management Center to configure your devices instead of the integrated Firepower Device Manager.  

You cannot use both the FDM and FMC to manage an FTDv deployed to VMware or KVM. Once the FDM onboard management is enabled, it won't 
be possible to use an FMC to manage the FTDv, unless you disable the local management and re-configure the management to use an FMC. 
On the other hand, when you register the FTDv to an FMC, the FDM onboard management service is disabled. 

**Note: Right now Cisco does not have an option to migrate your FDM Firepower configuration to an FMC and vice-versa. 
Take this into consideration when you choose what type of management you configure for the FTDv deployed to VMware and KVM.** 

## Support & Downloads  
All support information for Cisco Firepower Threat Defense Virtual (FTDv)  

**Data Sheet**  
[Cisco Firepower Next-Generation Firewall (NGFW) Data Sheet](https://www.cisco.com/c/en/us/support/security/defense-center/products-release-notes-list.html)

**Documentation**  
* Firepower System Release Notes: [Go here](https://www.cisco.com/c/en/us/support/security/virtual-adaptive-security-appliance-firewall/products-release-notes-list.html).  
* Technical Documentation: [FTDv Getting Started Guides](https://www.cisco.com/c/en/us/support/security/firepower-ngfw-virtual/products-installation-guides-list.html)  
* White Papers: [Go here](https://www.cisco.com/c/en/us/products/security/virtual-adaptive-security-appliance-firewall/white-paper-listing.html)  

**Software**  
[Downloads Home](https://software.cisco.com/download/home/286306503/type)  

## Public Cloud Deployment  
### Azure  
The FTDv on Microsoft Azure supports the Standard D3 and Standard D3_v2 instances, which supports four vCPUs, 14 GB, and four interfaces.  

You can deploy the FDTv on Microsoft Azure in one of two ways:
* As a stand-alone firewall using the Azure Resource Manager
* As an integrated partner solution using the Azure Security Center

**Azure Resource Templates**  
You can deploy the FTDv using Azure Resource Manager templates. An Azure Resource Template is a JSON file. 
To simplify the deployment of all the required resources, you can use two JSON files:  
* **Template File** — This is the main resources file that deploys all the components within the resource group. 
* **Parameter File** — This file includes the parameters required to successfully deploy the FTDv. It includes details such 
as the subnet information, virtual machine tier and size, username and password for the FTDv, the name of the storage container, etc. 
You can customize this file for your Azure deployment environment.  

*Example: Azure Resource Manager JSON Template File*  
```
{
    "$schema": "http://schema.management.azure.com/schemas/2018-01-01/deploymentTemplate.json#",
    "contentVersion": "",
    "parameters": {  },
    "variables": {  },
    "resources": [  ],
    "outputs": {  }
}
```
**Documentation**  
* Templates and Examples: Included in this repository.
* Technical Documentation: [Cisco Firepower NGFW Virtual](https://www.cisco.com/c/en/us/support/security/firepower-ngfw-virtual/products-installation-guides-list.html)

[<img src="http://azuredeploy.net/deploybutton.png"/>](https://portal.azure.com)  
___

### AWS  
The FTDv runs as a guest in the AWS environment of the Xen Hypervisor. FTDv on AWS supports the following instance types:  
* **c4.xlarge** — 4 vCPUs, 7.5 GB, 3 interfaces (1 management interface, 2 data interfaces) *Recommended*
* **c3.xlarge** — 4 vCPUs, 7.5 GB, 4 interfaces (1 management interface, 2 data interfaces)

You create an account on AWS, set up the FTDv using the AWS Wizard, and chose an Amazon Machine Image (AMI). 
The AMI is a template that contains the software configuration needed to launch your instance.  
**Note:** The AMI images are not available for download outside of the AWS environment.  

**Documentation**  
* Technical Documentation: [Cisco Firepower NGFW Virtual](https://www.cisco.com/c/en/us/support/security/firepower-ngfw-virtual/products-installation-guides-list.html)

[<img src="https://a0.awsstatic.com/libra-css/images/logos/aws_logo_smile_179x109.png"/>](https://aws.amazon.com/)  
___ 
# FTDv templates and artifacts  

#### TBD

# firepower-ngfw
Firepower Threat Defense Virtual templates and artifacts
