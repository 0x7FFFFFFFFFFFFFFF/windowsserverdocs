---
title: winsat mfmedia
ms.custom: na
ms.prod: windows-server-2012
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 09a3b3dd-f746-4e6e-b684-76a9bde0c78d
---
# winsat mfmedia
Measures the performance of video decoding \(playback\) using the Media Foundation framework.

for examples of how to use this command, see [Examples](#BKMK_examples).

## Syntax

```
winsat mfmedia <parameters>
```

## Parameters

|Parameters|Description|
|--------------|---------------|
|\-input <file name>|Required: Specify the file containing the video clip to be played or encoded. The file can be in any format that can be rendered by Media Foundation.|
|\-dumpgraph|Specify that the filter graph should be saved to a Graphedit\-compatible file before the assessment starts.|
|\-ns|Specify that the filter graph should run at the normal playback speed of the input file. By default, the filter graph runs as fast as possible, ignoring presentation times.|
|\-play|Run the assessment in decode mode and play any supplied audio content in the file specified in **\-input** using the default directSound device. By default, audio playback is disabled.|
|\-nopmp|Do not make use of the Media Foundation Protected Media Pipeline \(MFPMP\) process during the assessment.|
|\-pmp|Always make use of the MFPMP process during the assessment. **Note:** if **\-pmp** or **\-nopmp** is not specified, MFPMP will be used only when necessary.|
|\-v|Send verbose output to STDOUT, including status and progress information. Any errors will also be written to the command window.|
|\-xml <file name>|Save the output of the assessment as the specified XML file. if the specified file exists, it will be overwritten.|
|\-idiskinfo|Save information about physical volumes and logical disks as part of the **<SystemConfig>** section in the XML output.|
|\-iguid|create a globally unique identifier \(GUID\) in the XML output file.|
|\-note "note text"|add the note text to the **<note>** section in the XML output file.|
|\-icn|Include the local computer name in the XML output file.|
|\-eef|Enumerate extra system information in the XML output file.|

## <a name="BKMK_examples"></a>Examples

-   The following example runs the assessment with the input file that is used during a **winsat formal** assessment, without employing the Media Foundation Protected Media Pipeline \(MFPMP\), on a computer where c:\\windows is the location of the Windows folder.

    ```
    winsat mfmedia -input c:\windows\performance\winsat\winsat.wmv -nopmp
    ```

## remarks

-   Membership in the local Administrators group, or equivalent, is the minimum required to use **winsat**. The command must be executed from an elevated command prompt window.

-   To open an elevated command prompt window, click **start**, click **Accessories**, right\-click **Command prompt**, and click **Run as administrator**.

#### additional references
[winsat \[vista\]](assetId:///11b0e51f-fe58-4553-9e7c-a562e5385fbb)

[winsat formal](assetId:///a098662a-85d6-41c8-ae61-7624d01d0521)


