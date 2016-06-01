---
title: Add Production Computers to the Membership Group for a Zone
ms.custom: na
ms.prod: windows-server-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - techgroup-networking
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 74f9c4a5-e339-4994-bd94-c3f19a7aa280
---
# Add Production Computers to the Membership Group for a Zone
After you test the GPOs for your design on a small set of computers, you can deploy them to the production computers.

> [!CAUTION]
> For GPOs that contain connection security rules that prevent unauthenticated connections, be sure to set the rules to request, not require, authentication during testing. After you deploy the GPO and confirm that all of your computers are successfully communicating by using authenticated IPsec, then you can modify the GPO to require authentication. Do not change the boundary zone GPO to require mode.

The method discussed in this guide uses the **Domain Computers** built\-in group. The advantage of this method is that all new computers that are joined to the domain automatically receive the isolated domain GPO. To do this successfully, you must make sure that the WMI filters and security group filters exclude computers that must not receive the GPOs. Use computer groups that deny both read and apply Group Policy permissions to the GPOs, such as a group used in the CG\_DOMISO\_NOIPSEC example design. Computers that are members of some zones must also be excluded from applying the GPOs for the main isolated domain. For more information, see the "Prevent members of a group from applying a GPO" section in [Assign Security Group Filters to the GPO](Assign-Security-Group-Filters-to-the-GPO.md).

Without such a group \(or groups\), you must either add computers individually or use the groups containing computer accounts that are available to you.

**Administrative credentials**

To complete these procedures, you must be a member of the Domain Administrators group, or otherwise be delegated permissions to modify the membership of the group for the GPO.

In this topic:

-   [Add the group Domain Computers to the GPO membership group](#bkmk_ToaddDomainComputerstotheGPOmembershipgroup)

-   [Refresh Group Policy on the computers in the membership group](#bkmk_TorefreshGroupPolicyonacomputer)

-   [Check which GPOs apply to a computer](#bkmk_ToseewhatGPOsareappliedtoacomputer)

## <a name="bkmk_ToaddDomainComputerstotheGPOmembershipgroup"></a>
#### To add domain computers to the GPO membership group

1.  On a computer that has the Active Directory management tools installed, click the **Start** charm, then click the **Active Directory Users and Computers** tile.

2.  In the navigation pane, expand **Active Directory Users and Computers**, expand *YourDomainName*, and then the container in which you created the membership group.

3.  In the details pane, double\-click the GPO membership group to which you want to add computers.

4.  Select the **Members** tab, and then click **Add**.

5.  Type **Domain Computers** in the text box, and then click **OK**.

6.  Click **OK** to close the group properties dialog box.

After a computer is a member of the group, you can force a Group Policy refresh on the computer.

## <a name="bkmk_TorefreshGroupPolicyonacomputer"></a>
#### To refresh Group Policy on a computer

-   For a computer that is running [!INCLUDE[win8_client_2](includes/win8_client_2_md.md)], [!INCLUDE[nextref_client_7](includes/nextref_client_7_md.md)], [!INCLUDE[nextref_vista](includes/nextref_vista_md.md)], [!INCLUDE[win8_server_2](includes/win8_server_2_md.md)], [!INCLUDE[nextref_longhorn](includes/nextref_longhorn_md.md)], or [!INCLUDE[nextref_server_7](includes/nextref_server_7_md.md)], [Start a Command Prompt as an Administrator](Start-a-Command-Prompt-as-an-Administrator.md), and then type the following command:

    ```
    gpupdate /target:computer /force
    ```

After Group Policy is refreshed, you can see which GPOs are currently applied to the computer.

## <a name="bkmk_ToseewhatGPOsareappliedtoacomputer"></a>
#### To see which GPOs are applied to a computer

-   For a computer that is running [!INCLUDE[win8_client_2](includes/win8_client_2_md.md)], [!INCLUDE[nextref_client_7](includes/nextref_client_7_md.md)], [!INCLUDE[nextref_vista](includes/nextref_vista_md.md)], [!INCLUDE[win8_server_2](includes/win8_server_2_md.md)], [!INCLUDE[nextref_longhorn](includes/nextref_longhorn_md.md)], or [!INCLUDE[nextref_server_7](includes/nextref_server_7_md.md)], [Start a Command Prompt as an Administrator](Start-a-Command-Prompt-as-an-Administrator.md), and then type the following command:

    ```
    gpresult /r /scope:computer
    ```


