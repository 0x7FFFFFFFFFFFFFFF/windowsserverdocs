---
title: Planning GPO Deployment
ms.custom: na
ms.prod: windows-server-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - techgroup-networking
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a0655db3-77a2-4b94-8a7f-12c76797fc7e
---
# Planning GPO Deployment
You can control which GPOs are applied to computers in Active Directory in a combination of three ways:

-   **Active Directory organizational unit hierarchy**. This involves linking the GPO to a specific OU in the Active Directory OU hierarchy. All computers in the OU and its subordinate containers receive and apply the GPO.

    Controlling GPO application through linking to OUs is typically used when you can organize the OU hierarchy according to your domain isolation zone requirements. GPOs can apply settings to computers based on their location within Active Directory. If a computer is moved from one OU to another, the policy linked to the second OU will eventually take effect when Group Policy detects the change during polling.

-   **Security group filtering**. This involves linking the GPOs to the domain level \(or other parent OU\) in the OU hierarchy, and then selecting which computers receive the GPO by using permissions that only allow correct group members to apply the GPO.

    The security group filters are attached to the GPOs themselves. A group is added to the security group filter of the GPO in Active Directory, and then assigned Read and Apply Group Policy permissions. Other groups can be explicitly denied Read and Apply Group Policy permissions. Only those computers whose group membership are granted Read and Apply Group Policy permissions without any explicit deny permissions can apply the GPO.

-   **WMI filtering**. A WMI filter is a query that is run dynamically when the GPO is evaluated. If a computer is a member of the result set when the WMI filter query runs, the GPO is applied to the computer.

    A WMI filter consists of one or more conditions that are evaluated against the local computer. You can check almost any characteristic of the computer, its operating system, and its installed programs. If all of the specified conditions are true for the computer, the GPO is applied; otherwise the GPO is ignored.

This guide uses a combination of security group filtering and WMI filtering to provide the most flexible options. If you follow this guidance, even though there might be five different GPOs linked to a specific group because of operating system version differences, only the correct GPO is applied.

## General considerations

-   Deploy your GPOs before you add any computer accounts to the groups that receive the GPOs. That way you can add your computers to the groups in a controlled manner. Be sure to add only a few test computers at first. Before adding many group members, examine the results on the test computers and verify that the configured firewall and connection security rules have the effect that you want. See the following sections for some suggestions on what to test before you continue.

## Test your deployed groups and GPOs
After you have deployed your GPOs and added some test computers to the groups, confirm the following before you continue with more group members:

-   Examine the GPOs that are both assigned to and filtered from the computer. Run the **gpresult** tool at a command prompt.

-   Examine the rules deployed to the computer. Open the [!INCLUDE[wfas](includes/wfas_md.md)] MMC snap\-in, expand the **Monitoring** node, and then expand the **Firewall** and **Connection Security** nodes.

-   Verify that communications are authenticated. Open the [!INCLUDE[wfas](includes/wfas_md.md)] MMC snap\-in, expand the **Monitoring** node, expand the **Security Associations** node, and then click **Main Mode**.

-   Verify that communications are encrypted when the computers require it. Open the [!INCLUDE[wfas](includes/wfas_md.md)] MMC snap\-in, expand the **Monitoring** node, expand the **Security Associations** node, and then select **Quick Mode**. Encrypted connections display a value other than **None** in the **ESP Confidentiality** column.

-   Verify that your programs are unaffected. Run them and confirm that they still work as expected.

After you have confirmed that the GPOs have been correctly applied, and that the computers are now communicating by using IPsec network traffic in request mode, you can begin to add more computers to the group accounts, in manageable numbers at a time. Continue to monitor and confirm the correct application of the GPOs to the computers.

## Do not enable require mode until deployment is complete
If you deploy a GPO that requires authentication to a computer before the other computers have a GPO deployed, communication between them might not be possible. Wait until you have all the zones and their GPOs deployed in request mode and confirm \(as described in the previous section\) that the computers are successfully communicating by using IPsec.

If there are problems with GPO deployment, or errors in configuration of one or more of the IPsec GPOs, computers can continue to operate, because request mode enables any computer to fall back to clear communications.

Only after you have added all of the computers to their zones, and you have confirmed that communications are working as expected, you can start changing the request mode rules to require mode rules where it is required in the zones. We recommend that you enable require mode in the zones one zone at a time, pausing to confirm that they are functioning properly before you continue. Turn the required mode setting on for the server isolation zones first, then the encryption zone, and then the isolated domain.

Do not change the boundary zone GPO, because it must stay in request mode for both inbound and outbound connections.

If you create other zones that require either inbound or outbound require mode, make the setting change in a manner that applies the setting in stages from the smaller groups of computers to the larger groups.

## Example Woodgrove Bank deployment plans
Woodgrove Bank links all its GPOs to the domain level container in the Active Directory OU hierarchy. It then uses the following WMI filters and security group filters to control the application of the GPOs to the correct subset of computers. All of the GPOs have the User Configuration section disabled to improve performance.

### GPO\_DOMISO\_Firewall\_2008\_Win7\-Vista

-   **WMI filter**. The WMI filter allows this GPO to apply only to computers that match the following WMI query:

    `select * from Win32_OperatingSystem where Version like "6.%" and ProductType <> "2"`

    > [!NOTE]
    > This excludes domain controllers \(which report a ProductType value of 2\). Do not include domain controllers in the isolated domain if there are computers running versions of Windows earlier than [!INCLUDE[nextref_vista](includes/nextref_vista_md.md)] and [!INCLUDE[nextref_longhorn](includes/nextref_longhorn_md.md)].

-   **Security filter**. This GPO grants Read and Apply Group Policy permissions only to computers that are members of the group CG\_DOMISO\_IsolatedDomain. The GPO also explicitly denies Read and Apply Group Policy permissions to members of the CG\_DOMISO\_NO\_IPSEC.

### GPO\_DOMISO\_IsolatedDomain\_Clients\_Win7Vista

-   **WMI filter**. The WMI filter allows this GPO to apply only to computers that match the following WMI query:

    `select * from Win32_OperatingSystem where Version like "6.%" and ProductType = "1"`

-   **Security filter**. This GPO grants Read and Apply Group Policy permissions only to computers that are members of the group CG\_DOMISO\_IsolatedDomain. The GPO also explicitly denies Read and Apply Group Policy permissions to members of the group CG\_DOMISO\_NO\_IPSEC.

### GPO\_DOMISO\_IsolatedDomain\_Servers\_WS2008

-   **WMI filter**. The WMI filter allows this GPO to apply only to computers that match the following WMI query:

    `select * from Win32_OperatingSystem where Version like "6.%" and ProductType = "3"`

    > [!NOTE]
    > This excludes domain controllers \(which report a ProductType value of 2\). Do not include domain controllers in the isolated domain if there are computers that are running versions of Windows earlier than [!INCLUDE[nextref_vista](includes/nextref_vista_md.md)] and [!INCLUDE[nextref_longhorn](includes/nextref_longhorn_md.md)].

-   **Security filter**. This GPO grants Read and Apply Group Policy permissions only to computers that are members of the group CG\_DOMISO\_IsolatedDomain. The GPO also explicitly denies Read and Apply Group Policy permissions to members of the group CG\_DOMISO\_NO\_IPSEC.

### GPO\_DOMISO\_Boundary\_WS2008

-   **WMI filter**. The WMI filter allows this GPO to apply only to computers that match the following WMI query:

    `select * from Win32_OperatingSystem where Version like "6.%" and ProductType = "3"`

    > [!NOTE]
    > This excludes domain controllers \(which report a ProductType value of 2\). Do not include domain controllers in the isolated domain if there are computers that are running versions of Windows earlier than [!INCLUDE[nextref_vista](includes/nextref_vista_md.md)] and [!INCLUDE[nextref_longhorn](includes/nextref_longhorn_md.md)].

-   **Security filter**. This GPO grants Read and Apply Group Policy permissions only to computers that are members of the group CG\_DOMISO\_Boundary. The GPO also explicitly denies Read and Apply Group Policy permissions to members of the group CG\_DOMISO\_NO\_IPSEC.

### GPO\_DOMISO\_Encryption\_WS2008

-   **WMI filter**. The WMI filter allows this GPO to apply only to computers that match the following WMI query:

    `select * from Win32_OperatingSystem where Version like "6.%" and ProductType = "3"`

    > [!NOTE]
    > This excludes domain controllers \(which report a ProductType value of 2\). Do not include domain controllers in the isolated domain if there are computers that are running versions of Windows earlier than [!INCLUDE[nextref_vista](includes/nextref_vista_md.md)] and [!INCLUDE[nextref_longhorn](includes/nextref_longhorn_md.md)].

-   **Security filter**. This GPO grants Read and Apply permissions in Group Policy only to computers that are members of the group CG\_DOMISO\_Encryption. The GPO also explicitly denies Read and Apply permissions in Group Policy to members of the group CG\_DOMISO\_NO\_IPSEC.


