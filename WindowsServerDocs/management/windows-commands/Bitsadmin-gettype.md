---
title: Bitsadmin gettype
description: "Windows Commands topic for **Bitsadmin gettype** - Retrieves the job type of the specified job."
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bec16f04-3e95-4587-889e-3de6ad03c9c8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
---
# Bitsadmin gettype

>Applies To: Windows Server&reg; 2016, Windows Server&reg; 2012 R2, Windows Server&reg; 2012

Retrieves the job type of the specified job.
## Syntax
```
bitsadmin /GetType <Job>
```
## Parameters
|Parameter|Description|
|-------|--------|
|Job|The job's display name or GUID|
## Remarks
The type can be DOWNLOAD, UPLOAD, UPLOAD-REPLY, or UNKNOWN.
## <a name="BKMK_examples"></a>Examples
The following example retrieves the job type for the job named *myDownloadJob*.
```
C:\>bitsadmin /GetType myDownloadJob
```
## Additional references
[Command-Line Syntax Key](Command-Line-Syntax-Key.md)
