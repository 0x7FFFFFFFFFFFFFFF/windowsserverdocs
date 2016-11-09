---
title: takeown
description: "Windows Commands topic for **** - "
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0683cd65-a6db-4cab-962b-45a0ff61f43c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
---
# takeown

>Applies To: Windows Server&reg; 2016, Windows Server&reg; 2012 R2, Windows Server&reg; 2012

Enables an administrator to recover access to a file that previously was denied, by making the administrator the owner of the file.
for examples of how to use this command, see [Examples](#BKMK_examples).
## Syntax
```
takeown [/s <computer> [/u [<Domain>\]<User name> [/p [<Password>]]]] /f <File name> [/a] [/r [/d {Y|N}]]
```
## Parameters
|Parameter|Description|
|-------|--------|
|/s <computer>|Specifies the name or IP address of a remote computer (do not use backslashes). The default value is the local computer. This parameter applies to all of the files and folders specified in the command.|
|/u [<Domain>\\]<User name>|Runs the script with the permissions of the specified user account. The default value is system permissions.|
|/p [<Password>]|Specifies the password of the user account that is specified in the **/u** parameter.|
|/f <File name>|Specifies the file name or directory name pattern. You can use the wildcard character \* when specifying the pattern. You can also use the syntax *Sharename*\\*FileName*.|
|/a|Gives ownership to the Administrators group instead of the current user.|
|/r|Performs a recursive operation on all files in the specified directory and subdirectories.|
|/d {Y &#124; N}|Suppresses the confirmation prompt that is displayed when the current user does not have the "list Folder" permission on a specified directory, and instead uses the specified default value. Valid values for the **/d** option are as follows:<br /><br />-   Y: Take ownership of the directory.<br />-   N: Skip the directory.<br /><br />Note that you must use this option in conjunction with the **/r** option.|
|/?|Displays help at the command prompt.|
## remarks
-   This command is typically used in batch files.
-   if the **/a** parameter is not specified, file ownership is given to the user who is currently logged on to the computer.
-   Mixed patterns using (**?** and **\***) are not supported by **takeown** command.
-   After deleting the lock with **takeown**, you might have to use Windows Explorer or the **cacls** command to give yourself full permissions to the files and directories before you can delete them. for more information about **cacls**, see "additional references" at the end of this topic.
## <a name="BKMK_examples"></a>Examples
To take ownership of a file named Lostfile, type:
```
takeown /f lostfile
```
#### additional references
[Command-Line Syntax Key](command-line-syntax-key.md)
