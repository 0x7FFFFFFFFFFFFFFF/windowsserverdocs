---
title: Store
description: 
author: JasonGerend
manager: elizapo
layout: LandingPage
ms.prod: windows-server-threshold
ms.technology: storage
ms.assetid: 6b74bc7c-a58d-4915-af8e-2cc27f2c4726
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: landing-page
ms.author: jgerend
ms.localizationpriority: medium
---
# Store

>Applies To: Windows Server (Semi-Annual Channel), Windows Server 2016

>[!TIP]
> Looking for information about older versions of Windows Server? Check out our other [Windows Server libraries](/previous-versions/windows/) on docs.microsoft.com. You can also [search this site](https://docs.microsoft.com/search/index?search=Windows+Server&dataSource=previousVersions) for specific information.

Storage in Windows Server provides new and improved features for software-defined datacenter (SDDC) customers focusing on virtualized workloads. Windows Server also provides extensive support for enterprise customers using file servers with existing workloads.

<hr />
<ul class="cardsF panelContent">
<li>
 <a href="get-started-19/whats-new-19.md">
                            <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-whats-new.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                            <h2>What's new?</h2>
                                            <p>Find out what's new in Windows Server</p>
                                        </div>
                                    </div>
                                </div>
                            </div>
                          </a>
                        </li>
</ul>
<hr />
<ul class="cardsF panelContent">
<li>
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-store.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h2>Software-defined storage for virtualized workloads</h2>
<HR />
                        <p><h3><a href="storage-spaces/storage-spaces-direct-overview.md">Storage Spaces Direct</a></h3> Directly attached local storage, including SATA and NVME devices, to optimize disk usage after adding new physical disks, and for faster virtual disk repair times. Also see [Storage Spaces]<a href="storage-spaces/overview.md">Storage Spaces</a> for info on shared SAS and stand-alone Storage Spaces.</p>
<HR />
                        <p><h3><a href="storage-replica/storage-replica-overview.md">Storage Replica</a></h3> Storage-agnostic, block-level, synchronous replication between clusters or servers for disaster preparedness and recovery, as well as stretching of a failover cluster across sites for high availability. Synchronous replication enables mirroring of data in physical sites with crash-consistent volumes, ensuring zero data loss at the file system level.</p>
<HR />
                        <p><h3><a href="storage-qos/storage-qos-overview.md">Storage Quality of Service (QoS)</a></h3> Centrally monitor and manage storage performance for virtual machines using Hyper-V and the Scale-Out File Server roles automatically improveing storage resource fairness between multiple virtual machines using the same file server cluster.</p>
<HR />
                        <p><h3><a href="data-deduplication/overview.md">Data Deduplication</a></h3> Optimizes free space on a volume by examining the data on the volume for duplication. Once identified, duplicated portions of the volume's dataset are stored once and are (optionally) compressed for additional savings. Data Deduplication optimizes redundancies without compromise data fidelity or integrity.</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<li>
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-store.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h2>General-purpose file servers</h2>
<HR />
                        <p><h3><a href="work-folders/work-folders-overview.md">Work Folders</a></h3> Store and access work files on personal computers and devices, often referred to as bring-your-own device (BYOD), in addition to corporate PCs. Users gain a convenient location to store work files, and they can access them from anywhere. Organizations maintain control over corporate data by storing the files on centrally managed file servers, and optionally specifying user device policies such as encryption and lock-screen passwords.</p>
<HR />
                        <p><h3><a href="folder-redirection/folder-redirection-rup-overview.md">Offline Files and Folder Redirection</a></h3> Redirect the path of local folders (such as the Documents folder) to a network location, while caching the contents locally for increased speed and availability.</p>
<HR />
                        <p><h3><a href="folder-redirection/deploy-roaming-user-profiles.md">Roaming User Profiles</a></h3> Redirect a user profile to a network location.</p>
<HR />
                        <p><h3><a href="dfs-namespaces/dfs-overview.md">DFS Namespaces</a></h3> Group shared folders that are located on different servers into one or more logically structured namespaces. Each namespace appears to users as a single shared folder with a series of subfolders. However, the underlying structure of the namespace can consist of numerous file shares that are located on different servers and in multiple sites.</p>
<HR />
                        <p><h3><a href="https://technet.microsoft.com/library/jj127250(v=ws.11).aspx">DFS Replication</a></h3> Replicate folders (including those referred to by a DFS namespace path) across multiple servers and sites. DFS Replication uses a compression algorithm known as remote differential compression (RDC). RDC detects changes to the data in a file, and it enables DFS Replication to replicate only the changed file blocks instead of the entire file.</p>
<HR />
                        <p><h3><a href="fsrm/fsrm-overview.md">File Server Resource Manager</a></h3> Manage and classify data stored on file servers.<p>
<HR />
                        <p><h3><a href="https://technet.microsoft.com/library/hh848272(v=ws.11).aspx">iSCSI Target Server</a></h3> Provides block storage to other servers and applications on the network by using the Internet SCSI (iSCSI) standard.</p>
<HR />
                       <p><h3><a href="iscsi/iscsi-boot-overview.md">iSCSI Target Server</a></h3> Can boot hundreds of computers from a single operating system image that is stored in a centralized location. This improves efficiency, manageability, availability, and security.</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<li>
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-store.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h2>File systems, protocols, etc.</h2>
<HR />
                        <p><h3><a href="refs/refs-overview.md">ReFS</a></h3> A resilient file system that maximizes data availability, scales efficiently to very large data sets across diverse workloads, and provides data integrity by means of resiliency to corruption (regardless of software or hardware failures).<p>
<HR />
                        <p><h3><a href="file-server/file-server-smb-overview.md">Server Message Block (SMB) protocol</a></h3> A network file sharing protocol that allows applications on a computer to read and write to files and to request services from server programs in a computer network. The SMB protocol can be used on top of its TCP/IP protocol or other network protocols. Using the SMB protocol, an application (or the user of an application) can access files or other resources at a remote server. This allows applications to read, create, and update files on the remote server. It can also communicate with any server program that is set up to receive an SMB client request.<p>
<HR />
                        <p><h3><a href="storage-spaces/Storage-class-memory-health.md">Storage-class memory</a></h3> Provides performance similar to computer memory (really fast), but with the data persistence of normal storage drives. Windows treats storage-class memory similary to normal drives (just faster), but there are some differences in the way device health is managed.<p>
<HR />
                        <p><h3><a href="https://technet.microsoft.com/library/cc766295(v=ws.10).aspx">BitLocker Drive Encryption</a></h3> Stores data on volumes in an encrypted format, even if the computer is tampered with or when the operating system is not running. This helps protect against offline attacks, attacks made by disabling or circumventing the installed operating system, or made by physically removing the hard drive to attack the data separately.<p>
<HR />
                        <p><h3><a href="https://technet.microsoft.com/library/dn466522(v=ws.11).aspx">NTFS</a></h3> The primary file system for recent versions of Windows and Windows Server—provides a full set of features including security descriptors, encryption, disk quotas, and rich metadata, and can be used with Cluster Shared Volumes (CSV) to provide continuously available volumes that can be accessed simultaneously from multiple nodes of a Failover Cluster.<p>
<HR />
                        <p><h3><a href="https://technet.microsoft.com/library/jj592688(v=ws.11).aspx">Network File System (NFS)</a></h3> Provides a file sharing solution for enterprises that have heterogeneous environments that consist of both Windows and non-Windows computers.<p>
                    </div>
                </div>
            </div>
        </div>
    </li>
</ul>

---


## See also

* [What's new in storage](whats-new-in-storage.md)
* [What's new in Failover Clustering](../failover-clustering/whats-new-in-failover-clustering.md)
* [Windows IT Pro Support](https://www.microsoft.com/itpro/windows/support)
* [PowerShell cmdlets in Windows Server 2016 and Windows 10](https://technet.microsoft.com/library/mt156917.aspx)
* [Azure Storage](https://azure.microsoft.com/documentation/services/storage/)
* [Azure StorSimple](https://www.microsoft.com/en-us/cloud-platform/azure-storsimple)
