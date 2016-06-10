---
title: Server Message Block Overview
ms.custom: na
ms.prod: windows-server-2012
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d5399314-77e2-4d73-889d-d62f062cb0cc
author: JasonGerend
---
# Server Message Block Overview
This topic describes the SMB 3.0 feature in Windows Server® 2012 \-\- practical uses for the feature, the most significant new or updated functionality in this version compared to previous versions, and the hardware requirements.  
  
## Feature description  
The Server Message Block \(SMB\) protocol is a network file sharing protocol that allows applications on a computer to read and write to files and to request services from server programs in a computer network. The SMB protocol can be used on top of its TCP\/IP protocol or other network protocols. Using the SMB protocol, an application \(or the user of an application\) can access files or other resources at a remote server. This allows applications to read, create, and update files on the remote server. It can also communicate with any server program that is set up to receive an SMB client request.  Windows Server 2012  introduces the new 3.0 version of the SMB protocol.  
  
## Practical applications  
This section discusses some new practical ways to use the new SMB 3.0 protocol.  
  
**File storage for virtualization \(Hyper\-V™ over SMB\)**. Hyper\-V can store virtual machine files, such as configuration, Virtual hard disk \(VHD\) files, and snapshots, in file shares over the SMB 3.0 protocol. This can be used for both stand\-alone file servers and clustered file servers that use Hyper\-V together with shared file storage for the cluster.  
  
**Microsoft SQL Server over SMB**. SQL Server can store user database files on SMB file shares. Currently, this is supported with SQL Server 2008 R2 for stand\-alone SQL servers. Upcoming versions of SQL Server will add support for clustered SQL servers and system databases.  
  
**Traditional storage for end\-user data**. The SMB 3.0 protocol provides enhancements to the Information Worker \(or client\) workloads. These enhancements include reducing the application latencies experienced by branch office users when accessing data over wide area networks \(WAN\) and protecting data from eavesdropping attacks.  
  
## New and changed functionality  
For information on new and changed functionality in  Windows Server 2012 R2 , see [What's New for SMB](assetId:///46c0ac80-a54a-4324-948a-2dee66bcec75).  
  
SMB in  Windows Server 2012  includes the new SMB 3.0 protocol and many new improvements which are described in the following table.  
  
|Feature\/functionality|New or updated|Summary|  
|--------------------------|------------------|-----------|  
|SMB Transparent Failover|New|Enables administrators to perform hardware or software maintenance of nodes in a clustered file server without interrupting server applications storing data on these file shares. Also, if a hardware or software failure occurs on a cluster node, SMB clients transparently reconnect to another cluster node without interrupting server applications that are storing data on these file shares.|  
|SMB Scale Out|New|Using Cluster Shared Volumes \(CSV\) version 2, administrators can create file shares that provide simultaneous access to data files, with direct I\/O, through all nodes in a file server cluster. This provides better utilization of network bandwidth and load balancing of the file server clients, and optimizes performance for server applications.|  
|SMB Multichannel|New|Enables aggregation of network bandwidth and network fault tolerance if multiple paths are available between the SMB 3.0 client and the SMB 3.0 server. This enables server applications to take full advantage of all available network bandwidth and be resilient to a network failure.|  
|SMB Direct|New|Supports the use of network adapters that have RDMA capability and can function at full speed with very low latency, while using very little CPU. For workloads such as Hyper\-V or Microsoft SQL Server, this enables a remote file server to resemble local storage.|  
|Performance Counters for server applications|New|The new SMB performance counters provide detailed, per\-share information about throughput, latency, and I\/O per second \(IOPS\), allowing administrators to analyze the performance of SMB 3.0 file shares where their data is stored. These counters are specifically designed for server applications, such as Hyper\-V and SQL Server, which store files on remote file shares.|  
|Performance optimizations|Updated|Both the SMB 3.0 client and SMB 3.0 server have been optimized for small random read\/write I\/O, which is common in server applications such as SQL Server OLTP. In addition, large Maximum Transmission Unit \(MTU\) is turned on by default, which significantly enhances performance in large sequential transfers, such as SQL Server data warehouse, database backup or restore, deploying or copying virtual hard disks.|  
|SMB\-specific Windows PowerShell cmdlets|New|With Windows PowerShell cmdlets for SMB, an administrator can manage file shares on the file server, end to end, from the command line.|  
|SMB Encryption|New|Provides end\-to\-end encryption of SMB data and protects data from eavesdropping occurrences on untrusted networks. Requires no new deployment costs, and no need for Internet Protocol security \(IPsec\), specialized hardware, or WAN accelerators. It may be configured on a per share basis, or for the entire file server, and may be enabled for a variety of scenarios where data traverses untrusted networks.|  
|SMB Directory Leasing|New|Improves application response times in branch offices. With the use of directory leases, roundtrips from client to server are reduced since metadata is retrieved from a longer living directory cache. Cache coherency is maintained because clients are notified when directory information on the server changes. Works with scenarios for *HomeFolder* \(read\/write with no sharing\) and *Publication* \(read\-only with sharing\).|  
  
## Hardware requirements  
SMB Transparent Failover has the following requirements:  
  
-   A failover cluster running  Windows Server 2012  with at least two nodes configured. The cluster must pass the cluster validation tests included in the validation wizard.  
  
-   File shares must be created with the Continuous Availability \(CA\) property, which is the default.  
  
-   File shares must be created on CSV volume paths to attain SMB Scale\-Out.  
  
-   Client computers must be running Windows® 8 or  Windows Server 2012 , both of which include the updated SMB client that supports continuous availability.  
  
> [!NOTE]  
> Note that down\-level clients can connect to file shares that have the CA property, but transparent failover will not be supported for these clients.  
  
SMB Multichannel has the following requirements:  
  
-   At least two computers running  Windows Server 2012  are required. No extra features need to be installed—the technology is on by default.  
  
-   For information on recommended network configurations, see the See Also section at the end of this overview topic.  
  
SMB Direct has the following requirements:  
  
-   At least two computers running  Windows Server 2012  are required. No extra features need to be installed—the technology is on by default.  
  
-   Network adapters with RDMA capability are required. Currently, these adapters are available in three different types: iWARP, Infiniband, or RoCE \(RDMA over Converged Ethernet\).  
  
## See also  
The following list provides additional resources on the web about SMB and related technologies in  Windows Server 2012 R2  and  Windows Server 2012 .  
  
-   [File and Storage Services Overview](File-and-Storage-Services-Overview.md)  
  
-   [Scale-Out File Server for Application Data Overview_1](Scale-Out-File-Server-for-Application-Data-Overview_1.md)  
  
-   [Deploy Hyper\-V over SMB](assetId:///5a169fa2-f5c8-4c0d-a122-79ecdbdebc98)  
  
-   [Deploy SMB Multichannel](../smb/Deploy-SMB-Multichannel.md)  
  
-   [Improve Performance of a File Server with SMB Direct](../smb/Improve-Performance-of-a-File-Server-with-SMB-Direct.md)  
  
-   [Deploying Fast and Efficient File Servers for Server Applications](http://technet.microsoft.com/library/hh831723.aspx)  
  
-   [SMB: Troubleshooting Guide](../smb/SMB--Troubleshooting-Guide.md)  
  

