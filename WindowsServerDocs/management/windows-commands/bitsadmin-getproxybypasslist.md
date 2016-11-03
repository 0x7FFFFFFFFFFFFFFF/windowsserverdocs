---
title: bitsadmin getproxybypasslist
description: "Windows Commands topic for **bitsadmin getproxybypasslist** - Retrieves the proxy bypass list for the specified job."
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 50959be3-7014-4bc9-9a7b-68f1ff94a94a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
---
# bitsadmin getproxybypasslist

>Applies To: Windows Server&reg; 2016, Windows Server&reg; 2012 R2, Windows Server&reg; 2012

Retrieves the proxy bypass list for the specified job.
## Syntax
```
bitsadmin /GetProxyBypasslist <Job>
```
## Parameters
|Parameter|Description|
|-------|--------|
|Job|The job's display name or GUID|
## remarks
-   The bypass list contains the host names or IP addresses, or both, that are not to be routed through a proxy. The list can contain "<local>" to refer to all servers on the same LAN. The list can be semicolon or space-delimited.
## <a name="BKMK_examples"></a>Examples
The following example retrieves the proxy bypass list for the job named *myDownloadJob*.
```
C:\>bitsadmin /GetProxyBypasslist myDownloadJob
```
## additional references
[Command-Line Syntax Key](command-line-syntax-key.md)
