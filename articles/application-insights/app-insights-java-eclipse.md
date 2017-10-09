---
title: aaaGet slag met Azure Application Insights met behulp van Java in Eclipse | Microsoft docs
description: Hallo Eclipse invoegtoepassing tooadd prestaties en gebruik bewaking van Java-website met Application Insights tooyour gebruiken
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: e88c9f53-cd90-4abc-b097-1f170937908e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/12/2016
ms.author: bwren
ms.openlocfilehash: 3142a26a9e2d14c2c433882e3d337f2a8c8f2247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-application-insights-with-java-in-eclipse"></a>Aan de slag met Application Insights met behulp van Java in Eclipse
Hallo Application Insights-SDK verzendt telemetrie van uw Java-webtoepassing, zodat u gebruik en prestaties kan analyseren. Hallo Eclipse-invoegtoepassing voor Application Insights installeert automatisch Hallo SDK in uw project, zodat u buiten Hallo vak telemetrie, plus een API waarmee u kunt aangepaste telemetrie toowrite ophalen.   

## <a name="prerequisites"></a>Vereisten
Hallo-invoegtoepassing werkt momenteel voor Maven-projecten en dynamische webprojecten in Eclipse.
([Application Insights toevoegen tooother typen Java-project][java].)

U hebt het volgende nodig:

* Oracle JRE 1.6 of hoger
* Een abonnement te[Microsoft Azure](https://azure.microsoft.com/).
* [Eclipse IDE voor Java EE-ontwikkelaars](http://www.eclipse.org/downloads/), Indigo of hoger.
* Windows 7 of hoger, of WindowsServer 2008 of hoger

## <a name="install-hello-sdk-on-eclipse-one-time"></a>Hallo SDK installeren op Eclipse (eenmaal)
U hoeft alleen toodo dit één keer per computer. Deze stap installeert een werkset waarmee Hallo SDK tooeach dynamisch webproject vervolgens kunt toevoegen.

1. Klik op Help, nieuwe Software installeren in Eclipse.

    ![Help, installeert u nieuwe Software](./media/app-insights-java-eclipse/0-plugin.png)
2. Hallo SDK wordt http://dl.microsoft.com/eclipse onder Azure Toolkit.
3. Schakel het selectievakje **Neem contact op met alle updatewebsites...**

    ![Voor Application Insights-SDK, schakelt u contact op met bijwerken alle sites](./media/app-insights-java-eclipse/1-plugin.png)

Ga als volgt Hallo resterende stappen voor elk Java-project.

## <a name="create-an-application-insights-resource-in-azure"></a>Een Application Insights-resource maken in Azure
1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Maak een nieuwe Application Insights-resource. Hallo toepassing type tooJava-webtoepassing instellen.  

    ![Op + klikken en Application Insights kiezen](./media/app-insights-java-eclipse/01-create.png)  

4. Hallo-instrumentatiesleutel van Hallo nieuwe bron vinden. U moet toopaste dit in uw CodeProject binnenkort.  

    ![In de nieuwe resource overzicht Hallo, klikt u op eigenschappen en Hallo Instrumentatiesleutel kopiëren](./media/app-insights-java-eclipse/03-key.png)  

## <a name="add-application-insights-tooyour-project"></a>Application Insights tooyour project toevoegen
1. Application Insights toevoegen in het contextmenu Hallo van uw Java-webproject.

    ![In de nieuwe resource overzicht Hallo, klikt u op eigenschappen en Hallo Instrumentatiesleutel kopiëren](./media/app-insights-java-eclipse/02-context-menu.png)
2. Plak Hallo instrumentatiesleutel die u hebt gekregen hello Azure-portal.

    ![In de nieuwe resource overzicht Hallo, klikt u op eigenschappen en Hallo Instrumentatiesleutel kopiëren](./media/app-insights-java-eclipse/03-ikey.png)

Hallo sleutel samen met elk telemetrie-item is verzonden en instrueert Application Insights toodisplay in de resource.

## <a name="run-hello-application-and-see-metrics"></a>Voer de toepassing hello en metrische gegevens
Voer uw toepassing.

Tooyour Application Insights-resource in Microsoft Azure retourneren.

HTTP-aanvragen gegevens worden weergegeven op de overzichtsblade Hallo. (Als dit niet het geval is, wacht u een paar seconden en klikt u vervolgens op Vernieuwen.)

![Reactie van server, telt het aantal aanvragen en fouten ](./media/app-insights-java-eclipse/5-results.png)

Klik op via een grafiek toosee gedetailleerdere metrische gegevens.

![Het aantal aanvragen met de naam](./media/app-insights-java-eclipse/6-barchart.png)

[Meer informatie over metrische gegevens.][metrics]

En wanneer u bekijkt hello eigenschappen van een aanvraag, ziet u Hallo telemetrische gebeurtenissen gekoppeld zoals aanvragen en uitzonderingen.

![Alle traces voor deze aanvraag](./media/app-insights-java-eclipse/7-instance.png)

## <a name="client-side-telemetry"></a>Telemetrie-clientzijde
Hallo Quick Start-blade, klik op Get code toomonitor mijn webpagina's:

![Op de overzichtsblade van uw app, kiest u snel starten, kunt u code toomonitor mijn webpagina's. Hallo script kopiëren.](./media/app-insights-java-eclipse/02-monitor-web-page.png)

Hallo-codefragment invoegen in Hallo-head van uw HTML-bestanden.

#### <a name="view-client-side-data"></a>Client-side '-gegevens weergeven
Open uw bijgewerkte webpagina's en ze gebruiken. Wacht een minuut of twee en tooApplication Insights en open Hallo gebruik blade geretourneerd. (Overzichtsblade hello, schuif naar beneden en klik op informatie over het gebruik.)

Pagina metrische gegevens weergeven, de gebruiker en de sessie wordt weergegeven op Hallo gebruik blade:

![Sessies, gebruikers en paginaweergaven](./media/app-insights-java-eclipse/appinsights-47usage-2.png)

[Meer informatie over het instellen van de client-side telemetrie.][usage]

## <a name="publish-your-application"></a>Uw toepassing publiceren
Publiceer nu uw app toohello-server, kunnen gebruikers worden gebruikt en bekijkt hello telemetrie op Hallo portal weergegeven.

* Zorg ervoor dat uw firewall kunt uw toepassing toosend telemetrie toothese poorten:

  * dc.services.visualstudio.com:443
  * dc.services.visualstudio.com:80
  * f5.services.visualstudio.com:443
  * f5.services.visualstudio.com:80
* Installeer op Windows-servers:

  * [Microsoft Visual C++ Redistributable](http://www.microsoft.com/download/details.aspx?id=40784)

    (Hiermee kunt u prestatiemeteritems instellen.)

## <a name="exceptions-and-request-failures"></a>Uitzonderingen en mislukte aanvragen
Onverwerkte uitzonderingen worden automatisch verzameld:

![](./media/app-insights-java-eclipse/21-exceptions.png)

toocollect gegevens over andere uitzonderingen, hebt u twee opties:

* [INSERT tooTrackException in uw code roept](app-insights-api-custom-events-metrics.md#trackexception).
* [Hallo Java-Agent installeren op uw server](app-insights-java-agent.md). U opgeven Hallo-methoden die u wilt dat toowatch.

## <a name="monitor-method-calls-and-external-dependencies"></a>Methodeaanroepen en externe afhankelijkheden bewaken
[Hallo Java-Agent installeren](app-insights-java-agent.md) toolog opgegeven interne methoden en oproepen via JDBC vast, inclusief timinggegevens.

## <a name="performance-counters"></a>Prestatiemeteritems
Op de overzichtsblade Schuif naar beneden en klikt u op Hallo **Servers** tegel. Hier ziet u een groot aantal prestatiemeteritems.

![Schuif naar beneden tooclick Hallo Servers tegel](./media/app-insights-java-eclipse/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a>Het verzamelen van prestatiemeteritems aanpassen
toodisable verzameling Hallo standaardset prestatiemeteritems toevoegen Hallo code onder de hoofdknooppunt Hallo van Hallo ApplicationInsights.xml-bestand te volgen:

```XML

    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a>Verzamelen van aanvullende prestatiemeteritems
U kunt aanvullende prestatie-items toobe verzamelde opgeven.

#### <a name="jmx-counters-exposed-by-hello-java-virtual-machine"></a>JMX-tellers (weergegeven door Hallo virtuele Java-Machine)

```XML

    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* `displayName`– Hallo naam die wordt weergegeven in Hallo Application Insights-portal.
* `objectName`– hello JMX-objectnaam.
* `attribute`– Hallo-kenmerk van Hallo JMX-object naam toofetch
* `type`(optioneel) - Hallo type van kenmerk JMX-object:
  * Standaard: een eenvoudig type, zoals int of long.
  * `composite`: Hallo prestatiemetergegevens is Hallo indeling 'Attribute.Data'
  * `tabular`: Hallo prestatiemetergegevens heeft Hallo-indeling van de rij in een tabel

#### <a name="windows-performance-counters"></a>Windows-prestatiemeteritems
Elke [Windows-prestatiemeteritem](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) lid is van een categorie (in Hallo dezelfde manier als een veld deel uitmaakt van een klasse). Categorieën kunnen globaal zijn, maar ook genummerde of benoemde exemplaren hebben.

```XML

    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* displayName: Hallo naam weergegeven in Hallo Application Insights-portal.
* Categorynaam: Hallo prestatiemeteritemcategorie (prestatie-object) waaraan dit prestatiemeteritem gekoppeld is.
* counterName: de naam van het prestatiemeteritem Hallo Hallo.
* instanceName: de naam van exemplaar categorie Hallo van prestatiemeteritem hello of een lege tekenreeks (""), als Hallo categorie slechts één exemplaar bevat. Als Hallo categorienaam Process, en Hallo prestatiemeteritem gewenst toocollect is uit de huidige JVM-proces Hallo op waarop uw app wordt uitgevoerd, specificeert `"__SELF__"`.

De prestatiemeteritems zijn zichtbaar als aangepaste metrische gegevens in [Metrics Explorer][metrics].

![](./media/app-insights-java-eclipse/12-custom-perfs.png)

### <a name="unix-performance-counters"></a>Unix-prestatiemeteritems
* [Installeer collectd met Application Insights-invoegtoepassing Hallo](app-insights-java-collectd.md) tooget een scala aan systeem- en netwerkbeveiliging.

## <a name="availability-web-tests"></a>Webtests voor beschikbaarheid
Application Insights kunnen testen uw website op regelmatige intervallen toocheck of deze actief is en goed reageert. [tooset up][availability], schuif omlaag tooclick beschikbaarheid.

![Omlaag schuiven, op Beschikbaarheid klikken en vervolgens op Webtest toevoegen klikken](./media/app-insights-java-eclipse/31-config-web-test.png)

Er worden grafieken weergegeven met reactietijden en u ontvangt e-mailmeldingen als uw site uitvalt.

![Voorbeeld van een webtest](./media/app-insights-java-eclipse/appinsights-10webtestresult.png)

[Meer informatie over de webtests voor beschikbaarheid.][availability]

## <a name="diagnostic-logs"></a>Diagnostische logboeken
Als u Logback en Log4J (versie 1.2 of 2.0) voor voor tracering, hebt u uw traceerlogboeken tooApplication Insights waar u kunt verkennen en zoeken op deze automatisch verzonden.

[Meer informatie over diagnostische logboeken][javalogs]

## <a name="custom-telemetry"></a>Aangepaste telemetrie
Een paar regels code in uw Java web application toofind uit wat gebruikers met het doen invoegen of toohelp analyseren van problemen.

U kunt de code kunt invoegen in webpagina's, JavaScript en in Hallo serverzijde Java.

[Meer informatie over aangepaste telemetrie][track]

## <a name="next-steps"></a>Volgende stappen
#### <a name="detect-and-diagnose-issues"></a>Detecteren en onderzoeken van problemen
* [Voeg telemetrie van de webclient] [ usage] tooget prestatietelemetrie van de webclient Hallo.
* [Webtests instellen] [ availability] toomake zorgen dat uw toepassing live en responsief blijft.
* [Zoek naar gebeurtenissen en logboeken] [ diagnostic] toohelp analyseren van problemen.
* [Vastleggen van traces Log4J of Logback][javalogs]

#### <a name="track-usage"></a>Bijhouden van gebruik
* [Voeg telemetrie van de webclient] [ usage] toomonitor pagina weergaven en basisgebruiker metrische gegevens.
* [Aangepaste gebeurtenissen en metrische gegevens bijhouden](app-insights-web-track-usage.md) toolearn over hoe uw toepassing wordt gebruikt, zowel op Hallo-client en server Hallo.

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md
