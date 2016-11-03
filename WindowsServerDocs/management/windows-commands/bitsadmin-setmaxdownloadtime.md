---
title: bitsadmin setmaxdownloadtime
description: "Windows Commands topic for **bitsadmin setmaxdownloadtime** - Sets the download timeout in seconds."
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 16b96cf1-5738-415c-9b9d-c4ea8d5e4fec
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016 
---
# bitsadmin setmaxdownloadtime

>Applies To: Windows Server&reg; 2016, Windows Server&reg; 2012 R2, Windows Server&reg; 2012

Sets the download timeout in seconds.

## Syntax

```
bitsadmin /SetMaxDownloadtime <Job> <timeout>
```

## Parameters

|Parameter|Description|
|-------|--------|
|Job|The job's display name or GUID|
|timeout|The timeout in seconds|

## remarks

-   N\/A

## <a name="BKMK_examples"></a>Examples
The following example sets the timeout for the job named *myDownloadJob* to 10 seconds.

```
C:\>bitsadmin /SetMaxDownloadtime myDownloadJob 10
```

## additional references
[Command-Line Syntax Key](command-line-syntax-key.md)


