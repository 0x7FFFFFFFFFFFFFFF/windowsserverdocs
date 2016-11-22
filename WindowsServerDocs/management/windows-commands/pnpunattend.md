---
title: pnpunattend
description: "Windows Commands topic for **** - "
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4fa88932-cff0-4dfc-936c-98c0e3dfbeb8 britw
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
---
# pnpunattend

>Applies To: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Audits a computer for device drivers, and perform unattended driver installations, or search for drivers without installing and, optionally, report the results to the command line. Use this command to specify the installation of specific drivers for specific hardware devices. See remarks.  
## Syntax  
```  
pnpunattend.exe auditSystem [/help] [/?] [/h] [/s] [/L]  
```  
## Parameters  
|Parameter|Description|  
|-------|--------|  
|auditSystem|Specifies online driver install.<br /><br />Required, except when pnpunattend is run with either the **/help** or **/?** parameters.|  
|/s|Optional. Specifies to search for drivers without installing.|  
||Optional. Specifies to display the log information for this command in the command prompt.|  
|/?|Optional. Displays help for this command at the command prompt.|  
## remarks  
Preliminary preparation is required. Prior to using this command, you must complete the following tasks:  
1.  Create a directory for the drivers you want to install. For example, create a folder at **C:\Drivers\Video** for video adapter drivers.  
2.  Download and extract the driver package for your device. Copy the contents of the subfolder that contains the INF file for your version of the operating system and any subfolders to the video folder that you created. For example, copy the video driver files to C:\Drivers\Video.  
3.  Add a system environment path variable to the folder you created in step 1.for example, **C:\Drivers\Video**.  
4.  Create the following registry key, and then for the **Driverpaths** key you create, set the **Value Data** to **1**.  
-   For  Windows 7   navigate the registry path: **HKEY_LOCAL_Machine\Software\Microsoft\Windows NT\Currentversion\\**, and then create the keys: **UnattendSettings\pnpunattend\Driverpaths\\**  
-   For Windows Vista, navigate to the registry path: **HK_LM\Software\Microsoft\Windows NT\Currentversion\\**, and then create the keys = **\UnattendSettings\pnpunattend\Driverpaths**.  
## Examples  
The following example command shows how to use the **pnpunattend.exe** to audit a computer for possible driver updates, and then report the findings to the Command prompt.  
```  
pnpunattend auditsystem /s /l   
```  
## additional references  
[Command-Line Syntax Key](command-line-syntax-key.md)  
