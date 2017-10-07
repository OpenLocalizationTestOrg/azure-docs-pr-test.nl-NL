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
# <a name="explore-java-trace-logs-in-application-insights"></a><span data-ttu-id="0bc04-103">Java in Application Insights traceerlogboeken verkennen</span><span class="sxs-lookup"><span data-stu-id="0bc04-103">Explore Java trace logs in Application Insights</span></span>
<span data-ttu-id="0bc04-104">Als u Logback en Log4J (versie 1.2 of 2.0) voor voor tracering, hebt u uw traceerlogboeken tooApplication Insights waar u kunt verkennen en zoeken op deze automatisch verzonden.</span><span class="sxs-lookup"><span data-stu-id="0bc04-104">If you're using Logback or Log4J (v1.2 or v2.0) for tracing, you can have your trace logs sent automatically tooApplication Insights where you can explore and search on them.</span></span>

## <a name="install-hello-java-sdk"></a><span data-ttu-id="0bc04-105">Hallo Java SDK installeren</span><span class="sxs-lookup"><span data-stu-id="0bc04-105">Install hello Java SDK</span></span>

<span data-ttu-id="0bc04-106">Installeer [Application Insights-SDK voor Java][java], als u nog niet hebt gedaan die.</span><span class="sxs-lookup"><span data-stu-id="0bc04-106">Install [Application Insights SDK for Java][java], if you haven't already done that.</span></span>

<span data-ttu-id="0bc04-107">(Als u niet dat tootrack HTTP-aanvragen wilt, kunt u de meeste van de XML-configuratiebestand Hallo weglaten, maar u moet ten minste Hallo opnemen `InstrumentationKey` element.</span><span class="sxs-lookup"><span data-stu-id="0bc04-107">(If you don't want tootrack HTTP requests, you can omit most of hello .xml configuration file, but you must at least include hello `InstrumentationKey` element.</span></span> <span data-ttu-id="0bc04-108">U moet ook aanroepen `new TelemetryClient()` tooinitialize Hallo SDK.)</span><span class="sxs-lookup"><span data-stu-id="0bc04-108">You should also call `new TelemetryClient()` tooinitialize hello SDK.)</span></span>


## <a name="add-logging-libraries-tooyour-project"></a><span data-ttu-id="0bc04-109">Logboekregistratie bibliotheken tooyour project toevoegen</span><span class="sxs-lookup"><span data-stu-id="0bc04-109">Add logging libraries tooyour project</span></span>
<span data-ttu-id="0bc04-110">*Kies de juiste manier Hallo voor uw project.*</span><span class="sxs-lookup"><span data-stu-id="0bc04-110">*Choose hello appropriate way for your project.*</span></span>

#### <a name="if-youre-using-maven"></a><span data-ttu-id="0bc04-111">Als u Maven gebruikt...</span><span class="sxs-lookup"><span data-stu-id="0bc04-111">If you're using Maven...</span></span>
<span data-ttu-id="0bc04-112">Als uw project is al ingesteld om toouse Maven voor build, voegt u een van de volgende codefragmenten in het bestand pom.xml Hallo.</span><span class="sxs-lookup"><span data-stu-id="0bc04-112">If your project is already set up toouse Maven for build, merge one of hello following snippets of code into your pom.xml file.</span></span>

<span data-ttu-id="0bc04-113">Vernieuw Projectafhankelijkheden hello, tooget Hallo binaire bestanden te downloaden.</span><span class="sxs-lookup"><span data-stu-id="0bc04-113">Then refresh hello project dependencies, tooget hello binaries downloaded.</span></span>

<span data-ttu-id="0bc04-114">*Logback*</span><span class="sxs-lookup"><span data-stu-id="0bc04-114">*Logback*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-logback</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

<span data-ttu-id="0bc04-115">*Log4J v2.0*</span><span class="sxs-lookup"><span data-stu-id="0bc04-115">*Log4J v2.0*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

<span data-ttu-id="0bc04-116">*Log4J versie 1.2*</span><span class="sxs-lookup"><span data-stu-id="0bc04-116">*Log4J v1.2*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j1_2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

#### <a name="if-youre-using-gradle"></a><span data-ttu-id="0bc04-117">Als u Gradle gebruikt...</span><span class="sxs-lookup"><span data-stu-id="0bc04-117">If you're using Gradle...</span></span>
<span data-ttu-id="0bc04-118">Als uw project is al ingesteld om toouse Gradle voor build, Voeg een van de volgende regels toohello Hallo `dependencies` groep in uw build.gradle-bestand:</span><span class="sxs-lookup"><span data-stu-id="0bc04-118">If your project is already set up toouse Gradle for build, add one of hello following lines toohello `dependencies` group in your build.gradle file:</span></span>

<span data-ttu-id="0bc04-119">Vernieuw Projectafhankelijkheden hello, tooget Hallo binaire bestanden te downloaden.</span><span class="sxs-lookup"><span data-stu-id="0bc04-119">Then refresh hello project dependencies, tooget hello binaries downloaded.</span></span>

<span data-ttu-id="0bc04-120">**Logback**</span><span class="sxs-lookup"><span data-stu-id="0bc04-120">**Logback**</span></span>

```

    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-logback', version: '1.0.+'
```

<span data-ttu-id="0bc04-121">**Log4J v2.0**</span><span class="sxs-lookup"><span data-stu-id="0bc04-121">**Log4J v2.0**</span></span>

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j2', version: '1.0.+'
```

<span data-ttu-id="0bc04-122">**Log4J versie 1.2**</span><span class="sxs-lookup"><span data-stu-id="0bc04-122">**Log4J v1.2**</span></span>

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j1_2', version: '1.0.+'
```

#### <a name="otherwise-"></a><span data-ttu-id="0bc04-123">Of...</span><span class="sxs-lookup"><span data-stu-id="0bc04-123">Otherwise ...</span></span>
<span data-ttu-id="0bc04-124">Downloaden en uitpakken van de juiste appender Hallo Hallo juiste bibliotheek tooyour project toevoegen:</span><span class="sxs-lookup"><span data-stu-id="0bc04-124">Download and extract hello appropriate appender, then add hello appropriate library tooyour project:</span></span>

| <span data-ttu-id="0bc04-125">Logboek</span><span class="sxs-lookup"><span data-stu-id="0bc04-125">Logger</span></span> | <span data-ttu-id="0bc04-126">Downloaden</span><span class="sxs-lookup"><span data-stu-id="0bc04-126">Download</span></span> | <span data-ttu-id="0bc04-127">Bibliotheek</span><span class="sxs-lookup"><span data-stu-id="0bc04-127">Library</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0bc04-128">Logback</span><span class="sxs-lookup"><span data-stu-id="0bc04-128">Logback</span></span> |[<span data-ttu-id="0bc04-129">SDK met Logback appender</span><span class="sxs-lookup"><span data-stu-id="0bc04-129">SDK with Logback appender</span></span>](https://aka.ms/xt62a4) |<span data-ttu-id="0bc04-130">applicationinsights-logboekregistratie-logback</span><span class="sxs-lookup"><span data-stu-id="0bc04-130">applicationinsights-logging-logback</span></span> |
| <span data-ttu-id="0bc04-131">Log4J v2.0</span><span class="sxs-lookup"><span data-stu-id="0bc04-131">Log4J v2.0</span></span> |[<span data-ttu-id="0bc04-132">SDK met Log4J v2 appender</span><span class="sxs-lookup"><span data-stu-id="0bc04-132">SDK with Log4J v2 appender</span></span>](https://aka.ms/qypznq) |<span data-ttu-id="0bc04-133">applicationinsights-logboekregistratie-log4j2</span><span class="sxs-lookup"><span data-stu-id="0bc04-133">applicationinsights-logging-log4j2</span></span> |
| <span data-ttu-id="0bc04-134">Log4j versie 1.2</span><span class="sxs-lookup"><span data-stu-id="0bc04-134">Log4j v1.2</span></span> |[<span data-ttu-id="0bc04-135">SDK met Log4J versie 1.2 appender</span><span class="sxs-lookup"><span data-stu-id="0bc04-135">SDK with Log4J v1.2 appender</span></span>](https://aka.ms/ky9cbo) |<span data-ttu-id="0bc04-136">applicationinsights-logboekregistratie-log4j1_2</span><span class="sxs-lookup"><span data-stu-id="0bc04-136">applicationinsights-logging-log4j1_2</span></span> |

## <a name="add-hello-appender-tooyour-logging-framework"></a><span data-ttu-id="0bc04-137">Hallo appender tooyour logboekregistratie framework toevoegen</span><span class="sxs-lookup"><span data-stu-id="0bc04-137">Add hello appender tooyour logging framework</span></span>
<span data-ttu-id="0bc04-138">toostart aan traceringen, samenvoegen Hallo relevante codefragment code toohello Log4J of Logback-configuratiebestand:</span><span class="sxs-lookup"><span data-stu-id="0bc04-138">toostart getting traces, merge hello relevant snippet of code toohello Log4J or Logback configuration file:</span></span> 

<span data-ttu-id="0bc04-139">*Logback*</span><span class="sxs-lookup"><span data-stu-id="0bc04-139">*Logback*</span></span>

```XML

    <appender name="aiAppender" 
      class="com.microsoft.applicationinsights.logback.ApplicationInsightsAppender">
    </appender>
    <root level="trace">
      <appender-ref ref="aiAppender" />
    </root>
```

<span data-ttu-id="0bc04-140">*Log4J v2.0*</span><span class="sxs-lookup"><span data-stu-id="0bc04-140">*Log4J v2.0*</span></span>

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

<span data-ttu-id="0bc04-141">*Log4J versie 1.2*</span><span class="sxs-lookup"><span data-stu-id="0bc04-141">*Log4J v1.2*</span></span>

```XML

    <appender name="aiAppender" 
         class="com.microsoft.applicationinsights.log4j.v1_2.ApplicationInsightsAppender">
    </appender>
    <root>
      <priority value ="trace" />
      <appender-ref ref="aiAppender" />
    </root>
```

<span data-ttu-id="0bc04-142">Hallo Application Insights appenders kunnen alleen worden verwezen door een geconfigureerde berichtenlogboek en niet per se Hallo hoofdmap berichtenlogboek (zoals weergegeven in de codevoorbeelden Hallo hierboven).</span><span class="sxs-lookup"><span data-stu-id="0bc04-142">hello Application Insights appenders can be referenced by any configured logger, and not necessarily by hello root logger (as shown in hello code samples above).</span></span>

## <a name="explore-your-traces-in-hello-application-insights-portal"></a><span data-ttu-id="0bc04-143">Bekijk de traceringen in Hallo Application Insights-portal</span><span class="sxs-lookup"><span data-stu-id="0bc04-143">Explore your traces in hello Application Insights portal</span></span>
<span data-ttu-id="0bc04-144">Nu dat u hebt geconfigureerd uw project toosend tooApplication Insights traceert, kunt u bekijken en zoeken naar deze traceringen in Hallo Application Insights-portal in Hallo [Search] [ diagnostic] blade.</span><span class="sxs-lookup"><span data-stu-id="0bc04-144">Now that you've configured your project toosend traces tooApplication Insights, you can view and search these traces in hello Application Insights portal, in hello [Search][diagnostic] blade.</span></span>

![Open in Hallo Application Insights-portal zoeken](./media/app-insights-java-trace-logs/10-diagnostics.png)

## <a name="next-steps"></a><span data-ttu-id="0bc04-146">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0bc04-146">Next steps</span></span>
<span data-ttu-id="0bc04-147">[Diagnostische gegevens doorzoeken][diagnostic]</span><span class="sxs-lookup"><span data-stu-id="0bc04-147">[Diagnostic search][diagnostic]</span></span>

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md


