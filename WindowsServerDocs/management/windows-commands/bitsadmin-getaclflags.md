---
title: bitsadmin getaclflags
description: "Windows Commands topic for **bitsadmin getaclflags** - Retrieves the access control list propagations flags."
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 99266def-7479-4430-a61c-98ec433fa88b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
---
# bitsadmin getaclflags

>Applies To: Windows Server&reg; 2016, Windows Server&reg; 2012 R2, Windows Server&reg; 2012

Retrieves the access control list propagations flags.
## Syntax
```
bitsadmin /GetAclFlags <Job>
```
## Parameters
|Parameter|Description|
|-------|--------|
|Job|The job's display name or GUID|
## remarks
Displays one or more of the following flag values:
-   O: copy owner information with file.
-   G: copy group information with file.
-   D: copy DACL information with file.
-   S: copy SACL information with file.
## <a name="BKMK_examples"></a>Examples
The following example retrieves the access control list propagation flags for the job named *myDownloadJob*.
```
C:\>bitsadmin /getaclflags myDownloadJob
```
## additional references
[Command-Line Syntax Key](command-line-syntax-key.md)
