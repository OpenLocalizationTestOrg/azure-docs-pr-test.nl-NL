---
title: aaaApplication Insights voor Java web-apps die al live zijn
description: Bewaking van een webtoepassing die al wordt uitgevoerd op uw server starten
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 12f3dbb9-915f-4087-87c9-807286030b0b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/10/2016
ms.author: bwren
ms.openlocfilehash: 2b01cd61657522ccf1d2d97b2a29cdeb08ec9a18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-java-web-apps-that-are-already-live"></a>Application Insights voor Java-web-apps die al live


Als u een webtoepassing die al wordt uitgevoerd op uw J2EE-server hebt, kunt u starten met bewaking [Application Insights](app-insights-overview.md) zonder Hallo toomake moet wijzigingen code of opnieuw moet compileren uw project. Met deze optie krijgt u informatie over HTTP-aanvragen verzonden tooyour server, niet-verwerkte uitzonderingen en prestatiemeteritems.

U hebt een abonnement te[Microsoft Azure](https://azure.com).

> [!NOTE]
> Hallo-procedure op deze pagina wordt Hallo SDK tooyour web-app toegevoegd tijdens runtime. Deze instrumentation runtime is handig als u niet wilt dat tooupdate of opnieuw opbouwen van de broncode. Maar indien mogelijk, raden we u [Hallo SDK toohello broncode toevoegen](app-insights-java-get-started.md) in plaats daarvan. Die biedt u meer mogelijkheden, zoals het schrijven van code tootrack gebruikersactiviteit.
> 
> 

## <a name="1-get-an-application-insights-instrumentation-key"></a>1. Een Application Insights-instrumentatiesleutel ophalen
1. Meld u aan toohello [Microsoft Azure-portal](https://portal.azure.com)
2. Maak een nieuwe Application Insights-resource en stel Hallo toepassing type tooJava-webtoepassing.
   
    ![Een naam invoeren, Java-web-app kiezen en op Maken klikken](./media/app-insights-java-live/02-create.png)

    Hallo-resource is gemaakt in een paar seconden.

4. Open de nieuwe resource Hallo en de instrumentatiesleutel ophalen. U moet toopaste deze sleutel in uw CodeProject binnenkort.
   
    ![In de nieuwe resource overzicht Hallo, klikt u op eigenschappen en Hallo Instrumentatiesleutel kopiëren](./media/app-insights-java-live/03-key.png)

## <a name="2-download-hello-sdk"></a>2. Hallo SDK downloaden
1. Hallo downloaden [Application Insights-SDK voor Java](https://aka.ms/aijavasdk). 
2. Pak op uw server Hallo SDK inhoud toohello-map van waaruit u de binaire project worden geladen. Als u Tomcat, zou deze map normaal zijn onder`webapps/<your_app_name>/WEB-INF/lib`

Houd er rekening mee dat u toorepeat dit op elke server-exemplaar en voor elke app moet.

## <a name="3-add-an-application-insights-xml-file"></a>3. Een Application Insights XML-bestand toevoegen
Maak ApplicationInsights.xml in Hallo map waarin u Hallo SDK hebt toegevoegd. In deze geplaatst Hallo na XML.

Vervang Hallo instrumentatiesleutel die u hebt gekregen hello Azure-portal.

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsights xmlns="http://schemas.microsoft.com/ApplicationInsights/2013/Settings" schemaVersion="2014-05-30">


      <!-- hello key from hello portal: -->

      <InstrumentationKey>** Your instrumentation key **</InstrumentationKey>


      <!-- HTTP request component (not required for bare API) -->

      <TelemetryModules>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebRequestTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebSessionTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebUserTrackingTelemetryModule"/>
      </TelemetryModules>

      <!-- Events correlation (not required for bare API) -->
      <!-- These initializers add context data tooeach event -->

      <TelemetryInitializers>
        <Add   type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationIdTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationNameTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebSessionTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserAgentTelemetryInitializer"/>

      </TelemetryInitializers>
    </ApplicationInsights>
```

* Hallo-instrumentatiesleutel samen met elk telemetrie-item is verzonden en instrueert Application Insights toodisplay in de resource.
* Hallo onderdeel HTTP-aanvraag is optioneel. Het verzendt automatisch telemetrie over aanvragen en -antwoord keren toohello portal.
* Correlatie tussen gebeurtenissen is een onderdeel toevoeging toohello HTTP-aanvraag. Het wijst een id tooeach-aanvraag is ontvangen door Hallo-server en deze id wordt als een item van de eigenschap tooevery telemetrie als Hallo-eigenschap 'Operation.Id'. Hiermee kunt u toocorrelate Hallo telemetrie die is gekoppeld aan elke aanvraag door een filter in te stellen [diagnostische gegevens doorzoeken](app-insights-diagnostic-search.md).

## <a name="4-add-an-http-filter"></a>4. Een HTTP-filter toevoegen
Zoek en open het web.xml-bestand Hallo in uw project en merge Hallo volgende codefragment onder Hallo web-app-knooppunt, waar de toepassingsfilters zijn geconfigureerd.

tooget hello nauwkeurigste resultaten Hallo filter moeten vóór alle andere filters worden toegewezen.

```XML

    <filter>
      <filter-name>ApplicationInsightsWebFilter</filter-name>
      <filter-class>
        com.microsoft.applicationinsights.web.internal.WebRequestTrackingFilter
      </filter-class>
    </filter>
    <filter-mapping>
       <filter-name>ApplicationInsightsWebFilter</filter-name>
       <url-pattern>/*</url-pattern>
    </filter-mapping>
```

## <a name="5-check-firewall-exceptions"></a>5. Controleer de firewall-uitzonderingen
U moet mogelijk te[uitzonderingen instellen toosend uitgaande gegevens](app-insights-ip-addresses.md).

## <a name="6-restart-your-web-app"></a>6. Opnieuw opstarten van uw web-app
## <a name="7-view-your-telemetry-in-application-insights"></a>7. Uw telemetrie in Application Insights weergeven
Application Insights-resource in tooyour retourneren [Microsoft Azure-portal](https://portal.azure.com).

Telemetrie over HTTP-aanvragen wordt weergegeven op de overzichtsblade Hallo. (Als dit niet het geval is, wacht u een paar seconden en klikt u vervolgens op Vernieuwen.)

![voorbeeldgegevens](./media/app-insights-java-live/5-results.png)

Klik op via een grafiek toosee gedetailleerdere metrische gegevens. 

![](./media/app-insights-java-live/6-barchart.png)

En wanneer u bekijkt hello eigenschappen van een aanvraag, ziet u Hallo telemetrische gebeurtenissen gekoppeld zoals aanvragen en uitzonderingen.

![](./media/app-insights-java-live/7-instance.png)

[Meer informatie over metrische gegevens.](app-insights-metrics-explorer.md)

## <a name="next-steps"></a>Volgende stappen
* [Voeg telemetrie tooyour webpagina's](app-insights-javascript.md) toomonitor pagina weergaven en metrische gegevens over gebruikers.
* [Webtests instellen](app-insights-monitor-web-app-availability.md) toomake zorgen dat uw toepassing live en responsief blijft.
* [Logboektraceringen vastleggen](app-insights-java-trace-logs.md)
* [Zoek naar gebeurtenissen en logboeken](app-insights-diagnostic-search.md) toohelp analyseren van problemen.

