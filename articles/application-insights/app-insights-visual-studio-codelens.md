---
title: aaaApplication Insights telemetrie in Visual Studio CodeLens | Microsoft Docs
description: Krijg snel toegang tot uw Application Insights-aanvraag en uitzonderingstelemetrie met CodeLens in Visual Studio.
services: application-insights
documentationcenter: .net
author: numberbycolors
manager: carmonm
ms.assetid: 93559e44-23cb-4b9d-8425-60f7f0d0a82c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: bwren
ms.openlocfilehash: e812aa48f2a67eea860e7ecde341855763bb8a8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-telemetry-in-visual-studio-codelens"></a>Application Insights Telemetry in Visual Studio CodeLens
Methoden in Hallo-code van uw web-app kunnen worden gemarkeerd met telemetrie over de runtime-uitzonderingen en reactietijden van de aanvraag. Als u installeert [Azure Application Insights](app-insights-overview.md) in uw toepassing hello telemetrie wordt weergegeven in Visual Studio [CodeLens](https://msdn.microsoft.com/library/dn269218.aspx) -opmerkingen Hallo boven aan elke functie waar bent u gewend Hallo tooseeing nuttig informatie zoals het aantal locaties Hallo functie hello wordt verwezen, of Hallo laatste persoon die het bewerkt.

![CodeLens](./media/app-insights-visual-studio-codelens/codelens-overview.png)

> [!NOTE]
> Application Insights in CodeLens is beschikbaar in Visual Studio 2015 Update 3 en hoger, of met de meest recente versie van Hallo [Analytics hulpprogramma's voor ontwikkelaars extensie](https://visualstudiogallery.msdn.microsoft.com/82367b81-3f97-4de1-bbf1-eaf52ddc635a). CodeLens is beschikbaar in Hallo Enterprise en Professional-edities van Visual Studio.
> 
> 

## <a name="where-toofind-application-insights-data"></a>Waar toofind Application Insights-gegevens
Zoek naar Application Insights telemetrie in Hallo CodeLens indicatoren van openbare aanvraagmethoden Hallo van uw webtoepassing. De CodeLens-indicatoren worden boven de methode en andere verklaringen weergegeven in C#- en Visual Basic-code. Als er Application Insights-gegevens beschikbaar zijn voor een methode, ziet u indicatoren voor aanvragen en uitzonderingen, zoals '100 aanvragen, 1% is mislukt' of '10 uitzonderingen'. Klik op een CodeLens-indicator voor meer informatie. 

> [!TIP]
> Application Insights-aanvragen en uitzonderingen indicatoren kunnen een paar seconden duren tooload nadat andere indicatoren CodeLens worden weergegeven.
> 
> 

## <a name="exceptions-in-codelens"></a>Uitzonderingen in CodeLens
![NOG TE BEPALEN](./media/app-insights-visual-studio-codelens/codelens-exceptions.png)

Hallo uitzondering CodeLens indicator toont Hallo aantal uitzonderingen dat is opgetreden in Hallo afgelopen 24 uur uit Hallo 15 meeste voorkomende uitzonderingen in uw toepassing in die periode wordt tijdens het verwerken van aanvraag Hallo afgehandeld door Hallo-methode.

toosee om meer details, klikt u op Hallo uitzonderingen CodeLens indicator:

* Hallo Percentagewijziging in aantal uitzonderingen op Hallo meest recente 24 uur relatieve toohello voorgaande 24 uur
* Kies **gaat toocode** toonavigate toohello broncode voor Hallo functie er Hallo uitzondering is opgetreden
* Kies **Search** tooquery alle exemplaren van deze uitzondering dat is opgetreden in de afgelopen 24 uur Hallo
* Kies **Trend** tooview een visualisatie trend voor exemplaren van deze uitzondering in Hallo afgelopen 24 uur
* Kies **alle uitzonderingen in deze app weer** tooquery alle uitzonderingen die zijn opgetreden in de afgelopen 24 uur Hallo
* Kies **verkennen uitzonderingstrends** tooview een visualisatie trend voor alle uitzonderingen die hebben plaatsgevonden in Hallo afgelopen 24 uur. 

> [!TIP]
> Als u '0 uitzonderingen' in CodeLens ziet, maar u weet dat er uitzonderingen, Controleer of de juiste Application Insights-resource Hallo is geselecteerd in CodeLens toomake. tooselect een andere resource met de rechtermuisknop op het project in Solution Explorer Hallo en kies **Application Insights > telemetrie bron kiezen**. CodeLens wordt alleen weergegeven voor Hallo 15 meeste voorkomende uitzonderingen in uw toepassing in Hallo afgelopen 24 uur, als een uitzondering is de meeste 16de vaak Hallo of minder, ziet u "0 uitzonderingen." Uitzonderingen op de ASP.NET-weergaven mogelijk niet weergegeven op Hallo controllermethoden die deze weergaven gegenereerd.
> 
> [!TIP]
> Als u '? uitzonderingen' in CodeLens, moet u uw Azure-account met Visual Studio of de referenties van uw Azure-account is mogelijk verlopen tooassociate. In beide gevallen klikt u op '? uitzonderingen' en kies **account toevoegen...**  tooenter uw referenties.
> 
> 

## <a name="requests-in-codelens"></a>Aanvragen in CodeLens
![NOG TE BEPALEN](./media/app-insights-visual-studio-codelens/codelens-requests.png)

Hallo aanvraag CodeLens statusindicator geeft Hallo het aantal HTTP-aanvragen die zijn verwerkt door een methode in Hallo na 24 uur, plus Hallo percentage van deze aanvragen die niet zijn geslaagd.

Klik op toosee meer details Hallo CodeLens indicator aanvragen:

* Hallo absolute en het percentage wijzigingen in het aantal aanvragen, mislukte aanvragen en reactietijden van de gemiddelde via Hallo na 24 uur gestegen ten toohello voorgaande 24 uur
* Hallo betrouwbaarheid van Hallo-methode, berekend als Hallo percentage verzoeken die u niet in Hallo afgelopen 24 uur mislukken hebt
* Kies **Search** voor aanvragen of mislukte aanvragen tooquery alle Hallo (mislukte) aanvragen dat is opgetreden in Hallo afgelopen 24 uur
* Kies **Trend** tooview een visualisatie trend voor aanvragen en mislukte aanvragen en het gemiddelde reactietijd van keer Hallo afgelopen 24 uur.
* Kies Hallo naam Hallo Application Insights-resource in Hallo linksboven Hallo CodeLens details weergeven toochange welke resource Hallo bron voor CodeLens gegevens is.

## <a name="next"></a>Volgende stappen
|  |  |
| --- | --- |
| **[Met Application Insights werken in Visual Studio](app-insights-visual-studio.md)**<br/>Telemetrie zoeken, data in CodeLens bekijken en configureren van Application Insights. Allen vanuit Visual Studio. |![Met de rechtermuisknop op het Hallo-project en kies Application Insights zoeken](./media/app-insights-visual-studio-codelens/34.png) |
| **[Meer gegevens toevoegen](app-insights-asp-net-more.md)**<br/>Bewaak het gebruik, de beschikbaarheid, de afhankelijkheden en de uitzonderingen. Integreer bijgehouden informatie uit frameworks voor logboekregistratie. Schrijf aangepaste telemetrie. |![Visual Studio](./media/app-insights-visual-studio-codelens/64.png) |
| **[Werken met Hallo Application Insights-portal](app-insights-dashboards.md)**<br/>Dashboards, krachtige hulpprogramma's voor diagnose en analyse, waarschuwingen, een live afhankelijkheidskaart van uw toepassing en exportmogelijkheden voor telemetrie. |![Visual Studio](./media/app-insights-visual-studio-codelens/62.png) |

