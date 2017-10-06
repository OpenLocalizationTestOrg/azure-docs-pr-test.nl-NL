---
title: aaaHow tooLink een Azure-abonnement tooAzure AD B2C | Microsoft Docs
description: Stapsgewijze handleiding tooenable facturering voor Azure AD B2C-tenant in een Azure-abonnement.
services: active-directory-b2c
documentationcenter: dev-center-name
author: rojasja
manager: mbaldwin
ms.service: active-directory-b2c
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/05/2016
ms.author: joroja
ms.openlocfilehash: 07b2ed5f7f5f543c9cbb8e9a35107462448e9440
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="linking-an-azure-subscription-tooan-azure-b2c-tenant-toopay-for-usage-charges"></a>Koppelen van een Azure-abonnement tooan Azure B2C-tenant toopay voor gebruikskosten

Doorlopende gebruikskosten voor Azure Active Directory B2C (of Azure AD B2C) worden gefactureerd tooan Azure-abonnement. Dit is nodig voor Hallo tenant administrator tooexplicitly koppeling hello Azure AD B2C-tenant tooan Azure-abonnement na het maken van Hallo B2C-tenant zelf.  Deze koppeling wordt bereikt door het maken van een Azure AD 'B2C-Tenant' resource in Hallo doel-Azure-abonnement. Veel B2C tenants mag gekoppelde tooa één Azure-abonnement samen met andere Azure-resources (bijvoorbeeld virtuele machines, gegevensopslag, LogicApps)


> [!IMPORTANT]
> meest recente informatie over het gebruik van facturering en prijzen voor B2C is op de volgende pagina Hallo Hallo: [prijzen van Azure AD B2C](
https://azure.microsoft.com/pricing/details/active-directory-b2c/)

## <a name="step-1---create-an-azure-ad-b2c-tenant"></a>Stap 1: een Azure AD B2C-Tenant maken
Maken van de B2C-tenant moet eerst worden voltooid. Deze stap overslaan als u uw doel B2C-Tenant al hebt gemaakt. [Aan de slag met Azure AD B2C](active-directory-b2c-get-started.md)

## <a name="step-2---open-azure-portal-in-hello-azure-ad-tenant-that-shows-your-azure-subscription"></a>Stap 2: Open Azure-portal op Hallo Azure AD-Tenant waarin uw Azure-abonnement
Navigeer toohello [Azure-portal](https://portal.azure.com). Azure AD-Tenant waarin hello Azure-abonnement u wilt dat toouse toohello overschakelen. Deze Azure AD-tenant is anders dan Hallo B2C-tenant. Klik in hello Azure-portal, op Hallo-accountnaam op Hallo rechtsboven Hallo dashboard tooselect hello Azure AD-Tenant. Een Azure-abonnement is nodig tooproceed. [Een Azure-abonnement ophalen](https://account.windowsazure.com/signup?showCatalog=True)

![Azure AD-Tenant tooyour overschakelen](./media/active-directory-b2c-how-to-enable-billing/SelectAzureADTenant.png)

## <a name="step-3---create-a-b2c-tenant-resource-in-azure-marketplace"></a>Stap 3: een B2C-Tenant-resource maken in Azure Marketplace
Marketplace openen door te klikken op Hallo Marketplace-pictogram of Hallo groen plusteken (+) te selecteren in Hallo linksboven Hallo-dashboard.  Zoek en selecteer Azure Active Directory B2C. Selecteer maken.

![Selecteer Marketplace](./media/active-directory-b2c-how-to-enable-billing/marketplace.png)

![AD B2C zoeken](./media/active-directory-b2c-how-to-enable-billing/searchb2c.png)

Hello Azure AD B2C-Resource maken dialoogvenster dekt Hallo volgende parameters:

1. Azure AD B2C-Tenant – Selecteer een Azure AD B2C-Tenant in Hallo vervolgkeuzelijst.  Alleen in aanmerking komende Azure AD B2C tenants weergeven.  In aanmerking komende B2C tenants aan deze voorwaarden voldoet: U bent Hallo globale beheerder van Hallo B2C-tenant en Hallo B2C-tenant is niet gekoppeld tooan Azure-abonnement

2. Resourcenaam van Azure AD B2C - is voorgeselecteerde toomatch Hallo-domeinnaam van Hallo B2C-Tenant

3. Abonnement - een actief Azure-abonnement waarin u een beheerder of medebeheerder zijn.  Meerdere Tenants van Azure AD B2C kunnen tooone Azure-abonnement worden toegevoegd

4. Locatie van de resourcegroep en resourcegroep - deze artefacten kunt u meerdere Azure-resources te organiseren.  Deze optie heeft geen invloed op uw B2C-tenant locatie, prestaties of facturering status

5. Toodashboard voor eenvoudigste toegang tooyour B2C-tenant informatie en Hallo B2C-tenant instellingen facturering vastmaken ![B2C-Resource maken](./media/active-directory-b2c-how-to-enable-billing/createresourceb2c.png)

## <a name="step-4---manage-your-b2c-tenant-resources-optional"></a>Stap 4: uw B2C-Tenant resources (optioneel) beheren
Zodra de implementatie is voltooid, wordt een nieuwe 'B2C-Tenant'-resource is gemaakt in de doelresourcegroep Hallo en gerelateerde Azure-abonnement.  U ziet een nieuwe resource van het type 'B2C-Tenant' toegevoegd naast uw andere Azure-resources.

![B2C-Resource maken](./media/active-directory-b2c-how-to-enable-billing/b2cresourcedashboard.png)

Door te klikken op Hallo B2C-tenant resource, zich u kunt
- Klik op abonnement naam tooreview factureringsgegevens. Zie facturering en informatie over het gebruik.
- Klik op Azure AD B2C-instellingen tooopen een nieuw browsertabblad rechtstreeks in tooyour B2C-tenant blade instellingen
- Een ondersteuningsaanvraag indienen
- Verplaats uw B2C-tenant resource tooanother Azure-abonnement of resourcegroep tooanother.  Deze keuze wijzigingen in welke Azure-abonnement ontvangt gebruikskosten.

![B2C broninstellingen](./media/active-directory-b2c-how-to-enable-billing/b2cresourcesettings.png)

## <a name="known-issues"></a>Bekende problemen
- Verwijderen van een B2C-Tenant. Als een B2C-Tenant is gemaakt, verwijderd en opnieuw gemaakt met dezelfde domeinnaam hello, neem ook verwijderen en opnieuw maken 'Koppelen' Hallo-resource met de Hallo dezelfde domeinnaam.  U vindt dit 'Koppelen' bron op onder 'Alle resources' in hello abonnement tenant via hello Azure-portal.
- Zelf-opgelegde beperkingen op regionale Resourcelocatie.  In zeldzame gevallen, kan een gebruiker een regionale beperking voor het maken van Azure resource hebt vastgesteld.  Deze beperking kan voorkomt het maken van Hallo Hallo koppeling tussen een Azure-abonnement en een B2C-Tenant. toomitigate, neem versoepelen deze beperking.

## <a name="next-steps"></a>Volgende stappen
Zodra deze stappen voltooid voor elk van uw B2C-tenants zijn, wordt uw Azure-abonnement in rekening gebracht volgens de details van uw Azure directe of Enterprise Agreement.
- Bekijk informatie over het gebruik en facturering binnen uw geselecteerde Azure-abonnement
- Bekijk gedetailleerde dag gebruiksrapporten Hallo met [gebruik rapportage-API](active-directory-b2c-reference-usage-reporting-api.md)
