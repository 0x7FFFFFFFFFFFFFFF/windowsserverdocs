---
title: Deploy a RD Web Access and Gateway farm
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6f837325-cd40-4414-a8a5-ebf759fbbb18
author: lizap
---
# Deploy a RD Web Access and Gateway farm
You can deploy a Remote Desktop Web Access (RD Web Access) and Remote Desktop Gateway (RD Gateway) farm to improve the availability and scale of a Windows Server 2012 R2 Remote Desktop Services (RDS) deployment in Microsoft Azure Infrastructure Services. This document assumes, as a starting point, a basic desktop hosting deployment based on the Microsoft Azure Desktop Hosting Reference Architecture Guide and the Microsoft Azure Desktop Hosting Deployment Guide.  
  
The scope of this document is limited to:  
- Deployment guidance for adding a second RD Web Access and RD Gateway virtual machine to a basic desktop hosting deployment.  
  
  For higher scale, additional virtual machines running RD Web Access and RD Gateway can be added by repeating the steps in this document.  
After reading this document, the reader should understand:  
  
- How to deploy a second RD Web Access and RD Gateway virtual machine within a basic desktop hosting deployment in a single Microsoft Azure Cloud Service.  
  
  
There are multiple ways to deploy a desktop hosting solution. Throughout the document, specific examples are given that can be used as a starting point for a deployment. These examples are identified with ().  
  
Before you start, make sure you have configured your environment for Remote Desktop Services. Also, you need to create a basic Remote Desktop Services desktop hosting deployment, as described in Desktop hosting in Azure IaaS.