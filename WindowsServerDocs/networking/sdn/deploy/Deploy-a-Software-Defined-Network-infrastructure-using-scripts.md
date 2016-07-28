---
title: Deploy a Software Defined Network infrastructure using scripts
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.service: virtual-network
ms.suite: na
ms.technology: 
  - techgroup-networking
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5ba5bb37-ece0-45cb-971b-f7149f658d19
author: vhorne
---
# Deploy a Software Defined Network infrastructure using scripts

>Applies To: Windows Server 2016

This topic covers how to deploy a Microsoft Software Defined Network (SDN) infrastructure using scripts. The infrastructure includes a highly available (HA) network controller, an HA Software Load Balancer (SLB)/MUX, virtual networks, and associated Access Control Lists (ACLs). Additionally, another script deploys a tenant workload for you to validate your SDN infrastructure.  
  
If you want your tenant workloads to communicate outside their virtual networks, you can setup SLB NAT rules, Site-to-Site Gateway tunnels, or Layer-3 Forwarding to route between virtual and physical workloads.  
  
You can also deploy an SDN infrastructure using Virtual Machine Manager (VMM). For more information, see [Deploy a Software Defined Network infrastructure using VMM](https://technet.microsoft.com/en-us/library/mt695701.aspx).  
  
## Pre-deployment  
  
> [!IMPORTANT]  
> Before you begin deployment, you must plan and configure your hosts and physical network infrastructure. For more information, see [Plan a Software Defined Network Infrastructure](../../sdn/plan/../../sdn/plan/../../sdn/plan/Plan-a-Software-Defined-Network-Infrastructure.md).  
  
All Hyper-V hosts must have Windows Server 2016 installed.  
  
## Deployment Steps  
Start by configuring the Hyper-V host's (physical servers) Hyper-V virtual switch and  IP address assignment. Any storage type that is compatible with Hyper-V, shared or local may be used.  
### Install host networking  
1. Install the latest network drivers available for your NIC hardware.  
2. Install the Hyper-V role on all hosts (For more information, see [Get started with Hyper-V on Windows Server 2016 Technical Preview](https://technet.microsoft.com/en-us/library/mt126159.aspx).   
  
   From an elevated Windows PowerShellcommand prompt:  
   ``Install-WindowsFeature -Name Hyper-V -ComputerName <computer_name> -IncludeManagementTools -Restart``  
    
    a. Create the Hyper-V virtual switch (use the same switch name for all hosts. For example: **sdnSwitch**). Configure at least one network adapter or, if using Switch Embedded Teaming, configure at least two network adapters. Maximum inbound spreading occurs when using two NICs.  
 `` New-VMSwitch "<switch name>" -NetAdapterName "<NetAdapter1>" [, "<NetAdapter2>" -EnableEmbeddedTeaming $True] -AllowManagementOS $True``  
 
 >[!NOTE] 
 >You  can skip steps 4 and 5 if you have separate Management NICs.

 b. Refer to the planning topic ([Plan a Software Defined Network Infrastructure](../../sdn/plan/../../sdn/plan/../../sdn/plan/Plan-a-Software-Defined-Network-Infrastructure.md)) and work with your network administrator to obtain the VLAN ID of the Management VLAN. Attach the Management vNIC of the newly created Virtual Switch to the Management VLAN. This step can be omitted if your environment does not use VLAN tags.  
 `` Set-VMNetworkAdapterIsolation -ManagementOS -IsolationMode Vlan -DefaultIsolationID <Management VLAN> -AllowUntaggedTraffic $True``  
 
 c. Refer to the planning topic ([Plan a Software Defined Network Infrastructure](../../sdn/plan/../../sdn/plan/../../sdn/plan/Plan-a-Software-Defined-Network-Infrastructure.md)) and work with your network administrator to use either DHCP or static IP assignments to assign an IP address to the Management vNIC of the newly created vSwitch. The following example shows how to create a static IP address and assign it to the Management vNIC of the vSwitch:  
 ``New-NetIPAddress -InterfaceAlias "vEthernet (<switch name>)" -IPAddress <IP> -DefaultGateway <Gateway IP> -AddressFamily IPv4 -PrefixLength <Length of Subnet Mask - for example: 24>``  
      
3. [Optional] Deploy a virtual machine to host Active Directory Domain Services ([Install Active Directory Domain Services (Level 100)](https://technet.microsoft.com/library/hh472162.aspx) and a DNS Server.  
   
    a. Connect the Active Directory/DNS Server virtual machine to the Management VLAN:
    
        ``Set-VMNetworkAdapterIsolation -VMName "<VM Name>" -Access -VlanId <Management VLAN> -AllowUntaggedTraffic $True``  
   
   b. Install Active Directory Domain Services and DNS.  
      >[!NOTE]
      >The network controller supports both Kerberos and X.509 certificates for authentication. This guide uses both authentication mechanisms for different purposes (although only one is required).  
        
4. Join all Hyper-V hosts to the domain. Ensure the DNS server entry for the network adapter that has an IP address assigned to the Management network points to a DNS server that can resolve the domain name. For example:  
``Set-DnsClientServerAddress -InterfaceAlias "vEthernet (<switch name>)" -ServerAddresses <DNS Server IP>``  
   
   a. Right-click **Start**, click **System**, and then click **Change Settings**.  
   b. Click **Change**.  
   c. Click **Domain** and specify the domain name.  
   d. Click **OK**.  
   e. Type the user name and password credentials when prompted.  
   f. Restart the server.  
  
### Validation  
Use the following steps to validate that host networking is setup correctly.  
1. Ensure the VM Switch was created successfully:  
      
    ``Get-VMSwitch "<switch name>"``  
2. Verify that the Management vNIC on the VM Switch is connected to the Management VLAN:  
	>[!NOTE]
	>Relevant only if Management and Tenant traffic share the same NIC.    
	  
    ``Get-VMNetworkAdapterIsolation -ManagementOS``  
3. Validate that all Hyper-V hosts (and external management resources, for example: DNS servers) are accessible via ping using their Management IP address and/or fully qualified domain name (FQDN).   
      
   ``ping <Hyper-V Host IP>``  
   ``ping <Hyper-V Host FQDN>``  
4. Run the following command on the deployment host and specify the FQDN of each Hyper-V host to ensure the Kerberos credentials used provides access to all the servers.  
      
   ``winrm id -r:<Hyper-V Host FQDN>``  
      
### Nano installation requirements and notes  
If you use Nano as your Hyper-V hosts (physical servers) for the deployment, the following are additional requirements:  
1. All Nano nodes need to have the DSC package installed with the language pack:  
   
   * Microsoft-NanoServer-DSC-Package.cab  
   * Microsoft-NanoServer-DSC-Package_en-us.cab
   
        ``dism /online /add-package /packagepath:<Path> /loglevel:4``  
2. The SDN Express scripts must be run from a non-Nano host  (Windows Server Core or Windows Server w/ GUI). PowerShell Workflows are not supported on Nano.  
3.  Invoking the Network Controller NorthBound API using PowerShell or NC REST Wrappers (which rely on Invoke-WebRequest and Invoke-RestMethod) must be done from a non-Nano host.  
   
         
### Run SDN Express Scripts  
  
1.  The installation files are located on GitHub. Download the zip file from the [Microsoft SDN GitHub Repository](https://github.com/Microsoft/SDN.git). On the Microsoft SDN repository page, click **Clone or download** and then click **Download ZIP**.  
  
2.  Designate one computer as your deployment computer.  This computer must be running Windows Server 2016. Expand the zip file and copy the **SDNExpress** folder to the deployment computer's `C:\` folder.  
  
3.  Share the `C:\SDNExpress` folder as "**SDNExpress**" with permission for **Everyone** to **Read/Write**.  
  
4.  Navigate to the `C:\SDNExpress` folder.

 You will see the following folders:  

|Folder Name|Description|  
|---------------|---------------|  
|AgentConf|Holds fresh copies of OVSDB schemas used by the SDN Host Agent on each Windows Server 2016 Hyper-V host to program network policy.|  
|Certs|Temporary shared location for the NC certificate file.|  
|Images|Empty, place your Windows Server 2016 vhdx image here|  
|Tools|Utilities for troubleshooting and debugging.  Copied to the hosts and virtual machines.  We recommend you place Network Monitor or Wireshark here so it is available if needed.|  
|Scripts|Deployment scripts.<br /><br />-   **SDNExpress.ps1**<br />    Deploys and configures the fabric, including the Network controller virtual machines, SLB Mux virtual machines, gateway pool(s) and the HNV gateway virtual machine(s) corresponding to the pool(s) .<br />-   **FabricConfig.psd1**<br />    A  configuration file template for the SDNExpress script.  You will customize this for your environment.<br />-   **SDNExpressTenant.ps1**<br />    Deploys a sample tenant workload on a virtual network with a load balanced VIP.<br />    Also provisions one or more network connections (IPSec S2S VPN, GRE, L3) on the service provider edge gateways which are connected to the previously created tenant workload. The IPSec and GRE gateways are available for connectivity over the corresponding VIP IP Address, and the L3 forwarding gateway over the corresponding address pool.<br />    This script can be used to delete  the corresponding configuration with an Undo option as well.<br />-   **TenantConfig.psd1**<br />    A template configuration file for tenant workload and S2S gateway configuration.<br />-   **SDNExpressUndo.ps1**<br />    Cleans up the fabric environment and resets it to a starting state.<br />-   **SDNExpressEnterpriseExample.ps1**<br />    Provisions one or more enterprise site environments with one Remote Access Gateway and (optionally) one corresponding enterprise virtual machine per site. The IPSec or GRE enterprise gateways connects to the corresponding VIP IP address of the service provider gateway to establish the S2S tunnels. The L3 Forwarding Gateway connects over the corresponding Peer IP Address. <br />            This script can be used to delete the corresponding configuration with an Undo option as well.<br />-   **EnterpriseConfig.psd1**<br />    A template configuration file for the Enterprise site-to-site gateway and Client VM configuration.|  
|TenantApps|Files used to deploy example tenant workloads.|  
  
5.  Verify the Windows Server 2016 VHDX file is in the **Images** folder.  
  
6. Customize the SDNExpress\scripts\FabricConfig.psd1 file by changing the **<< Replace >>** tags with specific values to fit your lab infrastructure including host names, domain names, usernames and passwords, and network information for the networks listed in the Planning Network topic.  
7. Create a Host A record in DNS for the NetworkControllerRestName (FQDN) and NetworkControllerRestIP.  
8. Run the script as a user with domain administrator credentials:  
      
    ``SDNExpress\scripts\SDNExpress.ps1 -ConfigurationDataFile FabricConfig.psd1 -Verbose``  
      
9.  To undo all operations, run the following command:  
      
    ``SDNExpress\scripts\SDNExpressUndo.ps1 -ConfigurationDataFile FabricConfig.psd1 -Verbose``  
      
#### Validation  
Assuming that the SDN Express script ran to completion without reporting any errors, you can perform the following steps to ensure the fabric resources have been deployed correctly and are available for tenant deployment.  
1. Ensure that both the NC Host Agent and SLB Host Agent is running on all Hyper-V hosts.  
    ``Get-Service NCHostAgent``  
    ``Get-Service SlbHostAgent``  
2.  Test network connectivity (on the Management logical network) between all Network Controller node virtual machines and Hyper-V hosts using ping.  
3.  Check that the NC Host Agent is connected to the network controller on TCP:6640.  
      
    ``netstat -anp tcp |findstr 6640``  
      
4. Ensure that the DIPs (Dynamic IPs) associated with all Hyper-V hosts that will be hosting load-balanced tenant workload virtual machines have Layer-3 IP connectivity to the Software Load Balancer Manager (SLBM) Virtual IP (VIP) address. The SLBM VIP is usually the first IP address in the VIP IP Pool range specified in the FabricConfig.psd file   
5.  Use [diagnostic tools](../../sdn/troubleshoot/Troubleshoot-Software-Defined-Networking.md) to ensure there are no errors on any fabric resources in the network controller.  
      
    ``Debug-NetworkControllerConfigurationState -NcIpAddress <FQDN of Network Controller Rest Name>``  
      
6.  Check the BGP peering state to ensure that the SLB/MUX is peered to the Top-of-Rack (ToR) switch or RRAS virtual machine (the BGP peer). Run the following command from a network controller node virtual machine:  
      
    ``Debug-SlbConfigState``  
      
    Output from this command is saved at C:\Tools\SlbConfigState.txt. You can change this location with the ``-LogPath <Path>`` parameter.  
   
### Deploy a sample tenant workload with the software load balancer  
    
Now that fabric resources have been deployed, you can validate your SDN deployment end-to-end by deploying a sample tenant workload. This tenant workload consists of two virtual subnets (web tier and database tier) protected via Access Control List (ACL) rules using the SDN distributed firewall. The web tier's virtual subnet is accessible through the SLB/MUX using a Virtual IP (VIP) address. The script automatically deploys two web tier virtual machines and one database tier virtual machine and connects these to the virtual subnets.  
  
1.  Customize the SDNExpress\scripts\TenantConfig.psd1 file by changing the **<< Replace >>** tags with specific values (for example: VHD image name, network controller REST name, vSwitch Name, etc. as previously defined in the FabricConfig.psd1 file)  
2.  Run the script. For example:  
``SDNExpress\scripts\SDNExpressTenant.ps1 -ConfigurationDataFile TenantConfig.psd1 -Verbose``  
3.  To undo the configuration, run the same script with the **undo** parameter. For example:  
``SDNExpress\scripts\SDNExpressTenant.ps1 -Undo -ConfigurationDataFile TenantConfig.psd1 -Verbose``  

#### Validation  
To validate that the tenant deployment was successful, do the following:
1.	Log into the database tier virtual machine and try to ping the IP address of one of the web tier virtual machines (ensure Windows Firewall is turned off in web tier virtual machines).  
2.	Check the network controller tenant resources for any errors. Run the following from any Hyper-V host with Layer-3 connectivity to the network controller:  
	  
	``Debug-NetworkControllerConfigurationState -NCIP <FQDN of Network Controller REST Name>``  
	  
3.	Validate policy has been received and persisted in the Network Controller Host Agent  
	  
	``ovsdb-client.exe dump tcp:127.0.0.1:6641 ms_vtep``  
	  
4.	Check that an IP address has been assigned for a Provider Address (PA) Host vNIC and the ethernet adapters for the PA Host vNIC.  
	  
	``ipconfig /allcompartments /all``   
	  
5.	Check PA connectivity between two hosts using ping. Obtain the compartment ID from the output of the previous command (for example: Compartment 3)  
	  
	``ping -c <compartment Id> <Remote Hyper-V Host PA IP Address>``  
  
  
## Deploy a simulated tenant enterprise infrastructure  
  
1.  To deploy simulated tenant enterprise site gateways and virtual machines, open the **EnterpriseConfig.psd1** file in the Powershell ISE, and customize the enterprise gateway settings that you need for your environment. Make sure you specify the Routing Type that you want (**Dynamic** for BGP Routing, **Static** otherwise).  
  
2.  Run the **SDNExpressEnterpriseExample.ps1** script to deploy the Enterprise site Gateways and (optionally) clients:  
  
    ``  
    ./SDNExpressEnterpriseExample.ps1 -ConfigurationDataFile .\EnterpriseConfig.psd1 verbose  
    ``  
  
    This script creates the following:  
  
    -   One or more tenant enterprise sites with a VPN S2S Gateway per site, connected to the "Internet" network.  
  
    -   An internal tenant enterprise network switch for this site's internal connectivity.  
  
    -   A S2S VPN interface on this gateway with a destination to the gateway's public IP address and post connect IPv4 route to the service provider BGP router IPv4 address.  
  
    -   Installs a BGP router on the tenant enterprise site and creates a BGP Peer with the destination IP address at the service provider BGP router.  
  
3.  Now you can run the following cmdlets on the tenant enterprise gateways to check the state of network connections (and/or connect them):  
  
    -   `Get-VpnS2SInterface | Connect-VpnS2SInterface`  
  
    -   `Get-BgpRouter`  
  
    -   `Get-BgpPeer | Start-BgpPeer`  
  
    -   `Get-BgpRouteInformation`  
  
4.  To check if the end-to-end connectivity is up, try the following:  
  
    -   From one of the tenant enterprise gateways, ping the other tenant enterprise network.  
        
        For example: `ping 14.1.20.1 -S 14.1.10.1`  
  
    -   From one of the tenant enterprise gateways, try to establish an RDP connection with the WebTier virtual machine in the virtual network hosted at the service provider.  

        For example: `mstsc -v 192.168.0.10`  
  
        In this example, 192.168.0.10 is the DIP on one of the VNET VMs.  
  
5.  Optional - gateway failover scenario  
  
    To simulate a gateway failover scenario in M+N deployment mode, find out the currently active gateway for the tenant by using the following Windows PowerShell command: `Get-NCVirtualGateway -ResourceID <TenantName>`  
  
    Now log on to the gateway virtual machine and either shutdown the Remote Access service or shutdown the virtual machine to simulate failover. Check whether the tenant's virtual gateway has been re-provisioned on a standby Gateway virtual machine by running the above Windows PowerShell command again.  
  
This completes the configuration for SDN environment and the corresponding tenant enterprise sites.  
If you need to configure additional tenant enterprise sites or network connections, you can modify the corresponding configuration and run it again.  
  


