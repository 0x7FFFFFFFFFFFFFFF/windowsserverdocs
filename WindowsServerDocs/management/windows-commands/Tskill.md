---
title: tskill
ms.custom: na
ms.prod: windows-server-2012
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 08986e6a-6900-4ece-85a1-8f73b14db1b3
author: Lizap
---
# tskill
Ends a process running in a session on a remote Desktop Session Host \(rd Session Host\) server.

for examples of how to use this command, see [Examples](#BKMK_examples).

> [!NOTE]
> In Windows Server 2008 R2, Terminal Services was renamed remote Desktop Services. To find out what's new in the latest version, see [What’s New in remote Desktop Services in Windows Server 2012](http://technet.microsoft.com/library/hh831527) in the Windows Server TechNet Library.

## Syntax

```
tskill {<ProcessID> | <ProcessName>} [/server:<ServerName>] [/id:<SessionID> | /a] [/v]
```

## Parameters

|Parameter|Description|
|-------------|---------------|
|<ProcessID>|Specifies the ID of the process that you want to end.|
|<ProcessName>|Specifies the name of the process that you want to end. This parameter can include wildcard characters.|
|\/server:<ServerName>|Specifies the terminal server that contains the process that you want to end. if **\/server** is not specified, the current rd Session Host server is used.|
|\/id:<SessionID>|Ends the process that is running in the specified session.|
|\/a|Ends the process that is running in all sessions.|
|\/v|Displays information about the actions being performed.|
|\/?|Displays help at the command prompt.|

## remarks

-   You can use **tskill** to end only those processes that belong to you, unless you are an administrator. Administrators have full access to all **tskill** functions and can end processes that are running in other user sessions.

-   When all processes that are running in a session end, the session also ends.

-   if you use the *ProcessName* and the **\/server:***ServerName* parameters, you must also specify either the **\/id:***SessionID* or the **\/a** parameter.

## <a name="BKMK_examples"></a>Examples

-   To end process 6543, type:

    ```
    tskill 6543
    ```

-   To end the process "explorer" running on session 5, type:

    ```
    tskill explorer /id:5
    ```

#### additional references
[Command-Line Syntax Key](commandline-syntax-key.md)

[remote Desktop Services &#40;Terminal Services&#41; Command Reference](commands-by-server-role/remote-desktop-services-terminal-services-command-reference.md)


