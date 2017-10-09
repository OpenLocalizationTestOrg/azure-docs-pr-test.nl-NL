---
title: 'Azure Active Directory B2C: Google + configuratie | Microsoft Docs'
description: Geef tooconsumers zich kunnen registreren en aanmelden met Google + accounts in uw toepassingen die zijn beveiligd met Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 4dcca66f-29e4-4b4d-8840-50baad736bd7
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 6ef66eb17777acd95b5f4745ed6097c77e37663b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-google-accounts"></a>Azure Active Directory B2C: Bieden tooconsumers zich kunnen registreren en aanmelden met Google + accounts
## <a name="create-a-google-application"></a>Een Google +-toepassing maken
toouse Google + als een id-provider in Azure Active Directory (Azure AD) B2C, u moet een Google +-toepassing toocreate en leveren met de juiste parameters Hallo. U moet een Google + account toodo dit. Als u niet hebt, kunt u krijgen op het [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).

1. Ga toohello [Google ontwikkelaars Console](https://console.developers.google.com/) en meld u aan met de referenties van uw Google + account.
2. Klik op **project maken**, voer een **projectnaam**, en klik vervolgens op **maken**.
   
    ![Google + - aan de slag](./media/active-directory-b2c-setup-goog-app/google-get-started.png)
   
    ![Google + - nieuw project](./media/active-directory-b2c-setup-goog-app/google-new-project.png)
3. Klik op **API Manager** en klik vervolgens op **referenties** in Hallo linkernavigatiebalk.
4. Klik op Hallo **OAuth toestemming scherm** Hallo boven op tabblad.
   
    ![Google + - referenties](./media/active-directory-b2c-setup-goog-app/google-add-cred.png)
5. Selecteer of geef een geldige **e-mailadres**, bieden een **Productnaam**, en klik op **opslaan**.
   
    ![Google + - OAuth toestemming scherm](./media/active-directory-b2c-setup-goog-app/google-consent-screen.png)
6. Klik op **nieuwe referenties** en kies vervolgens **OAuth-Clientidentiteit**.
   
    ![Google + - OAuth toestemming scherm](./media/active-directory-b2c-setup-goog-app/google-add-oauth2-client-id.png)
7. Onder **toepassingstype**, selecteer **webtoepassing**.
   
    ![Google + - OAuth toestemming scherm](./media/active-directory-b2c-setup-goog-app/google-web-app.png)
8. Geef een **naam** voor uw toepassing, voert u `https://login.microsoftonline.com` in Hallo **geautoriseerd JavaScript oorsprongen** veld en `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in Hallo **geautoriseerde omleidings-URI's**veld. Vervang **{tenant}** met de naam van uw tenant (bijvoorbeeld contosob2c.onmicrosoft.com). Hallo **{tenant}** hoofdlettergevoelig. Klik op **Create**.
   
    ![Google + - client-ID maken](./media/active-directory-b2c-setup-goog-app/google-create-client-id.png)
9. Kopieer de waarden Hallo van **Client-ID** en **clientgeheim**. U moet ze tooconfigure Google + als een id-provider in uw tenant. **Clientgeheim** is een belangrijke beveiligingsreferentie.
   
    ![Google + - clientgeheim](./media/active-directory-b2c-setup-goog-app/google-client-secret.png)

## <a name="configure-google-as-an-identity-provider-in-your-tenant"></a>Google + als een id-provider in uw tenant configureren
1. Volg deze stappen te[toohello B2C-functiesblade navigeren](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) op Hallo Azure-portal.
2. Klik op de blade Hallo B2C-functies, **identiteitsproviders**.
3. Klik op **+ toevoegen** Hallo boven aan het Hallo-blade.
4. Geef een beschrijvende **naam** voor Hallo identiteit provider configureren. Voer bijvoorbeeld "G +".
5. Klik op **identiteit providertype**, selecteer **Google**, en klik op **OK**.
6. Klik op **instellen van deze id-provider** en Voer Hallo-ID en client clientgeheim Hallo Google +-toepassing die u eerder hebt gemaakt.
7. Klik op **OK** en klik vervolgens op **maken** toosave uw Google +-configuratie.

