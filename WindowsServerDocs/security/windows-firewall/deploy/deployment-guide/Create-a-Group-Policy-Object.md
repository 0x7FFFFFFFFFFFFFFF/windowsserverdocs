---
title: Create a Group Policy Object
ms.custom: na
ms.prod: windows-server-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - techgroup-networking
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9bf1ed44-8ff4-48a0-ac9e-2ace722376a3
---
# Create a Group Policy Object
To create a new GPO, use the Active Directory Users and Computers MMC snap\-in.

**Administrative credentials**

To complete this procedure, you must be a member of the Domain Administrators group, or otherwise be delegated permissions to create new GPOs.

### To create a new GPO

1.  On a computer that has the Group Policy Management feature installed, click the **Start** charm, and then click the **Group Policy Management** tile.

2.  In the navigation pane, expand **Forest:***YourForestName*, expand **Domains**, expand *YourDomainName*, and then click **Group Policy Objects**.

3.  Click **Action**, and then click **New**.

4.  In the **Name** text box, type the name for your new GPO.

    > [!NOTE]
    > Be sure to use a name that clearly indicates the purpose of the GPO. Check to see if your organization has a naming convention for GPOs.

5.  Leave **Source Starter GPO** set to **\(none\)**, and then click **OK**.

6.  If your GPO will not contain any user settings, then you can improve performance by disabling the **User Configuration** section of the GPO. To do this, perform these steps:

    1.  In the navigation pane, click the new GPO.

    2.  In the details pane, click the **Details** tab.

    3.  Change the **GPO Status** to **User configuration settings disabled**.

If you arrived at this page by clicking a link in a checklist, use your browser’s **Back** button to return to the checklist.


