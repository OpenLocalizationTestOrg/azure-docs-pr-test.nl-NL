---
title: 'Azure Active Directory B2C: Q configuratie | Microsoft Docs'
description: Bieden zich kunnen registreren en aanmelden tooconsumers q-accounts in uw toepassingen die zijn beveiligd met Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 18c2cf94-8004-4de1-81c2-e45be65ce12d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: 896d6221e01d15de1652a5717cf1f65619101e0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-qq-accounts"></a>Azure Active Directory B2C: Tooconsumers zich kunnen registreren en aanmelden met q-accounts bieden

> [!NOTE]
> Deze functie is in preview.
> 

## <a name="create-a-qq-application"></a>Een q-toepassing maken

toouse q als een id-provider in Azure Active Directory (Azure AD) B2C, u moet een toepassing q toocreate en leveren met de juiste parameters Hallo. U moet een account q toodo dit. Als u niet hebt, kunt u één voor één [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033).

### <a name="register-for-hello-qq-developer-program"></a>Registreren voor Hallo q Ontwikkelaarsprogramma

1. Ga toohello [q-portal voor ontwikkelaars](http://open.qq.com) en meld u aan met de referenties van uw q-account.
2. Na het aanmelden, ga te[http://open.qq.com/reg](http://open.qq.com/reg) tooregister zelf als ontwikkelaar.
3. Selecteer in het menu Hallo**个人**(afzonderlijke developer).
4. Hallo vereist gegevens invoeren in Hallo-formulier en klik op**下一步**(volgende stap).
5. Hallo e-verificatieproces voltooien.

> [!NOTE]
> U moet een paar dagen toobe goedgekeurd na de registratie als ontwikkelaar toowait. 

### <a name="register-a-qq-application"></a>Een q-toepassing registreren

1. Ga te[https://connect.qq.com/index.html](https://connect.qq.com/index.html).
2. Klik op**应用管理**(app management).
3. Klik op**创建应用**(app maken).
4. Geef informatie op Hallo app nodig.
5. Klik op**创建应用**(app maken).
6. Geef informatie op Hallo vereist.
7. Voor Hallo**授权回调域**(callback URL) Voer `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`. Bijvoorbeeld, als uw `tenant_name` contoso.onmicrosoft.com, set Hallo URL toobe is `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.
8. Klik op**创建应用**(app maken).
9. Klik op de pagina Bevestiging Hallo op**应用管理**(app management) tooreturn toohello app management-pagina.
10. Klik op**查看**(weergave) volgende toohello app die u zojuist hebt gemaakt.
11. Klik op**修改**(bewerken).
12. Kopiëren van Hallo bovenaan pagina Hallo Hallo **APP-ID** en **APP-sleutel**.

## <a name="configure-qq-as-an-identity-provider-in-your-tenant"></a>Q configureren als een id-provider in uw tenant
1. Volg deze stappen te[toohello B2C-functiesblade navigeren](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) op Hallo Azure-portal.
2. Klik op de blade Hallo B2C-functies, **identiteitsproviders**.
3. Klik op **+ toevoegen** Hallo boven aan het Hallo-blade.
4. Geef een beschrijvende **naam** voor Hallo identiteit provider configureren. Voer bijvoorbeeld 'Q'.
5. Klik op **identiteit providertype**, selecteer **q**, en klik op **OK**.
6. Klik op **instellen van deze id-provider**
7. Voer Hallo **App-sleutel** die u eerder hebt gekopieerd als Hallo **Client-ID**.
8. Voer Hallo **App geheim** die u eerder hebt gekopieerd als Hallo **Clientgeheim**.
9. Klik op **OK** en klik vervolgens op **maken** toosave uw q-configuratie.

