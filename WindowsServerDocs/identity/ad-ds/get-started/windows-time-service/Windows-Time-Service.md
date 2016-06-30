---
title: Windows Time Service
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.service: 
ms.suite: na
ms.technology: 
  - active-directory-domain-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a0fcd250-e5f7-41b3-b0e8-240f8236e210
author: femila
---
# Windows Time Service

>Applies To: Windows Server Technical Preview

  
  
## <a name="w2k3tr_times_intro"></a>Windows Time Service Technical Reference  
**In this guide**  
  
* Where to find Windows Time Service Configuration Information  
* What is the Windows Time Service?  
* Importance of Time Protocols  
* How the Windows Time Service Works   
* Windows Time Service Tools and Settings  
  
> [!NOTE]  
<<<<<<< HEAD
> In Windows Server 2003 and Microsoft Windows 2000 Server, the directory service is named Active Directory directory service. In  Windows Server 2008 R2  and  Windows Server 2008 , the directory service is named Active Directory Domain Services (AD DS). The rest of this topic refers to AD DS, but the information is also applicable to Active Directory Domain Services in Windows Server 2016.  
  
The Windows Time service, also known as W32Time, synchronizes the date and time for all computers running in an AD DS domain. Time synchronization is critical for the proper operation of many Windows services and line-of-business applications. The Windows Time service uses the Network Time Protocol (NTP) to synchronize computer clocks on the network so that an accurate clock value, or time stamp, can be assigned to network validation and resource access requests. The service integrates NTP and time providers, making it a reliable and scalable time service for enterprise administrators.  
=======
> In Windows Server� 2003 and Microsoft Windows 2000 Server, the directory service is named Active Directory� directory service. In  Windows Server 2008 R2  and  Windows Server 2008 , the directory service is named Active Directory Domain Services (AD DS). The rest of this topic refers to AD DS, but the information is also applicable to Active Directory Domain Services in Windows Server 2016.  
  
The Windows� Time service, also known as W32Time, synchronizes the date and time for all computers running in an AD DS domain. Time synchronization is critical for the proper operation of many Windows services and line-of-business applications. The Windows Time service uses the Network Time Protocol (NTP) to synchronize computer clocks on the network so that an accurate clock value, or time stamp, can be assigned to network validation and resource access requests. The service integrates NTP and time providers, making it a reliable and scalable time service for enterprise administrators.  
>>>>>>> 9aa2dce86f802cd3079157fffcd57e0fc313c401
  
> [!IMPORTANT]  
> The W32Time service is not a full-featured NTP solution that meets time-sensitive application needs and is not supported by Microsoft as such. For more information, see Microsoft Knowledge Base article 939322, [Support boundary to configure the Windows Time service for high-accuracy environments](http://go.microsoft.com/fwlink/?LinkID=179459) (http://go.microsoft.com/fwlink/?LinkID=179459).  
  
## <a name="BKMK_Config"></a>Where to Find Windows Time Service Configuration Information  
This guide does **not** discuss configuring the Windows Time service. There are several different topics on Microsoft TechNet and in the Microsoft Knowledge Base that do explain procedures for configuring the Windows Time service. If you require configuration information, the following topics should help you locate the appropriate information.  
  
-   To configure the Windows Time service for the forest root primary domain controller (PDC) emulator, see:  
  
    -   [Configure the Windows Time service on the PDC emulator in the forest root domain](http://go.microsoft.com/fwlink/?LinkId=91969) (http://go.microsoft.com/fwlink/?LinkId=91969)  
  
    -   [Configuring a time source for the forest](http://go.microsoft.com/fwlink/?LinkId=111146) (http://go.microsoft.com/fwlink/?LinkId=111146)  
  
    -   Microsoft Knowledge Base article 816042, [How to configure an authoritative time server in Windows Server](http://go.microsoft.com/fwlink/?LinkID=60402) (http://go.microsoft.com/fwlink/?LinkID=60402), which describes configuration settings for computers running Windows Server 2008 R2, Windows Server 2008, Windows Server 2003, and Windows Server 2003 R2.  
  
    -   Microsoft Knowledge Base article 216734, [How to configure an authoritative time server in Windows 2000](http://go.microsoft.com/fwlink/?LinkID=23042) (http://go.microsoft.com/fwlink/?LinkID=23042), which describes configuration settings for computers running Windows 2000 Server.  
  
-   To configure the Windows Time service on any domain member client or server, or even domain controllers that are not configured as the forest root PDC emulator, see [Configure a client computer for automatic domain time synchronization](http://go.microsoft.com/fwlink/?LinkId=91376) (http://go.microsoft.com/fwlink/?LinkId=91376).  
  
    > [!WARNING]  
    > Some applications may require their computers to have high-accuracy time services. If that is the case, you may choose to configure a manual time source, but be aware that the Windows Time service was not designed to function as a highly accurate time source. Ensure that you are aware of the support limitations for high-accuracy time environments as described in Microsoft Knowledge Base article 939322, [Support boundary to configure the Windows Time service for high-accuracy environments](http://go.microsoft.com/fwlink/?LinkID=179459) (http://go.microsoft.com/fwlink/?LinkID=179459).  
  
-   To configure the Windows Time service on any Windows-based client or server computers that are configured as workgroup members instead of domain members see [Configure a manual time source for a selected client computer](http://go.microsoft.com/fwlink/?LinkId=91377) (http://go.microsoft.com/fwlink/?LinkId=91377).  
  
-   To configure the Windows Time service on a host computer that runs a virtual environment, see Microsoft Knowledge Base article 816042, [How to configure an authoritative time server in Windows Server](http://go.microsoft.com/fwlink/?LinkID=60402) (http://go.microsoft.com/fwlink/?LinkID=60402). If you are working with a non-Microsoft virtualization product, be sure to consult the documentation of the vendor for that product.  
  
<<<<<<< HEAD
-   To configure the Windows Time service on a domain controller that is running in a virtual machine, it is recommended that you partially disable time synchronization between the host system and guest operating system acting as a domain controller. This enables your guest domain controller to synchronize time for the domain hierarchy, but protects it from having a time skew if it is restored from a Saved state. For more information, see Microsoft Knowledge Base article 976924, [You receive Windows Time Service event IDs 24, 29, and 38 on a virtualized domain controller that is running on a Windows Server 2008-based host server with Hyper-V](http://go.microsoft.com/fwlink/?LinkID=192236) (http://go.microsoft.com/fwlink/?LinkID=192236) and [Deployment Considerations for Virtualized Domain Controllers](http://go.microsoft.com/fwlink/?LinkID=192235) (http://go.microsoft.com/fwlink/?LinkID=192235).  
=======
-   To configure the Windows Time service on a domain controller that is running in a virtual machine, it is recommended that you partially disable time synchronization between the host system and guest operating system acting as a domain controller. This enables your guest domain controller to synchronize time for the domain hierarchy, but protects it from having a time skew if it is restored from a Saved state. For more information, see Microsoft Knowledge Base article 976924, [You receive Windows Time Service event IDs 24, 29, and 38 on a virtualized domain controller that is running on a Windows Server 2008�based host server with Hyper-V](http://go.microsoft.com/fwlink/?LinkID=192236) (http://go.microsoft.com/fwlink/?LinkID=192236) and [Deployment Considerations for Virtualized Domain Controllers](http://go.microsoft.com/fwlink/?LinkID=192235) (http://go.microsoft.com/fwlink/?LinkID=192235).  
>>>>>>> 9aa2dce86f802cd3079157fffcd57e0fc313c401
  
-   To configure the Windows Time service on a domain controller acting as the forest root PDC emulator that is also running in a virtual computer, follow the same instructions for a physical computer as described in [Configure the Windows Time service on the PDC emulator in the Forest Root Domain](http://go.microsoft.com/fwlink/?LinkId=91969) (http://go.microsoft.com/fwlink/?LinkId=91969).  
  
-   To configure the Windows Time service on a member server running as a virtual computer, use the domain time hierarchy as described in ([Configure a client computer for automatic domain time synchronization](http://go.microsoft.com/fwlink/?LinkId=91376) (http://go.microsoft.com/fwlink/?LinkId=91376).  
  
## <a name="BKMK_WTS"></a>What is the Windows Time Service?  
The Windows Time service (W32Time) provides network clock synchronization for computers without the need for extensive configuration.  
  
The Windows Time service is essential to the successful operation of Kerberos version 5 authentication and, therefore, to AD DS-based authentication. Any Kerberos-aware application, including most security services, relies on time synchronization between the computers that are participating in the authentication request. AD DS domain controllers must also have synchronized clocks to help to ensure accurate data replication.  
  
The Windows Time service is implemented in a dynamic link library called W32Time.dll. W32Time.dll is installed by default in the **%Systemroot%\System32** folder during operating system setup and installation.  
  
W32Time.dll was originally developed for Windows 2000 Server to support a specification by the Kerberos V5 authentication protocol that required clocks on a network to be synchronized. Starting with Windows Server 2003, W32Time.dll provided increased accuracy in network clock synchronization over the Windows 2000 Server operating system and, in addition, supported a variety of hardware devices and network time protocols by means of time providers. Although originally designed to provide clock synchronization for Kerberos authentication, many current applications use timestamps to ensure transactional consistency, to record the time of important events, and other business-critical, time-sensitive information. These applications benefit from time synchronization between computers that is provided by the Windows Time service.  
  
## <a name="BKMK_TimeProtocols"></a>Importance of Time Protocols  
Time protocols communicate between two computers to exchange time information and then use that information to synchronize their clocks. With the Windows Time service time protocol, a client requests time information from a server and synchronizes its clock based on the information that is received.  
  
The Windows Time service uses NTP to help synchronize time across a network. NTP is an Internet time protocol that includes the discipline algorithms necessary for synchronizing clocks. NTP is a more accurate time protocol than the Simple Network Time Protocol (SNTP) that is used in some versions of Windows; however, W32Time continues to support SNTP to enable backward compatibility with computers running SNTP-based time services such as Windows 2000.  
  
## See Also  
[How the Windows Time Service Works](How-the-Windows-Time-Service-Works.md)  
[Windows Time Service Tools and Settings](Windows-Time-Service-Tools-and-Settings.md)  
[Microsoft Knowledge Base article 902229](http://go.microsoft.com/fwlink/?LinkId=186066)  
[Videos about the Windows Time Service](http://go.microsoft.com/fwlink/?LinkID=197277)  
  


