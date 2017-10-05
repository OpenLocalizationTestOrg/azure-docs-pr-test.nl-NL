---
title: Verificatie met de on-premises Active Directory in uw app in Azure | Microsoft Docs
description: Meer informatie over de verschillende opties voor line-of-business-apps in Azure App Service voor verificatie met de lokale Active Directory
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
ms.openlocfilehash: a68bcd7040498515a6e35a87ee6e6940a84506d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-with-on-premises-active-directory-in-your-azure-app"></a>Verificatie met de on-premises Active Directory in uw app in Azure
Dit artikel laat zien hoe u verifieert met on-premises Active Directory (AD) in [Azure App Service](../app-service/app-service-value-prop-what-is.md). Een Azure-app wordt gehost in de cloud, maar er zijn verificatiemethoden on-premises AD gebruikers veilig. 

## <a name="authenticate-through-azure-active-directory"></a>Verifiëren via Azure Active Directory
Een Azure Active Directory-tenant kan worden directory zijn gesynchroniseerd met een on-premises AD. Deze aanpak kunt AD-gebruikers toegang tot uw App via internet en zich verifiëren met hun on-premises referenties. Bovendien Azure App Service biedt een [directe oplossing voor deze methode](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md). Met een paar klikken een knop kunt u verificatie met een tenant directory gesynchroniseerd inschakelen voor uw app in Azure. Deze methode biedt de volgende voordelen:

* Vereist geen een verificatiecode op te geven in uw app. Kan App Service de verificatie voor u doen en tijd kwijt aan op het bieden van functionaliteit in uw app.
* [Azure AD Graph API](http://msdn.microsoft.com/library/azure/hh974476.aspx) kan toegang worden ingeschakeld voor Active directory-gegevens van uw app in Azure.
* SSO biedt [alle toepassingen die worden ondersteund door Azure Active Directory](/marketplace/active-directory/), zoals Office 365, Dynamics CRM Online, Microsoft Intune en duizenden niet-Microsoft-cloud-toepassingen. 
* Azure Active Directory biedt ondersteuning voor toegangsbeheer op basis van rollen. U kunt het patroon [Authorize(Roles="X")] met minimale wijzigingen aan uw code.

Zie voor het schrijven van een Azure line-of-business-app die met Azure Active Directory verifieert [een Azure line-of-business-app maken met Azure Active Directory-verificatie](web-sites-dotnet-lob-application-azure-ad.md).

## <a name="authenticate-through-an-on-premises-sts"></a>Verificatie via een on-premises STS
Als er een lokale veilige beveiligingstokenservice (STS) zoals Active Directory Federation Services (AD FS), kunt u die kunt gebruiken voor het federeren van verificatie voor uw app in Azure. Deze methode werkt het beste wanneer bedrijfsbeleid verhindert dat AD-gegevens worden opgeslagen in Azure. Let echter op het volgende:

* STS-topologie moet zijn geïmplementeerd met on-premises, kosten en beheer-overhead.
* Alleen beheerders van AD FS kunnen configureren [relying partij vertrouwensrelaties en claimregels](http://technet.microsoft.com/library/dd807108.aspx), die de ontwikkelaar opties kunnen beperken. Anderzijds, is het mogelijk om te beheren en aanpassen [claims](http://technet.microsoft.com/library/ee913571.aspx) op basis van de per toepassing.
* Toegang tot on-premises AD-gegevens vereist een afzonderlijke oplossing via de firewall van het bedrijf.

Zie voor het schrijven van een Azure line-of-business-app die verifieert met een STS lokale [een Azure line-of-business-app maken met AD FS-authenticatie](web-sites-dotnet-lob-application-adfs.md).

