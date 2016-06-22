# Create a High Availabilty SharePoint Farm with additional File Servers and Gateways using the Powershell DSC Extension

This template will create the following resources:

+	A Virtual Network
+	Six Subnets (Gateway, File Server, Front-end, SharePoint, SQL, AD)
+	Six Storage Accounts (one is used for Active Directory VMs, one for SQL Server VMs, two for SharePoint VMs, one for the File Server VMs and one for VM diagnostic info)
+	Two VMs as Domain Controllers for a new Forest and Domain
+	Two VMs in a Windows Server Cluster running SQL Server with an availability group, + One additional VM acting as a File Share Witness for the Cluster
+	Two SharePoint App Servers
+	Two SharePoint Web Servers
+	Two File Servers in HA configuration using DFSR
+	One Expressroute Gateway, one Point-to-Site VPN Gateway
+	Three external and one internal load balancers
+	A NAT Rule to allow RDP to one VM which can be used as a jumpbox, a load balancer rule for ILB for a SQL Listener, a load balancer rule for HTTP traffic on port 80 for SharePoint and a NAT rule for SharePoint Central Admin access
+	Three public IP addresses, one for RDP access, one for the SharePoint site and one for SharePoint Central Admin.
+	Four Availability Sets one for the AD VMs, one for the SQL and Witness VMs, one for the SharePoint App Servers and one for the SharePoint Web Servers 

## Notes

+	The default settings for storage are to deploy using **premium storage**, the AD witness and SP VMs use a P10 Disk and the SQL VMs use two P30 disks each, these sizes can be changed by changing the relevant variables. In addition there is a P10 Disk used for each VMs OS Disk.

+ 	In default settings for compute require that you have at least 19 cores of free quota to deploy.

+	Public Endpoints are created for the SharePoint site that this template creates and for the Central Admin site, however no permissions are given to any user for the new SharePoint site created, these will need to be added from the Central Admin site.

+ 	The images used to create this deployment are
	+ 	AD - Latest Windows Server 2012 R2 Image
	+ 	SQL Server - Latest SQL Server 2014 on Windows Server 2012 R2 Image
	+ 	Witness - Latest Windows Server 2012 R2 Image
	+	SharePoint - Latest SharePoint server 2013 trial image on Windows Server 2012 R2
	+ 	File Servers - Latest Windows Server 2012 R2 Image

+ 	The image configuration is defined in variables - details below - but the scripts that configure this deployment have only been tested with these versions and may not work on other images.

+ 	Once deployed access can be gained at the following addresses:

	+	**SharePoint Website** - http://parameter(dnsPrefix).parameter(location).cloudapp.azure.com
	+	**Central Admin Website** - http://parameter(spCentralAdminDNSPrefix).parameter(location).cloudapp.azure.com
	+	**RDP Jump Box** - mstsc -v parameter(rdpDNSPrefix).parameter(location).cloudapp.azure.com


<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fgkazup%2Fazure-templates%2Fmaster%2FGHD-Azure-POC%2Fazuredeploy.json" target="_blank">
    <img src="http://azuredeploy.net/deploybutton.png"/>
</a>
<a href="http://armviz.io/#/?load=https://raw.githubusercontent.com/gkazup/azure-templates/master/GHD-Azure-POC/azuredeploy.json" target="_blank">
  <img src="http://armviz.io/visualizebutton.png"/>
</a>

## Notable Variables

|Name|Description|
|:---|:---------------------|
|virtualNetworkName|Name of the Virtual Network|
|adPDCVMName|The name of the Primary Domain Controller|
|adBDCVMName|The name of the Backup\Second Domain Controller|
|sqlVMName|The prefix for the SQL VM Names|
|sqlwVMName|The name of the File Share Witness|
|spwebVMName|The Prefix of the SharePoint Web Server VMs|
|spappVMName|The Prefix of the SharePoint App Server VMs|
|fsVMName|The Prefix of the File Server VMs|
