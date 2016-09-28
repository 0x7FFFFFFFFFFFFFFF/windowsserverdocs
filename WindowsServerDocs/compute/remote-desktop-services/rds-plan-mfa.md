---
title: Remote Desktop Services - Multi-Factor Authentication
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 09ea784e-5644-417a-a3d9-bdbcebc313f9
author: lizap
ms.author: elizapo
ms.date: 09/07/2016
manager: dongill
---
# Remote Desktop Services - Multi-Factor Authentication

>Applies To: Windows Server 2016

Leverage the power of Active Directory with Multi-Factor Authentication to enforce high security protection of your business resources.

For your end-users connecting to their desktops and applications, the experience is similar to what they already face as they perform a second authentication measure to connect to the desired resource:
- Launch a desktop or RemoteApp from an RDP file or through a Remote Desktop client application
- Upon connecting to the RD Gateway for secure, remote access, receive an SMS or mobile application MFA challenge
- Correctly authenticate and get connected to their resource!

As an admin, there are several steps to take:
- **Create Azure MFA provider (requires Azure subscription)**: Performs the MFA challenge and validation for the end-user
- **Create/install Azure MFA server**: Receives authentication requests from the RD Gateway, uses the MFA service for authentication, then relays the success/failure to the RD Gateway
- **Configure RD Gateway server as RADIUS server**: Instead of immediately processing the username/password for the user, prompts the MFA server to perform a MFA challenge, then validates credentials after receiving the successful MFA challenge

For a more in-depth description of the step-by-step configuration process, please read this detailed [article](http://www.rdsgurus.com/uncategorized/step-by-step-using-windows-server-2012-r2-rd-gateway-with-azure-multifactor-authentication/) provided by Microsoft MVPs.