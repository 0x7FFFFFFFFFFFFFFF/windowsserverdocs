---
title: Bdehdcfg: restart
description: "Windows Commands topic for **Bdehdcfg: restart** - Tells Bdehdcfg that the computer should be restarted after the drive preparation has concluded."
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a98b76bb-36f1-4790-b337-7dc35f606bc6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
---
# Bdehdcfg: restart

>Applies To: Windows Server&reg; 2016, Windows Server&reg; 2012 R2, Windows Server&reg; 2012

Informs the Bdehdcfg command-line tool that the computer should be restarted after the drive preparation has concluded. For an example of how this command can be used, see [Examples](#BKMK_Examples).
## Syntax
```
bdehdcfg -target {default|unallocated|<DriveLetter> shrink|<DriveLetter> merge} -restart
```
### Parameters
This command takes no additional parameters.
## Remarks
If other users are logged on to the computer and the **quiet** command is not specified, a prompt will be displayed to confirm that the computer should be restarted.
## <a name="BKMK_Examples"></a>Examples
The following example illustrates using the **restart** command.
```
bdehdcfg -target default -restart
```
## Additional references
-   [Command-Line Syntax Key](Command-Line-Syntax-Key.md)
-   [Bdehdcfg](Bdehdcfg.md)
