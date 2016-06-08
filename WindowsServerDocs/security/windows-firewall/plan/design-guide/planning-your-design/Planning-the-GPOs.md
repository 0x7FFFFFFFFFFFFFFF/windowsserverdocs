---
title: Planning the GPOs
ms.custom: na
ms.prod: windows-server-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - techgroup-networking
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f6fcc307-b97a-4918-ac76-a0754eae2155
---
# Planning the GPOs
When you plan the GPOs for your different isolation zones, you must complete the layout of the required zones and their mappings to the groups that link the computers to the zones.

## General considerations
A few things to consider as you plan the GPOs:

-   Do not allow a computer to be a member of more than one isolation zone. A computer in more than one zone receives multiple and possibly contradictory GPOs. This can result in unexpected, and difficult to troubleshoot behavior.

    The examples in this guide show GPOs that are designed to prevent the requirement to belong to multiple zones.

-   Ensure that the IPsec algorithms you specify in your GPOs are compatible across all the versions of Windows. The same principle applies to the data integrity and encryption algorithms. We recommend that you include the more advanced algorithms when you have the option of selecting several in an ordered list. The computers will negotiate down from the top of their lists, selecting one that is configured on both computers. So a computer that is running Windows Vista that is connected to a server that is running  Windows Server 2012  can communicate by using a much more secure algorithm.

-   The primary difference in your domain isolation GPOs is whether the rules request or require authentication.

    > [!CAUTION]
    > It is **critical** that you begin with all your GPOs set to request authentication instead of requiring it. Since the GPOs are delivered to the computers over time, applying a require policy to one computer breaks its ability to communicate with another computer that has not yet received its policy. Using request mode at the beginning enables computers to continue communicating by using plaintext connections if required. After you confirm that your computers are using IPsec where expected, you can schedule a conversion of the rules in the GPOs from requesting to requiring authentication, as required by each zone.

-   Windows Firewall with Advanced Security in Windows Vista and  Windows Server 2008  only support one network location profile at a time. If you add a second network adapter that is connected to a different network, or not connected at all, you could unintentionally change the profile that is currently active on the computer. If your GPO specifies different firewall and connection security rules based on the current network location profile, the behavior of how the computer handles network traffic will change accordingly. We recommend for stationary computers, such as desktops and servers, that you assign any rule for the computer to all profiles. Apply GPOs that change rules per network location to computers that must move between networks, such as your portable computers. Consider creating a separate domain isolation GPO for your servers that uses the same settings as the GPO for the clients, except that the server GPO specifies the same rules for all network location profiles. For more information, see Network Location Types at [http:\/\/go.microsoft.com\/fwlink\/?linkid\=110826](http://go.microsoft.com/fwlink/?linkid=110826).

    > [!NOTE]
    > Computers running Windows 8,  Windows 7 ,  Windows Server 2012 , and  Windows Server 2008 R2  support different network location types, and therefore profiles, for each network adapter at the same time. Each network adapter is assigned the network location appropriate for the network to which it is connected. Windows Firewall then enforces only those rules that apply to that network type’s profile. So certain types of traffic are blocked when coming from a network adapter connected to a public network, but those same types might be permitted when coming from a private or domain network.

After considering these issues, document each GPO that you require, and the details about the connection security and firewall rules that it needs.

## Woodgrove Bank example GPOs
The Woodgrove Bank example uses the following set of GPOs to support its domain isolation requirements. This section only discusses the rules and settings for server and domain isolation. GPO settings that affect which computers receive the GPO, such as security group filtering and WMI filtering, are discussed in the [Planning GPO Deployment](Planning-GPO-Deployment.md) section.

In this section you can find information about the following:

-   [Firewall GPOs](Firewall-GPOs.md)

-   [Isolated Domain GPOs](Isolated-Domain-GPOs.md)

-   [Boundary Zone GPOs](Boundary-Zone-GPOs.md)

-   [Encryption Zone GPOs](Encryption-Zone-GPOs.md)

-   [Server Isolation GPOs](Server-Isolation-GPOs.md)


