---
title: aaaSingle tooapps aanmelding met Azure AD-toepassingsproxy | Microsoft Docs
description: Schakel eenmalige aanmelding voor uw gepubliceerde on-premises toepassingen met Azure AD-toepassingsproxy in hello Azure-portal.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 5ff288d36163b74215677d9e34c93c985ac33d54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="password-vaulting-for-single-sign-on-with-application-proxy"></a>Wachtwoord voor eenmalige aanmelding met toepassingsproxy vaulting

Azure Active Directory-toepassingsproxy helpt u bij de productiviteit door on-premises toepassingen publiceren zodat externe werknemers veilig toegang deze te tot verbeteren. In hello Azure-portal, kunt u ook eenmalige aanmelding (SSO) toothese apps instellen. Uw gebruikers hoeven alleen tooauthenticate met Azure AD en toegang te krijgen tot uw zakelijke toepassing zonder toosign in opnieuw.

Toepassingsproxy ondersteunt verschillende [eenmalige aanmelding modi](application-proxy-sso-overview.md). Op basis van wachtwoorden eenmalige aanmelding is bedoeld voor toepassingen die gebruikmaken van een combinatie van gebruikersnaam en wachtwoord voor verificatie. Wanneer u op basis van wachtwoorden eenmalige aanmelding voor uw toepassing configureert, hebben uw gebruikers toosign in één keer toohello on-premises toepassing. Hierna is Azure Active Directory Hallo aanmelden informatie opslaat en automatisch biedt deze toepassing toohello wanneer uw gebruikers toegang op afstand. 

U moet al hebt gepubliceerd en uw app met toepassingsproxy getest. Als dit niet het geval is, volgt u de stappen Hallo in [toepassingen publiceren met Azure AD-toepassingsproxy](application-proxy-publish-azure-portal.md) vervolgens kun je hier. 

## <a name="set-up-password-vaulting-for-your-application"></a>Wachtwoord voor uw toepassing vaulting instellen

1. Meld u aan toohello [Azure-portal](https://portal.azure.com) als beheerder.
2. Selecteer **Azure Active Directory** > **bedrijfstoepassingen** > **alle toepassingen**.
3. Selecteer in Hallo lijst Hallo-app die u wilt dat tooset up met eenmalige aanmelding.  
4. Selecteer **eenmalige aanmelding**.

   ![Schakel eenmalige aanmelding](./media/application-proxy-sso-azure-portal/select-sso.png)

5. Kies bij Hallo SSO-modus **op basis van wachtwoorden aanmelding**.
6. Voor Hallo aanmeldings-URL, Hallo URL opgeven voor Hallo pagina waar gebruikers hun gebruikersnaam en wachtwoord toosign in tooyour app buiten het bedrijfsnetwerk Hallo invoeren. Kan dit Hallo externe URL die u hebt gemaakt toen u Hallo-app via toepassingsproxy gepubliceerd. 

   ![Kiezen op basis van wachtwoorden eenmalige aanmelding en voer de URL](./media/application-proxy-sso-azure-portal/password-sso.png)

7. Selecteer **Opslaan**.

<!-- Need toorepro?
7. hello page should tell you that a sign-in form was successfully detected at hello provided URL. If it doesn't, select **Configure [your app name] Password Single Sign-on Settings** and choose **Manually detect sign-in fields**. Follow hello instructions toopoint out where hello sign-in credentials go. 
-->

## <a name="test-your-app"></a>Uw app testen

Ga tooexternal-URL die u hebt geconfigureerd voor externe toegang tooyour toepassing. Aanmelden met uw referenties voor die app (of het Hallo-referenties voor een testaccount dat u toegang hebt ingesteld). Zodra u zich is aanmeldt, moet u kunnen tooleave Hallo app en keert u terug zonder uw referenties opnieuw invoeren. 

## <a name="next-steps"></a>Volgende stappen

- Meer informatie over andere manieren tooimplement [eenmalige aanmelding met toepassingsproxy](application-proxy-sso-overview.md)
- Meer informatie over [beveiligingsoverwegingen voor toegang tot apps op afstand met Azure AD-toepassingsproxy](application-proxy-security-considerations.md)