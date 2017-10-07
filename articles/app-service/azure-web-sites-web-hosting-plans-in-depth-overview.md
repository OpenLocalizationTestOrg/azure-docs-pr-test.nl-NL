---
title: gedetailleerd overzicht van aaaAzure App Service-plannen | Microsoft Docs
description: Lees hoe App Service-plannen voor Azure App Service werk, en hoe ze uw beheerervaring profiteren.
keywords: App Service, Azure App Service, schaal, schaalbaar, App Service-abonnement, kosten App Service
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: dea3f41e-cf35-481b-a6bc-33d7fc9d01b1
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: byvinyal
ms.openlocfilehash: b384790d9e69b234ca69ac591164c48a4b6ed210
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-plans-in-depth-overview"></a>Gedetailleerd overzicht van de abonnementen voor Azure App Service

App Service-abonnementen vertegenwoordigen Hallo-verzameling van fysieke resources gebruikt toohost uw apps.

In App Service-plannen wordt het volgende gedefinieerd:

- Regio (VS-West, VS-Oost, enz.)
- Schaalaanpassingsaantal (een, twee, drie exemplaren, enz.)
- De exemplaargrootte van het (klein, normaal, groot)
- SKU (Free, Shared, Basic, Standard, Premium)

Web-Apps, Mobile Apps, API-Apps, Apps van de functie (of functies), in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) alle uitvoeren in een App Service-plan.  Apps in Hallo hetzelfde abonnement en regio een App Service-abonnement kunt delen. 

Alle toepassingen toegewezen tooan **App Service-abonnement** gedefinieerd door het Hallo-resources delen. Deze delen, bespaart geld bij het hosten van meerdere apps in een enkele App Service-abonnement.

Uw **App Service-abonnement** kunt opschalen van **vrije** en **gedeelde** SKU's te**Basic**, **standaard**, en **Premium** SKU's zodat u toegang tot resources toomore en functies langs Hallo manier.

Als uw App Service-abonnement te is ingesteld**Basic** SKU of hoger, en vervolgens u Hallo bepalen kunt **grootte** en aantal Hallo virtuele machines worden geschaald.

Bijvoorbeeld: als het abonnement heeft een geconfigureerde toouse twee 'kleine' exemplaren in de standaard servicelaag hello, uitvoeren alle apps die gekoppeld aan een plan zijn voor beide exemplaren. Apps hebben ook toegangsfuncties toohello standaardservice laag. Plan exemplaren apps waarop zijn volledig beheerde en maximaal beschikbaar.

> [!IMPORTANT]
> Hallo **SKU** en **Scale** Hallo App Service plan bepaalt Hallo kosten en niet Hallo aantal apps die erin worden gehost.

Dit artikel behandelt Hallo belangrijke kenmerken, zoals laag en schaal van een App Service-plan en hoe ze rol spelen bij het beheren van uw apps.

## <a name="apps-and-app-service-plans"></a>Apps en App Service-abonnementen

Een app in App Service kan worden gekoppeld aan slechts één App Service-abonnement op elk moment.

Zowel apps als abonnementen zijn opgenomen in een **resourcegroep**. Een resourcegroep fungeert als Hallo lifecycle grens voor elke bron die binnen het. U kunt resource groepen toomanage alle Hallo gedeelten van een toepassing samen.

Omdat één resourcegroep meerdere App Service-abonnementen hebt kan, kunt u verschillende apps toodifferent fysieke bronnen toewijzen.

U kunt bijvoorbeeld resources tussen de ontwikkeling, testen en productie-omgevingen scheiden. Met afzonderlijke omgevingen voor productie en ontwikkelen en testen, kunt u resources isoleren. Op deze manier load getest op een nieuwe versie van uw apps niet zou concurreren voor Hallo dezelfde bronnen als uw productie-apps, die echte klanten fungeren.

Wanneer u meerdere abonnementen in één resourcegroep hebt, kunt u ook een toepassing die geografische regio's omvat definiëren.

Bijvoorbeeld: een maximaal beschikbare app uitgevoerd in twee gebieden bevat ten minste twee plannen, één voor elke regio en een app die is gekoppeld aan elk plan. In een dergelijke situatie zijn vervolgens alle Hallo kopieën van Hallo app opgenomen in één resourcegroep. Met een resourcegroep met meerdere abonnementen en meerdere apps maakt het eenvoudig toomanage, controle en status van de weergave Hallo van Hallo-toepassing.

## <a name="create-an-app-service-plan-or-use-existing-one"></a>Maken van een App Service-abonnement of bestaande gebruiken

Wanneer u een app maakt, kunt u overwegen een resourcegroep maken. Op Hallo anderzijds, als deze app is een onderdeel voor een grotere toepassing, maakt u dit binnen de resourcegroep Hallo die voor die grotere toepassing toegewezen.

Of Hallo-app een geheel nieuwe toepassing of een deel van een groter voorbeeld is, kunt u kiezen toouse een bestaand plan toohost deze of een nieuwe maken. Deze beslissing is meer een vraag van capaciteit en de verwachte belasting.

Het is raadzaam het isoleren van uw app in een nieuwe App Service plannen wanneer:

- App is een bronintensieve.
- App heeft verschillende schalen factoren van Hallo andere apps die wordt gehost in een bestaand abonnement.
- App moet resource in een andere geografische regio.

Op deze manier kunt u een nieuwe set bronnen toewijzen voor uw app en meer controle over uw apps te krijgen.

## <a name="create-an-app-service-plan"></a>Een App Service-plan maken

> [!TIP]
> Als u een App Service-omgeving hebt, kunt u Hallo documentatie specifieke tooApp Service-omgevingen hier bekijken: [maken van een App Service-abonnement in een App-serviceomgeving](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)

U kunt een lege App Service-abonnement maken van App Service plan Bladerervaring Hallo of als onderdeel van app maken.

In Hallo [Azure-portal](https://portal.azure.com), klikt u op **nieuw** > **Web en mobiel**, en selecteer vervolgens **Web-App** of een ander type App Service-app.

![Een app maken in hello Azure-portal.][createWebApp]

Vervolgens kunt u selecteren of maken van App Service-plan voor de nieuwe app Hallo Hallo.

 ![Maak een App Service-abonnement.][createASP]

toocreate een App Service-abonnement, klik op **[+] maken nieuwe**, type Hallo **App Service-abonnement** een naam en selecteer vervolgens een geschikte **locatie**. Klik op **prijscategorie**, en selecteer vervolgens een juiste prijscategorie voor Hallo-service. Selecteer **weergeven van alle** tooview meer opties, zoals prijzen **vrije** en **gedeelde**. Nadat u Hallo prijscategorie hebt geselecteerd, klikt u op Hallo **Selecteer** knop.

## <a name="move-an-app-tooa-different-app-service-plan"></a>Verplaatsen van een app tooa verschillende App Service-abonnement

U kunt een app tooa verschillende App Service-abonnement in Hallo verplaatsen [Azure-portal](https://portal.azure.com). U kunt apps verplaatsen tussen plannen zolang Hallo plannen in Hallo zijn dezelfde resourcegroep en de geografische regio.

een app tooanother plan toomove:

- Navigeer toohello app die u toomove wilt.
- In Hallo **Menu**, zoekt u naar Hallo **App Service-Plan** sectie.
- Selecteer **wijziging App Service-abonnement** toostart Hallo proces.

**App Service-abonnement wijzigen** wordt geopend Hallo **App Service-abonnement** selector. Op dit moment kunt u kiezen een bestaand plan toomove deze app in.

> [!IMPORTANT]
> Hallo Selecteer App Service-abonnement UI wordt gefilterd op Hallo volgende criteria:
> - Binnen bestaat Hallo dezelfde resourcegroep
> - Bestaat in Hallo dezelfde geografische regio
> - Binnen bestaat Hallo dezelfde webruimte
>
> Een webruimte is een logische constructie in App Service waarmee een groepering van serverbronnen zijn gedefinieerd. Een geografische regio (zoals VS-West) bevat veel Webspaces in volgorde tooallocate klanten die gebruikmaken van App Service. App Service-resources zijn op dit moment kunnen toobe verplaatst tussen Webspaces niet.
>

![Selector van App Service-plan.][change]

Elk plan heeft zijn eigen prijscategorie. Voor informatie over het verplaatsen van een site van een gratis laag tooa Standard-laag kan bijvoorbeeld alle apps die zijn toegewezen tooit toouse Hallo functies en bronnen van Hallo Standard-laag.

## <a name="clone-an-app-tooa-different-app-service-plan"></a>Klonen van een app tooa verschillende App Service-abonnement

Als u toomove Hallo app tooa andere regio wilt, een alternatief is app klonen. Klonen wordt een kopie van uw app in een nieuw of bestaand App Service-abonnement in elke regio.

U vindt **kloon App** in Hallo **ontwikkelingsprogramma's** gedeelte van Hallo-menu.

> [!IMPORTANT]
> Klonen, is enkele beperkingen die u op over kunt lezen [klonen van de Azure App Service-App met Azure portal](../app-service-web/app-service-web-app-cloning-portal.md).

## <a name="scale-an-app-service-plan"></a>Schalen van een App Service-abonnement

Er zijn drie manieren tooscale een plan:

- **Wijziging Hallo abonnement de prijscategorie**. Een plan in de basisstaffel Hallo kunt geconverteerde tooStandard, en alle apps toegewezen tooit toouse Hallo functies van Hallo Standard-laag.
- **Wijzig de exemplaargrootte van het plan Hallo**. Als u bijvoorbeeld mag een plan in de basisstaffel Hallo die gebruikmaakt van kleine exemplaren zijn gewijzigde toouse grote exemplaren. Alle apps die gekoppeld aan een plan nu zijn kunnen Hallo extra geheugen en CPU-bronnen die grotere exemplaar grootte aanbiedingen Hallo gebruiken.
- **Aantal exemplaren op Hallo-abonnement wijzigen**. Een standaard-plan toothree exemplaren wordt uitgebreid kan bijvoorbeeld geschaalde too10 exemplaren. Premium-abonnement kan worden uitgebreid tot too20 exemplaren (onderwerp tooavailability). Alle apps die gekoppeld aan een plan nu zijn kunnen Hallo extra geheugen en CPU-bronnen die grotere exemplaar aantal aanbiedingen Hallo gebruiken.

Kunt u Hallo prijscategorie laag en de exemplaar-grootte door te klikken op Hallo **omhoog schalen** item onder instellingen voor Hallo app of Hallo App Service-abonnement. Wijzigingen toepassen toohello App Service-abonnement en van invloed zijn op alle apps die deze als host fungeert.

 ![Stel tooscale waarden van een app.][pricingtier]

## <a name="app-service-plan-cleanup"></a>App Service plan opschonen

> [!IMPORTANT]
> **App Service-plannen** die geen apps die zijn gekoppeld toothem nog steeds kosten omdat ze nog steeds tooreserve Hallo rekencapaciteit hebben.

tooavoid onverwachte kosten, wanneer de laatste app Hallo gehost in een App Service-abonnement wordt verwijderd, Hallo resulterende lege App Service-abonnement wordt ook verwijderd.

## <a name="summary"></a>Samenvatting

App Service-abonnementen vertegenwoordigen een reeks functies en mogelijkheden die u in uw apps delen kunt. App Service-plannen kunt u Hallo flexibiliteit tooallocate specifieke apps tooa set resources en het gebruik van uw Azure-resource verder te optimaliseren. Op deze manier als u wilt dat toosave money op de testomgeving kunt u een plan voor meerdere apps delen. U kunt ook doorvoer voor uw productieomgeving maximaliseren door schalen in meerdere regio's en plannen.

## <a name="whats-changed"></a>Wat is er gewijzigd

- Zie voor een wijziging van de toohello handleiding van Websites tooApp Service: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)

[pricingtier]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/appserviceplan-pricingtier.png
[assign]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/assing-appserviceplan.png
[change]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/change-appserviceplan.png
[createASP]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-appserviceplan.png
[createWebApp]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-web-app.png
