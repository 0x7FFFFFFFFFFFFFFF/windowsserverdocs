---
title: gpfixup
description: "Windows Commands topic for **** - "
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2b145410-fc75-4526-932d-f16b7ee3aaef
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
---
# gpfixup

>Applies To: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Fix domain name dependencies in Group Policy Objects and Group Policy links after a domain rename operation. For examples of how this command can be used, see [Examples](#BKMK_Examples).
## Syntax
```
gpfixup [/v] 
[/olddns:<OLDDNSNAME> /newdns:<NEWDNSNAME>] 
[/oldnb:<OLDFLatNAME> /newnb:<NEWFLatNAME>] 
[/dc:<DCNAME>] [/sionly] 
[/user:<USERNAME> [/pwd:{<PASSWOrd>|*}]] [/?]
```
### Parameters
|Parameter|Description|
|-------|--------|
|/v|Displays detailed status messages.<br /><br />if this parameter is not used, only error messages or a summary status message of **SUCCESS** or **FAILURE** appears.|
|/olddns:<OLDDNSNAME>|Specifies the old DNS name of the renamed domain as *<OLDDNSNAME>* when the domain rename operation changes the DNS name of a domain. You can use this parameter only if you also use the **/newdns** parameter to specify a new domain DNS name.|
|/newdns:<NEWDNSNAME>|Specifies the new DNS name of the renamed domain as *<NEWDNSNAME>* when the domain rename operation changes the DNS name of a domain. You can use this parameter only if you also use the **/olddns** parameter to specify the old domain DNS name.|
|/oldnb:<OLDFLatNAME>|Specifies the old NetBIOS name of the renamed domain as *<OLDFLatNAME>* when the domain rename operation changes the NetBIOS name of a domain. You can use this parameter only if you use the **/newnb** parameter to specify a new domain NetBIOS name.|
|/newnb:<NEWFLatNAME>|Specifies the new NetBIOS name of the renamed domain as *<NEWFLatNAME>* when the domain rename operation changes the NetBIOS name of a domain. You can use this parameter only if you use the **/oldnb** parameter to specify the old domain NetBIOS name.|
|/dc:<DCNAME>|Connect to the domain controller named *<DCNAME>* (a DNS name or a NetBIOS name). *<DCNAME>* must host a writable replica of the domain directory partition as indicated by one of the following:<br /><br />-   The DNS name *<NEWDNSNAME>* by using **/newdns**<br />-   The NetBIOS name *<NEWFLatNAME>* by using **/newnb**<br /><br />if this parameter is not used, connect to any domain controller in the renamed domain indicated by *<NEWDNSNAME>* or *<NEWFLatNAME>*.|
|/sionly|Performs only the Group Policy fix that relates to managed software installation (the Software Installation extension for Group Policy). Skip the actions that fix Group Policy links and the SYSvol paths in GPOs.|
|/user:<USERNAME>|Runs this command in the security context of the user *<USERNAME>*, where *<USERNAME>* is in the format domain\user.<br /><br />if this parameter is not used, runs this command as the logged in user.|
|/pwd:{<PASSWOrd>&#124;*}|Specifies the password for the other security context indicated by using **/user**. If **\*** is specified instead of a password, you are prompted for a password.|
|/?|Displays help at the command prompt.|
## remarks
-   The **gpfixup** command is available in  Windows Server 2008 R2  and  Windows Server 2008 , except on Server Core installations.
-   Although the Group Policy Management Console (GPMC) is distributed with  Windows Server 2008 R2  and  Windows Server 2008 , you must install Group Policy Management as a feature through Server Manager.
## <a name="BKMK_Examples"></a>Examples
This example assumes that you have already performed a domain rename operation in which you changed the DNS name from **MyOldDnsName** to **MyNewDnsName**, and the NetBIOS name from **MyOldNetBIOSName** to **MyNewNetBIOSName**. In this example, you use the **gpfixup** command to connect to the domain controller named **MyDcdnsName** and repair GPOs and Group Policy links by updating the old domain name embedded in the GPOs and links. Status and error output is saved to a file that is named **gpfixup.log**.
```
gpfixup /olddns: MyOldDnsName /newdns:MyNewDnsName /oldnb:MyOldNetBIOSName /newnb:MyNewNetBIOSName /dc:MyDcdnsName 2>&1 >gpfixup.log
```
This example is the same as the previous one, except that it assumes the NetBIOS name of the domain was not changed during the domain rename operation.
```
gpfixup /olddns: MyOldDnsName /newdns:MyNewDnsName /dc:MyDcdnsName 2>&1 >gpfixup.log
```
## additional references
-   [Administering active directory Domain rename](http://go.microsoft.com/fwlink/?LinkId=198385)
-   [Group Policy TechCenter](http://go.microsoft.com/fwlink/?LinkID=145531)
-   [Command-Line Syntax Key](command-line-syntax-key.md)
