---
title: Configure Authentication Methods on Windows 8, Windows 7, Windows Vista, Windows Server 2012, Windows Server 2008, and Windows Server 2008 R2
ms.custom: na
ms.prod: windows-server-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - techgroup-networking
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a0c26e9f-2f0e-46ad-a38b-8d5077ace49d
author: vhorne
---
# Configure Authentication Methods on Windows 8, Windows 7, Windows Vista, Windows Server 2012, Windows Server 2008, and Windows Server 2008 R2
This procedure shows you how to configure the authentication methods that can be used by computers in an isolated domain or standalone isolated server zone.  
  
> [!NOTE]  
> If you follow the steps in the procedure in this topic, you alter the system\-wide default settings. Any connection security rule can use these settings by specifying **Default** on the **Authentication** tab.  
  
**Administrative credentials**  
  
To complete these procedures, you must be a member of the Domain Administrators group, or otherwise be delegated permissions to modify the GPOs.  
  
### To configure authentication methods  
  
1.  [Open the Group Policy Management Console to Windows Firewall with Advanced Security](../Topic/Open-the-Group-Policy-Management-Console-to-Windows-Firewall-with-Advanced-Security.md).  
  
2.  In the details pane on the main [!INCLUDE[wfas](../Token/wfas_md.md)] page, click **Windows Firewall Properties**.  
  
3.  On the **IPsec Settings** tab, click **Customize**.  
  
4.  In the **Authentication Method** section, select the type of authentication that you want to use from among the following:  
  
    1.  **Default**. Selecting this option tells the computer to use the authentication method currently defined by the local administrator in [!INCLUDE[wfas](../Token/wfas_md.md)] or by Group Policy as the default.  
  
    2.  **Computer and User \(using Kerberos V5\)**. Selecting this option tells the computer to use and require authentication of both the computer and the currently logged\-on user by using their domain credentials. This authentication method works only with other computers that can use Authenticated IP \(AuthIP\), including [!INCLUDE[win8_client_2](../Token/win8_client_2_md.md)], [!INCLUDE[nextref_client_7](../Token/nextref_client_7_md.md)], [!INCLUDE[nextref_vista](../Token/nextref_vista_md.md)], [!INCLUDE[win8_server_2](../Token/win8_server_2_md.md)], [!INCLUDE[nextref_longhorn](../Token/nextref_longhorn_md.md)], and [!INCLUDE[nextref_server_7](../Token/nextref_server_7_md.md)]. User\-based authentication using Kerberos V5 is not supported by IKE v1.  
  
    3.  **Computer \(using Kerberos V5\)**. Selecting this option tells the computer to use and require authentication of the computer by using its domain credentials. This option works with other computers that can use IKE v1, including earlier versions of Windows.  
  
    4.  **User \(using Kerberos V5\)**. Selecting this option tells the computer to use and require authentication of the currently logged\-on user by using his or her domain credentials. This authentication method works only with other computers that can use AuthIP, including [!INCLUDE[win8_client_2](../Token/win8_client_2_md.md)], [!INCLUDE[nextref_client_7](../Token/nextref_client_7_md.md)], [!INCLUDE[nextref_vista](../Token/nextref_vista_md.md)], [!INCLUDE[win8_server_2](../Token/win8_server_2_md.md)], [!INCLUDE[nextref_longhorn](../Token/nextref_longhorn_md.md)], and [!INCLUDE[nextref_server_7](../Token/nextref_server_7_md.md)]. User\-based authentication using Kerberos V5 is not supported by IKE v1.  
  
    5.  **Computer certificate from this certification authority**. Selecting this option and entering the identification of a certification authority \(CA\) tells the computer to use and require authentication by using a certificate that is issued by the selected CA. If you also select **Accept only health certificates**, then only certificates that include the system health authentication enhanced key usage \(EKU\) typically provided in a Network Access Protection \(NAP\) infrastructure can be used for this rule.  
  
    6.  **Advanced**. Click **Customize** to specify a custom combination of authentication methods required for your scenario. You can specify both a **First authentication method** and a **Second authentication method**.  
  
        The first authentication method can be one of the following:  
  
        -   **Computer \(Kerberos V5\)**. Selecting this option tells the computer to use and require authentication of the computer by using its domain credentials. This option works with other computers that can use IKE v1, including earlier versions of Windows.  
  
        -   **Computer \(NTLMv2\)**. Selecting this option tells the computer to use and require authentication of the computer by using its domain credentials. This option works only with other computers that can use AuthIP, including [!INCLUDE[win8_client_2](../Token/win8_client_2_md.md)], [!INCLUDE[nextref_client_7](../Token/nextref_client_7_md.md)], [!INCLUDE[nextref_vista](../Token/nextref_vista_md.md)], [!INCLUDE[win8_server_2](../Token/win8_server_2_md.md)], [!INCLUDE[nextref_longhorn](../Token/nextref_longhorn_md.md)], and [!INCLUDE[nextref_server_7](../Token/nextref_server_7_md.md)]. User\-based authentication using Kerberos V5 is not supported by IKE v1.  
  
        -   **Computer certificate from this certification authority \(CA\)**. Selecting this option and entering the identification of a CA tells the computer to use and require authentication by using a certificate that is issued by that CA. If you also select **Accept only health certificates**, then only certificates issued by a NAP server can be used.  
  
        -   **Preshared key \(not recommended\)**. Selecting this method and entering a preshared key tells the computer to authenticate by exchanging the preshared keys. If they match, then the authentication succeeds. This method is not recommended, and is included only for backward compatibility and testing purposes.  
  
        If you select **First authentication is optional**, then the connection can succeed even if the authentication attempt specified in this column fails.  
  
        The second authentication method can be one of the following:  
  
        -   **User \(Kerberos V5\)**. Selecting this option tells the computer to use and require authentication of the currently logged\-on user by using his or her domain credentials. This authentication method works only with other computers that can use AuthIP, including [!INCLUDE[win8_client_2](../Token/win8_client_2_md.md)], [!INCLUDE[nextref_client_7](../Token/nextref_client_7_md.md)], [!INCLUDE[nextref_vista](../Token/nextref_vista_md.md)], [!INCLUDE[win8_server_2](../Token/win8_server_2_md.md)], [!INCLUDE[nextref_longhorn](../Token/nextref_longhorn_md.md)], and [!INCLUDE[nextref_server_7](../Token/nextref_server_7_md.md)]. User\-based authentication using Kerberos V5 is not supported by IKE v1.  
  
        -   **User \(NTLMv2\)**. Selecting this option tells the computer to use and require authentication of the currently logged\-on user by using his or her domain credentials, and uses the NTLMv2 protocol instead of Kerberos V5. This authentication method works only with other computers that can use AuthIP, including [!INCLUDE[win8_client_2](../Token/win8_client_2_md.md)], [!INCLUDE[nextref_client_7](../Token/nextref_client_7_md.md)], [!INCLUDE[nextref_vista](../Token/nextref_vista_md.md)], [!INCLUDE[win8_server_2](../Token/win8_server_2_md.md)], [!INCLUDE[nextref_longhorn](../Token/nextref_longhorn_md.md)], and [!INCLUDE[nextref_server_7](../Token/nextref_server_7_md.md)]. User\-based authentication using Kerberos V5 is not supported by IKE v1.  
  
        -   **User health certificate from this certification authority \(CA\)**. Selecting this option and entering the identification of a CA tells the computer to use and require user\-based authentication by using a certificate that is issued by the specified CA. If you also select **Enable certificate to account mapping**, then the certificate can be associated with a user in Active Directory for purposes of granting or denying access to specified users or user groups.  
  
        -   **Computer health certificate from this certification authority \(CA\)**. Selecting this option and entering the identification of a CA tells the computer to use and require authentication by using a certificate that is issued by the specified CA. If you also select **Accept only health certificates**, then only certificates that include the system health authentication EKU typically provided in a NAP infrastructure can be used for this rule.  
  
        If you select **Second authentication is optional**, then the connection can succeed even if the authentication attempt specified in this column fails.  
  
        > [!IMPORTANT]  
        > Make sure that you do not select the check boxes to make both first and second authentication optional. Doing so allows plaintext connections whenever authentication fails.  
  
5.  Click **OK** on each dialog box to save your changes and return to the Group Policy Management Editor.  
  
If you arrived at this page by clicking a link in a checklist, use your browser’s **Back** button to return to the checklist.  
  
