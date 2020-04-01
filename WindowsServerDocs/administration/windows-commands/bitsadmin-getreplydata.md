---
title: bitsadmin getreplydata
description: Windows Commands topic for bitsadmin getreplydata, which retrieves the server's reply data in hexadecimal format.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 819f97d5-b255-4b2d-9f63-0daa73915434
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
---

# bitsadmin getreplydata

Retrieves the server's reply data in hexadecimal format.

**BITS 1.2 and earlier**: Not supported.

## Syntax

```
bitsadmin /GetReplyData <Job>
```

## Parameters

|Parameter|Description|
|---------|-----------|
|Job|The job's display name or GUID|

## Remarks

Valid only for upload-reply jobs.

## <a name=BKMK_examples></a>Examples

The following example retrieves the reply data for the job named *myDownloadJob*.
```
C:\>bitsadmin /GetReplyData myDownloadJob
```

## Additional References

[Command-Line Syntax Key](command-line-syntax-key.md)