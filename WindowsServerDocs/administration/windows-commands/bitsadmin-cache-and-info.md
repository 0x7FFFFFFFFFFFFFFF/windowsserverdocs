---
title: bitsadmin cache and info
description: Windows Commands topic for **bitsadmin cache and info**, which dumps a specific cache entry.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 15975cbf-dba6-49ca-a725-d15ce1952de5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
---

# bitsadmin cache and info

Dumps a specific cache entry.

## Syntax

```
bitsadmin /cache /info recordID [/verbose]
```

### Parameters

| Paramreter | Description |
| -------------- | -------------- |
| recordID | The GUID associated with the cache entry. |

## <a name=BKMK_examples></a>Examples

The following example dumps the cache entry with the recordID value of {6511FB02-E195-40A2-B595-E8E2F8F47702}.

```
C:\>bitsadmin /cache /info {6511FB02-E195-40A2-B595-E8E2F8F47702}
```

## Additional References

- [Command-Line Syntax Key](command-line-syntax-key.md)