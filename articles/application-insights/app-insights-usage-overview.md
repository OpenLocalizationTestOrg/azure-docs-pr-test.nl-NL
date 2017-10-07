---
title: analyse van aaaUsage voor webtoepassingen met Azure Application Insights | Microsoft docs
description: Begrijp uw gebruikers- en wat ze doen met uw web-app.
services: application-insights
documentationcenter: 
author: botatoes
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/03/2017
ms.author: bwren
ms.openlocfilehash: f7f9173cf411fa0d2dfb3b5ba99134a02bbc0e89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="usage-analysis-for-web-applications-with-application-insights"></a>Gebruiksanalyse voor webtoepassingen met Application Insights

Welke functies van uw web-app zijn het meest populaire? Voer uw gebruikers hun doelstellingen met uw app controles? Ze niet verwijderen uit op bepaalde tijdstippen en ze kom later terug?  [Azure Application Insights](app-insights-overview.md) kunt u krachtige inzicht in hoe mensen uw web-app gebruiken. Telkens wanneer u uw app bijwerkt, kunt u beoordelen hoe goed werkt voor gebruikers. Met deze kennis, kunt u gegevensgestuurde nemen van beslissingen over de volgende ontwikkelingscycli.

## <a name="send-telemetry-from-your-app"></a>Verzend telemetrie vanuit uw app

de beste ervaring Hello wordt verkregen door het installeren van Application Insights in uw servercode app, en in uw webpagina's. Hallo-client- en serveronderdelen van uw app verzenden telemetrie back toohello Azure-portal voor analyse.

1. **Servercode:** installeren Hallo juiste-module voor uw [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), of [andere](app-insights-platforms.md) app.

    * *Niet wilt dat servercode tooinstall? NET [een Azure Application Insights-resource maken](app-insights-create-new-resource.md).*

2. **Code webpagina:** Open Hallo [Azure-portal](https://portal.azure.com), Hallo Application Insights-resource voor uw app openen en open vervolgens **aan de slag > bewaken en onderzoeken van Client-Side**. 

    ![Hallo script naar Hallo hoofd van uw hoofdwebpagina kopiëren.](./media/app-insights-usage-overview/02-monitor-web-page.png)


3. **Telemetrie ophalen:** uw project in de foutopsporingsmodus uitvoeren voor een paar minuten en zoek naar resulteert in het Hallo-overzichtsblade in Application Insights.

    Publiceren van uw app toomonitor prestaties van uw app en weten wat uw gebruikers met uw app doen.

## <a name="include-user-and-session-id-in-your-telemetry"></a>Gebruikers- en sessie-ID opnemen in uw telemetrie
tootrack gebruikers gedurende een bepaalde periode, Application Insights vereist een tooidentify manier ze. Hallo gebeurtenissen hulpprogramma is Hallo enige informatie over het gebruik hulpprogramma dat hoeft niet een gebruikers-ID of een sessie-ID.

Beginnen met het verzenden van deze id's [hier](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).

## <a name="explore-usage-demographics-and-statistics"></a>Gebruik demografische gegevens en statistieken verkennen
Weten wanneer mensen uw app gebruikt, welke pagina's die ze zijn het meest geïnteresseerd, waar uw gebruikers zich bevinden, welke browsers en besturingssystemen die ze gebruiken. 

Hallo-gebruikers en sessies rapporten filter uw gegevens door's of aangepaste gebeurtenissen en ze segmenteren door eigenschappen zoals locatie-omgeving en pagina. U kunt ook uw eigen filters toevoegen.

![Gebruikers](./media/app-insights-usage-overview/users.png)  

Inzichten op Hallo rechts wijst interessante patronen in Hallo reeks gegevens.  

* Hallo **gebruikers** rapport telt het aantal unieke gebruikers die toegang hebben tot uw pagina's binnen uw gekozen perioden Hallo. (Gebruikers worden geteld met behulp van cookies. Als iemand toegang heeft tot uw site met verschillende browsers of clientcomputers, of hun cookies worden gewist en vervolgens wordt meer dan één keer worden geteld.)
* Hallo **sessies** rapport telt Hallo aantal gebruikerssessies die toegang uw site tot. Een sessie is een periode van de activiteit van een gebruiker, gevolgd door een periode van inactiviteit van meer dan half uur.

[Meer informatie over gebruikers, sessies en gebeurtenissen Hallo-hulpprogramma 's](app-insights-usage-segmentation.md)  

## <a name="page-views"></a>Paginaweergaven

Hallo gebruik blade doorklikken Hallo paginaweergaven tegel tooget een uitsplitsing van de meest populaire's:

![Overzichtsblade hello, klik op Hallo pagina weergaven grafiek](./media/app-insights-usage-overview/05-games.png)

Hallo in bovenstaand voorbeeld is van een website games. Van Hallo grafieken ziet onmiddellijk:

* Gebruik niet is verbeterd in Hallo afgelopen week. Mogelijk moet u bedenken Zoekmachineoptimalisatie?
* Tennis is de meest populaire game pagina Hallo. Laten we de nadruk gelegd op verdere verbeteringen toothis pagina.
* Gemiddeld bezoeken gebruikers Hallo Tennis drie keer per week. (Er zijn drie keer meer sessies dan gebruikers).
* De meeste gebruikers bezoeken Hallo Hallo VS werkende week, en met werkuren. Misschien bieden we een knop 'snel verbergen' op Hallo-webpagina.
* Hallo [aantekeningen](app-insights-annotations.md) op Hallo grafiek weergeven wanneer nieuwe versies van het Hallo-website zijn geïmplementeerd. Geen recente implementaties Hallo had een merkbare invloed op de informatie over het gebruik.

Wat gebeurt er als u wilt dat tooinvestigate Hallo verkeer tooyour site in meer detail, zoals de splitsing door een aangepaste eigenschap die in de telemetrie van paginaweergaven uw site stuurt?

1. Open Hallo **gebeurtenissen** hulpprogramma in het menu Hallo Application Insights-bron. Dit hulpprogramma kunt u het aantal paginaweergaven en aangepaste gebeurtenissen is verzonden vanaf uw app, op basis van tal van opties voor filteren, cohorting en segmentering analyseren.
2. Selecteer in de vervolgkeuzelijst "Wie gebruikt" Hallo, 'Any paginaweergave'.
3. Selecteer in de vervolgkeuzelijst 'Gesplitste door' hello een eigenschap door welke toosplit uw pagina telemetrie weergeven.

## <a name="retention---how-many-users-come-back"></a>Bewaartermijn - hoeveel gebruikers terugkeren?

Bewaartermijn helpt u begrijpen hoe vaak uw gebruikers retourneren toouse hun app op basis van cohorten van gebruikers die een bepaalde actie business tijdens een bepaald tijdsinterval uitgevoerd. 

- Inzicht in welke specifieke functies ervoor zorgen dat gebruikers toocome back meer dan andere 
- Formulier hypothesen op basis van echte gebruikersgegevens 
- Bepalen of bewaarperiode een probleem is met uw product is 

![Bewaartermijn](./media/app-insights-usage-overview/retention.png) 

Hallo bewaren besturingselementen op de voorgrond kunt u toodefine specifieke gebeurtenissen en het tijdstip bereik toocalculate bewaren. Hallo grafiek in het midden Hallo biedt een visuele representatie van Hallo algehele bewaren percentage Hallo tijdbereik opgegeven. Hallo-grafiek aan de onderkant Hallo vertegenwoordigt afzonderlijke bewaren in een bepaalde periode. Dit detailniveau kunt u toounderstand wat uw gebruikers doen en wat van invloed kunnen zijn op de bestaande gebruikers op een meer gedetailleerde granulatie.  

[Meer informatie over het hulpprogramma voor het bewaren van Hallo](app-insights-usage-retention.md)

## <a name="custom-business-events"></a>Aangepaste zakelijke gebeurtenissen

tooget een duidelijk beeld krijgt van wat gebruikers doen met uw web-app, is het nuttig tooinsert regels code toolog aangepaste gebeurtenissen. Deze gebeurtenissen kunnen alles volgen op gedetailleerde gebruikersacties zoals specifieke knoppen toomore aanzienlijke zakelijke gebeurtenissen zoals tot aanschaf overgaat of een ronde winnen. 

Hoewel in sommige gevallen paginaweergaven nuttige gebeurtenissen vertegenwoordigen kunnen, is het niet de waarde true in het algemeen. Een gebruiker kan een productpagina openen zonder Hallo product kopen. 

Met specifieke zakelijke gebeurtenissen, kunt u uw gebruikers voortgang grafiekgebied via uw site. U kunt achterhalen van de voorkeuren voor de verschillende opties en wanneer ze drop out- of problemen hebt. Met deze kennis kunt u weloverwogen beslissingen over Hallo prioriteiten in uw achterstand ontwikkeling.

Gebeurtenissen kunnen worden vastgelegd in Hallo webpagina:

```JavaScript

    appInsights.trackEvent("ExpandDetailTab", {DetailTab: tabName});
```

Of in Hallo servergedeelte van Hallo web-app:

```C#
    var tc = new Microsoft.ApplicationInsights.TelemetryClient();
    tc.TrackEvent("CreatedAccount", new Dictionary<string,string> {"AccountType":account.Type}, null);
    ...
    tc.TrackEvent("AddedItemToCart", new Dictionary<string,string> {"Item":item.Name}, null);
    ...
    tc.TrackEvent("CompletedPurchase");
```

U kunt eigenschap waarden toothese gebeurtenissen koppelen zodat u kunt filteren of Hallo gebeurtenissen wanneer u ze in de portal Hallo inspecteert splitsen. Bovendien is een standaardset eigenschappen gekoppelde tooeach gebeurtenis, zoals anonieme gebruikers-ID, zodat u tootrace Hallo volgorde van activiteiten van een afzonderlijke gebruiker.

Meer informatie over [aangepaste gebeurtenissen](app-insights-api-custom-events-metrics.md#trackevent) en [eigenschappen](app-insights-api-custom-events-metrics.md#properties).

### <a name="slice-and-dice-events"></a>Opdelen gebeurtenissen

U kunt in Hallo gebruikers, sessies en gebeurtenissen's segmenteren en aangepaste gebeurtenissen door de gebruiker, de gebeurtenisnaam van de en eigenschappen te analyseren.
![Gebruikers](./media/app-insights-usage-overview/users.png)  
  
## <a name="design-hello-telemetry-with-hello-app"></a>Hallo telemetrie met Hallo app ontwerpen

Tijdens het ontwerpen van elk onderdeel van uw app, overweeg dan hoe u gaat toomeasure de succes met uw gebruikers. Bepaal wat zakelijke gebeurtenissen u toorecord nodig hebt en code aanroepen voor deze gebeurtenissen bijhouden in uw app uit Hallo Hallo starten.

## <a name="a--b-testing"></a>EEN | B-tests
Als u niet welke variant van een functie wel meer gemaakt weet, laat u beide parameters, waardoor elke gebruikers toegankelijk toodifferent. Hallo succes van elke meten en verplaats tooa uniforme versie.

Voor deze methode, moet u afzonderlijke eigenschap waarden tooall Hallo telemetrie die is verzonden door elke versie van uw app koppelen. U kunt dit doen door de eigenschappen definiëren in Hallo active TelemetryContext. Deze standaardeigenschappen worden toegevoegd aan de tooevery telemetrie message die toepassing hello verzendt - niet alleen uw aangepaste berichten, maar ook in standaard telemetrie Hallo.

Filteren en uw gegevens op Hallo van eigenschapswaarden, dus als verschillende versies van toocompare Hallo splitsen in Hallo Application Insights-portal.

toodo, [instellen van een initialisatiefunctie telemetrie](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):

```C#


    // Telemetry initializer class
    public class MyTelemetryInitializer : ITelemetryInitializer
    {
        public void Initialize (ITelemetry telemetry)
        {
            telemetry.Properties["AppVersion"] = "v2.1";
        }
    }
```

In de web-app initialisatiefunctie Hallo zoals Global.asax.cs:

```C#

    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```

Alle nieuwe TelemetryClients automatisch toegevoegd Hallo eigenschapswaarde die u opgeeft. Afzonderlijke telemetrische gebeurtenissen kunnen Hallo standaardwaarden overschrijven.

## <a name="next-steps"></a>Volgende stappen
   - [Gebruikers, sessies, gebeurtenissen](app-insights-usage-segmentation.md)
   - [Trechters](usage-funnels.md)
   - [Retentie](app-insights-usage-retention.md)
   - [Gebruikersstromen](app-insights-usage-flows.md)
   - [Werkmappen](app-insights-usage-workbooks.md)
   - [Gebruikerscontext toevoegen](app-insights-usage-send-user-context.md)
