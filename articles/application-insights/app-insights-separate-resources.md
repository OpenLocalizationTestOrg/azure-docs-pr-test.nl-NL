---
title: aaaSeparating telemetrie van ontwikkeling, testen en release in Azure Application Insights | Microsoft Docs
description: Directe telemetrie toodifferent bronnen voor ontwikkeling, testen en productie stempels.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 578e30f0-31ed-4f39-baa8-01b4c2f310c9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: a294c8c70f46d7c29b460461c3494c83e13a0cbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="separating-telemetry-from-development-test-and-production"></a>Telemetrie scheiden van ontwikkeling, testen en productie

Wanneer u de volgende versie van een webtoepassing Hallo ontwikkelt, u niet wilt dat toomix up Hallo [Application Insights](app-insights-overview.md) telemetrie van de nieuwe versie Hallo en Hallo al is vrijgegeven versie. tooavoid verwarring verzenden Hallo telemetrie van de ontwikkeling van de verschillende fasen tooseparate Application Insights-resources, met afzonderlijke instrumentatiesleutels (ikeys). toomake deze eenvoudiger toochange hello instrumentatiesleutel versie wordt verplaatst van één fase tooanother, kan het nuttig tooset Hallo ikey in de code in plaats van in het configuratiebestand Hallo zijn. 

(Als u een Azure Cloud Service er [een andere methode voor het instellen van afzonderlijke ikeys](app-insights-cloudservices.md).)

## <a name="about-resources-and-instrumentation-keys"></a>Over de resources en instrumentatiesleutels

Als u bewaking van de Application Insights voor uw web-app instelt, maakt u een Application Insights *resource* in Microsoft Azure. U opent u deze resource in hello Azure-portal op volgorde toosee en analyseren van Hallo verzamelen van telemetriegegevens van uw app. Hallo resource wordt geïdentificeerd door een *instrumentatiesleutel* (ikey). Wanneer u Hallo installeert uw app-pakket toomonitor Application Insights, kunt u deze configureren met de instrumentatiesleutel hello, zodat deze weet waar toosend telemetrie Hallo.

U meestal kiezen afzonderlijke resources toouse of één gedeelde resource in verschillende scenario's:

* Andere, onafhankelijke toepassingen - gebruik een afzonderlijke resource en ikey voor elke app.
* Meerdere onderdelen of rollen zijn van een zakelijke toepassing - gebruiken een [één gedeelde bron](app-insights-monitor-multi-role-apps.md) voor alle Hallo onderdeel apps. Telemetrie worden gefilterd of gesegmenteerd op Hallo cloud_RoleName eigenschap.
* Ontwikkeling, testen en Release - gebruik een afzonderlijke resource en ikey voor versies van het systeem in de tijdstempel' Hallo of fase van de productie.
* EEN | B-tests - gebruik van één resource. Maak een tooadd TelemetryInitializer een eigenschap toohello telemetrie die Hallo varianten identificeert.


## <a name="dynamic-ikey"></a>Dynamische instrumentatiesleutel

toomake is die het eenvoudiger toochange Hallo ikey als Hallo code worden verplaatst tussen stadia van de productie, stel deze in de code in plaats van in het Hallo-configuratiebestand.

Hallo-sleutel in een initialiseringsmethode, zoals global.aspx.cs in een ASP.NET-beheerservice ingesteld:

*C#*

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey = 
          // - for example -
          WebConfigurationManager.AppSettings["ikey"];
      ...

In dit voorbeeld worden in verschillende versies van het webconfiguratiebestand Hallo Hallo ikeys voor verschillende resources Hallo geplaatst. Wisselen Hallo webconfiguratiebestand - die u kunt doen als onderdeel van Hallo release script - wordt Hallo doelbron wisselen.

### <a name="web-pages"></a>Webpagina's
Hallo iKey wordt ook gebruikt in uw app webpagina's in Hallo [script die u hebt verkregen via Snel starten-blade Hallo](app-insights-javascript.md). In plaats van een bekend letterlijk in Hallo script, kunt u het genereren van Hallo server staat. Bijvoorbeeld in een ASP.NET-app:

*JavaScript in Razor*

    <script type="text/javascript">
    // Standard Application Insights web page script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      "@Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="create-additional-application-insights-resources"></a>Aanvullende bronnen voor Application Insights maken
tooseparate telemetrie voor andere toepassingsonderdelen, of voor verschillende stempels (ontwikkeling/tests/productie) Hallo hetzelfde onderdeel, dan hebt u hebt toocreate een nieuwe Application Insights-resource.

In Hallo [portal.azure.com](https://portal.azure.com), een Application Insights-resource toevoegen:

![Klik op Nieuw > Application Insights](./media/app-insights-separate-resources/01-new.png)

* **Toepassingstype** is van invloed op wat er op de blade overzicht Hallo en Hallo eigenschappen beschikbaar zijn in [metrische explorer](app-insights-metrics-explorer.md). Als u uw app-type niet ziet, kiest u een van Hallo webtypen voor webpagina's.
* **Resourcegroep** is nuttig voor het beheren van eigenschappen zoals [toegangsbeheer](app-insights-resources-roles-access-control.md). U kunt afzonderlijke resourcegroepen voor ontwikkeling, testen en productie.
* **Abonnement** is uw betaling-account in Azure.
* **Locatie** is waar we uw gegevens wilt bewaren. Op dit moment worden niet gewijzigd. 
* **Toevoegen van toodashboard** plaatst u een snelle toegang tegel voor uw resource op de startpagina van Azure. 

Hallo-resource maken duurt een paar seconden. U ziet een waarschuwing wanneer deze wordt uitgevoerd.

(U kunt schrijven een [PowerShell-script](app-insights-powershell-script-create-resource.md) toocreate een resource automatisch.)

### <a name="getting-hello-instrumentation-key"></a>Hallo-instrumentatiesleutel ophalen
de instrumentatiesleutel Hallo identificeert Hallo resource die u hebt gemaakt. 

![Klik op Essentials, Hallo Instrumentatiesleutel, CTRL + C](./media/app-insights-separate-resources/02-props.png)

U Hallo instrumentatiesleutels nodig van alle Hallo resources toowhich uw app gegevens worden verzonden.

## <a name="filter-on-build-number"></a>Filteren op build-nummer
Wanneer u een nieuwe versie van uw app publiceert, moet u toobe kunnen tooseparate Hallo telemetrie uit verschillende builds.

U kunt Hallo toepassingsversie eigenschap instellen, zodat u kunt filteren [search](app-insights-diagnostic-search.md) en [metrische explorer](app-insights-metrics-explorer.md) resultaten.

![Filteren op een eigenschap](./media/app-insights-separate-resources/050-filter.png)

Er zijn verschillende methoden gebruiken voor het instellen van Hallo toepassingsversie eigenschap.

* Rechtstreeks worden ingesteld:

    `telemetryClient.Context.Component.Version = typeof(MyProject.MyClass).Assembly.GetName().Version;`
* Inpakken van die regel in een [telemetrie initialisatiefunctie](app-insights-api-custom-events-metrics.md#defaults) tooensure die alle exemplaren van TelemetryClient consistent zijn ingesteld.
* [ASP.NET] Stel de versie van de Hallo in `BuildInfo.config`. Hallo-versie van het Hallo BuildLabel knooppunt Hallo webmodule opgehaald. Dit bestand opnemen in uw project en vergeet niet tooset Hallo kopie altijd eigenschap in Solution Explorer.

    ```XML

    <?xml version="1.0" encoding="utf-8"?>
    <DeploymentEvent xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/VisualStudio/DeploymentEvent/2013/06">
      <ProjectName>AppVersionExpt</ProjectName>
      <Build type="MSBuild">
        <MSBuild>
          <BuildLabel kind="label">1.0.0.2</BuildLabel>
        </MSBuild>
      </Build>
    </DeploymentEvent>

    ```
* [ASP.NET] BuildInfo.config automatisch genereren in MSBuild. toodo hiervan kan een paar regels tooyour toevoegen `.csproj` bestand:

    ```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
    ```

    Hiermee wordt een bestand met de naam gegenereerd *yourProjectName*. BuildInfo.config. Hallo publicatieproces wijzigt de naam van het tooBuildInfo.config.

    Hallo build-label bevat een tijdelijke aanduiding (AutoGen_...) wanneer u bij het maken van Visual Studio. Maar wanneer gebouwd met MSBuild, wordt dit ingevuld met de juiste versienummer Hallo.

    tooallow MSBuild toogenerate versienummers, stel de versie in hello, zoals `1.0.*` in AssemblyReference.cs

## <a name="version-and-release-tracking"></a>Versie en release bijhouden
toepassingsversie tootrack hello, zorg ervoor dat `buildinfo.config` wordt gegenereerd door de Engine voor het bouwen van Microsoft wordt uitgevoerd. Voeg het volgende toe in uw .csproj-bestand:  

```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
```

Wanneer Hallo Buildgegevens beschikbaar zijn, voegt Hallo Application Insights-webmodule automatisch **toepassingsversie** als een item van de eigenschap tooevery telemetrie. Hierdoor kunt u toofilter door versie bij het uitvoeren van [diagnostische zoekopdrachten](app-insights-diagnostic-search.md), of wanneer u [verkennen van metrische gegevens](app-insights-metrics-explorer.md).

Let er echter op dat Hallo buildversienummer alleen wordt gegenereerd door Hallo Microsoft bouwen Engine, niet door de ontwikkelaar van de Hallo bouwen in Visual Studio.

### <a name="release-annotations"></a>Release-aantekeningen
Als u Visual Studio Team Services gebruikt, kunt u [ophalen van de markering van een aantekening](app-insights-annotations.md) tooyour grafieken toegevoegd wanneer u een nieuwe versie. Hallo volgende afbeelding ziet u hoe deze markering wordt weergegeven.

![Schermopname van aantekening bij voorbeeldrelease in een grafiek](./media/app-insights-asp-net/release-annotation.png)
## <a name="next-steps"></a>Volgende stappen

* [Gedeelde bronnen voor meerdere functies](app-insights-monitor-multi-role-apps.md)
* [Maken van een telemetrie initialisatiefunctie toodistinguish A | Varianten B](app-insights-api-filtering-sampling.md#add-properties)
