---
title: aaaExploring metrische gegevens in Azure Application Insights | Microsoft Docs
description: Hoe toointerpret op metrische explorer-grafieken en hoe toocustomize metrische explorer blades.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 1f471176-38f3-40b3-bc6d-3f47d0cbaaa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: bwren
ms.openlocfilehash: b77ae227ae61e800ad6f3af8a05cd123ea1d69e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="exploring-metrics-in-application-insights"></a>Verkennen van metrische gegevens in Application Insights
Metrische gegevens in [Application Insights] [ start] zijn gemeten waarden en het aantal gebeurtenissen die worden verzonden in de telemetrie van uw toepassing. Ze helpen u bij het detecteren van prestatieproblemen en bekijk hoe trends in hoe uw toepassing wordt gebruikt. Er is een breed scala aan standard metrische gegevens en u kunt ook uw eigen aangepaste metrische gegevens en gebeurtenissen maken.

Aantal metrische gegevens en gebeurtenissen worden weergegeven in de grafieken van de geaggregeerde waarden zoals optellen, gemiddelden of aantallen.

Hier volgt een voorbeeld reeks grafieken:

![](./media/app-insights-metrics-explorer/01-overview.png)

U vindt metrische gegevens grafieken overal in Hallo Application Insights-portal. In de meeste gevallen kan worden aangepast en u kunt meer grafieken toohello blade toevoegen. Hallo overzicht blade doorklikken toomore gedetailleerde grafieken (die titels zoals 'Servers'), of klik op **Metrics Explorer** tooopen een nieuwe blade waarin u aangepaste grafieken kunt maken.

## <a name="time-range"></a>Tijdsbereik
Hallo tijdsbereik Hallo grafieken of rasters op een blade vallen, kunt u wijzigen.

![Overzichtsblade Open Hallo van uw toepassing hello Azure-portal](./media/app-insights-metrics-explorer/03-range.png)

Als u binnen enkele gegevens die nog niet zijn geregistreerd verwacht, klikt u op vernieuwen. Grafieken vernieuwd met een interval, maar hello-intervallen zijn langer van grotere tijdsbereik. Het kan even toocome via Hallo analysis pipeline gegevens naar een diagram duren.

toozoom in deel van een grafiek Sleep eroverheen:

![Sleep over een deel van een diagram.](./media/app-insights-metrics-explorer/12-drag.png)

Klik op Hallo ongedaan zoomen knop toorestore deze.

## <a name="granularity-and-point-values"></a>Samenvattingen en punt waarden
De muisaanwijzer op Hallo toodisplay Hallo grafiekwaarden van Hallo metrische gegevens op dat moment.

![Beweeg de muisaanwijzer Hallo over een grafiek](./media/app-insights-metrics-explorer/02-focus.png)

Hallo-waarde van Hallo metriek op een bepaald punt wordt tijdens de voorgaande steekproefinterval Hallo geaggregeerd.

Hallo steekproefinterval of 'granulatie' wordt hello boven aan het Hallo-blade weergegeven.

![Hallo-header van een blade.](./media/app-insights-metrics-explorer/11-grain.png)

U kunt Hallo granulatie Hallo tijd bereik blade aanpassen:

![Hallo-header van een blade.](./media/app-insights-metrics-explorer/grain.png)

Hallo granulariteit beschikbaar, is afhankelijk van Hallo tijdsbereik die u selecteert. Hallo expliciete granulaties zijn alternatieven toohello 'automatisch' verfijning voor Hallo tijdsbereik.


## <a name="editing-charts-and-grids"></a>Grafieken en rasters bewerken
een nieuwe grafiek toohello blade tooadd:

![Kies in Metrics Explorer grafiek toevoegen](./media/app-insights-metrics-explorer/04-add.png)

Selecteer **bewerken** op een bestaande of nieuwe grafiek tooedit wat er wordt weergegeven:

![Selecteer een of meer waarden](./media/app-insights-metrics-explorer/08-select.png)

Hoewel er beperkingen van het Hallo-combinaties die samen kunnen worden weergegeven, kunt u meer dan een waarde in een grafiek weergeven. Als u een waarde, aantal Hallo die andere protocollen zijn uitgeschakeld.

Als u gecodeerde [aangepaste metrische gegevens] [ track] in uw app (aanroepen tooTrackMetric en TrackEvent) ze worden hier vermeld.

## <a name="segment-your-data"></a>Segmenteren van uw gegevens
U kunt een waarde splitsen door eigenschap - bijvoorbeeld toocompare paginaweergaven op clients met verschillende besturingssystemen worden uitgevoerd.

Selecteer een grafiek of het raster, switch voor de groepering en kies een eigenschap toogroup door:

![Selecteer groepering op set en selecteer vervolgens een eigenschap in Group By](./media/app-insights-metrics-explorer/15-segment.png)

> [!NOTE]
> Wanneer u groepering gebruikt, geef Hallo gebied en staafdiagram typen een gestapelde weergave. Dit is geschikt waarbij Hallo aggregatiemethode Sum. Maar wanneer Hallo samenvoegingstype gemiddelde, ervoor kiezen de Hallo Line- of het raster weergave typen.
>
>

Als u gecodeerde [aangepaste metrische gegevens] [ track] in uw app en ze waarden van eigenschappen bevatten, u kunt tooselect Hallo-eigenschap in Hallo-lijst.

Is Hallo-diagram te klein voor gesegmenteerde gegevens? De hoogte aanpassen:

![Hallo schuifregelaar aanpassen](./media/app-insights-metrics-explorer/18-height.png)

## <a name="aggregation-types"></a>Aggregatietypen
Hallo legenda Hallo side standaard geeft meestal Hallo geaggregeerd waarde gedurende de periode Hallo van Hallo-grafiek. Als u de muisaanwijzer op Hallo grafiek, toont het Hallo-waarde op dat moment.

Elk gegevenspunt op Hallo grafiek is een totaal van Hallo gegevenswaarden in de vorige steekproef nemen interval of 'granulatie' hello ontvangen. Hallo granulatie Hallo boven aan het Hallo-blade wordt weergegeven en is afhankelijk van Hallo algehele tijdschaal van Hallo-grafiek.

Metrische gegevens kunnen op verschillende manieren worden samengevoegd:

* **Aantal** is een telling van Hallo-gebeurtenissen ontvangen in Hallo steekproefinterval. Het wordt gebruikt voor gebeurtenissen zoals aanvragen. Verschillen in de Hallo hoogte van de grafiek Hallo geeft variaties in Hallo snelheid waarmee Hallo gebeurtenissen plaatsvinden. Maar houd er rekening mee dat Hallo numerieke waarde verandert wanneer u Hallo steekproefinterval wijzigt.
* **Som** Hallo waarden van alle Hallo gegevenspunten ontvangen via Hallo steekproefinterval of Hallo periode van Hallo grafiek worden toegevoegd.
* **Gemiddelde** delen Hallo som door Hallo aantal gegevenspunten ontvangen via hello-interval.
* **Unieke** tellingen voor aantallen gebruikers en -accounts worden gebruikt. Via Hallo steekproefinterval of gedurende de periode Hallo van grafiek Hallo ziet Hallo afbeelding u Hallo-telling van andere gebruikers in die tijd weergegeven.
* **%**-percentage versies van elke aggregatie worden alleen gebruikt met gesegmenteerde grafieken. Hallo totale wordt altijd een too100% en Hallo diagram toont de relatieve bijdrage Hallo van verschillende onderdelen van een totaal.

    ![Percentage aggregatie](./media/app-insights-metrics-explorer/percentage-aggregation.png)

### <a name="change-hello-aggregation-type"></a>Hallo samenvoegingstype wijzigen

![Hallo grafiek bewerken en selecteer vervolgens aggregatie](./media/app-insights-metrics-explorer/05-aggregation.png)

Hallo standaardmethode voor elke waarde wordt weergegeven wanneer u een nieuwe grafiek of wanneer alle metrische gegevens zijn uitgeschakeld:

![Schakel alle metrische gegevens toosee Hallo standaardwaarden](./media/app-insights-metrics-explorer/06-total.png)

## <a name="pin-y-axis"></a>Y-as pincode 
Standaard bevat een grafiek Y-as waarden vanaf nul tot de maximale waarden in het gegevensbereik hello, toogive een visuele representatie van quantum van Hallo waarden. Maar in sommige gevallen meer dan Hallo quantum mogelijk interessant toovisually inspecteren kleine wijzigingen in waarden. Voor aanpassingen als Hallo dit gebruik y-as bewerken functie toopin Hallo y-as minimum of maximum bereikwaarde op het gewenste plaats.
Klik op 'Advanced instellingen' selectievakje toobring up Hallo bereik voor y-as instellingen

![Klik op Geavanceerde instellingen aangepast bereik, en selecteer min max-waarden opgeven](./media/app-insights-metrics-explorer/y-axis-range.png)

## <a name="filter-your-data"></a>Filter uw gegevens
toosee alleen Hallo metrische gegevens voor een geselecteerde set met eigenschapswaarden:

![Klik op Filter, vouw een eigenschap en sommige waarden controleren](./media/app-insights-metrics-explorer/19-filter.png)

Als u geen waarden voor een bepaalde eigenschap selecteert, is deze gelijk aan te vinken ze allemaal Hallo: Er is geen filter op die eigenschap.

Kennisgeving Hallo telt van gebeurtenissen naast elke eigenschapswaarde. Wanneer u de waarden van een eigenschap selecteert, telt Hallo naast een andere eigenschap waarden worden aangepast.

Tooall hello grafieken toepassen filters op een blade. Als u verschillende filters zijn toegepast toodifferent grafieken, maken en opslaan van andere metrische gegevens blades. Als u wilt, kunt u diagrammen in verschillende blades toohello dashboard vastmaken zodat u ze naast elkaar kan zien.

### <a name="remove-bot-and-web-test-traffic"></a>Verkeer van bot en web-test verwijderen
Gebruik Hallo filter **daadwerkelijk of synthetisch verkeer** en Controleer **echte**.

U kunt ook filteren op **bron van synthetisch verkeer**.

### <a name="tooadd-properties-toohello-filter-list"></a>tooadd eigenschappen toohello-filterlijst
Wilt u toofilter telemetrie voor een categorie van uw eigen kiezen? Bijvoorbeeld, misschien verdeelt u van uw gebruikers in verschillende categorieën en u wilt dat uw gegevens te segmenteren in deze categorieën.

[Maak uw eigen eigenschap](app-insights-api-custom-events-metrics.md#properties). Stel deze een [telemetrie initialisatiefunctie](app-insights-api-custom-events-metrics.md#defaults) toohave wordt dit weergegeven in alle telemetrie - inclusief Hallo standaard telemetrie verzonden door de verschillende SDK-modules.

## <a name="edit-hello-chart-type"></a>Hallo grafiektype bewerken
Merk op dat u tussen rasters en diagrammen kunt maken schakelen kunt:

![Selecteer een raster of de grafiek en een grafiektype kiezen](./media/app-insights-metrics-explorer/16-chart-grid.png)

## <a name="save-your-metrics-blade"></a>De blade metrische gegevens opslaan
Wanneer u sommige grafieken hebt gemaakt, kunt u ze als favoriet opslaan. U kunt kiezen of tooshare met andere teamleden, als u een organisatie-account gebruiken.

![Kies favoriet](./media/app-insights-metrics-explorer/21-favorite-save.png)

Hallo blade opnieuw toosee **Ga toohello overzichtsblade** en Favorieten openen:

![Kies in de overzichtsblade Hallo Favorieten](./media/app-insights-metrics-explorer/22-favorite-get.png)

Als u relatief tijdsbereik kiest wanneer u hebt opgeslagen, wordt met de meest recente metrische gegevens Hallo Hallo blade bijgewerkt. Als u een absoluut tijdsbereik kiest, wordt het weergegeven Hallo dezelfde gegevens elke keer.

## <a name="reset-hello-blade"></a>Hallo-blade opnieuw instellen
Als u een blade bewerken, maar vervolgens de gewenste tooget back toohello oorspronkelijke opgeslagen instellen, klikt u op opnieuw instellen.

![In de knoppen Hallo Hallo boven aan het metriek Explorer](./media/app-insights-metrics-explorer/17-reset.png)

## <a name="live-metrics-stream"></a>Stream Live metrische gegevens

Uw telemetrie veel meer direct wilt bekijken, opent u [Live Stream](app-insights-live-stream.md). De meeste metrische gegevens nemen een paar minuten tooappear, vanwege Hallo-proces voor aggregatie. Daarentegen zijn live metrische gegevens geoptimaliseerd voor lage latentie. 

## <a name="set-alerts"></a>Waarschuwingen instellen
op de hoogte met e-mailadres van ongebruikelijke waarden van een metriek toobe een waarschuwing toevoegen. U kunt toohello accountbeheerders voor toosend Hallo e of e-mailadressen toospecific.

![Kies in Metrics Explorer waarschuwingsregels, waarschuwing toevoegen](./media/app-insights-metrics-explorer/appinsights-413setMetricAlert.png)

[Meer informatie over waarschuwingen][alerts].


## <a name="continuous-export"></a>Continuous Export
Als u gegevens continu exporteren wilt, zodat u deze extern kan verwerken, kunt u overwegen [continue export](app-insights-export-telemetry.md).

### <a name="power-bi"></a>Power BI
Als u nog meer weergaven van uw gegevens wilt, kunt u [tooPower BI exporteren](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx).

## <a name="analytics"></a>Analytische gegevens
[Analytics](app-insights-analytics.md) is een flexibeler manier tooanalyze uw telemetrie met behulp van een krachtige querytaal. Te gebruiken als u toocombine wilt berekenen van de resultaten van de metrische gegevens, of een diepgaande exploratie van recente prestaties van uw app uitvoeren. 

In een grafiek metrische, klikt u op Hallo Analytics pictogram tooget rechtstreeks toohello gelijkwaardige Analytics-query.

## <a name="troubleshooting"></a>Problemen oplossen
*Ik zie niet alle gegevens in de grafiek.*

* Tooall hello grafieken toepassen filters op Hallo-blade. Zorg ervoor dat u een filter dat alle Hallo gegevens op een andere uitsluit niet instellen terwijl u te op één grafiek focussen bent.

    Als u tooset verschillende filters in verschillende grafieken wilt, maken ze in verschillende blades, opslaan als afzonderlijke Favorieten. Als u wilt, kunt u ze vastmaken als toohello dashboard zodat u ze naast elkaar kan zien.
* Als u een grafiek met een eigenschap die niet is gedefinieerd op Hallo metriek groepeert, wordt er niets op Hallo-grafiek. Wist u 'groeperen op' of kies een verschillende groepeerniveaus-eigenschap.
* Prestatiegegevens (CPU, i/o-snelheid, enzovoort) is beschikbaar voor Java-web-services, Windows desktop-apps, [IIS web-apps en services als u de statusmonitor installeren](app-insights-monitor-performance-live-website-now.md), en [Azure Cloud Services](app-insights-azure.md). Het is niet beschikbaar voor Azure websites.

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Volgende stappen
* [Gebruik met Application Insights controleren](app-insights-web-track-usage.md)
* [Met behulp van diagnostische gegevens doorzoeken](app-insights-diagnostic-search.md)

<!--Link references-->

[alerts]: app-insights-alerts.md
[start]: app-insights-overview.md
[track]: app-insights-api-custom-events-metrics.md
