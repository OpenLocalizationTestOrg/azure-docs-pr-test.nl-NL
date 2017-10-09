---
title: aaaDebug toepassingen met Azure Application Insights in Visual Studio | Microsoft Docs
description: Analyse van web-app-prestaties en diagnostische gegevens tijdens foutopsporing en algemeen gebruik.
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 2059802b-1131-477e-a7b4-5f70fb53f974
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/7/2017
ms.author: bwren
ms.openlocfilehash: 20491fbe4505bf719039e5d1c220b1afec01db25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-applications-with-azure-application-insights-in-visual-studio"></a>Fouten opsporen in uw toepassingen met Azure Application Insights in Visual Studio
In Visual Studio (2015 en hoger) kunt u de prestaties analyseren en problemen in uw ASP.NET web-app identificeren tijdens de foutopsporing en algemeen gebruik. Dit gebeurt aan de hand van telemetrie uit [Azure Application Insights](app-insights-overview.md).

Als u uw ASP.NET-web-app met behulp van Visual Studio 2017 gemaakt of hoger, er al Hallo Application Insights-SDK. Als u dit nog niet hebt gedaan, anders [Application Insights tooyour app toevoegen](app-insights-asp-net.md).

toomonitor uw app wanneer deze in live productie is, u normaal gesproken Hallo Application Insights telemetrie weergeven in Hallo [Azure-portal](https://portal.azure.com), waar u kunt waarschuwingen instellen en krachtige bewakingsprogramma's toepassen. Maar voor foutopsporing, u kunt ook zoeken en analyseren Hallo telemetrie in Visual Studio. U kunt Visual Studio tooanalyze telemetrie van uw productiesite en van foutopsporing wordt uitgevoerd op uw ontwikkelcomputer. In het laatste geval hello, kunt u foutopsporing wordt uitgevoerd analyseren, zelfs als u Hallo SDK toosend telemetrie toohello Azure-portal nog niet hebt geconfigureerd. 

## <a name="run"></a> Fouten opsporen in uw project
Voer uw web-app in de lokale foutopsporingsmodus door op F5 te drukken. Open verschillende pagina's toogenerate telemetrie.

In Visual Studio ziet u een aantal Hallo-gebeurtenissen die zijn geregistreerd door Hallo Application Insights-module in uw project.

![In Visual Studio weergegeven de knop Application Insights Hallo tijdens de foutopsporing.](./media/app-insights-visual-studio/appinsights-09eventcount.png)

Klik op deze knop toosearch uw telemetrie. 

## <a name="application-insights-search"></a>Application Insights-zoekopdracht
Hallo Application Insights zoekvenster worden gebeurtenissen weergegeven die zijn geregistreerd. (Als u tooAzure aangemeld bij het instellen van Application Insights, kunt u zoeken Hallo dezelfde gebeurtenissen in hello Azure-portal.)

![Met de rechtermuisknop op het Hallo-project en kies Application Insights zoeken](./media/app-insights-visual-studio/34.png)

> [!NOTE] 
> Nadat u selecteren of selectie filters opheffen, klikt u op Hallo zoekknop achter Hallo Hallo zoeken tekstveld.
>

zoeken met vrije tekst Hello werkt voor alle velden in het Hallo-gebeurtenissen. Bijvoorbeeld zoeken naar een deel van Hallo-URL van een pagina. of Hallo-waarde van een eigenschap, zoals de clientlocatie, of naar specifieke woorden in een traceringslogboek.

Klik op een gebeurtenis toosee gedetailleerde eigenschappen ervan.

U kunt de code toohello doorklikken voor aanvragen tooyour web-app.

![Klik onder Details aanvragen door toohello code](./media/app-insights-visual-studio/31.png)

U kunt ook verwante items openen toohelp onderzoeken mislukte aanvragen of uitzonderingen.

![Onder aanvraaggegevens, schuif naar beneden toorelated items](./media/app-insights-visual-studio/41.png)

## <a name="view-exceptions-and-failed-requests"></a>Weergave uitzonderingen en mislukte aanvragen
Uitzondering rapporten weergeven in het zoekvenster Hallo. (In sommige oudere typen van ASP.NET-toepassing, hebt u te[instellen uitzonderingenmonitor](app-insights-asp-net-exceptions.md) toosee uitzonderingen die worden verwerkt door het Hallo-framework.)

Klik op een uitzondering tooget een stack-trace. Als Hallo-code van Hallo app openen in Visual Studio, kunt u zich kunt doorklikken van Hallo stack trace toohello relevante coderegel Hallo.

![Uitzondering voor stack-trace](./media/app-insights-visual-studio/17.png)

## <a name="view-request-and-exception-summaries-in-hello-code"></a>Samenvattingen van de aanvraag en uitzondering in Hallo code weergeven
In Hallo Code Lens regel boven elke handler-methode ziet u een aantal van Hallo aanvragen en uitzonderingen die zijn geregistreerd door Application Insights in Hallo afgelopen 24 uur.

![Uitzondering voor stack-trace](./media/app-insights-visual-studio/21.png)

> [!NOTE] 
> Code Lens toont alleen de gegevens voor de Application Insights als er [geconfigureerd van uw app toosend telemetrie toohello Application Insights-portal](app-insights-asp-net.md).
>

[Meer informatie over Application Insights in Code Lens](app-insights-visual-studio-codelens.md)

## <a name="trends"></a>Trends
Trends is een hulpprogramma waarmee u de werking van uw app gedurende een bepaalde periode kunt visualiseren. 

Kies **verkennen telemetrie Trends** van Application Insights-werkbalkknop Hallo of venster Application Insights zoeken. Kies een van vijf algemene query's tooget gestart. U kunt verschillende gegevenssets analyseren op basis van telemetrietypen, tijdsbereik en andere eigenschappen. 

toofind afwijkingen in uw gegevens, kies een van de Hallo afwijkingsdetectie opties onder Hallo 'Weergavetype' vervolgkeuzelijst. Hallo filteropties onderaan Hallo Hallo-venster maken het gemakkelijk toohone in op specifieke subreeksen van uw telemetrie.

![Trends](./media/app-insights-visual-studio/51.png)

[Meer informatie over Trends](app-insights-visual-studio-trends.md).

## <a name="local-monitoring"></a>Lokale bewaking
(Vanaf Visual Studio 2015 Update 2) Als u dit nog niet hebt Hallo SDK toosend telemetrie toohello Application Insights-portal (zo geconfigureerd dat er geen instrumentatiesleutel in ApplicationInsights.config is) geeft de diagnostics-venster Hallo telemetrie van de meest recente foutopsporingssessie. 

Dit is handig als u al een eerdere versie van uw app hebt gepubliceerd. U wilt niet dat Hallo telemetrie van uw foutopsporing sessies toobe verward met Hallo telemetrie over Hallo Hallo gepubliceerde app Application Insights-portal.

Het is ook handig als u beschikt over sommige [aangepaste telemetrie](app-insights-api-custom-events-metrics.md) dat u wilt dat toodebug voor het verzenden van telemetrie toohello portal.

* *Volledig geconfigureerd ik aanvankelijk Application Insights toosend telemetrie toohello-portal. Maar nu wil ik toosee Hallo telemetrie alleen in Visual Studio.*
  
  * In de instellingen van Hallo zoekvenster is er een optie toosearch lokale diagnostische gegevens zelfs als uw app telemetrie toohello portal verzendt.
  * toostop telemetrie verstuurd toohello portal commentaar Hallo regel `<instrumentationkey>...` in ApplicationInsights.config. Wanneer u klaar toosend telemetrie toohello portal opnieuw bent, verwijdert u het commentaarteken.


## <a name="next-steps"></a>Volgende stappen
|  |  |
| --- | --- |
| **[Meer gegevens toevoegen](app-insights-asp-net-more.md)**<br/>Bewaak het gebruik, de beschikbaarheid, de afhankelijkheden en de uitzonderingen. Integreer bijgehouden informatie uit frameworks voor logboekregistratie. Schrijf aangepaste telemetrie. |![Visual Studio](./media/app-insights-visual-studio/64.png) |
| **[Werken met Hallo Application Insights-portal](app-insights-dashboards.md)**<br/>Dashboards, krachtige hulpprogramma's voor diagnose en analyse, waarschuwingen, een live afhankelijkheidskaart van uw toepassing en de geëxporteerde telemetriegegevens weergeven. |![Visual Studio](./media/app-insights-visual-studio/62.png) |

