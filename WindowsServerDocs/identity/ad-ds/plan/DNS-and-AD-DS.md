---
title: DNS and AD DS
description:
author: billmath
ms.author: billmath
manager: femila
ms.date: 09/29/2016
ms.topic: article
ms.prod: windows-server-threshold
ms.service: active-directory
ms.technology: identity-adds
---

# DNS and AD DS

>Applies To: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active Directory Domain Services (AD DS) uses Domain Name System (DNS) name resolution services to make it possible for clients to locate domain controllers and for the domain controllers that host the directory service to communicate with each other.  
  
AD DS enables easy integration of the Active Directory namespace into an existing DNS namespace. Features such as Active Directory-integrated DNS zones make it easier for you to deploy DNS by eliminating the need to set up secondary zones, and then configure zone transfers.  
  
For information about how DNS supports AD DS, see the DNS Support for Active Directory Technical Reference ([http://go.microsoft.com/fwlink/?LinkID=48147](http://go.microsoft.com/fwlink/?LinkID=48147)).  
  
> [!NOTE]  
> If you implement a disjoint namespace in which the AD DS domain name differs from the primary DNS suffix that clients use, AD DS integration with DNS is more complex. For more information, see [Disjoint Namespace](../../ad-ds/plan/../../ad-ds/plan/Disjoint-Namespace.md).  
  
## In this section  
  
-   [Domain Controller Location](../../ad-ds/plan/Domain-Controller-Location.md)  
  
-   [Active Directory-Integrated DNS Zones](../../ad-ds/plan/Active-Directory-Integrated-DNS-Zones.md)  
  
-   [Computer Naming](../../ad-ds/plan/Computer-Naming.md)  
  
-   [Disjoint Namespace](../../ad-ds/plan/../../ad-ds/plan/Disjoint-Namespace.md)  
  


