---
title: bitsadmin getproxylist
Retrieves the proxy list for the specified job.
description: "Windows Commands topic for **bitsadmin getproxylist** - Retrieves the proxy list for the specified job."
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: eebfa727-d8f1-4ae3-9382-6d8ffe8c3df3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
---
# bitsadmin getproxylist

>Applies To: Windows Server&reg; 2016, Windows Server&reg; 2012 R2, Windows Server&reg; 2012

Retrieves the proxy list for the specified job.
## Syntax
```
bitsadmin /GetProxylist <Job>
```
## Parameters
|Parameter|Description|
|-------|--------|
|Job|The job's display name or GUID|
## remarks
-   The proxy list is the list of proxy servers to use. The list is comma-delimited.
## <a name="BKMK_examples"></a>Examples
The following example retrieves the proxy list for the job named *myDownloadJob*.
```
C:\>bitsadmin /GetProxylist myDownloadJob
```
## additional references
[Command-Line Syntax Key](command-line-syntax-key.md)
