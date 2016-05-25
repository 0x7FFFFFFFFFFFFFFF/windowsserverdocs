---
title: Deploy Primary Computers for Folder Redirection and Roaming User Profiles
ms.custom: na
ms.prod: windows-server-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - techgroup-storage
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1f0aea30-ea0f-4a58-88f9-4e72e3c0b96c
author: JasonGerend
---
# Deploy Primary Computers for Folder Redirection and Roaming User Profiles
This topic describes how to enable primary computer support and designate primary computers for users. Doing so enables you to control which computers use Folder Redirection and Roaming User Profiles.  
  
> [!IMPORTANT]  
> When enabling primary computer support for Roaming User Profiles, always enable primary computer support for Folder Redirection as well. This keeps documents and other user files out of the user profiles, which helps profiles remain small and sign on times stay fast.  
  
**In this document**  
  
-   [Prerequisites](#PrimaryComputer_Prerequisites)  
  
-   [Step 1: Designate primary computers for users](#PrimaryComputer_Step1Designateprimarycomputersforusers)  
  
-   [Step 2: Optionally enable primary computers for Folder Redirection in Group Policy](#PrimaryComputer_Step2OptionallyenableprimarycomputersforFolderRedirectioninGro)  
  
-   [Step 3: Optionally enable primary computers for Roaming User Profiles in Group Policy](#PrimaryComputer_Step3OptionallyenableprimarycomputersforRoamingUserProfilesinG)  
  
-   [Step 4: Enable the GPO](#PrimaryComputer_Step4EnabletheGPO)  
  
-   [Step 5: Test primary computer function](#PrimaryComputer_Step5Testprimarycomputerfunction)  
  
## <a name="PrimaryComputer_Prerequisites"></a>Prerequisites  
  
### Software requirements  
Primary computer support has the following requirements:  
  
-   The Active Directory Domain Services \(AD DS\) schema must be updated to include [!INCLUDE[win8_server_2](../Token/win8_server_2_md.md)] schema additions \(installing a [!INCLUDE[win8_server_2](../Token/win8_server_2_md.md)] domain controller automatically updates the schema\). For information about updating the AD DS schema, see [What’s new for Adprep.exe?](http://technet.microsoft.com/library/a0c7e030-27e5-4d58-bc11-e2d180a3ffb2) and [Running Adprep.exe](http://technet.microsoft.com/library/dd464018.aspx).  
  
-   Client computers must run [!INCLUDE[winblue_client_2](../Token/winblue_client_2_md.md)], [!INCLUDE[win8_client_2](../Token/win8_client_2_md.md)], [!INCLUDE[winblue_server_2](../Token/winblue_server_2_md.md)], or [!INCLUDE[win8_server_2](../Token/win8_server_2_md.md)].  
  
> [!TIP]  
> Although primary computer support requires Folder Redirection and\/or Roaming User Profiles, if you are deploying these technologies for the first time, it is best to set up primary computer support before enabling the GPOs that configure Folder Redirection and Roaming User Profiles. This prevents user data from being copied to non\-primary computers before primary computer support is enabled. For configuration information, see [Deploy Folder Redirection, Offline Files, and Roaming User Profiles](../Topic/Deploy-Folder-Redirection,-Offline-Files,-and-Roaming-User-Profiles.md) and [Deploy Roaming User Profiles](../Topic/Deploy-Roaming-User-Profiles.md).  
  
## <a name="PrimaryComputer_Step1Designateprimarycomputersforusers"></a>Step 1: Designate primary computers for users  
The first step in deploying primary computers support is designating the primary computers for each user. To do so, use Active Directory Administration Center to obtain the distinguished name of the relevant computers and then set the **msDs\-PrimaryComputer** attribute.  
  
> [!TIP]  
> To use Windows PowerShell to work with primary computers, see the blog post [Digging a little deeper into Windows 8 Primary Computer](http://blogs.technet.com/b/askds/archive/2012/10/23/digging-a-little-deeper-into-windows-8-primary-computer.aspx).  
  
#### To specify the primary computers for users  
  
1.  Open Server Manager on a computer with Active Directory Administration Tools installed.  
  
2.  On the **Tools** menu, click **Active Directory Administration Center**. Active Directory Administration Center appears.  
  
3.  Navigate to the **Computers** container in the appropriate domain.  
  
4.  Right\-click a computer that you want to designate as a primary computer and then click **Properties**.  
  
5.  In the Navigation pane, click **Extensions**.  
  
6.  Click the **Attribute Editor** tab, scroll to **distinguishedName**, click **View**, right\-click the value listed, click **Copy**, click **OK**, and then click **Cancel**.  
  
7.  Navigate to the **Users** container in the appropriate domain, right\-click the user to which you want to assign the computer, and then click **Properties**.  
  
8.  In the Navigation pane, click **Extensions**.  
  
9. Click the **Attribute Editor** tab, select **msDs\-PrimaryComputer** and then click **Edit**. The Multi\-valued String Editor dialog box appears.  
  
10. Right\-click the text box, click **Paste**, click **Add**, click **OK**, and then click **OK** again.  
  
## <a name="PrimaryComputer_Step2OptionallyenableprimarycomputersforFolderRedirectioninGro"></a>Step 2: Optionally enable primary computers for Folder Redirection in Group Policy  
The next step is to optionally configure Group Policy to enable primary computer support for Folder Redirection. Doing so enables a user's folders to be redirected on computers designated as the user's primary computers, but not on any other computers. You can control primary computers for Folder Redirection on a per\-computer basis, or a per\-user basis.  
  
#### To enable primary computers for Folder Redirection  
  
1.  In Group Policy Management, right\-click the GPO you created when doing the initial configuration of Folder Redirection and\/or Roaming User Profiles \(for example, **Folder Redirection Settings** or **Roaming User Profiles Settings**\), and then click **Edit**.  
  
2.  To enable primary computers support using computer\-based Group Policy, navigate to **Computer Configuration**. For user\-based Group Policy, navigate to **User Configuration**.  
  
    -   Computer\-based Group Policy applies primary computer processing to all computers to which the GPO applies, affecting all users of the computers.  
  
    -   User\-based Group Policy to applies primary computer processing to all user accounts to which the GPO applies, affecting all computers to which the users sign on.  
  
3.  Under **Computer Configuration** or **User Configuration**, navigate to **Policies**, then **Administrative Templates**, then **System**, then **Folder Redirection**.  
  
4.  Right\-click **Redirect folders on primary computers only**, and then click **Edit**.  
  
5.  Click **Enabled**, and then click **OK**.  
  
## <a name="PrimaryComputer_Step3OptionallyenableprimarycomputersforRoamingUserProfilesinG"></a>Step 3: Optionally enable primary computers for Roaming User Profiles in Group Policy  
The next step is to optionally configure Group Policy to enable primary computer support for Roaming User Profiles. Doing so enables a user's profile to roam on computers designated as the user's primary computers, but not on any other computers.  
  
#### To enable primary computers for Roaming User Profiles  
  
1.  Enable primary computer support for Folder Redirection, if you have not already.  
  
    This keeps documents and other user files out of the user profiles, which helps profiles remain small and sign on times stay fast.  
  
2.  In Group Policy Management, right\-click the GPO you created \(for example, **Folder Redirection and Roaming User Profiles Settings**\), and then click **Edit**.  
  
3.  Navigate to **Computer Configuration**, then **Policies**, then **Administrative Templates**, then **System**, and then **User Profiles**.  
  
4.  Right\-click **Download roaming profiles on primary computers only,** and then click **Edit**.  
  
5.  Click **Enabled**, and then click **OK**.  
  
## <a name="PrimaryComputer_Step4EnabletheGPO"></a>Step 4: Enable the GPO  
Once you have completed configuring Folder Redirection and Roaming User Profiles, enable the GPO if you have not already. Doing so permits it to be applied to affected users and computers.  
  
#### To enable the Folder Redirection and\/or Roaming User Profiles GPOs  
  
1.  Open Group Policy Management  
  
2.  Right\-click the GPOs that you created, and then click **Link Enabled**. A checkbox should appear next to the menu item.  
  
## <a name="PrimaryComputer_Step5Testprimarycomputerfunction"></a>Step 5: Test primary computer function  
To test primary computer support, sign in to a primary computer, confirm that the folders and profiles are redirected, then sign in to a non\-primary computer and confirm that the folders and profiles are not redirected.  
  
#### To test primary computer functionality  
  
1.  Sign in to a designated primary computer with a user account for which you have enabled Folder Redirection and\/or Roaming User Profiles.  
  
2.  If the user account has signed on to the computer previously, open a Windows PowerShell session or Command Prompt window as an administrator, type the following command and then sign off when prompted to ensure that the latest Group Policy settings are applied to the client computer:  
  
    ```  
    Gpupdate /force  
    ```  
  
3.  Open [!INCLUDE[win8_explorer](../Token/win8_explorer_md.md)].  
  
4.  Right\-click a redirected folder \(for example, the My Documents folder in the Documents library\), and then click **Properties**.  
  
5.  Click the **Location** tab, and confirm that the path displays the file share you specified instead of a local path. To confirm that the user profile is roaming, open **Control Panel**, click **System and Security**, click **System**, click **Advanced System Settings**, click **Settings** in the User Profiles section and then look for **Roaming** in the **Type** column.  
  
6.  Sign in with the same user account to a computer that is not designated as the user’s primary computer.  
  
7.  Repeat steps 2\-5, instead looking for local paths and a **Local** profile type.  
  
> [!NOTE]  
> If folders were redirected on a computer before you enabled primary computer support, the folders will remain redirected unless the following setting is configured in each folder's folder redirection policy setting: **Redirect the folder back to the local userprofile location when the policy is removed**. Similarly, profiles that were previously roaming on a particular computer will show **Roaming** in the **Type** columns; however, the **Status** column will show **Local**.  
  
## See Also  
[Deploy Folder Redirection with Offline Files](../Topic/Deploy-Folder-Redirection-with-Offline-Files.md)  
[Deploy Roaming User Profiles](../Topic/Deploy-Roaming-User-Profiles.md)  
[Folder Redirection, Offline Files, and Roaming User Profiles overview](../Topic/Folder-Redirection,-Offline-Files,-and-Roaming-User-Profiles-overview.md)  
[Digging a little deeper into Windows 8 Primary Computer](http://blogs.technet.com/b/askds/archive/2012/10/23/digging-a-little-deeper-into-windows-8-primary-computer.aspx)  
  
