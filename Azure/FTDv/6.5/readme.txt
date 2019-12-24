Azure NGFWv deployment using VHD and ARM template
==================================================

Azure NGFWv quick start guide: https://www.cisco.com/c/en/us/td/docs/security/firepower/quick_start/azure/ftdv-azure-qsg.html

In addition to the Marketplace-based deployment, Cisco provides a compressed virtual hard disk (VHD) that you can upload to Azure to simplify the process of deploying the Firepower Threat Defense Virtual in Azure. 
Using a Managed Image and two JSON files (a Template file and a Parameter File), you can deploy and provision all the resources for the Firepower Threat Defense Virtual in a single, coordinated operation. 

To deploy using a VHD image, you must upload the VHD image to your Azure storage account. Then, you can create a managed image using the uploaded disk image and an Azure Resource Manager template.
Azure templates are JSON files that contain resource descriptions and parameter definitions.

Use the instructions in the quick start guide for NGFWv deployment.

Azure NGFWv quick start guide: https://www.cisco.com/c/en/us/td/docs/security/firepower/quick_start/azure/ftdv-azure-qsg.html


Overview of deployment procedure:
=================================

1. Download the NGFWv vhd image from Cisco Download Software download page. 
e.g. 6.5.0-102 NGFWv image can be downloaded from:
URL  : https://software.cisco.com/download/home/286306503/type/286306337/release/6.5.0 
File : [ Firepower NGFW Virtual v6.5.0 on Azure ]  Cisco_Firepower_Threat_Defense_Virtual-6.5.0-102.vhd.bz2

2. Create a linux VM in Azure and uncompress & upload the VHD image to container in Azure storage account.

3. Create a Managed Image from the VHD and acquire the Resource ID of the newly created Managed Image.

4. Use the ARM template to deploy a Firepower Threat Defense Virtual firewall using the managed image.

5. Update the parameters in the parametrs template file(json) and use it to provide the parameters to the ARM template.

6. Review and purchase the template to deploy Firepower Threat Defense Virtual firewall.

7. Configure the NGFWv 
    a. Update the Firepower Threat Defense Virtual’s IP configuration in Azure.
    b. Update the Public IP Address Configuration
    c. Optionally, add a public IP address to a data interface.
    d. Configure the Firepower Threat Defense Virtual for management by a Firepower Management Center.
    e. Update the Azure Security Groups.
    f. Register the Firepower Threat Defense Virtual with the Firepower Management Center.
    g. Enable and configure the two data interfaces.
    h. Configure Device Settings
 


Parameters required for the Azure ARM template:
===============================================

Pre-requisites:
---------------
* Managed image ID (created using the downloaded vhd)
* Virtual network with 4 subnets corresponding to management, diagnostic, GigabitEthernet0/0 and GigabitEthernet0/1 respectively.

1. vmName: The name the Firepower Threat Defense Virtual VM will have in Azure.
e.g. cisco-ngfw

2. vmManagedImageId: The ID of the managed image used for deployment. Internally, Azure associates every resource with a Resource ID.
e.g. /subscriptions/73d2537e-ca44-46aa-beb2-74ff1dd61b41/resourceGroups/ewManagedImages-rg/providers/Microsoft.Compute/images/FTDv-6.2.2-81-Managed-Image

3. adminUsername: The username for logging into Firepower Threat Defense Virtual. This cannot be the reserved name ‘admin’.
e.g. jdoe

4. adminPassword: The admin password. This must be 12 to 72 characters long, and include three of the following: 1 lower case, 1 upper case, 1 number, 1 special character.
e.g. Password@123123

5. vmStorageAccount: Your Azure storage account. You can use an existing storage account or create a new one. The storage account name must be between 3 and 24 characters, and can only contain lowercase letters and numbers.
e.g. ciscongfwstorage

6. customData: The field to provide Day 0 configuration to the FTDv. By default it has 3 key-value pairs to configure 'admin' user password, the FMCv hostname and whether to use FDM or FMC for management.
'ManageLocally : yes' - will configure the FDM to be used as FTDv manager.
e.g. {"AdminPassword": "FtdvPass@123123", "Hostname": "cisco-fmcv", "ManageLocally": "Yes"}

You can configure the FMCv as FTDv manager and also give the inputs for fields required to configure the same on FTDv.
e.g. {"AdminPassword": "FtdvPass@123123", "Hostname": "cisco-fmcv", "ManageLocally": "No", "FmcIp": "<fmcIp>", "FmcRegKey": "<fmcRegKey>", "FmcNatId": "<fmcNatId>" }

7. virtualNetworkResourceGroup: The name of the virtual network's Resource Group. The Firepower Threat Defense Virtual is always deployed into a new Resource Group.
e.g. test-ngfw-rg

8. virtualNetworkName: The name of the virtual network.
e.g. test-ngfw-vnet

9. mgmtSubnetName: The management interface will attach to this subnet. This maps to Nic0, the first subnet. Note, this must match an existing subnet name if joining an existing network.
e.g. mgmt

10. mgmtSubnetIP: The Management interface IP address.
e.g. 10.8.0.55

11. diagSubnetName: The diagnostic interface will attach to this subnet. This maps to Nic1, the second subnet. Note, this must match an existing subnet name if joining an existing network.
e.g. diag

12. diagSubnetIP: The diagnostic interface IP address.
e.g. 10.8.1.55

13. gig00SubnetName: The GigabitEthernet 0/0 interface will attach to this subnet. This maps to Nic2, the third subnet. Note, this must match an existing subnet name if joining an existing network.
e.g. inside

14. gig00SubnetIP: The GigabitEthernet 0/0 interface IP address. This is for Firepower Threat Defense Virtual’s first data interface.
e.g. 10.8.2.55

15. gig01SubnetName: The GigabitEthernet 0/1 interface will attach to this subnet. This maps to Nic3, the third subnet. Note, this must match an existing subnet name if joining an existing network.
e.g. outside

16. gig01SubnetIP: The GigabitEthernet 0/1 interface IP address. This is for Firepower Threat Defense Virtual’s second data interface.
e.g. 10.8.3.55

17. vmSize: The VM size to use for the Firepower Threat Defense Virtual VM. Standard_D3_V2 is the default.
Supported sizes: Standard_D3_V2, Standard_D3, Standard_D4_v2 & Standard_D5_v2
e.g. Standard_D3_V2 or Standard_D3 or Standard_D4_v2 or Standard_D5_v2



