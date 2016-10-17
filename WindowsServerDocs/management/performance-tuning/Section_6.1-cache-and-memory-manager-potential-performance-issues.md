---
title: Cache and Memory Manager Potential Performance Issues
description: Cache and Memory Manager Potential Performance Issues
---

# Cache and Memory Manager Potential Performance Issues

Before Windows Server 2012, two primary potential issues caused system file cache to grow until available memory was almost depleted under certain workloads. When this situation results in the system being sluggish, you can determine whether the server is facing one of these issues.

**In this topic:**

-   [Counters to monitor](#counters-to-monitor)

-   [System file cache contains NTFS metafile data structures](#system-file-cache-contains-ntfs-metafile-data-structures)

-   [System file cache contains memory mapped files](#system-file-cache-contains-memory-mapped-files)

## Counters to monitor

-   Memory\\Long-Term Average Standby Cache Lifetime (s) &lt; 1800 seconds

-   Memory\\Available Mbytes is low

-   Memory\\System Cache Resident Bytes

If Memory\\Available Mbytes is low and at the same time Memory\\System Cache Resident Bytes is consuming significant part of the physical memory, you can use [RAMMAP](http://technet.microsoft.com/sysinternals/ff700229.aspx) to find out what the cache is being used for.

## System file cache contains NTFS metafile data structures


This problem is indicated by a very high number of active Metafile pages in RAMMAP output, as shown in the following figure. This problem might have been observed on busy servers with millions of files being accessed, thereby resulting in caching NTFS metafile data not being released from the cache.

![rammap view](../media/performance-tuning/perftune-guide-rammap.png)

The problem used to be mitigated by *DynCache* tool. In Windows Server 2012, the architecture has been redesigned and this problem should no longer exist.

## System file cache contains memory mapped files


This problem is indicated by very high number of active Mapped file pages in RAMMAP output. This usually indicates that some application on the server is opening a lot of large files using [CreateFile](http://msdn.microsoft.com/library/windows/desktop/aa363858.aspx) API with FILE\_FLAG\_RANDOM\_ACCESS flag set.

This issue is described in detail in KB article [2549369](http://support.microsoft.com/default.aspx?scid=kb;en-US;2549369). FILE\_FLAG\_RANDOM\_ACCESS flag is a hint for Cache Manager to keep mapped views of the file in memory as long as possible (until Memory Manager doesn’t signal low memory condition). At the same time, this flag instructs Cache Manager to disable prefetching of file data.

This situation has been mitigated to some extent by working set trimming improvements in Windows Server 2012 and Windows Server 2012 R2, but the issue itself needs to be primarily addressed by the application vendor by not using FILE\_FLAG\_RANDOM\_ACCESS. An alternative solution for the app vendor might be to use low memory priority when accessing the files. This can be achieved using the [SetThreadInformation](http://msdn.microsoft.com/library/windows/desktop/hh448390.aspx) API. Pages that are accessed at low memory priority are removed from the working set more aggressively.

## Related topics

[Performance Tuning for Cache and Memory Manager Subsystems](performance-tuning-for-cache-and-memory-manager-subsystems.md)
