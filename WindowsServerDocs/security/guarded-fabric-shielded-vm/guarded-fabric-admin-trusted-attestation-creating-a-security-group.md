---
title: Admin-trusted attestation for a guarded fabric - creating a security group
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: a12c8494-388c-4523-8d70-df9400bbc2c0
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 10/14/2016
---

# Admin-trusted attestation for a guarded fabric - creating a security group

This topic describes the intermediate steps that a fabric administrator takes to prepare Hyper-V hosts to become guarded hosts using Admin-trusted attestation (AD mode). Before taking these steps, complete the steps in [Configuring the fabric DNS for hosts that will become guarded hosts](guarded-fabric-configuring-fabric-dns.md).

## Prerequisites for guarded hosts using Admin-trusted attestation

Hyper-V hosts must meet the following prerequisites for AD mode:

-   **Hardware**: Hosts only need hardware capable of running Hyper-V in Windows Server 2016. One host is required for initial deployment. To test Hyper-V live migration for shielded VMs, you must have at least two hosts.

-   **Operating system**: Windows Server 2016 Datacenter edition

   > [!IMPORTANT]
   > Install the [latest cumulative update](https://support.microsoft.com/help/4000825/windows-10-and-windows-server-2016-update-history).

-   **Role and features**: Hyper-V role and the Host Guardian Hyper-V Support feature, which is only available on Datacenter editions of Windows Server 2016. If you are using the Nano Server installation option, see [Appendix A - Configure Nano server as TPM attested guarded host](guarded-fabric-configure-nano-server-as-tpm-guarded-host.md). 

> [!WARNING]
> The Host Guardian Hyper-V Support feature enables Virtualization-based protection of code integrity that may be incompatible with some devices. 
> We strongly recommend testing this configuration in your lab before enabling this feature. 
> Failure to do so may result in unexpected failures up to and including data loss or a blue screen error (also called a stop error). 
> For more information, see [Compatible hardware with Windows Server 2016 Virtualization-based protection of Code Integrity](guarded-fabric-compatible-hardware-with-virtualization-based-protection-of-code-integrity.md).

## Create a security group and place hosts in the group

1. Create a new **GLOBAL** security group in the fabric domain and add Hyper-V hosts that will run shielded VMs. Restart the hosts to update their group membership.

2. Use Get-ADGroup to obtain the security identifier (SID) of the security group and provide it to the HGS administrator. 

    ```powershell
    Get-ADGroup "Guarded Hosts"
    ```

    ![Get-AdGroup command with output](../media/Guarded-Fabric-Shielded-VM/guarded-host-get-adgroup.png)

    The HGS administrator will [register the group with HGS as an Attestation Host Group](guarded-fabric-setting-up-the-host-guardian-service-hgs.md#admin-trusted-attestation-only---adding-security-group-information-to-the-hgs-configuration).

## Next step

[Confirm hosts can attest successfully](guarded-fabric-confirm-hosts-can-attest-successfully.md)

## See also

- [Deploying the Host Guardian Service for guarded hosts and shielded VMs](guarded-fabric-deploying-hgs-overview.md)
