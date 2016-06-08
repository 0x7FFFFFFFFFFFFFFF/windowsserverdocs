---
title: Assign Security Group Filters to the GPO
ms.custom: na
ms.prod: windows-server-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - techgroup-networking
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6f364586-8839-4ac9-b90a-1e25255ce12c
---
# Assign Security Group Filters to the GPO
To make sure that your GPO is applied to the correct computers, use the Group Policy Management MMC snap\-in to assign security group filters to the GPO.

> [!IMPORTANT]
> This deployment guide uses the method of adding the Domain Computers group to the membership group for the main isolated domain after testing is complete and you are ready to go live in production. To make this method work, you must prevent any computer that is a member of either the boundary or encryption zone from applying the GPO for the main isolated domain. For example, on the GPOs for the main isolated domain, deny Read and Apply Group Policy permissions to the membership groups for the boundary and encryption zones.

**Administrative credentials**

To complete these procedures, you must be a member of the Domain Administrators group, or otherwise be delegated permissions to modify the relevant GPOs.

In this topic:

-   [Allow members of a group to apply a GPO](#bkmk_ToallowamembersofagrouptoapplyaGPO)

-   [Prevent members of a group from applying a GPO](#bkmk_TopreventmembersofgroupfromapplyingaGPO)

## <a name="bkmk_ToallowamembersofagrouptoapplyaGPO"></a>Use the following procedure to add a group to the security filter on the GPO that allows group members to apply the GPO.

#### To allow members of a group to apply a GPO

1.  On a computer that has the Group Policy Management feature installed, click the **Start** charm, and then click the **Group Policy Management** tile.

2.  In the navigation pane, find and then click the GPO that you want to modify.

3.  In the details pane, under **Security Filtering**, click **Authenticated Users**, and then click **Remove**.

    > [!NOTE]
    > You must remove the default permission granted to all authenticated users and computers to restrict the GPO to only the groups you specify.

4.  Click **Add**.

5.  In the **Select User, Computer, or Group** dialog box, type the name of the group whose members are to apply the GPO, and then click **OK**. If you do not know the name, you can click **Advanced** to browse the list of groups available in the domain.

## <a name="bkmk_TopreventmembersofgroupfromapplyingaGPO"></a>Use the following procedure to add a group to the security filter on the GPO that prevents group members from applying the GPO. This is typically used to prevent members of the boundary and encryption zones from applying the GPOs for the isolated domain.

#### To prevent members of group from applying a GPO

1.  On a computer that has the Group Policy Management feature installed, click the **Start** charm, and then click the **Group Policy Management** tile.

2.  In the navigation pane, find and then click the GPO that you want to modify.

3.  In the details pane, click the **Delegation** tab.

4.  Click **Advanced**.

5.  Under the **Group or user names** list, click **Add**.

6.  In the **Select User, Computer, or Group** dialog box, type the name of the group whose members are to be prevented from applying the GPO, and then click **OK**. If you do not know the name, you can click **Advanced** to browse the list of groups available in the domain.

7.  Select the group in the **Group or user names** list, and then select the box in the **Deny** column for both **Read** and **Apply group policy**.

8.  Click **OK**, and then in the **Windows Security** dialog box, click **Yes**.

9. The group appears in the list with **Custom** permissions.

If you arrived at this page by clicking a link in a checklist, use your browser’s **Back** button to return to the checklist.


