---
title: Set context
description: "Windows Commands topic for **** - "
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fc16c7dd-e8f0-4c2a-8742-0bddb2848bfd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
---
# Set contex

>Applies To: Windows Server&reg; 2016, Windows Server&reg; 2012 R2, Windows Server&reg; 2012

Sets the context for shadow copy creation. If used without parameters, **set context** displays help at the command prompt.  
  
for examples of how to use this command, see [Examples](#BKMK_examples).  
  
## Syntax  
  
```  
set context {clientaccessible | persistent [nowriters] | volatile [nowriters]}  
```  
  
## Parameters  
  
|Parameter|Description|  
|-------|--------|  
|clientaccessible|Specifies that the shadow copy is usable by client versions of Windows.|  
|persistent|Specifies that the shadow copy persists across program exit, reset, or restart.|  
|volatile|deletes the shadow copy on exit or reset.|  
|nowriters|Specifies that all writers are excluded.|  
  
## remarks  
  
-   The *clientaccessible* context is persistent by default.  
  
## <a name="BKMK_examples"></a>Examples  
To prevent shadow copies from being deleted when you exit diskshadow, type:  
  
```  
set context persistent  
```  
  
#### additional references  
[Command-Line Syntax Key](command-line-syntax-key.md)  
  

