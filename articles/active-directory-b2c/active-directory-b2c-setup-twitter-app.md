---
title: 'Azure Active Directory B2C: Twitter configuratie | Microsoft Docs'
description: Geef tooconsumers zich kunnen registreren en aanmelden met Twitter-accounts in uw toepassingen die zijn beveiligd met Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 579a6841-9329-45b8-a351-da4315a6634e
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/06/2017
ms.author: parakhj
ms.openlocfilehash: 275c5c73fd5e8e5075e77fee942cbc1b5e1586cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-twitter-accounts"></a>Azure Active Directory B2C: Tooconsumers zich kunnen registreren en aanmelden met Twitter-accounts bieden

> [!NOTE]
> Deze functie is in preview.
> 

## <a name="create-a-twitter-application"></a>Een Twitter-toepassing maken
toouse Twitter als een id-provider in Azure Active Directory (Azure AD) B2C, u toocreate Twitter-toepassing nodig hebt en deze met de juiste parameters Hallo opgeven. U moet een Twitter developer-account toodo dit. Als u niet hebt, kunt u krijgen op het [https://dev.twitter.com/](https://dev.twitter.com/).

1. Ga toohello [Twitter-website voor ontwikkelaars van](https://dev.twitter.com/) en meld u aan met uw referenties.
2. Klik op **mijn apps** onder **hulpprogramma's en ondersteuning** en klik vervolgens op **nieuwe App maken**. 
3. In de vorm hello, kunt u een waarde opgeven voor Hallo **naam**, **beschrijving**, en **Website**.
4. Voor Hallo **retouraanroep URL**, voer `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`. Zorg ervoor dat tooreplace **{tenant}** met de naam van uw tenant (bijvoorbeeld contosob2c.onmicrosoft.com).
5. Controleer Hallo vak tooagree toohello **Developer overeenkomst** en klik op **uw Twitter-toepassing maken**.
6. Zodra het Hallo-app is gemaakt, klikt u op **sleutels en toegangstokens**.
7. Hallo-waarde van kopiëren **consumentsleutel** en **consumentgeheim**. U moet ze tooconfigure Twitter als een id-provider in uw tenant.

## <a name="configure-twitter-as-an-identity-provider-in-your-tenant"></a>Twitter configureren als een id-provider in uw tenant
1. Volg deze stappen te[toohello B2C-functiesblade navigeren](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) op Hallo Azure-portal.
2. Klik op de blade Hallo B2C-functies, **identiteitsproviders**.
3. Klik op **+ toevoegen** Hallo boven aan het Hallo-blade.
4. Geef een beschrijvende **naam** voor Hallo identiteit provider configureren. Voer bijvoorbeeld 'Twitter'.
5. Klik op **identiteit providertype**, selecteer **Twitter**, en klik op **OK**.
6. Klik op **instellen van deze id-provider** en Voer Hallo Twitter **consumentsleutel** voor Hallo **Client-id** en Twitter Hallo **consumentgeheim**voor Hallo **clientgeheim**.
7. Klik op **OK**, en klik vervolgens op **maken** toosave uw Twitter-configuratie.

