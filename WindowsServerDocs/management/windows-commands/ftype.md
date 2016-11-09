---
title: ftype
description: "Windows Commands topic for **** - "
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6fb53cee-9bed-44dd-af5d-bc7cec1dd114
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
---
# ftype

>Applies To: Windows Server&reg; 2016, Windows Server&reg; 2012 R2, Windows Server&reg; 2012

Displays or modifies file types that are used in file name extension associations. if used without an assignment operator (**=**), **ftype** displays the current open command string for the specified file type. if used without parameters, **ftype** displays the file types that have open command strings defined.
for examples of how to use this command, see [Examples](#BKMK_examples).
## Syntax
```
ftype [<Filetype>[=[<OpenCommandString>]]]
```
## Parameters
|Parameter|Description|
|-------|--------|
|<Filetype>|Specifies the file type to display or change.|
|<OpenCommandString>|Specifies the open command string to use when opening files of the specified file type.|
|/?|Displays help at the command prompt.|
## remarks
The following table describes how **ftype** substitutes variables within an open command string:
|Variable|replacement value|
|------|-----------|
|%0 or %1|Gets substituted with the file name being launched through the association.|
|%*|Gets all of the parameters.|
|%2, %3, ...|Gets the first parameter (%2), the second parameter (%3), and so on.|
|%~<N>|Gets all of the remaining parameters starting with the *N*th parameter, where *N* can be any number from 2 to 9.|
## <a name="BKMK_examples"></a>Examples
To display the current file types that have open command strings defined, type:
```
ftype
```
To display the current open command string for the *txtfile* file type, type:
```
ftype txtfile
```
This command produces output similar to the following:
```
txtfile=%SystemRoot%\system32\NOTEPAD.EXE %1
```
To delete the open command string for a file type called *Example*, type:
```
ftype example=
```
To associate the .pl file name extension with the PerlScript file type and enable the PerlScript file type to run PERL.EXE, type the following commands:
```
assoc .pl=PerlScript 
ftype PerlScript=perl.exe %1 %*
```
To eliminate the need to type the .pl file name extension when invoking a Perl script, type:
```
set pathEXT=.pl;%pathEXT%
```
#### additional references
[Command-Line Syntax Key](command-line-syntax-key.md)
