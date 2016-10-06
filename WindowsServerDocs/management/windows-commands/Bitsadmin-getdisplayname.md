---
title: Bitsadmin getdisplayname
description: "Windows Commands"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e5c0e76c-4cc6-42d8-ac30-30bf3dc11b9b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
---

# Bitsadmin getdisplayname

>Applies To: Windows Server&reg; 2016, Windows Server&reg; 2012 R2, Windows Server&reg; 2012

Retrieves the display name of the specified job.
## Syntax
```
bitsadmin /GetDisplayName <Job>
```
## Parameters
|Parameter|Description|
|-------------|---------------|
|Job|The job's display name or GUID|
## <a name="BKMK_examples"></a>Examples
The following example retrieves the display name for the job named *myDownloadJob*.
```
C:\>bitsadmin /GetDisplayName myDownloadJob
```
Additional references
[Command-Line Syntax Key](Command-Line-Syntax-Key.md)
