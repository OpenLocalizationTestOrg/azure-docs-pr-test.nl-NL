---
title: Enterprise State Roaming in Azure Active Directory inschakelen | Microsoft Docs
description: Veelgestelde vragen over Enterprise State Roaming-instellingen in Windows-apparaten. Enterprise State Roaming biedt gebruikers een uniforme ervaring via hun Windows-apparaten en minder tijd nodig voor het configureren van een nieuw apparaat.
services: active-directory
keywords: Enterprise-status tijdens roaming windows cloud, het inschakelen van enterprise state roaming
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
ms.openlocfilehash: 77d75f4a647e44f27cd9ba8db5286f1456c3ac66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="enable-enterprise-state-roaming-in-azure-active-directory"></a>Enterprise state roaming inschakelen in Azure Active Directory
Enterprise State Roaming is beschikbaar voor elke organisatie met een Premium Azure Active Directory (Azure AD) abonnement. Zie voor meer informatie over het verkrijgen van een Azure AD-abonnement de [productpagina Azure AD](https://azure.microsoft.com/services/active-directory).

Wanneer u Enterprise State Roaming inschakelt, wordt uw organisatie automatisch verleend licenties voor een gratis abonnement met beperkt gebruik naar Azure Rights Management. Dit gratis abonnement is beperkt tot het versleutelen en ontsleutelen van de instellingen van de onderneming en toepassingsgegevens gesynchroniseerd door de service Enterprise State Roaming; u moet een betaald abonnement op het gebruik van de volledige functionaliteit van Azure Rights Management hebben.

Volg deze stappen voor het inschakelen van Enterprise State Roaming na het verkrijgen van een Azure AD Premium-abonnement:

1. Meld u aan bij de klassieke Azure portal.
2. Selecteer aan de linkerkant **ACTIVE DIRECTORY**, en selecteer vervolgens de map waarvoor u wilt inschakelen Enterprise State Roaming.
   ![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming.png)
3. Ga naar de **configureren** tabblad bovenaan.
   ![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-configure.png)
4. Schuif omlaag in de pagina en selecteer **gebruikers kunnen instellingen en ENTERPRISE-APP-gegevens SYNCHRONISEREN**, en klik vervolgens op **opslaan**.
   ![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-select-all-sync-settings.png)

Het apparaat moet verifiëren met de identiteit van een Azure AD voor een Windows 10-apparaten kunnen roamen instellingen met de service Enterprise State Roaming. Voor apparaten die zijn gekoppeld aan Azure AD, is de primaire aanmelding van de gebruiker de identiteit van de Azure AD, zodat er geen aanvullende configuratie vereist. Voor apparaten die gebruikmaken van een traditionele on-premises Active Directory, de IT-beheerder moet [de domein-apparaten verbinden met Azure AD voor Windows 10 optreedt](active-directory-azureadjoin-devices-group-policy.md).

## <a name="sync-data-storage"></a>Synchronisatie-gegevensopslag
Enterprise State Roaming gegevens wordt gehost in een of meer [Azure-regio's](https://azure.microsoft.com/regions/) dat beste wordt uitgelijnd met de waarde land/regio in de Azure Active Directory-exemplaar. Enterprise State Roaming gegevens is gepartitioneerd op basis van drie belangrijke geografische regio's: Noord-Amerika, EMEA en APAC. Gegevens voor de tenant Enterprise State Roaming lokaal bevindt met de geografische regio en wordt niet gerepliceerd tussen regio's.  Bijvoorbeeld, klanten die hun land/regio waarde worden ingesteld op een van de EMEA-landen, zoals 'Frankrijk' of 'Zambia' hebben hun gegevens die worden gehost in een of van de Azure-regio's binnen Europa.  Klanten die hun land/regio-waarde in Azure AD op een van de landen Noord-Amerika instellen zoals 'Verenigde Staten' of 'Canada' hun gegevens gehost in een of meer van de Azure-regio's binnen de Verenigde Staten hebben.  Klanten die hun land/regio-waarde in Azure AD op een van de landen APAC instellen zoals 'Australië' of 'Nieuw-Zeeland' hun gegevens gehost in een of meer van de Azure-regio's binnen Azië hebben.  Zuid-Amerika landen en Antarctica gegevens zal worden gehost in een of meer Azure-regio's binnen de Verenigde Staten.  De land/regio-waarde is ingesteld als onderdeel van het maakproces van de Azure AD-directory en vervolgens kan niet worden gewijzigd. 

Als u meer informatie over de locatie voor de gegevensopslag moet, neem een ticket met bestand [ondersteuning van Azure](https://azure.microsoft.com/support/options/).

## <a name="manage-enterprise-state-roaming"></a>Enterprise State Roaming beheren
Globale beheerders van Azure AD kunnen inschakelen en uitschakelen van Enterprise State Roaming in de klassieke Azure portal.
![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-manage.png)

Globale beheerders kunnen instellingen voor de synchronisatie met bepaalde beveiligingsgroepen worden beperkt.

Globale beheerders kunnen ook een statusrapport per gebruiker apparaat synchroniseren bekijken door een bepaalde gebruiker selecteren in de Active Directory-exemplaar **gebruikers** lijst en klikken op **apparaten** tabblad en de weergave te selecteren **apparaten synchroniseren instellingen en enterprise-app-gegevens**.
![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-device-sync-settings.png)

## <a name="data-retention"></a>Bewaartijd van gegevens
Gegevens die zijn gesynchroniseerd met Azure via Enterprise State Roaming blijven voor onbepaalde tijd bewaard tenzij een handmatige delete-bewerking wordt uitgevoerd of wordt bepaald dat de betrokken gegevens verlopen. 

**Expliciet verwijderen:** de gegevens worden verwijderd wanneer u een Azure-beheerder verwijdert een gebruiker of een map of een beheerder aanvragen expliciet dat gegevens worden verwijderd.

* **Verwijderen van een gebruiker**: wanneer een gebruiker wordt verwijderd in Azure AD, het gebruikersaccount zwervende wordt gemarkeerd voor verwijdering en tussen 90 tot 180 dagen wordt verwijderd. 
* **Verwijderen van een Directory**: verwijderen van een volledige map in Azure AD is een directe bewerking. Alle instellingsgegevens die zijn gekoppeld aan die directory wordt gemarkeerd voor verwijdering en wordt verwijderd tussen 90 tot 180 dagen. 
* **Op aanvraag verwijdering**: als de beheerder van Azure AD wil Verwijder handmatig de gegevens of instellingsgegevens voor een specifieke gebruiker, de beheerder een ticket met kunt indienen [ondersteuning van Azure](https://azure.microsoft.com/support/). 

**Verouderde gegevens verwijderen**: gegevens die niet is geopend voor één jaar ('de bewaarperiode'), worden behandeld als verouderd en kan worden verwijderd uit Azure. De bewaarperiode kan worden gewijzigd maar niet minder dan 90 dagen. Verouderde gegevens mogelijk een specifieke set van Windows-toepassing of alle instellingen voor een gebruiker. Bijvoorbeeld:

* Als u apparaten geen toegang tot een verzameling bepaalde instellingen (bijvoorbeeld een toepassing wordt verwijderd van het apparaat of een instellingengroep zoals 'Thema' is uitgeschakeld voor alle apparaten van een gebruiker), en vervolgens die verzameling wordt verlopen na de bewaarperiode en kunnen worden verwijderd. 
* Als een gebruiker heeft de synchronisatie van instellingen op alle apparaten zijn uitgeschakeld, klikt u vervolgens geen van de instellingsgegevens wordt geopend en alle instellingsgegevens voor die gebruiker wordt zijn verouderd en kan worden verwijderd na de bewaarperiode. 
* Als de Azure AD-directory-beheerder uitgeschakeld Enterprise State Roaming voor de hele map, worden alle gebruikers wordt in die map stopt met het synchroniseren van de instellingen en alle instellingsgegevens voor alle gebruikers worden verlopen en kan worden verwijderd na de bewaarperiode. 

**Gegevensherstel verwijderd**: het beleid voor het bewaren van gegevens kan niet worden geconfigureerd. Nadat de gegevens is nu definitief verwijderd, is deze niet worden hersteld. Het is echter belangrijk te weten dat de instellingsgegevens alleen worden verwijderd uit Azure, niet de apparaten van eindgebruikers. Als een apparaat later opnieuw verbinding mee met de service Enterprise State Roaming maakt, worden de instellingen opnieuw gesynchroniseerd en opgeslagen in Azure.

## <a name="related-topics"></a>Verwante onderwerpen
* [Overzicht van Enterprise State Roaming](active-directory-windows-enterprise-state-roaming-overview.md)
* [Instellingen en veelgestelde vragen voor dataroaming](active-directory-windows-enterprise-state-roaming-faqs.md)
* [Instellingen voor beleid en MDM voor synchronisatie van instellingen voor groep](active-directory-windows-enterprise-state-roaming-group-policy-settings.md)
* [Windows 10 zwervende naslaginformatie](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
* [Problemen oplossen](active-directory-windows-enterprise-state-roaming-troubleshooting.md)
