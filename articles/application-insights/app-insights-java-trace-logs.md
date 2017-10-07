---
title: aaaExplore Java tracering geregistreerd in Azure Application Insights | Microsoft Docs
description: Search Log4J of Logback traceringen in Application Insights
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: fc0a9e2f-3beb-4f47-a9fe-3f86cd29d97a
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/12/2016
ms.author: bwren
ms.openlocfilehash: e5f8e8c67e57753ba7574b97aa96dbb41db00ce1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="explore-java-trace-logs-in-application-insights"></a>Java in Application Insights traceerlogboeken verkennen
Als u Logback en Log4J (versie 1.2 of 2.0) voor voor tracering, hebt u uw traceerlogboeken tooApplication Insights waar u kunt verkennen en zoeken op deze automatisch verzonden.

## <a name="install-hello-java-sdk"></a>Hallo Java SDK installeren

Installeer [Application Insights-SDK voor Java][java], als u nog niet hebt gedaan die.

(Als u niet dat tootrack HTTP-aanvragen wilt, kunt u de meeste van de XML-configuratiebestand Hallo weglaten, maar u moet ten minste Hallo opnemen `InstrumentationKey` element. U moet ook aanroepen `new TelemetryClient()` tooinitialize Hallo SDK.)


## <a name="add-logging-libraries-tooyour-project"></a>Logboekregistratie bibliotheken tooyour project toevoegen
*Kies de juiste manier Hallo voor uw project.*

#### <a name="if-youre-using-maven"></a>Als u Maven gebruikt...
Als uw project is al ingesteld om toouse Maven voor build, voegt u een van de volgende codefragmenten in het bestand pom.xml Hallo.

Vernieuw Projectafhankelijkheden hello, tooget Hallo binaire bestanden te downloaden.

*Logback*

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-logback</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

*Log4J v2.0*

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

*Log4J versie 1.2*

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j1_2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

#### <a name="if-youre-using-gradle"></a>Als u Gradle gebruikt...
Als uw project is al ingesteld om toouse Gradle voor build, Voeg een van de volgende regels toohello Hallo `dependencies` groep in uw build.gradle-bestand:

Vernieuw Projectafhankelijkheden hello, tooget Hallo binaire bestanden te downloaden.

**Logback**

```

    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-logback', version: '1.0.+'
```

**Log4J v2.0**

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j2', version: '1.0.+'
```

**Log4J versie 1.2**

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j1_2', version: '1.0.+'
```

#### <a name="otherwise-"></a>Of...
Downloaden en uitpakken van de juiste appender Hallo Hallo juiste bibliotheek tooyour project toevoegen:

| Logboek | Downloaden | Bibliotheek |
| --- | --- | --- |
| Logback |[SDK met Logback appender](https://aka.ms/xt62a4) |applicationinsights-logboekregistratie-logback |
| Log4J v2.0 |[SDK met Log4J v2 appender](https://aka.ms/qypznq) |applicationinsights-logboekregistratie-log4j2 |
| Log4j versie 1.2 |[SDK met Log4J versie 1.2 appender](https://aka.ms/ky9cbo) |applicationinsights-logboekregistratie-log4j1_2 |

## <a name="add-hello-appender-tooyour-logging-framework"></a>Hallo appender tooyour logboekregistratie framework toevoegen
toostart aan traceringen, samenvoegen Hallo relevante codefragment code toohello Log4J of Logback-configuratiebestand: 

*Logback*

```XML

    <appender name="aiAppender" 
      class="com.microsoft.applicationinsights.logback.ApplicationInsightsAppender">
    </appender>
    <root level="trace">
      <appender-ref ref="aiAppender" />
    </root>
```

*Log4J v2.0*

```XML

    <Configuration packages="com.microsoft.applicationinsights.Log4j">
      <Appenders>
        <ApplicationInsightsAppender name="aiAppender" />
      </Appenders>
      <Loggers>
        <Root level="trace">
          <AppenderRef ref="aiAppender"/>
        </Root>
      </Loggers>
    </Configuration>
```

*Log4J versie 1.2*

```XML

    <appender name="aiAppender" 
         class="com.microsoft.applicationinsights.log4j.v1_2.ApplicationInsightsAppender">
    </appender>
    <root>
      <priority value ="trace" />
      <appender-ref ref="aiAppender" />
    </root>
```

Hallo Application Insights appenders kunnen alleen worden verwezen door een geconfigureerde berichtenlogboek en niet per se Hallo hoofdmap berichtenlogboek (zoals weergegeven in de codevoorbeelden Hallo hierboven).

## <a name="explore-your-traces-in-hello-application-insights-portal"></a>Bekijk de traceringen in Hallo Application Insights-portal
Nu dat u hebt geconfigureerd uw project toosend tooApplication Insights traceert, kunt u bekijken en zoeken naar deze traceringen in Hallo Application Insights-portal in Hallo [Search] [ diagnostic] blade.

![Open in Hallo Application Insights-portal zoeken](./media/app-insights-java-trace-logs/10-diagnostics.png)

## <a name="next-steps"></a>Volgende stappen
[Diagnostische gegevens doorzoeken][diagnostic]

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md


