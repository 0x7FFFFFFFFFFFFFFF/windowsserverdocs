---
title: Bitsadmin getminretrydelay
description: "Windows Commands"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 54f0abab-c129-40ed-a603-50f464d26011
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
---

# Bitsadmin getminretrydelay

>Applies To: Windows Server&reg; 2016, Windows Server&reg; 2012 R2, Windows Server&reg; 2012

Retrieves the length of time, in seconds, that the service waits after encountering a transient error before trying to transfer the file.
## Syntax
```
bitsadmin /GetMinRetryDelay <Job>
```
## Parameters
|Parameter|Description|
|-------------|---------------|
|Job|The job's display name or GUID|
## <a name="BKMK_examples"></a>Examples
The following example retrieves the minimum retry delay for the job named *myDownloadJob*.
```
C:\>bitsadmin /GetMinRetryDelay myDownloadJob
```
## Additional references
[Command-Line Syntax Key](Command-Line-Syntax-Key.md)
