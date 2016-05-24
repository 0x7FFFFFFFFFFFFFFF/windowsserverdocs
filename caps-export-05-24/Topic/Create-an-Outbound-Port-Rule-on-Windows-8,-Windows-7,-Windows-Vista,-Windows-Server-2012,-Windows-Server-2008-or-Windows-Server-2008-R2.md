---
title: Create an Outbound Port Rule on Windows 8, Windows 7, Windows Vista, Windows Server 2012, Windows Server 2008 or Windows Server 2008 R2
ms.custom: na
ms.prod: windows-server-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - techgroup-networking
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: de7b0417-b07c-4c14-b16a-9495165e3feb
author: vhorne
---
# Create an Outbound Port Rule on Windows 8, Windows 7, Windows Vista, Windows Server 2012, Windows Server 2008 or Windows Server 2008 R2
By default, [!INCLUDE[wfas](../Token/wfas_md.md)] allows all outbound network traffic unless it matches a rule that prohibits the traffic. To block outbound network traffic on a specified TCP or UDP port number, use the [!INCLUDE[wfas](../Token/wfas_md.md)] node in the Group Policy Management MMC snap\-in to create firewall rules. This type of rule blocks any outbound network traffic that matches the specified TCP or UDP port numbers.  
  
**Administrative credentials**  
  
To complete these procedures, you must be a member of the Domain Administrators group, or otherwise be delegated permissions to modify the GPOs.  
  
### To create an outbound port rule  
  
1.  [Open the Group Policy Management Console to Windows Firewall with Advanced Security](../Topic/Open-the-Group-Policy-Management-Console-to-Windows-Firewall-with-Advanced-Security.md).  
  
2.  In the navigation pane, click **Outbound Rules**.  
  
3.  Click **Action**, and then click **New rule**.  
  
4.  On the **Rule Type** page of the New Outbound Rule wizard, click **Custom**, and then click **Next**.  
  
    > [!NOTE]  
    > Although you can create rules by selecting **Program** or **Port**, those choices limit the number of pages presented by the wizard. If you select **Custom**, you see all of the pages, and have the most flexibility in creating your rules.  
  
5.  On the **Program** page, click **All programs**, and then click **Next**.  
  
6.  On the **Protocol and Ports** page, select the protocol type that you want to block. To restrict the rule to a specified port number, you must select either **TCP** or **UDP**. Because this is an outbound rule, you typically configure only the remote port number.  
  
    If you select another protocol, then only packets whose protocol field in the IP header match this rule are blocked by Windows Firewall. Network traffic for protocols is allowed as long as other rules that match do not block it.  
  
    To select a protocol by its number, select **Custom** from the list, and then type the number in the **Protocol number** box.  
  
    When you have configured the protocols and ports, click **Next**.  
  
7.  On the **Scope** page, you can specify that the rule applies only to network traffic to or from the IP addresses entered on this page. Configure as appropriate for your design, and then click **Next**.  
  
8.  On the **Action** page, select **Block the connection**, and then click **Next**.  
  
9. On the **Profile** page, select the network location types to which this rule applies, and then click **Next**.  
  
    > [!NOTE]  
    > If this GPO is targeted at server computers running [!INCLUDE[nextref_longhorn](../Token/nextref_longhorn_md.md)] that never move, consider applying the rules to all network location type profiles. This prevents an unexpected change in the applied rules if the network location type changes due to the installation of a new network card or the disconnection of an existing network card’s cable. A disconnected network card is automatically assigned to the Public network location type.  
  
10. On the **Name** page, type a name and description for your rule, and then click **Finish**.  
  
If you arrived at this page by clicking a link in a checklist, use your browser’s **Back** button to return to the checklist.  
  
