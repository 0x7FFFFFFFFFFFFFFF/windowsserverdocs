---
title: Add Test Computers to the Membership Group for a Zone
ms.custom: na
ms.prod: windows-server-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - techgroup-networking
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 762001b1-069c-4f79-927a-e1b0f633f245
---
# Add Test Computers to the Membership Group for a Zone
Before you deploy your rules to large numbers of computers, you must thoroughly test the rules to make sure that communications are working as expected. A misplaced WMI filter or an incorrectly typed IP address in a filter list can easily block communications between computers. Although we recommend that you set your rules to request mode until testing and deployment is complete, we also recommend that you initially deploy the rules to a small number of computers only to be sure that the correct GPOs are being processed by each computer.

Add at least one computer of each supported operating system type to each membership group. Make sure every GPO for a specific version of Windows and membership group has a computer among the test group. After Group Policy has been refreshed on each test computer, check the output of the **gpresult** command to confirm that each computer is receiving only the GPOs it is supposed to receive.

**Administrative credentials**

To complete these procedures, you must be a member of the Domain Administrators group, or otherwise be delegated permissions to modify the membership of the group for the GPO.

In this topic:

-   [Add the test computers to the GPO membership groups](#bkmk_ToaddDomainComputerstotheGPOmembershipgroup)

-   [Refresh Group Policy on the computers in each membership group](#bkmk_TorefreshGroupPolicyonacomputer)

-   [Check which GPOs apply to a computer](#bkmk_ToseewhatGPOsareappliedtoacomputer)

## <a name="bkmk_ToaddDomainComputerstotheGPOmembershipgroup"></a>
#### To add test computers to the GPO membership groups

1.  On a computer that has the Active Directory management tools installed, click the **Start** charm, then click the **Active Directory Users and Computers** tile.

2.  In the navigation pane, expand **Active Directory Users and Computers**, expand *YourDomainName*, and then expand the container that holds your membership group account.

3.  In the details pane, double-click the GPO membership group to which you want to add computers.

4.  Select the **Members** tab, and then click **Add**.

5.  Type the name of the computer in the text box, and then click **OK**.

6.  Repeat steps 5 and 6 for each additional computer account or group that you want to add.

7.  Click **OK** to close the group properties dialog box.

After a computer is a member of the group, you can force a Group Policy refresh on the computer.

## <a name="bkmk_TorefreshGroupPolicyonacomputer"></a>
#### To refresh Group Policy on a computer

-   For a computer that is running Windows 8,  Windows 7 , Windows Vista,  Windows Server 2012 ,  Windows Server 2008 , or  Windows Server 2008 R2 , [Start a Command Prompt as an Administrator](Start-a-Command-Prompt-as-an-Administrator.md), and then type the following command:

    ```
    gpupdate /target:computer /force
    ```

After Group Policy is refreshed, you can see which GPOs are currently applied to the computer.

## <a name="bkmk_ToseewhatGPOsareappliedtoacomputer"></a>
#### To see which GPOs are applied to a computer

-   For a computer that is running Windows 8,  Windows 7 , Windows Vista,  Windows Server 2012 ,  Windows Server 2008 , or  Windows Server 2008 R2 , [Start a Command Prompt as an Administrator](Start-a-Command-Prompt-as-an-Administrator.md), and then type the following command:

    ```
    gpresult /r /scope:computer
    ```


