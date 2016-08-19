# Create a DFSR environment using the Powershell DSC Extension

This template will create the following resources:

+	A Virtual Network
+	Subnets (Gateway, File Server, Name Server, AD)
+	Storage Accounts (one is used for Active Directory VMs, one for DFSR nameserver, one for the File Server VMs and one for VM diagnostic info)
+	One VM as Domain Controller for a new Forest and Domain
+	One DFSR Name Server
+	Two File Servers in HA configuration using DFSR
+	A NAT Rule to allow RDP to the DC
+	One public IP address for RDP access
+	Availability Sets: one for the DFSR Servers 

## Notes

+	The default settings for storage are to deploy using **local replicated storage**

+ 	The image used to create this deployment is
	+ 	Latest Windows Server 2012 R2 Image

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
|adPDCVMName|The name of the Domain Controller|
|DFSRVMName|The name of the DFSR Name server|
|fsVMName|The Prefix of the File Server VMs|
