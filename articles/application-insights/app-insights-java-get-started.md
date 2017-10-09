---
title: aaaJava web app analytics met Azure Application Insights | Microsoft Docs
description: 'Toepassingsprestaties bewaken met Application Insights voor Java-web-apps. '
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 051d4285-f38a-45d8-ad8a-45c3be828d91
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 6555ee53a44f937350e4fa296080f7dce4f45226
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-application-insights-in-a-java-web-project"></a>Aan de slag met Application Insights in een Java-webproject


[Application Insights](https://azure.microsoft.com/services/application-insights/) is een uitbreidbare Analyseservice voor webontwikkelaars die u helpt Hallo prestaties en gebruik van uw live-toepassing te begrijpen. Te gebruiken[detecteren en onderzoeken van prestatieproblemen en uitzonderingen](app-insights-detect-triage-diagnose.md), en [code schrijven] [ api] tootrack wat gebruikers met uw app doen.

![voorbeeldgegevens](./media/app-insights-java-get-started/5-results.png)

Application Insights biedt ondersteuning voor Java-apps die in Linux, Unix of Windows worden uitgevoerd.

U hebt de volgende zaken nodig:

* Oracle JRE 1.6 of hoger, of Zulu JRE 1.6 of hoger
* Een abonnement te[Microsoft Azure](https://azure.microsoft.com/).

*Als u een web-app die al live hebt, kunt u volgen Hallo alternatieve procedure te[Hallo SDK tijdens runtime in Hallo webserver toevoegen](app-insights-java-live.md). Met deze alternatieve voorkomt Hallo code opnieuw samenstellen, maar er geen gebruikersactiviteit Hallo optie toowrite code tootrack.*

## <a name="1-get-an-application-insights-instrumentation-key"></a>1. Een Application Insights-instrumentatiesleutel ophalen
1. Meld u aan toohello [Microsoft Azure-portal](https://portal.azure.com).
2. Maak een Application Insights-resource. Hallo toepassing type tooJava-webtoepassing instellen.

    ![Een naam invoeren, Java-web-app kiezen en op Maken klikken](./media/app-insights-java-get-started/02-create.png)
3. Hallo-instrumentatiesleutel van Hallo nieuwe bron vinden. U moet toopaste deze sleutel in uw CodeProject binnenkort.

    ![In de nieuwe resource overzicht Hallo, klikt u op eigenschappen en Hallo Instrumentatiesleutel kopiëren](./media/app-insights-java-get-started/03-key.png)

## <a name="2-add-hello-application-insights-sdk-for-java-tooyour-project"></a>2. Hallo Application Insights-SDK voor Java tooyour project toevoegen
*Kies de juiste manier Hallo voor uw project.*

#### <a name="if-youre-using-eclipse-toocreate-a-maven-or-dynamic-web-project-"></a>Als u een Maven- of Dynamic Web project Eclipse toocreate...
Gebruik Hallo [Application Insights-SDK voor Java-invoegtoepassing][eclipse].

#### <a name="if-youre-using-maven"></a>Als u Maven gebruikt...
Als uw project is al ingesteld om toouse Maven voor build, foutcode samenvoegen Hallo volgende tooyour pom.xml-bestand.

Vervolgens vernieuwen Hallo project afhankelijkheden tooget Hallo binaire bestanden worden gedownload.

```XML

    <repositories>
       <repository>
          <id>central</id>
          <name>Central</name>
          <url>http://repo1.maven.org/maven2</url>
       </repository>
    </repositories>

    <dependencies>
      <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>applicationinsights-web</artifactId>
        <!-- or applicationinsights-core for bare API -->
        <version>[1.0,)</version>
      </dependency>
    </dependencies>
```

* *Validatiefouten in build of controlesom?* Probeer een specifieke versie te gebruiken, bijvoorbeeld: `<version>1.0.n</version>`. U vindt de nieuwste versie Hallo in Hallo [SDK-releaseopmerkingen](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) of in onze [Maven-artefacten](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights).
* *Tooupdate tooa nodig nieuwe SDK?* Vernieuw de afhankelijkheden van uw project.

#### <a name="if-youre-using-gradle"></a>Als u Gradle gebruikt...
Als uw project is al ingesteld om toouse Gradle voor build, foutcode samenvoegen Hallo volgende tooyour build.gradle-bestand.

Vervolgens vernieuwen Hallo project afhankelijkheden tooget Hallo binaire bestanden worden gedownload.

```JSON

    repositories {
      mavenCentral()
    }

    dependencies {
      compile group: 'com.microsoft.azure', name: 'applicationinsights-web', version: '1.+'
      // or applicationinsights-core for bare API
    }
```

* *Validatiefouten in build of controlesom? Probeer een specifieke versie te gebruiken, bijvoorbeeld:* `version:'1.0.n'`. *U vindt de nieuwste versie Hallo in Hallo [SDK-releaseopmerkingen](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).*
* *tooupdate tooa nieuwe SDK*
  * Vernieuw de afhankelijkheden van uw project.

#### <a name="otherwise-"></a>Of...
Handmatig toevoegen Hallo SDK:

1. Hallo downloaden [Application Insights-SDK voor Java](https://aka.ms/aijavasdk).
2. Hallo binaire bestanden van Hallo zip-bestand extraheren en ze tooyour project toevoegen.

### <a name="questions"></a>Vragen...
* *Wat is de relatie Hallo tussen Hallo `-core` en `-web` onderdelen in Hallo ZIP-bestand?*

  * `applicationinsights-core`biedt Hallo van bare-API. U hebt dit onderdeel altijd nodig.
  * `applicationinsights-web` biedt u metrische gegevens waarin het aantal HTTP-aanvragen en -reactietijden worden bijhouden. U kunt dit onderdeel weglaten als u deze telemetrie niet automatisch wilt verzamelen. Bijvoorbeeld als u wilt dat toowrite zelf.
* *tooupdate hello SDK wanneer we wijzigingen publiceren*

  * Meest recente Hallo downloaden [Application Insights-SDK voor Java](https://aka.ms/qqkaq6) en vervang Hallo oude versie.
  * Wijzigingen worden beschreven in Hallo [SDK-releaseopmerkingen](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).

## <a name="3-add-an-application-insights-xml-file"></a>3. Een Application Insights-.xml-bestand toevoegen
ApplicationInsights.xml toohello resourcesmap in uw project toevoegen of zorg dat het implementatieklassepad van het project tooyour is toegevoegd. Hallo XML in het volgende kopiëren.

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
* Correlatie tussen gebeurtenissen is een onderdeel toevoeging toohello HTTP-aanvraag. Het wijst een id tooeach-aanvraag is ontvangen door Hallo-server en deze id wordt als een item van de eigenschap tooevery telemetrie als Hallo-eigenschap 'Operation.Id'. Hiermee kunt u toocorrelate Hallo telemetrie die is gekoppeld aan elke aanvraag door een filter in te stellen [diagnostische gegevens doorzoeken][diagnostic].
* Hallo Application Insights-sleutel van kan worden doorgegeven dynamisch hello Azure-portal als een systeemeigenschap (-DAPPLICATION_INSIGHTS_IKEY = your_ikey). Als er geen eigenschap is gedefinieerd, wordt gecontroleerd op omgevingsvariabelen (APPLICATION_INSIGHTS_IKEY) in de Azure App-instellingen. Als beide Hallo-eigenschappen niet gedefinieerd zijn, wordt standaard Hallo InstrumentationKey van ApplicationInsights.xml gebruikt. Deze reeks helpt u bij toomanage verschillende InstrumentationKeys voor verschillende omgevingen dynamisch.

### <a name="alternative-ways-tooset-hello-instrumentation-key"></a>Alternatieve manieren tooset hello instrumentatiesleutel
Application Insights-SDK wordt gezocht naar Hallo-sleutel in deze volgorde:

1. Systeemeigenschap: -DAPPLICATION_INSIGHTS_IKEY=your_ikey
2. Omgevingsvariabele: APPLICATION_INSIGHTS_IKEY
3. Configuratiebestand: ApplicationInsights.xml

U kunt de instrumentatiesleutel ook [instellen in code](app-insights-api-custom-events-metrics.md#ikey):

```Java

    telemetryClient.InstrumentationKey = "...";
```

## <a name="4-add-an-http-filter"></a>4. Een HTTP-filter toevoegen
de laatste configuratiestap Hallo kunt Hallo HTTP-aanvraag onderdeel toolog elke webaanvraag. (Niet vereist als u alleen Hallo bare-API wilt).

Zoek en open het web.xml-bestand Hallo in uw project en merge Hallo na de code onder Hallo web-app-knooppunt, waar de toepassingsfilters zijn geconfigureerd.

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

#### <a name="if-youre-using-spring-web-mvc-31-or-later"></a>Als u Spring Web MVC 3.1 of hoger gebruikt
Bewerk deze elementen in *-servlet.xml tooinclude Hallo Application Insights-pakket:

```XML

    <context:component-scan base-package=" com.springapp.mvc, com.microsoft.applicationinsights.web.spring"/>

    <mvc:interceptors>
        <mvc:interceptor>
            <mvc:mapping path="/**"/>
            <bean class="com.microsoft.applicationinsights.web.spring.RequestNameHandlerInterceptorAdapter" />
        </mvc:interceptor>
    </mvc:interceptors>
```

#### <a name="if-youre-using-struts-2"></a>Als u Struts 2 gebruikt
Voeg dit item toohello Struts-configuratiebestand (meestal benoemde struts.xml of struts-default.xml):

```XML

     <interceptors>
       <interceptor name="ApplicationInsightsRequestNameInterceptor" class="com.microsoft.applicationinsights.web.struts.RequestNameInterceptor" />
     </interceptors>
     <default-interceptor-ref name="ApplicationInsightsRequestNameInterceptor" />
```

(Als u interceptors gedefinieerd in een standaardstack hebt, Hallo interceptor kan alleen worden toegevoegd toothat stack.)

## <a name="5-run-your-application"></a>5. Uw toepassing uitvoeren
Ofwel het uitvoeren in de foutopsporingsmodus op uw ontwikkelcomputer of publiceer tooyour server.

## <a name="6-view-your-telemetry-in-application-insights"></a>6. Uw telemetrie in Application Insights weergeven
Application Insights-resource in tooyour retourneren [Microsoft Azure-portal](https://portal.azure.com).

HTTP-aanvragen gegevens worden weergegeven op de overzichtsblade Hallo. (Als dit niet het geval is, wacht u een paar seconden en klikt u vervolgens op Vernieuwen.)

![voorbeeldgegevens](./media/app-insights-java-get-started/5-results.png)

[Meer informatie over metrische gegevens.][metrics]

Klik door elke grafiek toosee gedetailleerdere metrische gegevens geaggregeerd.

![](./media/app-insights-java-get-started/6-barchart.png)

> Application Insights gaat uit Hallo-indeling van HTTP-aanvragen voor MVC-toepassingen: `VERB controller/action`. Bijvoorbeeld, `GET Home/Product/f9anuh81`, `GET Home/Product/2dffwrf5` en `GET Home/Product/sdf96vws` worden gegroepeerd in `GET Home/Product`. Door deze groepering kunnen er zinvolle sets van aanvragen worden samengesteld, zoals het aantal aanvragen en de gemiddelde runtime voor aanvragen.
>
>

### <a name="instance-data"></a>Gegevens van exemplaren
Klik in een specifieke aanvraag type toosee afzonderlijke exemplaren.

In Application Insights worden twee soorten gegevens weergegeven: cumulatieve gegevens (opgeslagen en weergegeven als gemiddelden, aantallen en sommen) en gegevens van exemplaren (afzonderlijke rapporten over HTTP-aanvragen, uitzonderingen, paginaweergaven of aangepaste gebeurtenissen).

Wanneer u bekijkt hello eigenschappen van een aanvraag, ziet u Hallo telemetrische gebeurtenissen gekoppeld zoals aanvragen en uitzonderingen.

![](./media/app-insights-java-get-started/7-instance.png)

### <a name="analytics-powerful-query-language"></a>Analyse: krachtige querytaal
Als u meer gegevens verzamelt, kunt u query's uitvoeren beide tooaggregate gegevens en toofind afzonderlijke exemplaren.  [Analyse](app-insights-analytics.md) is een krachtig hulpprogramma om inzicht te krijgen in prestaties en gebruik, en om diagnoses uit te voeren.

![Voorbeeld van het hulpprogramma Analyse](./media/app-insights-java-get-started/025.png)

## <a name="7-install-your-app-on-hello-server"></a>7. Uw app op Hallo-server installeren
Publiceer nu uw app toohello-server, kunnen gebruikers worden gebruikt en bekijkt hello telemetrie op Hallo portal weergegeven.

* Zorg ervoor dat uw firewall kunt uw toepassing toosend telemetrie toothese poorten:

  * dc.services.visualstudio.com:443
  * f5.services.visualstudio.com:443

* Als uitgaand verkeer via een firewall moet worden gerouteerd, definieert u de systeemeigenschappen `http.proxyHost` en `http.proxyPort`.

* Installeer op Windows-servers:

  * [Microsoft Visual C++ Redistributable](http://www.microsoft.com/download/details.aspx?id=40784)

    (Dit onderdeel schakelt prestatiemeteritems in.)


## <a name="exceptions-and-request-failures"></a>Uitzonderingen en mislukte aanvragen
Onverwerkte uitzonderingen worden automatisch verzameld:

![Open Instellingen, Fouten](./media/app-insights-java-get-started/21-exceptions.png)

toocollect gegevens over andere uitzonderingen, hebt u twee opties:

* [INSERT tootrackException() in uw code roept][apiexceptions].
* [Hallo Java-Agent installeren op uw server](app-insights-java-agent.md). U opgeven Hallo-methoden die u wilt dat toowatch.

## <a name="monitor-method-calls-and-external-dependencies"></a>Methodeaanroepen en externe afhankelijkheden bewaken
[Hallo Java-Agent installeren](app-insights-java-agent.md) toolog opgegeven interne methoden en oproepen via JDBC vast, inclusief timinggegevens.

## <a name="performance-counters"></a>Prestatiemeteritems
Open **instellingen**, **Servers**, toosee een groot aantal prestatiemeteritems.

![](./media/app-insights-java-get-started/11-perf-counters.png)

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

![](./media/app-insights-java-get-started/12-custom-perfs.png)

### <a name="unix-performance-counters"></a>Unix-prestatiemeteritems
* [Installeer collectd met Application Insights-invoegtoepassing Hallo](app-insights-java-collectd.md) tooget een scala aan systeem- en netwerkbeveiliging.

## <a name="get-user-and-session-data"></a>Gebruikers- en sessiegegevens ophalen
U verzendt nu telemetrie vanaf de webserver. Nu Hallo tooget 360-graden weergave van uw toepassing, kunt u meer controle toevoegen:

* [Voeg telemetrie tooyour webpagina's] [ usage] toomonitor pagina weergaven en metrische gegevens over gebruikers.
* [Webtests instellen] [ availability] toomake zorgen dat uw toepassing live en responsief blijft.

## <a name="capture-log-traces"></a>Logboektraceringen vastleggen
U kunt Application Insights tooslice gebruiken en te analyseren, logboeken van Log4J, Logback en andere frameworks voor logboekregistratie. U kunt Hallo logboeken correleren met HTTP-aanvragen en andere telemetrie. [Meer informatie][javalogs].

## <a name="send-your-own-telemetry"></a>Uw eigen telemetrie verzenden
Nu dat u Hallo SDK hebt geïnstalleerd, kunt u uw eigen telemetrie Hallo API toosend gebruiken.

* [Aangepaste gebeurtenissen en metrische gegevens bijhouden] [ api] toolearn wat gebruikers met uw toepassing doen.
* [Zoek naar gebeurtenissen en logboeken] [ diagnostic] toohelp analyseren van problemen.

## <a name="availability-web-tests"></a>Webtests voor beschikbaarheid
Application Insights kunnen testen uw website op regelmatige intervallen toocheck of deze actief is en goed reageert. [tooset up][availability], klikt u op webtests.

![Klik op webtests en vervolgens op Webtest toevoegen.](./media/app-insights-java-get-started/31-config-web-test.png)

Er worden grafieken weergegeven met reactietijden en u ontvangt e-mailmeldingen als uw site uitvalt.

![Voorbeeld van een webtest](./media/app-insights-java-get-started/appinsights-10webtestresult.png)

[Meer informatie over de webtests voor beschikbaarheid.][availability]

## <a name="questions-problems"></a>Vragen? Problemen?
[Problemen met Java oplossen](app-insights-java-troubleshoot.md)

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Volgende stappen
* [Afhankelijkheidsaanroepen bewaken](app-insights-java-agent.md)
* [Unix-prestatiemeteritems bewaken](app-insights-java-collectd.md)
* Voeg [tooyour webpagina's bewaken](app-insights-javascript.md) toomonitor laadtijd time-out, AJAX-aanroepen browseruitzonderingen.
* Schrijven [aangepaste telemetrie](app-insights-api-custom-events-metrics.md) tootrack gebruik in Hallo browser of op Hallo-server.
* Maak [dashboards](app-insights-dashboards.md) toobring samen Hallo sleutel grafieken voor het bewaken van uw systeem.
* Gebruik [Analytics](app-insights-analytics.md) om vanuit uw app krachtige query's voor telemetrie uit te voeren
* Voor meer informatie gaat u naar [Azure voor Java-ontwikkelaars](/java/azure).

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#trackexception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[usage]: app-insights-javascript.md
