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
# <a name="collectd-linux-performance-metrics-in-application-insights"></a><span data-ttu-id="b5768-103">collectd: Linux maatstaven voor prestaties in Application Insights</span><span class="sxs-lookup"><span data-stu-id="b5768-103">collectd: Linux performance metrics in Application Insights</span></span>


<span data-ttu-id="b5768-104">tooexplore systeemprestaties van Linux in [Application Insights](app-insights-overview.md), installeren [collectd](http://collectd.org/), samen met de Application Insights-invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="b5768-104">tooexplore Linux system performance metrics in [Application Insights](app-insights-overview.md), install [collectd](http://collectd.org/), together with its Application Insights plug-in.</span></span> <span data-ttu-id="b5768-105">Deze oplossing open source worden verschillende statistieken voor systeem- en netwerkgegevens verzameld.</span><span class="sxs-lookup"><span data-stu-id="b5768-105">This open-source solution gathers various system and network statistics.</span></span>

<span data-ttu-id="b5768-106">Doorgaans kunt u collectd als u al hebt [uw Java-webservice met Application Insights geïnstrumenteerd][java].</span><span class="sxs-lookup"><span data-stu-id="b5768-106">Typically you'll use collectd if you have already [instrumented your Java web service with Application Insights][java].</span></span> <span data-ttu-id="b5768-107">Dit biedt u meer gegevens toohelp tooenhance u de prestaties van uw app of het analyseren van problemen.</span><span class="sxs-lookup"><span data-stu-id="b5768-107">It gives you more data toohelp you tooenhance your app's performance or diagnose problems.</span></span> 

![voorbeeldgrafieken](./media/app-insights-java-collectd/sample.png)

## <a name="get-your-instrumentation-key"></a><span data-ttu-id="b5768-109">De instrumentatiesleutel ophalen</span><span class="sxs-lookup"><span data-stu-id="b5768-109">Get your instrumentation key</span></span>
<span data-ttu-id="b5768-110">In Hallo [Microsoft Azure-portal](https://portal.azure.com)Open Hallo [Application Insights](app-insights-overview.md) resource waar u Hallo gegevens tooappear.</span><span class="sxs-lookup"><span data-stu-id="b5768-110">In hello [Microsoft Azure portal](https://portal.azure.com), open hello [Application Insights](app-insights-overview.md) resource where you want hello data tooappear.</span></span> <span data-ttu-id="b5768-111">(Of [Maak een nieuwe resource](app-insights-create-new-resource.md).)</span><span class="sxs-lookup"><span data-stu-id="b5768-111">(Or [create a new resource](app-insights-create-new-resource.md).)</span></span>

<span data-ttu-id="b5768-112">Een kopie van de instrumentatiesleutel hello, waarmee Hallo resource in beslag nemen.</span><span class="sxs-lookup"><span data-stu-id="b5768-112">Take a copy of hello instrumentation key, which identifies hello resource.</span></span>

![Alles bekijken, opent u de resource en vervolgens in Hallo Essentials vervolgkeuzelijst, selecteer en kopieer Hallo Instrumentatiesleutel](./media/app-insights-java-collectd/02-props.png)

## <a name="install-collectd-and-hello-plug-in"></a><span data-ttu-id="b5768-114">Installeer collectd en Hallo invoegtoepassing</span><span class="sxs-lookup"><span data-stu-id="b5768-114">Install collectd and hello plug-in</span></span>
<span data-ttu-id="b5768-115">Op de Linux-servers:</span><span class="sxs-lookup"><span data-stu-id="b5768-115">On your Linux server machines:</span></span>

1. <span data-ttu-id="b5768-116">Installeer [collectd](http://collectd.org/) versie 5.4.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="b5768-116">Install [collectd](http://collectd.org/) version 5.4.0 or later.</span></span>
2. <span data-ttu-id="b5768-117">Hallo downloaden [Application Insights-invoegtoepassing voor collectd writer](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="b5768-117">Download hello [Application Insights collectd writer plugin](https://aka.ms/aijavasdk).</span></span> <span data-ttu-id="b5768-118">Houd er rekening mee Hallo versienummer.</span><span class="sxs-lookup"><span data-stu-id="b5768-118">Note hello version number.</span></span>
3. <span data-ttu-id="b5768-119">Hallo-invoegtoepassing JAR kopiëren naar `/usr/share/collectd/java`.</span><span class="sxs-lookup"><span data-stu-id="b5768-119">Copy hello plugin JAR into `/usr/share/collectd/java`.</span></span>
4. <span data-ttu-id="b5768-120">Bewerken `/etc/collectd/collectd.conf`:</span><span class="sxs-lookup"><span data-stu-id="b5768-120">Edit `/etc/collectd/collectd.conf`:</span></span>
   * <span data-ttu-id="b5768-121">Zorg ervoor dat [Hallo Java-invoegtoepassing](https://collectd.org/wiki/index.php/Plugin:Java) is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="b5768-121">Ensure that [hello Java plugin](https://collectd.org/wiki/index.php/Plugin:Java) is enabled.</span></span>
   * <span data-ttu-id="b5768-122">Update hello JVMArg voor Hallo java.class.path tooinclude Hallo JAR te volgen.</span><span class="sxs-lookup"><span data-stu-id="b5768-122">Update hello JVMArg for hello java.class.path tooinclude hello following JAR.</span></span> <span data-ttu-id="b5768-123">Hallo versie nummer toomatch Hallo die één gedownloade bijwerken:</span><span class="sxs-lookup"><span data-stu-id="b5768-123">Update hello version number toomatch hello one you downloaded:</span></span>
   * `/usr/share/collectd/java/applicationinsights-collectd-1.0.5.jar`
   * <span data-ttu-id="b5768-124">In dit fragment, met behulp van Hallo Instrumentatiesleutel van uw resource toevoegen:</span><span class="sxs-lookup"><span data-stu-id="b5768-124">Add this snippet, using hello Instrumentation Key from your resource:</span></span>

```XML

     LoadPlugin "com.microsoft.applicationinsights.collectd.ApplicationInsightsWriter"
     <Plugin ApplicationInsightsWriter>
        InstrumentationKey "Your key"
     </Plugin>
```

<span data-ttu-id="b5768-125">Dit is onderdeel van een voorbeeldconfiguratiebestand:</span><span class="sxs-lookup"><span data-stu-id="b5768-125">Here's part of a sample configuration file:</span></span>

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

<span data-ttu-id="b5768-126">Configureer andere [collectd plugins](https://collectd.org/wiki/index.php/Table_of_Plugins), dat kan verschillende gegevens verzamelen van verschillende gegevensbronnen.</span><span class="sxs-lookup"><span data-stu-id="b5768-126">Configure other [collectd plugins](https://collectd.org/wiki/index.php/Table_of_Plugins), which can collect various data from different sources.</span></span>

<span data-ttu-id="b5768-127">Start opnieuw op op basis van tooits collectd [handmatige](https://collectd.org/wiki/index.php/First_steps).</span><span class="sxs-lookup"><span data-stu-id="b5768-127">Restart collectd according tooits [manual](https://collectd.org/wiki/index.php/First_steps).</span></span>

## <a name="view-hello-data-in-application-insights"></a><span data-ttu-id="b5768-128">Hallo-gegevens weergeven in Application Insights</span><span class="sxs-lookup"><span data-stu-id="b5768-128">View hello data in Application Insights</span></span>
<span data-ttu-id="b5768-129">Open in uw Application Insights-resource [Metrics Explorer en grafieken toe te voegen][metrics], selecteren Hallo metrische gegevens wilt toosee van Hallo aangepaste categorie.</span><span class="sxs-lookup"><span data-stu-id="b5768-129">In your Application Insights resource, open [Metrics Explorer and add charts][metrics], selecting hello metrics you want toosee from hello Custom category.</span></span>

![](./media/app-insights-java-collectd/result.png)

<span data-ttu-id="b5768-130">Standaard worden Hallo metrische gegevens geaggregeerd alle host machines waaruit de Hallo metrische gegevens zijn verzameld.</span><span class="sxs-lookup"><span data-stu-id="b5768-130">By default, hello metrics are aggregated across all host machines from which hello metrics were collected.</span></span> <span data-ttu-id="b5768-131">tooview hello metrische gegevens per host Hallo grafiek details blade, schakelt u Grouping en kies vervolgens toogroup door CollectD-Host.</span><span class="sxs-lookup"><span data-stu-id="b5768-131">tooview hello metrics per host, in hello Chart details blade, turn on Grouping and then choose toogroup by CollectD-Host.</span></span>

## <a name="tooexclude-upload-of-specific-statistics"></a><span data-ttu-id="b5768-132">uploaden van specifieke statistieken tooexclude</span><span class="sxs-lookup"><span data-stu-id="b5768-132">tooexclude upload of specific statistics</span></span>
<span data-ttu-id="b5768-133">Hallo Application Insights-invoegtoepassing verzendt standaard alle Hallo gegevens verzameld door alle Hallo ingeschakeld collectd 'read' invoegtoepassingen gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b5768-133">By default, hello Application Insights plugin sends all hello data collected by all hello enabled collectd 'read' plugins.</span></span> 

<span data-ttu-id="b5768-134">tooexclude gegevens van specifieke invoegtoepassingen of gegevensbronnen:</span><span class="sxs-lookup"><span data-stu-id="b5768-134">tooexclude data from specific plugins or data sources:</span></span>

* <span data-ttu-id="b5768-135">Hallo-configuratiebestand bewerken.</span><span class="sxs-lookup"><span data-stu-id="b5768-135">Edit hello configuration file.</span></span> 
* <span data-ttu-id="b5768-136">In `<Plugin ApplicationInsightsWriter>`, richtlijn regels als volgt toevoegen:</span><span class="sxs-lookup"><span data-stu-id="b5768-136">In `<Plugin ApplicationInsightsWriter>`, add directive lines like this:</span></span>

| <span data-ttu-id="b5768-137">Richtlijn</span><span class="sxs-lookup"><span data-stu-id="b5768-137">Directive</span></span> | <span data-ttu-id="b5768-138">Effect</span><span class="sxs-lookup"><span data-stu-id="b5768-138">Effect</span></span> |
| --- | --- |
| `Exclude disk` |<span data-ttu-id="b5768-139">Alle gegevens die worden verzameld door Hallo uitsluiten `disk` invoegtoepassing</span><span class="sxs-lookup"><span data-stu-id="b5768-139">Exclude all data collected by hello `disk` plugin</span></span> |
| `Exclude disk:read,write` |<span data-ttu-id="b5768-140">Hallo-bronnen met de naam uitsluiten `read` en `write` van Hallo `disk` invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="b5768-140">Exclude hello sources named `read` and `write` from hello `disk` plugin.</span></span> |

<span data-ttu-id="b5768-141">Afzonderlijke richtlijnen met een nieuwe regel.</span><span class="sxs-lookup"><span data-stu-id="b5768-141">Separate directives with a newline.</span></span>

## <a name="problems"></a><span data-ttu-id="b5768-142">Problemen?</span><span class="sxs-lookup"><span data-stu-id="b5768-142">Problems?</span></span>
<span data-ttu-id="b5768-143">*Gegevens in de portal Hallo weergegeven niet*</span><span class="sxs-lookup"><span data-stu-id="b5768-143">*I don't see data in hello portal*</span></span>

* <span data-ttu-id="b5768-144">Open [Search] [ diagnostic] toosee als Hallo onbewerkte gebeurtenissen zijn ontvangen.</span><span class="sxs-lookup"><span data-stu-id="b5768-144">Open [Search][diagnostic] toosee if hello raw events have arrived.</span></span> <span data-ttu-id="b5768-145">Soms worden ze langer tooappear in metrics explorer.</span><span class="sxs-lookup"><span data-stu-id="b5768-145">Sometimes they take longer tooappear in metrics explorer.</span></span>
* <span data-ttu-id="b5768-146">U moet mogelijk te[firewalluitzonderingen voor uitgaande gegevens instellen](app-insights-ip-addresses.md)</span><span class="sxs-lookup"><span data-stu-id="b5768-146">You might need too[set firewall exceptions for outgoing data](app-insights-ip-addresses.md)</span></span>
* <span data-ttu-id="b5768-147">Tracering in Application Insights-invoegtoepassing Hallo inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b5768-147">Enable tracing in hello Application Insights plugin.</span></span> <span data-ttu-id="b5768-148">Deze regel in te voegen `<Plugin ApplicationInsightsWriter>`:</span><span class="sxs-lookup"><span data-stu-id="b5768-148">Add this line within `<Plugin ApplicationInsightsWriter>`:</span></span>
  * `SDKLogger true`
* <span data-ttu-id="b5768-149">Open een terminal en collectd starten in de uitgebreide modus toosee meldt problemen:</span><span class="sxs-lookup"><span data-stu-id="b5768-149">Open a terminal and start collectd in verbose mode, toosee any issues it is reporting:</span></span>
  * `sudo collectd -f`

## <a name="known-issue"></a><span data-ttu-id="b5768-150">Bekende problemen</span><span class="sxs-lookup"><span data-stu-id="b5768-150">Known issue</span></span>

<span data-ttu-id="b5768-151">Hallo schrijven van Application Insights-invoegtoepassing is niet compatibel met bepaalde invoegtoepassingen lezen.</span><span class="sxs-lookup"><span data-stu-id="b5768-151">hello Application Insights Write plugin is incompatible with certain Read plugins.</span></span> <span data-ttu-id="b5768-152">Sommige invoegtoepassingen verzenden soms 'NaN', waarbij Hallo Application Insights-invoegtoepassing een getal met drijvende komma verwacht.</span><span class="sxs-lookup"><span data-stu-id="b5768-152">Some plugins sometimes send "NaN" where hello Application Insights plugin expects a floating-point number.</span></span>

<span data-ttu-id="b5768-153">Symptoom: Hallo collectd logboek bevat fouten die zijn 'AI:... SyntaxError: onverwacht token N ".</span><span class="sxs-lookup"><span data-stu-id="b5768-153">Symptom: hello collectd log shows errors that include "AI: ... SyntaxError: Unexpected token N".</span></span>

<span data-ttu-id="b5768-154">Tijdelijke oplossing: Uitsluiten door Hallo probleem schrijven plugins verzamelde gegevens.</span><span class="sxs-lookup"><span data-stu-id="b5768-154">Workaround: Exclude data collected by hello problem Write plugins.</span></span> 

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md


