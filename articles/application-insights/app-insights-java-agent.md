---
title: Prestatiebewaking voor Java-web-apps in Azure Application Insights | Microsoft Docs
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
ms.openlocfilehash: 4e56998382610ad3d7224e6a8de5aee5419ebe43
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-dependencies-exceptions-and-execution-times-in-java-web-apps"></a><span data-ttu-id="4cd74-103">Afhankelijkheden, uitzonderingen en uitvoeringstijden in Java-web-apps bewaken</span><span class="sxs-lookup"><span data-stu-id="4cd74-103">Monitor dependencies, exceptions and execution times in Java web apps</span></span>


<span data-ttu-id="4cd74-104">Als u hebt [uw Java-web-app met Application Insights geïnstrumenteerd][java], kunt u de Java-Agent voor dieper inzicht, zonder codewijzigingen:</span><span class="sxs-lookup"><span data-stu-id="4cd74-104">If you have [instrumented your Java web app with Application Insights][java], you can use the Java Agent to get deeper insights, without any code changes:</span></span>

* <span data-ttu-id="4cd74-105">**Afhankelijkheden:** gegevens over aanroepen waarmee uw toepassing op andere onderdelen, met inbegrip van:</span><span class="sxs-lookup"><span data-stu-id="4cd74-105">**Dependencies:** Data about calls that your application makes to other components, including:</span></span>
  * <span data-ttu-id="4cd74-106">**REST-aanroepen** gedaan via HttpClient OkHttp en RestTemplate (bron).</span><span class="sxs-lookup"><span data-stu-id="4cd74-106">**REST calls** made via HttpClient, OkHttp, and RestTemplate (Spring).</span></span>
  * <span data-ttu-id="4cd74-107">**Redis** aanroepen via de client-Jedis.</span><span class="sxs-lookup"><span data-stu-id="4cd74-107">**Redis** calls made via the Jedis client.</span></span> <span data-ttu-id="4cd74-108">Als de oproep langer dan per 10 duurt, haalt de agent ook de van aanroepargumenten.</span><span class="sxs-lookup"><span data-stu-id="4cd74-108">If the call takes longer than 10s, the agent also fetches the call arguments.</span></span>
  * <span data-ttu-id="4cd74-109">**[JDBC aanroepen](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)**  -MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB of Apache Derby DB.</span><span class="sxs-lookup"><span data-stu-id="4cd74-109">**[JDBC calls](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)** - MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB or Apache Derby DB.</span></span> <span data-ttu-id="4cd74-110">aanroepen van 'executeBatch' worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="4cd74-110">"executeBatch" calls are supported.</span></span> <span data-ttu-id="4cd74-111">Als de oproep langer dan per 10 duurt, rapporteert de agent voor MySQL en PostgreSQL het queryplan.</span><span class="sxs-lookup"><span data-stu-id="4cd74-111">For MySQL and PostgreSQL, if the call takes longer than 10s, the agent reports the query plan.</span></span>
* <span data-ttu-id="4cd74-112">**Uitzonderingen wordt onderschept:** gegevens over uitzonderingen die worden verwerkt door uw code.</span><span class="sxs-lookup"><span data-stu-id="4cd74-112">**Caught exceptions:** Data about exceptions that are handled by your code.</span></span>
* <span data-ttu-id="4cd74-113">**Uitvoeringstijd voor methode:** gegevens over de tijd die nodig zijn bepaalde methoden uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="4cd74-113">**Method execution time:** Data about the time it takes to execute specific methods.</span></span>

<span data-ttu-id="4cd74-114">Voor het gebruik van de Java-agent moet installeren u deze op uw server.</span><span class="sxs-lookup"><span data-stu-id="4cd74-114">To use the Java agent, you install it on your server.</span></span> <span data-ttu-id="4cd74-115">Uw web-apps moeten zijn uitgerust met de [Application Insights-SDK voor Java][java].</span><span class="sxs-lookup"><span data-stu-id="4cd74-115">Your web apps must be instrumented with the [Application Insights Java SDK][java].</span></span> 

## <a name="install-the-application-insights-agent-for-java"></a><span data-ttu-id="4cd74-116">Installeer de Application Insights-agent voor Java</span><span class="sxs-lookup"><span data-stu-id="4cd74-116">Install the Application Insights agent for Java</span></span>
1. <span data-ttu-id="4cd74-117">Op de computer waarop u uw server Java [de agent downloaden](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="4cd74-117">On the machine running your Java server, [download the agent](https://aka.ms/aijavasdk).</span></span>
2. <span data-ttu-id="4cd74-118">Het opstartscript van application server bewerken en de volgende JVM toevoegen:</span><span class="sxs-lookup"><span data-stu-id="4cd74-118">Edit the application server startup script, and add the following JVM:</span></span>
   
    <span data-ttu-id="4cd74-119">`javaagent:`*volledig pad naar het JAR-bestand van agent*</span><span class="sxs-lookup"><span data-stu-id="4cd74-119">`javaagent:`*full path to the agent JAR file*</span></span>
   
    <span data-ttu-id="4cd74-120">Bijvoorbeeld in Tomcat op een Linux-machine:</span><span class="sxs-lookup"><span data-stu-id="4cd74-120">For example, in Tomcat on a Linux machine:</span></span>
   
    `export JAVA_OPTS="$JAVA_OPTS -javaagent:<full path to agent JAR file>"`
3. <span data-ttu-id="4cd74-121">Start de toepassingsserver van uw opnieuw.</span><span class="sxs-lookup"><span data-stu-id="4cd74-121">Restart your application server.</span></span>

## <a name="configure-the-agent"></a><span data-ttu-id="4cd74-122">De agent configureren</span><span class="sxs-lookup"><span data-stu-id="4cd74-122">Configure the agent</span></span>
<span data-ttu-id="4cd74-123">Maak een bestand met de naam `AI-Agent.xml` en plaats deze in dezelfde map als de agent JAR-bestand.</span><span class="sxs-lookup"><span data-stu-id="4cd74-123">Create a file named `AI-Agent.xml` and place it in the same folder as the agent JAR file.</span></span>

<span data-ttu-id="4cd74-124">Stel de inhoud van het xml-bestand.</span><span class="sxs-lookup"><span data-stu-id="4cd74-124">Set the content of the xml file.</span></span> <span data-ttu-id="4cd74-125">Het volgende voorbeeld als u wilt opnemen in of uitsluiten van de functies die u wilt bewerken.</span><span class="sxs-lookup"><span data-stu-id="4cd74-125">Edit the following example to include or omit the features you want.</span></span>

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

           <!-- Report on the particular signature
                void methodTwo(String, int) -->
           <Method name="methodTwo"
              reportExecutionTime="true"
              signature="(Ljava/lang/String;I)V" />
        </Class>

      </Instrumentation>
    </ApplicationInsightsAgent>

```

<span data-ttu-id="4cd74-126">U moet rapporten uitzondering en timing van de methode voor afzonderlijke methoden inschakelen.</span><span class="sxs-lookup"><span data-stu-id="4cd74-126">You have to enable reports exception and method timing for individual methods.</span></span>

<span data-ttu-id="4cd74-127">Standaard `reportExecutionTime` is ingesteld op true en `reportCaughtExceptions` is ingesteld op false.</span><span class="sxs-lookup"><span data-stu-id="4cd74-127">By default, `reportExecutionTime` is true and `reportCaughtExceptions` is false.</span></span>

## <a name="view-the-data"></a><span data-ttu-id="4cd74-128">De gegevens weergeven</span><span class="sxs-lookup"><span data-stu-id="4cd74-128">View the data</span></span>
<span data-ttu-id="4cd74-129">In de Application Insights-resource geaggregeerde externe afhankelijkheid en methode uitvoeringstijden weergegeven [onder de tegel prestaties][metrics].</span><span class="sxs-lookup"><span data-stu-id="4cd74-129">In the Application Insights resource, aggregated remote dependency and method execution times appears [under the Performance tile][metrics].</span></span>

<span data-ttu-id="4cd74-130">Als u wilt zoeken naar afzonderlijke exemplaren van afhankelijkheid en uitzondering methode rapporten, open [Search][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="4cd74-130">To search for individual instances of dependency, exception, and method reports, open [Search][diagnostic].</span></span>

<span data-ttu-id="4cd74-131">[Diagnose afhankelijkheidsproblemen - meer](app-insights-asp-net-dependencies.md#diagnosis).</span><span class="sxs-lookup"><span data-stu-id="4cd74-131">[Diagnosing dependency issues - learn more](app-insights-asp-net-dependencies.md#diagnosis).</span></span>

## <a name="questions-problems"></a><span data-ttu-id="4cd74-132">Vragen?</span><span class="sxs-lookup"><span data-stu-id="4cd74-132">Questions?</span></span> <span data-ttu-id="4cd74-133">Problemen?</span><span class="sxs-lookup"><span data-stu-id="4cd74-133">Problems?</span></span>
* <span data-ttu-id="4cd74-134">Zijn er geen gegevens?</span><span class="sxs-lookup"><span data-stu-id="4cd74-134">No data?</span></span> [<span data-ttu-id="4cd74-135">Set firewall-uitzonderingen</span><span class="sxs-lookup"><span data-stu-id="4cd74-135">Set firewall exceptions</span></span>](app-insights-ip-addresses.md)
* [<span data-ttu-id="4cd74-136">Problemen met Java oplossen</span><span class="sxs-lookup"><span data-stu-id="4cd74-136">Troubleshooting Java</span></span>](app-insights-java-troubleshoot.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
