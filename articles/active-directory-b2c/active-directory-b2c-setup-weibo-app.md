---
title: 'Azure Active Directory B2C: Weibo configuratie | Microsoft Docs'
description: Bieden zich kunnen registreren en aanmelden tooconsumers Weibo accounts in uw toepassingen die zijn beveiligd met Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 1860de34-94cb-4ceb-851e-102f930f7230
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: c0648620f318046c1d9d24feb92a0c5f19c6a91a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-weibo-accounts"></a>Azure Active Directory B2C: Bieden Weibo accounts zich kunnen registreren en aanmelden tooconsumers

> [!NOTE]
> Deze functie is in preview. Gebruik deze id-provider niet in uw productieomgeving.
> 

## <a name="create-a-weibo-application"></a>Een toepassing Weibo maken

toouse Weibo als een id-provider in Azure Active Directory (Azure AD) B2C, u moet een toepassing Weibo toocreate en leveren met de juiste parameters Hallo. U moet een account Weibo toodo dit. Als u niet hebt, kunt u één voor één [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us).

### <a name="register-for-hello-weibo-developer-program"></a>Registreren voor Hallo Weibo Ontwikkelaarsprogramma

1. Ga toohello [Weibo ontwikkelaarsportal](http://open.weibo.com/) en meld u aan met de referenties van uw Weibo-account.
2. Na het aanmelden, klik op de weergavenaam van uw in de rechterbovenhoek Hallo.
3. Selecteer in de vervolgkeuzelijst Hallo**编辑开发者信息**(informatie voor ontwikkelaars bewerken).
4. Hallo vereist gegevens invoeren in Hallo-formulier en klik op**提交**(verzenden).
5. Hallo e-verificatieproces voltooien.
6. Ga toohello [identiteitverificatie pagina](http://open.weibo.com/developers/identity/edit).
7. Hallo vereist gegevens invoeren in Hallo-formulier en klik op**提交**(verzenden).

### <a name="register-a-weibo-application"></a>Een toepassing Weibo registreren

1. Ga toohello [app de registratiepagina van nieuwe Weibo](http://open.weibo.com/apps/new).
2. Geef informatie op Hallo benodigde toepassing.
3. Klik op**创建**(maken).
4. Kopieer de waarden Hallo van **App-sleutel** en **App geheim**. U nodig deze later.
5. Hallo vereist foto's uploaden en voer de benodigde informatie Hallo.
6. Klik op**保存以上信息**(opslaan).
7. Klik op**高级信息**(Geavanceerd informatie).
8. Klik op**编辑**(bewerken) volgende toohello veld voor OAuth2.0**授权设置**(Omleidings-URL).
9. Voer `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp` voor OAuth2.0**授权设置**(Omleidings-URL). Bijvoorbeeld, als uw `tenant_name` contoso.onmicrosoft.com, set Hallo URL toobe is `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.
10. Klik op**提交**(verzenden).  

## <a name="configure-weibo-as-an-identity-provider-in-your-tenant"></a>Weibo configureren als een id-provider in uw tenant
1. Volg deze stappen te[toohello B2C-functiesblade navigeren](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) op Hallo Azure-portal.
2. Klik op de blade Hallo B2C-functies, **identiteitsproviders**.
3. Klik op **+ toevoegen** Hallo boven aan het Hallo-blade.
4. Geef een beschrijvende **naam** voor Hallo identiteit provider configureren. Voer bijvoorbeeld 'Weibo'.
5. Klik op **identiteit providertype**, selecteer **Weibo**, en klik op **OK**.
6. Klik op **instellen van deze id-provider**
7. Voer Hallo **App-sleutel** die u eerder hebt gekopieerd als Hallo **Client-ID**.
8. Voer Hallo **App geheim** die u eerder hebt gekopieerd als Hallo **Clientgeheim**.
9. Klik op **OK** en klik vervolgens op **maken** toosave uw Weibo-configuratie.

