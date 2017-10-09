---
title: Java-web-appprestaties op Linux - Azure aaaMonitor | Microsoft Docs
description: Uitgebreid application performance monitoring van uw Java-website met de Hallo CollectD invoegtoepassing Application Insights.
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 40c68f45-197a-4624-bf89-541eb7323002
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: bwren
ms.openlocfilehash: f783e8607a83b2b43f67d3a2fc20f100aa2f75ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="collectd-linux-performance-metrics-in-application-insights"></a>collectd: Linux maatstaven voor prestaties in Application Insights


tooexplore systeemprestaties van Linux in [Application Insights](app-insights-overview.md), installeren [collectd](http://collectd.org/), samen met de Application Insights-invoegtoepassing. Deze oplossing open source worden verschillende statistieken voor systeem- en netwerkgegevens verzameld.

Doorgaans kunt u collectd als u al hebt [uw Java-webservice met Application Insights geïnstrumenteerd][java]. Dit biedt u meer gegevens toohelp tooenhance u de prestaties van uw app of het analyseren van problemen. 

![voorbeeldgrafieken](./media/app-insights-java-collectd/sample.png)

## <a name="get-your-instrumentation-key"></a>De instrumentatiesleutel ophalen
In Hallo [Microsoft Azure-portal](https://portal.azure.com)Open Hallo [Application Insights](app-insights-overview.md) resource waar u Hallo gegevens tooappear. (Of [Maak een nieuwe resource](app-insights-create-new-resource.md).)

Een kopie van de instrumentatiesleutel hello, waarmee Hallo resource in beslag nemen.

![Alles bekijken, opent u de resource en vervolgens in Hallo Essentials vervolgkeuzelijst, selecteer en kopieer Hallo Instrumentatiesleutel](./media/app-insights-java-collectd/02-props.png)

## <a name="install-collectd-and-hello-plug-in"></a>Installeer collectd en Hallo invoegtoepassing
Op de Linux-servers:

1. Installeer [collectd](http://collectd.org/) versie 5.4.0 of hoger.
2. Hallo downloaden [Application Insights-invoegtoepassing voor collectd writer](https://aka.ms/aijavasdk). Houd er rekening mee Hallo versienummer.
3. Hallo-invoegtoepassing JAR kopiëren naar `/usr/share/collectd/java`.
4. Bewerken `/etc/collectd/collectd.conf`:
   * Zorg ervoor dat [Hallo Java-invoegtoepassing](https://collectd.org/wiki/index.php/Plugin:Java) is ingeschakeld.
   * Update hello JVMArg voor Hallo java.class.path tooinclude Hallo JAR te volgen. Hallo versie nummer toomatch Hallo die één gedownloade bijwerken:
   * `/usr/share/collectd/java/applicationinsights-collectd-1.0.5.jar`
   * In dit fragment, met behulp van Hallo Instrumentatiesleutel van uw resource toevoegen:

```XML

     LoadPlugin "com.microsoft.applicationinsights.collectd.ApplicationInsightsWriter"
     <Plugin ApplicationInsightsWriter>
        InstrumentationKey "Your key"
     </Plugin>
```

Dit is onderdeel van een voorbeeldconfiguratiebestand:

```XML

    ...
    # collectd plugins
    LoadPlugin cpu
    LoadPlugin disk
    LoadPlugin load
    ...

    # Enable Java Plugin
    LoadPlugin "java"

    # Configure Java Plugin
    <Plugin "java">
      JVMArg "-verbose:jni"
      JVMArg "-Djava.class.path=/usr/share/collectd/java/applicationinsights-collectd-1.0.5.jar:/usr/share/collectd/java/collectd-api.jar"

      # Enabling Application Insights plugin
      LoadPlugin "com.microsoft.applicationinsights.collectd.ApplicationInsightsWriter"

      # Configuring Application Insights plugin
      <Plugin ApplicationInsightsWriter>
        InstrumentationKey "12345678-1234-1234-1234-123456781234"
      </Plugin>

      # Other plugin configurations ...
      ...
    </Plugin>
    ...
```

Configureer andere [collectd plugins](https://collectd.org/wiki/index.php/Table_of_Plugins), dat kan verschillende gegevens verzamelen van verschillende gegevensbronnen.

Start opnieuw op op basis van tooits collectd [handmatige](https://collectd.org/wiki/index.php/First_steps).

## <a name="view-hello-data-in-application-insights"></a>Hallo-gegevens weergeven in Application Insights
Open in uw Application Insights-resource [Metrics Explorer en grafieken toe te voegen][metrics], selecteren Hallo metrische gegevens wilt toosee van Hallo aangepaste categorie.

![](./media/app-insights-java-collectd/result.png)

Standaard worden Hallo metrische gegevens geaggregeerd alle host machines waaruit de Hallo metrische gegevens zijn verzameld. tooview hello metrische gegevens per host Hallo grafiek details blade, schakelt u Grouping en kies vervolgens toogroup door CollectD-Host.

## <a name="tooexclude-upload-of-specific-statistics"></a>uploaden van specifieke statistieken tooexclude
Hallo Application Insights-invoegtoepassing verzendt standaard alle Hallo gegevens verzameld door alle Hallo ingeschakeld collectd 'read' invoegtoepassingen gebruikt. 

tooexclude gegevens van specifieke invoegtoepassingen of gegevensbronnen:

* Hallo-configuratiebestand bewerken. 
* In `<Plugin ApplicationInsightsWriter>`, richtlijn regels als volgt toevoegen:

| Richtlijn | Effect |
| --- | --- |
| `Exclude disk` |Alle gegevens die worden verzameld door Hallo uitsluiten `disk` invoegtoepassing |
| `Exclude disk:read,write` |Hallo-bronnen met de naam uitsluiten `read` en `write` van Hallo `disk` invoegtoepassing. |

Afzonderlijke richtlijnen met een nieuwe regel.

## <a name="problems"></a>Problemen?
*Gegevens in de portal Hallo weergegeven niet*

* Open [Search] [ diagnostic] toosee als Hallo onbewerkte gebeurtenissen zijn ontvangen. Soms worden ze langer tooappear in metrics explorer.
* U moet mogelijk te[firewalluitzonderingen voor uitgaande gegevens instellen](app-insights-ip-addresses.md)
* Tracering in Application Insights-invoegtoepassing Hallo inschakelen. Deze regel in te voegen `<Plugin ApplicationInsightsWriter>`:
  * `SDKLogger true`
* Open een terminal en collectd starten in de uitgebreide modus toosee meldt problemen:
  * `sudo collectd -f`

## <a name="known-issue"></a>Bekende problemen

Hallo schrijven van Application Insights-invoegtoepassing is niet compatibel met bepaalde invoegtoepassingen lezen. Sommige invoegtoepassingen verzenden soms 'NaN', waarbij Hallo Application Insights-invoegtoepassing een getal met drijvende komma verwacht.

Symptoom: Hallo collectd logboek bevat fouten die zijn 'AI:... SyntaxError: onverwacht token N ".

Tijdelijke oplossing: Uitsluiten door Hallo probleem schrijven plugins verzamelde gegevens. 

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md


