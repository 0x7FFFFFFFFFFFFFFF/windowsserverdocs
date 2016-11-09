---
title: manage-bde: changepassword
description: "Windows Commands topic for **** - "
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b174e152-8442-4fba-8b33-56a81ff4f547
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
---
# manage-bde: changepassword

>Applies To: Windows Server&reg; 2016, Windows Server&reg; 2012 R2, Windows Server&reg; 2012

Modifies the password for a data drive. The user is prompted for a new password. For examples of how this command can be used, see [Examples](#BKMK_Examples).
## Syntax
```
manage-bde -changepassword [<Drive>] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```
### Parameters
|Parameter|Description|
|-------|--------|
|<Drive>|Represents a drive letter followed by a colon.|
|-computername|Specifies that manage-bde.exe will be used to modify BitLocker protection on a different computer. You can also use **-cn** as an abbreviated version of this command.|
|<Name>|Represents the name of the computer on which to modify BitLocker protection. Accepted values include the computer's NetBIOS name and the computer's IP address.|
|-? or /?|Displays brief help at the command prompt.|
|-help or -h|Displays complete help at the command prompt.|
## <a name="BKMK_Examples"></a>Examples
The following example illustrates using the **-changepassword** command to change the password used to unlock BitLocker on data drive D.
```
manage-bde  changepassword D:
```
## additional references
-   [Command-Line Syntax Key](command-line-syntax-key.md)
-   [manage-bde](manage-bde.md)
