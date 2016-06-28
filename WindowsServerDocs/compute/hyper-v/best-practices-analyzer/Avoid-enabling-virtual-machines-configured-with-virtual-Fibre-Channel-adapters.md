---
title: Avoid enabling virtual machines configured with virtual Fibre Channel adapters to allow live migrations when there are fewer paths to Fibre Channel logical units (LUNs) on the destination than on the source
description: " "
ms.prod: windows-server-threshold
ms.service: na
manager: timlt
ms.technology: 
  - hyper-v
  - techgroup-compute
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9f5ddb52-bfb2-4d57-90e5-3e1bf595941c
author: KBDAzure
---
# Avoid enabling virtual machines configured with virtual Fibre Channel adapters to allow live migrations when there are fewer paths to Fibre Channel logical units (LUNs) on the destination than on the source

>Applies To: Windows Server Technical Preview

[This information is preliminary and subject to change.]  
  
For more information about best practices and scans, see [Run Best Practices Analyzer Scans and Manage Scan Results](http://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|||  
|-|-|  
|**Operating System**|Windows Server 2016 Technical Preview|  
|**Product/Feature**|Hyper-V|  
|**Severity**|Warning|  
|**Category**|Configuration|  
  
## **Issue**  
*One or more virtual machines have the AllowReducedFcRedunancy property set in the virtualization WMI provider.*  
  
## **Impact**  
*Live migration of the following virtual machines might lead to data loss or interrupt I/O to storage:*  
  
\<list of virtual machines>  
  
## **Resolution**  
*Consider clearing the AllowReducedFcRedundancy WMI property on the affected virtual machines. When this property is cleared, you can perform a live migration on virtual machines configured with virtual Fibre Channel adapters only when the number of paths to Fibre Channel on the destination is the same or more than the number of paths on the source. These checks help prevent loss of data or interruption of I/O to the storage.* 