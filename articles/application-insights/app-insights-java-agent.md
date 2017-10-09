---
title: aaaPerformance bewaking van Java-web-apps in Azure Application Insights | Microsoft Docs
description: Uitgebreide bewaking van prestaties en gebruik van uw Java-website met Application Insights.
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 84017a48-1cb3-40c8-aab1-ff68d65e2128
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: bwren
ms.openlocfilehash: bf3983e3b4a16e72bc606b6468a757288d05ebaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-dependencies-exceptions-and-execution-times-in-java-web-apps"></a>Afhankelijkheden, uitzonderingen en uitvoeringstijden in Java-web-apps bewaken


Als u hebt [uw Java-web-app met Application Insights geïnstrumenteerd][java], kunt u Hallo Java-Agent tooget beter inzicht, zonder codewijzigingen:

* **Afhankelijkheden:** gegevens over aanroepen die uw toepassing tooother onderdelen maakt, waaronder:
  * **REST-aanroepen** gedaan via HttpClient OkHttp en RestTemplate (bron).
  * **Redis** aanroepen via Hallo Jedis client. Als Hallo aanroep langer dan per 10 duurt, haalt Hallo agent ook Hallo aanroepargumenten.
  * **[JDBC aanroepen](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)**  -MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB of Apache Derby DB. aanroepen van 'executeBatch' worden ondersteund. Als Hallo aanroep langer dan per 10 duurt, rapporteert Hallo-agent voor MySQL en PostgreSQL Hallo queryplan.
* **Uitzonderingen wordt onderschept:** gegevens over uitzonderingen die worden verwerkt door uw code.
* **Uitvoeringstijd voor methode:** gegevens over Hallo keer dat er vergt tooexecute specifieke methoden.

toouse hello Java-agent, u deze installeren op uw server. Uw web-apps moeten zijn uitgerust met Hallo [Application Insights-SDK voor Java][java]. 

## <a name="install-hello-application-insights-agent-for-java"></a>Hallo Application Insights-agent voor Java installeren
1. Uitgevoerd uw Java-server op Hallo machine [Hallo-agent downloaden](https://aka.ms/aijavasdk).
2. Hallo application server opstartscript bewerken en volgende JVM Hallo toevoegen:
   
    `javaagent:`*volledig pad toohello agent JAR-bestand*
   
    Bijvoorbeeld in Tomcat op een Linux-machine:
   
    `export JAVA_OPTS="$JAVA_OPTS -javaagent:<full path tooagent JAR file>"`
3. Start de toepassingsserver van uw opnieuw.

## <a name="configure-hello-agent"></a>Hallo-agent configureren
Maak een bestand met de naam `AI-Agent.xml` en plaats deze in Hallo dezelfde map als Hallo agent JAR-bestand.

Hallo-inhoud van xml-bestand Hallo ingesteld. Hallo na voorbeeld tooinclude bewerken of Hallo-functies die u wilt weglaten.

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsightsAgent>
      <Instrumentation>

        <!-- Collect remote dependency data -->
        <BuiltIn enabled="true">
           <!-- Disable Redis or alter threshold call duration above which arguments are sent.
               Defaults: enabled, 10000 ms -->
           <Jedis enabled="true" thresholdInMS="1000"/>

           <!-- Set SQL query duration above which query plan is reported (MySQL, PostgreSQL). Default is 10000 ms. -->
           <MaxStatementQueryLimitInMS>1000</MaxStatementQueryLimitInMS>
        </BuiltIn>

        <!-- Collect data about caught exceptions
             and method execution times -->

        <Class name="com.myCompany.MyClass">
           <Method name="methodOne"
               reportCaughtExceptions="true"
               reportExecutionTime="true"
               />

           <!-- Report on hello particular signature
                void methodTwo(String, int) -->
           <Method name="methodTwo"
              reportExecutionTime="true"
              signature="(Ljava/lang/String;I)V" />
        </Class>

      </Instrumentation>
    </ApplicationInsightsAgent>

```

U hebt tooenable rapporten uitzondering en timing van de methode voor afzonderlijke methoden.

Standaard `reportExecutionTime` is ingesteld op true en `reportCaughtExceptions` is ingesteld op false.

## <a name="view-hello-data"></a>Hallo-gegevens weergeven
In Application Insights-resource hello, geaggregeerde externe afhankelijkheid en methode uitvoeringstijden weergegeven [onder Hallo prestaties tegel][metrics].

toosearch voor afzonderlijke exemplaren van afhankelijkheid en uitzondering methode rapporten openen [Search][diagnostic].

[Diagnose afhankelijkheidsproblemen - meer](app-insights-asp-net-dependencies.md#diagnosis).

## <a name="questions-problems"></a>Vragen? Problemen?
* Zijn er geen gegevens? [Set firewall-uitzonderingen](app-insights-ip-addresses.md)
* [Problemen met Java oplossen](app-insights-java-troubleshoot.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
