---
title: Test failover should be attempted after initial replication is complete
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - hyper-v
  - techgroup-compute
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cea7eeaa-c1a7-4f87-89be-d4e1208c546f
author: KBDAzure
---
# Test failover should be attempted after initial replication is complete
\[This information is preliminary and subject to change.\]  
  
For more information about best practices and scans, see [Run Best Practices Analyzer Scans and Manage Scan Results](http://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|||  
|-|-|  
|**Operating System**|Windows Server 2016 Technical Preview|  
|**Product\/Feature**|Hyper\-V|  
|**Severity**|Warning|  
|**Category**|Operations|  
  
In the following sections, italics indicates UI text that appears in the Best Practices Analyzer tool for this issue.  
  
## Problem  
*There has been no test failover in at least one month.*  
  
## Impact  
*There is no confirmation that a planned or unplanned failover will succeed or workload operations will continue properly after a failover. This impacts the following virtual machines:*  
  
\<list of virtual machines>  
  
## Resolution  
*Use Hyper\-V Manager to conduct a test failover.*  
  

