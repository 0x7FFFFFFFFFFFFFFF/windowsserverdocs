---
title: Create a Group Account in Active Directory
ms.custom: na
ms.prod: windows-server-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - techgroup-networking
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3d592a3f-eda7-4b11-a12b-0b888a75d163
author: vhorne
---
# Create a Group Account in Active Directory
To create a security group to contain the computer accounts for the computers that are to receive a set of Group Policy settings, use the Active Directory Users and Computers MMC snap\-in.  
  
**Administrative credentials**  
  
To complete this procedure, you must be a member of the Domain Administrators group, or otherwise be delegated permissions to create new group accounts.  
  
### To add a new membership group in Active Directory  
  
1.  On a computer that has Active Directory management tools installed, click the **Start** charm, and then click the **Active Directory Users and Computers** tile.  
  
2.  In the navigation pane, select the container in which you want to store your group. This is typically the **Users** container under the domain.  
  
3.  Click **Action**, click **New**, and then click **Group**.  
  
4.  In the **Group name** text box, type the name for your new group.  
  
    > [!NOTE]  
    > Be sure to use a name that clearly indicates its purpose. Check to see if your organization has a naming convention for groups.  
  
5.  In the **Description** text box, enter a description of the purpose of this group.  
  
6.  In the **Group scope** section, select either **Global** or **Universal**, depending on your Active Directory forest structure. If your group must include computers from multiple domains, then select **Universal**. If all of the members are from the same domain, then select **Global**.  
  
7.  In the **Group type** section, click **Security**.  
  
8.  Click **OK** to save your group.  
  
