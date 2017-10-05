---
title: Azure voorwaardelijke toegang voor SaaS-Apps | Microsoft Docs
description: 'Voorwaardelijke toegang in Azure AD kunt u regels voor toegang per toepassing multi-factor authentication-server en de mogelijkheid om te blokkeren van toegang voor gebruikers niet op een vertrouwd netwerk configureren. '
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 51a1ee61-3ffe-4f65-b8de-ff21903e1e74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: efaa70467346e910a78a63d182041029bb34b1cc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="getting-started-with-azure-active-directory-conditional-access"></a>Aan de slag met Azure Active Directory voorwaardelijke toegang
Azure Active Directory voorwaardelijke toegang voor [SaaS](https://azure.microsoft.com/overview/what-is-saas/) apps en Azure AD verbonden apps kunt u voorwaardelijke toegang op basis van de groep, de locatie en de gevoeligheid van de toepassing configureren. 

Met voorwaardelijke toegang op basis van de gevoeligheid van toepassing, kunt u regels voor multi-factor authentication (MFA) toegang per toepassing instellen. MFA per toepassing biedt de mogelijkheid om te blokkeren van toegang voor gebruikers die zich niet op een vertrouwd netwerk. U kunt MFA regels toepassen op alle gebruikers die zijn toegewezen aan de toepassing of alleen voor gebruikers binnen de opgegeven beveiligingsgroepen.  Gebruikers kunnen worden uitgesloten van de MFA-vereiste als ze toegang hebben tot de toepassing van een IP-adres in het bedrijfsnetwerk.

Deze mogelijkheden zijn beschikbaar voor klanten die een Azure Active Directory Premium-licentie hebt aangeschaft.

## <a name="scenario-prerequisites"></a>Scenario-vereisten
* Licentie voor Azure Active Directory Premium
* Federatieve of beheerde Azure Active Directory-tenant
* Federatieve tenants vereisen meervoudige verificatie worden ingeschakeld.

## <a name="configure-per-application-access-rules"></a>Configureer regels voor toegang per toepassing
Deze sectie beschrijft het configureren van regels voor toegang per toepassing.

1. Aanmelden bij de klassieke Azure portal met behulp van een account dat een hoofdbeheerder voor Azure AD.
2. Selecteer in het linkerdeelvenster **Active Directory**.
3. Selecteer uw directory op het tabblad map.
4. Selecteer de **toepassingen** tabblad.
5. Selecteer de toepassing die de regel worden ingesteld voor.
6. Selecteer de tab **Configureren**.
7. Schuif omlaag naar de sectie toegang regels. Selecteer de gewenste toegangsregel.
8. Geef de gebruikers die de regel van toepassing.
9. Inschakelen van het beleid door het selecteren **ingeschakeld op**.

## <a name="understanding-access-rules"></a>Understanding toegangsregels
Deze sectie geeft een gedetailleerde beschrijving van de toegangsregels die worden ondersteund in de Azure voorwaardelijke toegang tot toepassingen.

### <a name="specifying-the-users-the-access-rules-apply-to"></a>Geven de gebruikers de regels voor toegang van toepassing op
Standaard wordt het beleid toepassen op alle gebruikers die toegang tot de toepassing hebben. U kunt echter ook het beleid voor gebruikers die lid van de opgegeven beveiligingsgroepen zijn beperken. De **groep toevoegen** knop wordt gebruikt om te selecteren van een of meer groepen in het groepsdialoogvenster waarop de toegangsregel van toepassing. Dit dialoogvenster kan ook worden gebruikt om te verwijderen van de geselecteerde groepen. Wanneer de regels toepassen op groepen zijn geselecteerd, wordt de toegangsregels alleen afgedwongen voor gebruikers die deel uitmaken van een van de opgegeven beveiligingsgroepen.

Beveiligingsgroepen kunnen ook worden expliciet uitgesloten van het beleid door het selecteren van de **behalve** optie en een of meer groepen op te geven. Gebruikers die lid zijn van een groep in de **behalve** lijst niet worden gebruikt voor de vereiste voor meervoudige verificatie, zelfs als ze lid zijn van een groep die de toegangsregel van toepassing op.
De toegangsregel die hieronder wordt weergegeven, moeten alle gebruikers in de groep beheerders meervoudige verificatie gebruiken bij het openen van de toepassing.

![Instellen van regels voor voorwaardelijke toegang met MFA](./media/active-directory-conditional-access-azuread-connected-apps/conditionalaccess-saas-apps.png)

## <a name="conditional-access-rules-with-mfa"></a>Regels voor voorwaardelijke toegang met MFA
Als een gebruiker is geconfigureerd met de functie van de multi-factor authentication-server per gebruiker, wordt deze instelling op de gebruiker wordt gecombineerd met de regels van de multi-factor authentication-server van de app. Dit betekent dat een gebruiker die is geconfigureerd voor de per gebruiker multi-factor authentication-server moet aan de multi-factor authentication uitvoeren, zelfs als ze de multi-factor authentication-server-regels van toepassing zijn uitgesloten. Meer informatie over instellingen voor meervoudige verificatie en per gebruiker.

### <a name="access-rule-options"></a>Opties voor toegang tot de regel
De volgende opties worden ondersteund:

* **Meervoudige authenticatie**: de gebruikers aan wie de toegangsregels van toepassing op, moeten volledige multi-factor authentication-server voordat de toegang tot de toepassing die het beleid van toepassing.
* **Meervoudige authenticatie niet op het werk**: een gebruiker die afkomstig is van een vertrouwde IP-adres niet moeten worden multi-factor authentication uitvoeren. De vertrouwde IP-adresbereiken kunnen worden geconfigureerd op de pagina voor meervoudige verificatie-instellingen.
* **Blokkeert de toegang niet op het werk**: een gebruiker die niet afkomstig is van een vertrouwde IP-adres wordt geblokkeerd. De vertrouwde IP-adresbereiken kunnen worden geconfigureerd op de pagina voor meervoudige verificatie-instellingen.

### <a name="setting-rule-status"></a>Regelstatus is ingesteld
Toegangsstatus van de regel kan de regels in of uit te schakelen. Wanneer de toegangsregels uitgeschakeld zijn, worden de vereiste voor meervoudige verificatie wordt niet afgedwongen.

### <a name="access-rule-evaluation"></a>Regeltoepassing toegang
Toegangsregels worden geëvalueerd wanneer een gebruiker een federatieve toepassing die gebruikmaakt van OAuth 2.0, OpenID Connect, SAML of WS-Federation. Toegangsregels worden bovendien geëvalueerd wanneer de OAuth 2.0 en OpenID Connect een vernieuwingstoken dat is gebruikt om toegang te verkrijgen van een toegangstoken. Als de evaluatie van het beleid mislukt als een vernieuwingstoken wordt gebruikt, de fout **invalid_grant** wordt geretourneerd, wordt hiermee de gebruiker moet opnieuw worden geverifieerd aan de client.

### <a name="configure-federation-services-to-provide-multi-factor-authentication"></a>Federatieservices om multi-factorauthenticatie configureren
Voor federatieve tenants MFA mag worden uitgevoerd met Azure Active Directory of met de on-premises AD FS-server.

MFA wordt standaard uitgevoerd op een pagina die wordt gehost door Azure Active Directory. Voor het configureren van MFA on-premises de **– SupportsMFA** eigenschap moet worden ingesteld op **true** in Azure Active Directory, met behulp van de Azure AD-module voor Windows PowerShell.

Het volgende voorbeeld laat zien hoe lokale MFA inschakelen via de [cmdlet Set-MsolDomainFederationSettings](https://msdn.microsoft.com/library/azure/dn194088.aspx) op de tenant contoso.com:

    Set-MsolDomainFederationSettings -DomainName contoso.com -SupportsMFA $true

Naast deze vlag instelt, moet het federatieve tenant AD FS-exemplaar worden geconfigureerd voor multi-factor authentication uitvoeren. Volg de instructies voor [implementeren van Azure multi-factor Authentication lokale](../multi-factor-authentication/multi-factor-authentication-get-started-server.md).

## <a name="related-articles"></a>Verwante artikelen
* [Beveiligen van toegang tot Office 365 en andere apps die zijn verbonden met Azure Active Directory](active-directory-conditional-access.md)
* [Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)

