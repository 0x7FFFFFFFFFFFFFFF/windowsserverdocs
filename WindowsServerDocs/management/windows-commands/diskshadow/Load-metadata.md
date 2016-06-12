---
title: Load metadata
ms.custom: na
ms.prod: windows-server-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - techgroup-storage
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2c535487-668b-44fc-babb-ff59cf7d190e
---
# Load metadata
Loads a metadata .cab file prior to importing a transportable shadow copy or loads the writer metadata in the case of a restore. if used without parameters, **load metadata** displays help at the command prompt.

for examples of how to use this command, see [Examples](#BKMK_examples).

## Syntax

```
load metadata [<Drive>:][<path>]<MetaData.cab>
```

## Parameters

|Parameter|Description|
|-------------|---------------|
|\[<Drive>:\]\[<path>\]|Specifies the location of the metadata file.|
|MetaData.cab|Specifies the metadata .cab file to load.|

## remarks

-   You can use the **import** command to import a transportable shadow copy based on the metadata specified by **load metadata**.

-   This command is needed before the **begin restore** command to load the selected writers and components for the restore.

## <a name="BKMK_examples"></a>Examples
To load a metadata file called metafile.cab from the default location, type:

```
load metadata metafile.cab
```

#### additional references
[Command-Line Syntax Key](../commandline-syntax-key.md)


