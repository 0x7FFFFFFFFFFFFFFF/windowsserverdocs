---
title: Install RDS client access licenses
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: df3f3d58-2ae6-4816-9c59-1821262b508b
author: lizap
ms.author: elizapo
ms.date: 09/20/2016
manager: dongill
---
# Install RDS client access licenses on the Remote Desktop license server

>Applies To: Windows Server 2016

Use the following information to install Remote Desktop Services client access licenses (CALs) on the license server. Once the CALs are installed, the license server will issue them to users as appropriate.

Note you need Internet connectivity on the computer running Remote Desktop Licensing Manager but not on the computer running the license server.

1. On the license server (usually the first RD Connection Broker), open the Remote Desktop Licensing Manager.
2. Right-click the license server, and then click **Install licenses**.
3. Click **Next** on the welcome page.
4. Select the program you purchased your RDS CALs from, and then click **Next**. If you are a service provider, select **Service Provider License Agreement**.
5. Enter the information for your license program. In most cases, this will be the license code or an agreement number, but this varies depending on the license program you're using.
6. Click **Next**.
7. Select the product version, license type, and number of licenses for your environment, and then click **Next**. The license manager contacts the Microsoft Clearinghouse to validate and retrieve your licenses.
8.  Click **Finish** to complete the process.