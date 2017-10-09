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
# <a name="monitor-dependencies-exceptions-and-execution-times-in-java-web-apps"></a><span data-ttu-id="e3067-103">Afhankelijkheden, uitzonderingen en uitvoeringstijden in Java-web-apps bewaken</span><span class="sxs-lookup"><span data-stu-id="e3067-103">Monitor dependencies, exceptions and execution times in Java web apps</span></span>


<span data-ttu-id="e3067-104">Als u hebt [uw Java-web-app met Application Insights geïnstrumenteerd][java], kunt u Hallo Java-Agent tooget beter inzicht, zonder codewijzigingen:</span><span class="sxs-lookup"><span data-stu-id="e3067-104">If you have [instrumented your Java web app with Application Insights][java], you can use hello Java Agent tooget deeper insights, without any code changes:</span></span>

* <span data-ttu-id="e3067-105">**Afhankelijkheden:** gegevens over aanroepen die uw toepassing tooother onderdelen maakt, waaronder:</span><span class="sxs-lookup"><span data-stu-id="e3067-105">**Dependencies:** Data about calls that your application makes tooother components, including:</span></span>
  * <span data-ttu-id="e3067-106">**REST-aanroepen** gedaan via HttpClient OkHttp en RestTemplate (bron).</span><span class="sxs-lookup"><span data-stu-id="e3067-106">**REST calls** made via HttpClient, OkHttp, and RestTemplate (Spring).</span></span>
  * <span data-ttu-id="e3067-107">**Redis** aanroepen via Hallo Jedis client.</span><span class="sxs-lookup"><span data-stu-id="e3067-107">**Redis** calls made via hello Jedis client.</span></span> <span data-ttu-id="e3067-108">Als Hallo aanroep langer dan per 10 duurt, haalt Hallo agent ook Hallo aanroepargumenten.</span><span class="sxs-lookup"><span data-stu-id="e3067-108">If hello call takes longer than 10s, hello agent also fetches hello call arguments.</span></span>
  * <span data-ttu-id="e3067-109">**[JDBC aanroepen](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)**  -MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB of Apache Derby DB.</span><span class="sxs-lookup"><span data-stu-id="e3067-109">**[JDBC calls](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)** - MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB or Apache Derby DB.</span></span> <span data-ttu-id="e3067-110">aanroepen van 'executeBatch' worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="e3067-110">"executeBatch" calls are supported.</span></span> <span data-ttu-id="e3067-111">Als Hallo aanroep langer dan per 10 duurt, rapporteert Hallo-agent voor MySQL en PostgreSQL Hallo queryplan.</span><span class="sxs-lookup"><span data-stu-id="e3067-111">For MySQL and PostgreSQL, if hello call takes longer than 10s, hello agent reports hello query plan.</span></span>
* <span data-ttu-id="e3067-112">**Uitzonderingen wordt onderschept:** gegevens over uitzonderingen die worden verwerkt door uw code.</span><span class="sxs-lookup"><span data-stu-id="e3067-112">**Caught exceptions:** Data about exceptions that are handled by your code.</span></span>
* <span data-ttu-id="e3067-113">**Uitvoeringstijd voor methode:** gegevens over Hallo keer dat er vergt tooexecute specifieke methoden.</span><span class="sxs-lookup"><span data-stu-id="e3067-113">**Method execution time:** Data about hello time it takes tooexecute specific methods.</span></span>

<span data-ttu-id="e3067-114">toouse hello Java-agent, u deze installeren op uw server.</span><span class="sxs-lookup"><span data-stu-id="e3067-114">toouse hello Java agent, you install it on your server.</span></span> <span data-ttu-id="e3067-115">Uw web-apps moeten zijn uitgerust met Hallo [Application Insights-SDK voor Java][java].</span><span class="sxs-lookup"><span data-stu-id="e3067-115">Your web apps must be instrumented with hello [Application Insights Java SDK][java].</span></span> 

## <a name="install-hello-application-insights-agent-for-java"></a><span data-ttu-id="e3067-116">Hallo Application Insights-agent voor Java installeren</span><span class="sxs-lookup"><span data-stu-id="e3067-116">Install hello Application Insights agent for Java</span></span>
1. <span data-ttu-id="e3067-117">Uitgevoerd uw Java-server op Hallo machine [Hallo-agent downloaden](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="e3067-117">On hello machine running your Java server, [download hello agent](https://aka.ms/aijavasdk).</span></span>
2. <span data-ttu-id="e3067-118">Hallo application server opstartscript bewerken en volgende JVM Hallo toevoegen:</span><span class="sxs-lookup"><span data-stu-id="e3067-118">Edit hello application server startup script, and add hello following JVM:</span></span>
   
    <span data-ttu-id="e3067-119">`javaagent:`*volledig pad toohello agent JAR-bestand*</span><span class="sxs-lookup"><span data-stu-id="e3067-119">`javaagent:`*full path toohello agent JAR file*</span></span>
   
    <span data-ttu-id="e3067-120">Bijvoorbeeld in Tomcat op een Linux-machine:</span><span class="sxs-lookup"><span data-stu-id="e3067-120">For example, in Tomcat on a Linux machine:</span></span>
   
    `export JAVA_OPTS="$JAVA_OPTS -javaagent:<full path tooagent JAR file>"`
3. <span data-ttu-id="e3067-121">Start de toepassingsserver van uw opnieuw.</span><span class="sxs-lookup"><span data-stu-id="e3067-121">Restart your application server.</span></span>

## <a name="configure-hello-agent"></a><span data-ttu-id="e3067-122">Hallo-agent configureren</span><span class="sxs-lookup"><span data-stu-id="e3067-122">Configure hello agent</span></span>
<span data-ttu-id="e3067-123">Maak een bestand met de naam `AI-Agent.xml` en plaats deze in Hallo dezelfde map als Hallo agent JAR-bestand.</span><span class="sxs-lookup"><span data-stu-id="e3067-123">Create a file named `AI-Agent.xml` and place it in hello same folder as hello agent JAR file.</span></span>

<span data-ttu-id="e3067-124">Hallo-inhoud van xml-bestand Hallo ingesteld.</span><span class="sxs-lookup"><span data-stu-id="e3067-124">Set hello content of hello xml file.</span></span> <span data-ttu-id="e3067-125">Hallo na voorbeeld tooinclude bewerken of Hallo-functies die u wilt weglaten.</span><span class="sxs-lookup"><span data-stu-id="e3067-125">Edit hello following example tooinclude or omit hello features you want.</span></span>

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

<span data-ttu-id="e3067-126">U hebt tooenable rapporten uitzondering en timing van de methode voor afzonderlijke methoden.</span><span class="sxs-lookup"><span data-stu-id="e3067-126">You have tooenable reports exception and method timing for individual methods.</span></span>

<span data-ttu-id="e3067-127">Standaard `reportExecutionTime` is ingesteld op true en `reportCaughtExceptions` is ingesteld op false.</span><span class="sxs-lookup"><span data-stu-id="e3067-127">By default, `reportExecutionTime` is true and `reportCaughtExceptions` is false.</span></span>

## <a name="view-hello-data"></a><span data-ttu-id="e3067-128">Hallo-gegevens weergeven</span><span class="sxs-lookup"><span data-stu-id="e3067-128">View hello data</span></span>
<span data-ttu-id="e3067-129">In Application Insights-resource hello, geaggregeerde externe afhankelijkheid en methode uitvoeringstijden weergegeven [onder Hallo prestaties tegel][metrics].</span><span class="sxs-lookup"><span data-stu-id="e3067-129">In hello Application Insights resource, aggregated remote dependency and method execution times appears [under hello Performance tile][metrics].</span></span>

<span data-ttu-id="e3067-130">toosearch voor afzonderlijke exemplaren van afhankelijkheid en uitzondering methode rapporten openen [Search][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="e3067-130">toosearch for individual instances of dependency, exception, and method reports, open [Search][diagnostic].</span></span>

<span data-ttu-id="e3067-131">[Diagnose afhankelijkheidsproblemen - meer](app-insights-asp-net-dependencies.md#diagnosis).</span><span class="sxs-lookup"><span data-stu-id="e3067-131">[Diagnosing dependency issues - learn more](app-insights-asp-net-dependencies.md#diagnosis).</span></span>

## <a name="questions-problems"></a><span data-ttu-id="e3067-132">Vragen?</span><span class="sxs-lookup"><span data-stu-id="e3067-132">Questions?</span></span> <span data-ttu-id="e3067-133">Problemen?</span><span class="sxs-lookup"><span data-stu-id="e3067-133">Problems?</span></span>
* <span data-ttu-id="e3067-134">Zijn er geen gegevens?</span><span class="sxs-lookup"><span data-stu-id="e3067-134">No data?</span></span> [<span data-ttu-id="e3067-135">Set firewall-uitzonderingen</span><span class="sxs-lookup"><span data-stu-id="e3067-135">Set firewall exceptions</span></span>](app-insights-ip-addresses.md)
* [<span data-ttu-id="e3067-136">Problemen met Java oplossen</span><span class="sxs-lookup"><span data-stu-id="e3067-136">Troubleshooting Java</span></span>](app-insights-java-troubleshoot.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
