---
title: Using the convert-RiprepImage Command
description: "Windows Commands topic for **** - "
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 88c2b96f-5947-4b64-9dcf-1946b3c013cf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
---
# Using the convert-RiprepImage Command

>Applies To: Windows Server&reg; 2016, Windows Server&reg; 2012 R2, Windows Server&reg; 2012

converts an existing remote Installation Preparation (RIPrep) image to Windows Image (.wim) format.
## Syntax
```
wdsutil [Options] /convert-RIPrepImage /Filepath:<File path and name>
     /DestinationImage
         /Filepath:<File path and name>
         [/Name:<Name>]
         [/Description:<Description>]
         [/InPlace]
         [/Overwrite:{Yes | No | append}]
```
## Parameters
|Parameter|Description|
|-------|--------|
|/Filepath:<File path and name>|Specifies the full path and file name of the .sif file that corresponds to the RIPrep image. This file is typically called Riprep.sif and is found in the \Templates subfolder of the folder that contains the RIPrep image.|
|/DestinationImage|Specifies the settings for the destination image, using the following options.<br /><br />-   /Filepath:<File path and name> - Sets the full file path for the new file. For example: **C:\Temp\convert.wim**<br />-   [/Name:<Name>] - Sets the display name of the image. If no display name is specified, the display name of the source image will be used.<br />-   [/Description: <Description>] - Sets the description of the image.<br />-   [/InPlace] - Specifies that the conversion should take place on the original RIPrep image and not on a copy of the original image, which is the default behavior.<br />-   [/Overwrite:{Yes &#124; No &#124; append}] - Determines whether the file specified in the **/DestinationImage** option should be overwritten if an existing file with that name already exists at /Filepath. **Yes** overwrites the existing file. **No** (default) causes an error to occur if another file with the same name already exists. **append** attaches the generated image as a new image withi the pre-existing .wim file.|
## <a name="BKMK_examples"></a>Examples
To convert the specified RIPrep.sif image to RIPREP.wim, type:
```
wdsutil /convert-RiPrepImage /Filepath:"R:\remoteInstall\Setup\English
\Images\Win2k3.SP1\i386\Templates\riprep.sif" /DestinationImage
/Filepath:"C:\Temp\RIPREP.wim"
```
To convert the specified RIPrep.sif image to RIPREP.wim with the specified name and description, and overwrite it with the new file if a file already exists, type:
```
wdsutil /verbose /Progress /convert-RiPrepImage /Filepath:"\\Server
\remInst\Setup\English\Images\WinXP.SP2\i386\Templates\riprep.sif"
/DestinationImage /Filepath:"\\Server\Share\RIPREP.wim"
/Name:"WindowsXP image" /Description:"converted RIPREP image of WindowsXP"
/Overwrite:append
```
#### additional references
[Command-Line Syntax Key](command-line-syntax-key.md)
