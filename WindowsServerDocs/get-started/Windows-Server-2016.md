---
title: Windows Server 2016
description: "Get started with Windows Server 2016. "
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.date: 11/02/2016
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d8972680-d5ee-430e-a97a-991ac872b0d6
author: jaimeo
ms.author: jaimeo
manager: dongill
---

# Windows Server 2016

<img src="https://i-technet.sec.s-msft.com/en-us/windows-server-docs/get-started/2whats-new.png" alt="alt text" title="What's newer  in Windows Server 2016?" />
    <font size="5">
    &nbsp;<a href="what-s-new-in-windows-server-2016">Read what's new in Windows Server 2016</a></font>
<br/><br/>
[![Storage Spaces Direct Overview Video](media/front-page-video.png)](https://www.youtube.com/embed/V8oF0JpDzaM)

<table border="0" width="100%">
</tr>
  <tr style="text-align:center;">
    <td style="width:25%; border:0;">
      <a href="https://technet.microsoft.com/windows-server-docs/get-started/server-basics">
        <img height=145 src="https://i-technet.sec.s-msft.com/en-us/windows-server-docs/get-started/media/1-getstarted.png" alt="alt text" title="Get started" />
      </a>
    </td>
    <td style="width:25%; border:0;">
      <a href="https://technet.microsoft.com/windows-server-docs/compute/compute">
        <img height=145 src="https://i-technet.sec.s-msft.com/en-us/windows-server-docs/get-started/media/2-compute.png" alt="alt text" title="Windows Server Compute" />
      </a>
    </td>
    <td style="width:25%; border:0;">
      <a href="https://technet.microsoft.com/windows-server-docs/failover-clustering/failover-clustering-overview">
        <img height=145 src="https://i-technet.sec.s-msft.com/en-us/windows-server-docs/get-started/media/3-failover.png" alt="Failover clustering" title="Failover clustering" />
      </a>
    </td>
    <td style="width:25%; border:0;">
      <a href="https://technet.microsoft.com/windows-server-docs/identity/identity-and-access">
        <img height=145 src="https://i-technet.sec.s-msft.com/en-us/windows-server-docs/get-started/media/4-identity.png" alt="alt text" title="Windows Server Identity and Access" />
      </a>
    </td>
  </tr>
  <tr style="text-align:center;">
    <td style="width:25%; border:0;">
      <a href="https://technet.microsoft.com/windows-server-docs/security/security-and-assurance">
        <img height=145 src="https://i-technet.sec.s-msft.com/en-us/windows-server-docs/get-started/media/5-security.png" alt="alt text" title="Windows Server Security and Assurance" />
      </a>
    </td>
    <td style="width:25%; border:0;">
      <a href="https://technet.microsoft.com/windows-server-docs/networking/networking">
        <img height=145 src="https://i-technet.sec.s-msft.com/en-us/windows-server-docs/get-started/media/6-networking.png" alt="alt text" title="Windows Server Networking" />
      </a>
    </td>
    <td style="width:25%; border:0;">
      <a href="https://technet.microsoft.com/en-us/windows-server-docs/storage/storage">
        <img height=145 src="https://i-technet.sec.s-msft.com/en-us/windows-server-docs/get-started/media/7-storage.png" alt="alt text" title="Windows Server Storage" />
      </a>
    </td>
    <td style="width:25%; border:0;">
      <a href="https://technet.microsoft.com/windows-server-docs/management/management-and-automation">
        <img height=145 src="https://i-technet.sec.s-msft.com/en-us/windows-server-docs/get-started/media/8-management.png" alt="alt text" title="Windows Server Management and Automation" />
      </a>
    </td>
  </tr>
</table>

> [!Note]  
> To experience first-hand new features and functionality available in Windows Server 2016, you can download an evaluation version by visiting [Windows Server Evaluations](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016?i=1).  
>   

## Windows Server 2016 editions

Windows Server 2016 is available in Standard, Datacenter, and Essentials editions. Windows Server 2016 Datacenter includes unlimited virtualization rights plus new features to build a software-defined datacenter. Windows Server 2016 Standard offers enterprise-class features with limited virtualization rights. Windows Server Essentials is an ideal cloud-connected first server. It has its own [extensive documentation](http://go.microsoft.com/fwlink/?LinkID=827171)—the content here focuses on Standard and Datacenter editions. The following table briefly summarizes the key differences between Standard and Datacenter editions:

|Feature|Datacenter|Standard|  
|-------------------|----------|-----------------------|  
|Core functionality of Windows Server| yes| yes|
|OSEs / Hyper-V containers|unlimited|	2|
|Windows Server containers|unlimited|	unlimited|
|Host Guardian Service| yes| yes|
|Nano Server installation option| yes| yes|
|Storage features including Storage Spaces Direct and Storage Replica| yes| no|
|Shielded Virtual Machines| yes| no|
|Software Defined Networking Infrastructure (Network Controller, Software Load Balancer, and Multi-tenant Gateway)| yes| no|

For more information, see [Pricing and licensing for Windows Server 2016](https://www.microsoft.com/en-us/cloud-platform/windows-server-pricing) and [Compare features in Windows Server versions](https://www.microsoft.com/en-us/cloud-platform/windows-server-comparison).

## Installation options

Both Standard and Datacenter editions offer three installation options:

- **Server Core:** reduces the space required on disk, the potential attack surface, and especially the servicing requirements. This is the **recommended** option unless you have a particular need for additional user interface elements and graphical management tools.
- **Server with Desktop Experience:** installs the standard user interface and all tools, including client experience features that required a separate installation in Windows Server 2012 R2. Server roles and features are installed with Server Manager or by other methods.
- **Nano Server:** is a remotely administered server operating system optimized for private clouds and datacenters. It is similar to Windows Server in Server Core mode, but significantly smaller, has no local logon capability, and only supports 64-bit applications, tools, and agents. It takes up far less disk space, sets up significantly faster, and requires far fewer updates and restarts than the other options.


Now that you know which edition and installation option is right for you, click below to get started with Windows Server 2016.


<table border=0 width="100%">
  <tr style='text-align:center;'>
    <td style='width:34%'><a href="https://technet.microsoft.com/en-us/windows-server-docs/get-started/getting-started-with-nano-server">![Nano](media/nano.png)</a></td>
    <td style='width:33%'><a href="https://technet.microsoft.com/en-us/windows-server-docs/get-started/getting-started-with-server-core">![Server core](media/servercore.png)</a></td>
    <td style='width:33%'><a href="https://technet.microsoft.com/en-us/windows-server-docs/get-started/getting-started-with-server-with-desktop-experience">![Desktop](media/desktop.png)</a></td>
  </tr>
</table>


> [!Note]  
> To experience first-hand new features and functionality available in Windows Server 2016, you can download an evaluation version by visiting [Windows Server Evaluations](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016?i=1).  
>   

## Windows Server 2016 editions

Windows Server 2016 is available in Standard, Datacenter, and Essentials editions. Windows Server 2016 Datacenter includes unlimited virtualization rights plus new features to build a software-defined datacenter. Windows Server 2016 Standard offers enterprise-class features with limited virtualization rights. Windows Server Essentials is an ideal cloud-connected first server. It has its own [extensive documentation](http://go.microsoft.com/fwlink/?LinkID=827171)—the content here focuses on Standard and Datacenter editions. The following table briefly summarizes the key differences between Standard and Datacenter editions:

|Feature|Datacenter|Standard|  
|-------------------|----------|-----------------------|  
|Core functionality of Windows Server| yes| yes|
|OSEs / Hyper-V containers|unlimited|	2|
|Windows Server containers|unlimited|	unlimited|
|Host Guardian Service| yes| yes|
|Nano Server installation option| yes| yes|
|Storage features including Storage Spaces Direct and Storage Replica| yes| no|
|Shielded Virtual Machines| yes| no|
|Software Defined Networking Infrastructure (Network Controller, Software Load Balancer, and Multi-tenant Gateway)| yes| no|

For more information, see [Pricing and licensing for Windows Server 2016](https://www.microsoft.com/en-us/cloud-platform/windows-server-pricing) and [Compare features in Windows Server versions](https://www.microsoft.com/en-us/cloud-platform/windows-server-comparison).

## Installation options

Both Standard and Datacenter editions offer three installation options:

- **Server Core:** reduces the space required on disk, the potential attack surface, and especially the servicing requirements. This is the **recommended** option unless you have a particular need for additional user interface elements and graphical management tools.
- **Server with Desktop Experience:** installs the standard user interface and all tools, including client experience features that required a separate installation in Windows Server 2012 R2. Server roles and features are installed with Server Manager or by other methods.
- **Nano Server:** is a remotely administered server operating system optimized for private clouds and datacenters. It is similar to Windows Server in Server Core mode, but significantly smaller, has no local logon capability, and only supports 64-bit applications, tools, and agents. It takes up far less disk space, sets up significantly faster, and requires far fewer updates and restarts than the other options.


Now that you know which edition and installation option is right for you, click below to get started with Windows Server 2016.


<table border=0 width="100%">
  <tr style='text-align:center;'>
    <td style='width:34%'><a href="https://technet.microsoft.com/en-us/windows-server-docs/get-started/getting-started-with-nano-server">![Nano](nano.png)</a></td>
    <td style='width:33%'><a href="https://technet.microsoft.com/en-us/windows-server-docs/get-started/getting-started-with-server-core">![Server core](servercore.png)</a></td>
    <td style='width:33%'><a href="https://technet.microsoft.com/en-us/windows-server-docs/get-started/getting-started-with-server-with-desktop-experience">![Desktop](desktop.png)</a></td>
  </tr>
</table>
