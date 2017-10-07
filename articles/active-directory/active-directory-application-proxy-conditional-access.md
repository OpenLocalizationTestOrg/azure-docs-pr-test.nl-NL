---
title: aaaConditional toegang tooon-premises apps - Azure AD | Microsoft Docs
description: Bevat informatie over hoe tooset van voorwaardelijke toegang voor toepassingen u publiceren toobe toegankelijk is op afstand met Azure AD-toepassingsproxy.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 2e97722b-eb4e-4078-b607-9fed210d8a0f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 7bed25dd4ba17941e77d8c4b2b9ba4edcf0cf597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-conditional-access-in-azure-ad-application-proxy"></a>Werken met voorwaardelijke toegang in Azure AD-toepassingsproxy

>[!NOTE]
>In dit artikel is van toepassing toohello klassieke Azure-portal, die wordt buiten gebruik gesteld. Het is raadzaam dat u Hallo [Azure-portal](https://portal.azure.com). In hello Azure-portal Hallo toepassingsproxy apps hebben dezelfde functies voor voorwaardelijke toegang als andere SaaS-app. toolearn meer informatie over voorwaardelijke toegang, Zie [aan de slag met voorwaardelijke toegang in Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).

U kunt de toegang configureren regels toogrant voorwaardelijke toegang tooapplications gepubliceerd met toepassingsproxy. Hiermee kunt u:

* Meervoudige authenticatie per toepassing
* Meervoudige verificatie vereisen alleen wanneer gebruikers zich niet op het werk
* Gebruikers toegang tot de toepassing hello wanneer ze niet op het werk blokkeren

Deze regels kunnen worden toegepast tooall gebruikers en groepen of alleen toospecific gebruikers en groepen. Hallo-regel wordt standaard tooall gebruikers die toegang toohello toepassing hebt toegepast. Hallo regel kan echter ook worden beperkt toousers die lid van de opgegeven beveiligingsgroepen zijn.  

Toegangsregels worden geëvalueerd wanneer een gebruiker een federatieve toepassing die gebruikmaakt van OAuth 2.0, OpenID Connect, SAML of WS-Federation. Toegangsregels worden bovendien met OAuth 2.0 en OpenID Connect geëvalueerd wanneer een vernieuwingstoken gebruikte tooacquire een toegangstoken.

## <a name="conditional-access-prerequisites"></a>Vereisten voor voorwaardelijke toegang
* Abonnement tooAzure Active Directory Premium
* Een federatieve of beheerde Azure Active Directory-tenant
* Federatieve tenants is vereist voor multi-factor authentication (MFA)  
    ![Toegangsregels configureren - meervoudige authenticatie](./media/active-directory-application-proxy-conditional-access/application-proxy-conditional-access.png)

## <a name="configure-per-application-multi-factor-authentication"></a>Per toepassing multi-factor authentication configureren
1. Meld u aan als beheerder aan in Hallo klassieke Azure-portal.
2. Ga tooActive Directory en Hallo directory waarin u toepassingsproxy tooenable wilt selecteren.
3. Klik op **toepassingen** en schuif omlaag toohello **toegangsregels** sectie. Hallo toegang regels sectie wordt alleen weergegeven voor toepassingen die worden gepubliceerd met toepassingsproxy die gebruikmaken van federatieve verificatie.
4. Hallo regel inschakelen door het selecteren **toegangsregels inschakelen** te**op**.
5. Geef Hallo gebruikers en groepen toowhom Hallo regels zijn van toepassing. Gebruik Hallo **groep toevoegen** knop tooselect een of meer groepen toowhich Hallo toegangsregel van toepassing is. Dit dialoogvenster kan ook worden gebruikt tooremove geselecteerde groepen.  Wanneer regels Hallo geselecteerde tooapply toogroups, Hallo toegangsregels worden afgedwongen alleen voor gebruikers die deel uitmaken van tooone Hallo opgegeven beveiligingsgroepen.  

   * Controleer tooexplicitly uitsluiten beveiligingsgroepen van Hallo-regel **behalve** en geef een of meer groepen. Gebruikers die lid van een groep in Hallo behalve lijst zijn zijn niet vereist tooperform multi-factor authentication-server.  
   * Als een gebruiker is geconfigureerd met de Hallo per gebruiker multi-factor authentication-Server-functie, heeft deze instelling voorrang op Hallo autorisatieregels multi-factor authentication-server. Een gebruiker die is geconfigureerd voor de per gebruiker multi-factor authentication-server is vereist tooperform multi-factor authentication-server, zelfs als ze van de toepassing hello multi-factorauthenticatie regels zijn uitgesloten. Meer informatie over [meervoudige verificatie en per gebruiker instellingen](../multi-factor-authentication/multi-factor-authentication.md).
6. Selecteer Hallo toegangsregel gewenste tooset:

   * **Meervoudige authenticatie**: gebruikers toowhom toegangsregels van toepassing zijn vereist toocomplete multi-factor authentication-server voordat toegang tot Hallo toepassing toowhich Hallo-regel van toepassing is.
   * **Meervoudige authenticatie niet op het werk**: gebruikers die toegang proberen tooaccess Hallo toepassing van een vertrouwde IP-adres worden niet vereist tooperform multi-factor authentication-server. Hallo vertrouwd IP-adresbereiken kunnen worden geconfigureerd op de pagina Hallo meerledige verificatie-instellingen.
   * **Blokkeert de toegang niet op het werk**: gebruikers die toegang proberen tooaccess Hallo toepassing van buiten uw bedrijfsnetwerk kunt tooaccess Hallo toepassing niet worden.

## <a name="configuring-mfa-for-federation-services"></a>Configureren van MFA voor federatieservices
Voor federatieve tenants multi-factor authentication (MFA) kan worden uitgevoerd met Azure Active Directory of Hallo lokale AD FS-server. MFA wordt standaard op elke pagina die wordt gehost door Azure Active Directory. tooconfigure MFA on-premises Windows PowerShell en gebruik Hallo – SupportsMFA eigenschap tooset hello Azure AD-module worden uitgevoerd.

Hallo volgende voorbeeld laat zien hoe tooenable on-premises MFA door met behulp van Hallo [cmdlet Set-MsolDomainFederationSettings](https://msdn.microsoft.com/library/azure/dn194088.aspx) op Hallo contoso.com tenant:`Set-MsolDomainFederationSettings -DomainName contoso.com -SupportsMFA $true `

In aanvulling toosetting deze vlag Hallo federatieve AD FS-tenant-exemplaar moet tooperform multi-factor authentication-server geconfigureerd. Volg de instructies Hallo voor [implementeren van Microsoft Azure multi-factor authentication-server op de lokale](../multi-factor-authentication/multi-factor-authentication-get-started-server.md).

## <a name="see-also"></a>Zie ook
* [Werken met claim-compatibele toepassingen](active-directory-application-proxy-claims-aware-apps.md)
* [Publiceren van toepassingen met toepassingsproxy](active-directory-application-proxy-publish.md)
* [Eenmalige aanmelding inschakelen](active-directory-application-proxy-sso-using-kcd.md)
* [Toepassingen publiceren met uw eigen domeinnaam](active-directory-application-proxy-custom-domains.md)

Bekijk voor Hallo laatste nieuws en updates Hallo [blog over toepassingsproxy](http://blogs.technet.com/b/applicationproxyblog/)
