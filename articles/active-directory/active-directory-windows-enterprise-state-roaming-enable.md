---
title: aaaEnable Enterprise State Roaming in Azure Active Directory | Microsoft Docs
description: Veelgestelde vragen over Enterprise State Roaming-instellingen in Windows-apparaten. Enterprise State Roaming biedt gebruikers een uniforme ervaring via hun Windows-apparaten en minder Hallo tijd die nodig zijn voor het configureren van een nieuw apparaat.
services: active-directory
keywords: Enterprise-status tijdens roaming windows cloud, hoe tooenable enterprise state roaming
documentationcenter: 
author: tanning
manager: femila
editor: curtand
ms.assetid: f71d66fd-7f9e-45eb-9cfe-5d989870f8a4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: c69a9cfa8055f418a3b81c62939885d5bec8a6f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-enterprise-state-roaming-in-azure-active-directory"></a>Enterprise state roaming inschakelen in Azure Active Directory
Enterprise State Roaming is beschikbaar tooany organisatie met een Premium Azure Active Directory (Azure AD) abonnement. Voor meer informatie over hoe u een Azure AD-abonnement tooget Zie Hallo [productpagina Azure AD](https://azure.microsoft.com/services/active-directory).

Wanneer u Enterprise State Roaming inschakelt, wordt uw organisatie automatisch verleend licenties voor een gratis abonnement met beperkt gebruik tooAzure Rights Management. Dit gratis abonnement is beperkt tooencrypting en ontsleutelen van de instellingen van de onderneming en toepassingsgegevens gesynchroniseerd door Hallo Enterprise State Roaming service; u moet een betaald abonnement toouse Hallo volledige functionaliteit van Azure Rights Management hebben.

Volg deze stappen tooenable Enterprise State Roaming na het verkrijgen van een Azure AD Premium-abonnement:

1. Aanmelding toohello klassieke Azure-portal.
2. Selecteer aan de linkerkant Hallo **ACTIVE DIRECTORY**, en selecteer vervolgens Hallo-directory waarvan u tooenable Enterprise State Roaming wilt.
   ![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming.png)
3. Ga toohello **configureren** tabblad Hallo bovenaan.
   ![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-configure.png)
4. Schuif omlaag Hallo pagina en selecteer **gebruikers kunnen instellingen en ENTERPRISE-APP-gegevens SYNCHRONISEREN**, en klik vervolgens op **opslaan**.
   ![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-select-all-sync-settings.png)

Voor een apparaat tooroam instellingen voor Windows 10 Enterprise State Roaming service Hello, Hallo apparaat moet worden geverifieerd met een Azure AD-identiteit. Voor apparaten die gekoppeld tooAzure AD zijn, is Hallo van primaire gebruikersaanmelding hello Azure AD-identiteit, zodat er geen aanvullende configuratie vereist. Voor apparaten die gebruikmaken van een traditionele on-premises Active Directory, Hallo IT-beheerder moet [hello domeinapparaten tooAzure AD connect voor Windows 10 optreedt](active-directory-azureadjoin-devices-group-policy.md).

## <a name="sync-data-storage"></a>Synchronisatie-gegevensopslag
Enterprise State Roaming gegevens wordt gehost in een of meer [Azure-regio's](https://azure.microsoft.com/regions/) dat beste wordt uitgelijnd met de waarde die Hallo land/regio in hello Azure Active Directory-exemplaar. Enterprise State Roaming gegevens is gepartitioneerd op basis van drie belangrijke geografische regio's: Noord-Amerika, EMEA en APAC. Enterprise State Roaming-gegevens voor de tenant Hallo lokaal bevindt met Hallo geografische regio en wordt niet gerepliceerd tussen regio's.  Bijvoorbeeld, klanten die hun land/regio waarde set tooone EMEA-landen hebben zoals 'Frankrijk' of 'Zambia' hun gegevens hebben gehost in een of Hallo Azure-regio's binnen Europa.  Klanten die hun land/regio-waarde in Azure AD-tooone van Noord-Amerika landen, instellen zoals 'Verenigde Staten' of 'Canada' hun gegevens hebben gehost in een of meer hello Azure-regio's binnen Hallo VS.  Klanten die hun land/regio-waarde in Azure AD-tooone van APAC landen, instellen zoals 'Australië' of 'Nieuw-Zeeland' hun gegevens hebben gehost in een of meer hello Azure-regio's binnen Azië.  Zuid-Amerika landen en Antarctica gegevens zal worden gehost in een of meer Azure-regio's binnen Hallo VS.  Hallo land/regio-waarde is ingesteld als onderdeel van Hallo aanmaakproces voor Azure AD-directory en vervolgens kan niet worden gewijzigd. 

Als u meer informatie over de locatie voor de gegevensopslag moet, neem een ticket met bestand [ondersteuning van Azure](https://azure.microsoft.com/support/options/).

## <a name="manage-enterprise-state-roaming"></a>Enterprise State Roaming beheren
Globale beheerders van Azure AD kunnen inschakelen en uitschakelen van Enterprise State Roaming in Hallo klassieke Azure-portal.
![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-manage.png)

Globale beheerders kunnen instellingen sync toospecific beveiligingsgroepen worden beperkt.

Globale beheerders kunt ook een statusrapport per gebruiker apparaat synchroniseren weergeven door te selecteren van een bepaalde gebruiker in Active Directory-exemplaar Hallo **gebruikers** lijst en klikken op **apparaten** tabblad en de selectie van een weergave **Apparaten synchroniseren instellingen en enterprise-app-gegevens**.
![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-device-sync-settings.png)

## <a name="data-retention"></a>Bewaartijd van gegevens
Gegevens die zijn gesynchroniseerd tooAzure via Enterprise State Roaming, blijven behouden voor onbepaalde tijd tenzij een handmatige delete-bewerking wordt uitgevoerd of Hallo gegevens betreffende bepaald toobe verlopen. 

**Expliciet verwijderen:** Hallo gegevens worden verwijderd wanneer u een Azure-beheerder verwijdert een gebruiker of een map of een beheerder aanvragen expliciet dat er gegevens toobe verwijderd.

* **Verwijderen van een gebruiker**: wanneer een gebruiker wordt verwijderd in Azure AD, Hallo gebruikersaccount roaming gegevens worden gemarkeerd voor verwijdering en tussen de too180 90 dagen wordt verwijderd. 
* **Verwijderen van een Directory**: verwijderen van een volledige map in Azure AD is een directe bewerking. Alle gegevens voor Hallo-instellingen die zijn gekoppeld aan die directory wordt gemarkeerd voor verwijdering en tussen de too180 90 dagen wordt verwijderd. 
* **Op aanvraag verwijdering**: als hello Azure AD-beheerder wil toomanually de gegevens of instellingsgegevens voor een specifieke gebruiker verwijdert, Hallo beheerder een ticket met kunt indienen [ondersteuning van Azure](https://azure.microsoft.com/support/). 

**Verouderde gegevens verwijderen**: gegevens die niet is geopend voor één jaar ('hello bewaarperiode'), worden behandeld als verouderd en kan worden verwijderd uit Azure. Hallo bewaarperiode is onderwerp toochange maar niet minder dan 90 dagen. verouderde gegevens van Hallo mogelijk een specifieke set van Windows-toepassing of alle instellingen voor een gebruiker. Bijvoorbeeld:

* Als u apparaten geen toegang tot een verzameling bepaalde instellingen (bijvoorbeeld een toepassing wordt verwijderd uit het Hallo-apparaat of een instellingengroep zoals 'Thema' is uitgeschakeld voor alle apparaten van een gebruiker), en vervolgens die verzameling na de bewaarperiode hello wordt zijn verouderd en is mogelijk verwijderd. 
* Als een gebruiker heeft de synchronisatie van instellingen op alle apparaten zijn uitgeschakeld, vervolgens geen Hallo instellingsgegevens worden geopend en alle gegevens van Hallo-instellingen voor deze gebruiker wordt verouderd en kunnen worden verwijderd na de bewaarperiode Hallo. 
* Als hello Azure AD-directory-beheerder uitgeschakeld Enterprise State Roaming Hallo gehele Active directory, worden alle gebruikers worden in die map stopt met het synchroniseren van de instellingen en alle instellingsgegevens voor alle gebruikers zullen zijn verouderd en kan worden verwijderd na de bewaarperiode Hallo. 

**Gegevensherstel verwijderd**: Hallo bewaarbeleid voor gegevens kan niet worden geconfigureerd. Zodra het Hallo-gegevens is nu definitief verwijderd, is deze niet worden hersteld. Het is echter belangrijk toonote die Hallo instellingsgegevens worden alleen verwijderd van Azure, niet de apparaten van Hallo-eindgebruikers. Als een apparaat later opnieuw verbinding toohello Enterprise State Roaming service maakt, worden Hallo-instellingen opnieuw gesynchroniseerd en opgeslagen in Azure.

## <a name="related-topics"></a>Verwante onderwerpen
* [Overzicht van Enterprise State Roaming](active-directory-windows-enterprise-state-roaming-overview.md)
* [Instellingen en veelgestelde vragen voor dataroaming](active-directory-windows-enterprise-state-roaming-faqs.md)
* [Instellingen voor beleid en MDM voor synchronisatie van instellingen voor groep](active-directory-windows-enterprise-state-roaming-group-policy-settings.md)
* [Windows 10 zwervende naslaginformatie](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
* [Problemen oplossen](active-directory-windows-enterprise-state-roaming-troubleshooting.md)
