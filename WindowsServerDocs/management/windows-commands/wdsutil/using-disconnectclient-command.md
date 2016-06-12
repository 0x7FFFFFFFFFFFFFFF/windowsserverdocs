---
title: Using the Disconnect-Client Command
ms.custom: na
ms.prod: windows-server-2012
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 876bbe6c-76ab-4de5-879b-d2066e700326
---
# Using the Disconnect-Client Command
Disconnects a client from a multicast transmission or namespace. Unless you specify **\/force**, the client will fall back to another transfer method \(if it is supported by the client\).

## Syntax

```
wdsutil /Disconnect-Client /ClientId:<Client ID> [/Server:<Server name>] [/force]
```

## Parameters

|Parameter|Description|
|-------------|---------------|
|\/ClientId:<Client ID>|Specifies the ID of the client to be disconnected. To view the ID of a client, type **wdsutil \/get\-multicasttransmission \/show:clients**.|
|\[\/Server:<Server name>\]|Specifies the name of the server. This can be the NetBIOS name or the fully qualified domain name \(FQDN\). if no server name is specified, the local server is used.|
|\[\/force\]|Stops the installation completely and does not use a fallback method. Note that Wdsmcast.exe does not support any fallback mechanism. if you do not use this option, the default behavior is as follows:<br /><br />-   if you are using the Windows deployment Services client, the client continues the installation by using unicasting.<br />-   if you are not using the Windows deployment Services client, the installation fails. **important:** You should use this option with caution because the installation will fail and the computer could be left in an unusable state.|

## <a name="BKMK_examples"></a>Examples
To disconnect a client, type:

```
wdsutil /Disconnect-Client /ClientId:1
```

To disconnect a client and force the installation to fail, type:

```
wdsutil /Disconnect-Client /Server:MyWDSServer /ClientId:1 /force
```

#### additional references
[Command-Line Syntax Key](../commandline-syntax-key.md)


