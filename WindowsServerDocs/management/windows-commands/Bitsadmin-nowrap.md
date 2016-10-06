---
title: Bitsadmin nowrap
description: "Windows Commands"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 85a47b90-783a-41e4-96f2-81f26ae8ca93
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
---

# Bitsadmin nowrap

>Applies To: Windows Server&reg; 2016, Windows Server&reg; 2012 R2, Windows Server&reg; 2012

Truncates any line of output text extending beyond the rightmost edge of the command window.
## Syntax
```
bitsadmin /NoWrap
```
## Remarks
By default, all commands, except the **Monitor** command, wrap the output. Specify the **NoWrap** command before other commands.
## <a name="BKMK_examples"></a>Examples
The following example retrieves the state for the job named *myDownloadJob* and does not wrap the output
```
C:\>bitsadmin /NoWrap /GetState myDownloadJob
```
## Additional references
[Command-Line Syntax Key](Command-Line-Syntax-Key.md)
