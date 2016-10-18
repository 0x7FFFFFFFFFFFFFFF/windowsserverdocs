---
title: Bitsadmin setdescription
description: "Windows Commands topic for **Bitsadmin setdescription** -- Sets the description of the specified job."
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1e46a5dd-4637-4a2e-b88f-d3f85b177db8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
---

# Bitsadmin setdescription

>Applies To: Windows Server&reg; 2016, Windows Server&reg; 2012 R2, Windows Server&reg; 2012

Sets the description of the specified job.
## Syntax
```
bitsadmin /SetDescription <Job> <Description>
```
## Parameters
|Parameter|Description|
|-------------|---------------|
|Job|The job's display name or GUID|
|Description|Text used to describe the job.|
## <a name="BKMK_examples"></a>Examples
The following example retrieves the description for the job named *myDownloadJob*.
```
C:\>bitsadmin /SetDescription myDownloadJob "Music Downloads"
```
## Additional references
[Command-Line Syntax Key](Command-Line-Syntax-Key.md)
