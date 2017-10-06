---
title: 'Azure Active Directory B2C: WeChat configuratie | Microsoft Docs'
description: Bieden zich kunnen registreren en aanmelden tooconsumers WeChat accounts in uw toepassingen die zijn beveiligd met Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: d2424c66-ba68-4d82-847e-d137683527b0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: 92cc3579d818d2379a503ccc695138b33a34466d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-wechat-accounts"></a>Azure Active Directory B2C: Bieden WeChat accounts zich kunnen registreren en aanmelden tooconsumers

> [!NOTE]
> Deze functie is in preview.
> 

## <a name="create-a-wechat-application"></a>Een toepassing WeChat maken

toouse WeChat als een id-provider in Azure Active Directory (Azure AD) B2C, u moet een toepassing WeChat toocreate en leveren met de juiste parameters Hallo. U moet een account WeChat toodo dit. Als u niet hebt, kunt u een aanmelden via een van hun mobiele apps of via het nummer van uw q krijgen. Hierna is uw account is geregistreerd bij Hallo WeChat Ontwikkelaarsprogramma worden opgehaald. U vindt meer informatie [hier](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html).

### <a name="register-a-wechat-application"></a>Een toepassing WeChat registreren

1. Ga te[https://open.weixin.qq.com/](https://open.weixin.qq.com/) en zich aanmelden.
2. Klik op**管理中心**(center management).
3. Ga als volgt Hallo nodige tooregister een nieuwe toepassing.
4. Voor**授权回调域**(callback URL), voer `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`. Bijvoorbeeld, als uw `tenant_name` contoso.onmicrosoft.com, set Hallo URL toobe is `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.
5. Zoeken en kopieer Hallo **APP-ID** en **APP-sleutel**. U moet deze later.

## <a name="configure-wechat-as-an-identity-provider-in-your-tenant"></a>WeChat configureren als een id-provider in uw tenant
1. Volg deze stappen te[toohello B2C-functiesblade navigeren](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) op Hallo Azure-portal.
2. Klik op de blade Hallo B2C-functies, **identiteitsproviders**.
3. Klik op **+ toevoegen** Hallo boven aan het Hallo-blade.
4. Geef een beschrijvende **naam** voor Hallo identiteit provider configureren. Voer bijvoorbeeld 'WeChat'.
5. Klik op **identiteit providertype**, selecteer **WeChat**, en klik op **OK**.
6. Klik op **instellen van deze id-provider**
7. Voer Hallo **App-sleutel** die u eerder hebt gekopieerd als Hallo **Client-ID**.
8. Voer Hallo **App geheim** die u eerder hebt gekopieerd als Hallo **Clientgeheim**.
9. Klik op **OK** en klik vervolgens op **maken** toosave uw WeChat-configuratie.

