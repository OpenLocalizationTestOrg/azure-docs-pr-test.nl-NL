---
title: aaaAzure voorwaardelijke toegang voor SaaS-Apps | Microsoft Docs
description: 'Voorwaardelijke toegang in Azure AD kunt u tooconfigure per toepassing meerledige verificatie toegangsregels en Hallo mogelijkheid tooblock toegang voor gebruikers niet op een vertrouwd netwerk. '
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
ms.openlocfilehash: 69748014c0c8e266ba66562980c784aba4c68d80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-active-directory-conditional-access"></a>Aan de slag met Azure Active Directory voorwaardelijke toegang
Azure Active Directory voorwaardelijke toegang voor [SaaS](https://azure.microsoft.com/overview/what-is-saas/) apps en Azure AD verbonden apps kunt u voorwaardelijke toegang op basis van de groep, de locatie en de gevoeligheid van de toepassing configureren. 

Met voorwaardelijke toegang op basis van de gevoeligheid van toepassing, kunt u regels voor multi-factor authentication (MFA) toegang per toepassing instellen. MFA per toepassing biedt Hallo mogelijkheid tooblock toegang voor gebruikers die zich niet op een vertrouwd netwerk. U kunt MFA regels tooall gebruikers die zijn toegewezen toohello toepassing, of alleen voor gebruikers binnen de opgegeven beveiligingsgroepen kunt toepassen.  Gebruikers kunnen worden uitgesloten van MFA-vereiste Hallo als ze Hallo toepassing van een IP-adres in van de organisatie Hallo-netwerk.

Deze mogelijkheden zijn beschikbaar toocustomers die een Azure Active Directory Premium-licentie hebt aangeschaft.

## <a name="scenario-prerequisites"></a>Scenario-vereisten
* Licentie voor Azure Active Directory Premium
* Federatieve of beheerde Azure Active Directory-tenant
* Federatieve tenants vereisen meervoudige verificatie worden ingeschakeld.

## <a name="configure-per-application-access-rules"></a>Configureer regels voor toegang per toepassing
Deze sectie wordt beschreven hoe tooconfigure per toepassing toegang tot regels.

1. Meld u aan toohello klassieke Azure-portal met behulp van een account dat een hoofdbeheerder voor Azure AD.
2. Selecteer in het linkerdeelvenster Hallo **Active Directory**.
3. Tabblad Hallo-map, selecteer uw directory.
4. Selecteer Hallo **toepassingen** tabblad.
5. Selecteer Hallo-toepassing die Hallo regel worden ingesteld voor.
6. Selecteer Hallo **configureren** tabblad.
7. Schuif naar beneden toohello toegang regels sectie. Selecteer de gewenste toegangsregel Hallo.
8. Geef gebruikers met Hallo Hallo regel van toepassing.
9. Hallo-beleid inschakelen door het selecteren **toobe ingeschakeld op**.

## <a name="understanding-access-rules"></a>Understanding toegangsregels
Deze sectie geeft een gedetailleerde beschrijving van de toegangsregels hello wordt ondersteund in hello Azure voorwaardelijke toegang tot toepassingen.

### <a name="specifying-hello-users-hello-access-rules-apply-to"></a>Geven Hallo gebruikers Hallo toegang regels van toepassing op
Standaard Hallo beleid van toepassing tooall-gebruikers die toegang toohello toepassing hebben. Echter, u kunt ook beperken Hallo beleid toousers die lid van Hallo opgegeven zijn beveiligingsgroepen. Hallo **groep toevoegen** knop is gebruikte tooselect een of meer groepen van dialoogvenster voor Groepselectie Hallo die Hallo toegangsregel van toepassing op. Dit dialoogvenster kan ook worden gebruikt tooremove geselecteerde groepen. Wanneer regels Hallo geselecteerde tooapply tooGroups, Hallo toegangsregels alleen worden afgedwongen voor gebruikers die deel uitmaken van tooone Hallo opgegeven beveiligingsgroepen.

Beveiligingsgroepen kunnen ook worden expliciet uitgesloten van Hallo beleid door het selecteren van Hallo **behalve** optie en een of meer groepen op te geven. Gebruikers die lid van een groep in Hallo zijn **behalve** lijst niet meer worden onderwerp toohello meerledige verificatie vereist, zelfs als ze lid zijn van een groep die Hallo toegangsregel van toepassing op.
Hallo toegangsregel hieronder wordt alle gebruikers in Hallo Managers groep toouse meervoudige verificatie vereisen wanneer toegang tot de toepassing hello.

![Instellen van regels voor voorwaardelijke toegang met MFA](./media/active-directory-conditional-access-azuread-connected-apps/conditionalaccess-saas-apps.png)

## <a name="conditional-access-rules-with-mfa"></a>Regels voor voorwaardelijke toegang met MFA
Als een gebruiker is geconfigureerd met de Hallo per gebruiker multi-factor authentication-Server-functie, wordt deze instelling op Hallo gebruiker combineren met Hallo multi-factorauthenticatie regels van Hallo-app. Dit betekent een gebruiker die is geconfigureerd voor de per gebruiker multi-factor authentication-server vereist tooperform multi-factorauthenticatie zelfs als ze zijn vrijgesteld van autorisatieregels Hallo multi-factor authentication-server. Meer informatie over instellingen voor meervoudige verificatie en per gebruiker.

### <a name="access-rule-options"></a>Opties voor toegang tot de regel
Hallo volgende opties worden ondersteund:

* **Meervoudige authenticatie**: Hallo gebruikers toowhom Hallo toegangsregels van toepassing op, kunnen vereist toocomplete multi-factor authentication-server voordat toegang tot Hallo-toepassing die Hallo beleid van toepassing op.
* **Meervoudige authenticatie niet op het werk**: een gebruiker die afkomstig is van een vertrouwde IP-adres worden niet vereist tooperform multi-factor authentication-server. Hallo vertrouwd IP-adresbereiken kunnen worden geconfigureerd op de pagina Hallo meerledige verificatie-instellingen.
* **Blokkeert de toegang niet op het werk**: een gebruiker die niet afkomstig is van een vertrouwde IP-adres wordt geblokkeerd. Hallo vertrouwd IP-adresbereiken kunnen worden geconfigureerd op de pagina Hallo meerledige verificatie-instellingen.

### <a name="setting-rule-status"></a>Regelstatus is ingesteld
Toegangsstatus van de regel kan het Hallo-regels in- of uitschakelen. Wanneer hello toegangsregels uitgeschakeld zijn, wordt Hallo MFA-vereiste niet afgedwongen.

### <a name="access-rule-evaluation"></a>Regeltoepassing toegang
Toegangsregels worden geëvalueerd wanneer een gebruiker een federatieve toepassing die gebruikmaakt van OAuth 2.0, OpenID Connect, SAML of WS-Federation. Toegangsregels worden bovendien geëvalueerd wanneer een vernieuwing token tooacquire een toegangstoken hello OAuth 2.0- en OpenID Connect. Als de evaluatie van het beleid mislukt als een vernieuwingstoken wordt gebruikt, Hallo fout **invalid_grant** wordt geretourneerd, wordt hiermee Hallo gebruiker moet toore-toohello-client te verifiëren.

### <a name="configure-federation-services-tooprovide-multi-factor-authentication"></a>Federation services tooprovide multi-factor authentication configureren
Voor federatieve tenants MFA mag worden uitgevoerd met Azure Active Directory of Hallo lokale AD FS-server.

MFA wordt standaard uitgevoerd op een pagina die wordt gehost door Azure Active Directory. tooconfigure MFA on-premises Hallo **– SupportsMFA** eigenschap te moet worden ingesteld**true** in Azure Active Directory, met behulp van hello Azure AD-module voor Windows PowerShell.

Hallo volgende voorbeeld laat zien hoe tooenable on-premises MFA door met behulp van Hallo [cmdlet Set-MsolDomainFederationSettings](https://msdn.microsoft.com/library/azure/dn194088.aspx) op Hallo contoso.com tenant:

    Set-MsolDomainFederationSettings -DomainName contoso.com -SupportsMFA $true

In aanvulling toosetting deze vlag Hallo federatieve AD FS-tenant-exemplaar moet tooperform multi-factor authentication-server geconfigureerd. Volg de instructies Hallo voor [implementeren van Azure multi-factor Authentication lokale](../multi-factor-authentication/multi-factor-authentication-get-started-server.md).

## <a name="related-articles"></a>Verwante artikelen
* [Toegang beveiligen tooOffice 365 en andere apps verbonden tooAzure Active Directory](active-directory-conditional-access.md)
* [Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)

