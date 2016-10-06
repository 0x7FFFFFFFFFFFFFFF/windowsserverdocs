---
title: Bitsadmin rawreturn
description: "Windows Commands"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bbe97130-26f6-4cdd-84f1-baf530ce38b7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
---

# Bitsadmin rawreturn

>Applies To: Windows Server&reg; 2016, Windows Server&reg; 2012 R2, Windows Server&reg; 2012

Returns data suitable for parsing.
## Syntax
```
bitsadmin /RawReturn
```
## Remarks
Strips new line characters and formatting from the output.
Typically, you use this command in conjunction with the **Create** and **Get\*** commands to receive only the value. You must specify this command before other commands.
## <a name="BKMK_examples"></a>Examples
The following example retrieves the raw data for the state of the job named *myDownloadJob*.
```
C:\>bitsadmin /RawReturn /GetState myDownloadJob
```
## Additional references
[Command-Line Syntax Key](Command-Line-Syntax-Key.md)
