---
title: aaaApplication kaart in Azure Application Insights | Microsoft Docs
description: Een visuele presentatie van Hallo afhankelijkheden tussen de onderdelen van de app, voorzien van KPI's en waarschuwingen.
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 3bf37fe9-70d7-4229-98d6-4f624d256c36
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 96ab753a100ea53ec7d367e3559b6622ab6fd182
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="application-map-in-application-insights"></a>De toepassingstoewijzing in Application Insights
In [Azure Application Insights](app-insights-overview.md), toepassingstoewijzing is een visuele indeling van Hallo afhankelijkheidsrelaties tussen onderdelen van uw toepassing. Elk onderdeel toont KPI's zoals belasting, prestaties, fouten en waarschuwingen, toohelp detecteren van de onderdelen die zijn veroorzaakt door een prestatieprobleem of fout. U kunt doorklikken van elk onderdeel toomore gedetailleerde diagnostische gegevens, zoals Application Insights-gebeurtenissen. Als uw app gebruikmaakt van Azure-services, kunt u ook doorklikken tooAzure diagnostische gegevens, zoals SQL Database Advisor aanbevelingen.

U kunt een toepassing kaart toohello Azure-dashboard, waar deze zich volledig functioneel vastmaken zoals andere grafieken. 

## <a name="open-hello-application-map"></a>Open Hallo toepassingstoewijzing
Open Hallo toewijzing van de overzichtsblade Hallo voor uw toepassing:

![Open de app-kaart](./media/app-insights-app-map/01.png)

![App-kaart](./media/app-insights-app-map/02.png)

Hallo-kaart toont:

* Beschikbaarheidstests
* Client-side-onderdeel (bewaakt met Hallo JavaScript SDK)
* Server-side-onderdeel
* Afhankelijkheden van de client- en serveronderdelen Hallo

U kunt uitvouwen en samenvouwen afhankelijkheid koppeling groepen:

![samenvouwen](./media/app-insights-app-map/03.png)

Als er veel afhankelijkheden van een bepaald type (SQL, HTTP-enzovoort), kunnen ze gegroepeerde weergegeven. 

![gegroepeerde afhankelijkheden](./media/app-insights-app-map/03-2.png)

## <a name="spot-problems"></a>Ter plaatse problemen
Elk knooppunt heeft relevante prestatie-indicatoren, zoals Hallo belasting, prestaties en fout tarieven voor het desbetreffende onderdeel. 

De pictogrammen waarschuwing Markeer mogelijke problemen. Een oranje waarschuwing betekent dat er fouten zijn in aanvragen, paginaweergaven of afhankelijkheidsaanroepen. Rood betekent een Faalpercentage 5% of hoger. Als u deze drempels tooadjust wilt, opent u de opties.

![Fout pictogrammen](./media/app-insights-app-map/04.png)

Actieve waarschuwingen ook weergeven van: 

![actieve waarschuwingen](./media/app-insights-app-map/05.png)

Als u SQL Azure gebruikt, is er een pictogram dat ziet u wanneer er zijn aanbevelingen voor hoe u kunt de prestaties verbeteren. 

![Azure aanbeveling](./media/app-insights-app-map/06.png)

Klik op een pictogram tooget meer informatie:

![Azure aanbeveling](./media/app-insights-app-map/07.png)

## <a name="diagnostic-click-through"></a>Diagnostische klik door
Elk knooppunt op Hallo kaart Hallo biedt gerichte klik door voor diagnostische gegevens. Hallo-opties zijn afhankelijk van Hallo type Hallo-knooppunt.

![Serveropties](./media/app-insights-app-map/09.png)

Hallo-opties, voor de onderdelen die worden gehost in Azure, directe koppelingen toothem zijn.

## <a name="filters-and-time-range"></a>Filters en tijdsbereik
Standaard Hallo kaart bevat een overzicht van alle Hallo gegevens beschikbaar voor Hallo gekozen tijdsbereik. Maar u kunt deze filteren tooinclude alleen specifieke bewerking namen of afhankelijkheden.

* Naam van de bewerking: dit omvat zowel paginaweergaven en serverzijde aanvraagtypen. Met deze optie Hallo Hallo kaart toont KPI op Hallo server-clientzijde knooppunt voor bewerkingen alleen Hallo geselecteerd. Hallo afhankelijkheden aangeroepen in de context Hallo van deze specifieke bewerkingen worden weergegeven.
* Basisnaam voor afhankelijkheid: dit omvat Hallo AJAX browser afhankelijkheden en afhankelijkheden van de serverzijde. Als u aangepaste afhankelijkheidstelemetrie Hello TrackDependency API, weergegeven ze ook hier. Hallo afhankelijkheden tooshow op Hallo-kaart, kunt u selecteren. Deze selectie filteren op dit moment niet Hallo serverzijde aanvragen of Hallo clientzijde paginaweergaven.

![Filters instellen](./media/app-insights-app-map/11.png)

## <a name="save-filters"></a>Filters opslaan
toosave hello filters die u hebt toegepast, pincode Hallo gefilterde weergave naar een [dashboard](app-insights-dashboards.md).

![Pincode toodashboard](./media/app-insights-app-map/12.png)

## <a name="error-pane"></a>Foutvenster
Als u op een knooppunt in het Hallo-kaart, wordt een foutvenster weergegeven aan de rechterkant Hallo samenvatten fouten voor dat knooppunt. Fouten zijn gegroepeerd eerst op bewerkings-ID en vervolgens gegroepeerd op probleem-ID.

![Foutvenster](./media/app-insights-app-map/error-pane.png)

Op een fout te klikken, gaat u toohello meest recente exemplaar van deze fout.

## <a name="resource-health"></a>Status van resources
Voor sommige brontypen resourcestatus Hallo boven aan het foutvenster Hallo weergegeven. Bijvoorbeeld, ziet te klikken op een SQL-knooppunt Hallo database status en waarschuwingen die zijn gestart.

![Status van resources](./media/app-insights-app-map/resource-health.png)

U kunt klikken op Hallo resource naam tooview standaard overzicht metrische gegevens voor die bron.

## <a name="end-to-end-system-app-maps"></a>End-to-end-systeem app maps

*SDK-versie 2.3 of hoger vereist*

Als u uw toepassing heeft verschillende onderdelen - bijvoorbeeld een back-endservice bovendien toohello web-app- en u kunt weergeven ze allemaal op één geïntegreerde app-kaart.

![Filters instellen](./media/app-insights-app-map/multi-component-app-map.png)

Hallo app kaart wordt opgezocht serverknooppunten HTTP afhankelijkheid-aanroepen tussen servers met Hallo die Application Insights-SDK geïnstalleerd. Elke Application Insights-resource wordt uitgegaan van één server toocontain.

### <a name="multi-role-app-map-preview"></a>Met meerdere functie-app-kaart (preview)

Hallo preview met meerdere functie-app kaartfunctie kunt u toouse Hallo app kaart met meerdere servers voor het verzenden van gegevens toohello dezelfde Application Insights-resource / instrumentatiesleutel. Servers in kaart Hallo zijn gesegmenteerd op Hallo cloud_RoleName-eigenschap op telemetrie-items. Stel *toepassing van meerdere rollenoverzicht* te*op* Hallo van Previews blade tooenable deze configuratie.

Deze aanpak is het wellicht wenselijk in een toepassing micro-services of in andere scenario's waar u toocorrelate gebeurtenissen op meerdere servers binnen één Application Insights-resource.

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="feedback"></a>Feedback
Geef feedback via Hallo portal feedbackoptie.

![Afbeelding van MapLink-1](./media/app-insights-app-map/13.png)


## <a name="next-steps"></a>Volgende stappen

* [Azure Portal](https://portal.azure.com)
