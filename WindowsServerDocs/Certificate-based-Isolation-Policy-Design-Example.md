---
title: Certificate-based Isolation Policy Design Example
ms.custom: na
ms.prod: windows-server-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - techgroup-networking
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 80160e43-0b9d-408e-aa83-bd3672b712b1
---
# Certificate-based Isolation Policy Design Example
This design example continues to use the fictitious company Woodgrove Bank, as described in the sections [Firewall Policy Design Example](Firewall-Policy-Design-Example.md), [Domain Isolation Policy Design Example](Domain-Isolation-Policy-Design-Example.md), and [Server Isolation Policy Design Example](Server-Isolation-Policy-Design-Example.md).

One of the servers that must be included in the domain isolation environment is a computer running UNIX that supplies other information to the WGBank dashboard program running on the client computers. This computer sends updated information to the WGBank front\-end servers as it becomes available, so it is considered unsolicited inbound traffic to the computers that receive this information.

## Design requirements
One possible solution to this is to include an authentication exemption rule in the GPO applied to the WGBank front\-end servers. This rule would instruct the front\-end servers to accept traffic from the non\-Windows computer even though it cannot authenticate.

A more secure solution, and the one selected by Woodgrove Bank, is to include the non\-Windows computer in the domain isolation design. Because it cannot join an Active Directory domain, Woodgrove Bank chose to use certificate\-based authentication. Certificates are cryptographically\-protected documents, encrypted in such a way that their origin can be positively confirmed.

In this case, Woodgrove Bank used Microsoft Certificate Services, included with [!INCLUDE[nextref_longhorn](includes/nextref_longhorn_md.md)], to create the appropriate certificate. They might also have acquired and installed a certificate from a third\-party commercial certification authority. They then used Group Policy to deploy the certificate to the front\-end servers. The GPOs applied to the front\-end servers also include updated connection security rules that permit certificate\-based authentication in addition to Kerberos V5 authentication. They then manually installed the certificate on the UNIX server.

The UNIX server is configured with firewall and IPsec connection security rules using the tools that are provided by the operating system vendor. Those rules specify that authentication is performed by using the certificate.

The creation of the IPsec connection security rules for a non\-Windows computer is beyond the scope of this document, but support for a certificate that can be used to authenticate such a non\-Windows computer by using the standard IPsec protocols is the subject of this design.

The non\-Windows computer can be effectively made a member of the boundary zone or the encryption zone based on the IPsec rules applied to the computer. The only constraint is that the main mode and quick mode encryption algorithms supported by the UNIX computer must also be supported by the Windows\-based computers with which it communicates.

**Other traffic notes:**

-   None of the capabilities of the other designs discussed in this guide are compromised by the use of certificate authentication by a non\-Windows computer.

## Design details
Woodgrove Bank uses Active Directory groups and GPOs to deploy the domain isolation settings and rules to the computers in their organization.

The inclusion of one or more non\-Windows computers to the network requires only a simple addition to the GPOs for computers that must communicate with the non\-Windows computer. The addition is allowing certificate\-based authentication in addition to the Active Directory–supported Kerberos V5 authentication. This does not require including new rules, just adding certificate\-based authentication as an option to the existing rules.

When multiple authentication methods are available, two negotiating computers agree on the first one in their lists that match. Because the majority of the computers in Woodgrove Bank's network run Windows, Kerberos V5 is listed as the first authentication method in the rules. Certificate\-based authentication is added as an alternate authentication type.

By using the Active Directory Users and Computers snap\-in, Woodgrove Bank created a group named NAG\_COMPUTER\_WGBUNIX. They then added the computer accounts to this group for Windows computers that need to communicate with the non\-Windows computers. If all the computers in the isolated domain need to be able to access the non\-Windows computers, then the **Domain Computers** group can be added to the group as a member.

Woodgrove Bank then created a GPO that contains the certificate, and then attached security group filters to the GPO that allow read and apply permissions to only members of the NAG\_COMPUTER\_WGBUNIX group. The GPO places the certificate in the **Local Computer \/ Personal \/ Certificates** certificate store. The certificate used must chain back to a certificate that is in the **Trusted Root Certification Authorities** store on the local computer.

**Next:**[Designing a Windows Firewall with Advanced Security Strategy](Designing-a-Windows-Firewall-with-Advanced-Security-Strategy.md)


