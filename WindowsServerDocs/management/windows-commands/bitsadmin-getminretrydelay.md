---
title: bitsadmin getminretrydelay
description: "Windows Commands topic for **bitsadmin getminretrydelay** - 
Retrieves the length of time, in seconds, that the service waits after encountering a transient error before trying to transfer the file."
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
# bitsadmin getminretrydelay

>Applies To: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Retrieves the length of time, in seconds, that the service waits after encountering a transient error before trying to transfer the file.
## Syntax
```
bitsadmin /GetMinRetrydelay <Job>
```
## Parameters
|Parameter|Description|
|-------|--------|
|Job|The job's display name or GUID|
## <a name="BKMK_examples"></a>Examples
The following example retrieves the minimum retry delay for the job named *myDownloadJob*.
```
C:\>bitsadmin /GetMinRetrydelay myDownloadJob
```
## additional references
[Command-Line Syntax Key](command-line-syntax-key.md)
