---
title: Bitsadmin listfiles
description: "Windows Commands topic for **Bitsadmin listfiles** - Lists the files in the specified job."
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ad0d1eaa-3bd8-45e5-8f72-4da7366f0d59
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
---
# Bitsadmin listfiles

>Applies To: Windows Server&reg; 2016, Windows Server&reg; 2012 R2, Windows Server&reg; 2012

Lists the files in the specified job.
## Syntax
```
bitsadmin /ListFiles <Job>
```
## Parameters
|Parameter|Description|
|-------|--------|
|Job|The job's display name or GUID|
## <a name="BKMK_examples"></a>Examples
The following example retrieves the list of files for the job named *myDownloadJob*.
```
C:\>bitsadmin /GetNotifyFlags myDownloadJob
```
## Additional references
[Command-Line Syntax Key](Command-Line-Syntax-Key.md)
