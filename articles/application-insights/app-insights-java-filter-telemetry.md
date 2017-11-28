---
title: Azure Application Insights telemetrie in uw Java-web-app aaaFilter | Microsoft Docs
description: Verminderen het verkeer van telemetrie Hallo gebeurtenissen filteren hoeft u niet toomonitor.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: bwren
ms.openlocfilehash: 95713e11d5f86472777c67e4e7f3177fbf2cd0b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="filter-telemetry-in-your-java-web-app"></a><span data-ttu-id="6d468-103">Filteren van telemetrie in uw Java-web-app</span><span class="sxs-lookup"><span data-stu-id="6d468-103">Filter telemetry in your Java web app</span></span>

<span data-ttu-id="6d468-104">Filters bieden een manier tooselect Hallo telemetrie die uw [Java-web-app verzendt tooApplication Insights](app-insights-java-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6d468-104">Filters provide a way tooselect hello telemetry that your [Java web app sends tooApplication Insights](app-insights-java-get-started.md).</span></span> <span data-ttu-id="6d468-105">Er zijn een aantal out-of-the-box-filters die u kunt gebruiken en u kunt ook uw eigen aangepaste filters schrijven.</span><span class="sxs-lookup"><span data-stu-id="6d468-105">There are some out-of-the-box filters that you can use, and you can also write your own custom filters.</span></span>

<span data-ttu-id="6d468-106">Hallo out-of-the-box filters omvatten:</span><span class="sxs-lookup"><span data-stu-id="6d468-106">hello out-of-the-box filters include:</span></span>

* <span data-ttu-id="6d468-107">Traceerniveau ernst</span><span class="sxs-lookup"><span data-stu-id="6d468-107">Trace severity level</span></span>
* <span data-ttu-id="6d468-108">Specifieke URL's, trefwoorden of reactiecodes</span><span class="sxs-lookup"><span data-stu-id="6d468-108">Specific URLs, keywords or response codes</span></span>
* <span data-ttu-id="6d468-109">Snel op netwerkaanvragen - aanvragen dat wil zeggen toowhich uw app gereageerd tooquickly</span><span class="sxs-lookup"><span data-stu-id="6d468-109">Fast responses - that is, requests toowhich your app responded tooquickly</span></span>
* <span data-ttu-id="6d468-110">Namen van de specifieke gebeurtenis</span><span class="sxs-lookup"><span data-stu-id="6d468-110">Specific event names</span></span>

> [!NOTE]
> <span data-ttu-id="6d468-111">Filters leiden tot onjuiste Hallo metrische gegevens van uw app.</span><span class="sxs-lookup"><span data-stu-id="6d468-111">Filters skew hello metrics of your app.</span></span> <span data-ttu-id="6d468-112">U kunt bijvoorbeeld besluiten dat de snelle responstijden van een filter-toodiscard in trage reacties in bindingsvolgorde toodiagnose, wordt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="6d468-112">For example, you might decide that, in order toodiagnose slow responses, you will set a filter toodiscard fast response times.</span></span> <span data-ttu-id="6d468-113">Maar u moet rekening houden dat Hallo gemiddelde reactietijd van gerapporteerd door de Application Insights vervolgens langzamer dan Hallo ware snelheid zijn en Hallo aantal aanvragen kleiner dan de werkelijke telling Hallo is.</span><span class="sxs-lookup"><span data-stu-id="6d468-113">But you must be aware that hello average response times reported by Application Insights will then be slower than hello true speed, and hello count of requests will be smaller than hello real count.</span></span>
> <span data-ttu-id="6d468-114">Als dit een probleem is, gebruikt u [steekproeven](app-insights-sampling.md) in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="6d468-114">If this is a concern, use [Sampling](app-insights-sampling.md) instead.</span></span>

## <a name="setting-filters"></a><span data-ttu-id="6d468-115">Filters instellen</span><span class="sxs-lookup"><span data-stu-id="6d468-115">Setting filters</span></span>

<span data-ttu-id="6d468-116">Voeg ApplicationInsights.xml, een `TelemetryProcessors` sectie zoals in dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="6d468-116">In ApplicationInsights.xml, add a `TelemetryProcessors` section like this example:</span></span>


```XML

    <ApplicationInsights>
      <TelemetryProcessors>

        <BuiltInProcessors>
           <Processor type="TraceTelemetryFilter">
                  <Add name="FromSeverityLevel" value="ERROR"/>
           </Processor>

           <Processor type="RequestTelemetryFilter">
                  <Add name="MinimumDurationInMS" value="100"/>
                  <Add name="NotNeededResponseCodes" value="200-400"/>
           </Processor>

           <Processor type="PageViewTelemetryFilter">
                  <Add name="DurationThresholdInMS" value="100"/>
                  <Add name="NotNeededNames" value="home,index"/>
                  <Add name="NotNeededUrls" value=".jpg,.css"/>
           </Processor>

           <Processor type="TelemetryEventFilter">
                  <!-- Names of events we don't want toosee -->
                  <Add name="NotNeededNames" value="Start,Stop,Pause"/>
           </Processor>

           <!-- Exclude telemetry from availability tests and bots -->
           <Processor type="SyntheticSourceFilter">
                <!-- Optional: specify which synthetic sources,
                     comma-separated
                     - default is all synthetics -->
                <Add name="NotNeededSources" value="Application Insights Availability Monitoring,BingPreview"
           </Processor>

        </BuiltInProcessors>

        <CustomProcessors>
          <Processor type="com.fabrikam.MyFilter">
            <Add name="Successful" value="false"/>
          </Processor>
        </CustomProcessors>

      </TelemetryProcessors>
    </ApplicationInsights>

```




<span data-ttu-id="6d468-117">[Inspecteer de volledige set Hallo van ingebouwde processors](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor).</span><span class="sxs-lookup"><span data-stu-id="6d468-117">[Inspect hello full set of built-in processors](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor).</span></span>

## <a name="built-in-filters"></a><span data-ttu-id="6d468-118">Ingebouwde filters</span><span class="sxs-lookup"><span data-stu-id="6d468-118">Built-in filters</span></span>

### <a name="metric-telemetry-filter"></a><span data-ttu-id="6d468-119">Metrische telemetrie-filter</span><span class="sxs-lookup"><span data-stu-id="6d468-119">Metric Telemetry filter</span></span>

```XML

           <Processor type="MetricTelemetryFilter">
                  <Add name="NotNeeded" value="metric1,metric2"/>
           </Processor>
```

* <span data-ttu-id="6d468-120">`NotNeeded`-Met door komma's gescheiden lijst met aangepaste metrische namen.</span><span class="sxs-lookup"><span data-stu-id="6d468-120">`NotNeeded` - Comma-separated list of custom metric names.</span></span>


### <a name="page-view-telemetry-filter"></a><span data-ttu-id="6d468-121">Filter telemetrie van paginaweergaven</span><span class="sxs-lookup"><span data-stu-id="6d468-121">Page View Telemetry filter</span></span>

```XML

           <Processor type="PageViewTelemetryFilter">
                  <Add name="DurationThresholdInMS" value="500"/>
                  <Add name="NotNeededNames" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```

* <span data-ttu-id="6d468-122">`DurationThresholdInMS`-Duur verwijst toohello tijd tooload Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="6d468-122">`DurationThresholdInMS` - Duration refers toohello time taken tooload hello page.</span></span> <span data-ttu-id="6d468-123">Als deze optie is ingesteld, worden pagina's die sneller dan de opgegeven tijd wordt geladen niet gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="6d468-123">If this is set, pages that loaded faster than this time are not reported.</span></span>
* <span data-ttu-id="6d468-124">`NotNeededNames`-Met door komma's gescheiden lijst met paginanamen.</span><span class="sxs-lookup"><span data-stu-id="6d468-124">`NotNeededNames` - Comma-separated list of page names.</span></span>
* <span data-ttu-id="6d468-125">`NotNeededUrls`-Door komma's gescheiden lijst met URL-fragmenten.</span><span class="sxs-lookup"><span data-stu-id="6d468-125">`NotNeededUrls` - Comma-separated list of URL fragments.</span></span> <span data-ttu-id="6d468-126">Bijvoorbeeld: `"home"` gefilterd op alle pagina's die u hebt "home" Hallo-URL.</span><span class="sxs-lookup"><span data-stu-id="6d468-126">For example, `"home"` filters out all pages that have "home" in hello URL.</span></span>


### <a name="request-telemetry-filter"></a><span data-ttu-id="6d468-127">Telemetrie-Filter aanvragen</span><span class="sxs-lookup"><span data-stu-id="6d468-127">Request Telemetry Filter</span></span>


```XML

           <Processor type="RequestTelemetryFilter">
                  <Add name="MinimumDurationInMS" value="500"/>
                  <Add name="NotNeededResponseCodes" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```



### <a name="synthetic-source-filter"></a><span data-ttu-id="6d468-128">Synthetische bronfilter</span><span class="sxs-lookup"><span data-stu-id="6d468-128">Synthetic Source filter</span></span>

<span data-ttu-id="6d468-129">Alle telemetrie met waarden in Hallo SyntheticSource eigenschap gefilterd.</span><span class="sxs-lookup"><span data-stu-id="6d468-129">Filters out all telemetry that have values in hello SyntheticSource property.</span></span> <span data-ttu-id="6d468-130">Het gaat hierbij om aanvragen van bots, spiders en beschikbaarheidstests.</span><span class="sxs-lookup"><span data-stu-id="6d468-130">These include requests from bots, spiders and availability tests.</span></span>

<span data-ttu-id="6d468-131">Telemetrie voor alle synthetische aanvragen filteren:</span><span class="sxs-lookup"><span data-stu-id="6d468-131">Filter out telemetry for all synthetic requests:</span></span>


```XML

           <Processor type="SyntheticSourceFilter" />
```

<span data-ttu-id="6d468-132">Telemetrie voor specifieke synthetische bronnen filteren:</span><span class="sxs-lookup"><span data-stu-id="6d468-132">Filter out telemetry for specific synthetic sources:</span></span>


```XML

           <Processor type="SyntheticSourceFilter" >
                  <Add name="NotNeeded" value="source1,source2"/>
           </Processor>
```

* <span data-ttu-id="6d468-133">`NotNeeded`-Met door komma's gescheiden lijst met namen van synthetische gegevensbronnen.</span><span class="sxs-lookup"><span data-stu-id="6d468-133">`NotNeeded` - Comma-separated list of synthetic source names.</span></span>

### <a name="telemetry-event-filter"></a><span data-ttu-id="6d468-134">Gebeurtenisfilter telemetrie</span><span class="sxs-lookup"><span data-stu-id="6d468-134">Telemetry Event filter</span></span>

<span data-ttu-id="6d468-135">Aangepaste gebeurtenissen gefilterd (vastgelegd met behulp van [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)).</span><span class="sxs-lookup"><span data-stu-id="6d468-135">Filters custom events (logged using [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)).</span></span>


```XML

           <Processor type="TelemetryEventFilter" >
                  <Add name="NotNeededNames" value="event1, event2"/>
           </Processor>
```


* <span data-ttu-id="6d468-136">`NotNeededNames`-Met door komma's gescheiden lijst met gebeurtenisnamen.</span><span class="sxs-lookup"><span data-stu-id="6d468-136">`NotNeededNames` - Comma-separated list of event names.</span></span>


### <a name="trace-telemetry-filter"></a><span data-ttu-id="6d468-137">Tracering telemetrie filter</span><span class="sxs-lookup"><span data-stu-id="6d468-137">Trace Telemetry filter</span></span>

<span data-ttu-id="6d468-138">Meld u filters traceringen (vastgelegd met behulp van [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) of een [logboekregistratie framework collector](app-insights-java-trace-logs.md)).</span><span class="sxs-lookup"><span data-stu-id="6d468-138">Filters log traces (logged using [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) or a [logging framework collector](app-insights-java-trace-logs.md)).</span></span>

```XML

           <Processor type="TraceTelemetryFilter">
                  <Add name="FromSeverityLevel" value="ERROR"/>
           </Processor>
```

* <span data-ttu-id="6d468-139">`FromSeverityLevel`geldige waarden zijn:</span><span class="sxs-lookup"><span data-stu-id="6d468-139">`FromSeverityLevel` valid values are:</span></span>
 *  <span data-ttu-id="6d468-140">BUITEN - alle traceringen filteren</span><span class="sxs-lookup"><span data-stu-id="6d468-140">OFF             - Filter out ALL traces</span></span>
 *  <span data-ttu-id="6d468-141">TRACE - geen filters.</span><span class="sxs-lookup"><span data-stu-id="6d468-141">TRACE           - No filtering.</span></span> <span data-ttu-id="6d468-142">tooTrace niveau is gelijk aan</span><span class="sxs-lookup"><span data-stu-id="6d468-142">equals tooTrace level</span></span>
 *  <span data-ttu-id="6d468-143">INFO - uitfilteren traceerniveau</span><span class="sxs-lookup"><span data-stu-id="6d468-143">INFO            - Filter out TRACE level</span></span>
 *  <span data-ttu-id="6d468-144">Waarschuwen - uitfilteren TRACE en gegevens</span><span class="sxs-lookup"><span data-stu-id="6d468-144">WARN            - Filter out TRACE and INFO</span></span>
 *  <span data-ttu-id="6d468-145">Fout - uitfilteren waarschuwen, INFO, traceren</span><span class="sxs-lookup"><span data-stu-id="6d468-145">ERROR           - Filter out WARN, INFO, TRACE</span></span>
 *  <span data-ttu-id="6d468-146">KRITIEKE - filter uit alle kritieke</span><span class="sxs-lookup"><span data-stu-id="6d468-146">CRITICAL        - filter out all but CRITICAL</span></span>


## <a name="custom-filters"></a><span data-ttu-id="6d468-147">Aangepaste filters</span><span class="sxs-lookup"><span data-stu-id="6d468-147">Custom filters</span></span>

### <a name="1-code-your-filter"></a><span data-ttu-id="6d468-148">1. Code van uw filter</span><span class="sxs-lookup"><span data-stu-id="6d468-148">1. Code your filter</span></span>

<span data-ttu-id="6d468-149">Maak een klasse die wordt geïmplementeerd in uw code `TelemetryProcessor`:</span><span class="sxs-lookup"><span data-stu-id="6d468-149">In your code, create a class that implements `TelemetryProcessor`:</span></span>

```Java

    package com.fabrikam.MyFilter;
    import com.microsoft.applicationinsights.extensibility.TelemetryProcessor;
    import com.microsoft.applicationinsights.telemetry.Telemetry;

    public class SuccessFilter implements TelemetryProcessor {

       /* Any parameters that are required toosupport hello filter.*/
       private final String successful;

       /* Initializers for hello parameters, named "setParameterName" */
       public void setNotNeeded(String successful)
       {
          this.successful = successful;
       }

       /* This method is called for each item of telemetry toobe sent.
          Return false toodiscard it.
          Return true tooallow other processors tooinspect it. */
       @Override
       public boolean process(Telemetry telemetry) {
        if (telemetry == null) { return true; }
        if (telemetry instanceof RequestTelemetry)
        {
            RequestTelemetry requestTelemetry = (RequestTelemetry)telemetry;
            return request.getSuccess() == successful;
        }
        return true;
       }
    }

```


### <a name="2-invoke-your-filter-in-hello-configuration-file"></a><span data-ttu-id="6d468-150">2. Het filter in het configuratiebestand Hallo aanroepen</span><span class="sxs-lookup"><span data-stu-id="6d468-150">2. Invoke your filter in hello configuration file</span></span>

<span data-ttu-id="6d468-151">In ApplicationInsights.xml:</span><span class="sxs-lookup"><span data-stu-id="6d468-151">In ApplicationInsights.xml:</span></span>

```XML


    <ApplicationInsights>
      <TelemetryProcessors>
        <CustomProcessors>
          <Processor type="com.fabrikam.SuccessFilter">
            <Add name="Successful" value="false"/>
          </Processor>
        </CustomProcessors>
      </TelemetryProcessors>
    </ApplicationInsights>

```

## <a name="troubleshooting"></a><span data-ttu-id="6d468-152">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="6d468-152">Troubleshooting</span></span>

<span data-ttu-id="6d468-153">*Mijn filter werkt niet.*</span><span class="sxs-lookup"><span data-stu-id="6d468-153">*My filter isn't working.*</span></span>

* <span data-ttu-id="6d468-154">Controleer of u geldige parameterwaarden hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="6d468-154">Check that you have provided valid parameter values.</span></span> <span data-ttu-id="6d468-155">Duur moet bijvoorbeeld gehele getallen zijn.</span><span class="sxs-lookup"><span data-stu-id="6d468-155">For example, durations should be integers.</span></span> <span data-ttu-id="6d468-156">Ongeldige waarden zal Hallo filter toobe genegeerd.</span><span class="sxs-lookup"><span data-stu-id="6d468-156">Invalid values will cause hello filter toobe ignored.</span></span> <span data-ttu-id="6d468-157">Als u een aangepaste filter er een uitzondering gegenereerd vanuit een constructor of een set-methode, worden genegeerd.</span><span class="sxs-lookup"><span data-stu-id="6d468-157">If your custom filter throws an exception from a constructor or set method, it will be ignored.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d468-158">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6d468-158">Next steps</span></span>

* <span data-ttu-id="6d468-159">[Steekproef nemen](app-insights-sampling.md) -steekproeven als alternatief die niet leiden tot metrische gegevens over uw onjuiste komt overwegen.</span><span class="sxs-lookup"><span data-stu-id="6d468-159">[Sampling](app-insights-sampling.md) - Consider sampling as an alternative that does not skew your metrics.</span></span>
