---
title: manage-bde: tpm
ms.custom: na
ms.prod: windows-server-2012
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 11a8530d-edd7-4fe3-ae81-b943766760fe
---
# manage-bde: tpm

> [!importANT]
> This command is not supported for use on computers running Windows 8,  Windows Server 2012  or later operating systems. for those computers, you can use the [TPM management cmdlets for Windows powershell](http://technet.microsoft.com/library/jj603116.aspx).

if you are using this command on computer running Windows 7 or Windows Server 2008, you can still configure the computer's Trusted Platform Module \(TPM\) using this command. for examples of how this command can be used, see [Examples](#BKMK_Examples).

## Syntax

```
manage-bde -tpm [-turnon] [-takeownership <OwnerPassword>] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

### Parameters

|Parameter|Description|
|-------------|---------------|
|\-turnon|Enables and activates the TPM, allowing the TPM owner password to be set. You can also use **\-t** as an abbreviated version of this command.|
|\-takeownership|Takes ownership of the TPM by setting an owner password. You can also use **\-o** as an abbreviated version of this command.|
|<OwnerPassword>|Represents the owner password that you specify for the TPM.|
|\-computername|Specifies that manage\-bde.exe will be used to modify BitLocker protection on a different computer. You can also use **\-cn** as an abbreviated version of this command.|
|<Name>|Represents the name of the computer on which to modify BitLocker protection. Accepted values include the computer's NetBIOS name and the computer's IP address.|
|\-? or \/?|Displays brief help at the command prompt.|
|\-help or \-h|Displays complete help at the command prompt.|

## <a name="BKMK_Examples"></a>Examples
The following example illustrates using the **\-tpm** command to turn on the TPM.

```
manage-bde –tpm -turnon
```

The following example illustrates using the **–tpm** command to take ownership of the TPM and set the owner password to 0wnerP@ss.

```
manage-bde –tpm –takeownership 0wnerP@ss
```

## additional references

-   [Command-Line Syntax Key](../commandline-syntax-key.md)

-   [manage-bde]()


