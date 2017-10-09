---
title: aaaAnalyzing Trends in Visual Studio | Microsoft Docs
description: Trends analyseren, visualiseren en verkennen in uw Application Insights Telemetry in Visual Studio.
services: application-insights
documentationcenter: .net
author: numberbycolors
manager: carmonm
ms.assetid: 3150c6fc-2691-44f6-a290-fc5cd68e692a
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: bwren
ms.openlocfilehash: 5c623ec040363f05e80ca927dc8855eb016adc99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="analyzing-trends-in-visual-studio"></a>Trends analyseren in Visual Studio
Hallo Application Insights Trends hulpprogramma visualiseren hoe uw webtoepassing belangrijk telemetrische gebeurtenissen wijzigen gedurende een periode, zodat u snel identificeren van problemen en afwijkingen. Gedetailleerde diagnostische informatie, koppelt u toomore Trends kunt u de prestaties van uw app verbeteren, sporen Hallo oorzaken van uitzonderingen en inzicht in uw aangepaste gebeurtenissen onthullen.

![Voorbeeld Trends-venster](./media/app-insights-visual-studio-trends/app-insights-trends-hero-750.png)

## <a name="configure-your-web-app-for-application-insights"></a>Uw web-app configureren voor Application Insights

[Configureer uw web-app voor Application Insights](app-insights-overview.md) als u dit nog hebt gedaan. Hiermee kunt toosend telemetrie toohello Application Insights-portal. Hallo Trends wordt gelezen Hallo telemetrie van daaruit.

Application Insights Trends is beschikbaar in Visual Studio 2015 Update 3 en hoger.

## <a name="open-application-insights-trends"></a>Open Application Insights Trends
tooopen hello Trends in Application Insights-venster:

* Kies in de Application Insights werkbalkknop Hallo **verkennen telemetrie Trends**, of
* Kies in het contextmenu Hallo-project, **Application Insights > verkennen telemetrie Trends**, of
* Kies in de menubalk van Hallo Visual Studio **weergave > Overige vensters > Application Insights Trends**.

U ziet mogelijk een prompt tooselect een resource. Klik op **selecteert u een resource**, meld u aan met een Azure-abonnement en kies vervolgens een Application Insights-resource in Hallo lijst waarvoor u tooanalyze telemetrie trends wilt.

## <a name="choose-a-trend-analysis"></a>Kies een trendanalyse
![Menu van algemene typen trendanalyse](./media/app-insights-visual-studio-trends/app-insights-trends-1-750.png)

Aan de slag door een van vijf algemene trend analyses, elke analyseren van gegevens van de afgelopen 24 uur hello te kiezen:

* **Onderzoeken van prestatieproblemen met uw serveraanvragen** -aanvragen gedaan tooyour service, gegroepeerd op reactietijden
* **Fouten in uw serveraanvragen analyseren** -aanvragen gedaan tooyour service, gegroepeerd op HTTP-antwoordcode
* **Hallo uitzonderingen in uw toepassing onderzoeken** -uitzonderingen van uw service, gegroepeerd op uitzonderingstype
* **Controleer de prestaties van de afhankelijkheden van uw toepassing hello** -Services die worden aangeroepen door uw service, gegroepeerd op reactietijden
* **Uw aangepaste gebeurtenissen controleren** - Aangepaste gebeurtenissen die u hebt ingesteld voor uw service, gegroepeerd op gebeurtenistype.

Deze vooraf gemaakte analyses kunnen later vanaf Hallo **algemene typen telemetrie analysis weergeven** knop in Hallo linkerbovenhoek van Hallo Trends venster.

## <a name="visualize-trends-in-your-application"></a>Trends in uw toepassing visualiseren
Application Insights Trends maakt een tijdreeksvisualisatie vanaf de telemetrie van uw app. Elke keer reeksvisualisatie geeft een soort telemetrie, gegroepeerd op een eigenschap van die telemetrie over een bepaalde tijdspanne. U kunt bijvoorbeeld tooview serververzoeken, gegroepeerd op Hallo land waarvan ze afkomstig is, via Hallo afgelopen 24 uur. In dit voorbeeld zou elke bel op Hallo visualisatie gedurende één uur een telling van Hallo serveraanvragen voor sommige land/regio vertegenwoordigen.

Hallo-opties gebruiken bovenaan Hallo Hallo venster tooadjust welke typen telemetrie weergeven. Kies eerst Hallo telemetrie typen waarin u geïnteresseerd bent in:

* **Telemetrytype** - Serveraanvragen, uitzonderingen, afhankelijkheden of aangepaste gebeurtenissen
* **Tijdsbereik** - overal van Hallo afgelopen 30 minuten toohello afgelopen 3 dagen
* **Groeperen op** - uitzonderingstype, probleem-id, land/regio en meer.

Klik vervolgens op **analyseren telemetrie** toorun Hallo query.

toonavigate tussen bellen in Hallo visualisatie:

* Klik op tooselect een bel die updates Hallo filters onderaan Hallo Hallo venster alleen Hallo-gebeurtenissen die is opgetreden tijdens een bepaalde periode samenvatten
* Dubbelklik op een zoekprogramma belgrootte toonavigate toohello en alle Hallo afzonderlijke telemetrische gebeurtenissen die is opgetreden tijdens deze periode
* Terwijl u CTRL ingedrukt houdt een belgrootte toode-Selecteer in het Hallo-visualisatie.

> [!TIP]
> Hallo Trends en zoekt u hulpprogramma's werken samen toohelp lokaliseren van Hallo oorzaken van problemen in uw service tussen duizenden telemetrische gebeurtenissen. Als uw klanten bijvoorbeeld ‘s middags melden dat uw app minder reageert, start dan met Trends. Analyseer aanvragen tooyour service via Hallo afgelopen paar uur, gegroepeerd op reactietijd. Kijk of er een ongebruikelijk groot cluster van trage aanvragen is. Dubbelklikt u op dat belgrootte toogo toohello zoeken hulpprogramma, gefilterde toothose gebeurtenissen. In een zoekvak, kunt u Hallo inhoud van deze aanvragen verkennen en navigeer toohello code tooresolve Hallo probleem wordt betrokken.
> 
> 

## <a name="filter"></a>Filteren
Ontdek meer specifieke trends Hallo filter controlemechanismen Hallo Hallo venster onderaan in. tooapply een filter, klik op de naam ervan. U kunt snel schakelen tussen verschillende filters toodiscover trends kunnen worden verborgen in een bepaalde dimensie van uw telemetrie. Als u een filter in één dimensie, zoals het uitzonderingstype toepassen, blijven filters in andere dimensies klikbaar ondanks dat ze uitgegrijsd. tooun-een filter toepassen, klikt u op het opnieuw. CTRL ingedrukt tooselect meerdere filters in Hallo dezelfde dimensie.

![Trendfilters](./media/app-insights-visual-studio-trends/TrendsFiltering-750.png)

Wat gebeurt er als u wilt dat de tooapply meerdere filters? 

1. Hallo eerste filter toepassen. 
2. Klik op Hallo **geselecteerde filters toepassen en opnieuw vragen** knop met de naam van de dimensie van het eerste filter Hallo Hallo. Uw telemetrie voor alleen gebeurtenissen die overeenkomen met het eerste filter Hallo dit opnieuw een query. 
3. Een tweede filter toepassen. 
4. Herhaal Hallo proces toofind trends in specifieke subreeksen van uw telemetrie. Bijvoorbeeld serveraanvragen met de naam "GET Home/Index" *en* die afkomstig zijn van Duitsland *en* die een 500 antwoordcode ontvangen. 

tooun-een van deze filters toepassen, klikt u op Hallo **geselecteerde filters te verwijderen en opnieuw opvragen** knop voor de dimensie Hallo.

![Meerdere filters](./media/app-insights-visual-studio-trends/TrendsFiltering2-750.png)

## <a name="find-anomalies"></a>Afwijkingen vinden
Hallo Trends hulpprogramma bellen van gebeurtenissen die afwijkende vergeleken tooother bellen in Hallo zijn kunt markeren dezelfde reeks tijd. Kies in de vervolgkeuzelijst Hallo weergavetype **telt in tijdsinterval (markeren afwijkingen)** of **Percentages in tijdsinterval (markeren afwijkingen)**. Rode bellen zijn afwijkend. Afwijkingen worden gedefinieerd als bellen met aantallen/percentages van meer dan 2.1 keren Hallo standaardafwijking van Hallo aantallen/percentages die is opgetreden in Hallo voorbij twee perioden (48 uur als u hello bekijkt afgelopen 24 uur, enzovoort).

![Gekleurde punten geven aan afwijkingen aan](./media/app-insights-visual-studio-trends/TrendsAnomalies-750.png)

> [!TIP]
> Markering van afwijkingen wordt met name handig voor het vinden van uitschieters in tijdreeks van kleine bellen die er anders mogelijk gelijkaardig uitzien.  
> 
> 

## <a name="next"></a>Volgende stappen
|  |  |
| --- | --- |
| **[Met Application Insights werken in Visual Studio](app-insights-visual-studio.md)**<br/>Telemetrie zoeken, data in CodeLens bekijken en configureren van Application Insights. Allen vanuit Visual Studio. |![Met de rechtermuisknop op het Hallo-project en kies Application Insights zoeken](./media/app-insights-visual-studio-trends/34.png) |
| **[Meer gegevens toevoegen](app-insights-asp-net-more.md)**<br/>Bewaak het gebruik, de beschikbaarheid, de afhankelijkheden en de uitzonderingen. Integreer bijgehouden informatie uit frameworks voor logboekregistratie. Schrijf aangepaste telemetrie. |![Visual Studio](./media/app-insights-visual-studio-trends/64.png) |
| **[Werken met Hallo Application Insights-portal](app-insights-dashboards.md)**<br/>Dashboards, krachtige hulpprogramma's voor diagnose en analyse, waarschuwingen, een live afhankelijkheidskaart van uw toepassing en exportmogelijkheden voor telemetrie. |![Visual Studio](./media/app-insights-visual-studio-trends/62.png) |

