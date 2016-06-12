---
title: Net print
ms.custom: na
ms.prod: windows-server-2012
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f59b2015-4698-415d-9a74-09566c466f40
---
# Net print
Displays information about a specified printer queue or a specified print job, or controls a specified print job.

for examples of how to use this command, see the [Examples](#BKMK_examples) section of this document.

> [!NOTE]
> This command has been deprecated in  Windows 7  and  Windows Server 2008 R2 . However, you can perform many of the same tasks using prnjobsvbs, Windows management Instrumentation \(WMI\), or Windows powershell cmdlets. for more information, see [prnjobsvbs](prnjobsvbs.md), [Windows management Instrumentation](http://go.microsoft.com/fwlink/?LinkID=29991) \(http:\/\/go.microsoft.com\/fwlink\/?LinkID\=29991\), [Windows powershell](http://go.microsoft.com/fwlink/?LinkID=128426) \(http:\/\/go.microsoft.com\/fwlink\/?LinkID\=128426\), and the [TechNet Script Center Gallery](http://go.microsoft.com/fwlink/?LinkId=164635) \(http:\/\/go.microsoft.com\/fwlink\/?LinkId\=164635\).

## Syntax

```
Net print {\\<computerName>\<Sharename> | 
\\<computerName> <JobNumber> [/hold | /release | /delete]} [help]
```

## Parameters

|Parameters|Description|
|--------------|---------------|
|\\\\<computerName>\\<Sharename>|Specifies \(by name\) the computer and print queue about which you want to display information.|
|\\\\<computerName>|Specifies \(by name\) the computer that hosts the print job you want to control. if you do not specify a computer, the local computer is assumed. Requires the <JobNumber> parameter.|
|<JobNumber>|Specifies the number of the print job you want to control. This number is assigned by the computer that hosts the print queue where the print job is sent. After a computer assigns a number to a print job, that number is not assigned to any other print jobs in any queue hosted by that computer. Required when using the \\\\<computerName> parameter.|
|\[\/hold &#124; \/release &#124; \/delete\]|Specifies the action to take with the print job.<br /><br />-   The **\/hold** parameter delays the job, allowing other print jobs to bypass it until it is released.<br />-   The **\/release** parameter releases a print job that has been delayed.<br />-   The **\/delete** parameter removes a print job from a print queue.<br /><br />if you specify a job number, but do not specify any action, information about the print job is displayed.|
|help|Displays help for the **Net print** command.|

## remarks

-   **Net print** \\\\<computerName> displays information about print jobs in a shared printer queue. The following is an example of a report for all print jobs in a queue for a shared printer named LASER:

    ```
    printers at \\PRODUCTION
    Name              Job #      Size      Status
    ---------------------------------------------------------
    LASER Queue       3 jobs               *printer active*
       USER1          84        93844      printing
       USER2          85        12555      Waiting
       USER3          86        10222      Waiting
    ```

-   The following is an example of a report for a print job:

    ```
    Job #            35
    Status           Waiting
    Size             3096
    remark
    Submitting user  USER2
    Notify           USER2
    Job data type
    Job parameters
    additional info
    ```

## <a name="BKMK_examples"></a>Examples
This example shows how to list the contents of the Dotmatrix print queue on the \\\\Production computer:

```
Net print \\Production\Dotmatrix 
```

This example shows how to display information about job number 35 on the \\\\Production computer:

```
Net print \\Production 35 
```

This example shows how to delay job number 263 on the \\\\Production computer:

```
Net print \\Production 263 /hold 
```

This example shows how to release job number 263 on the \\\\Production computer:

```
Net print \\Production 263 /release 
```

#### additional references
[Command-Line Syntax Key](commandline-syntax-key.md)

[print Command Reference](commands-by-server-role/print-command-reference.md)


