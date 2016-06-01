---
title: Getting Started with Group Managed Service Accounts
ms.custom: na
ms.prod: windows-server-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - techgroup-security
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7130ad73-9688-4f64-aca1-46a9187a46cf
---
# Getting Started with Group Managed Service Accounts
This guide provides step\-by\-step instructions and background information for enabling and using group Managed Service Accounts in [!INCLUDE[win8_server_2](includes/win8_server_2_md.md)].

**In this document**

-   [Prerequisites](#BKMK_Prereqs)

-   [Introduction](#BKMK_Intro)

-   [Deploying a new server farm](#BKMK_DeployNewFarm)

-   [Adding member hosts to an existing server farm](#BKMK_AddMemberHosts)

-   [Updating the Group Managed Service Account properties](#BKMK_Update_gMSA)

-   [Decommissioning member hosts from an existing server farm](#BKMK_DecommMemberHosts)

-   [Decommissioning an existing server farm](#BKMK_DecommFarm)

> [!NOTE]
> [!INCLUDE[wps_howtorun](includes/wps_howtorun_md.md)]

## Prerequisites
See the section in this topic on [Requirements for group Managed Service Accounts](#BKMK_gMSA_Req).

## <a name="BKMK_Intro"></a>Introduction
When a client computer connects to a service which is hosted on a server farm using network load balancing \(NLB\) or some other method where all the servers appear to be the same service to the client, then authentication protocols supporting mutual authentication such as Kerberos cannot be used unless all the instances of the services use the same principal. This means that each service has to use the same passwords\/keys to prove their identity.

> [!NOTE]
> Failover clusters do not support gMSAs. However, services that run on top of the Cluster service can use a gMSA or a sMSA if they are a Windows service, an App pool, a scheduled task, or natively support gMSA or sMSA.

Services have the following principals from which to choose, and each has certain limitations.

|Principals|Scope|Services supported|Password management|
|--------------|---------|----------------------|-----------------------|
|Computer Account of Windows system|Domain|Limited to one domain joined server|Computer manages|
|Computer Account without Windows system|Domain|Any domain joined server|None|
|Virtual Account|Local|Limited to one server|Computer manages|
|Windows 7 standalone Managed Service Account|Domain|Limited to one domain joined server|Computer manages|
|User Account|Domain|Any domain joined server|None|
|Group Managed Service Account|Domain|Any [!INCLUDE[win8_server_2](includes/win8_server_2_md.md)] domain\-joined server|The domain controller manages, and the host retrieves|

A Windows computer account, or a Windows 7 standalone Managed Service Account \(sMSA\), or virtual accounts cannot be shared across multiple systems. If you configure one account for services on server farms to share, you would have to choose a user account or a computer account apart from a Windows system. Either way, these accounts do not have the capability of single\-point\-of\-control password management. This creates problem where each organization needs to create an expensive solution to update keys for the service in Active Directory and then distribute the keys to all instances of those services.

With [!INCLUDE[win8_server_2](includes/win8_server_2_md.md)], services or service administrators do not need to manage password synchronization between service instances when using group Managed Service Accounts \(gMSA\). You provision the gMSA in AD and then configure the service which supports Managed Service Accounts. You can provision a gMSA using the \*\-ADServiceAccount cmdlets which are part of the Active Directory module. Service identity configuration on the host is supported by:

-   Same APIs as sMSA, so products which support sMSA will support gMSA

-   Services which use Service Control Manager to configure logon identity

-   Services which use the IIS manager for application pools to configure identity

-   Tasks using Task Scheduler.

For more information about standalone Managed Service Accounts, see [Managed Service Accounts](http://technet.microsoft.com/library/ff641731(v=WS.10).aspx). For more information about group Managed Service Accounts, see [Group Managed Service Accounts Overview](Group-Managed-Service-Accounts-Overview.md).

### <a name="BKMK_gMSA_Req"></a>Requirements for group Managed Service Accounts
The following table lists the operating system requirements for Kerberos authentication to work with services using gMSA. The Active Directory requirements are listed after the table.

A 64\-bit architecture is required to run the Windows PowerShell commands used to administer group Managed Service Accounts.

**Operating system requirements**

|Element|Requirement|Operating system|
|-----------|---------------|--------------------|
|Client Application host|RFC compliant Kerberos client|At least Windows XP|
|User account’s domain DCs|RFC compliant KDC|At least Windows Server 2003|
|Shared service member hosts||[!INCLUDE[win8_server_2](includes/win8_server_2_md.md)]|
|Member host’s domain DCs|RFC compliant KDC|At least Windows Server 2003|
|gMSA account’s domain DCs|[!INCLUDE[win8_server_2](includes/win8_server_2_md.md)] DCs available for host to retrieve the password|Domain with [!INCLUDE[win8_server_2](includes/win8_server_2_md.md)] which can have some systems earlier than [!INCLUDE[win8_server_2](includes/win8_server_2_md.md)]|
|Backend service host|RFC compliant Kerberos application server|At least Windows Server 2003|
|Backend service account’s domain DCs|RFC compliant KDC|At least Windows Server 2003|
|Windows PowerShell for Active Directory|Windows PowerShell for Active Directory installed locally on a computer supporting a 64\-bit architecture or on your remote management computer \(for example, using the Remote Server Administration Toolkit\)|[!INCLUDE[win8_server_2](includes/win8_server_2_md.md)]|

**Active Directory Domain Service requirements**

-   The Active Directory schema in the gMSA domain’s forest needs to be updated to [!INCLUDE[win8_server_2](includes/win8_server_2_md.md)] to create a gMSA.

    You can update the schema by installing a domain controller that runs [!INCLUDE[win8_server_2](includes/win8_server_2_md.md)] or by running the version of adprep.exe from a computer running [!INCLUDE[win8_server_2](includes/win8_server_2_md.md)]. The object\-version attribute value for the object CN\=Schema,CN\=Configuration,DC\=Contoso,DC\=Com must be 52.

-   New gMSA account provisioned

-   If you are managing the service host permission to use gMSA by group, then new or existing security group

-   If managing service access control by group, then new or existing security group

-   If the first master root key for Active Directory is not deployed in the domain or has not been created, then create it. The result of its creation can be verified in the KdsSvc Operational log, Event ID 4004.

For instructions how to create the key, see [Create the Key Distribution Services KDS Root Key](Create-the-Key-Distribution-Services-KDS-Root-Key.md). Microsoft Key Distribution Service \(kdssvc.dll\) the root key for AD.

**Lifecycle**

The lifecycle of a server farm using the gMSA feature typically involves the following tasks:

-   Deploying a new server farm

-   Adding member hosts to an existing server farm

-   Decommissioning member hosts from an existing server farm

-   Decommissioning an existing server farm

-   Removing a compromised member host from a server farm if required.

## <a name="BKMK_DeployNewFarm"></a>Deploying a new server farm
When deploying a new server farm, the service administrator will need to determine:

-   If the service supports using gMSAs

-   If the service requires inbound or outbound authenticated connections

-   The computer account names for the member hosts for the service using the gMSA

-   The NetBIOS name for the service

-   The DNS host name for the service

-   The Service Principal Names \(SPNs\) for the service

-   The password change interval \(default is 30 days\).

### <a name="BKMK_Step1"></a>Step 1: Provisioning group Managed Service Accounts
You can create a gMSA only if the forest schema has been updated to [!INCLUDE[win8_server_2](includes/win8_server_2_md.md)], the master root key for Active Directory has been deployed, and there is at least one [!INCLUDE[win8_server_2](includes/win8_server_2_md.md)] DC in the domain in which the gMSA will be created.

Membership in **Domain Admins**, **Account Operators** or ability to create msDS\-GroupManagedServiceAccount objects, is the minimum required to complete the following procedures. For detailed information about using the appropriate accounts and group memberships, see [Local and Domain Default Groups](http://technet.microsoft.com/library/dd728026(WS.10).aspx).

#### <a name="BKMK_CreateGMSA"></a>To create a gMSA using the New\-ADServiceAccount cmdlet

1.  On the [!INCLUDE[win8_server_2](includes/win8_server_2_md.md)] domain controller, run Windows PowerShell from the Taskbar.

2.  At the command prompt for the Windows PowerShell, type the following commands, and then press ENTER. \(The Active Directory module will load automatically.\)

    **New\-ADServiceAccount \[\-Name\] <string> \-DNSHostName <string> \[\-KerberosEncryptionType <ADKerberosEncryptionType>\] \[\-ManagedPasswordIntervalInDays <Nullable\[Int32\]>\] \[\-PrincipalsAllowedToRetrieveManagedPassword <ADPrincipal\[\]>\] \-SamAccountName <string> \-ServicePrincipalNames <string\[\]>**

    |Parameter|String|Example|
    |-------------|----------|-----------|
    |Name|Name of the account|ITFarm1|
    |DNSHostName|DNS host name of service|ITFarm1.contoso.com|
    |KerberosEncryptionType|Any encryption types supported by the host servers|RC4, AES128, AES256|
    |ManagedPasswordIntervalInDays|Password change interval in days \(default is 30 days if not provided\)|90|
    |PrincipalsAllowedToRetrieveManagedPassword|The computer accounts of the member hosts or the security group that the member hosts are a member of|ITFarmHosts|
    |SamAccountName|NetBIOS name for the service if not same as Name|ITFarm1|
    |ServicePrincipalNames|Service Principal Names \(SPNs\) for the service|http\/ITFarm1.contoso.com\/contoso.com, http\/ITFarm1.contoso.com\/contoso, http\/ITFarm1\/contoso.com, http\/ITFarm1\/contoso|

    > [!IMPORTANT]
    > The password change interval can only be set during creation. If you need to change the interval, you must create a new gMSA and set it at creation time.

    **Example**

    Enter the command on a single line, even though they might appear word\-wrapped across several lines here because of formatting constraints.

    ```
    New-ADServiceAccount ITFarm1 -DNSHostName ITFarm1.contoso.com -PrincipalsAllowedToRetrieveManagedPassword ITFarmHosts -KerberosEncryptionType RC4, AES128, AES256 -ServicePrincipalNames http/ITFarm1.contoso.com/contoso.com, http/ITFarm1.contoso.com/contoso, http/ITFarm1/contoso.com, http/ITFarm1/contoso

    ```

Membership in **Domain Admins**, **Account Operators**, or ability to create msDS\-GroupManagedServiceAccount objects, is the minimum required to complete this procedure. For detailed information about using the appropriate accounts and group memberships, see [Local and Domain Default Groups](http://technet.microsoft.com/library/dd728026(WS.10).aspx).

##### To create a gMSA for outbound authentication only using the New\-ADServiceAccount cmdlet

1.  On the [!INCLUDE[win8_server_2](includes/win8_server_2_md.md)] domain controller, run Windows PowerShell from the Taskbar.

2.  At the command prompt for the Windows PowerShell Active Directory module, type the following commands, and then press ENTER:

    **New\-ADServiceAccount \[\-Name\] <string> \-RestrictToOutboundAuthenticationOnly \[\-ManagedPasswordIntervalInDays <Nullable\[Int32\]>\] \[\-PrincipalsAllowedToRetrieveManagedPassword <ADPrincipal\[\]>\]**

    |Parameter|String|Example|
    |-------------|----------|-----------|
    |Name|Name the account|ITFarm1|
    |ManagedPasswordIntervalInDays|Password change interval in days \(default is 30 days if not provided\)|75|
    |PrincipalsAllowedToRetrieveManagedPassword|The computer accounts of the member hosts or the security group that the member hosts are a member of|ITFarmHosts|

    > [!IMPORTANT]
    > The password change interval can only be set during creation. If you need to change the interval, you must create a new gMSA and set it at creation time.

**Example**

```
New-ADServiceAccount ITFarm1 -RestrictToOutboundAuthenticationOnly - PrincipalsAllowedToRetrieveManagedPassword ITFarmHosts

```

### <a name="BKMK_ConfigureServiceIdentity"></a>Step 2: Configuring service identity application service
To configure the services in [!INCLUDE[win8_server_2](includes/win8_server_2_md.md)], see the following feature documentation:

-   IIS application pool

    For more information, see [Specify an Identity for an Application Pool \(IIS 7\)](http://technet.microsoft.com/library/cc771170(WS.10).aspx).

-   Windows Services

    For more information, see [Services](http://technet.microsoft.com/library/cc772408.aspx).

-   Tasks

    For more information, see the [Task Scheduler Overview](http://technet.microsoft.com/library/cc721871.aspx).

Other services could support gMSA. See the appropriate product documentation for details on how to configure those services.

## <a name="BKMK_AddMemberHosts"></a>Adding member hosts to an existing server farm
If using security groups for managing member hosts, add the computer account for the new member host to the security group \(that the gMSA’s member hosts are a member of\) using one of the following methods.

Membership in **Domain Admins**, or the ability to add members to the security group object, is the minimum required to complete these procedures. For detailed information about using the appropriate accounts and group memberships, see [Local and Domain Default Groups](http://technet.microsoft.com/library/dd728026(WS.10).aspx).

-   Method 1: Active Directory Users and Computers

    For procedures how to use this method, see [Add a computer account to a group](http://technet.microsoft.com/library/cc733097.aspx) using the Windows interface, and [Manage Different Domains in Active Directory Administrative Center](http://technet.microsoft.com/library/dd560632(WS.10).aspx).

-   Method 2: dsmod

    For procedures how to use this method, see [Add a computer account to a group](http://technet.microsoft.com/library/cc733097.aspx) using the command line.

-   Method 3: Windows PowerShell Active Directory cmdlet Add\-ADPrincipalGroupMembership

    For procedures how to use this method, see [Add\-ADPrincipalGroupMembership](http://technet.microsoft.com/library/ee617203.aspx).

If using computer accounts, find the existing accounts and then add the new computer account.

Membership in **Domain Admins**, **Account Operators**, or ability to manage msDS\-GroupManagedServiceAccount objects, is the minimum required to complete this procedure. For detailed information about using the appropriate accounts and group memberships, see Local and Domain Default Groups.

#### To add member hosts using the Set\-ADServiceAccount cmdlet

1.  On the [!INCLUDE[win8_server_2](includes/win8_server_2_md.md)] domain controller, run Windows PowerShell from the Taskbar.

2.  At the command prompt for the Windows PowerShell Active Directory module, type the following commands, and then press ENTER:

    **Get\-ADServiceAccount \[\-Name\] <string> \-PrincipalsAllowedToRetrieveManagedPassword**

3.  At the command prompt for the Windows PowerShell Active Directory module, type the following commands, and then press ENTER:

    **Set\-ADServiceAccount \[\-Name\] <string> \-PrincipalsAllowedToRetrieveManagedPassword <ADPrincipal\[\]>**

|Parameter|String|Example|
|-------------|----------|-----------|
|Name|Name the account|ITFarm1|
|PrincipalsAllowedToRetrieveManagedPassword|The computer accounts of the member hosts or the security group that the member hosts are a member of|Host1, Host2, Host3|

**Example**

For example, to add member hosts type the following commands, and then press ENTER.

```
Get-ADServiceAccount [-Name] ITFarm1 -PrincipalsAllowedToRetrieveManagedPassword

```

```
Set-ADServiceAccount [-Name] ITFarm1-PrincipalsAllowedToRetrieveManagedPassword Host1 Host2 Host3

```

## <a name="BKMK_Update_gMSA"></a>Updating the group Managed Service Account properties
Membership in **Domain Admins**, **Account Operators**, or the ability to write to msDS\-GroupManagedServiceAccount objects, is the minimum required to complete these procedures. For detailed information about using the appropriate accounts and group memberships, see [Local and Domain Default Groups](http://technet.microsoft.com/library/dd728026(WS.10).aspx).

Open the Active Directory Module for Windows PowerShell, and set any property by using the Set\-ADServiceAccount cmdlet.

For detailed information how to set these properties, see [Set\-ADServiceAccount](http://technet.microsoft.com/library/ee617252.aspx) in the TechNet Library or by typing **Get\-Help Set\-ADServiceAccount** at the Active Directory module for Windows PowerShell command prompt and pressing ENTER.

## <a name="BKMK_DecommMemberHosts"></a>Decommissioning member hosts from an existing server farm
Membership in **Domain Admins**, or ability to remove members from the security group object, is the minimum required to complete these procedures. For detailed information about using the appropriate accounts and group memberships, see [Local and Domain Default Groups](http://technet.microsoft.com/library/dd728026(WS.10).aspx).

### Step 1: Remove member host from gMSA
If using security groups for managing member hosts, remove the computer account for the decommissioned member host from the security group that the gMSA’s member hosts are a member of using either of the following methods.

-   Method 1: Active Directory Users and Computers

    For procedures how to use this method, see [Delete a Computer Account](http://technet.microsoft.com/library/cc754624.aspx) using the Windows interface, and [Manage Different Domains in Active Directory Administrative Center](http://technet.microsoft.com/library/dd560632(WS.10).aspx).

-   Method 2: drsm

    For procedures how to use this method, see [Delete a Computer Account](http://technet.microsoft.com/library/cc754624.aspx) using the command line.

-   Method 3: Windows PowerShell Active Directory cmdlet Remove\-ADPrincipalGroupMembership

    For detailed information how to do this, see  [Remove\-ADPrincipalGroupMembership](http://technet.microsoft.com/library/ee617243.aspx) in the TechNet Library or by typing **Get\-Help Remove\-ADPrincipalGroupMembership** at the Active Directory module for Windows PowerShell command prompt and pressing ENTER.

If listing computer accounts, retrieve the existing accounts and then add all but the removed computer account.

Membership in **Domain Admins**, **Account Operators**, or ability to manage msDS\-GroupManagedServiceAccount objects, is the minimum required to complete this procedure. For detailed information about using the appropriate accounts and group memberships, see Local and Domain Default Groups.

##### To remove member hosts using the Set\-ADServiceAccount cmdlet

1.  On the [!INCLUDE[win8_server_2](includes/win8_server_2_md.md)] domain controller, run Windows PowerShell from the Taskbar.

2.  At the command prompt for the Windows PowerShell Active Directory module, type the following commands, and then press ENTER:

    **Get\-ADServiceAccount \[\-Name\] <string> \-PrincipalsAllowedToRetrieveManagedPassword**

3.  At the command prompt for the Windows PowerShell Active Directory module, type the following commands, and then press ENTER:

    **Set\-ADServiceAccount \[\-Name\] <string> \-PrincipalsAllowedToRetrieveManagedPassword <ADPrincipal\[\]>**

|Parameter|String|Example|
|-------------|----------|-----------|
|Name|Name the account|ITFarm1|
|PrincipalsAllowedToRetrieveManagedPassword|The computer accounts of the member hosts or the security group that the member hosts are a member of|Host1,  Host3|

**Example**

For example, to remove member hosts type the following commands, and then press ENTER.

```
Get-ADServiceAccount [-Name] ITFarm1 -PrincipalsAllowedToRetrieveManagedPassword

```

```
Set-ADServiceAccount [-Name] ITFarm1 -PrincipalsAllowedToRetrieveManagedPassword Host1 Host3

```

### <a name="BKMK_RemoveGMSA"></a>Step 2: Removing a group Managed Service Account from the system
Remove the cached gMSA credentials from the member host using Uninstall\-ADServiceAccount or the NetRemoveServiceAccount API on the host system.

Membership in **Administrators**, or equivalent, is the minimum required to complete these procedures. For detailed information about using the appropriate accounts and group memberships, see [Local and Domain Default Groups](http://technet.microsoft.com/library/dd728026(WS.10).aspx).

##### To remove a gMSA using the Uninstall\-ADServiceAccount cmdlet

1.  On the [!INCLUDE[win8_server_2](includes/win8_server_2_md.md)] domain controller, run Windows PowerShell from the Taskbar.

2.  At the command prompt for the Windows PowerShell Active Directory module, type the following commands, and then press ENTER:

    **Uninstall\-ADServiceAccount < ADServiceAccount>**

    **Example**

    For example, to remove the cached credentials for a gMSA named ITFarm1 type the following command, and then press ENTER:

    ```
    Uninstall-ADServiceAccount ITFarm1
    ```

For more information about the Uninstall\-ADServiceAccount cmdlet, at the Active Directory module for Windows PowerShell command prompt, type **Get\-Help Uninstall\-ADServiceAccount**, and then press ENTER, or see the information on the TechNet web at [Uninstall\-ADServiceAccount](http://technet.microsoft.com/library/ee617202.aspx).

## <a name="BKMK_DecommFarm"></a>Decommissioning an existing server farm
When decommissioning an existing server farm, you should remove the following objects from AD:

-   If the gMSA is the only member, the security group that the gMSA is a member of which is used for access control

-   If the security group is only used for member hosts, the security group that the member hosts are a member of

-   gMSA.

To delete a security group, use Active Directory Users and Computers, dsrm or Remove\-ADGroup. To delete a gMSA, use Active Directory Users and Computers or Remove\-ADServiceAccount.

### Step 1: Deleting Active Directory Objects
Membership in **Domain Admins**, **Account Operators**, or ability to delete msDS\-GroupManagedServiceAccount and security group objects, is the minimum required to complete these procedures. For detailed information about using the appropriate accounts and group memberships, see [Local and Domain Default Groups](http://technet.microsoft.com/library/dd728026(WS.10).aspx).

##### To remove a gMSA using the Remove\-ADServiceAccount cmdlet

1.  On the [!INCLUDE[win8_server_2](includes/win8_server_2_md.md)] domain controller, run Windows PowerShell from the Taskbar.

2.  At the command prompt for the Windows PowerShell Active Directory module, type the following commands, and then press ENTER:

    **Remove\-ADServiceAccount < ADServiceAccount>**

    **Example**

    For example, to delete a gMSA named ITFarm1 type the following command, and then press ENTER:

    ```
    Remove-ADServiceAccount ITFarm1

    ```

For more information about the Remove\-ADServiceAccount cmdlet, at the Active Directory module for Windows PowerShell command prompt, type **Get\-Help Remove\-ADServiceAccount**, and then press ENTER, or see the information on the TechNet web at [Remove\-ADServiceAccount](http://technet.microsoft.com/library/ee617190.aspx).

### Step 2: Removing a group Managed Service Account from the system
Use the procedures described in [Removing a group Managed Service Account from the system](#BKMK_RemoveGMSA) in this topic.

## <a name="BKMK_Links"></a>See also

-   [Group Managed Service Accounts Overview](Group-Managed-Service-Accounts-Overview.md)

-   [Managed Service Accounts](http://technet.microsoft.com/library/ff641731(v=ws.10).aspx)


