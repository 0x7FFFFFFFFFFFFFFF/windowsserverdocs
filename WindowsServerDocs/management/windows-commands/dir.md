---
title: dir
description: "Windows Commands topic for **** - "
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: edcbf69b-eaa4-466e-b210-3dd8892f4d93
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
---
# dir

>Applies To: Windows Server&reg; 2016, Windows Server&reg; 2012 R2, Windows Server&reg; 2012

Displays a list of a directory's files and subdirectories. if used without parameters, **dir** displays the disk's volume label and serial number, followed by a list of directories and files on the disk (including their names and the date and time each was last modified). for files, **dir** displays the name extension and the size in bytes. **dir** also displays the total number of files and directories listed, their cumulative size, and the free space (in bytes) remaining on the disk.
for examples of how to use this command, see [Examples](#BKMK_examples).
## Syntax
```
dir [<Drive>:][<path>][<FileName>] [...] [/p] [/q] [/w] [/d] [/a[[:]<attributes>]][/o[[:]<sortOrder>]] [/t[[:]<timeField>]] [/s] [/b] [/l] [/n] [/x] [/c] [/4]
```
## Parameters
|Parameter|Description|
|-------|--------|
|[<Drive>:][<path>]|Specifies the drive and directory for which you want to see a listing.|
|[<FileName>]|Specifies a particular file or group of files for which you want to see a listing.|
|/p|Displays one screen of the listing at a time. To see the next screen, press any key on the keyboard.|
|/q|Displays file ownership information.|
|/w|Displays the listing in wide format, with as many as five file names or directory names on each line.|
|/d|Displays the listing in the same format as **/w**, but the files are sorted by column.|
|/a[[:]<attributes>]|Displays only the names of those directories and files with the attributes that you specify. if you omit **/a**, **dir** displays the names of all files except hidden and system files. if you use **/a** without specifying *attributes*, **dir** displays the names of all files, including hidden and system files.<br /><br />The following list describes each of the values that you can use for *attributes*. Using a colon (:) is optional. Use any combination of these values, and do not separate the values with spaces.<br /><br />**d** directories<br /><br />**h** Hidden files<br /><br />**s** System files<br /><br />**l** Reparse points<br /><br />**r** Read-only files<br /><br />**a** Files ready for archiving<br /><br />**i** Not content indexed files<br /><br />**-** Prefix meaning "not"|
|/o[[:]<sortOrder>]|sorts the output according to *sortOrder*, which can be any combination of the following values:<br /><br />**n** By name (alphabetical)<br /><br />**e** By extension (alphabetical)<br /><br />**g** Group directories first<br /><br />**s** By size (smallest first)<br /><br />**d** By date/time (oldest first)<br /><br />**-** Prefix to reverse order **Note:** Using a colon is optional. Multiple values are processed in the order in which you list them. Do not separate multiple values with spaces.<br /><br />if *sortOrder* is not specified, **dir /o** lists the directories in alphabetic order, followed by the files, which are also sorted in alphabetic order.|
|/t[[:]<timeField>]|Specifies which time field to display or use for sorting. The following list describes each of the values you can use for *timeField*:<br /><br />**c** Creation<br /><br />**a** Last access<br /><br />**w** Last written|
|/s|lists every occurrence of the specified file name within the specified directory and all subdirectories.|
|/b|Displays a bare list of directories and files, with no additional information. **/b** overrides **/w**.|
|/l|Displays unsorted directory names and file names in lowercase.|
|/n|Displays a long list format with file names on the far right of the screen.|
|/x|Displays the short names generated for non-8dot3 file names. The display is the same as the display for **/n**, but the short name is inserted before the long name.|
|/c|Displays the thousand separator in file sizes. This is the default behavior. Use **/-c** to hide separators.|
|/4|Displays years in four-digit format.|
|/?|Displays help at the command prompt.|
## remarks
-   To use multiple *FileName* parameters, separate each file name with a space, comma, or semicolon.
-   You can use wildcard characters (**\*** or**?**), to represent one or more characters of a file name and to display a subset of files or subdirectories.
    **Asterisk (\*):** Use the asterisk as a substitute for any string of characters, for example:
    -   **dir \*.txt** lists all files in the current directory with extensions that begin with .txt, such as .txt, .txt1, .txt_old.
    -   **dir read\*.txt** lists all files in the current directory that begin with "read" and with extensions that begin with .txt, such as .txt, .txt1, or .txt_old.
    -   **dir read\*.\*** lists all files in the current directory that begin with "read" with any extension.
    The asterisk wildcard always uses short file name mapping, so you might get unexpected results. for example, the following directory contains two files (t.txt2 and t97.txt):
    ```
    C:\test>dir /x
    volume in drive C has no label.
    volume Serial Number is B86A-EF32
    directory of C:\test
    11/30/2004  01:40 PM <dir>  .
    11/30/2004  01:40 PM <dir> ..
    11/30/2004  11:05 AM 0 T97B4~1.TXT t.txt2
    11/30/2004  01:16 PM 0 t97.txt
    ```
    You might expect that typing **dir t97\*** would return the file t97.txt. However, typing **dir t97\*** returns both files, because the asterisk wildcard matches the file t.txt2 to t97.txt by using its short name map T97B4~1.TXT. Similarly, typing **del t97\*** would delete both files.
    **Question mark (?):** Use the question mark as a substitute for a single character in a name. for example, typing **dir read .txt** lists any files in the current directory with the .txt extension that begin with "read" and are followed by up to three characters. This includes Read.txt, Read1.txt, Read12.txt, Read123.txt, and Readme1.txt, but not Readme12.txt.
-   Specifying file display attributes
    if you use **/a** with more than one value in *attributes*, **dir** displays the names of only those files with all the specified attributes. for example, if you use **/a** with **r** and **-h** as attributes (by using either **/a:r-h** or **/ar-h**), **dir** will only display the names of the read-only files that are not hidden.
-   Specifying file name sorting
    if you specify more than one *sortOrder* value, **dir** sorts the file names by the first criterion, then by the second criterion, and so on. for example, if you use **/o** with the **e** and **-s** values for *sortOrder* (by using either **/o:e-s** or **/oe-s**), **dir** sorts the names of directories and files by extension, with the largest first, and then displays the final result. The alphabetic sorting by extension causes file names with no extensions to appear first, then directory names, and then file names with extensions.
-   Using redirection symbols and pipes
    When you use the redirection symbol (**>**) to send **dir** output to a file or a pipe (**|**) to send **dir** output to another command, use **/a:-d** and **/b** to list the file names only. You can use *FileName* with **/b** and **/s** to specify that **dir** is to search the current directory and its subdirectories for all file names that match *FileName*. **dir** lists only the drive letter, directory name, file name, and file name extension (one path per line), for each file name it finds. Before you use a pipe to send **dir** output to another command, you should set the TEMP environment variable in your Autoexec.nt file.
-   The **dir** command, with different parameters, is available from the recovery Console.
## <a name="BKMK_examples"></a>Examples
To display all directories one after the other, in alphabetical order, in wide format, and pausing after each screen, make sure that the root directory is the current directory, and then type:
```
dir /s/w/o/p
```
**dir** lists the root directory, the subdirectories, and the files in the root directory, including extensions. Then, **dir** lists the subdirectory names and file names in each subdirectory in the tree.
To alter the preceding example so that **dir** displays the file names and extensions, but omits the directory names, type:
```
dir /s/w/o/p/a:-d
```
To print a directory listing, type:
```
dir > prn
```
When you specify **prn**, the directory list is sent to the printer that is attached to the LPT1 port. if your printer is attached to a different port, you must replace **prn** with the name of the correct port.
You can also redirect output of the **dir** command to a file by replacing **prn** with a file name. You can also type a path. for example, to direct **dir** output to the file dir.doc in the Records directory, type:
```
dir > \records\dir.doc
```
if dir.doc does not exist, **dir** creates it, unless the Records directory does not exist. In that case, the following message appears:
`File creation error`
To display a list of all the file names with the .txt extension in all directories on drive C, type:
```
dir c:\*.txt /w/o/s/p
```
**dir** displays, in wide format, an alphabetized list of the matching file names in each directory, and it pauses each time the screen fills until you press any key to continue.
#### additional references
[Command-Line Syntax Key](command-line-syntax-key.md)
