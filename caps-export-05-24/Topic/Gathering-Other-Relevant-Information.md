---
title: Gathering Other Relevant Information
ms.custom: na
ms.prod: windows-server-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - techgroup-networking
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 15513023-96d9-4f9f-a799-8a20319681e6
author: vhorne
---
# Gathering Other Relevant Information
This topic discusses several other things that you should examine to see whether they will cause any complications in your ability to deploy [!INCLUDE[wfas](../Token/wfas_md.md)] policies in your organization.  
  
## Capacity considerations  
Because IPsec uses mathematically intensive cryptographic techniques, it can consume significant overhead on a computer. Areas to watch:  
  
-   **Encryption.** You might use 256\-bit Advanced Encryption Standard \(AES\-256\) and 384\-bit Secure Hash Algorithm \(SHA\-384\) to check integrity in situations that require the strongest available encryption and key exchange protection. If you have NICs that support IPsec Task Offload, you can reduce the effect that encryption has on network throughput. For more information, see [IPsec Task Offload](http://technet.microsoft.com/network/dd277647.aspx) at http:\/\/technet.microsoft.com\/network\/dd277647.aspx  
  
-   **Security association \(SA\) negotiation.** You can use a shorter lifetime for the main mode SA, such as three hours, but then you might need  to make tradeoffs. Because each main mode SA occupies approximately 5  KB of RAM, situations in which a server brokers tens of thousands of concurrent connections can lead to overutilization.  
  
-   **NAT devices.** As discussed earlier, NAT does not allow Authentication Header \(AH\) conversations between hosts. If NAT devices exist on the internal network, ESP must be selected instead of AH.  
  
-   **Switches and routers.** Proper capacity planning for the implementation of IPsec is more about thorough testing and expected traffic loads than exact calculations. You might have to upgrade or reconfigure switches or routers that currently exceed 75 percent usage to allow for increased traffic on the device and still provide some extra usage for bursts of traffic.  
  
-   **Other factors.** These include CPU usage on network infrastructure servers, increased overhead on servers and workstations running IPsec \(especially servers, because they usually contain more main mode SAs than clients\), and increased network latency because of IPsec negotiation.  
  
    > [!NOTE]  
    > When Microsoft deployed its own domain isolation solution, it found a one to three percent increase in usage on the network as a direct result of IPsec.  
  
## Group Policy deployment groups and WMI filters  
You do not have to rearrange the organization unit \(OU\) hierarchy of your Active Directory domains to effectively deploy [!INCLUDE[wfas](../Token/wfas_md.md)] GPOs. Instead, you can link your GPOs at the domain level \(or another high level container\), and then use security group filtering or WMI filtering to ensure that only the appropriate computers or users can apply the GPO settings. Because the firewall and connection security rules have evolved significantly from Windows 2000 Server to Windows XP and Windows Server 2003, and now with [!INCLUDE[win8_client_2](../Token/win8_client_2_md.md)], [!INCLUDE[nextref_client_7](../Token/nextref_client_7_md.md)], [!INCLUDE[nextref_vista](../Token/nextref_vista_md.md)], [!INCLUDE[win8_server_2](../Token/win8_server_2_md.md)], [!INCLUDE[nextref_longhorn](../Token/nextref_longhorn_md.md)], and [!INCLUDE[nextref_server_7](../Token/nextref_server_7_md.md)], we recommend that you use WMI filtering to dynamically ensure that GPOs apply only to computers that are running the correct operating system. It is not necessary to use this technique if your network consists of computers running [!INCLUDE[nextref_vista](../Token/nextref_vista_md.md)] or later.  
  
## Different Active Directory trust environments  
When you design a domain isolation policy, consider any logical boundaries that might affect IPsec\-secured communications. For example, the trust relationships between your domains and forests are critical in determining an appropriate IKE authentication method.  
  
Kerberos V5 authentication is recommended for use in a two\-way \(mutual\) domain and forest trust environment. You can use Kerberos V5 for IKE authentication across domains that have two\-way trusts established, if the domains are in the same forest or different forests. If the two domains are in different forests, you must configure two external trusts, one for each direction, between the domains. The external trusts must use the fully qualified domain name \(FQDN\) of the domains, and IPsec policy must allow an IKE initiator in one domain to communicate with any domain controller in the forest domain hierarchy, so that the initiator can obtain a Kerberos V5 ticket from a domain controller in the responder’s domain. If firewalls separate the domains then you must configure the firewall to allow Kerberos V5 traffic over UDP destination port 88, TCP destination port 88, and UDP destination port 389.  
  
For more information, see "Active Directory in Networks Segmented by Firewalls" at [http:\/\/go.microsoft.com\/fwlink\/?LinkId\=45087](http://go.microsoft.com/fwlink/?LinkId=45087).  
  
If the use of Kerberos V5 authentication is not possible because two\-way trusts across forests cannot be established as in some large enterprise environments, you can use a public key infrastructure \(PKI\) and digital certificates to establish IPsec\-trusted communication. For an example of how Microsoft deployed their PKI, see "Deploying PKI Inside Microsoft" at [http:\/\/go.microsoft.com\/fwlink\/?LinkId\=45088](http://go.microsoft.com/fwlink/?LinkId=45088).  
  
## Creating firewall rules to permit IKE, AH, and ESP traffic  
In some cases, IPsec\-secured traffic might have to pass through a router, perimeter firewall, or other filtering device. In the case of a router, unless the router filters TCP and UDP traffic or other upper\-level protocol headers, no special configuration is required to allow the IPsec traffic to be forwarded.  
  
In the case of a filtering router or a firewall, you must configure these devices to allow IPsec traffic to be forwarded. Configure the firewall to allow IPsec traffic on UDP source and destination port 500 \(IKE\), UDP source and destination port 4500 \(IPsec NAT\-T\), and IP Protocol 50 \(ESP\). You might also have to configure the firewall to allow IPsec traffic on IP protocol 51 \(AH\) to allow troubleshooting by IPsec administrators and to allow the IPsec traffic to be inspected.  
  
For more information, see "How to Enable IPsec Traffic Through a Firewall" at [http:\/\/go.microsoft.com\/fwlink\/?LinkId\=45085](http://go.microsoft.com/fwlink/?LinkId=45085).  
  
## Network load balancing and server clusters  
There are challenges implementing connection security for network traffic going to and from network load balancing \(NLB\) clusters and server clusters. NLB enables multiple servers to be clustered together to provide high availability for a service by providing automatic failover to other nodes in the cluster. Because IPsec matches a security association to a specific computer, it prevents different computers from handling the same client connection. If a different node in the cluster responds to an IPsec connection that was originally established by another node, the traffic will be dropped by the client computer as untrusted.  
  
This means that NLB in "no affinity" mode is not supported by IPsec at all. If you must use "no affinity" mode in the cluster then consider including the servers that make up the cluster in your IPsec exemption group, and allowing clients to communicate with the servers without IPsec.  
  
**IPsec improvements for clusters running Windows Server 2008**  
  
Starting with [!INCLUDE[nextref_longhorn](../Token/nextref_longhorn_md.md)] and [!INCLUDE[nextref_vista](../Token/nextref_vista_md.md)], IPsec is much more tightly integrated into TCP\/IP than in earlier versions of Windows. When a TCP connection is dropped because of a cluster node failover, IPsec on a computer that is running [!INCLUDE[win8_client_2](../Token/win8_client_2_md.md)], [!INCLUDE[nextref_client_7](../Token/nextref_client_7_md.md)], [!INCLUDE[nextref_vista](../Token/nextref_vista_md.md)], [!INCLUDE[win8_server_2](../Token/win8_server_2_md.md)], [!INCLUDE[nextref_longhorn](../Token/nextref_longhorn_md.md)], and [!INCLUDE[nextref_server_7](../Token/nextref_server_7_md.md)] detects the TCP connection failure and removes the IPsec SAs for that connection. When the new TCP connection is established to another node, IPsec can negotiate new SAs immediately without having to wait for the obsolete SAs to time out.  
  
## Network inspection technologies  
Within a TCP\/IP packet, IPsec without encryption changes the offsets for the destination ports and protocols. These changes can adversely affect applications that are running on network devices such as routers that monitor and manage traffic on the network. While some network applications have been updated to support IPsec, some are not yet compatible. Check with the vendor of your device to see whether the changes in the protocol and port fields caused by IPsec are compatible with the device.  
  
Any device designed to view network traffic, such as hardware protocol analyzers or Microsoft Network Monitor, cannot parse ESP\-encrypted traffic. Only the destination computer, with which the originating computer negotiated the connection, can decrypt the traffic.  
  
In general, IPsec defeats network\-based prioritization and port\- or protocol\-based traffic management. For encrypted packets, there is no workaround; the host itself must handle any traffic management functions. For unencrypted, authenticated\-only packets, the devices and applications must be aware of how IPsec changes packets to be able to do anything with them other than route them to the correct host. If you cannot upgrade monitoring or management devices to support IPsec, it is important that you record this information and figure it into your domain or server isolation design.  
  
Network Monitor includes parsers for the ISAKMP \(IKE\), AH, and ESP protocols. Network Monitor parsers for ESP can parse inside the ESP packet only if ESP null\-encryption is being used. Network Monitor cannot parse the encrypted parts of IPsec ESP traffic when encryption is performed in software. However, if encryption is performed by an IPsec hardware offload network adapter, the ESP packets can be decrypted when Network Monitor captures them on either the source or the destination and, therefore, they can be parsed. To diagnose ESP software\-encrypted communication, you must disable ESP encryption and use ESP\-null encryption by changing the IPsec policy or connection security rule on both computers.  
  
Network Monitor is available as a free download from Microsoft at [http:\/\/go.microsoft.com\/fwlink\/?linkid\=94770](http://go.microsoft.com/fwlink/?linkid=94770).  
  
**Next:**[Determining the Trusted State of Your Computers](../Topic/Determining-the-Trusted-State-of-Your-Computers.md)  
  
