---
title: bitsadmin monitor
description: Windows Commands topic for **bitsadmin monitor**, which monitors jobs in the transfer queue that are owned by the current user.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2c424d27-e011-49c2-b579-a2c235467c39
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
---

# bitsadmin monitor

Monitors jobs in the transfer queue that are owned by the current user.

## Syntax

```
bitsadmin /monitor [/allusers] [/refresh <seconds>]
```

### Parameters

| Parameter | Description |
| -------------- | -------------- |
| /allusers | Optional. Monitors jobs for all users. You must have administrator privileges to use this parameter. |
| /refresh | Optional. Refreshes the data at an interval specified by `<seconds>`. The default refresh interval is five seconds. To stop the refresh, press CTRL+C. |

## <a name=BKMK_examples></a>Examples

The following example monitors the transfer queue for jobs owned by the current user and refreshes the information every 60 seconds.

```
C:\>bitsadmin /monitor /refresh 60
```

## Additional References

- [Command-Line Syntax Key](command-line-syntax-key.md)