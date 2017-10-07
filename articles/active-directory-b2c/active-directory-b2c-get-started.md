---
title: 'Azure Active Directory B2C: Een Azure Active Directory B2C-tenant maken | Microsoft Docs'
description: In dit artikel hoe toocreate een Azure Active Directory B2C-tenant
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: patricka
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 06/07/2017
ms.author: swkrish
ms.openlocfilehash: e8b257d66c1f66ffb84f5d3d21b30b42eddcbac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-active-directory-b2c-tenant-in-hello-azure-portal"></a>Een Azure Active Directory B2C-tenant maken in hello Azure-portal

Door Sipi bewerkt.

Deze snelstartgids kunt u een Microsoft Azure Active Directory (Azure AD) B2C-tenant maken in een paar minuten. Wanneer u klaar bent, hebt u een B2C-tenant toouse voor het registreren van de B2C-toepassingen.

## <a name="prerequisites"></a>Vereisten

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

##  <a name="log-in-tooazure"></a>Meld u bij tooAzure

Meld u bij toohello [Azure-portal](https://portal.azure.com/).

## <a name="create-an-azure-ad-b2c-tenant"></a>Een Azure AD B2C-tenant maken

B2C-functies kunnen niet worden ingeschakeld in uw bestaande tenants. U moet toocreate een Azure AD B2C-tenant.

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

Gefeliciteerd, u hebt een Azure Active Directory B2C-tenant gemaakt. Bent u een globale beheerder van Hallo-tenant. U kunt naar believen hoofdbeheerders toevoegen. tooswitch tooyour nieuwe tenant, klikt u op Hallo *beheren van uw nieuwe koppeling van de tenant*.

![Uw nieuwe koppeling van de tenant beheren](./media/active-directory-b2c-get-started/manage-new-b2c-tenant-link.png)

> [!IMPORTANT]
> Als u van plan bent toouse een B2C-tenant voor een productie-app, leest u Hallo-artikel op [productie-scale versus B2C preview tenants](active-directory-b2c-reference-tenant-type.md). Er zijn bekende problemen bij het verwijderen van een bestaande B2C-tenant en opnieuw maken met de Hallo dezelfde domeinnaam. U moet toocreate een B2C-tenant met een andere domeinnaam.
>
>

## <a name="link-your-tenant-tooyour-subscription"></a>Uw tenant tooyour abonnement koppelen

U moet toolink uw Azure AD B2C tenant tooyour Azure-abonnement tooenable alle B2C-functies en hiervoor te betalen voor gebruikskosten. toolearn meer lezen [in dit artikel](active-directory-b2c-how-to-enable-billing.md). Als u uw Azure AD B2C-tenant tooyour Azure-abonnement niet koppelt, bepaalde functionaliteit is geblokkeerd en ziet u een waarschuwing ('geen abonnement gekoppelde toothis B2C-tenant of Hallo abonnement vereist uw aandacht.') in Hallo B2C-instellingen. Het is belangrijk dat u deze stap uitvoeren voordat u uw apps naar de productie verzendt.

## <a name="easy-access-toosettings"></a>Eenvoudige toegang toosettings

[!INCLUDE [active-directory-b2c-find-service-settings](../../includes/active-directory-b2c-find-service-settings.md)]

U kunt Hallo blade ook openen door te voeren `Azure AD B2C` in **zoeken bronnen** Hallo boven aan het Hallo-portal. Selecteer in de lijst met resultaten Hallo **Azure AD B2C** tooaccess Hallo blade B2C-instellingen.

## <a name="next-steps"></a>Volgende stappen

> [!div class="nextstepaction"]
> [Uw B2C-toepassing registreren in een B2C-tenant](active-directory-b2c-app-registration.md)
