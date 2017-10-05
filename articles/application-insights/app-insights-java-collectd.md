---
title: Java-web-appprestaties op Linux - Azure controleren | Microsoft Docs
description: Uitgebreide bewaking van toepassingsprestaties van uw Java-website met de invoegtoepassing CollectD voor Application Insights.
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
ms.openlocfilehash: 4ea917b068e0242bfb88d7357eca032607a43a3f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="collectd-linux-performance-metrics-in-application-insights"></a><span data-ttu-id="c9fbd-103">collectd: Linux maatstaven voor prestaties in Application Insights</span><span class="sxs-lookup"><span data-stu-id="c9fbd-103">collectd: Linux performance metrics in Application Insights</span></span>


<span data-ttu-id="c9fbd-104">Om te verkennen systeemprestaties in Linux [Application Insights](app-insights-overview.md), installeren [collectd](http://collectd.org/), samen met de Application Insights-invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="c9fbd-104">To explore Linux system performance metrics in [Application Insights](app-insights-overview.md), install [collectd](http://collectd.org/), together with its Application Insights plug-in.</span></span> <span data-ttu-id="c9fbd-105">Deze oplossing open source worden verschillende statistieken voor systeem- en netwerkgegevens verzameld.</span><span class="sxs-lookup"><span data-stu-id="c9fbd-105">This open-source solution gathers various system and network statistics.</span></span>

<span data-ttu-id="c9fbd-106">Doorgaans kunt u collectd als u al hebt [uw Java-webservice met Application Insights geïnstrumenteerd][java].</span><span class="sxs-lookup"><span data-stu-id="c9fbd-106">Typically you'll use collectd if you have already [instrumented your Java web service with Application Insights][java].</span></span> <span data-ttu-id="c9fbd-107">Dit biedt u meer gegevens kunt verbeteren de prestaties van uw app of het analyseren van problemen.</span><span class="sxs-lookup"><span data-stu-id="c9fbd-107">It gives you more data to help you to enhance your app's performance or diagnose problems.</span></span> 

![voorbeeldgrafieken](./media/app-insights-java-collectd/sample.png)

## <a name="get-your-instrumentation-key"></a><span data-ttu-id="c9fbd-109">De instrumentatiesleutel ophalen</span><span class="sxs-lookup"><span data-stu-id="c9fbd-109">Get your instrumentation key</span></span>
<span data-ttu-id="c9fbd-110">In de [Microsoft Azure-portal](https://portal.azure.com), open de [Application Insights](app-insights-overview.md) resource waar u de gegevens wilt weergeven.</span><span class="sxs-lookup"><span data-stu-id="c9fbd-110">In the [Microsoft Azure portal](https://portal.azure.com), open the [Application Insights](app-insights-overview.md) resource where you want the data to appear.</span></span> <span data-ttu-id="c9fbd-111">(Of [Maak een nieuwe resource](app-insights-create-new-resource.md).)</span><span class="sxs-lookup"><span data-stu-id="c9fbd-111">(Or [create a new resource](app-insights-create-new-resource.md).)</span></span>

<span data-ttu-id="c9fbd-112">Duren voordat u een kopie van de instrumentatiesleutel die de resource identificeert.</span><span class="sxs-lookup"><span data-stu-id="c9fbd-112">Take a copy of the instrumentation key, which identifies the resource.</span></span>

![Alles bekijken, opent u de bron en klik vervolgens in de vervolgkeuzelijst Essentials selecteren en de Instrumentatiesleutel kopiëren](./media/app-insights-java-collectd/02-props.png)

## <a name="install-collectd-and-the-plug-in"></a><span data-ttu-id="c9fbd-114">Installeer collectd en de invoegtoepassing</span><span class="sxs-lookup"><span data-stu-id="c9fbd-114">Install collectd and the plug-in</span></span>
<span data-ttu-id="c9fbd-115">Op de Linux-servers:</span><span class="sxs-lookup"><span data-stu-id="c9fbd-115">On your Linux server machines:</span></span>

1. <span data-ttu-id="c9fbd-116">Installeer [collectd](http://collectd.org/) versie 5.4.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="c9fbd-116">Install [collectd](http://collectd.org/) version 5.4.0 or later.</span></span>
2. <span data-ttu-id="c9fbd-117">Download de [Application Insights-invoegtoepassing voor collectd writer](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="c9fbd-117">Download the [Application Insights collectd writer plugin](https://aka.ms/aijavasdk).</span></span> <span data-ttu-id="c9fbd-118">Noteer het versienummer.</span><span class="sxs-lookup"><span data-stu-id="c9fbd-118">Note the version number.</span></span>
3. <span data-ttu-id="c9fbd-119">Kopieer de invoegtoepassing JAR in `/usr/share/collectd/java`.</span><span class="sxs-lookup"><span data-stu-id="c9fbd-119">Copy the plugin JAR into `/usr/share/collectd/java`.</span></span>
4. <span data-ttu-id="c9fbd-120">Bewerken `/etc/collectd/collectd.conf`:</span><span class="sxs-lookup"><span data-stu-id="c9fbd-120">Edit `/etc/collectd/collectd.conf`:</span></span>
   * <span data-ttu-id="c9fbd-121">Zorg ervoor dat [de Java-invoegtoepassing](https://collectd.org/wiki/index.php/Plugin:Java) is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="c9fbd-121">Ensure that [the Java plugin](https://collectd.org/wiki/index.php/Plugin:Java) is enabled.</span></span>
   * <span data-ttu-id="c9fbd-122">De JVMArg voor de java.class.path zodanig dat de volgende JAR bijwerken.</span><span class="sxs-lookup"><span data-stu-id="c9fbd-122">Update the JVMArg for the java.class.path to include the following JAR.</span></span> <span data-ttu-id="c9fbd-123">Update het versienummer overeenkomen met de naam die u hebt gedownload:</span><span class="sxs-lookup"><span data-stu-id="c9fbd-123">Update the version number to match the one you downloaded:</span></span>
   * `/usr/share/collectd/java/applicationinsights-collectd-1.0.5.jar`
   * <span data-ttu-id="c9fbd-124">In dit fragment, met behulp van de Instrumentatiesleutel van uw resource toevoegen:</span><span class="sxs-lookup"><span data-stu-id="c9fbd-124">Add this snippet, using the Instrumentation Key from your resource:</span></span>

```XML

     LoadPlugin "com.microsoft.applicationinsights.collectd.ApplicationInsightsWriter"
     <Plugin ApplicationInsightsWriter>
        InstrumentationKey "Your key"
     </Plugin>
```

<span data-ttu-id="c9fbd-125">Dit is onderdeel van een voorbeeldconfiguratiebestand:</span><span class="sxs-lookup"><span data-stu-id="c9fbd-125">Here's part of a sample configuration file:</span></span>

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

<span data-ttu-id="c9fbd-126">Configureer andere [collectd plugins](https://collectd.org/wiki/index.php/Table_of_Plugins), dat kan verschillende gegevens verzamelen van verschillende gegevensbronnen.</span><span class="sxs-lookup"><span data-stu-id="c9fbd-126">Configure other [collectd plugins](https://collectd.org/wiki/index.php/Table_of_Plugins), which can collect various data from different sources.</span></span>

<span data-ttu-id="c9fbd-127">Opnieuw opstarten collectd volgens de [handmatige](https://collectd.org/wiki/index.php/First_steps).</span><span class="sxs-lookup"><span data-stu-id="c9fbd-127">Restart collectd according to its [manual](https://collectd.org/wiki/index.php/First_steps).</span></span>

## <a name="view-the-data-in-application-insights"></a><span data-ttu-id="c9fbd-128">De gegevens in Application Insights weergeven</span><span class="sxs-lookup"><span data-stu-id="c9fbd-128">View the data in Application Insights</span></span>
<span data-ttu-id="c9fbd-129">Open in uw Application Insights-resource [Metrics Explorer en grafieken toe te voegen][metrics], de metrische gegevens die u wilt zien, uit de categorie Aangepast selecteren.</span><span class="sxs-lookup"><span data-stu-id="c9fbd-129">In your Application Insights resource, open [Metrics Explorer and add charts][metrics], selecting the metrics you want to see from the Custom category.</span></span>

![](./media/app-insights-java-collectd/result.png)

<span data-ttu-id="c9fbd-130">Standaard worden de metrische gegevens geaggregeerd alle host machines waaruit de metrische gegevens zijn verzameld.</span><span class="sxs-lookup"><span data-stu-id="c9fbd-130">By default, the metrics are aggregated across all host machines from which the metrics were collected.</span></span> <span data-ttu-id="c9fbd-131">Om weer te geven de metrische gegevens per host in de grafiek details blade, schakelt u Grouping en kies vervolgens groeperen op CollectD-Host.</span><span class="sxs-lookup"><span data-stu-id="c9fbd-131">To view the metrics per host, in the Chart details blade, turn on Grouping and then choose to group by CollectD-Host.</span></span>

## <a name="to-exclude-upload-of-specific-statistics"></a><span data-ttu-id="c9fbd-132">Uploaden van specifieke statistieken uitsluiten</span><span class="sxs-lookup"><span data-stu-id="c9fbd-132">To exclude upload of specific statistics</span></span>
<span data-ttu-id="c9fbd-133">De Application Insights-invoegtoepassing verzendt standaard alle gegevens die door de ingeschakelde collectd lezen plugins verzameld.</span><span class="sxs-lookup"><span data-stu-id="c9fbd-133">By default, the Application Insights plugin sends all the data collected by all the enabled collectd 'read' plugins.</span></span> 

<span data-ttu-id="c9fbd-134">Gegevens uitsluiten van specifieke invoegtoepassingen of gegevensbronnen:</span><span class="sxs-lookup"><span data-stu-id="c9fbd-134">To exclude data from specific plugins or data sources:</span></span>

* <span data-ttu-id="c9fbd-135">Het configuratiebestand bewerken.</span><span class="sxs-lookup"><span data-stu-id="c9fbd-135">Edit the configuration file.</span></span> 
* <span data-ttu-id="c9fbd-136">In `<Plugin ApplicationInsightsWriter>`, richtlijn regels als volgt toevoegen:</span><span class="sxs-lookup"><span data-stu-id="c9fbd-136">In `<Plugin ApplicationInsightsWriter>`, add directive lines like this:</span></span>

| <span data-ttu-id="c9fbd-137">Richtlijn</span><span class="sxs-lookup"><span data-stu-id="c9fbd-137">Directive</span></span> | <span data-ttu-id="c9fbd-138">Effect</span><span class="sxs-lookup"><span data-stu-id="c9fbd-138">Effect</span></span> |
| --- | --- |
| `Exclude disk` |<span data-ttu-id="c9fbd-139">Uitsluiten van alle gegevens die worden verzameld door de `disk` invoegtoepassing</span><span class="sxs-lookup"><span data-stu-id="c9fbd-139">Exclude all data collected by the `disk` plugin</span></span> |
| `Exclude disk:read,write` |<span data-ttu-id="c9fbd-140">Uitsluiten van de bronnen met de naam `read` en `write` van de `disk` invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="c9fbd-140">Exclude the sources named `read` and `write` from the `disk` plugin.</span></span> |

<span data-ttu-id="c9fbd-141">Afzonderlijke richtlijnen met een nieuwe regel.</span><span class="sxs-lookup"><span data-stu-id="c9fbd-141">Separate directives with a newline.</span></span>

## <a name="problems"></a><span data-ttu-id="c9fbd-142">Problemen?</span><span class="sxs-lookup"><span data-stu-id="c9fbd-142">Problems?</span></span>
<span data-ttu-id="c9fbd-143">*Gegevens in de portal weergegeven niet*</span><span class="sxs-lookup"><span data-stu-id="c9fbd-143">*I don't see data in the portal*</span></span>

* <span data-ttu-id="c9fbd-144">Open [Search] [ diagnostic] om te zien als de onbewerkte gebeurtenissen zijn ontvangen.</span><span class="sxs-lookup"><span data-stu-id="c9fbd-144">Open [Search][diagnostic] to see if the raw events have arrived.</span></span> <span data-ttu-id="c9fbd-145">Soms duurt langer in metrics explorer wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c9fbd-145">Sometimes they take longer to appear in metrics explorer.</span></span>
* <span data-ttu-id="c9fbd-146">Mogelijk moet u [firewalluitzonderingen voor uitgaande gegevens instellen](app-insights-ip-addresses.md)</span><span class="sxs-lookup"><span data-stu-id="c9fbd-146">You might need to [set firewall exceptions for outgoing data](app-insights-ip-addresses.md)</span></span>
* <span data-ttu-id="c9fbd-147">Tracering in de Application Insights-invoegtoepassing inschakelen.</span><span class="sxs-lookup"><span data-stu-id="c9fbd-147">Enable tracing in the Application Insights plugin.</span></span> <span data-ttu-id="c9fbd-148">Deze regel in te voegen `<Plugin ApplicationInsightsWriter>`:</span><span class="sxs-lookup"><span data-stu-id="c9fbd-148">Add this line within `<Plugin ApplicationInsightsWriter>`:</span></span>
  * `SDKLogger true`
* <span data-ttu-id="c9fbd-149">Open een terminal en collectd starten in de uitgebreide modus om te zien of er problemen zijn meldt:</span><span class="sxs-lookup"><span data-stu-id="c9fbd-149">Open a terminal and start collectd in verbose mode, to see any issues it is reporting:</span></span>
  * `sudo collectd -f`

## <a name="known-issue"></a><span data-ttu-id="c9fbd-150">Bekende problemen</span><span class="sxs-lookup"><span data-stu-id="c9fbd-150">Known issue</span></span>

<span data-ttu-id="c9fbd-151">Het schrijven van Application Insights-invoegtoepassing is niet compatibel met bepaalde invoegtoepassingen lezen.</span><span class="sxs-lookup"><span data-stu-id="c9fbd-151">The Application Insights Write plugin is incompatible with certain Read plugins.</span></span> <span data-ttu-id="c9fbd-152">Sommige invoegtoepassingen verzenden soms 'NaN', waarbij de Application Insights-invoegtoepassing een getal met drijvende komma verwacht.</span><span class="sxs-lookup"><span data-stu-id="c9fbd-152">Some plugins sometimes send "NaN" where the Application Insights plugin expects a floating-point number.</span></span>

<span data-ttu-id="c9fbd-153">Symptoom: Het logboek collectd bevat fouten die zijn 'AI:... SyntaxError: onverwacht token N ".</span><span class="sxs-lookup"><span data-stu-id="c9fbd-153">Symptom: The collectd log shows errors that include "AI: ... SyntaxError: Unexpected token N".</span></span>

<span data-ttu-id="c9fbd-154">Tijdelijke oplossing: Uitsluiten gegevens die door het probleem schrijven plugins verzameld.</span><span class="sxs-lookup"><span data-stu-id="c9fbd-154">Workaround: Exclude data collected by the problem Write plugins.</span></span> 

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md


