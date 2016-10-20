---
title: Revert
description: "Windows Commands topic for **** - "
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 75ad40e4-502a-401e-b11e-8b31e00424b5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
---
# Revert

>Applies To: Windows Server&reg; 2016, Windows Server&reg; 2012 R2, Windows Server&reg; 2012

Reverts a volume back to a specified shadow copy. This is supported only for shadow copies in the CLIENTACCESSIBLE context. These shadow copies are persistent and can only be made by the system provider. If used without parameters, **revert** displays help at the command prompt.  
  
## Syntax  
  
```  
revert <ShadowCopyID>  
```  
  
## Parameters  
  
|Parameter|Description|  
|-------|--------|  
|<ShadowCopyID>|Specifies the shadow copy ID to revert the volume to.|  
  
#### Additional references  
[Command-Line Syntax Key](Command-Line-Syntax-Key.md)  
  

