---
title: Work Folders Overview
ms.custom: na
ms.prod: windows-server-2012-r2
ms.reviewer: na
ms.suite: na
ms.technology: 
  - techgroup-storage
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 46e5bf69-b9cc-4dcb-bfd3-6f1036076cbf
author: JasonGerend
---
# Work Folders Overview
This topic discusses Work Folders, which is a role service for file servers running Windows Server that provides a consistent way for users to access their work files from their PCs and devices.  
  
**Did you mean…**  
  
-   [Work Folders for Windows 7 \(64 bit download\)](http://www.microsoft.com/download/details.aspx?id=42558)  
  
-   [Work Folders for Windows 7 \(32 bit download\)](http://www.microsoft.com/download/details.aspx?id=42559)  
  
-   [Work Folders in Windows 10](http://windows.microsoft.com/en-us/windows-10/work-folders-in-windows-10)  
  
-   [Work Folders FAQ: Windows 8.1 Help](http://windows.microsoft.com/en-us/windows-8/work-folders-faq)  
  
-   [Work Folders iPhone and iPad app: FAQ](http://windows.microsoft.com/en-us/windows/work-folders-ipad-faq)  
  
## In this topic  
  
-   [Role description](../Topic/Work-Folders-Overview.md#BKMK_OVER)  
  
-   [Practical applications](../Topic/Work-Folders-Overview.md#BKMK_APP)  
  
-   [Important functionality](#BKMK_NEW)  
  
-   [New and changed functionality](#BKMK_New)  
  
-   [Software requirements](../Topic/Work-Folders-Overview.md#BKMK_SOFT)  
  
-   [Work Folders compared to other sync technologies](../Topic/Work-Folders-Overview.md#BKMK_Comparison)  
  
-   [Server Manager information](../Topic/Work-Folders-Overview.md#BKMK_INSTALL)  
  
-   [Interoperability with Windows Azure virtual machines](../Topic/Work-Folders-Overview.md#BKMK_Azure)  
  
-   [See also](../Topic/Work-Folders-Overview.md#BKMK_LINKS)  
  
## <a name="BKMK_OVER"></a>Role description  
With Work Folders users can store and access work files on personal computers and devices, often referred to as bring\-your\-own device \(BYOD\), in addition to corporate PCs. Users gain a convenient location to store work files, and they can access them from anywhere. Organizations maintain control over corporate data by storing the files on centrally managed file servers, and optionally specifying user device policies such as encryption and lock\-screen passwords.  
  
Work Folders can be deployed with existing deployments of Folder Redirection, Offline Files, and home folders. Work Folders stores user files in a folder on the server called a *sync share*. You can specify a folder that already contains user data, which enables you to adopt Work Folders without migrating servers and data or immediately phasing out your existing solution.  
  
## <a name="BKMK_APP"></a>Practical applications  
Administrators can use Work Folders to provide users with access to their work files while keeping centralized storage and control over the organization’s data. Some specific applications for Work Folders include:  
  
-   Provide a single point of access to work files from a user’s work and personal computers and devices  
  
-   Access work files while offline, and then sync with the central file server when the PC or device next has Internet or intranet connectivity  
  
-   Deploy with existing deployments of Folder Redirection, Offline Files, and home folders  
  
-   Use existing file server management technologies, such as file classification and folder quotas, to manage user data  
  
-   Specify security policies to instruct user’s PCs and devices to encrypt Work Folders and use a lock screen password  
  
-   Use Failover Clustering with Work Folders to provide a high\-availability solution  
  
## <a name="BKMK_NEW"></a>Important functionality  
Work Folders includes the following functionality.  
  
|Functionality|Availability|Description|  
|-----------------|----------------|---------------|  
|Work Folders role service in Server Manager|[!INCLUDE[winblue_server_2](../Token/winblue_server_2_md.md)]|File and Storage Services provides a way to set up sync shares \(folders that store user’s work files\), monitors Work Folders, and manages sync shares and user access|  
|Work Folders cmdlets|[!INCLUDE[winblue_server_2](../Token/winblue_server_2_md.md)]|A Windows PowerShell module that contains comprehensive cmdlets for managing Work Folders servers|  
|Work Folders integration with Windows|[!INCLUDE[winblue_client_2](../Token/winblue_client_2_md.md)]<br /><br />[!INCLUDE[winblue_winrt_2](../Token/winblue_winrt_2_md.md)]<br /><br />Windows 7 \(download required\)|Work Folders provides the following functionality in Windows computers:<br /><br />-   A Control Panel item that sets up and monitors Work Folders<br />-   File Explorer integration that enables easy access to files in Work Folders<br />-   A sync engine that transfers files to and from a central file server while maximizing battery life and system performance|  
|Work Folders app for devices|Apple iPhone and iPad®|An app that allows popular devices to access files in Work Folders|  
  
## <a name="BKMK_New"></a>New and changed functionality  
The following table describes some of the major changes in Work Folders.  
  
|Feature\/functionality|New or updated?|Description|  
|--------------------------|-------------------|---------------|  
|Faster change replication|Updated in Windows 10|In Windows 8.1, file changes get uploaded to the server once the file is closed, but other devices aren’t notified of the change, and can wait up to 10 minutes to get the change. In Windows 10, the Work Folders server immediately notifies client PCs and devices of the change so that the changes are synced immediately.|  
|Integrated with Enterprise data protection \(EDP\) policy|Added to Windows 10 in  November 2015 update|If an administrator deploys EDP, Work Folders can enforce data protection by encrypting the data on the PC. The encryption is using a key associated with the Enterprise ID, which can be remotely wiped by using a supported mobile device management package such as Microsoft Intune.|  
|Microsoft Office integration|Added to Windows 10 in  November 2015 update|In Windows 8.1 you can navigate to Work Folders inside Office apps by clicking or tapping This PC and then navigating to the Work Folders location on your PC. In Windows 10 you can make it even easier to get to Work Folders by adding it to the list of locations that Office shows when saving or opening files. For more info, see [Work Folders in Windows 10](http://windows.microsoft.com/en-us/windows-10/work-folders-in-windows-10) and  [Troubleshooting using Work Folders as a Place in Microsoft Office](http://social.technet.microsoft.com/wiki/contents/articles/32881.troubleshooting-using-work-folders-as-a-place-in-microsoft-office.aspx).|  
  
## <a name="BKMK_SOFT"></a>Software requirements  
Work Folders has the following software requirements for file servers and your network infrastructure:  
  
-   A server running [!INCLUDE[winblue_server_2](../Token/winblue_server_2_md.md)] for hosting sync shares with user files  
  
-   A volume formatted with the NTFS file system for storing user files  
  
-   To enforce password policies on Windows 7 PCs, you must use Group Policy password policies. You also have to exclude the Windows 7 PCs from Work Folders password policies \(if you use them\).  
  
To enable users to sync across the Internet, there are additional requirements:  
  
-   A server certificate for each file server that will host Work Folders \(plus a server certificate for your reverse proxy server\). These certificates should be from a certification authority \(CA\) that is trusted by your users—ideally a public CA  
  
-   The ability to make a server accessible from the Internet by creating publishing rules in your organization’s reverse proxy or network gateway  
  
-   A publicly registered domain name and the ability to create additional public DNS records for the domain  
  
-   \(Optional\) An Active Directory Domain Services forest with schema extensions in [!INCLUDE[winblue_server_2](../Token/winblue_server_2_md.md)] to support automatically referring PCs and devices to the correct file server when using multiple file servers  
  
-   \(Optional\) Active Directory Federation Services \(AD FS\) infrastructure when using AD FS authentication  
  
Work Folders has the following software requirements for client computers:  
  
-   PCs and devices must be running one of the following operating systems:  
  
    -   [!INCLUDE[winblue_client_2](../Token/winblue_client_2_md.md)]  
  
    -   [!INCLUDE[winblue_winrt_2](../Token/winblue_winrt_2_md.md)]  
  
    -   Windows 7  
  
    -   iOS 8 on an Apple iPad  
  
-   Windows 7 PCs must be running one of the following editions of Windows:  
  
    -   Windows 7 Professional  
  
    -   Windows 7 Ultimate  
  
    -   Windows 7 Enterprise  
  
-   Windows 7 PCs must be joined to your organization’s domain \(they can’t be joined to a workgroup\).  
  
-   Enough free space on a local, NTFS\-formatted drive to store all the user’s files in Work Folders, plus an additional 6 GB of free space if Work Folders is located on the system drive, as it is by default. Work Folders uses the following location by default: **%USERPROFILE%\\Work Folders**  
  
    However, users can change the location during setup \(microSD cards and USB drives formatted with the NTFS file system are supported locations, though sync will stop if the drives are removed\).  
  
    The maximum size for individual files is 10 GB by default. There is no per\-user storage limit, although administrators can use the quotas functionality of File Server Resource Manager to implement quotas.  
  
-   Work Folders doesn’t support rolling back the virtual machine state of client virtual machines. Instead perform backup and restore operations from inside the client virtual machine by using System Image Backup or another backup app.  
  
## <a name="BKMK_Comparison"></a>Work Folders compared to other sync technologies  
The following table discusses how various Microsoft sync technologies are positioned and when to use each.  
  
||Work Folders|Offline Files|OneDrive for Business|OneDrive|  
|-|----------------|-----------------|-------------------------|------------|  
|**Technology summary**|Syncs files that are stored on a file server with PCs and devices|Syncs files that are stored on a file server with PCs that have access to the corporate network \(can be replaced by Work Files\)|Syncs files that are stored in Office 365 or in SharePoint with PCs and devices inside or outside a corporate network, and provides document collaboration functionality|Syncs personal files that are stored in OneDrive with PCs, Mac computers, and devices|  
|**Intended to provide user access to work files**|Yes|Yes|Yes|No|  
|**Cloud service**|None|None|Office 365|Microsoft OneDrive|  
|**Internal network servers**|File servers running [!INCLUDE[winblue_server_2](../Token/winblue_server_2_md.md)]|File servers|SharePoint server \(optional\)|None|  
|**Supported clients**|PCs and iPads inside or outside a corporate network|PCs in a corporate network or connected through DirectAccess, VPNs, or other remote access technologies|PCs, iOS, Android, Windows Phone|PCs, Mac computers, Windows Phone, iOS, Android|  
  
> [!NOTE]  
> In addition to the sync technologies listed in the previous table, Microsoft offers other replication technologies, including DFS Replication, which is designed for server\-to\-server replication, and BranchCache, which is designed as a branch office WAN acceleration technology. For more information, see [DFS Namespaces and DFS Replication Overview](../Topic/DFS-Namespaces-and-DFS-Replication-Overview.md) and [BranchCache Overview](assetId:///e25ed2da-80d0-4f32-8518-a736ad806272)  
  
## <a name="BKMK_INSTALL"></a>Server Manager information  
Work Folders is part of the File and Storage Services role. You can install Work Folders by using the Add Roles and Features Wizard or the `Install-WindowsFeature` cmdlet. Both methods accomplish the following:  
  
-   Adds the **Work Folders** page to **File and Storage Services** in Server Manager  
  
-   Installs the Windows Sync Shares service, which is used by Windows Server to host sync shares  
  
-   Installs the SyncShare Windows PowerShell module to manage Work Folders on the server  
  
## <a name="BKMK_Azure"></a>Interoperability with Windows Azure virtual machines  
You can run this Windows Server role service on a virtual machine in Windows Azure. This scenario has been tested with [!INCLUDE[winblue_server_2](../Token/winblue_server_2_md.md)].  
  
To learn about how to get started with Windows Azure virtual machines, visit the [Windows Azure web site](http://www.windowsazure.com/en-us/documentation/services/virtual-machines).  
  
## <a name="BKMK_LINKS"></a>See also  
For additional related information, see the following resources.  
  
|Content type|References|  
|----------------|--------------|  
|**Product evaluation**|-   [Work Folders for iOS – iPad App Release](http://blogs.technet.com/b/filecab/archive/2015/01/16/work-folders-for-ios-ipad-app-release.aspx) \(blog post\)<br />-   [Introducing Work Folders on Windows Server 2012 R2](http://blogs.technet.com/b/filecab/archive/2013/07/09/introducing-work-folders-on-windows-server-2012-r2.aspx) \(blog post\)<br />-   [Introduction to Work Folders](http://channel9.msdn.com/posts/Introduction-to-Work-Folders) \(Channel 9 Video\)<br />-   [Work Folders Test Lab Deployment](http://blogs.technet.com/b/filecab/archive/2013/07/10/work-folders-test-lab-deployment.aspx) \(blog post\)<br />-   [Work Folders for Windows 7](http://blogs.technet.com/b/filecab/archive/2014/04/24/work-folders-for-windows-7.aspx) \(blog post\)|  
|**Deployment**|-   [Designing a Work Folders Implementation](../Topic/Designing-a-Work-Folders-Implementation.md)<br />-   [Deploying Work Folders](../Topic/Deploying-Work-Folders.md)<br />-   [Performance Considerations for Work Folders Deployments](http://blogs.technet.com/b/filecab/archive/2013/11/01/performance-considerations-for-large-scale-work-folders-deployments.aspx)<br />-   [Work Folders for Windows 7 \(64 bit download\)](http://www.microsoft.com/download/details.aspx?id=42558)<br />-   [Work Folders for Windows 7 \(32 bit download\)](http://www.microsoft.com/download/details.aspx?id=42559)|  
|**Operations**|-   [Work Folders iPad app: FAQ](http://windows.microsoft.com/en-us/windows/work-folders-ipad-faq) \(for users\)<br />-   [Work Folders Certificate Management](http://blogs.technet.com/b/filecab/archive/2013/08/09/work-folders-certificate-management.aspx) \(blog post\)<br />-   [Monitoring Windows Server 2012 R2 Work Folders Deployments](http://blogs.technet.com/b/filecab/archive/2013/10/15/monitoring-windows-server-2012-r2-work-folders-deployments.aspx) \(blog post\)<br />-   [SyncShare \(Work Folders\) Cmdlets in Windows PowerShell](http://technet.microsoft.com/library/dn296644.aspx)<br />-   [Storage and File Services PowerShell Cmdlets Quick Reference Card For Windows Server 2012 R2 Preview Edition](http://blogs.technet.com/b/filecab/archive/2013/07/30/storage-and-file-services-powershell-cmdlets-quick-reference-card-for-windows-server-2012-r2-preview-edition.aspx)|  
|**Troubleshooting**|-   [Windows Server 2012 R2 – Resolving Port Conflict with IIS Websites and Work Folders](http://blogs.technet.com/b/filecab/archive/2013/10/15/windows-server-2012-r2-resolving-port-conflict-with-iis-websites-and-work-folders.aspx) \(blog post\)<br />-   [Common Errors in Work Folders](http://social.technet.microsoft.com/wiki/contents/articles/30578.common-errors-in-work-folders.aspx)|  
|**Community resources**|-   [File Services and Storage Forum](http://social.technet.microsoft.com/Forums/windowsserver/home?forum=winserverfiles)<br />-   [The Storage Team at Microsoft \- File Cabinet Blog](http://blogs.technet.com/b/filecab/)<br />-   [Ask the Directory Services Team Blog](http://blogs.technet.com/b/askds/)|  
|**Related technologies**|-   [File and Storage Services Overview](../Topic/File-and-Storage-Services-Overview.md)<br />-   [File Server Resource Manager Overview_1](../Topic/File-Server-Resource-Manager-Overview_1.md)<br />-   [Folder Redirection, Offline Files, and Roaming User Profiles overview](../Topic/Folder-Redirection,-Offline-Files,-and-Roaming-User-Profiles-overview.md)<br />-   [BranchCache Overview](assetId:///a92ec0b2-eb08-4fe7-b6a6-d140e0f55fd5)<br />-   [DFS Namespaces and DFS Replication Overview](../Topic/DFS-Namespaces-and-DFS-Replication-Overview.md)|  
  
