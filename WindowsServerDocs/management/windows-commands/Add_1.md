---
title: add_1
description: "Windows Commands topic for **add_1** - adds volumes to the set of volumes that are to be shadow copied, or adds aliases to the alias environment."
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 47efce7a-86d2-4872-ae31-baa108757afd

author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
---
# add_1

>Applies To: Windows Server&reg; 2016, Windows Server&reg; 2012 R2, Windows Server&reg; 2012

adds volumes to the set of volumes that are to be shadow copied, or adds aliases to the alias environment. if used without subcommands, **add** lists the current volumes and aliases.  
  
> [!NOTE]  
> Aliases are not added to the alias environment until the shadow copy is created. Aliases that you need immediately should be added by using **add alias**.  
  
for examples of how to use this command, see [Examples](#BKMK_examples).  
  
## Syntax  
  
```  
add   
add volume <volume> [provider <ProviderID>]   
add alias <AliasName> <AliasValue>  
```  
  
## add subcommands  
  
|Subcommand|Description|  
|-------|--------|  
|volume|adds a volume to the shadow copy Set, which is the set of volumes to be shadow copied. See [add volume](add-volume.md) for syntax and parameters.|  
|alias|adds the given name and value to the alias environment. See [add alias](add-alias.md) for syntax and parameters.|  
|\/?|Displays help at the command line.|  
  
## <a name="BKMK_examples"></a>Examples  
To display the volumes added and the aliases that are currently in the environment, type:  
  
```  
add  
```  
  
The following output shows that drive C has been added to the shadow copy Set:  
  
```  
volume c: alias System1    GUID \\?\volume{XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX}\  
1 volume in shadow copy Set.  
No diskshadow aliases in the environment.  
```  
  
#### additional references  
[Command-Line Syntax Key](command-line-syntax-key.md)  
  

