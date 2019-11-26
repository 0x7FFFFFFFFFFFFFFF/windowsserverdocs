---
title: Virtual machine recommendations for remote sessions
description: Maximum recommended user storage for each workload type.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: helohr
ms.date: 11/28/2019
ms.tgt_pltfrm: na
ms.topic: article
author: Heidilohr
manager: daveba
---
# Virtual machine recommendations for remote sessions

Whether you're running your virtual machine on Remote Desktop Services or Windows Virtual Desktop, different types of workloads require different virtual machine (VM) configurations. For the best possible experience, scale your deployment depending on your users' needs.

## Recommended specs

The following table lists the maximum suggested number of users per virtual central processing unit (vCPU) and the minimum VM configuration for each workload.

>[!NOTE]
>These recommendations apply to the multisession VDI scenario for the workloads defined in [Remote Desktop workloads](remote-desktop-workloads.md).

|Workload type|Maximum users per vCPU|vCPU/RAM/OS storage minimum|Example Azure instances|User storage minimum|
|---|---|---|---|---|
|Light|6|2 vCPUs, 8 GB RAM, 16 GB storage|D2s_v3, F2s_v2|30 GB|
|Medium|4|4 vCPUs, 16 GB RAM, 32 GB storage|D4s_v3, F4s_v2|30 GB|
|Heavy|2|4 vCPUs, 16 GB RAM, 32 GB storage|D4s_v3, F4s_v2|30 GB|
|Power|1|6 vCPUs, 56 GB RAM, 340 GB storage|D4s_v3, F4s_v2, NV4as_v4*|30 GB|

We recommend you use Premium SSD storage in your OS disk for production workloads that require a service level agreement (SLA). For more details, see the [SLA for virtual machines](https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_8/).

Graphics processing units (GPUs) are a good choice for users who regularly use graphics-intensive programs for video rendering, 3D design, and simulations. To learn more about graphics acceleration, see [Choose your graphics rendering technology](rds-graphics-virtualization.md). Azure has several graphics acceleration deployment options and multiple available GPU VM sizes. Learn more at [GPU optimized virtual machine sizes](https://docs.microsoft.com/azure/virtual-machines/windows/sizes-gpu).

Bs-Series burstable VMs are a good choice for users who don't always need maximum CPU performance. For more information about VM types and szes, see [Sizes for Windows virtual machines in Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sizes) and [our Virtual Machine series page](https://azure.microsoft.com/pricing/details/virtual-machines/series/).

## Test your workload

Finally, we recommend you use simulation tools to test your deployment with both stress tests and real-life usage simulations. Make sure your system is responsive and resilient enough to meet user needs, and remember to vary the load size to avoid surprises.