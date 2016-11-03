---
title: bitsadmin info
description: "Windows Commands topic for **Displays summary information about the specified job.** - bitsadmin info"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5c306677-0d64-41c0-8276-5bba7750cecb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
---
# bitsadmin info

>Applies To: Windows Server&reg; 2016, Windows Server&reg; 2012 R2, Windows Server&reg; 2012

Displays summary information about the specified job.
## Syntax
```
bitsadmin /Info <Job> [/verbose]
```
## Parameters
|Parameter|Description|
|-------|--------|
|Job|The job's display name or GUID|
## remarks
Use the /verbose parameter to provide detailed information about the job.
## <a name="BKMK_examples"></a>Examples
The following example retrieves information about the job named *myDownloadJob*.
```
C:\>bitsadmin /Info myDownloadJob
```
## additional references
[Command-Line Syntax Key](command-line-syntax-key.md)
