---
title: Pushprinterconnections
description: "Windows Commands"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c30afb97-b149-478f-a4b9-2cbc25361818 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
---

# Pushprinterconnections

>Applies To: Windows Server&reg; 2016, Windows Server&reg; 2012 R2, Windows Server&reg; 2012

Reads Deployed Printer Connection settings from Group Policy, and deploys/removes printer connections as needed.  
## Syntax  
```  
pushprinterconnections <-log> <-?>  
```  
### Parameters  
|Parameter|Description|  
|-------------|---------------|  
|<-log>|Writes a per user debug log file to %temp, or writes a per machine debug log to %windir%\temp.|  
|<-?>|Displays Help at the command prompt.|  
## Remarks  
This utility is for use in machine startup or user logon scripts, and should not be run from the command line.  
## Additional references  
-   [Command-Line Syntax Key](Command-Line-Syntax-Key.md)  
-   [Deploy Printers by Using Group Policy](http://go.microsoft.com/fwlink/?LinkId=230627)  
