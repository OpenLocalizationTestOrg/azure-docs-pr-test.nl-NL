---
title: 'Azure Active Directory B2C: LinkedIn configuratie | Microsoft Docs'
description: Registreren en aanmelden tooconsumers voorzien van LinkedIn accounts in uw toepassingen die zijn beveiligd met Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: fa51a16b-9ce9-4e27-9eff-0869b4c4f0ef
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 6c5233ef48b24968fd6383f470b5d8a969a78ecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-linkedin-accounts"></a>Azure Active Directory B2C: Bieden LinkedIn accounts zich kunnen registreren en aanmelden tooconsumers
## <a name="create-a-linkedin-application"></a>Een LinkedIn-toepassing maken
toouse LinkedIn als een id-provider in Azure Active Directory (Azure AD) B2C, u moet een toepassing LinkedIn toocreate en leveren met de juiste parameters Hallo. U moet een account LinkedIn toodo dit. Als u niet hebt, kunt u krijgen op het [https://www.linkedin.com/](https://www.linkedin.com/).

1. Ga toohello [LinkedIn ontwikkelaars website](https://www.developer.linkedin.com/) en meld u aan met de referenties van uw LinkedIn-account.
2. Klik op **mijn Apps** in Hallo bovenste menubalk en klik vervolgens op **toepassing maken**.
   
    ![LinkedIn - nieuwe app](./media/active-directory-b2c-setup-li-app/linkedin-new-app.png)
3. In Hallo **Maak een nieuwe toepassing** Vul Hallo relevante informatie (**bedrijfsnaam**, **naam**, **beschrijving**, **Toepassing Logo URL**, **toepassing gebruik**, **Website-URL**, **zakelijke e** en **telefoon (werk)**).
4. Ik ga hiermee akkoord toohello **LinkedIn API gebruiksvoorwaarden** en klik op **indienen**.
   
    ![LinkedIn - app registreren](./media/active-directory-b2c-setup-li-app/linkedin-register-app.png)
5. Kopieer de waarden Hallo van **Client-ID** en **Clientgeheim**. (U vindt deze onder **verificatiesleutels**.) U moet ze tooconfigure LinkedIn als een id-provider in uw tenant.
   
   > [!NOTE]
   > **Clientgeheim** is een belangrijke beveiligingsreferentie.
   > 
   > 
6. Voer `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in Hallo **geautoriseerd Omleidings-URL's** veld (onder **OAuth 2.0**). Vervang **{tenant}** met de naam van uw tenant (bijvoorbeeld: contoso.onmicrosoft.com). Klik op **toevoegen**, en klik vervolgens op **Update**. Hallo **{tenant}** hoofdlettergevoelig.
   
    ![LinkedIn - Setup-app](./media/active-directory-b2c-setup-li-app/linkedin-setup.png)

## <a name="configure-linkedin-as-an-identity-provider-in-your-tenant"></a>LinkedIn configureren als een id-provider in uw tenant
1. Volg deze stappen te[toohello B2C-functiesblade navigeren](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) op Hallo Azure-portal.
2. Klik op de blade Hallo B2C-functies, **identiteitsproviders**.
3. Klik op **+ toevoegen** Hallo boven aan het Hallo-blade.
4. Geef een beschrijvende **naam** voor Hallo identiteit provider configureren. Voer bijvoorbeeld 'LI'.
5. Klik op **identiteit providertype**, selecteer **LinkedIn**, en klik op **OK**.
6. Klik op **instellen van deze id-provider** en Voer Hallo-ID en client clientgeheim Hallo LinkedIn-toepassing die u eerder hebt gemaakt.
7. Klik op **OK** en klik vervolgens op **maken** toosave uw LinkedIn-configuratie.

