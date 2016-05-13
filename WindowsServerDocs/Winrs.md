---
title: Winrs
ms.custom: na
ms.prod: windows-server-2012
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c370de31-5651-400a-872d-ef229aae2309
---
# Winrs
Windows Remote Management allows you to manage and execute programs remotely. For examples of how this command can be used, see [Examples](assetId:///c6d43992-8243-4f0a-8605-3152c8a8fe9a#BKMK_Examples).

## Syntax

```
winrs [/<parameter>[:<value>]] <command>
```

### Parameters

|Parameter|Description|
|-------------|---------------|
|\/r\[emote\]:<endpoint>|Specifies the target endpoint using a NetBIOS name or the standard connection:<br /><br />-   <url>: \[<transport>:\/\/\]<target>\[:<port>\]<br /><br />If not specified, **\/r:localhost** is used.|
|\/un\[encrypted\]|Specifies that the messages to the remote shell will not be encrypted. This is useful for troubleshooting or when the network traffic is already encrypted using **ipsec**, or when physical security is enforced.<br /><br />By default, the messages are encrypted using Kerberos or NTLM keys.<br /><br />This command\-line option is ignored when HTTPS transport is selected.|
|\/u\[sername\]:<username>|Specifies username on command line.<br /><br />If not specified, the tool will use Negotiate authentication or prompt for the name.<br /><br />If **\/u\[sername\]** is specified, **\/p\[assword\]** must also be specified.|
|\/p\[assword\]:<password>|Specifies password on command line.<br /><br />If **\/p\[assword\]** is not specified but **\/username** is, the tool will prompt for the password.<br /><br />If **\/p\[assword\]** is specified, **\/u\[sername\]** must also be specified.|
|\/t\[imeout\]:<seconds>|This option is deprecated.|
|\/d\[irectory\]:<path>|Specifies starting directory for remote shell.<br /><br />If not specified, the remote shell will start in the user's home directory defined by the environment variable **%USERPROFILE%**.|
|\/env\[ironment\]:<string>\=<value>|Specifies a single environment variable to be set when shell starts, which allows changing default environment for shell.<br /><br />Multiple occurrences of this switch must be used to specify multiple environment variables.|
|\/noe\[cho\]|Specifies that echo should be disabled. This may be necessary to ensure that user's answers to remote prompts are not displayed locally.<br /><br />By default echo is "on".|
|\/nop\[rofile\]|Specifies that the user's profile should not be loaded.<br /><br />By default, the server will attempt to load the user profile.<br /><br />If the remote user is not a local administrator on the target system, then this option will be required \(the default will result in error\).|
|\/a\[llow\]d\[elegate\]|Specifies that the user's credentials can be used to access a remote share, for example, found on a different machine than the target endpoint.|
|\/comp\[ression\]|Turn on compression.  Older installations on remote machines may not support compression so it is off by default.<br /><br />Default setting is off, since older installations on remote machines may not support compression.|
|\/\[use\]ssl|Use an SSL connection when using a remote endpoint.  Specifying this instead of the transport **https:** will use the default **WinRM** default port.|
|\/?|Displays Help at the command prompt.|

## Remarks

-   All command\-line options accept either short form or long form. For example both **\/r** and **\/remote** are valid.

-   To terminate the **\/remote** command, the user can type **Ctrl\-C** or **Ctrl\-Break**, which will be sent to the remote shell. The second **Ctrl\-C** will force termination of **winrs.exe**.

-   To manage active remote shells or WinRS configuration, use the WinRM tool.  The URI alias to manage active shells is **shell\/cmd**.  The URI alias for WinRS configuration is **winrm\/config\/winrs**.

## <a name="BKMK_Examples"></a>Examples

```
winrs /r:https://contoso.com command
```

```
winrs /r:contoso.com /usessl command
```

```
winrs /r:myserver command
```

```
winrs /r:http://127.0.0.1 command
```

```
winrs /r:http://169.51.2.101:80 /unencrypted command
```

```
winrs /r:https://[::FFFF:129.144.52.38] command
```

```
winrs /r:http://[1080:0:0:0:8:800:200C:417A]:80 command
```

```
winrs /r:https://contoso.com /t:600 /u:administrator /p:$%fgh7 ipconfig
```

```
winrs /r:myserver /env:PATH=^%PATH^%;c:\tools /env:TEMP=d:\temp config.cmd
```

```
winrs /r:myserver netdom join myserver /domain:testdomain /userd:johns /passwordd:$%fgh789
```

```
winrs /r:myserver /ad /u:administrator /p:$%fgh7 dir \\anotherserver\share
```

## Additional references

-   [Command-Line Syntax Key](Command-Line-Syntax-Key.md)

-   [Command-Line Reference_1](Command-Line-Reference_1.md)


