---
title: bitsadmin util and setieproxy
description: "Windows Commands topic for **bitsadmin util and setieproxy** - Set proxy settings to use when transferring files using a service account."
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0e9f31ba-3070-4ffd-a94c-388c8d78f688
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
---
# bitsadmin util and setieproxy

>Applies To: Windows Server&reg; 2016, Windows Server&reg; 2012 R2, Windows Server&reg; 2012

Set proxy settings to use when transferring files using a service account.
## Syntax
```
bitsadmin /Util /GetIEProxy <Account> <Usage>[/Conn <ConnectionName>]
```
## Parameters
|Parameter|Description|
|-------|--------|
|Account|Specifies the service account whose proxy settings you want to retrieve. Possible values are:<br /><br />-   LOCALSYSTEM<br />-   NETWORKSERVICE<br />-   LOCALSERVICE|
|Usage|Specifies the form of proxy detection to use. Possible values are:<br /><br /><ul><li>NO_PROXY Do not use a proxy server.</li><li>AUTODETECT Automatically detect the proxy settings.</li><li>MANUAL_PROXY Use an explicit proxy list and bypass list. Specify the proxy list and bypass list immediately following the usage tag. for example, MANUAL_PROXY proxy1,proxy2 NULL.<br /><br /><ul><li>The proxy list is a semicolon or space delimited list of proxy servers to use.</li><li>The bypass list is a semicolon or space-delimited list of host names or IP addresses, or both, for which transfers are not to be routed through a proxy. This can be <local> to refer to all servers on the same LAN. Values of NULL or "" may be used for an empty proxy bypass list.</li></ul></li><li>AUTOSCRIPT  Same as AUTODETECT, except it also executes a script. Specify the script URL immediately following the usage tag. for example, AUTOSCRIPT http://server/proxy.js.</li></ul>|
|ConnectionName|Optional used with the **/Conn** command to specify the use of a modem connection. if you do not specify the **/Conn** command, BITS uses the LAN connection. Specify the modem connection name immediately following the **/Conn** parameter.|
## remarks
Each successive call using this command replaces the previously specified usage but not the parameters of the previously defined usage. for example, if you specify NO_PROXY, AUTODETECT, and MANUAL_PROXY on separate calls, BITS uses the last supplied usage but keeps the parameters from the previously defined usage.
> [!importANT]
> You must run this command from an elevated command prompt for it to complete successfully.
## <a name="BKMK_examples"></a>Examples
The following example sets the proxy usage for the NETWORK SERVICE account.
```
C:\>bitsadmin /Util /SetIEProxy localsystem AUTODETECT
```
## additional references
[Command-Line Syntax Key](command-line-syntax-key.md)
