---
title: Clip
ms.custom: na
ms.prod: windows-server-2012
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 85322d85-3376-4806-845b-93ac77fe27bf
author: jaimeo
---
# Clip
Redirects command output from the command line to the Windows clipboard. You can then paste this text output into other programs.  
  
For examples of how to use this command, see [Examples](#BKMK_examples).  
  
## Syntax  
  
```  
<Command> | clip  
clip < <FileName>  
```  
  
## Parameters  
  
|Parameter|Description|  
|-------------|---------------|  
|<Command>|Specifies a command whose output you want to send to the Windows Clipboard.|  
|<FileName>|Specifies a file whose contents you want to send to the Windows Clipboard.|  
|\/?|Displays help at the command prompt.|  
  
## Remarks  
You can use the **clip** command to copy data directly into any application that can receive text from the Clipboard.  
  
## <a name="BKMK_examples"></a>Examples  
To copy the current directory listing to the Windows clipboard, type:  
  
```  
dir | clip  
```  
  
To copy the output of a program called Generic.awk to the Windows Clipboard, type:  
  
```  
awk -f generic.awk input.txt | clip  
```  
  
To copy the contents of a file called Readme.txt to the Windows Clipboard, type:  
  
```  
clip < readme.txt  
```  
  
#### Additional references  
[Command-Line Syntax Key](Command-Line-Syntax-Key.md)  
  

