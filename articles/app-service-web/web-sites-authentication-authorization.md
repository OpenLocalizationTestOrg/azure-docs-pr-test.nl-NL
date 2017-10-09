---
title: aaaAuthenticate met lokale Active Directory in uw app in Azure | Microsoft Docs
description: Meer informatie over de verschillende opties Hallo voor line-of-business-apps in Azure App Service-tooauthenticate met lokale Active Directory
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: dde6b7e6-bf6a-4fa5-8390-3a18155d21bd
ms.service: app-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 08/31/2016
ms.author: cephalin
ms.openlocfilehash: 65bf25aaa0447fbbea7c754db55842d57e70757e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-on-premises-active-directory-in-your-azure-app"></a>Verificatie met de on-premises Active Directory in uw app in Azure
Dit artikel laat zien hoe tooauthenticate met lokale Active Directory (AD) in [Azure App Service](../app-service/app-service-value-prop-what-is.md). Een Azure-app wordt gehost in Hallo cloud, maar er zijn manieren tooauthenticate on-premises AD gebruikers veilig. 

## <a name="authenticate-through-azure-active-directory"></a>Verifiëren via Azure Active Directory
Een Azure Active Directory-tenant kan worden directory zijn gesynchroniseerd met een on-premises AD. Deze aanpak kunt AD-gebruikers toegang tot uw App vanaf internet Hallo en zich verifiëren met hun on-premises referenties. Bovendien Azure App Service biedt een [directe oplossing voor deze methode](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md). Met een paar klikken een knop kunt u verificatie met een tenant directory gesynchroniseerd inschakelen voor uw app in Azure. Deze methode biedt Hallo volgende voordelen:

* Vereist geen een verificatiecode op te geven in uw app. App Service wilt Hallo verificatie voor u en uw tijd besteden biedt functionaliteit in uw app kunt.
* [Azure AD Graph API](http://msdn.microsoft.com/library/azure/hh974476.aspx) kunnen toegang krijgen tot toodirectory gegevens van uw app in Azure.
* Eenmalige aanmelding te biedt[alle toepassingen die worden ondersteund door Azure Active Directory](/marketplace/active-directory/), zoals Office 365, Dynamics CRM Online, Microsoft Intune en duizenden niet-Microsoft-cloud-toepassingen. 
* Azure Active Directory biedt ondersteuning voor toegangsbeheer op basis van rollen. U kunt Hallo [Authorize(Roles="X")]-patroon gebruiken met minimale wijzigingen tooyour code.

hoe een Azure line-of-business-app die met Azure Active Directory verifieert, toowrite zien toosee [een Azure line-of-business-app maken met Azure Active Directory-verificatie](web-sites-dotnet-lob-application-azure-ad.md).

## <a name="authenticate-through-an-on-premises-sts"></a>Verificatie via een on-premises STS
Als u een lokale veilige beveiligingstokenservice (STS) zoals Active Directory Federation Services (AD FS) hebt, kunt u dat toofederate-verificatie voor uw app in Azure. Deze methode werkt het beste wanneer bedrijfsbeleid verhindert dat AD-gegevens worden opgeslagen in Azure. Let echter op Hallo volgende:

* STS-topologie moet zijn geïmplementeerd met on-premises, kosten en beheer-overhead.
* Alleen beheerders van AD FS kunnen configureren [relying partij vertrouwensrelaties en claimregels](http://technet.microsoft.com/library/dd807108.aspx), beperkt dat mogelijk Hallo ontwikkelaarsopties. Op Hallo daarentegen het is mogelijk toomanage en aanpassen [claims](http://technet.microsoft.com/library/ee913571.aspx) op basis van de per toepassing.
* Toegang tot tooon-premises AD-gegevens een afzonderlijke oplossing via Hallo bedrijfsfirewall vereist.

hoe een Azure line-of-business-app die met een STS lokale verifieert toowrite zien toosee [een Azure line-of-business-app maken met AD FS-authenticatie](web-sites-dotnet-lob-application-adfs.md).

