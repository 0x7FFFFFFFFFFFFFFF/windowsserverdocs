---
title: Bitsadmin getcompletiontime
description: "Windows Commands topic for **Bitsadmin getcompletiontime** - Retrieves the time that the job finished transferring data."
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7a4b3c1c-9832-4724-86b2-cce3c01bfa28
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
---
# Bitsadmin getcompletiontime

>Applies To: Windows Server&reg; 2016, Windows Server&reg; 2012 R2, Windows Server&reg; 2012

Retrieves the time that the job finished transferring data.
## Syntax
```
bitsadmin /GetCompletionTime <Job>
```
## Parameters
|Parameter|Description|
|-------|--------|
|Job|The job's display name or GUID|
## <a name="BKMK_examples"></a>Examples
The following example retrieves the time that the job named *myDownloadJob* finished transferring data.
```
C:\>bitsadmin /GetCompletionTime myDownloadJob
```
## Additional references
[Command-Line Syntax Key](Command-Line-Syntax-Key.md)
