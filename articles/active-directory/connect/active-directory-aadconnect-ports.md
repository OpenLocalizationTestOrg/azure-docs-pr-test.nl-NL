---
title: Hybride identiteit nodig poorten en protocollen - Azure | Microsoft Docs
description: Deze pagina is een pagina met technische naslaginformatie voor poorten die vereist toobe open voor Azure AD Connect zijn
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: de97b225-ae06-4afc-b2ef-a72a3643255b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: 9c62b74b45e7f266e3a55baa2db07a9ff1c9c6aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-identity-required-ports-and-protocols"></a>Voor hybride identiteit benodigde poorten en protocollen
Hallo volgende document is technische naslaginformatie over Hallo nodig poorten en protocollen voor het implementeren van een hybride identiteitsoplossing. Gebruik Hallo afbeelding te volgen en toohello overeenkomstige tabel verwijzen.

![Wat is Azure AD Connect?](./media/active-directory-aadconnect-ports/required3.png)

## <a name="table-1---azure-ad-connect-and-on-premises-ad"></a>Tabel 1 - Azure AD Connect en On-premises AD
Deze tabel wordt beschreven Hallo poorten en protocollen die vereist voor communicatie tussen hello Azure AD Connect-server zijn en on-premises AD.

| Protocol | Poorten | Beschrijving |
| --- | --- | --- |
| DNS |53 (TCP/UDP) |DNS-zoekacties op Hallo doelforest. |
| Kerberos |88 (TCP/UDP) |Kerberos-verificatie toohello AD-forest. |
| MS-RPC |135 (TCP/UDP) |Gebruikt tijdens de eerste configuratie van de Hallo van hello Azure AD Connect-wizard wanneer deze verbinding heeft toohello AD-forest en tijdens de synchronisatie van wachtwoorden. |
| LDAP |389 (TCP/UDP) |Gebruikt voor het importeren van gegevens uit Active Directory. Gegevens worden versleuteld met Kerberos-teken & zegel. |
| RPC | 445 (TCP/UDP) |Gebruikt door naadloze eenmalige aanmelding toocreate een computeraccount in Hallo AD-forest. |
| LDAP/SSL |636 (TCP/UDP) |Gebruikt voor het importeren van gegevens uit Active Directory. Hallo-gegevensoverdracht is ondertekend en versleuteld. Alleen gebruikt als u SSL gebruikt. |
| RPC |49152 en 65535 (willekeurige hoge RPC Port)(TCP/UDP) |Gebruikt tijdens de eerste configuratie Hallo van Azure AD Connect wanneer deze verbinding heeft toohello AD-forests en tijdens de synchronisatie van wachtwoorden. Zie [KB929851](https://support.microsoft.com/kb/929851), [KB832017](https://support.microsoft.com/kb/832017), en [KB224196](https://support.microsoft.com/kb/224196) voor meer informatie. |

## <a name="table-2---azure-ad-connect-and-azure-ad"></a>Tabel 2 - Azure AD Connect en Azure AD
Deze tabel worden beschreven Hallo poorten en protocollen die vereist voor communicatie tussen hello Azure AD Connect-server en Azure AD zijn.

| Protocol | Poorten | Beschrijving |
| --- | --- | --- |
| HTTP |80 (TCP/UDP) |Toodownload CRL's (Certificate Revocation List) tooverify SSL-certificaten gebruikt. |
| HTTPS |443(TCP/UDP) |Gebruikte toosynchronize met Azure AD. |

Voor een lijst met URL's en IP-adressen die u nodig hebt tooopen in uw firewall Zie [Office 365-URL's en IP-adresbereiken](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).

## <a name="table-3---azure-ad-connect-and-ad-fs-federation-serverswap"></a>Tabel 3 - Azure AD Connect en AD FS Federation Servers/WAP
Deze tabel worden beschreven Hallo poorten en protocollen die vereist voor communicatie tussen hello Azure AD Connect-server en AD FS Federation/WAP-servers zijn.  

| Protocol | Poorten | Beschrijving |
| --- | --- | --- |
| HTTP |80 (TCP/UDP) |Toodownload CRL's (Certificate Revocation List) tooverify SSL-certificaten gebruikt. |
| HTTPS |443(TCP/UDP) |Gebruikte toosynchronize met Azure AD. |
| WinRM |5985 |WinRM-Listener |

## <a name="table-4---wap-and-federation-servers"></a>Tabel 4 - WAP en federatieservers
Deze tabel worden beschreven Hallo poorten en protocollen die vereist voor communicatie tussen federatieservers Hallo en WAP-servers zijn.

| Protocol | Poorten | Beschrijving |
| --- | --- | --- |
| HTTPS |443(TCP/UDP) |Gebruikt voor verificatie. |

## <a name="table-5---wap-and-users"></a>Tabel 5 - WAP en gebruikers
Deze tabel worden beschreven Hallo poorten en protocollen die vereist voor communicatie tussen gebruikers en Hallo WAP-servers zijn.

| Protocol | Poorten | Beschrijving |
| --- | --- | --- |
| HTTPS |443(TCP/UDP) |Gebruikt voor verificatie van apparaten. |
| TCP |49443 (TCP) |Gebruikt voor verificatie via certificaat. |

## <a name="table-6a--6b---pass-through-authentication-with-single-sign-on-sso-and-password-hash-sync-with-single-sign-on-sso"></a>Tabel 6a & 6 ter - Pass through-verificatie met eenmalige aanmelding (SSO) en Wachtwoordhashsynchronisatie met eenmalige aanmelding (SSO)
Hallo volgende tabellen worden beschreven Hallo poorten en protocollen die vereist voor communicatie tussen hello Azure AD Connect en Azure AD zijn.

### <a name="table-6a---pass-through-authentication-with-sso"></a>Tabel 6a - Pass through-verificatie met eenmalige aanmelding
|Protocol|Poortnummer|Beschrijving
| --- | --- | ---
|HTTP|80|Uitgaande HTTP-verkeer voor beveiligingsvalidatie zoals SSL inschakelen. Ook die nodig zijn voor de connector Hallo automatisch bijgewerkt mogelijkheid toofunction goed.
|HTTPS|443| Uitgaande HTTPS-verkeer voor bewerkingen zoals het inschakelen en uitschakelen van de functie hello, registreren connectors connector updates worden gedownload en alle gebruiker aanmelden aanvragen voor de verwerking inschakelen.

Azure AD Connect moet bovendien toobe kunnen toomake direct IP-verbindingen toohello [Azure datacentrum IP-adresbereiken](https://www.microsoft.com/en-us/download/details.aspx?id=41653).

### <a name="table-6b---password-hash-sync-with-sso"></a>Tabel 6 ter - Wachtwoordhashsynchronisatie met eenmalige aanmelding

|Protocol|Poortnummer|Beschrijving
| --- | --- | ---
|HTTPS|443| Registratie van eenmalige aanmelding (alleen vereist voor Hallo registratieproces SSO) inschakelen.

Azure AD Connect moet bovendien toobe kunnen toomake direct IP-verbindingen toohello [Azure datacentrum IP-adresbereiken](https://www.microsoft.com/en-us/download/details.aspx?id=41653). Opnieuw, dit is alleen vereist voor Hallo SSO registratieproces.

## <a name="table-7a--7b---azure-ad-connect-health-agent-for-ad-fssync-and-azure-ad"></a>Tabel 7 a & 7 ter - Azure AD Connect Health-agent voor (AD FS/Sync) en Azure AD
Hallo volgende tabellen worden beschreven Hallo eindpunten, poorten en protocollen die vereist voor communicatie tussen Azure AD Connect Health-agents en Azure AD zijn

### <a name="table-7a---ports-and-protocols-for-azure-ad-connect-health-agent-for-ad-fssync-and-azure-ad"></a>Tabel 7 - poorten en protocollen voor Azure AD Connect Health-agent voor (AD FS/Sync) en Azure AD
Deze tabel wordt beschreven Hallo uitgaande poorten en protocollen die vereist voor communicatie tussen hello Azure AD Connect Health-agents en Azure AD zijn te volgen.  

| Protocol | Poorten | Beschrijving |
| --- | --- | --- |
| HTTPS |443(TCP/UDP) |Uitgaand |
| Azure Service Bus |5671 (TCP/UDP) |Uitgaand |

### <a name="7b---endpoints-for-azure-ad-connect-health-agent-for-ad-fssync-and-azure-ad"></a>7 ter - eindpunten voor Azure AD Connect Health-agent voor (AD FS/Sync) en Azure AD
Zie voor een lijst met eindpunten [gedeelte van de vereisten voor hello Azure AD Connect Health agent Hallo](../connect-health/active-directory-aadconnect-health-agent-install.md#requirements).

