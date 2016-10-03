---
ms.assetid: a33bd54c-e6db-4b58-8264-c0f34bd8ba39
title: Walkthrough - Workplace Join to an Android device
description:
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/13/2016
ms.topic: article
ms.prod: windows-server-threshold
ms.service: active-directory
ms.technology: identity-adfs
---
# Walkthrough: Workplace Join to an Android device

>Applies To: Windows Server Technical Preview


## Join your device with Workplace Join

> [!NOTE]
> Android workplace join requires Azure Active Directory Device Registration Service. In order to enforce conditional device policies on-premises, Directory Synchronization Tool (DirSync) must be deployed with device object write-back option enabled. At the present time, device write-back to Active Directory from Azure Active Directory can take up-to 3 hours. As such, users must wait for 3 hours to access on-premises web applications, after creating a work account. For more information about deploying Azure Active Directory Device Registration service, see, [Azure Active Directory Device Registration Service Overview](http://msdn.microsoft.com/library/azure/dn788908.aspx)

#### Create a Work account that joins your device with workplace Join

1.  You will need to install Azure Authenticator application on your device to create a work account that joins your device with Workplace join. The following URL has instructions on how to install Azure authenticator app on your Android device and add a work account. The work account makes your Android device into a trusted device and provides Single Sign-On (SSO) to the applications on device. You can use the trusted device to access web applications and modern line-of-business applications as recommended by your IT administrator. For more information, see [Azure Authenticator for Android](http://sandboxmsdnstage.redmond.corp.microsoft.com/cef46959-2b2d-459e-a230-d6fff182fe82.aspx).

## See Also
[Join to Workplace from Any Device for SSO and Seamless Second Factor Authentication Across Company Applications](Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)
[Step-by-Step Guide for On-premises Conditional Access using Azure Active Directory Device Registration Service](http://sandboxmsdnstage.redmond.corp.microsoft.com/9cfac381-9235-4f47-923e-31866309b2be.aspx)


