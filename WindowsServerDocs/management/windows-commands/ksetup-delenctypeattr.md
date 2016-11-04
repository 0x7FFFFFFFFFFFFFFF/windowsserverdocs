---
title: ksetup:delenctypeattr
description: "Windows Commands topic for **** - "
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4fc25ef3-e271-4229-a712-72c507df55aa
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
---
# ksetup:delenctypeattr

>Applies To: Windows Server&reg; 2016, Windows Server&reg; 2012 R2, Windows Server&reg; 2012

removes the encryption type attribute for the domain. for examples of how this command can be used, see [Examples](#BKMK_Examples).
## Syntax
```
ksetup /delenctypeattr <DomainName> 
```
### Parameters
|Parameter|Description|
|-------|--------|
|<DomainName>|Name of the domain to which you want to establish a connection. Use the fully qualified domain name or a simple form of the name, such as corp.contoso.com or contoso.|
## remarks
To view the encryption type for the Kerberos ticket-granting ticket (TGT) and the session key, run the **klist** command and view the output.
A status message is displayed upon successful or failed completion.
To set the domain that you want to connect to and use, run the **ksetup /domain <DomainName>** command.
## <a name="BKMK_Examples"></a>Examples
Determine the current encryption types that are set on this computer:
```
klist
```
Set the domain to mit.contoso.com:
```
ksetup /domain mit.contoso.com
```
verify what the encryption type attribute is for the domain:
```
ksetup /getenctypeattr mit.contoso.com
```
remove the set encryption type attribute for the domain mit.contoso.com:
```
ksetup /delenctypeattr mit.contoso.com
```
## additional references
-   [klist](klist.md)
-   [ksetup:domain](ksetup-domain.md)
-   [ksetup:addenctypeattr](ksetup-addenctypeattr.md)
-   [ksetup:setenctypeattr](ksetup-setenctypeattr.md)
-   [ksetup:delenctypeattr](ksetup-delenctypeattr.md)
-   [Command-Line Syntax Key](command-line-syntax-key.md)
