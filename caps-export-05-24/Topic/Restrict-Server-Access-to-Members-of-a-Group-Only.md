---
title: Restrict Server Access to Members of a Group Only
ms.custom: na
ms.prod: windows-server-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - techgroup-networking
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8a372b8a-36a4-42f3-9f70-80f90de55d7f
author: vhorne
---
# Restrict Server Access to Members of a Group Only
After you have configured the IPsec connection security rules that force client computers to authenticate their connections to the isolated server, you must configure the rules that restrict access to only those computers or users who have been identified through the authentication process as members of the isolated server’s access group.  
  
The way in which you restrict access to the isolated server depends on which version of the Windows operating system the server is running.  
  
-   If the server is running [!INCLUDE[nextref_longhorn](../Token/nextref_longhorn_md.md)], [!INCLUDE[nextref_server_7](../Token/nextref_server_7_md.md)] or [!INCLUDE[win8_server_2](../Token/win8_server_2_md.md)], then you create a firewall rule that specifies the user and computer accounts that are allowed. The authentication method used in the connection must support the account type specified. Remember that only [!INCLUDE[win8_client_2](../Token/win8_client_2_md.md)], [!INCLUDE[nextref_client_7](../Token/nextref_client_7_md.md)], [!INCLUDE[nextref_vista](../Token/nextref_vista_md.md)], [!INCLUDE[win8_server_2](../Token/win8_server_2_md.md)], [!INCLUDE[nextref_longhorn](../Token/nextref_longhorn_md.md)], and [!INCLUDE[nextref_server_7](../Token/nextref_server_7_md.md)] support user\-based authentication.  
  
**Administrative credentials**  
  
To complete these procedures, you must be a member of the Domain Administrators group, or otherwise be delegated permissions to modify the GPOs.  
  
## <a name="bkmk_section1"></a>  
#### To create a firewall rule that grants access to an isolated server running Windows Server 2008 or later  
  
1.  [Open the Group Policy Management Console to Windows Firewall with Advanced Security](https://technet.microsoft.com/library/cc947816.aspx). You must edit the GPO that applies settings to servers in the isolated server zone.  
  
2.  In the navigation pane, right\-click **Inbound Rules**, and then click **New Rule**.  
  
3.  On the **Rule Type** page, click **Custom**, and then click **Next**.  
  
4.  If you must restrict access to a single network program, then you can select **This program path**, and specify the program or service to which to grant access. Otherwise, click **All programs**, and then click **Next**.  
  
5.  If you must restrict access to only some TCP or UDP port numbers, then enter the port numbers on the **Protocol and Ports** page. Otherwise, set **Protocol type** to **Any**, and then click **Next**.  
  
6.  On the **Scope** page, select **Any IP address** for both local and remote addresses, and then click **Next**.  
  
7.  On the **Action** page, click **Allow the connection if it is secure**. If required by your design, you can also click **Customize** and select **Require the connections to be encrypted**. Click **Next**.  
  
8.  On the **Users and Computers** page, select the check box for the type of accounts \(computer or user\) you want to allow, click **Add**, and then enter the group account that contains the computer and user accounts permitted to access the server.  
  
    > [!CAUTION]  
    > Remember that if you specify a user group on the Users page, your authentication scheme must include a method that uses user\-based credentials. User\-based credentials are only supported on versions of Windows that support AuthIP, such as [!INCLUDE[win8_client_2](../Token/win8_client_2_md.md)], [!INCLUDE[nextref_client_7](../Token/nextref_client_7_md.md)], [!INCLUDE[nextref_vista](../Token/nextref_vista_md.md)], [!INCLUDE[win8_server_2](../Token/win8_server_2_md.md)], [!INCLUDE[nextref_longhorn](../Token/nextref_longhorn_md.md)], and [!INCLUDE[nextref_server_7](../Token/nextref_server_7_md.md)]. Earlier versions of Windows and other operating systems that support IKE v1 only do not support user\-based authentication; computers running those versions or other operating systems will not be able to connect to the isolated server through this firewall rule.  
  
