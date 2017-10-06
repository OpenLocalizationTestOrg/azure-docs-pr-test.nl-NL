---
title: aaaFiltering en voorverwerking hello Azure Application Insights-SDK | Microsoft Docs
description: Telemetrie-Processors en initalisatiefuncties telemetrie schrijven voor Hallo SDK toofilter of eigenschappen toohello gegevens toevoegen voordat Hallo telemetrie toohello Application Insights-portal wordt verzonden.
services: application-insights
documentationcenter: 
author: beckylino
manager: carmonm
ms.assetid: 38a9e454-43d5-4dba-a0f0-bd7cd75fb97b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 11/23/2016
ms.author: bwren
ms.openlocfilehash: 51b9db69b2375b8799718f1b0e1af77620dc2692
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="filtering-and-preprocessing-telemetry-in-hello-application-insights-sdk"></a>Filteren en telemetrie in Application Insights-SDK Hallo voorverwerking


U kunt schrijven en configureren van invoegtoepassingen voor Hallo Application Insights-SDK toocustomize hoe telemetrie worden vastgelegd en verwerkt voordat deze toohello Application Insights-service wordt verzonden.

* [Steekproef nemen](app-insights-sampling.md) Hallo volume telemetrie zonder uw statistieken vermindert. Samen blijven gerelateerde gegevenspunten zodat u tussen deze twee navigeren kunt bij het oplossen van een probleem. In Hallo-portal zijn Hallo totale aantal uitkomsten toocompensate voor Hallo steekproeven.
* Filteren met telemetrie Processors [voor ASP.NET](#filtering) of [Java](app-insights-java-filter-telemetry.md) kunt u selecteren of telemetrie in Hallo SDK wijzigen voordat deze toohello server wordt verzonden. U kunt bijvoorbeeld Hallo volume telemetrie verminderen aanvragen door uit te sluiten robots. Maar voor het filteren is een eenvoudige benadering tooreducing verkeer dan steekproeven. Hiermee kunt u meer controle over wat wordt verzonden, maar u hebt toobe Houd er rekening mee dat dit van invloed op uw statistieken - bijvoorbeeld, als u alle geslaagde aanvragen filteren.
* [Telemetrie initalisatiefuncties eigenschappen toevoegen](#add-properties) tooany telemetrie van uw app, inclusief telemetrie van de standaard modules Hallo verzonden. Bijvoorbeeld zou u berekende waarden; of versienummers waarop toofilter Hallo de gegevens in Hallo-portal.
* [Hallo SDK-API](app-insights-api-custom-events-metrics.md) gebruikte toosend aangepaste gebeurtenissen en metrische gegevens is.

Voordat u begint:

* Installeer Application Insights-Hallo [SDK voor ASP.NET](app-insights-asp-net.md) of [SDK voor Java](app-insights-java-get-started.md) in uw app.

<a name="filtering"></a>

## <a name="filtering-itelemetryprocessor"></a>Filteren: ITelemetryProcessor
Deze techniek hebt u meer rechtstreekse controle over wat is opgenomen of uitgesloten van de telemetriestroom Hallo. U kunt deze gebruiken in combinatie met steekproeven, of afzonderlijk.

toofilter telemetrie, een processor telemetrie schrijven en bij Hallo SDK registreren. Alle telemetrie doorloopt de processor en kunt u toodrop op Hallo streamen of eigenschappen toevoegen. Dit omvat de telemetrie van Hallo standaard modules zoals Hallo HTTP-aanvraag collector en Hallo afhankelijkheid collector, evenals de telemetrie die u zelf hebt geschreven. U kunt, bijvoorbeeld telemetrie over aanvragen van robots of geslaagde afhankelijkheidsaanroepen filter.

> [!WARNING]
> Hallo telemetrie verzonden van Hallo SDK filteren met behulp van processors kan laten uitvallen Hallo statistieken zien in de portal Hallo en maken het moeilijk toofollow verwante objecten.
>
> In plaats daarvan kunt u overwegen [steekproeven](app-insights-sampling.md).
>
>

### <a name="create-a-telemetry-processor-c"></a>Maken van een telemetrie-processor (C#)
1. Controleer of deze Hallo Application Insights-SDK in uw project is versie 2.0.0 of hoger. Met de rechtermuisknop op het project in Visual Studio Solution Explorer en kies NuGet-pakketten beheren. Schakel in NuGet-Pakketbeheer Microsoft.ApplicationInsights.Web.
2. een filter, toocreate ITelemetryProcessor implementeren. Dit is een andere uitbreidbaar punt zoals telemetrie-module, telemetrie initialisatiefunctie en telemetrie-kanaal.

    U ziet dat telemetrie Processors samenstellen van een keten van verwerking. Bij het instantiëren van een processor telemetrie moet u een koppeling toohello volgende processor in de keten Hallo doorgeven. Wanneer een gegevenspunt telemetrie toohello proces methode doorgegeven wordt, wordt het werk en vervolgens aanroepen volgende telemetrie Processor in de keten Hallo Hallo.

    ``` C#

    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.Extensibility;

    public class SuccessfulDependencyFilter : ITelemetryProcessor
      {

        private ITelemetryProcessor Next { get; set; }

        // You can pass values from .config
        public string MyParamFromConfigFile { get; set; }

        // Link processors tooeach other in a chain.
        public SuccessfulDependencyFilter(ITelemetryProcessor next)
        {
            this.Next = next;
        }
        public void Process(ITelemetry item)
        {
            // toofilter out an item, just return
            if (!OKtoSend(item)) { return; }
            // Modify hello item if required
            ModifyItem(item);

            this.Next.Process(item);
        }

        // Example: replace with your own criteria.
        private bool OKtoSend (ITelemetry item)
        {
            var dependency = item as DependencyTelemetry;
            if (dependency == null) return true;

            return dependency.Success != true;
        }

        // Example: replace with your own modifiers.
        private void ModifyItem (ITelemetry item)
        {
            item.Context.Properties.Add("app-version", "1." + MyParamFromConfigFile);
        }
    }

    ```
1. Voeg dit in ApplicationInsights.config:

```XML

    <TelemetryProcessors>
      <Add Type="WebApplication9.SuccessfulDependencyFilter, WebApplication9">
         <!-- Set public property -->
         <MyParamFromConfigFile>2-beta</MyParamFromConfigFile>
      </Add>
    </TelemetryProcessors>

```

(Dit is Hallo dezelfde sectie waarin u een filter steekproeven initialiseren.)

U kunt tekenreekswaarden doorgeven van Hallo .config-bestand door openbare benoemde eigenschappen in uw klasse.

> [!WARNING]
> Wees voorzichtig toomatch Hallo typenaam en eventuele eigenschapsnamen in Hallo .config-bestand toohello klasse en eigenschapnamen in Hallo-code. Als Hallo .config-bestand verwijst naar een niet-bestaande type of een eigenschap, mislukken Hallo SDK achtergrond toosend alle telemetrie.
>
>

**U kunt ook** Hallo-filter in de code kan worden geïnitialiseerd. Voeg de processor in de keten Hallo in een initialisatieklasse geschikte - bijvoorbeeld AppStart in Global.asax.cs:

```C#

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;
    builder.Use((next) => new SuccessfulDependencyFilter(next));

    // If you have more processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

TelemetryClients gemaakt nadat dit punt wordt gebruik van uw processors.

### <a name="example-filters"></a>Voorbeeld-filters
#### <a name="synthetic-requests"></a>Synthetische aanvragen
Filter bots en web-tests. Hoewel Metrics Explorer geeft u de optie toofilter uit synthetische bronnen Hallo, deze optie verkeer beperkt door ze te filteren op Hallo SDK.

``` C#

    public void Process(ITelemetry item)
    {
      if (!string.IsNullOrEmpty(item.Context.Operation.SyntheticSource)) {return;}

      // Send everything else:
      this.Next.Process(item);
    }

```

#### <a name="failed-authentication"></a>Mislukte verificatiepogingen
Filteren van aanvragen met een '401'-respons.

```C#

public void Process(ITelemetry item)
{
    var request = item as RequestTelemetry;

    if (request != null &&
    request.ResponseCode.Equals("401", StringComparison.OrdinalIgnoreCase))
    {
        // toofilter out an item, just terminate hello chain:
        return;
    }
    // Send everything else:
    this.Next.Process(item);
}

```

#### <a name="filter-out-fast-remote-dependency-calls"></a>Snel externe afhankelijkheidsaanroepen uitfilteren
Als u wilt dat alleen toodiagnose aanroepen die traag, filter Hallo fast die zijn.

> [!NOTE]
> Hiermee wordt een verkeerd Hallo statistieken u op Hallo-portal ziet. Hallo afhankelijkheid grafiek ziet er als Hallo afhankelijkheidsaanroepen alle fouten zijn.
>
>

``` C#

public void Process(ITelemetry item)
{
    var request = item as DependencyTelemetry;

    if (request != null && request.Duration.TotalMilliseconds < 100)
    {
        return;
    }
    this.Next.Process(item);
}

```

#### <a name="diagnose-dependency-issues"></a>Problemen als gevolg van diagnoseafhankelijkheid
[Deze blog](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) beschrijft een project toodiagnose afhankelijkheidsproblemen door reguliere pings toodependencies automatisch verzenden.


<a name="add-properties"></a>

## <a name="add-properties-itelemetryinitializer"></a>Eigenschappen toevoegen: ITelemetryInitializer
Telemetrie initalisatiefuncties toodefine globale eigenschappen gebruiken die worden verzonden met alle telemetrie; en toooverride gedrag van Hallo standaard telemetrie modules geselecteerd.

Hallo Application Insights voor Web-pakket verzamelt bijvoorbeeld telemetrie over HTTP-aanvragen. Standaard worden gemarkeerd als een aanvraag met een antwoordcode mislukt > = 400. Maar als u wilt dat tootreat 400 een geslaagde test, kunt u een initialisatiefunctie voor telemetrie waarmee Hallo geslaagd eigenschap wordt ingesteld opgeven.

Als u een initialisatiefunctie telemetrie opgeeft, wordt aangeroepen wanneer een van de Track*() Hallo methoden wordt aangeroepen. Dit omvat de methoden die worden aangeroepen door Hallo standaard telemetrie modules. Volgens de conventies worden alle eigenschappen die al is ingesteld door een initialisatiefunctie voor objecten in deze modules niet ingesteld.

**De initialisatiefunctie definiëren**

*C#*

```C#

    using System;
    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.DataContracts;
    using Microsoft.ApplicationInsights.Extensibility;

    namespace MvcWebRole.Telemetry
    {
      /*
       * Custom TelemetryInitializer that overrides hello default SDK
       * behavior of treating response codes >= 400 as failed requests
       *
       */
      public class MyTelemetryInitializer : ITelemetryInitializer
      {
        public void Initialize(ITelemetry telemetry)
        {
            var requestTelemetry = telemetry as RequestTelemetry;
            // Is this a TrackRequest() ?
            if (requestTelemetry == null) return;
            int code;
            bool parsed = Int32.TryParse(requestTelemetry.ResponseCode, out code);
            if (!parsed) return;
            if (code >= 400 && code < 500)
            {
                // If we set hello Success property, hello SDK won't change it:
                requestTelemetry.Success = true;
                // Allow us toofilter these requests in hello portal:
                requestTelemetry.Context.Properties["Overridden400s"] = "true";
            }
            // else leave hello SDK tooset hello Success property      
        }
      }
    }
```

**De initialisatiefunctie laden**

In ApplicationInsights.config:

    <ApplicationInsights>
      <TelemetryInitializers>
        <!-- Fully qualified type name, assembly name: -->
        <Add Type="MvcWebRole.Telemetry.MyTelemetryInitializer, MvcWebRole"/>
        ...
      </TelemetryInitializers>
    </ApplicationInsights>

*U kunt ook* u Hallo initialisatiefunctie in code, bijvoorbeeld in Global.aspx.cs kunt instantiëren:

```C#
    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```


[Zie voor meer informatie in dit voorbeeld.](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/MvcWebRole)

<a name="js-initializer"></a>

### <a name="javascript-telemetry-initializers"></a>JavaScript telemetrie initalisatiefuncties
*JavaScript*

Voeg een initialisatiefunctie telemetrie direct na Hallo initialisatie van de code die u hebt verkregen via de portal Hallo:

```JS

    <script type="text/javascript">
        // ... initialization code
        ...({
            instrumentationKey: "your instrumentation key"
        });
        window.appInsights = appInsights;


        // Adding telemetry initializer.
        // This is called whenever a new telemetry item
        // is created.

        appInsights.queue.push(function () {
            appInsights.context.addTelemetryInitializer(function (envelope) {
                var telemetryItem = envelope.data.baseData;

                // toocheck hello telemetry item’s type - for example PageView:
                if (envelope.name == Microsoft.ApplicationInsights.Telemetry.PageView.envelopeType) {
                    // this statement removes url from all page view documents
                    telemetryItem.url = "URL CENSORED";
                }

                // tooset custom properties:
                telemetryItem.properties = telemetryItem.properties || {};
                telemetryItem.properties["globalProperty"] = "boo";

                // tooset custom metrics:
                telemetryItem.measurements = telemetryItem.measurements || {};
                telemetryItem.measurements["globalMetric"] = 100;
            });
        });

        // End of inserted code.

        appInsights.trackPageView();
    </script>
```

Zie voor een overzicht van Hallo niet aangepaste eigenschappen beschikbaar zijn op Hallo telemetryItem [Application Insights-exporteren gegevensmodel](app-insights-export-data-model.md).

U kunt zoveel initalisatiefuncties als u wilt toevoegen.

## <a name="itelemetryprocessor-and-itelemetryinitializer"></a>ITelemetryProcessor en ITelemetryInitializer
Wat is Hallo verschil tussen de telemetrie processors en telemetrie initalisatiefuncties?

* Er zijn enkele overlappingen in wat u ermee kunt doen: beide gebruikte tooadd eigenschappen tootelemetry kunnen zijn.
* TelemetryInitializers wordt altijd uitgevoerd voordat TelemetryProcessors.
* TelemetryProcessors kunt u toocompletely vervangen of een telemetrie-item te negeren.
* TelemetryProcessors niet prestatietelemetrie prestatiemeteritem niet verwerken.


## <a name="reference-docs"></a>Referentiedocumenten
* [API-overzicht](app-insights-api-custom-events-metrics.md)
* [ASP.NET-verwijzing](https://msdn.microsoft.com/library/dn817570.aspx)

## <a name="sdk-code"></a>SDK-Code
* [ASP.NET Core SDK](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [ASP.NET 5](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [JavaScript SDK](https://github.com/Microsoft/ApplicationInsights-JS)

## <a name="next"></a>Volgende stappen
* [Zoekopdracht gebeurtenissen en Logboeken](app-insights-diagnostic-search.md)
* [Steekproeven](app-insights-sampling.md)
* [Problemen oplossen](app-insights-troubleshoot-faq.md)
