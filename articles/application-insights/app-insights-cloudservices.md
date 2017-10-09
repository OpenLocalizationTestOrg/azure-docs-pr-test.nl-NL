---
title: aaaApplication Insights voor Azure Cloud Services | Microsoft Docs
description: Controleer uw web- en werkrollen op een effectieve manier met Application Insights
services: application-insights
documentationcenter: 
keywords: WAD2AI, Azure Diagnostics
author: CFreemanwa
manager: carmonm
editor: alancameronwills
ms.assetid: 5c7a5b34-329e-42b7-9330-9dcbb9ff1f88
ms.service: application-insights
ms.devlang: na
ms.tgt_pltfrm: ibiza
ms.topic: get-started-article
ms.workload: tbd
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: 6956ce423eea1e2cf387bd98250bae32d9501ed0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-azure-cloud-services"></a>Application Insights voor Azure Cloud Services
[Microsoft Azure Cloud-service-apps](https://azure.microsoft.com/services/cloud-services/) kunnen met [Application Insights][start] worden gecontroleerd op beschikbaarheid, prestaties, fouten en gebruik door gegevens uit de Application Insights-SDK's te combineren met [Azure Diagnotics](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/azure-diagnostics)-gegevens uit uw cloudservices. Hallo feedback die u over Hallo prestaties en de effectiviteit van uw app in Hallo wilde krijgen, kunt u beslissen Hallo richting van het Hallo-ontwerp in elke ontwikkelingscyclus.

![Voorbeeld](./media/app-insights-cloudservices/sample.png)

## <a name="before-you-start"></a>Voordat u begint
U hebt het volgende nodig:

* Een abonnement op [Microsoft Azure](http://azure.com). Meld u aan met een Microsoft-account, dat u mogelijk al hebt voor Windows, XBox Live of andere Microsoft-cloudservices. 
* Hulpprogramma’s van Microsoft Azure 2.9 of hoger
* Developer Analytics Tools 7.10 of hoger

## <a name="quick-start"></a>Snel starten
Hallo snelste en gemakkelijkste manier toomonitor die uw cloudservice met Application Insights toochoose die optie is wanneer u uw tooAzure service publiceert.

![Voorbeeld](./media/app-insights-cloudservices/azure-cloud-application-insights.png)

Deze optie instrumenten prestatiemeteritems van uw app tijdens runtime, zodat u alle Hallo telemetrie moet u toomonitor aanvragen, uitzonderingen en afhankelijkheden in uw Webrol, evenals de prestaties van uw werkrollen. Diagnostische traceringen die zijn gegenereerd door uw app worden ook verzonden tooApplication Insights.

Als dat alles is wat u nodig hebt, bent u klaar. De volgende stappen die u kunt nemen, zijn de [metrische gegevens van uw app bekijken](app-insights-metrics-explorer.md), [query’s uitvoeren op uw gegevens met Analytics](app-insights-analytics.md) en mogelijk een [dashboard](app-insights-dashboards.md) instellen. Kunt u tooset up [beschikbaarheidstests](app-insights-monitor-web-app-availability.md) en [code tooyour webpagina's toevoegen](app-insights-javascript.md) toomonitor prestaties in Hallo browser.

Maar u kunt desgewenst kiezen voor meer opties:

* Verzenden van gegevens uit verschillende onderdelen en configuraties tooseparate resources bouwen.
* U kunt aangepaste telemetrie uit uw app toevoegen.

Als u deze opties zijn van belang tooyou, leest u op.

## <a name="sample-application-instrumented-with-application-insights"></a>Voorbeeldtoepassing die is geïnstrumenteerd met Application Insights
Kijk eens naar dit [voorbeeldtoepassing](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService) waarin Application Insights tooa-cloudservice is toegevoegd met twee werkrollen gehost in Azure. 

Het volgende ziet u hoe tooadapt uw eigen cloudservice project in Hallo dezelfde manier.

## <a name="plan-resources-and-resource-groups"></a>Resources en resourcegroepen plannen
Hallo telemetrie van uw app wordt opgeslagen, geanalyseerd en in een Azure-resource van het type Application Insights weergegeven. 

Elke resource behoort tooa resourcegroep. Resourcegroepen worden gebruikt voor het beheer van kosten voor het verlenen van toegang tooteam-leden en toodeploy updates in een enkele, gecoördineerde transactie. Bijvoorbeeld, kunt u [schrijven van een script toodeploy](../azure-resource-manager/resource-group-template-deploy.md) een Azure Cloud Service en de Application Insights bewaking resources allemaal in één bewerking.

### <a name="resources-for-components"></a>Resources voor onderdelen
Hallo aanbevolen-schema is een afzonderlijke resource voor elk onderdeel van uw toepassing - dat wil zeggen, elke Webrol en een werkrol toocreate. Elk onderdeel afzonderlijk kunt analyseren, maar kunt maken een [dashboard](app-insights-dashboards.md) die samenbrengt Hallo sleutel grafieken van alle onderdelen van hello, zodat u kunt vergelijken en ze samen te controleren. 

Een alternatieve-schema is toosend Hallo telemetrie van meer dan één rol toohello dezelfde resource, maar [een dimensie-eigenschap tooeach telemetrie-item toevoegen](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer) die de bronrol identificeert. In dit schema metrische grafieken zoals uitzonderingen normaal weergeven een aggregatie van Hallo tellingen van Hallo verschillende rollen, maar u kunt Hallo grafiek segmenteren door Hallo rol-id wanneer nodig. Zoekopdrachten kunnen ook worden gefilterd op Hallo dezelfde dimensie. Dit alternatief maakt het een stuk eenvoudiger tooview alles op Hallo dezelfde tijd, maar kan ook toosome verwarring leiden tussen Hallo rollen.

Telemetrie van de browser wordt gewoonlijk opgenomen in Hallo dezelfde resource als de server-side '-Webrol.

Hallo Application Insights-resources voor de verschillende componenten Hallo in één resourcegroep geplaatst. Dit maakt het eenvoudig toomanage ze samen. 

### <a name="separating-development-test-and-production"></a>Ontwikkelings-, test- en productiegegevens scheiden
Als u aangepaste gebeurtenissen voor de volgende functie ontwikkelt terwijl de vorige versie Hallo live, wilt u toosend Hallo ontwikkeling telemetrie tooa afzonderlijke Application Insights-resource. Anders moeten harde toofind uw test telemetrie tussen alle verkeer van live site Hallo Hallo.

tooavoid deze situatie afzonderlijke resources maken voor elke buildconfiguratie of 'stempel' (ontwikkeling, testen, productie,...) van uw systeem. Hallo-bronnen voor elke buildconfiguratie in een afzonderlijke resourcegroep geplaatst. 

toosend hello telemetrie toohello juiste resources, u kunt instellen Hallo Application Insights-SDK zodat deze een andere instrumentatiesleutel afhankelijk van Hallo buildconfiguratie opneemt. 

## <a name="create-an-application-insights-resource-for-each-role"></a>Een Application Insights-resource maken voor elke rol
Als u hebt besloten toocreate een afzonderlijke resource voor elke rol - en het is mogelijk een afzonderlijke ingesteld voor elke buildconfiguratie - dan is het eenvoudigste toocreate ze Hallo Application Insights-portal. (Als u veel bronnen maakt, kunt u [Hallo automatiseren](app-insights-powershell.md).

1. In Hallo [Azure-portal][portal], maak een nieuwe Application Insights-resource. Kies ASP.NET-app als het toepassingstype. 

    ![Klik op Nieuw > Application Insights](./media/app-insights-cloudservices/01-new.png)
2. U ziet dat elke resource een instrumentatiesleutel krijgt. U kunt dit later nodig als u toomanually wilt configureren of Controleer de configuratie Hallo Hallo SDK.

    ![Klik op eigenschappen en druk op ctrl + C Hallo sleutel selecteren](./media/app-insights-cloudservices/02-props.png) 

## <a name="set-up-azure-diagnostics-for-each-role"></a>Azure Diagnostics instellen voor elke rol
Stel deze optie toomonitor uw app met Application Insights. Voor webrollen zorgt u hiermee voor prestatiebewaking, waarschuwingen en diagnostische gegevens en een gebruiksanalyse. U kunt zoeken en controleren van Azure diagnostics zoals opnieuw opstarten, prestatiemeteritems en aanroepen tooSystem.Diagnostics.Trace voor andere functies. 

1. In Visual Studio Solution Explorer, onder &lt;YourCloudService&gt;, rollen, open Hallo eigenschappen van elke rol.
2. In **configuratie**stelt **verzenden van diagnostische gegevens tooApplication Insights** en selecteer Hallo geschikte Application Insights-resource die u eerder hebt gemaakt.

Als u hebt besloten een afzonderlijke Application Insights-resource voor elke buildconfiguratie toouse, eerst Hallo configuration selecteren.

![In de eigenschappen van elke Azure rol Hallo Application Insights configureren](./media/app-insights-cloudservices/configure-azure-diagnostics.png)

Dit heeft Hallo effect van uw Application Insights-instrumentatiesleutels in Hallo-bestanden met de naam invoegen `ServiceConfiguration.*.cscfg`. ([Voorbeeldcode](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/AzureEmailService/ServiceConfiguration.Cloud.cscfg)).

Als u toovary Hallo niveau van diagnostische gegevens verzonden tooApplication Insights wilt, kunt u doen [door te bewerken Hallo `.cscfg` bestanden rechtstreeks](app-insights-azure-diagnostics.md).

## <a name="sdk"></a>Hallo SDK installeren in elk project
Deze optie wordt toegevoegd Hallo mogelijkheid tooadd aangepaste zakelijke telemetrie tooany rol, voor een dichter analyse van hoe uw toepassing wordt gebruikt en wordt uitgevoerd.

Configureer Hallo Application Insights-SDK voor elk cloud-app-project in Visual Studio.

1. **Web-rollen**: met de rechtermuisknop op het Hallo-project en kies **Configure Application Insights** of **toevoegen > Application Insights telemetrie**.

2. **Werkrollen**: 
 * Met de rechtermuisknop op het Hallo-project en selecteer **Nuget-pakketten beheren**.
 * Voeg [Application Insights voor Windows Servers](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) toe.

    ![Naar Application Insights zoeken](./media/app-insights-cloudservices/04-ai-nuget.png)

3. Configureer Hallo SDK toosend gegevens toohello Application Insights-resource.

    Instellen in een functie geschikte opstarten Hallo instrumentatiesleutel van Hallo configuratie-instelling in Hallo .cscfg-bestand:
 
    ```C#
   
     TelemetryConfiguration.Active.InstrumentationKey = RoleEnvironment.GetConfigurationSettingValue("APPINSIGHTS_INSTRUMENTATIONKEY");
    ```
   
    Doe dit voor elke rol in uw toepassing. Hallo voorbeelden:
   
   * [Webrol](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/Global.asax.cs#L27)
   * [Werkrol](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/WorkerRoleA.cs#L232)
   * [Voor webpagina’s](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/Views/Shared/_Layout.cshtml#L13) 
4. Set Hallo ApplicationInsights.config-bestand toobe gekopieerd altijd toohello uitvoermap. 
   
    (In Hallo .config-bestand ziet u berichten waarin u tooplace hello instrumentatiesleutel er wordt gevraagd. Voor cloudtoepassingen het is echter beter tooset op Hallo cscfg-bestand. Dit zorgt ervoor dat die rol Hallo correct wordt geïdentificeerd in de portal Hallo.)

#### <a name="run-and-publish-hello-app"></a>Uitvoeren en het Hallo-app publiceren
Voer uw app uit en meld u aan bij Azure. Open Hallo Application Insights-resources die u hebt gemaakt en ziet u afzonderlijke gegevenspunten worden weergegeven [Search](app-insights-diagnostic-search.md), en gegevens in geaggregeerd [metriek Explorer](app-insights-metrics-explorer.md). 

Toevoegen van meer telemetrie - Zie Hallo secties hieronder - en vervolgens uw app tooget live diagnostische en gebruiksgegevens feedback publiceren. 

#### <a name="no-data"></a>Zijn er geen gegevens?
* Open Hallo [Search] [ diagnostic] tegel, toosee afzonderlijke gebeurtenissen.
* Gebruik Hallo toepassing om verschillende pagina's te openen zodat er telemetrie wordt gegenereerd.
* Wacht een paar seconden en klik op Vernieuwen.
* Zie [Probleemoplossing][qna].

## <a name="view-azure-diagnostic-events"></a>Gebeurtenissen van Azure Diagnostics weergeven
Waar toofind hello [Azure Diagnostics](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/azure-diagnostics) informatie in de Application Insights:

* Prestatiemeteritems worden weergegeven als aangepaste functies voor het verzamelen van metrische gegevens. 
* Windows-gebeurtenislogboeken worden als traceringen en aangepaste gebeurtenissen weergegeven.
* Toepassinglogboeken, ETW-logboeken en logboeken met diagnostische gegevens over de infrastructuur worden weergegeven als traceringen.

toosee prestatiemeteritems en het aantal gebeurtenissen, open [Metrics Explorer](app-insights-metrics-explorer.md) en een nieuwe grafiek toe te voegen:

![Gegevens van Azure Diagnostics](./media/app-insights-cloudservices/23-wad.png)

Gebruik [Search](app-insights-diagnostic-search.md) of een [Analytics query](app-insights-analytics-tour.md) toosearch over Hallo verschillende verzonden door Azure Diagnostics traceerlogboeken. Stel dat u hebt een niet-verwerkte uitzondering, waardoor een rol toocrash en de Prullenbak. Deze informatie wordt weergegeven in Hallo toepassing kanaal van Windows-gebeurtenislogboek. U kunt zoeken toolook gebruiken op Windows-gebeurtenislogboek fout Hallo en Hallo volledige stack-trace ophalen voor Hallo-uitzondering. Die helpen u de hoofdoorzaak Hallo van Hallo probleem.

![Zoeken in Azure Diagnostics](./media/app-insights-cloudservices/25-wad.png)

## <a name="more-telemetry"></a>Meer telemetrie
Hallo secties hieronder tonen hoe tooget extra telemetrie van verschillende aspecten van uw toepassing.

## <a name="track-requests-from-worker-roles"></a>Aanvragen van werkrollen bijhouden
Hallo aanvragen module verzamelt automatisch gegevens over HTTP-aanvragen in web-rollen. Zie Hallo [MVCWebRole steekproef](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/MvcWebRole) voor voorbeelden van hoe u de verzameling standaardgedrag Hallo kunt negeren. 

Hallo-prestaties van aanroepen tooworker functies te kunnen vastleggen door bijhouden Hallo dezelfde manier als HTTP-aanvragen. In Application Insights meet Hallo telemetrie aanvraagtype een werkeenheid benoemde serverzijde die kunnen worden getimede en kunnen onafhankelijk slagen of mislukken. Tijdens het HTTP-aanvragen worden automatisch vastgelegd door Hallo SDK, kunt u uw eigen code tootrack aanvragen tooworker rollen kunt invoegen.

Hallo twee voorbeeld worker rollen providers tooreport aanvragen: [WorkerRoleA](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/WorkerRoleA) en [WorkerRoleB](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/WorkerRoleB)

## <a name="exceptions"></a>Uitzonderingen
Zie [Uitzonderingen controleren in Application Insights](app-insights-asp-net-exceptions.md) als u wilt weten hoe u onverwerkte uitzonderingen kunt verzamelen van verschillende typen webtoepassingen.

Hallo voorbeeld Webrol heeft MVC5 en Web API 2-controllers. Hallo worden niet-verwerkte uitzonderingen op Hallo twee vastgelegd met Hallo handlers te volgen:

* [AiHandleErrorAttribute](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/Telemetry/AiHandleErrorAttribute.cs) [hier](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/App_Start/FilterConfig.cs#L12) instellen voor MVC5-controllers
* [AiWebApiExceptionLogger](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/Telemetry/AiWebApiExceptionLogger.cs) [hier](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/App_Start/WebApiConfig.cs#L25) instellen voor Web API 2-controllers

Voor werkrollen zijn er twee manieren tootrack uitzonderingen:

* TrackException(ex)
* Als u Hallo Application Insights trace listener NuGet-pakket hebt toegevoegd, kunt u **System.Diagnostics.Trace** toolog uitzonderingen. [Codevoorbeeld](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/WorkerRoleA.cs#L107)

## <a name="performance-counters"></a>Prestatiemeteritems
Hallo prestatiemeteritems te volgen, worden standaard verzameld:

    * \Process(??APP_WIN32_PROC??)\% Processor Time
    * \Memory\Available Bytes
    * \.NET CLR Exceptions(??APP_CLR_PROC??)\# of Exceps Thrown / sec
    * \Process(??APP_WIN32_PROC??)\Private Bytes
    * \Process(??APP_WIN32_PROC??)\IO Data Bytes/sec
    * \Processor(_Total)\% Processor Time

Voor webrollen worden ook gegevens verzameld voor de volgende prestatiemeteritems:

    * \ASP.NET Applications(??APP_W3SVC_PROC??)\Requests/Sec
    * \ASP.NET Applications(??APP_W3SVC_PROC??)\Request Execution Time
    * \ASP.NET Applications(??APP_W3SVC_PROC??)\Requests In Application Queue

U kunt extra aangepaste prestatiemeteritems of andere Windows-prestatiemeteritems opgeven door ApplicationInsights.config te bewerken, [zoals in dit voorbeeld](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/ApplicationInsights.config#L14).

  ![Prestatiemeteritems](./media/app-insights-cloudservices/OLfMo2f.png)

## <a name="correlated-telemetry-for-worker-roles"></a>Gecorreleerde telemetrie voor werkrollen
Wanneer u zien kunt welke leidde tooa is mislukt of hoge latentie-aanvraag is een geavanceerde diagnostische ervaring. Web-functies gerelateerde Hallo die SDK worden automatisch ingesteld correlatie tussen telemetrie. Voor werkrollen, kunt u een aangepaste telemetrie initialisatiefunctie tooset een gemeenschappelijk Operation.Id context-kenmerk voor alle Hallo telemetrie tooachieve dit. Hiermee kunt u toosee of Hallo latentie/mislukte probleem is veroorzaakt vanwege tooa afhankelijkheid of uw code in een oogopslag! 

Dit doet u al volgt:

* Hallo correlatie Id in een CallContext instellen zoals [hier](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/WorkerRoleA.cs#L36). In dit geval gebruiken we Hallo aanvraag-ID als Hallo correlatie-id
* Toevoegen van een aangepaste TelemetryInitializer implementatie tooset hello Operation.Id toohello correlationId hierboven. Hier vindt u een voorbeeld: [ItemCorrelationTelemetryInitializer](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/Telemetry/ItemCorrelationTelemetryInitializer.cs#L13)
* Hallo aangepaste telemetrie initialisatiefunctie toevoegen. U kunt hiervoor in Hallo ApplicationInsights.config-bestand, of in code zoals [hier](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/WorkerRoleA.cs#L233)

Dat is alles. Hallo portal ervaring is al bekabeld up toohelp dat u alle gekoppelde telemetrie in één oogopslag zien:

![Gecorreleerde telemetrie](./media/app-insights-cloudservices/bHxuUhd.png)

## <a name="client-telemetry"></a>Telemetrie op de client
[Voeg Hallo JavaScript SDK tooyour webpagina's] [ client] tooget browser gebaseerde telemetrie zoals pagina weergave aantallen, laadtijden voor pagina's, script-uitzonderingen en toolet u aangepaste telemetrie schrijven in uw pagina-scripts.

## <a name="availability-tests"></a>Beschikbaarheidstests
[Webtests instellen] [ availability] toomake zorgen dat uw toepassing live en responsief blijft.

## <a name="display-everything-together"></a>Een totaaloverzicht weergeven
tooget een volledig beeld van uw systeem, kunt u Hallo sleutel grafieken samen bewaking op een brengt [dashboard](app-insights-dashboards.md). Bijvoorbeeld, u Hallo-aanvraag kan vastmaken en fout telt van elke rol. 

Als u in uw systeem andere Azure-services gebruikt, zoals Stream Analytics, kunt u ook de controlegrafieken daarvan weergeven. 

Als u een client mobiele app hebt, sommige code toosend aangepaste gebeurtenissen op belangrijke operations invoegen en maken een [HockeyApp bridge](app-insights-hockeyapp-bridge-app.md). Query's maken in [Analytics](app-insights-analytics.md) toodisplay Hallo gebeurtenis tellingen en toohello dashboard vastmaken.

## <a name="example"></a>Voorbeeld
[Hallo voorbeeld](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService) bewaakt van een service met een Webrol en twee werkrollen.

## <a name="exception-method-not-found-on-running-in-azure-cloud-services"></a>Uitzondering Methode niet gevonden bij het uitvoeren van uw app in Azure Cloud Services
Hebt u uw app ontwikkeld voor .NET 4.6? 4.6 wordt niet automatisch ondersteund in Azure Cloud Services-rollen. [Installeer 4.6 voor elke rol](../cloud-services/cloud-services-dotnet-install-dotnet.md) voordat u uw app uitvoert.

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Volgende stappen
* [Configureren van Azure Diagnostics tooApplication Insights verzenden](app-insights-azure-diagnostics.md)
* [Het maken van Application Insights-resources automatiseren](app-insights-powershell.md)
* [Azure Diagnostics automatiseren](app-insights-powershell-azure-diagnostics.md)
* [Azure Functions](https://github.com/christopheranderson/azure-functions-app-insights-sample)

[api]: app-insights-api-custom-events-metrics.md
[availability]: app-insights-monitor-web-app-availability.md
[azure]: app-insights-azure.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[netlogs]: app-insights-asp-net-trace-logs.md
[portal]: http://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md 
