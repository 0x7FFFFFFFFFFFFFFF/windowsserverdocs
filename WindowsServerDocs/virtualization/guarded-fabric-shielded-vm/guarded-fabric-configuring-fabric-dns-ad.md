---
title: Configure the fabric DNS for guarded hosts (AD)
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 074b6d09-f16e-49bf-b88a-377139d35067
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/24/2018
---

>[!div class="step-by-step"]
[« Initialize HGS](guarded-fabric-initialize-hgs-ad-mode.md)
[Configure HGS DNS and a one-way trust »](guarded-fabric-configure-dns-forwarding-and-trust.md)

>[!IMPORTANT]
>AD mode is deprecated beginning with Windows Server 2019. For environments where TPM attestation is not possible, configure [host key attestation](guarded-fabric-initialize-hgs-key-mode.md). Host key attestation provides similar assurance to AD mode and is simpler to set up. 


[!INCLUDE [Configure fabric DNS](../../../includes/guarded-fabric-configure-fabric-dns.md)] 


## See also

- [Configuration steps for Hyper-V hosts that will become guarded hosts](guarded-fabric-configure-hgs-with-authorized-hyper-v-hosts.md)
- [Deployment tasks for guarded fabrics and shielded VMs](guarded-fabric-deploying-hgs-overview.md#deployment-tasks-for-guarded-fabrics-and-shielded-vms)
