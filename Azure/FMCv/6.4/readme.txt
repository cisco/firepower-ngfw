Azure Firepower Management Center Virtual deployment using VHD and ARM template
==================================================

Azure FMCv quick start guide: https://www.cisco.com/c/en/us/td/docs/security/firepower/quick_start/fmcv/fpmc-virtual/fpmc-virtual-azure.html 

In addition to the Marketplace-based deployment, Cisco provides a compressed virtual hard disk (VHD) that you can upload to Azure to simplify the process of deploying the Firepower Management Center Virtual in Azure. 
Using a Managed Image and two JSON files (a Template file and a Parameter File), you can deploy and provision all the resources for the Firepower Management Center Virtual in a single, coordinated operation. 

To deploy using a VHD image, you must upload the VHD image to your Azure storage account. Then, you can create a managed image using the uploaded disk image and an Azure Resource Manager template.
Azure templates are JSON files that contain resource descriptions and parameter definitions.


Deployment Procedure:
=====================

Please refer the NGFWv/FTDv deployment procedure and this FMCv deployment is very similar to that.
    Azure NGFWv quick start guide: https://www.cisco.com/c/en/us/td/docs/security/firepower/quick_start/azure/ftdv-azure-qsg.html


1. Download the Firepower Management Center Virtual vhd image from Cisco Download Software download page. 
e.g. 6.4.0-102 NGFWv image can be downloaded from:
URL  : https://software.cisco.com/download/home/286259687/type/286271056/release/6.4.0 
File : [ Firepower Management Center Virtual 6.4.0 on Azure ]  	Cisco_Firepower_Mgmt_Center_Virtual-6.4.0-102.vhd.bz2

2. Create a linux VM in Azure and uncompress & upload the VHD image to container in Azure storage account.

3. Create a Managed Image from the VHD and acquire the Resource ID of the newly created Managed Image.

4. Use the ARM template to deploy a Firepower Management Center Virtual using the managed image.

5. Update the parameters in the parametrs template file(json) and use it to provide the parameters to the ARM template.

6. Review and purchase the template to deploy Firepower Management Center Virtual.

7. Configure the FMCv/Firepower Management Center Virtual 
 

Parameters required for the Azure ARM template:
===============================================

Pre-requisites:
---------------
* Managed image ID (created using the downloaded vhd)
* Virtual network with at least 1 subnet for management interface.

1. vmName: The name the Firepower Management Center Virtual VM will have in Azure.
e.g. cisco-fmcv

2. vmManagedImageId: The ID of the managed image used for deployment. Internally, Azure associates every resource with a Resource ID.
e.g. /subscriptions/f160cf7e-ae69-4e9f-8ad0-b434b9a63755/resourceGroups/blr-virtual-images-rg/providers/Microsoft.Compute/images/cisco-fmcv-640102

3. adminUsername: The username for logging into Firepower Management Center Virtual. This cannot be the reserved name "admin".
e.g. jdoe

4. adminPassword: The admin password. This must be 12 to 72 characters long, and include three of the following: 1 lower case, 1 upper case, 1 number, 1 special character.
e.g. Pw0987654321

5. customData: The field to provide Day 0 configuration to the FMCv. By default it has 2 key-value pairs to configure 'admin' user password and the FMCv hostname.
e.g. {"AdminPassword": "Cisco1234", "Hostname": "cisco-fmcv"}

6. vmStorageAccount: Your Azure storage account. You can use an existing storage account or create a new one. The storage account name must be between 3 and 24 characters, and can only contain lowercase letters and numbers.
e.g. testfmcvstorage

7. virtualNetworkResourceGroup: The name of the virtual network's Resource Group. The Firepower Management Center Virtual is always deployed into a new Resource Group.
e.g. test-fmcv-rg

8. virtualNetworkName: The name of the virtual network.
e.g. test-fmcv-vnet

9. mgmtSubnetName: The management interface will attach to this subnet. This maps to Nic0, the first subnet. Note, this must match an existing subnet name if joining an existing network.
e.g. mgmt

10. mgmtSubnetIP: The Management interface IP address.
e.g. 10.4.0.15

11. vmSize: The VM size to use for the Firepower Management Center Virtual VM. Standard_D3_V2, Standard_D3, Standard_D4_V2, Standard_D4 are supported. Standard_D3_V2 is the default.
e.g. Standard_D3_V2
