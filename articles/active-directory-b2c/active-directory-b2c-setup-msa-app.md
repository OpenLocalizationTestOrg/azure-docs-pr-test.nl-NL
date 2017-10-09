---
title: 'Azure Active Directory B2C: Configuratie Microsoft-account | Microsoft Docs'
description: Tooconsumers zich kunnen registreren en aanmelden met Microsoft-accounts in uw toepassingen die zijn beveiligd met Azure Active Directory B2C opgeven.
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 06407322-142c-4cb3-9106-a8d752c4c853
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: bec4777f003c459030f68c35b24f0e4bcddf84ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-microsoft-accounts"></a>Azure Active Directory B2C: Tooconsumers zich kunnen registreren en aanmelden met Microsoft-accounts bieden
## <a name="create-a-microsoft-account-application"></a>Een toepassing van Microsoft-account maken
toouse Microsoft account toe als een id-provider in Azure Active Directory (Azure AD) B2C, u moet een Microsoft-account-toepassing toocreate en leveren met de juiste parameters Hallo. U moet een Microsoft-account toodo dit. Als u niet hebt, kunt u krijgen op het [https://www.live.com/](https://www.live.com/).

1. Ga toohello [Portal voor registratie van Microsoft-toepassing](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) en meld u aan met uw Microsoft-accountreferenties.
2. Klik op **een app toevoegen**.
   
    ![Microsoft-account: een nieuwe app toevoegen](./media/active-directory-b2c-setup-msa-app/msa-add-new-app.png)
3. Geef een **naam** voor uw toepassing en klik op **-toepassing maken**.
   
    ![Microsoft-account - App-naam](./media/active-directory-b2c-setup-msa-app/msa-app-name.png)
4. Hallo-waarde van kopiëren **toepassings-Id**. U hebt deze tooconfigure Microsoft-account als een id-provider in uw tenant.
   
    ![Microsoft-account - toepassings-Id](./media/active-directory-b2c-setup-msa-app/msa-app-id.png)
5. Klik op **toevoegen platform** en kies **Web**.
   
    ![Microsoft-account - platform toevoegen](./media/active-directory-b2c-setup-msa-app/msa-add-platform.png)
   
    ![Microsoft-account - webservice](./media/active-directory-b2c-setup-msa-app/msa-web.png)
6. Voer `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in Hallo **omleidings-URI's** veld. Vervang **{tenant}** met de naam van uw tenant (bijvoorbeeld contosob2c.onmicrosoft.com).
   
    ![Microsoft-account - Omleidings-URL](./media/active-directory-b2c-setup-msa-app/msa-redirect-url.png)
7. Klik op **nieuw wachtwoord genereren** onder Hallo **toepassing geheimen** sectie. Kopieer Hallo nieuw wachtwoord op het scherm wordt weergegeven. U hebt deze tooconfigure Microsoft-account als een id-provider in uw tenant. Dit wachtwoord is een belangrijke beveiligingsreferentie.
   
    ![Microsoft-account: nieuw wachtwoord genereren](./media/active-directory-b2c-setup-msa-app/msa-generate-new-password.png)
   
    ![Microsoft-account - nieuw wachtwoord](./media/active-directory-b2c-setup-msa-app/msa-new-password.png)
8. Selectievakje Hallo waarin staat dat **ondersteuning voor Live SDK** onder Hallo **geavanceerde opties** sectie. Klik op **Opslaan**.
   
    ![Microsoft-account - ondersteuning voor Live SDK](./media/active-directory-b2c-setup-msa-app/msa-live-sdk-support.png)

## <a name="configure-microsoft-account-as-an-identity-provider-in-your-tenant"></a>Microsoft-account configureren als een id-provider in uw tenant
1. Volg deze stappen te[toohello B2C-functiesblade navigeren](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) op Hallo Azure-portal.
2. Klik op de blade Hallo B2C-functies, **identiteitsproviders**.
3. Klik op **+ toevoegen** Hallo boven aan het Hallo-blade.
4. Geef een beschrijvende **naam** voor Hallo identiteit provider configureren. Voer bijvoorbeeld 'MSA'.
5. Klik op **identiteit providertype**, selecteer **Microsoft-account**, en klik op **OK**.
6. Klik op **instellen van deze id-provider** en Voer Hallo toepassings-Id en het wachtwoord van Hallo Microsoft-account-toepassing die u eerder hebt gemaakt.
7. Klik op **OK** en klik vervolgens op **maken** toosave je Microsoft-account configureren.

