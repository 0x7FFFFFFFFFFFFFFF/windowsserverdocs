---
title: manage-bde: status
description: "Windows Commands topic for **** - "
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1444a360-fabf-4dd3-b67f-188e6ea3fa5b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
---
# manage-bde: status

>Applies To: Windows Server&reg; 2016, Windows Server&reg; 2012 R2, Windows Server&reg; 2012

Provides the following information about all drives on the computer; whether or not they are BitLocker-protected:
-   Size
-   BitLocker version
-   Conversion status
-   Percentage encrypted
-   Encryption method
-   Protection status
-   Lock status
-   Identification field
-   Key protectors
for examples of how this command can be used, see [Examples](#BKMK_Examples).
## Syntax
```
manage-bde -status [<Drive>] [-protectionaserrorlevel] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```
### Parameters
|Parameter|Description|
|-------|--------|
|<Drive>|Represents a drive letter followed by a colon.|
|-protectionaserrorlevel|Causes the manage-bde command-line tool to send the return code of 0 when the volume is protected and 1 when the volume is unprotected; most commonly used for batch scripts to determine if a drive is BitLocker-protected. You can also use **-p** as an abbreviated version of this command.|
|-computername|Specifies that manage-bde.exe will be used to modify BitLocker protection on a different computer. You can also use **-cn** as an abbreviated version of this command.|
|<Name>|Represents the name of the computer on which to modify BitLocker protection. Accepted values include the computer's NetBIOS name and the computer's IP address.|
|-? or /?|Displays brief help at the command prompt.|
|-help or -h|Displays complete help at the command prompt.|
## <a name="BKMK_Examples"></a>Examples
The following example illustrates using the **-status** command to display the status of drive C.
```
manage-bde  status C:
```
## additional references
-   [Command-Line Syntax Key](command-line-syntax-key.md)
-   [manage-bde](manage-bde.md)
