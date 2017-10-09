---
title: aaaDashboards en navigatie in hello Azure Application Insights | Microsoft Docs
description: Weergaven maken van uw belangrijkste APM-grafieken en query's.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 39b0701b-2fec-4683-842a-8a19424f67bd
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 58811388205643bb672e0405b3226f12d0f447a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="navigation-and-dashboards-in-hello-application-insights-portal"></a>Navigatie en Dashboards in Hallo Application Insights-portal
Nadat u hebt [Application Insights instellen op uw project](app-insights-overview.md), telemetriegegevens over de prestaties en het gebruik van uw app wordt weergegeven in uw project Application Insights-resource in Hallo [Azure-portal](https://portal.azure.com).

## <a name="find-your-telemetry"></a>Uw telemetrie vinden
Meld u aan toohello [Azure-portal](https://portal.azure.com) en navigeer toohello Application Insights-resource die u hebt gemaakt voor uw app.

![Klik op Bladeren en selecteer Application Insights en vervolgens uw app.](./media/app-insights-dashboards/00-start.png)

Hallo overzichtsblade (pagina) voor uw app bevat een overzicht van Hallo belangrijkste diagnostische metrische gegevens van uw app en is een gateway toohello andere functies van Hallo-portal.

![Primaire routes tooview uw telemetrie](./media/app-insights-dashboards/010-oview.png)

U kunt een van de Hallo grafieken en rasters aanpassen en tooa dashboard vastmaken. Op die manier u kunt samenbrengen Hallo sleutel telemetrie van andere apps op een centrale dashboard.

## <a name="dashboards"></a>Dashboards
Hallo eerst te beginnen u ziet nadat u zich aanmeldt toohello [Microsoft Azure-portal](https://portal.azure.com) wordt een dashboard. Hier kunt u overbrengen samen Hallo grafieken die belangrijkste tooyou binnen alle Azure-resources zijn, met inbegrip van telemetrie van [Azure Application Insights](app-insights-overview.md).

![Een aangepaste dashboard.](./media/app-insights-dashboards/31.png)

1. **Navigeer toospecific resources** zoals uw app in Application Insights: gebruik Hallo linkerbalk.
2. **Huidige dashboard Return toohello**, of schakel over recente weergaven tooother: gebruik Hallo vervolgkeuzelijst bovenaan links.
3. **Overschakelen van dashboards**: gebruik Hallo vervolgkeuzemenu op Hallo dashboard titel
4. **Maken, bewerken en dashboards delen** op Hallo dashboard werkbalk.
5. **Hallo dashboard bewerken**: Beweeg de muisaanwijzer over een tegel en gebruik vervolgens de bovenste balk toomove, aanpassen of verwijderen.

## <a name="add-tooa-dashboard"></a>Tooa dashboard toevoegen
Wanneer u een blade of een set van grafieken die interessants kijkt, kunt u een kopie van het toohello dashboard vastmaken. U ziet het volgende keer dat u terugkeert.

![een grafiek toopin Beweeg de muisaanwijzer over het en klik op '...' in de header Hallo.](./media/app-insights-dashboards/33.png)

1. Grafiek toodashboard vastmaken. Er verschijnt een kopie van de grafiek Hallo op Hallo-dashboard.
2. Pincode Hallo hele blade toohello dashboard - blijkt op Hallo dashboard als tegel die u kunt doorklikken.
3. Klik op Hallo linkerbovenhoek tooreturn toohello huidige dashboard. Vervolgens kunt u Hallo vervolgkeuzelijst tooreturn toohello huidige weergave.

U ziet dat de grafieken worden gegroepeerd in tegels: een tegel kan meer dan één grafiek bevatten. U vastmaken Hallo hele tegel toohello dashboard.

Hallo grafiek wordt automatisch vernieuwd met een frequentie die afhankelijk is van de grafiek Hallo tijdsbereik:

* Tijdsbereik up too1 uur: vernieuwen om de 5 minuten
* Bereik 1-24 uur tijd: vernieuwen om de 15 minuten
* Tijdsbereik hierboven 24 uur: (tijdsbereik) / 60.

### <a name="pin-any-query-in-analytics"></a>Een query in Analytics vastmaken
U kunt ook [Analytics vastmaken](app-insights-analytics-using.md#pin-to-dashboard) grafieken tooa [gedeelde](#share-dashboards-with-your-team) dashboard. Hiermee kunt u tooadd grafieken van elke willekeurige query naast Hallo standaard metrische gegevens. 

Resultaten automatisch opnieuw elk uur berekend. Pictogram Hallo op Hallo grafiek toorecalculate onmiddellijk klikt u op. (Browser vernieuwen wordt niet opnieuw worden berekend.)

## <a name="adjust-a-tile-on-hello-dashboard"></a>Een tegel op Hallo dashboard aanpassen
Zodra een tegel op Hallo dashboard, kunt u het kunt aanpassen.

![Beweeg de muisaanwijzer over een grafiek in volgorde tooedit deze.](./media/app-insights-dashboards/36.png)

1. Een grafiek toohello tegel toevoegen.
2. Hallo metriek, groeperen op dimensie en stijl (tabel, grafiek) van een grafiek instellen.
3. Sleep over Hallo diagram toozoom Klik op Hallo ongedaan maken knop tooreset Hallo timespan; filtereigenschappen instellen voor Hallo grafieken op Hallo tegel.
4. Titel van de tegel instellen.

Tegels die zijn vastgemaakt vanuit metrische explorer blades hebben opties voor het bewerken van meer dan tegels die zijn vastgemaakt vanuit een overzichtsblade.

Hallo oorspronkelijke tegel die u hebt vastgemaakt wordt niet beïnvloed door uw wijzigingen.

## <a name="switch-between-dashboards"></a>Schakelen tussen dashboards
U kunt meer dan één dashboard opslaan en tussen deze twee schakelt. Wanneer u een grafiek of blade vastmaken, zijn ze toohello huidige dashboard toegevoegd.

![tooswitch tussen dashboards, klik op Dashboard en selecteer een opgeslagen dashboard. toocreate en opslaan van een nieuw dashboard, klikt u op Nieuw. toorearrange, klikt u op bewerken.](./media/app-insights-dashboards/32.png)

U wellicht bijvoorbeeld één dashboard voor het weergeven van volledig scherm in Hallo team ruimte en een voor algemene ontwikkeling.

Op Hallo dashboard, een blade wordt weergegeven als een tegel: klik op de toogo toohello blade. Een grafiek repliceert Hallo grafiek in de oorspronkelijke locatie.

![Klik op een tegel tooopen Hallo blade vertegenwoordigt](./media/app-insights-dashboards/35.png)

## <a name="share-dashboards"></a>Dashboards delen
Wanneer u een dashboard hebt gemaakt, kunt u het delen met andere gebruikers.

![In de header Hallo dashboard, klikt u op delen](./media/app-insights-dashboards/41.png)

Meer informatie over [functies en toegangsbeheer](app-insights-resources-roles-access-control.md).

## <a name="app-navigation"></a>App-navigatie
overzichtsblade Hello is Hallo gateway toomore informatie over uw app.

* **Een grafiek of tegel** : klik op een tegel of grafiek toosee meer informatie over wat Hiermee wordt weergegeven.

### <a name="overview-blade-buttons"></a>Overzicht blade knoppen
![Overzicht blade bovenste navigatiebalk](./media/app-insights-dashboards/app-overview-top-nav.png)

* [**Metrics Explorer** ](app-insights-metrics-explorer.md) -grafieken van de prestaties en gebruik te maken.
* [**Search** ](app-insights-diagnostic-search.md) - specifieke exemplaren van gebeurtenissen, zoals aanvragen, uitzonderingen, te onderzoeken of meld u traceringen.
* [**Analytics** ](app-insights-analytics.md) -krachtige query's over uw telemetrie.
* **Tijdsbereik** -Hallo bereik weergegeven door alle Hallo grafieken op Hallo blade aanpassen.
* **Verwijder** -Hallo Application Insights-resource voor deze app te verwijderen. U moet ook Verwijder Hallo Application Insights-pakketten van uw app-code of Hallo bewerken [instrumentatiesleutel](app-insights-create-new-resource.md#copy-the-instrumentation-key) in uw app toodirect telemetrie tooa verschillende Application Insights-resource.

### <a name="essentials-tab"></a>Tabblad met essentiële gegevens
* [Instrumentatiesleutel](app-insights-create-new-resource.md#copy-the-instrumentation-key) -deze app resource identificeert.
* Prijzen - functies beschikbaar is en stel volume caps maken.

### <a name="app-navigation-bar"></a>App-navigatiebalk
![Linkernavigatiebalk](./media/app-insights-dashboards/app-left-nav-bar.png)

* **Overzicht** -Return toohello app overzichtsblade.
* **Activiteitenlogboek** -waarschuwingen en Azure Beheergebeurtenissen.
* [**Toegangsbeheer** ](app-insights-resources-roles-access-control.md) -toegang tooteam leden en andere bieden.
* [**Labels** ](../azure-resource-manager/resource-group-using-tags.md) -gebruik tags toogroup uw app met anderen.

ONDERZOEKEN

* [**De toepassingstoewijzing** ](app-insights-app-map.md) -actieve toewijzing Hallo-onderdelen van uw toepassing wordt weergegeven die zijn afgeleid van Hallo afhankelijkheidsinformatie.
* [**Detectie van smartcard** ](app-insights-proactive-diagnostics.md) -recente prestatiewaarschuwingen weergeven.
* [**Livestream** ](app-insights-live-stream.md) : een vaste set nuttig bij het implementeren van een nieuwe build handomdraai maatstaven of foutopsporing.
* [**Beschikbaarheid / Webtests** ](app-insights-monitor-web-app-availability.md) -verzenden reguliere aanvragen tooyour web-app uit rond hallo world.*
* [**Fouten, prestaties** ](app-insights-web-monitor-performance.md) -uitzonderingen, uitvalpercentage en de reactie time-out voor aanvragen tooyour app en voor aanvragen van uw app te[afhankelijkheden](app-insights-asp-net-dependencies.md).
* [**Prestaties** ](app-insights-web-monitor-performance.md) -reactietijd, reactietijden afhankelijkheid.
* [Servers](app-insights-web-monitor-performance.md) -prestatiemeteritems. Beschikbaar als u [Status Monitor installeren](app-insights-monitor-performance-live-website-now.md).
* **Browser** -pagina-weergave en AJAX-prestaties. Beschikbaar als u [instrumenteren uw webpagina's](app-insights-javascript.md).
* **Gebruik** -weergave, gebruiker en sessie aantallen pagina. Beschikbaar als u [instrumenteren uw webpagina's](app-insights-javascript.md).

CONFIGUREREN

* **Aan de slag** -inline-zelfstudie.
* **Eigenschappen** -instrumentatiesleutel, abonnement en de resource-id.
* [Waarschuwingen](app-insights-alerts.md) -metrische configuratie van de waarschuwing.
* [Continue export](app-insights-export-telemetry.md) -exporteren van telemetrie tooAzure opslag configureren.
* [Prestaties testen](app-insights-monitor-web-app-availability.md#performance-tests) -een synthetische werklast op uw website instellen.
* [Quotum en prijzen](app-insights-pricing.md) en [opname steekproeven](app-insights-sampling.md).
* **API-toegang** -maken [release aantekeningen](app-insights-annotations.md) en voor Hallo Data Access-API.
* [**Werkitems** ](app-insights-diagnostic-search.md#create-work-item) -verbinding tooa werk traceringssysteem zodat u fouten tijdens de inspectie van telemetrie kunt maken.

INSTELLINGEN

* [**Hiermee vergrendelt u** ](../azure-resource-manager/resource-group-lock-resources.md) -Azure-resources vergrendelen
* [**Automatiseringsscript** ](app-insights-powershell.md) -een definitie van hello Azure-resource exporteren, zodat u deze als een sjabloon toocreate nieuwe resources gebruiken kunt.


## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Volgende stappen

|  |  |
| --- | --- |
| [Metrics explorer](app-insights-metrics-explorer.md)<br/>Metrische gegevens filteren en segment |![Voorbeeld van de zoekopdracht](./media/app-insights-dashboards/64.png) |
| [Diagnostische gegevens doorzoeken](app-insights-diagnostic-search.md)<br/>Zoeken en gebeurtenissen, gerelateerde gebeurtenissen controleren en maken van fouten |![Voorbeeld van de zoekopdracht](./media/app-insights-dashboards/61.png) |
| [Analytische gegevens](app-insights-analytics.md)<br/>Krachtige querytaal |![Voorbeeld van de zoekopdracht](./media/app-insights-dashboards/63.png) |
