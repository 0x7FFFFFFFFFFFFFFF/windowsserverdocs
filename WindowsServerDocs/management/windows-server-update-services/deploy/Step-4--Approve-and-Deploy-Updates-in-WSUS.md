---
title: Step 4 - Approve and Deploy Updates in WSUS
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.technology: manage-wsus
ms.topic: article
ms.assetid: 8d728ff9-170f-47e6-aefe-52be93315a75
author: coreyp
ms.author: coreyp-at-msft
ms.date: 09/14/2016
---
# Step 4: Approve and Deploy Updates in WSUS

>Applies To: Windows Server Technical Preview

Computers in a computer group automatically contact the WSUS server over the next 24 hours to obtain updates. You can use the WSUS reporting feature to determine whether those updates were deployed to the test computers. When the tests are successfully completed, you can approve the updates for the applicable computer groups in your organization. The following checklist describes the steps to approve and deploy updates by using WSUS management console.

|Task|Description|
|--------|---------------|
|[4.1. Approve and deploy WSUS updates](Step-4--Approve-and-Deploy-Updates-in-WSUS.md#BKM_4.1.)|Approve and deploy WSUS updates by using the WSUS Management Console.|
|[4.2. Configure auto-approval rules](Step-4--Approve-and-Deploy-Updates-in-WSUS.md#BKM_4.2.a.)|Configure WSUS to automatically approve installation of updates for selected groups, and how to approve revisions to existing updates.|
|[4.3. Review installed updates with WSUS Reports](Step-4--Approve-and-Deploy-Updates-in-WSUS.md#BKM_4.3.)|Review the updates that were installed, the computers that received those updates and other details by using the WSUS Reporting feature.|

## <a name="BKM_4.1."></a>4.1. Approve and deploy WSUS updates
Use the following procedure to approve and deploy updates.

#### To approve and deploy WSUS updates

1.  On the WSUS Administration Console, click **Updates**. In the right pane, an update status summary is displayed for **All Updates**, **Critical Updates**, **Security Updates**, and **WSUS Updates**.

2.  In the **All Updates** section, click **Updates needed by computers**.

3.  In the list of updates, select the updates that you want to approve for installation in your test computer group. Information about a selected update is available in the bottom pane of the **Updates** panel. To select multiple contiguous updates, hold down the **SHIFT** key while clicking the update names. To select multiple noncontiguous updates, press down the **CTRL** key while clicking the update names.

4.  Right-click the selection, and then click **Approve**.

5.  In the **Approve Updates** dialog box, select your test group, and then click the down arrow.

6.  Click **Approved for Install**, and then click **OK**.

7.  The **Approval Progress** window appears, which shows the progress of the tasks that affect update approval. When the approval process is complete, click **Close**.

## <a name="BKM_4.2.a."></a>4.2. Configure auto-approval rules
Automatic Approvals enables you to specify how to automatically approve installation of updates for selected groups, and how to approve revisions to existing updates.

#### To configure Automatic Approvals

1.  In the WSUS Administration Console, under **Update Services**, expand the WSUS server, and then click **Options**. The **Options** window opens.

2.  In **Options**, click **Automatic Approvals**. The Automatic Approvals dialog opens.

3.  In **Update Rules**, click **New Rule**. The **Add Rule** dialog opens.

4.  In **Add Rule**, in **Step 1: Select Properties**, select any single option, or combination of options from the following:

    -   **When an update is in a specific classification**

    -   **When an update is in a specific product**

    -   **Set a deadline for the approva**l

5.  In **Step 2: Edit the properties**, click each of the options listed, and then select the appropriate options for each.

6.  In  **Step 3: Specify a name**, type a name for your rule, and then click **OK**.

7.  Click **OK** to close the Automatic Approvals dialog.

## <a name="BKM_4.3."></a>4.3. Review installed updates with WSUS Reports
24 hours after you approve the updates, you can use the WSUS Reports feature to determine whether the updates were deployed to the test group computers. To check the status of an update, you can use the WSUS Reports feature as follows.

#### To review updates

1.  In the navigation pane of the WSUS Administration Console, click **Reports**.

2.  On the **Reports** page, click the **Update Status Summary** report. The **Updates Report** window appears.

3.  If you want to filter the list of updates, select the criteria that you want to use, for example, **Include updates in these classifications**, and then click **Run Report**.

4.  You will see the **Updates Report** pane. You can check the status of individual updates by selecting the update in the left section of the pane. The last section of the report pane shows the status summary of the update.

5.  You can save or print this report by clicking the applicable icon on the toolbar.

6.  After you test the updates, you can approve the updates for installation on the applicable computer groups in your organization.

## <a name="BKMK_Links"></a>See also

-   [Step 3: Configure WSUS](Step-3--Configure-WSUS.md)

-   [Deploy Windows Server Update Services](Deploy-Windows-Server-Update-Services.md)
