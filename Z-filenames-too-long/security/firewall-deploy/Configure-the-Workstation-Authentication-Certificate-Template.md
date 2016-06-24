---
title: Configure the Workstation Authentication Certificate Template
ms.custom: na
ms.prod: windows-server-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - techgroup-networking
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 94131a01-dc33-4f87-b31c-ee7c6c3a8548
---
# Configure the Workstation Authentication Certificate Template
This procedure describes how to configure a certificate template that Active Directory Certification Services (AD CS) uses as the starting point for computer certificates that are automatically enrolled and deployed to workstations in the domain. It shows how to create a copy of a template, and then configure the template according to your design requirements.

**Administrative credentials**

To complete these procedures, you must be a member of both the Domain Admins group in the root domain of your forest, and a member of the Enterprise Admins group.

### To configure the workstation authentication certificate template and autoenrollment

1.  On the computer where AD CS is installed, click the **Start** charm, and then click **Certification Authority**.

2.  In the navigation pane, right-click **Certificate Templates**, and then click **Manage**.

3.  In the details pane, click the **Workstation Authentication** template.

4.  On the **Action** menu, click **Duplicate Template**. In the **Duplicate Template** dialog box, select the template version that is appropriate for your deployment, and then click **OK**. For the resulting certificates to have maximum compatibility with the available versions of Windows, we recommended that you select **Windows Server 2003**.

5.  On the **General** tab, in **Template display name**, type a new name for the certificate template, such as **Domain Isolation Workstation Authentication Template**.

6.  Click the **Subject Name** tab. Make sure that **Build from this Active Directory information** is selected. In **Subject name format**, select **Fully distinguished name**.

7.  Click the **Request Handling** tab. You must determine the best minimum key size for your environment. Large key sizes provide better security, but they can affect server performance. We recommended that you use the default setting of 2048.

8.  Click the **Security** tab. In **Group or user names**, click **Domain Computers**, under **Allow**, select **Enroll** and **Autoenroll**, and then click **OK**.

    > [!NOTE]
    > If you want do not want to deploy the certificate to every computer in the domain, then specify a different group or groups that contain the computer accounts that you want to receive the certificate.

9. Close the Certificate Templates Console.

10. In the Certification Authority MMC snap-in, in the left pane, right-click **Certificate Templates**, click **New**, and then click **Certificate Template to Issue**.

11. In the **Enable Certificate Templates** dialog box, click the name of the certificate template you just configured, and then click **OK**.


