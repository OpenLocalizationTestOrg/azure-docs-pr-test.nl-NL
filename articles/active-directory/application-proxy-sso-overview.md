---
title: aaaManage SSO voor Azure AD-toepassingsproxy | Microsoft Docs
description: Meer informatie over de basisprincipes Hallo van eenmalige aanmelding met toepassingsproxy
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: a278751a5cb1bf98c970a4e5d2eb3edc3b784096
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-ad-application-proxy-provide-single-sign-on"></a>Hoe biedt Azure AD-toepassingsproxy eenmalige aanmelding

Eenmalige aanmelding is een essentieel element van Azure AD-toepassingsproxy.  Het biedt de beste gebruikerservaring Hallo omdat uw gebruikers slechts toosign in Active Directory in de cloud Hallo tooAzure hebben. Nadat ze zich tooAzure Active Directory verifiëren, verwerkt Hallo Application Proxy connector Hallo verificatie toohello on-premises toepassing. Hallo back-end-toepassing kan niet zien Hallo verschil tussen een externe gebruiker aanmelden via toepassingsproxy en een reguliere gebruik op een apparaat voor het domein. 

toouse Azure Active Directory voor eenmalige aanmelding tooyour toepassingen, moet u tooselect **Azure Active Directory** als Hallo-methode voor verificatie vooraf. Als u selecteert **Passthrough** en vervolgens uw gebruikers tooAzure Active Directory niet helemaal niet worden geverifieerd, maar gerichte rechte toohello toepassing zijn. U kunt deze instelling kunt configureren wanneer u eerst een toepassing publiceren of navigeer tooyour toepassing hello Azure-portal en Hallo Application Proxy-instellingen bewerken. 

toosee uw opties voor eenmalige aanmelding als volgt te werk:

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Navigeer te**Azure Active Directory** > **bedrijfstoepassingen** > **alle toepassingen**.
3. Selecteer Hallo-app waarvan eenmalige aanmelding u opties wilt toomanage.
4. Selecteer **eenmalige aanmelding**.

   ![Het vervolgmenu van eenmalige aanmelding](./media/application-proxy-sso-overview/single-sign-on-mode.png)

Hallo vervolgkeuzemenu ziet u vijf opties voor eenmalige aanmelding tooyour toepassing:

* Azure AD eenmalige aanmelding uitgeschakeld
* Op basis van wachtwoorden eenmalige aanmelding
* Gekoppelde aanmelding
* Geïntegreerde Windows-verificatie
* Op basis van een koptekst eenmalige aanmelding

## <a name="azure-ad-single-sign-on-disabled"></a>Azure AD eenmalige aanmelding uitgeschakeld

Als u niet dat Azure Active Directory-integratie voor eenmalige aanmelding tooyour toepassing toouse wilt, kiest u **Azure AD eenmalige aanmelding uitgeschakeld**. Met deze optie selecteert, kunnen uw gebruikers tweemaal verifiëren. Eerst geverifieerd tooAzure Active Directory en vervolgens weer aanmelden toohello toepassing zelf. 

Deze optie is een goede keuze als uw on-premises toepassing geen gebruikers tooauthenticate vereist, maar u wilt tooadd Azure Active Directory gebruiken als een beveiligingslaag voor externe toegang. 

## <a name="password-based-sign-on"></a>Op basis van wachtwoorden eenmalige aanmelding

Als u toouse Azure Active Directory als de kluis van een wachtwoord voor uw on-premises toepassingen wilt, kiest u **op basis van wachtwoorden aanmelding**. Deze optie is een goede keuze als uw toepassing wordt geverifieerd met een gebruikersnaam en wachtwoord keuzelijst met invoervak in plaats van de toegangstokens of headers. Met op basis van wachtwoorden aanmelding moeten uw gebruikers toosign in toohello toepassing hello eerste keer dat ze het willen openen. Daarna biedt Azure Active Directory Hallo gebruikersnaam en wachtwoord namens Hallo-gebruiker. 

Zie voor meer informatie over het instellen van wachtwoorden gebaseerde aanmelding [wachtwoord vaulting voor eenmalige aanmelding met toepassingsproxy](application-proxy-sso-azure-portal.md).

## <a name="linked-sign-on"></a>Gekoppelde aanmelding

Als u al een oplossing voor eenmalige aanmelding instellen voor uw on-premises identiteiten, kiest u **gekoppelde aanmelding**. Deze optie kunt Azure Active Directory tooleverage bestaande SSO-oplossingen, maar nog steeds RAS toohello toepassing geeft uw gebruikers. 

Zie voor meer informatie over de gekoppelde aanmelding (voorheen bekend als bestaande eenmalige aanmelding) [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).

## <a name="integrated-windows-authentication"></a>Geïntegreerde Windows-verificatie

Als uw on-premises toepassingen met geïntegreerde Windows-Authentication(IWA) of als u wilt dat toouse Kerberos-beperkt delegatie (KCD) voor eenmalige aanmelding, kiest u **geïntegreerde Windows-verificatie**. Met deze optie uw gebruikers hoeven alleen tooauthenticate tooAzure Active Directory en vervolgens Hallo Application Proxy connector Hallo gebruiker tooget een Kerberos-token en meld u aan toohello toepassing imiteert. 

Zie voor meer informatie over het instellen van geïntegreerde Windows-verificatie [Kerberos-beperkte delegatie voor eenmalige aanmelding met toepassingsproxy](active-directory-application-proxy-sso-using-kcd.md).

## <a name="header-based-sign-on"></a>Op basis van een koptekst eenmalige aanmelding 

Als uw toepassingen headers voor verificatie gebruikt, kiest u **headers gebaseerde aanmelding**. Met deze optie kunnen vereist uw gebruikers alleen tooauthentication hello Azure Active Directory. Microsoft werkt samen met een derde partij verificatieservice PingAccess die hello Azure Active Directory-toegangstoken vertaald naar een header-indeling voor de toepassing hello genoemd. 

Zie voor meer informatie over het instellen van verificatie op basis van een koptekst [verificatie op basis van een koptekst voor eenmalige aanmelding met toepassingsproxy](application-proxy-ping-access.md).

## <a name="next-steps"></a>Volgende stappen

- [Wachtwoord voor eenmalige aanmelding met toepassingsproxy vaulting](application-proxy-sso-azure-portal.md)
- [Kerberos-beperkte delegatie voor eenmalige aanmelding met toepassingsproxy](active-directory-application-proxy-sso-using-kcd.md)
- [Verificatie op basis van een koptekst voor eenmalige aanmelding met toepassingsproxy](application-proxy-ping-access.md) 
