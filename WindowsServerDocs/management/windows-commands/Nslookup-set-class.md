---
title: Nslookup set class
description: "Windows Commands topic for **** -- "
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ed826400-40da-42b6-b7f0-95db73790723
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
---

# Nslookup set class

>Applies To: Windows Server&reg; 2016, Windows Server&reg; 2012 R2, Windows Server&reg; 2012

Changes the query class. The class specifies the protocol group of the information.
## Syntax
```
set class=<Class>
```
## Parameters
|Parameter|Description|
|-------------|---------------|
|<Class>|The default class is IN. The following table lists the valid values for this command.<br /><br />-   IN - Specifies the Internet class<br />-   CHAOS - Specifies the Chaos class<br />-   HESIOD - Specifies the MIT Athena Hesiod class<br />-   ANY - Specifies any of the previously listed wildcards|
|{help &#124; ?}|Displays a short summary of **nslookup** subcommands.|
## Additional references
[Command-Line Syntax Key](Command-Line-Syntax-Key.md)
