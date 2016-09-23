---
title: Storage Replica Overview
ms.prod: windows-server-threshold
manager: dongill
ms.author: JGerend
ms.technology: storage-replica
ms.topic: get-started-article
author: kumudd
ms.date: 09/23/2016
ms.assetid: e9b18e14-e692-458a-a39f-d5b569ae76c5
---
# Storage Replica Overview

>Applies To: Windows Server 2016

This topic provides an overview of the new Storage Replica feature in Windows Server 2016 and includes the following sections:  
* [Goals and Supported Replication Scenarios](#BKMK_SR1)  
* [Storage Replica Features](#BKMK_SR2)  
* [Storage Replica Prerequisites](#BKMK_SR3)  
* [Background](#BKMK_SR4)    

## <a name="BKMK_SR1"></a> Goals and Supported Replication Scenarios  
This guide outlines how your business can benefit from this new functionality and the different replication scenarios that are supported by Storage Replica. It assumes that you have a previous working knowledge of Windows Server, Failover Clustering, File Servers, and Hyper-V, to include basic administration.  

### Why use Storage Replica?  
Storage Replica offers new disaster recovery and preparedness capabilities in Windows Server 2016. For the first time, Windows Server offers the peace of mind of zero data loss, with the ability to synchronously protect data on different racks, floors, buildings, campuses, counties, and cities. After a disaster strikes, all data will exist elsewhere without any possibility of loss. The same applies *before* a disaster strikes; Storage Replica offers you the ability to switch workloads to safe locations prior to catastrophes when granted a few moments warning - again, with no data loss.  

Storage Replica allows more efficient use of multiple datacenters. By stretching clusters or replicating clusters, workloads can be run in multiple datacenters for quicker data access by local proximity users and applications, as well as better load distribution and use of compute resources. If a disaster takes one datacenter offline, you can move its typical workloads to the other site temporarily.  

Storage Replica may allow you to decommission existing file replication systems like DFSR that were pressed into duty as low-end disaster recovery solutions. While DFSR works very well over extremely low bandwidth networks, its latency is very high - often measured in hours or days. This is caused by its requirement for files to close and its artificial throttles meant to prevent network congestion. With those design characteristics, the newest and hottest files in a DFSR replica are the least likely to replicate. Storage Replica operates below the file level and has none of these restrictions.  

Storage Replica also supports asynchronous replication for longer ranges and higher latency networks. Because it is not checkpoint-based, and instead continuously replicates, the delta of changes will tend to be far lower than snapshot-based products. Furthermore, Storage Replica operates at the partition layer and therefore replicates all VSS snapshots created by Windows Server or backup software; this allows use of application-consistent data snapshots for point in time recovery, especially unstructured user data replicated asynchronously.  

### <a name="BKMK_SRSupportedScenarios"></a>Supported Storage Replica configurations in Windows Server 2016  
Using this guide and Windows Server 2016, you can deploy storage replication in a stretch cluster, between cluster-to-cluster, and in server-to-server configurations (see Figures 1-3).

**Stretch Cluster** allows configuration of computers and storage in a single cluster, where some nodes share one set of asymmetric storage and some nodes share another, then synchronously or asynchronously replicate with site awareness. This scenario can utilize shared Storage Spaces on JBOD, SAN and iSCSI-attached LUNs. It is managed with PowerShell and the Failover Cluster Manager graphical tool, and allows for automated workload failover.  

![](./media/Storage-Replica-Overview/Storage_SR_StretchCluster.png)  

**FIGURE 1: Storage replication in a stretch cluster using Storage Replica**  

**Cluster to Cluster** allows replication between two separate clusters, where one cluster synchronously or asynchronously replicates with another cluster. This scenario can utilize shared Storage Spaces on JBOD, SAN and iSCSI-attached LUNs. It is managed with PowerShell and requires manual intervention for failover.  

![](./media/Storage-Replica-Overview/Storage_SR_ClustertoCluster.png)  

**FIGURE 2: Cluster-to-cluster storage replication using Storage Replica**  

**Server to server** allows synchronous and asynchronous replication between two standalone servers, using Storage Spaces on JBOD, SAN and iSCSI-attached LUNs, and local drives. It is managed with PowerShell and requires manual intervention for failover.  

![](./media/Storage-Replica-Overview/Storage_SR_ServertoServer.png)  

**FIGURE 3: Server-to-server storage replication using Storage Replica**  

> [!NOTE]
> You can also configure server-to-self replication, using four separate volumes on one computer. However, this guide does not cover this scenario.  

## <a name="BKMK_SR2"> </a> Storage Replica Features  

* **Zero data loss, block-level replication**. With synchronous replication, there is no possibility of data loss. With block-level replication, there is no possibility of file locking.  

* **Simple deployment and management**. Storage Replica has a design mandate for ease of use. Creation of a replication partnership between two servers requires only a single PowerShell command. Deployment of stretch clusters uses intuitive wizard in the familiar Failover Cluster Manager tool.   

* **Guest and host**. All capabilities of Storage Replica are exposed in both virtualized guest and host-based deployments. This means guests can replicate their data volumes even if running on non-Windows virtualization platforms or in public clouds, as long as using Windows Server 2016 in the guest.  

* **SMB3-based**. Storage Replica uses the proven and mature technology of SMB 3, first released in Windows Server 2012. This means all of SMB's advanced characteristics - such as multichannel and SMB direct support on RoCE, iWARP, and InfiniBand RDMA network cards - are available to Storage Replica.   

* **Security**. Unlike many vendor's products, Storage Replica has industry-leading security technology baked in. This includes packet signing, AES-128-GCM full data encryption, support for Intel AES-NI encryption acceleration, and pre-authentication integrity man-in-the-middle attack prevention. Storage Replica utilizes Kerberos AES256 for all authentication between nodes.  

* **High performance initial sync**. Storage Replica supports seeded initial sync, where a subset of data already exists on a target from older copies, backups, or shipped drives. Initial replication will only copy the differing blocks, potentially shortening initial sync time and preventing data from using up limited bandwidth. Storage replicas block checksum calculation and aggregation means that initial sync performance is limited only by the speed of the storage and network.  

* **Consistency groups**. Write ordering guarantees that applications such as Microsoft SQL Server can write to multiple replicated volumes and know the data will write on the destination server sequentially.  

* **User delegation**. Users can be delegated permissions to manage replication without being a member of the built-in Administrators group on the replicated nodes, therefore limiting their access to unrelated areas.  

* **Network Constraint**. Storage Replica can be limited to individual networks by server and by replicated volumes, in order to provide application, backup, and management software bandwidth.  

* **Thin provisioning**. Support for thin provisioning in Storage Spaces and SAN devices is supported, in order to provide near-instantaneous initial replication times under many circumstances.  

Windows Server 2016 implements the following features in Storage Replica:  

|Feature|Details|  
|-----------|-----------|  
|Type|Host-based|  
|Synchronous|Yes|  
|Asynchronous|Yes|  
|Storage hardware agnostic|Yes|  
|Replication unit|Volume (Partition)|  
|Windows Server Stretch Cluster creation|Yes|  
|Server to server replication|Yes|  
|Cluster to cluster replication|Yes|  
|Transport|SMB3|  
|Network|TCP/IP or RDMA|
|Network constraint support|Yes|  
|RDMA*|iWARP, InfiniBand, RoCE v2|  
|Replication network port firewall requirements|Single IANA port (TCP 445 or 5445)|  
|Multipath/Multichannel|Yes (SMB3)|  
|Kerberos support|Yes (SMB3)|  
|Over the wire encryption and signing|Yes (SMB3)|  
|Per-volume failovers allowed|Yes|
|Thin-provisioned storage support|Yes|
|Management UI in-box|PowerShell, Failover Cluster Manager|  

*May require additional long haul equipment and cabling.  

## <a name="BKMK_SR3"></a> Storage Replica Prerequisites  

* Active Directory Domain Services forest.  
* SAS JBODs, Storage Spaces Direct, fibre channel SAN, shared VHDX, iSCSI Target, or local SAS/SCSI/SATA storage. SSD or faster recommended for replication log drives.  
* At least one 1GbE connection on each server for synchronous replication, but preferably RDMA.   
* At least 2GB of RAM and two cores per server.  
* A network between servers with enough bandwidth to contain your IO write workload and an average of 5ms round trip latency or lower, for synchronous replication. Asynchronous replication does not have a latency recommendation.  

##  <a name="BKMK_SR4"> </a> Background  
This section includes information about high-level industry terms, synchronous and asynchronous replication, and key behaviors.
### High level industry terms  
Disaster Recovery (DR) refers to a contingency plan for recovering from site catastrophes so that the business continues to operate. Data DR means multiple copies of production data in a separate physical location. For example, a stretch cluster, where half the nodes are in one site and half are in another. Disaster Preparedness (DP) refers to a contingency plan for preemptively moving workloads to a different location prior to an oncoming disaster, such as a hurricane.  

Service level agreements (SLAs) define the availability of a business' applications and their tolerance of down time and data loss during planned and unplanned outages. Recovery Time Objective (RTO) defines how long the business can tolerate total inaccessibility of data. Recovery Point Objective (RPO) defines how much data the business can afford to lose.  

### Synchronous Replication  
Synchronous replication guarantees that the application writes data to two locations at once before completion of the IO. This replication is more suitable for mission critical data, as it requires network and storage investments, as well as a risk of degraded application performance.  

When application writes occur on the source data copy, the originating storage does not acknowledge the IO immediately. Instead, those data changes replicate to the remote destination copy and return an acknowledgement. Only then does the application receive the IO acknowledgment. This ensures constant synchronization of the remote site with the source site, in effect extending storage IOs across the network. In the event of a source site failure, applications can failover to the remote site and resume their operations with assurance of zero data loss.  

|Mode|Diagram|Steps|  
|--------|-----------|---------|  
|**Synchronous**<br /><br />Zero Data Loss<br /><br />RPO|![](./media/Storage-Replica-Overview/Storage_SR_SynchronousV2.png)|1.  Application writes data<br />2.  Log data is written and the data is replicated to the remote site<br />3.  Log data is written at the remote site<br />4.  Acknowledgement from the remote site<br />5.  Application write acknowledged<br /><br />t & t1 : Data flushed to the volume, logs always write through|  

### Asynchronous Replication  
Contrarily, asynchronous replication means that when the application writes data, that data replicates to the remote site without immediate acknowledgment guarantees. This mode allows faster response time to the application as well as a DR solution that works geographically.  

When the application writes data, the replication engine captures the write and immediately acknowledges to the application. The captured data then replicates to the remote location. The remote node processes the copy of the data and lazily acknowledges back to the source copy. Since replication performance is no longer in the application IO path, the remote site's responsiveness and distance are less important factors. There is risk of data loss if the source data is lost and the destination copy of the data was still in buffer without leaving the source.  

With its higher than zero RPO, asynchronous replication is less suitable for HA solutions like Failover Clusters, as they are designed for continuous operation with redundancy and no loss of data.  

|Mode|Diagram|Steps|  
|--------|-----------|---------|  
|**Asynchronous**<br /><br />Near zero data loss<br /><br />(depends on multiple factors)<br /><br />RPO|![](./media/Storage-Replica-Overview/Storage_SR_AsynchronousV2.png)|1.  Application writes data<br />2.  Log data written<br />3.  Application write acknowledged<br />4.  Data replicated to the remote site<br />5.  Log data written at the remote site<br />6.  Acknowledgement from the remote site<br /><br />t & t1 : Data flushed to the volume, logs always write through|  

### Key Evaluation Points and Behaviors  
-   Performance. The Windows Server 2016 Technical Preview version of Storage Replica has not been fully optimized for performance.  

-   Network bandwidth and latency with fastest storage. There are physical limitations around synchronous replication. Because SR implements an IO filtering mechanism using logs and requiring network round trips, synchronous replication is likely make application writes slower. By using low latency, high-bandwidth networks as well as high-throughput disk subsystems for the logs, you will minimize performance overhead.  

-   The destination volume is not accessible while replicating. When you configure replication, the destination volume dismounts, making it inaccessible to any writes by users or visible in typical interfaces like File Explorer. Block-level replication technologies are incompatible with allowing access to the destination target's mounted file system in a volume; NTFS and ReFS do not support users writing data to the volume while blocks change underneath them.  

-   The Microsoft implementation of asynchronous replication is different than most. Most industry implementations of asynchronous replication rely on snapshot-based replication, where periodic differential transfers move to the other node and merge. Storage Replica asynchronous replication operates just like synchronous replication, except that it removes the requirement for a serialized synchronous acknowledgment from the destination. This means that SR theoretically has a lower RPO as it continuously replicates. However, this also means it relies on internal application consistency guarantees rather than using snapshots to force consistency in application files. SR guarantees crash consistency in all replication modes  

-   Many customers use DFSR as a disaster recovery solution even though often impractical for that scenario - DFSR cannot replicate open files and is designed to minimize bandwidth usage at the expense of performance, leading to large recovery point deltas. SR may allow you to retire DFSR from some of these types of disaster recovery duties.  

-   Storage Replica is not backup. Some IT environments deploy replication systems as backup solutions, due to their zero data loss options when compared to daily backups. SR replicates all changes to all blocks of data on the volume, regardless of the change type. If a user deletes all data from a volume, Storage Replica will replicate the deletion instantly to the other volume, irrevocably removing the data from both servers. Do not use SR as a replacement for a point-in-time backup solution.  

-   Storage Replica is not Hyper-V Replica or Microsoft SQL AlwaysOn Availability Groups. Storage Replica is a general purpose, storage-agnostic engine. By definition, it cannot tailor its behavior as ideally as application-level replication. This may lead to specific feature gaps that encourage you to deploy or remain on specific application replication technologies.  

> [!NOTE]
> This document contains a list of [known issues](storage-replica--known-issues.md) and expected behaviors as well as [Frequently Asked Questions](storage-replica--frequently-asked-questions.md) section.
 
### Storage Replica terminology  
This guide frequently uses the following terms:  

-   The source is a computer's volume that allows local writes and replicates outbound. Also known as "primary".  

-   The destination is a computer's volume that does not allow local writes and replicates inbound. Also known as "secondary".   

-   A replication partnership is the synchronization relationship between a source and destination computer for one or more volumes and utilizes a single log.  

-   A replication group is the organization of volumes and their replication configuration within a partnership, on a per server basis. A group may contain one or more volumes.  

## Related Topics  
- [Stretch Cluster Replication Using Shared Storage](stretch-cluster-replication-using-shared-storage.md)  
- [Server to Server Storage Replication](server-to-server-storage-replication.md)  
- [Cluster to Cluster Storage Replication](cluster-to-cluster-storage-replication.md)  
- [Storage Replica: Known Issues](storage-replica--known-issues.md)  
- [Storage Replica: Frequently Asked Questions](storage-replica--frequently-asked-questions.md)  

## See Also  
- [Windows Server 2016](../../get-started/Windows-Server-2016-Technical-Preview-5.md)  
- [Storage Spaces Direct in Windows Server 2016](../storage-spaces/storage-spaces-direct-overview.md)  
