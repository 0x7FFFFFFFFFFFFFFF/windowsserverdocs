---
title: bitsadmin list
description: Windows Commands topic for **bitsadmin list**, which lists the transfer jobs owned by the current user.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1416965e-e0e6-49cf-b1d4-b286d3cf8716
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
---

# bitsadmin list

Lists the transfer jobs owned by the current user.

## Syntax

```
bitsadmin /list [/allusers][/verbose]
```

### Parameters

| Parameter | Description |
| -------------- | -------------- |
| /allusers | Optional. Lists jobs for all users. You must have administrator privileges to use this parameter. |
| /verbose | Optional. Provides detailed information about each job. |

## <a name=BKMK_examples></a>Examples

The following example retrieves information about jobs owned by the current user.

```
C:\>bitsadmin /list
```

## Additional References

- [Command-Line Syntax Key](command-line-syntax-key.md)