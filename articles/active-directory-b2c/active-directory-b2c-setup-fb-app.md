---
title: 'Azure Active Directory B2C: Facebook-configuratie | Microsoft Docs'
description: Geef tooconsumers zich kunnen registreren en aanmelden met Facebook-accounts in uw toepassingen die zijn beveiligd met Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: 
author: sromeroz
manager: krassk
editor: sromeroz
ms.assetid: b875f235-a1d2-4abb-b9f0-b89beac38a32
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/7/2017
ms.author: sromeroz
ms.openlocfilehash: 4c3b79c7248bd1e789bf33fc467abb27d0170edd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-facebook-accounts"></a>Azure Active Directory B2C: Tooconsumers zich kunnen registreren en aanmelden met Facebook-accounts bieden
## <a name="create-a-facebook-application"></a>Een Facebook-toepassing maken
toouse Facebook als een id-provider in Azure Active Directory (Azure AD) B2C, u moet toocreate Facebook-toepassing en leveren met de juiste parameters Hallo. U moet een account Facebook toodo dit. Als u niet hebt, kunt u krijgen op het [https://www.facebook.com/](https://www.facebook.com/).

1. Ga toohello [Facebook voor ontwikkelaars](https://developers.facebook.com/) website en meld u aan met uw Facebook-accountreferenties.
2. Als u dit nog niet hebt gedaan, moet u tooregister als ontwikkelaar Facebook. toodo, klikt u op **registreren** (op Hallo rechterbovenhoek van Hallo pagina), Facebook van beleidsregels accepteren en Hallo registratie stappen uitvoeren.
3. Klik op **mijn Apps** en klik vervolgens op **toevoegen van een nieuwe App**. 
4. Hallo formulier, geeft u een **weergavenaam** en een geldig **Neem contact op met E-mail**.
5. Klik op **maken van App-ID**. Dit mogelijk dat u beleidsregels voor tooaccept Facebook-platform en een online security-controle voltooien.
6. Klik in de linkerkolom hello, **instellingen** en selecteer vervolgens **Basic** als niet al is ingeschakeld.
7. Selecteer een **categorie**. 
8. Klik op **+ toevoegen Platform** en selecteer **Website**.
   
    ![Facebook - instellingen](./media/active-directory-b2c-setup-fb-app/fb-settings.png)
   
    ![Facebook - instellingen - Website](./media/active-directory-b2c-setup-fb-app/fb-website.png)
9. Voer `https://login.microsoftonline.com/` in Hallo **Site-URL** veld en klik vervolgens op **wijzigingen opslaan** Hallo Hallo pagina onderaan in.
   
    ![Facebook - Site-URL](./media/active-directory-b2c-setup-fb-app/fb-site-url.png)

10. Hallo-waarde van kopiëren **App-ID**. Klik op **weergeven** en kopieer de waarde van Hallo **App geheim**. U moet ze tooconfigure Facebook als een id-provider in uw tenant. **App-geheim** is een belangrijke beveiligingsreferentie.
   
    ![Facebook - App-ID en App-geheim](./media/active-directory-b2c-setup-fb-app/fb-app-id-app-secret.png)
11. Klik op **+ Product toevoegen** Hallo linkernavigatiegedeelte en worden vervolgens Hallo **instellen** knop voor **Facebook aanmelding**.
   
    ![Facebook - Facebook-aanmelding](./media/active-directory-b2c-setup-fb-app/fb-login.png)
12. Klik op **instellingen** op de juiste nav Hallo onder **Facebook-aanmelding**

    ![Facebook - instellingen voor Facebook-aanmelding](./media/active-directory-b2c-setup-fb-app/fb-login-settings.png)
13. Voer `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in Hallo **geldig OAuth omleidings-URI's** veld Hallo **OAuth clientinstellingen** sectie. Vervang **{tenant}** met de naam van uw tenant (bijvoorbeeld contosob2c.onmicrosoft.com). Klik op **wijzigingen opslaan** Hallo Hallo pagina onderaan in.
    
    ![Facebook - OAuth omleidings-URI](./media/active-directory-b2c-setup-fb-app/fb-oauth-redirect-uri.png)
14. toomake uw Facebook-toepassing gebruikt door Azure AD B2C, moet u toomake deze openbaar beschikbaar. U kunt dit doen door te klikken op **App revisie** op Hallo linkernavigatiebalk en door Hallo schakelen overschakelen bovenaan Hallo Hallo pagina te**Ja** en te klikken op **bevestigen**.
    
    ![Facebook - App openbare](./media/active-directory-b2c-setup-fb-app/fb-app-public.png)

## <a name="configure-facebook-as-an-identity-provider-in-your-tenant"></a>Facebook configureren als een id-provider in uw tenant
1. Volg deze stappen te[toohello B2C-functiesblade navigeren](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) op Hallo Azure-portal.
2. Klik op de blade Hallo B2C-functies, **identiteitsproviders**.
3. Klik op **+ toevoegen** Hallo boven aan het Hallo-blade.
4. Geef een beschrijvende **naam** voor Hallo identiteit provider configureren. Voer bijvoorbeeld 'Facebook'.
5. Klik op **identiteit providertype**, selecteer **Facebook**, en klik op **OK**.
6. Klik op **instellen van deze id-provider** en Voer Hallo app-ID en app geheim (van Hallo Facebook-toepassing die u eerder hebt gemaakt) in Hallo **Client-ID** en **clientgeheim**respectievelijk velden.
7. Klik op **OK**, en klik vervolgens op **maken** toosave uw Facebook-configuratie.

> [!NOTE]
> Toevoegen van een **identiteitsprovider** tooyour tenant niet uw bestaande beleidsregels wijzigt. Houd er rekening mee tooupdate uw beleid door Hallo-identiteitsprovider die u zojuist hebt gemaakt.
>