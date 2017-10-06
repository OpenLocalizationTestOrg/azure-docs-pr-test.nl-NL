---
title: 'Azure Active Directory B2C: Amazon configuratie | Microsoft Docs'
description: Geef tooconsumers zich kunnen registreren en aanmelden met Amazon-accounts in uw toepassingen die zijn beveiligd met Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 77c099bb-a005-4d75-87f9-f61e3de48725
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 60d7c4b76d9d3e86ed535765329abed07f1e5996
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-amazon-accounts"></a>Azure Active Directory B2C: Tooconsumers zich kunnen registreren en aanmelden met Amazon-accounts bieden
## <a name="create-an-amazon-application"></a>Een Amazon-toepassing maken
toouse Amazon als een id-provider in Azure Active Directory (Azure AD) B2C, u moet een toepassing Amazon toocreate en leveren met de juiste parameters Hallo. U moet een Amazon-account toodo dit. Als u niet hebt, kunt u krijgen op het [http://www.amazon.com/](http://www.amazon.com/).

1. Ga toohello [Amazon Developer Center](https://login.amazon.com/) en meld u aan met de referenties van uw Amazon-account.
2. Als u dit nog niet hebt gedaan, klikt u op **aanmelden**stappen Hallo developer-registratie en Hallo beleid accepteren.
3. Klik op **nieuwe toepassing registreren**.
   
    ![Registreren van een nieuwe toepassing op Hallo Amazon-website](./media/active-directory-b2c-setup-amzn-app/amzn-new-app.png)
4. Bevatten toepassingsinformatie (**naam**, **beschrijving**, en **Privacy-URL voor kennisgeving**) en klik op **opslaan**.
   
    ![Informatie over de toepassing voor het registreren van een nieuwe toepassing op de Amazon bieden](./media/active-directory-b2c-setup-amzn-app/amzn-register-app.png)
5. In Hallo **Webinstellingen** sectie kopiëren Hallo waarden van **Client-ID** en **Clientgeheim**. (U moet tooclick hello **geheim weergeven** toosee knop dit.) U moet beide tooconfigure Amazon als een id-provider in uw tenant. Klik op **bewerken** onderaan Hallo Hallo-sectie. **Clientgeheim** is een belangrijke beveiligingsreferentie.
   
    ![Client-ID en Clientgeheim bieden voor uw nieuwe toepassing op de Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-client-secret.png)
6. Voer `https://login.microsoftonline.com` in Hallo **toegestaan JavaScript oorsprongen** veld en `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in Hallo **retourneren URL's toegestaan** veld. Vervang **{tenant}** met de naam van uw tenant (bijvoorbeeld: contoso.onmicrosoft.com). Klik op **Opslaan**. Hallo **{tenant}** hoofdlettergevoelig.
   
    ![Oorsprongen JavaScript en retourneren URL's voorziet in uw nieuwe toepassing op de Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-urls.png)

## <a name="configure-amazon-as-an-identity-provider-in-your-tenant"></a>Amazon configureren als een id-provider in uw tenant
1. Volg deze stappen te[toohello B2C-functiesblade navigeren](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) op Hallo Azure-portal.
2. Klik op de blade Hallo B2C-functies, **identiteitsproviders**.
3. Klik op **+ toevoegen** Hallo boven aan het Hallo-blade.
4. Geef een beschrijvende **naam** voor Hallo identiteit provider configureren. Voer bijvoorbeeld 'Amzn'.
5. Klik op **identiteit providertype**, selecteer **Amazon**, en klik op **OK**.
6. Klik op **instellen van deze id-provider** en Voer Hallo-ID en client clientgeheim Hallo Amazon-toepassing die u eerder hebt gemaakt.
7. Klik op **OK** en klik vervolgens op **maken** toosave uw Amazon-configuratie.

