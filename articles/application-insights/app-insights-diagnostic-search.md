---
title: aaaUsing zoeken in Azure Application Insights | Microsoft Docs
description: Zoeken en filteren onbewerkte telemetrie verzonden door uw web-app.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 2a437555-8043-45ec-937a-225c9bf0066b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: df2b0eb017ad48bcdc6ef57d8dff207d120143b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-search-in-application-insights"></a>Met behulp van zoeken in Application Insights
Search is een functie van [Application Insights](app-insights-overview.md) gebruiken toofind en verkennen afzonderlijke telemetrie-items, zoals uitzonderingen, paginaweergaven of web-aanvragen. En u kunt bekijken logboektraceringen en gebeurtenissen die u hebt gecodeerd.

(Voor complexere query's over uw gegevens, gebruikt u [Analytics](app-insights-analytics-tour.md).)

## <a name="where-do-you-see-search"></a>Waar ziet u zoeken?
### <a name="in-hello-azure-portal"></a>In hello Azure-portal
U kunt diagnostische gegevens doorzoeken expliciet openen vanuit Hallo Application Insights overzichtsblade van uw toepassing:

![Open diagnostische gegevens doorzoeken](./media/app-insights-diagnostic-search/01-open-Diagnostic.png)

Ook wordt geopend wanneer u klikt op via bepaalde grafieken en raster artikelen. De filters zijn in dit geval vooraf toofocus ingesteld op Hallo type item dat u hebt geselecteerd. 

Bijvoorbeeld: op de overzichtsblade hello, er is een staafdiagram van aanvragen die zijn geclassificeerd door reactietijd. Klik op via een bereik prestaties toosee een lijst met afzonderlijke aanvragen in dat bereik responstijd:

![Klik in de aanvraag-prestaties](./media/app-insights-diagnostic-search/07-open-from-filters.png)

Hallo-hoofdtekst van Diagnostic Search is een lijst van telemetrie-items - serveraanvragen pagina weergaven en aangepaste gebeurtenissen die u hebt gecodeerd. Boven aan de lijst Hallo is Hallo een overzichtstabel weergegeven aantal gebeurtenissen gedurende een bepaalde periode.

Klik op Vernieuwen tooget nieuwe gebeurtenissen.

### <a name="in-visual-studio"></a>In Visual Studio

In Visual Studio is er ook een venster Application Insights zoeken. Dit is vooral handig voor het weergeven van telemetriegebeurtenissen die worden gegenereerd door Hallo-toepassing die u fouten opspoort. Maar Hallo gebeurtenissen verzameld van uw gepubliceerde app op Hallo Azure-portal ook kan worden weergegeven.

Hallo zoekvenster openen in Visual Studio:

![Visual Studio Application Insights zoeken openen](./media/app-insights-diagnostic-search/32.png)

Hallo zoekvenster heeft functies vergelijkbare toohello web-portal:

![Venster van Visual Studio Application Insights zoeken](./media/app-insights-diagnostic-search/34.png)

Hallo bijhouden bewerking tabblad is beschikbaar wanneer u een aanvraag of een paginaweergave opent. Een ' bewerking ' is een reeks gebeurtenissen die is gekoppeld aan tooa één pagina of de aanvraag voor weergave. Bijvoorbeeld, afhankelijkheidsaanroepen, uitzonderingen, traceerlogboeken en aangepaste gebeurtenissen mogelijk deel uit van een enkele bewerking. Hallo bijhouden bewerking tabblad toont Hallo grafisch timing en duur van deze gebeurtenissen in de relatie toohello aanvraag of pagina. 

## <a name="inspect-individual-items"></a>Afzonderlijke items te inspecteren
Selecteer alle telemetrie-item toosee sleutelvelden en verwante items. Als u wilt dat toosee Hallo volledige set van velden, klikt u op '...'. 

![Klik op Nieuw werkitem, Hallo-velden bewerken en klik op OK.](./media/app-insights-diagnostic-search/10-detail.png)

## <a name="filter-event-types"></a>Typen gebeurtenissen filteren
Open de blade filteren Hallo en kies Hallo gebeurtenis typt u toosee wilt. (Als u later toorestore Hallo filters waarmee u Hallo blade geopend wilt, klikt u op opnieuw instellen.)

![Filter kiest en selecteert u de typen telemetrie](./media/app-insights-diagnostic-search/02-filter-req.png)

Hallo gebeurtenistypen zijn:

* **Tracering** - [diagnostische logboeken](app-insights-asp-net-trace-logs.md) inclusief TrackTrace, log4Net, NLog en System.Diagnostic.Trace aanroepen.
* **Aanvraag** -HTTP-aanvragen ontvangen door de server-toepassing, met inbegrip van pagina's, scripts, afbeeldingen, Stijlbestanden en gegevens. Deze gebeurtenissen zijn gebruikte toocreate Hallo aanvraag en -antwoord overzichtsgrafieken.
* **Paginaweergave** - [telemetrie verzonden door de webclient Hallo](app-insights-javascript.md), toocreate pagina view-rapporten gebruikt. 
* **Aangepaste gebeurtenis** : als u aanroepen tooTrackEvent() ingevoegd in de volgorde te[gebruik controleren](app-insights-api-custom-events-metrics.md), kunt u deze hier zoeken.
* **Uitzondering** : niet-onderschepte [uitzonderingen in Hallo server](app-insights-asp-net-exceptions.md), die u zich aanmeldt met TrackException() en.
* **Afhankelijkheid** - [aanroepen vanuit de servertoepassing](app-insights-asp-net-dependencies.md) tooother services zoals databases of REST-API's en AJAX-aanroepen vanuit uw [clientcode](app-insights-javascript.md).
* **Beschikbaarheid** -resultaten van [beschikbaarheidstests](app-insights-monitor-web-app-availability.md).

## <a name="filter-on-property-values"></a>Filteren op eigenschapswaarden
U kunt gebeurtenissen op Hallo waarden van de eigenschappen op te filteren. Hallo beschikbare eigenschappen, is afhankelijk van Hallo-gebeurtenistypen die u hebt geselecteerd. 

Bijvoorbeeld aanvragen met een specifieke antwoordcode pikken. 

![Vouw een eigenschap en een waarde kiezen](./media/app-insights-diagnostic-search/03-response500.png)

Er zijn geen waarden van een bepaalde eigenschap kiezen heeft Hallo hetzelfde effect als het kiezen van alle waarden. Het verandert filter voor die eigenschap uit.

### <a name="narrow-your-search"></a>Beperk uw zoekopdracht
Kennisgeving die Hallo telt toohello rechts van de filterwaarden Hallo weergeven hoeveel exemplaren er in de huidige gefilterde set Hallo zijn. 

In dit voorbeeld is het wissen dat die Hallo rapportkoptekst/werknemers aanvraag resulteert in de meeste Hallo '500'-fouten:

![Vouw een eigenschap en een waarde kiezen](./media/app-insights-diagnostic-search/04-failingReq.png)




## <a name="find-events-with-hello-same-property"></a>Zoeken naar gebeurtenissen met de Hallo dezelfde eigenschap
Zoeken naar alle Hallo items Hallo dezelfde waarde van eigenschap:

![Met de rechtermuisknop op een eigenschap](./media/app-insights-diagnostic-search/12-samevalue.png)


## <a name="search-hello-data"></a>Hallo zoekgegevens

> [!NOTE]
> toowrite meer complexe query's, open [ **Analytics** ](app-insights-analytics-tour.md) vanaf de bovenkant Hallo van Hallo Search-blade.
> 

U kunt voorwaarden in een van de eigenschapswaarden Hallo zoeken. Dit is vooral handig als u hebt geschreven [aangepaste gebeurtenissen](app-insights-api-custom-events-metrics.md) met eigenschapswaarden. 

U kunt een tijdsbereik als zoekopdrachten via een korter bereik zijn sneller tooset. 

![Open diagnostische gegevens doorzoeken](./media/app-insights-diagnostic-search/appinsights-311search.png)

Zoeken naar volledige woorden, niet subtekenreeksen. Aanhalingstekens tooenclose speciale tekens gebruiken.

| Tekenreeks | is *niet* gevonden door | maar deze worden gevonden |
| --- | --- | --- |
| HomeController.About |thuis<br/>Domeincontroller<br/>out | homecontroller<br/>over<br/>'homecontroller.about'|
|Verenigde Staten|UNI<br/>Ted|Verenigd<br/>statussen<br/>Verenigde Staten en<br/>'Verenigde Staten'

Hier volgen Hallo zoeken expressies die u kunt gebruiken:

| Voorbeeldquery | Effect |
| --- | --- |
| `apple` |Alle gebeurtenissen in Hallo tijdsbereik waarvan de velden Hallo-word "apple bevatten" zoeken |
| `apple AND banana` |Zoeken naar gebeurtenissen die beide woorden bevatten. Gebruik kapitaal 'en', niet 'en'. |
| `apple OR banana`<br/>`apple banana` |Gebeurtenissen die beide woord bevatten zoeken. Gebruik 'Of', niet "of".<br/>Korte vorm. |
| `apple NOT banana` |Gebeurtenissen die bevatten van één woord, maar niet Hallo andere zoeken. |



## <a name="sampling"></a>Steekproeven
Als uw app veel telemetrie genereert (en u Hallo ASP.NET-SDK-versie 2.0.0-beta3 of hoger), Hallo adaptieve steekproeven module vermindert automatisch Hallo volume dat toohello portal wordt verzonden door alleen een representatieve fractie van gebeurtenissen verzenden. Gebeurtenissen die zijn echter gerelateerde toohello dezelfde aanvraag zijn geselecteerd of gedeselecteerd als groep, zodat u tussen gerelateerde gebeurtenissen kunt navigeren. 

[Meer informatie over steekproeven](app-insights-sampling.md).



## <a name="create-work-item"></a>Werkitem maken
U kunt een bug in GitHub of Visual Studio Team Services maken met de Hallo details van elk telemetrie-item. 

![Klik op Nieuw werkitem, Hallo-velden bewerken en klik op OK.](./media/app-insights-diagnostic-search/42.png)

Hallo eerste keer dat u dit doet, tooconfigure wordt u gevraagd een koppeling tooyour Team Services-account en project.

![Hallo-URL van uw Team Services-server en de naam van het Project Hallo vullen en op autoriseren](./media/app-insights-diagnostic-search/41.png)

(U kunt ook Hallo-koppeling configureren op Hallo werkitems blade.)

## <a name="save-your-search"></a>Uw zoekopdracht opslaan
Als u alle gewenste Hallo filters hebt ingesteld, kunt u Hallo zoeken als favoriet opslaan. Als u in een organisatie-account werkt, kunt u kiezen of tooshare met andere teamleden.

![Klik op de favoriet en klik op Opslaan Hallo naam instellen](./media/app-insights-diagnostic-search/08-favorite-save.png)

toosee hello zoeken opnieuw **Ga toohello overzichtsblade** en Favorieten openen:

![Tegel Favorieten](./media/app-insights-diagnostic-search/09-favorite-get.png)

Als u met relatief tijdsbereik opgeslagen, is heropend blade Hallo Hallo meest recente gegevens. Als u met absoluut tijdsbereik opgeslagen, ziet u Hallo dezelfde gegevens elke keer. (Als 'Relatieve' niet beschikbaar als u wilt dat een favoriet toosave, tijdsbereik in Hallo-header op en een periode op die een aangepast bereik niet instellen.)

## <a name="send-more-telemetry-tooapplication-insights"></a>Meer telemetrie tooApplication Insights verzenden
In toevoeging toohello out-of-the-box-telemetrie is verzonden door de Application Insights-SDK, kunt u het volgende doen:

* Logboektraceringen van uw favoriete framework voor logboekregistratie in vastleggen [.NET](app-insights-asp-net-trace-logs.md) of [Java](app-insights-java-trace-logs.md). Dit betekent dat u kunt uw logboektraceringen doorzoeken en ze te correleren met paginaweergaven, uitzonderingen en andere gebeurtenissen. 
* [Schrijven van code](app-insights-api-custom-events-metrics.md) toosend aangepaste gebeurtenissen, paginaweergaven en uitzonderingen. 

[Meer informatie over hoe toosend registreert en aangepaste telemetrie tooApplication Insights](app-insights-asp-net-trace-logs.md).

## <a name="questions"></a>MET Q & A
### <a name="limits"></a>Hoeveel gegevens behouden blijven?

Zie Hallo [limieten samenvatting](app-insights-pricing.md#limits-summary).

### <a name="how-can-i-see-post-data-in-my-server-requests"></a>Hoe kan ik postgegevens zien in mijn serveraanvragen?
Er geen Hallo postgegevens automatisch wordt geregistreerd, maar u kunt [TrackTrace of logboek aanroepen](app-insights-asp-net-trace-logs.md). Hallo postgegevens in Hallo-bericht parameter geplaatst. U kunt niet filteren op het Hallo-bericht in Hallo dezelfde manier kunt u filteren op eigenschappen, maar de maximale grootte Hallo is langer.

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="add"></a>Volgende stappen
* [Schrijven van complexe query's in Analytics](app-insights-analytics-tour.md)
* [Logboeken en aangepaste telemetrie tooApplication Insights verzenden](app-insights-asp-net-trace-logs.md)
* [Beschikbaarheid en reactiesnelheid tests instellen](app-insights-monitor-web-app-availability.md)
* [Problemen oplossen](app-insights-troubleshoot-faq.md)
