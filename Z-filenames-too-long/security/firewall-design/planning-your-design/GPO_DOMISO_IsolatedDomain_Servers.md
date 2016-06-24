---
title: GPO_DOMISO_IsolatedDomain_Servers
ms.custom: na
ms.prod: windows-server-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - techgroup-networking
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2647cd2b-209e-4358-b700-249db528b787
---
# GPO_DOMISO_IsolatedDomain_Servers
This GPO is authored by using the Windows Firewall with Advanced Security interface in the Group Policy editing tools. The User Configuration section of the GPO is disabled. It is intended to only apply to server computers that are running  Windows Server 2012 ,  Windows Server 2008  or  Windows Server 2008 R2 .

Because so many of the settings and rules for this GPO are common to those in the GPO for Windows 8,  Windows 7  and Windows Vista, you can save time by exporting the Windows Firewall with Advanced Security piece of the GPO for Windows 8,  Windows 7  and Windows Vista, and importing it to the GPO for  Windows Server 2012 ,  Windows Server 2008  and  Windows Server 2008 R2 . After the import, change only the items specified here:

-   This GPO applies all its settings to all profiles: Domain, Private, and Public. Because a server is not expected to be mobile and changing networks, configuring the GPO in this way prevents a network failure or the addition of a new network adapter from unintentionally switching the computer to the Public profile with a different set of rules (in the case of a server running  Windows Server 2008 ).

    > [!IMPORTANT]
    > Windows Vista and  Windows Server 2008  support only one network location profile at a time. The profile for the least secure network type is applied to the computer. If you attach a network adapter to a computer that is not physically connected to a network, the public network location type is associated with the network adapter and applied to the computer.

**Next:**[Boundary Zone GPOs](Boundary-Zone-GPOs.md)


