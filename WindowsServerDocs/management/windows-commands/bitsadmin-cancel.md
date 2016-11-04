---
title: bitsadmin cancel
description: "Windows Commands topic for **bitsadmin cancel** - 
removes the job from the transfer queue and deletes all temporary files associated with the job."
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7374b544-6a16-4d3e-872c-dcf4c02ad89d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
---
# bitsadmin cancel

>Applies To: Windows Server&reg; 2016, Windows Server&reg; 2012 R2, Windows Server&reg; 2012

removes the job from the transfer queue and deletes all temporary files associated with the job.
## Syntax
```
bitsadmin /cancel <Job>
```
## Parameters
|Parameter|Description|
|-------|--------|
|Job|The job's display name or GUID|
## <a name="BKMK_examples"></a>Examples
The following example removes the *myDownloadJob* job from the transfer queue.
```
C:\>bitsadmin /cancel myDownloadJob
```
## additional references
[Command-Line Syntax Key](command-line-syntax-key.md)
