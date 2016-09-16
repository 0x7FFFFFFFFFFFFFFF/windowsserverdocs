---
title: Data Deduplication Interoperability
ms.technology: storage-deduplication
ms.topic: article
author: wmgries
manager: eldenc
ms.author: wgries
ms.date: 09/15/2016
--- 

# Data Deduplication Interoperability
> Applies to Windows Server 2016

## <a id="supported"></a>Supported
### <a id="supported-branchcache"></a>BranchCache
Accessing data over the network can be optimized by enabling [BranchCache](../../networking/branchcache/branchcache.md) on servers and clients. When a BranchCache-enabled system communicates over a WAN with a remote file server that is running data deduplication, all of the deduplicated files are already indexed and hashed, so requests for data from a branch office are quickly computed. This is similar to preindexing or prehashing a BranchCache-enabled server.

### <a id="supported-clusters"></a>Failover Clusters
[Failover Clustering](../../failover-clustering/failover-clustering-overview.md) is fully supported, and provided that every node in the cluster has the [Data Deduplication feature installed](install-enable.md#install-dedup), deduplicated volumes will failover gracefully. Other important notes:
* [Manually started Data Deduplication jobs](run.md#running-dedup-jobs-manually) must be run on the Owner node for the Cluster Shared Volume.
* Deduplication schedules are managed by using the task scheduler and when a cluster is formed, the schedule information is put into the cluster scheduler so that if a deduplicated volume is taken over by another node, the scheduled job will be applied on the next scheduled interval.
* Data Deduplication fully interoperates with the [Cluster OS Rolling Upgrade](../../failover-clustering/cluster-operating-system-rolling-upgrade.md) feature.
* Data Deduplication is fully supported on [Storage Spaces Direct](../storage-spaces/storage-spaces-direct-overview.md) NTFS-formatted volumes (mirror or parity). Deduplication isn't supported on volumes with multiple tiers, see [Data Deduplication on ReFS](interop.md#unsupported-refs) for more information.

### <a id="supported-dfsr"></a>DFS Replication
Data Deduplication works fine with Distributed File System (DFS) Replication. Optimizing or unoptimizing a file will not trigger a replication because the file does not change. DFS Replication uses Remote Differential Compression (RDC), not the chunks in the chunk store, for over-the-wire savings. The files on the replica can also be optimized by using deduplication if the replica is using Data Deduplication.

### <a id="supported-quotas"></a>Quotas
Creating a hard quota on a volume root folder that also has deduplication enabled is not supported. When a hard quota is present on a volume root, the actual free space on the volume and the quota restricted space on the volume are not the same. This may cause deduplication optimization jobs to fail.

Creating a soft quota on a volume root that has deduplication enabled is supported. When quota encounter a deduplicated file, it accounts for it based on the file’s logical size. Quota usage (including any quota thresholds) does not change when a file is processed by deduplication. All other quota functionality, including volume-root soft quotas and quotas on subfolders, work normally when using deduplication.

### <a id="supported-windows-server-backup"></a>Windows Server Backup
Windows Server Backup has the ability to back up an optimized volume "as-is" (that is, without removing deduplicated data). The following steps show how to back up a volume and how to restore a volume or selected files from a volume:
1. Install Windows Server Backup by running the following Windows PowerShell command:  
    ```PowerShell
    Install-WindowsFeature -Name Windows-Server-Backup
    ```

2. To back up the E: volume to another volume, run the following, substituting the correct volume names for your situation:  
    ```PowerShell
    wbadmin start backup –include:E: -backuptarget:F: -quiet
    ```

3. Get the version ID of the backup you just created:
    ```PowerShell
    wbadmin get versions
    ```

    This output version ID will be a date and time string, for example: 08/18/2016-06:22.

4. Restore the entire volume:
    ```PowerShell
    wbadmin start recovery –version:02/16/2012-06:22 -itemtype:Volume  -items:E: -recoveryTarget:E:
    ```

    **--OR--**  

    Restore a particular folder (in this case, the E:\Docs folder):
    ```PowerShell
    wbadmin start recovery –version:02/16/2012-06:22 -itemtype:File  -items:E:\Docs  -recursive
    ```

## <a id="unsupported"></a>Unsupported
### <a id="unsupported-refs"></a>ReFS
Data Deduplication on ReFS-formatted volumes is not supported in Windows Server 2016.

### <a id="unsupported-windows-search"></a>Windows Search
Windows Search unfortunately doesn’t support Data Deduplication. Because Data Deduplication uses reparse points, which Windows Search can’t index, Windows Search skips all deduplicated files, excluding them from the index. As a result, search results might be incomplete for deduplicated volumes.

### <a id="unsupported-robocopy"></a>Robocopy
Running Robocopy with Data Deduplication is not recommended because certain Robocopy commands can corrupt the Chunk Store. The Chunk Store is stored in the System Volume Information folder for a Volume. If the folder is deleted, the optimized files (reparse points) that are copied from the source volume become corrupted because the data chunks are not copied to the destination volume.  