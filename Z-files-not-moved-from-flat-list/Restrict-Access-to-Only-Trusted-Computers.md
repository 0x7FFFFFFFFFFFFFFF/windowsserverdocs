---
title: Restrict Access to Only Trusted Computers
ms.custom: na
ms.prod: windows-server-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - techgroup-networking
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4fe8fdce-5c8d-4984-914b-36e193f4b5b6
---
# Restrict Access to Only Trusted Computers
Your organizational network likely has a connection to the Internet. You also likely have partners, vendors, or contractors who attach computers that are not owned by your organization to your network. Because you do not manage those computers, you cannot trust them to be free of malicious software, maintained with the latest security updates, or in any way in compliance with your organization's security policies. These untrustworthy computers both on and outside of your physical network must not be permitted to access your organization's computers except where it is truly required.

To mitigate this risk, you must be able to isolate the computers you trust, and restrict their ability to receive unsolicited network traffic from untrusted computers. By using connection security and firewall rules available in [!INCLUDE[wfas](includes/wfas_md.md)], you can logically isolate the computers that you trust by requiring that all unsolicited inbound network traffic be authenticated. Authentication ensures that each computer or user can positively identify itself by using credentials that are trusted by the other computer. Connection security rules can be configured to use IPsec with the Kerberos V5 protocol available in Active Directory, or certificates issued by a trusted certification authority as the authentication method.

> [!NOTE]
> Because the primary authentication method recommended for computers that are running Windows is to use the Kerberos V5 protocol with membership in an Active Directory domain, this guide refers to this logical separation of computers as *domain isolation*, even when certificates are used to extend the protection to computers that are not part of an Active Directory domain.

The protection provided by domain isolation can help you comply with regulatory and legislative requirements, such as those found in the Federal Information Security Management Act of 2002 \(FISMA\), the Sarbanes\-Oxley Act of 2002, the Health Insurance Portability and Accountability Act of 1996 \(HIPAA\), and other government and industry regulations.

The following illustration shows an isolated domain, with one of the zones that are optionally part of the design. The rules that implement both the isolated domain and the different zones are deployed by using Group Policy and Active Directory.

![](media/WFAS-DomainIso.gif)

These goals, which correspond to [Domain Isolation Policy Design](https://technet.microsoft.com/library/cc725818(v=ws.10).aspx) and [Certificate\-based Isolation Policy Design](https://technet.microsoft.com/library/cc731463(v=ws.10).aspx), provide the following benefits:

-   Computers in the isolated domain accept unsolicited inbound network traffic only when it can be authenticated as coming from another computer in the isolated domain. Exemption rules can be defined to allow inbound traffic from trusted computers that for some reason cannot perform IPsec authentication.

    For example, Woodgrove Bank wants all of its computers to block all unsolicited inbound network traffic from any computer that it does not manage. The connection security rules deployed to domain member computers require authentication as a domain member or by using a certificate before an unsolicited inbound network packet is accepted.

-   Computers in the isolated domain can still send outbound network traffic to untrusted computers and receive the responses to the outbound requests.

    For example, Woodgrove Bank wants its users at client computers to be able to access Web sites on the Internet. The default [!INCLUDE[wfas](includes/wfas_md.md)] settings for outbound network traffic allow this. No additional rules are required.

These goals also support optional zones that can be created to add customized protection to meet the needs of subsets of an organization's computers:

-   Computers in the "boundary zone" are configured to use connection security rules that request but do not require authentication. This enables them to receive unsolicited inbound network traffic from untrusted computers, and also to receive traffic from the other members of the isolated domain.

    For example, Woodgrove Bank has a server that must be accessed by its partners' computers through the Internet. The rules applied to computers in the boundary zone use authentication when the client computer can support it, but do not block the connection if the client computer cannot authenticate.

-   Computers in the "encryption zone" require that all network traffic in and out must be encrypted to secure potentially sensitive material when it is sent over the network.

    For example, Woodgrove Bank wants the computers running SQL Server to only transmit data that is encrypted to help protect the sensitive data stored on those computers.

The following components are required for this deployment goal:

-   **Active Directory**: Active Directory supports centralized management of connection security rules by configuring the rules in one or more GPOs that can be automatically applied to all relevant computers in the domain. For more information about Active Directory, see [Additional Resources \[lhs\]](https://technet.microsoft.com/library/cc730668(v=ws.10).aspx).

**Next:**[Require Encryption When Accessing Sensitive Network Resources](https://technet.microsoft.com/library/cc770865(v=ws.10).aspx)


