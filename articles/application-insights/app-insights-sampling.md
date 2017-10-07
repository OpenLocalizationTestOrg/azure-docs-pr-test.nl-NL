---
title: aaaTelemetry steekproeven in Azure Application Insights | Microsoft Docs
description: Hoe Hallo tookeep volume telemetrie onder controle.
services: application-insights
documentationcenter: windows
author: vgorbenko
manager: carmonm
ms.assetid: 015ab744-d514-42c0-8553-8410eef00368
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bwren
ms.openlocfilehash: e19c350d0a5f16736c100322a9922fcfbf5d7b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sampling-in-application-insights"></a>Steekproeven in Application Insights


Steekproeven is een functie in [Azure Application Insights](app-insights-overview.md). Is Hallo aanbevolen manier tooreduce telemetrie verkeer en opslag, met behoud van een statistisch correcte analyse van toepassingsgegevens. Hallo filter selecteert items die zijn gerelateerd, zodat u tussen items navigeren kunt als u de diagnostische onderzoeken.
Wanneer metrische aantallen worden tooyou op Hallo portal worden weergegeven, zijn ze renormalized tootake account Hallo steekproef nemen toominimize een effect op Hallo statistieken.

Steekproeven verlaagt de kosten van verkeer en gegevens en kunt u voorkomen beperking.

## <a name="in-brief"></a>Kort gezegd:
* Steekproeven behoudt 1 in  *n*  Hallo rest wordt teruggezet en registreert. Het kan bijvoorbeeld een samplefrequentie van 20% 1: 5 gebeurtenissen behouden. 
* Steekproeven gebeurt automatisch als uw toepassing veel telemetrie, in ASP.NET web server-apps verzendt.
* U kunt ook instellen dat wordt handmatig, hetzij in Hallo portal op Hallo prijzen pagina. of in Hallo ASP.NET-SDK in Hallo .config-bestand, tooalso Hallo netwerkverkeer te verminderen.
* Als u aangepaste gebeurtenissen en u ervoor wilt dat een verzameling van gebeurtenissen wordt behouden of verwijderd samen toomake, ervoor zorgen dat ze dezelfde OperationId waarde hebben Hallo.
* Hallo steekproeven deler  *n*  wordt gerapporteerd in elke record in de eigenschap Hallo `itemCount`, die in de zoekopdracht wordt weergegeven onder Hallo beschrijvende naam 'aanvraag aantal' of 'gebeurtenis aantal'. Wanneer steekproeven niet uitgevoerd is, `itemCount==1`.
* Als u analysequery's schrijft, moet u [rekening houden met steekproeven](app-insights-analytics-tour.md#counting-sampled-data). In het bijzonder in plaats van gewoon telling registreert, moet u `summarize sum(itemCount)`.

## <a name="types-of-sampling"></a>Typen steekproeven
Er zijn drie steekproeven van alternatieve methoden:

* **Adaptieve steekproeven** automatisch wordt aangepast volume Hallo van telemetrie vanaf Hallo SDK in uw ASP.NET-app verzonden. De standaardinstelling van SDK v 2.0.0-beta3. Momenteel beschikbaar voor ASP.NET-serverzijde telemetrie alleen. 
* **Vast aantal steekproeven** vermindert Hallo volume telemetrie verzonden van zowel uw ASP.NET-server en de browsers van uw gebruikers. U instellen Hallo frequentie. Hallo-client en server synchroniseert de steekproeven zodat die, in zoekopdracht u tussen gerelateerde paginaweergaven en aanvragen navigeren kunt.
* **Opname steekproeven** werkt in hello Azure-portal. Het aantal Hallo telemetrie van uw app, met een frequentie die u instelt binnenkomt wordt verwijderd. Niet verminderen het verkeer van telemetrie, maar u kunt houden binnen uw maandelijkse quotum. Hallo groot voordeel van opname steekproeven is dat u dit instellen kunt zonder dat uw app en het op uniforme wijze voor alle servers en clients werkt. 

Als Adaptief of vast aantal steekproeven in bewerking, is opname steekproeven uitgeschakeld.

## <a name="ingestion-sampling"></a>Opname steekproeven
Deze vorm van steekproeven werkt op Hallo punt waar Hallo telemetrie van uw webserver, browsers en apparaten Hallo Application Insights-service-eindpunt is bereikt. Hoewel het Hallo telemetrie verkeer dat wordt verzonden vanuit uw app niet verkleinen, vermindert het Hallo bedrag verwerkt en bewaard (en in rekening gebracht voor) door Application Insights.

Gebruik dit type steekproeven als uw app vaak via het maandelijkse quotum wordt en er geen Hallo-optie van het gebruik van Hallo SDK gebaseerde typen steekproeven. 

Hallo samplefrequentie in Hallo quota's en prijzen blade instellen:

![Hallo toepassing overzicht blade, klik op instellingen, Quota, voorbeelden, en vervolgens een samplefrequentie selecteren en klik op bijwerken.](./media/app-insights-sampling/04.png)

Net als andere soorten steekproeven behoudt Hallo algoritme gerelateerde telemetrie-items. Bijvoorbeeld, wanneer u Hallo telemetrie in de zoekopdracht te bekijken bent, u hebt mogelijk toofind Hallo aanvraag gerelateerde tooa bepaalde uitzondering. Metriek telt zoals aanvraagsnelheid en snelheid van de uitzondering correct blijven behouden.

Gegevenspunten die zijn verwijderd door steekproeven zijn niet beschikbaar in de Application Insights-functies, zoals [continue Export](app-insights-export-telemetry.md).

Opname steekproeven functioneren niet terwijl er op basis van SDK adaptieve of vast aantal steekproeven wordt uitgevoerd. Als de samplefrequentie Hallo op Hallo SDK is minder dan 100%, wordt vervolgens hello opname samplefrequentie die u instelt genegeerd.

> [!WARNING]
> Hallo-waarde die wordt weergegeven op de tegel Hallo geeft Hallo-waarde die u voor opname steekproeven instelt. Het vertegenwoordigen niet Hallo werkelijke samplefrequentie als SDK steekproeven uitgevoerd wordt.
> 
> 

## <a name="adaptive-sampling-at-your-web-server"></a>Adaptieve steekproeven op uw webserver
Adaptieve steekproeven is beschikbaar voor Hallo Application Insights-SDK voor ASP.NET v 2.0.0-beta3 of hoger, en is standaard ingeschakeld. 

Adaptieve steekproeven is van invloed op Hallo volume telemetrie van uw web server app toohello Application Insights-service is verzonden. Hallo volume automatisch wordt aangepast tookeep binnen de opgegeven maximale overdrachtssnelheid van verkeer.

Deze werkt niet op lage volumes telemetrie, dus een app in foutopsporing of een website met geringe gebruiksduur, worden niet beïnvloed.

tooachieve hello doelvolume, aantal Hallo telemetrie die is gegenereerd, wordt verwijderd. Maar net als andere soorten steekproeven behoudt Hallo algoritme gerelateerde telemetrie-items. Bijvoorbeeld, wanneer u Hallo telemetrie in de zoekopdracht te bekijken bent, u hebt mogelijk toofind Hallo aanvraag gerelateerde tooa bepaalde uitzondering. 

Metriek telt zoals aanvraagsnelheid en snelheid van de uitzondering zich gecorrigeerde toocompensate voor Hallo steekproef nemen frequentie, zodat ze ongeveer juiste waarden in de metriek Explorer tonen.

**Bijwerken van uw project NuGet** toohello nieuwste pakketten *voorlopige versie* versie van Application Insights: Hallo-project in Solution Explorer met de rechtermuisknop, kies NuGet-pakketten beheren controleren **opnemen voorlopige** en zoek naar Microsoft.ApplicationInsights.Web. 

In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), kunt u verschillende parameters in Hallo `AdaptiveSamplingTelemetryProcessor` knooppunt. Hallo cijfers zijn Hallo standaardwaarden:

* `<MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>`
  
    Hallo doel snelheid waarmee Hallo adaptieve algoritme is erop gericht voor **op elke server-host**. Als uw web-app wordt uitgevoerd op veel hosts, verminderen door deze waarde dus als tooremain binnen de snelheid van uw doel van het verkeer op Hallo Application Insights-portal.
* `<EvaluationInterval>00:00:15</EvaluationInterval>` 
  
    Hallo-interval op welke Hallo huidige frequentie van telemetrie opnieuw geëvalueerd is. Evaluatie wordt uitgevoerd als een zwevend gemiddelde. U kunt de tooshorten dit interval als uw telemetrie aansprakelijk toosudden bursts.
* `<SamplingPercentageDecreaseTimeout>00:02:00</SamplingPercentageDecreaseTimeout>`
  
    Als u steekproeven percentage waarde, hoe snel nadat er worden wijzigingen aangebracht mogen we toolower percentage opnieuw wordt toocapture minder gegevens.
* `<SamplingPercentageIncreaseTimeout>00:15:00</SamplingPercentageIncreaseTimeout>`
  
    Als er steekproeven percentage waarde wijzigingen, hoe snel nadat we toegestaan tooincrease percentage opnieuw wordt toocapture meer gegevens.
* `<MinSamplingPercentage>0.1</MinSamplingPercentage>`
  
    Als percentage steekproef varieert, wat is de minimale waarde Hallo we tooset zijn toegestaan.
* `<MaxSamplingPercentage>100.0</MaxSamplingPercentage>`
  
    Als percentage steekproef varieert, wat is de maximumwaarde Hallo we tooset zijn toegestaan.
* `<MovingAverageRatio>0.25</MovingAverageRatio>` 
  
    In de berekening Hallo Hallo zwevend gemiddelde toegewezen Hallo gewicht toohello meest recente waarde. Gebruik een waarde gelijk tooor kleiner is dan 1. Lagere waarden worden Hallo algoritme op minder reactieve toosudden wijzigingen aanbrengen.
* `<InitialSamplingPercentage>100</InitialSamplingPercentage>`
  
    Hallo waarde toegewezen wanneer Hallo app NET is gestart. Niet verlaagt dit terwijl u fouten opspoort. 

* `<ExcludedTypes>Trace;Exception</ExcludedTypes>`
  
    Puntkomma's gescheiden lijst van typen die u niet dat door actieve toobe wilt. Typen zijn herkend: afhankelijkheid, gebeurtenis, uitzondering, PageView, aanvraag, Trace. Alle exemplaren van Hallo opgegeven typen worden verzonden; Hallo-typen die niet zijn opgegeven, worden vastgelegd.

* `<IncludedTypes>Request;Dependency</IncludedTypes>`
  
    Puntkomma's gescheiden lijst van typen die u wilt dat door actieve toobe. Typen zijn herkend: afhankelijkheid, gebeurtenis, uitzondering, PageView, aanvraag, Trace. Hallo opgegeven typen steekproeven worden genomen; alle exemplaren van Hallo de andere typen altijd worden verzonden.


**tooswitch uit** adaptieve steekproeven, verwijder Hallo AdaptiveSamplingTelemetryProcessor knooppunt uit applicationinsights-config.

### <a name="alternative-configure-adaptive-sampling-in-code"></a>Alternatief: adaptieve steekproeven in code configureren
In plaats van steekproeven in Hallo .config-bestand aanpassen, kunt u code. Hiermee kunt u toospecify een callbackfunctie die wordt aangeroepen wanneer de samplefrequentie Hallo opnieuw geëvalueerd. U kunt dit gebruiken, bijvoorbeeld toofind uit welke samplefrequentie wordt gebruikt.

Hallo verwijderen `AdaptiveSamplingTelemetryProcessor` knooppunt uit Hallo .config-bestand.

*C#*

```C#

    using Microsoft.ApplicationInsights;
    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.Channel.Implementation;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var adaptiveSamplingSettings = new SamplingPercentageEstimatorSettings();

    // Optional: here you can adjust hello settings from their defaults.

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;

    builder.UseAdaptiveSampling(
         adaptiveSamplingSettings,

        // Callback on rate re-evaluation:
        (double afterSamplingTelemetryItemRatePerSecond,
         double currentSamplingPercentage,
         double newSamplingPercentage,
         bool isSamplingPercentageChanged,
         SamplingPercentageEstimatorSettings s
        ) =>
        {
          if (isSamplingPercentageChanged)
          {
             // Report hello sampling rate.
             telemetryClient.TrackMetric("samplingPercentage", newSamplingPercentage);
          }
      });

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

([Meer informatie over de telemetrie processors](app-insights-api-filtering-sampling.md#filtering).)

<a name="other-web-pages"></a>

## <a name="sampling-for-web-pages-with-javascript"></a>Steekproef voor webpagina's met JavaScript
U kunt de webpagina's voor vast tarief steekproeven vanaf een willekeurige server configureren. 

Wanneer u [Hallo webpagina's configureren voor Application Insights](app-insights-javascript.md), Hallo codefragment die u via de Application Insights-portal Hallo wijzigen. (In ASP.NET-apps Hallo codefragment doorgaans gaat in _Layout.cshtml.)  Voeg een regel zoals `samplingPercentage: 10,` voordat de instrumentatiesleutel Hallo:

    <script>
    var appInsights= ... 
    }({ 


    // Value must be 100/N where N is an integer.
    // Valid examples: 50, 25, 20, 10, 5, 1, 0.1, ...
    samplingPercentage: 10, 

    instrumentationKey:...
    }); 

    window.appInsights=appInsights; 
    appInsights.trackPageView(); 
    </script> 

Voor voorbeeldpercentage hello, kiest u een percentage dat is sluiten too100/N, waarbij N een geheel getal.  Momenteel wordt biedt geen ondersteuning voor andere waarden.

Als u tevens vast aantal steekproeven op Hallo server inschakelt, synchroniseren Hallo-clients en de server zodat die, in zoekopdracht u tussen gerelateerde paginaweergaven en aanvragen navigeren kunt.

## <a name="fixed-rate-sampling-for-aspnet-web-sites"></a>Vast aantal steekproeven voor ASP.NET-websites
Vast tarief steekproeven vermindert Hallo verkeer dat wordt verzonden van uw webserver en webbrowsers. In tegenstelling tot adaptieve steekproeven wordt telemetrie tegen een vast tarief dat u hebt besloten gereduceerd. Het ook synchroniseert Hallo-client en server steekproeven zodat verwante items worden bewaard - bijvoorbeeld, zodat als u de weergave van een pagina in de zoekopdracht bekijkt, kunt u de gerelateerde aanvraag vinden.

Hallo steekproeven algoritme behoudt verwante items. Voor elke aanvraag HTTP-worden gebeurtenissen, deze en gerelateerde gebeurtenissen genegeerd of verzonden. 

In Metrics Explorer tarieven zoals het aantal aanvragen en uitzonderingen vermenigvuldigd met een factor toocompensate voor Hallo samplefrequentie, zodat ze ongeveer juist zijn.

1. **Bijwerken van uw project NuGet-pakketten** toohello nieuwste *voorlopige versie* versie van Application Insights. Hallo-project in Solution Explorer met de rechtermuisknop, kies NuGet-pakketten beheren controleren **Include prerelease** en zoek naar Microsoft.ApplicationInsights.Web. 
2. **Uitschakelen van adaptieve steekproeven**: In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), verwijderen of uitcommentariëren hello `AdaptiveSamplingTelemetryProcessor` knooppunt.
   
    ```xml
   
    <TelemetryProcessors>
   
    <!-- Disabled adaptive sampling:
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    -->

    ```

1. **Hallo vast tarief steekproeven module inschakelen.** In dit fragment te toevoegen[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):
   
    ```XML
   
    <TelemetryProcessors>
     <Add  Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
   
      <!-- Set a percentage close too100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
      <SamplingPercentage>10</SamplingPercentage>
      </Add>
    </TelemetryProcessors>
   
    ```

> [!NOTE]
> Voor voorbeeldpercentage hello, kiest u een percentage dat is sluiten too100/N, waarbij N een geheel getal.  Momenteel wordt biedt geen ondersteuning voor andere waarden.
> 
> 

### <a name="alternative-enable-fixed-rate-sampling-in-your-server-code"></a>Alternatief: vast tarief steekproeven in uw servercode inschakelen
In plaats van u Hallo steekproeven parameter in Hallo .config-bestand instelt, kunt u code. 

*C#*

```C#

    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var builder = TelemetryConfiguration.Active.GetTelemetryProcessorChainBuilder();
    builder.UseSampling(10.0); // percentage

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

([Meer informatie over de telemetrie processors](app-insights-api-filtering-sampling.md#filtering).)

## <a name="when-toouse-sampling"></a>Wanneer toouse steekproeven?
Adaptieve steekproeven wordt automatisch ingeschakeld als u Hallo ASP.NET-SDK-versie 2.0.0-beta3 of hoger. Ongeacht welke SDK versie die u gebruikt, kunt u opname steekproeven (op onze server).

U hoeft niet steekproeven voor de meeste grootte voor kleine en middelgrote toepassingen. Hallo nuttigst diagnostische gegevens en de meest nauwkeurige statistieken worden verkregen door het verzamelen van gegevens op alle activiteiten van gebruikers. 

belangrijkste voordelen van steekproeven Hallo zijn:

* Application Insights-service verwijdert ('vertragingen') gegevenspunten wanneer uw app verzendt een zeer hoge frequentie van telemetrie in korte tijd interval. 
* tookeep binnen Hallo [quotum](app-insights-pricing.md) van gegevenspunten voor uw prijscategorie. 
* netwerkverkeer tooreduce van Hallo-verzameling van telemetrie. 

### <a name="which-type-of-sampling-should-i-use"></a>Welk type steekproeven moet ik gebruiken?
**Gebruik de opname steekproef nemen als:**

* U doorlopen uw maandelijkse quotum telemetrie vaak.
* U gebruikt een versie van het Hallo-SDK die biedt geen ondersteuning voor sampling - voorbeeld, Hallo Java SDK of ASP.NET-versies ouder is dan 2.
* U krijgt een groot aantal telemetrie van uw gebruikers webbrowsers.

**Gebruik vast tarief steekproef nemen als:**

* U Hallo Application Insights-SDK voor ASP.NET-web-services versie 2.0.0 of hoger, en
* U wilt dat gesynchroniseerde meting tussen client en server, zodat, wanneer u gebeurtenissen in onderzoeken [Search](app-insights-diagnostic-search.md), kunt u navigeren tussen gerelateerde gebeurtenissen op Hallo-client en server, zoals paginaweergaven en http-aanvragen.
* Bent u er zeker van zijn van de juiste voorbeeldpercentage Hallo voor uw app. Het moet hoog genoeg tooget nauwkeurige meetgegevens, maar hieronder Hallo snelheid waarmee uw prijscategorie quotum wordt overschreden en Hallo beperking limieten. 

**Gebruik adaptieve steekproeven:**

Anders wordt aangeraden adaptieve steekproeven. Dit is standaard ingeschakeld in Hallo ASP.NET server SDK-versie 2.0.0-beta3 of hoger. Het verminderen niet het verkeer totdat een bepaalde minimale frequentie, zodat dit geen invloed op een site intensief wordt gebruikt.

## <a name="how-do-i-know-whether-sampling-is-in-operation"></a>Hoe weet ik of steekproeven uitgevoerd wordt?
toodiscover hello werkelijke snelheid ongeacht waar deze zijn toegepast, wordt gebruikt een [Analytics query](app-insights-analytics.md) zoals deze:

    requests | where timestamp > ago(1d)
    | summarize 100/avg(itemCount) by bin(timestamp, 1h) 
    | render areachart 

In elk bewaard record, `itemCount` geeft het aantal oorspronkelijke records die deze vertegenwoordigt, gelijk too1 + aantal eerdere verwijderde records Hallo Hallo. 

## <a name="how-does-sampling-work"></a>Hoe werkt steekproeven?
Vaste snelheid en adaptieve steekproeven zijn een functie van Hallo SDK in ASP.NET-versies van 2.0.0 en hoger. Opname steekproeven is een functie van Hallo Application Insights-service en kan zich in de bewerking als Hallo SDK steekproeven niet uitvoert. 

Hallo steekproeven algoritme besluit welke toodrop telemetrie-items en welke tookeep zijn (of het is in Hallo SDK of Hallo Application Insights-service). Hallo steekproeven beslissing is gebaseerd op verschillende regels die gericht toopreserve alle gerelateerde gegevenspunten intact onderhouden van een diagnostische ervaring in Application Insights die actie worden uitgevoerd en betrouwbare zelfs met een beperkte set van gegevens. Bijvoorbeeld, als voor een mislukte aanvraag verzendt uw app aanvullende telemetrie-items (zoals uitzondering en traceringen van deze aanvraag wordt vastgelegd), steekproeven niet gesplitst deze aanvraag en andere telemetrie. Het behouden of ze elkaar zakt. Wanneer u gegevens voor de aanvraag in Application Insights Hallo bekijkt, kunt u als gevolg hiervan altijd Hallo aanvraag samen met de bijbehorende telemetrie-items zien. 

Voor toepassingen die definiëren 'gebruiker' (dat wil zeggen, meest voorkomende webtoepassingen), Hallo steekproeven beslissing is gebaseerd op Hallo hash van de gebruikers-id hello, wat betekent dat alle telemetrie voor een bepaalde gebruiker wordt behouden of verwijderd. Voor Hallo typen toepassingen die geen gebruikers (zoals web-services) opgeven is Hallo steekproeven beslissing gebaseerd op Hallo bewerkings-id van Hallo-aanvraag. Ten slotte voor Hallo telemetrie-items waarvoor geen gebruiker noch bewerking-id ingesteld (voor voorbeeld telemetrie-items is gerapporteerd door asynchrone threads met geen http-context) bevat steekproeven gewoon een percentage van de telemetrie-items van elk type. 

Bij het weergeven van telemetrie back tooyou Hallo Hallo Application Insights-service wordt aangepast Hallo metrische gegevens door dezelfde voorbeeldpercentage die is gebruikt tijdens het Hallo van verzameling, toocompensate voor Hallo ontbrekende gegevenspunten. Daarom wanneer bekijkt hello telemetrie in Application Insights, zien Hallo gebruikers statistisch correcte benaderingen die zich dicht toohello real getallen zijn.

Hallo nauwkeurig Hallo aanpassing is grotendeels afhankelijk van voorbeeldpercentage Hallo geconfigureerd. Hallo nauwkeurigheid verhoogt ook, voor toepassingen die een groot aantal in het algemeen soortgelijke aanvragen van een groot aantal gebruikers verwerken. Op Hallo daarentegen voor toepassingen die niet met een aanzienlijke belasting werken, steekproeven is niet nodig als u deze toepassingen kunnen doorgaans alle hun telemetrie verzenden bijwerkt binnen quota hello, zonder verlies van gegevens van de beperking. 

Houd er rekening mee dat Application Insights biedt geen telemetrie-typen, metrische gegevens en sessies, sinds het voorbeeld voor deze typen, verminderde Hallo precisie mag maximaal ongewenste. 

### <a name="adaptive-sampling"></a>Adaptieve steekproeven
Adaptieve steekproeven voegt een onderdeel dat monitors Hallo huidige snelheid van de verzending van Hallo SDK en aangepast Hallo steekproeven percentage tootry toostay binnen Hallo doel maximale snelheid. Hallo aanpassing is berekend met regelmatige tussenpozen en is gebaseerd op een zwevend gemiddelde Hallo uitgaande verzending snelheid.

## <a name="sampling-and-hello-javascript-sdk"></a>Steekproeven en Hallo JavaScript SDK
Hallo-clientzijde (JavaScript) SDK deelneemt aan vast tarief steekproeven in combinatie met Hallo serverzijde SDK. Hallo geïnstrumenteerd pagina's wordt alleen verzonden clientzijde telemetrie van Hallo dezelfde gebruikers voor welke Hallo serverzijde de beslissing genomen te 'steekproef in." Deze logica is ontworpen toomaintain integriteit van de gebruikerssessie tussen de client - en server-zijde. Als gevolg hiervan op een bepaalde telemetrie-item in de Application Insights kunt u alle overige telemetrie-items voor deze gebruiker of de sessie vinden. 

*Client- en serverzijde telemetrie weergeven niet gecoördineerde voorbeelden zoals hierboven worden beschreven.*

* Controleer of u vast aantal steekproeven op server en client ingeschakeld.
* Zorg ervoor dat Hallo SDK-versie 2.0 of hoger.
* Controleer of u ingestelde Hallo dezelfde steekproef nemen percentage in zowel Hallo-client en server.

## <a name="frequently-asked-questions"></a>Veelgestelde vragen
*Waarom wordt niet wordt een eenvoudige 'verzamelen X procent van elk type telemetrie'?*

* Terwijl deze benadering steekproeven met een zeer hoge precisie in metrische benaderingen opgeven wilt, zou deze mogelijkheid toocorrelate diagnostische gegevens per gebruiker, sessie en verzoek, wat van essentieel belang voor diagnostische gegevens worden verbroken. Steekproef werkt daarom beter met "verzamelen alle telemetrie-items voor X procent van de app-gebruikers" of 'verzamelen alle telemetrie voor X percentage aanvragen dat app' logica. Voor Hallo telemetrie-items niet zijn gekoppeld aan het Hallo-aanvragen (zoals achtergrond asynchrone verwerking), is Hallo vallen terug te 'verzamelen X percentage van alle items voor elk type telemetrie." 

*Kan het voorbeeldpercentage Hallo na verloop van tijd wijzigen?*

* Ja, adaptieve steekproef nemen geleidelijk Hallo voorbeeldpercentage, op basis van waargenomen momenteel volume Hallo telemetrie Hallo wordt gewijzigd.

*Als ik vast tarief steekproeven gebruikt, hoe weet ik welke steekproeven percentage werkt Hallo aanbevolen voor mijn app?*

* Uitzoeken wat waardering geven betaalt op een manier is toostart met adaptieve steekproeven, (Zie Hallo hierboven vraag), en vervolgens switch toofixed rate-meting met behulp van dit percentage. 
  
    Anders kunt u tooguess hebben. Het gebruik van uw huidige telemetrie in AI analyseren, ziet u een beperking die optreden en schatting Hallo volume Hallo verzameld telemetrie. Deze drie invoer, samen met de geselecteerde prijscategorie voorstellen die u mogelijk wilt tooreduce Hallo volume Hallo verzameld telemetrie. Echter, een toename van Hallo-nummer van uw gebruikers- of sommige andere shift in Hallo volume telemetrie mogelijk uw schatting ongeldig.

*Wat gebeurt er als ik voorbeeldpercentage te laag configureren?*

* Uitzonderlijk lage voorbeeldpercentage (over-aggressive steekproeven) vermindert Hallo nauwkeurig Hallo benaderingen, wanneer Application Insights toocompensate Hallo visualisatie van gegevens Hallo Hallo gegevens volume te beperken probeert. Ook diagnostische ervaring mogelijk negatieve gevolgen hebben, zoals sommigen Hallo zelden mislukt of trage aanvragen mogen voorbeelden worden gemaakt uit.

*Wat gebeurt er als ik voorbeeldpercentage te hoog configureren?*

* Configureren steekproeven te hoog percentage (geen agressieve genoeg) resultaten in een onvoldoende vermindering van volume Hallo Hallo verzameld telemetrie. Telemetrie verlies van gegevens gerelateerd toothrottling en Hallo kosten van het gebruik van Application Insights kan niet hoger zijn dan u geplande einddatum toooverage kosten kunnen zich blijft voordoen.

*Op welke platforms kan ik steekproeven gebruiken?*

* Opname steekproeven kan automatisch voor alle telemetrie boven een bepaald volume optreden als Hallo SDK niet bezig is met steekproeven. Dit zou werkt, bijvoorbeeld, als uw app gebruikmaakt van een Java-server of als u een oudere versie van ASP.NET-SDK Hallo gebruikt.
* Als u ASP.NET-SDK-versies 2.0.0 en hoger (gehost in Azure of een eigen server), krijgt u adaptieve steekproef nemen standaard, maar u kunt toofixed snelheid overschakelen zoals hierboven is beschreven. Met vast tarief steekproeven Hallo browser SDK worden automatisch gesynchroniseerd toosample gerelateerde gebeurtenissen. 

*Er zijn bepaalde zeldzame gebeurtenissen wilt altijd toosee. Hoe krijg ik ze uit het verleden Hallo steekproeven module?*

* Initialiseren van een afzonderlijk exemplaar van TelemetryClient met een nieuwe TelemetryConfiguration (geen Hallo standaard actief). Die toosend uw zeldzame gebeurtenissen gebruiken.

## <a name="next-steps"></a>Volgende stappen
* [Filteren](app-insights-api-filtering-sampling.md) krijgt u meer strikte controle over wat uw SDK verzendt.

