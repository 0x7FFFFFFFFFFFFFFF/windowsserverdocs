---
title: Add the RD Connection Broker server to the deployment and configure high availability
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6581da74-f36a-48b6-a33c-97d02285389d
author: lizap
---
# Add the RD Connection Broker server to the deployment and configure high availability
1. Connect to the RDMS server virtual machine. (The RDMS virtual machine will typically be the virtual machine running the first instance of the RD Connection Broker role.)   
    1.	In the Azure portal click **Browse > Virtual Machines**.  
    2.	Select the new RDSH virtual machine (for example, Contoso-RDSH1).  
    3.	Click **Connect > Open**.  
    4.	Click **Connect**, and then click **Use another user account**. Enter the user name and password for the local administrator account.  
    5.	Click **Yes** when warned about the certificate.  
  
2. Add the new RD Connection Broker server to Server Manager:   
  
    1. In Server Manager, click **Manage > Add Servers**.   
    2. Click **DNS**.   
    3. Search for and select the newly created RD Connection Broker server, e.g. Contoso-CB2.   
    4. Click **OK**.   
  
3. Configure high availability for the RD Connection Broker:   
  
    1. In Server Manager, click **Remote Desktop Services > Overview**.   
  
    2. Right-click **RD Connection Broker**, and then click **Configure High Availability**.   
  
    3. Page through the wizard until you get to the Configuration type section. Select **Shared database server**, and then click **Next**.   
  
    4. Enter the DNS name for the RD Connection Broker cluster, which is the DNS entry we just created (for example, CBLB.Contoso.com).   
  
    5. Enter the connection string for the Azure SQL DB, and then page through the wizard to establish high availability.  
  
4. Add the new RD Connection Broker to the deployment   
  
    1. In Server Manager, click **Remote Desktop Services > Overview**.   
  
    2. Right-click the RD Connection Broker, and then click **Add RD Connection Broker Server**.   
  
    3. Page through wizard until you get to Server Selection, then select the newly created RD Connection Broker server (for example, Contoso-CB2).  
    4. Complete the wizard, accepting the default values.   
