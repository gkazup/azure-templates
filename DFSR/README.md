# Create a High Availabilty DFSR environment using the Powershell DSC Extension

This template will create the following resources:

+	A Virtual Network
+	Subnets (Gateway, File Server, AD)
+	Storage Accounts (one is used for Active Directory VMs, one for the File Server VMs and one for VM diagnostic info)
+	Two VMs as Domain Controllers for a new Forest and Domain
+	Two File Servers in HA configuration using DFSR
+	One external and one internal load balancers
+	A NAT Rule to allow RDP to the DCs
+	One public IP address for RDP access, one for the SharePoint site and one for SharePoint Central Admin.
+	Availability Sets: one for the AD VMs, one for the DFSR Servers 

## Notes

+	The default settings for storage are to deploy using **premium storage**, the AD witness and SP VMs use a P10 Disk and the SQL VMs use two P30 disks each, these sizes can be changed by changing the relevant variables. In addition there is a P10 Disk used for each VMs OS Disk.

+ 	The images used to create this deployment are
	+ 	AD - Latest Windows Server 2012 R2 Image
	+ 	File Servers - Latest Windows Server 2012 R2 Image

+ 	Once deployed access can be gained at the following addresses:

	+	**RDP Jump Box** - mstsc -v parameter(rdpDNSPrefix).parameter(location).cloudapp.azure.com


<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fgkazup%2Fazure-templates%2Fmaster%2FDFSR%2Fazuredeploy.json" target="_blank">
    <img src="http://azuredeploy.net/deploybutton.png"/>
</a>
<a href="http://armviz.io/#/?load=https://raw.githubusercontent.com/gkazup/azure-templates/master/DFSR/azuredeploy.json" target="_blank">
  <img src="http://armviz.io/visualizebutton.png"/>
</a>

## Notable Variables

|Name|Description|
|:---|:---------------------|
|virtualNetworkName|Name of the Virtual Network|
|adPDCVMName|The name of the Primary Domain Controller|
|adBDCVMName|The name of the Backup\Second Domain Controller|
|fsVMName|The Prefix of the File Server VMs|
