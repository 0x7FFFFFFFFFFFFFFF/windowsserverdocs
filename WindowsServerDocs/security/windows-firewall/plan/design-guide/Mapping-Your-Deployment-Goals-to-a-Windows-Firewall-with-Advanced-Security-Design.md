---
title: Mapping Your Deployment Goals to a Windows Firewall with Advanced Security Design
ms.custom: na
ms.prod: windows-server-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - techgroup-networking
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 855a7cad-2230-4c57-8903-e01acee69738
---
# Mapping Your Deployment Goals to a Windows Firewall with Advanced Security Design
After you finish reviewing the existing Windows Firewall with Advanced Security deployment goals and you determine which goals are important to your specific deployment, you can map those goals to a specific Windows Firewall with Advanced Security design.

> [!IMPORTANT]
> The first three designs presented in this guide build on each other to progress from simpler to more complex. Therefore during deployment, consider implementing them in the order presented. Each deployed design also provides a stable position from which to evaluate your progress, and to make sure that your goals are being met before you continue to the next design.

Use the following table to determine which Windows Firewall with Advanced Security design maps to the appropriate combination of Windows Firewall with Advanced Security deployment goals for your organization. This table refers only to the Windows Firewall with Advanced Security designs as described in this guide. However, you can create a hybrid or custom Windows Firewall with Advanced Security design by using any combination of the Windows Firewall with Advanced Security deployment goals to meet the needs of your organization.

|Deployment Goals|[Basic Firewall Policy Design](Basic-Firewall-Policy-Design.md)|[Domain Isolation Policy Design](Domain-Isolation-Policy-Design.md)|[Server Isolation Policy Design](Server-Isolation-Policy-Design.md)|[Certificate-based Isolation Policy Design](Certificate-based-Isolation-Policy-Design.md)|
|--------------------|--------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------|
|[Protect Computers from Unwanted Network Traffic](Protect-Computers-from-Unwanted-Network-Traffic.md)|Yes|Yes|Yes|Yes|
|[Restrict Access to Only Trusted Computers](Restrict-Access-to-Only-Trusted-Computers.md)|\-|Yes|Yes|Yes|
|[Restrict Access to Only Specified Users or Computers](Restrict-Access-to-Only-Specified-Users-or-Computers.md)|\-|\-|Yes|Yes|
|[Require Encryption When Accessing Sensitive Network Resources](Require-Encryption-When-Accessing-Sensitive-Network-Resources.md)|\-|Optional|Optional|Optional|

To examine details for a specific design, click the design title at the top of the column in the preceding table.

**Next:**[Basic Firewall Policy Design](Basic-Firewall-Policy-Design.md)


