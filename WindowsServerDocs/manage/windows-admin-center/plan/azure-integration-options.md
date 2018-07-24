---
title: What Azure integration options are there
description: What Azure integration options are there Windows Admin Center (Project Honolulu)
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
---

# What Azure integration options are there with Windows Admin Center?

>Applies To: Windows Admin Center, Windows Admin Center Preview

Windows Admin center was built with the cloud in mind - that means Azure integration is built in to help you leverage Azure resources from your servers, whether they're on-premises or in the cloud. Although Windows Admin Center has no Azure dependencies or requirements and doesn't require internet connectivity for deployment, you can optionally add integration with the Azure services described below.

## Azure Active Directory authentication
You can add an additional layer of security to Windows Admin Center by requiring users to authenticate using [Azure Active Directory (Azure AD)](https://azure.microsoft.com/services/active-directory/) identities to access the gateway. Azure AD authentication also lets you take advantage of Azure AD’s security features like conditional access and multi-factor authentication.

[Learn how to configure Azure AD authentication for Windows Admin Center.](../configure/user-access-control.md#azure-active-directory)  

## Manage Azure IaaS virtual machines
You can use Windows Admin Center to manage your Azure VMs as well as on-premises machines. By configuring your Windows Admin Center gateway to have connectivity to your Azure VNet, you can manage virtual machines in Azure using the consistent, simplified tools Windows Admin Center provides.

[Learn how to configure Windows Admin Center to manage VMs in Azure.](../configure/azure-integration.md)


## Protect your Hyper-V virtual machines with Azure Site Recovery
[Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) is an Azure service that replicates workloads running on VMs so that your business-critical infrastructure is protected in case of a disaster. Windows Admin Center streamlines setup and the process of replicating your virtual machines on your Hyper-V servers or clusters, making it easy to bolster the resiliency of your environment with Azure Site Recovery’s disaster recovery service.

[Learn how to protect your virtual machines with Azure Site Recovery with Windows Admin Center.](../use/azure-services.md)