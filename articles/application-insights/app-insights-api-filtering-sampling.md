---
title: aaaFiltering en voorverwerking hello Azure Application Insights-SDK | Microsoft Docs
description: Telemetrie-Processors en initalisatiefuncties telemetrie schrijven voor Hallo SDK toofilter of eigenschappen toohello gegevens toevoegen voordat Hallo telemetrie toohello Application Insights-portal wordt verzonden.
services: application-insights
documentationcenter: 
author: beckylino
manager: carmonm
ms.assetid: 38a9e454-43d5-4dba-a0f0-bd7cd75fb97b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 11/23/2016
ms.author: bwren
ms.openlocfilehash: 51b9db69b2375b8799718f1b0e1af77620dc2692
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="filtering-and-preprocessing-telemetry-in-hello-application-insights-sdk"></a><span data-ttu-id="66103-103">Filteren en telemetrie in Application Insights-SDK Hallo voorverwerking</span><span class="sxs-lookup"><span data-stu-id="66103-103">Filtering and preprocessing telemetry in hello Application Insights SDK</span></span>


<span data-ttu-id="66103-104">U kunt schrijven en configureren van invoegtoepassingen voor Hallo Application Insights-SDK toocustomize hoe telemetrie worden vastgelegd en verwerkt voordat deze toohello Application Insights-service wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="66103-104">You can write and configure plug-ins for hello Application Insights SDK toocustomize how telemetry is captured and processed before it is sent toohello Application Insights service.</span></span>

* <span data-ttu-id="66103-105">[Steekproef nemen](app-insights-sampling.md) Hallo volume telemetrie zonder uw statistieken vermindert.</span><span class="sxs-lookup"><span data-stu-id="66103-105">[Sampling](app-insights-sampling.md) reduces hello volume of telemetry without affecting your statistics.</span></span> <span data-ttu-id="66103-106">Samen blijven gerelateerde gegevenspunten zodat u tussen deze twee navigeren kunt bij het oplossen van een probleem.</span><span class="sxs-lookup"><span data-stu-id="66103-106">It keeps together related data points so that you can navigate between them when diagnosing a problem.</span></span> <span data-ttu-id="66103-107">In Hallo-portal zijn Hallo totale aantal uitkomsten toocompensate voor Hallo steekproeven.</span><span class="sxs-lookup"><span data-stu-id="66103-107">In hello portal, hello total counts are multiplied toocompensate for hello sampling.</span></span>
* <span data-ttu-id="66103-108">Filteren met telemetrie Processors [voor ASP.NET](#filtering) of [Java](app-insights-java-filter-telemetry.md) kunt u selecteren of telemetrie in Hallo SDK wijzigen voordat deze toohello server wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="66103-108">Filtering with Telemetry Processors [for ASP.NET](#filtering) or [Java](app-insights-java-filter-telemetry.md) lets you select or modify telemetry in hello SDK before it is sent toohello server.</span></span> <span data-ttu-id="66103-109">U kunt bijvoorbeeld Hallo volume telemetrie verminderen aanvragen door uit te sluiten robots.</span><span class="sxs-lookup"><span data-stu-id="66103-109">For example, you could reduce hello volume of telemetry by excluding requests from robots.</span></span> <span data-ttu-id="66103-110">Maar voor het filteren is een eenvoudige benadering tooreducing verkeer dan steekproeven.</span><span class="sxs-lookup"><span data-stu-id="66103-110">But filtering is a more basic approach tooreducing traffic than sampling.</span></span> <span data-ttu-id="66103-111">Hiermee kunt u meer controle over wat wordt verzonden, maar u hebt toobe Houd er rekening mee dat dit van invloed op uw statistieken - bijvoorbeeld, als u alle geslaagde aanvragen filteren.</span><span class="sxs-lookup"><span data-stu-id="66103-111">It allows you more control over what is transmitted, but you have toobe aware that it affects your statistics - for example, if you filter out all successful requests.</span></span>
* <span data-ttu-id="66103-112">[Telemetrie initalisatiefuncties eigenschappen toevoegen](#add-properties) tooany telemetrie van uw app, inclusief telemetrie van de standaard modules Hallo verzonden.</span><span class="sxs-lookup"><span data-stu-id="66103-112">[Telemetry Initializers add properties](#add-properties) tooany telemetry sent from your app, including telemetry from hello standard modules.</span></span> <span data-ttu-id="66103-113">Bijvoorbeeld zou u berekende waarden; of versienummers waarop toofilter Hallo de gegevens in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="66103-113">For example, you could add calculated values; or version numbers by which toofilter hello data in hello portal.</span></span>
* <span data-ttu-id="66103-114">[Hallo SDK-API](app-insights-api-custom-events-metrics.md) gebruikte toosend aangepaste gebeurtenissen en metrische gegevens is.</span><span class="sxs-lookup"><span data-stu-id="66103-114">[hello SDK API](app-insights-api-custom-events-metrics.md) is used toosend custom events and metrics.</span></span>

<span data-ttu-id="66103-115">Voordat u begint:</span><span class="sxs-lookup"><span data-stu-id="66103-115">Before you start:</span></span>

* <span data-ttu-id="66103-116">Installeer Application Insights-Hallo [SDK voor ASP.NET](app-insights-asp-net.md) of [SDK voor Java](app-insights-java-get-started.md) in uw app.</span><span class="sxs-lookup"><span data-stu-id="66103-116">Install hello Application Insights [SDK for ASP.NET](app-insights-asp-net.md) or [SDK for Java](app-insights-java-get-started.md) in your app.</span></span>

<a name="filtering"></a>

## <a name="filtering-itelemetryprocessor"></a><span data-ttu-id="66103-117">Filteren: ITelemetryProcessor</span><span class="sxs-lookup"><span data-stu-id="66103-117">Filtering: ITelemetryProcessor</span></span>
<span data-ttu-id="66103-118">Deze techniek hebt u meer rechtstreekse controle over wat is opgenomen of uitgesloten van de telemetriestroom Hallo.</span><span class="sxs-lookup"><span data-stu-id="66103-118">This technique gives you more direct control over what is included or excluded from hello telemetry stream.</span></span> <span data-ttu-id="66103-119">U kunt deze gebruiken in combinatie met steekproeven, of afzonderlijk.</span><span class="sxs-lookup"><span data-stu-id="66103-119">You can use it in conjunction with Sampling, or separately.</span></span>

<span data-ttu-id="66103-120">toofilter telemetrie, een processor telemetrie schrijven en bij Hallo SDK registreren.</span><span class="sxs-lookup"><span data-stu-id="66103-120">toofilter telemetry, you write a telemetry processor and register it with hello SDK.</span></span> <span data-ttu-id="66103-121">Alle telemetrie doorloopt de processor en kunt u toodrop op Hallo streamen of eigenschappen toevoegen.</span><span class="sxs-lookup"><span data-stu-id="66103-121">All telemetry goes through your processor, and you can choose toodrop it from hello stream, or add properties.</span></span> <span data-ttu-id="66103-122">Dit omvat de telemetrie van Hallo standaard modules zoals Hallo HTTP-aanvraag collector en Hallo afhankelijkheid collector, evenals de telemetrie die u zelf hebt geschreven.</span><span class="sxs-lookup"><span data-stu-id="66103-122">This includes telemetry from hello standard modules such as hello HTTP request collector and hello dependency collector, as well as telemetry you have written yourself.</span></span> <span data-ttu-id="66103-123">U kunt, bijvoorbeeld telemetrie over aanvragen van robots of geslaagde afhankelijkheidsaanroepen filter.</span><span class="sxs-lookup"><span data-stu-id="66103-123">You can, for example, filter out telemetry about requests from robots, or successful dependency calls.</span></span>

> [!WARNING]
> <span data-ttu-id="66103-124">Hallo telemetrie verzonden van Hallo SDK filteren met behulp van processors kan laten uitvallen Hallo statistieken zien in de portal Hallo en maken het moeilijk toofollow verwante objecten.</span><span class="sxs-lookup"><span data-stu-id="66103-124">Filtering hello telemetry sent from hello SDK using processors can skew hello statistics that you see in hello portal, and make it difficult toofollow related items.</span></span>
>
> <span data-ttu-id="66103-125">In plaats daarvan kunt u overwegen [steekproeven](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="66103-125">Instead, consider using [sampling](app-insights-sampling.md).</span></span>
>
>

### <a name="create-a-telemetry-processor-c"></a><span data-ttu-id="66103-126">Maken van een telemetrie-processor (C#)</span><span class="sxs-lookup"><span data-stu-id="66103-126">Create a telemetry processor (C#)</span></span>
1. <span data-ttu-id="66103-127">Controleer of deze Hallo Application Insights-SDK in uw project is versie 2.0.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="66103-127">Verify that hello Application Insights SDK in your project is  version 2.0.0 or later.</span></span> <span data-ttu-id="66103-128">Met de rechtermuisknop op het project in Visual Studio Solution Explorer en kies NuGet-pakketten beheren.</span><span class="sxs-lookup"><span data-stu-id="66103-128">Right-click your project in Visual Studio Solution Explorer and choose Manage NuGet Packages.</span></span> <span data-ttu-id="66103-129">Schakel in NuGet-Pakketbeheer Microsoft.ApplicationInsights.Web.</span><span class="sxs-lookup"><span data-stu-id="66103-129">In NuGet package manager, check Microsoft.ApplicationInsights.Web.</span></span>
2. <span data-ttu-id="66103-130">een filter, toocreate ITelemetryProcessor implementeren.</span><span class="sxs-lookup"><span data-stu-id="66103-130">toocreate a filter, implement ITelemetryProcessor.</span></span> <span data-ttu-id="66103-131">Dit is een andere uitbreidbaar punt zoals telemetrie-module, telemetrie initialisatiefunctie en telemetrie-kanaal.</span><span class="sxs-lookup"><span data-stu-id="66103-131">This is another extensibility point like telemetry module, telemetry initializer, and telemetry channel.</span></span>

    <span data-ttu-id="66103-132">U ziet dat telemetrie Processors samenstellen van een keten van verwerking.</span><span class="sxs-lookup"><span data-stu-id="66103-132">Notice that Telemetry Processors construct a chain of processing.</span></span> <span data-ttu-id="66103-133">Bij het instantiëren van een processor telemetrie moet u een koppeling toohello volgende processor in de keten Hallo doorgeven.</span><span class="sxs-lookup"><span data-stu-id="66103-133">When you instantiate a telemetry processor, you pass a link toohello next processor in hello chain.</span></span> <span data-ttu-id="66103-134">Wanneer een gegevenspunt telemetrie toohello proces methode doorgegeven wordt, wordt het werk en vervolgens aanroepen volgende telemetrie Processor in de keten Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="66103-134">When a telemetry data point is passed toohello Process method, it does its work and then calls hello next Telemetry Processor in hello chain.</span></span>

    ``` C#

    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.Extensibility;

    public class SuccessfulDependencyFilter : ITelemetryProcessor
      {

        private ITelemetryProcessor Next { get; set; }

        // You can pass values from .config
        public string MyParamFromConfigFile { get; set; }

        // Link processors tooeach other in a chain.
        public SuccessfulDependencyFilter(ITelemetryProcessor next)
        {
            this.Next = next;
        }
        public void Process(ITelemetry item)
        {
            // toofilter out an item, just return
            if (!OKtoSend(item)) { return; }
            // Modify hello item if required
            ModifyItem(item);

            this.Next.Process(item);
        }

        // Example: replace with your own criteria.
        private bool OKtoSend (ITelemetry item)
        {
            var dependency = item as DependencyTelemetry;
            if (dependency == null) return true;

            return dependency.Success != true;
        }

        // Example: replace with your own modifiers.
        private void ModifyItem (ITelemetry item)
        {
            item.Context.Properties.Add("app-version", "1." + MyParamFromConfigFile);
        }
    }

    ```
1. <span data-ttu-id="66103-135">Voeg dit in ApplicationInsights.config:</span><span class="sxs-lookup"><span data-stu-id="66103-135">Insert this in ApplicationInsights.config:</span></span>

```XML

    <TelemetryProcessors>
      <Add Type="WebApplication9.SuccessfulDependencyFilter, WebApplication9">
         <!-- Set public property -->
         <MyParamFromConfigFile>2-beta</MyParamFromConfigFile>
      </Add>
    </TelemetryProcessors>

```

<span data-ttu-id="66103-136">(Dit is Hallo dezelfde sectie waarin u een filter steekproeven initialiseren.)</span><span class="sxs-lookup"><span data-stu-id="66103-136">(This is hello same section where you initialize a sampling filter.)</span></span>

<span data-ttu-id="66103-137">U kunt tekenreekswaarden doorgeven van Hallo .config-bestand door openbare benoemde eigenschappen in uw klasse.</span><span class="sxs-lookup"><span data-stu-id="66103-137">You can pass string values from hello .config file by providing public named properties in your class.</span></span>

> [!WARNING]
> <span data-ttu-id="66103-138">Wees voorzichtig toomatch Hallo typenaam en eventuele eigenschapsnamen in Hallo .config-bestand toohello klasse en eigenschapnamen in Hallo-code.</span><span class="sxs-lookup"><span data-stu-id="66103-138">Take care toomatch hello type name and any property names in hello .config file toohello class and property names in hello code.</span></span> <span data-ttu-id="66103-139">Als Hallo .config-bestand verwijst naar een niet-bestaande type of een eigenschap, mislukken Hallo SDK achtergrond toosend alle telemetrie.</span><span class="sxs-lookup"><span data-stu-id="66103-139">If hello .config file references a non-existent type or property, hello SDK may silently fail toosend any telemetry.</span></span>
>
>

<span data-ttu-id="66103-140">**U kunt ook** Hallo-filter in de code kan worden geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="66103-140">**Alternatively,** you can initialize hello filter in code.</span></span> <span data-ttu-id="66103-141">Voeg de processor in de keten Hallo in een initialisatieklasse geschikte - bijvoorbeeld AppStart in Global.asax.cs:</span><span class="sxs-lookup"><span data-stu-id="66103-141">In a suitable initialization class - for example AppStart in Global.asax.cs - insert your processor into hello chain:</span></span>

```C#

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;
    builder.Use((next) => new SuccessfulDependencyFilter(next));

    // If you have more processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="66103-142">TelemetryClients gemaakt nadat dit punt wordt gebruik van uw processors.</span><span class="sxs-lookup"><span data-stu-id="66103-142">TelemetryClients created after this point will use your processors.</span></span>

### <a name="example-filters"></a><span data-ttu-id="66103-143">Voorbeeld-filters</span><span class="sxs-lookup"><span data-stu-id="66103-143">Example filters</span></span>
#### <a name="synthetic-requests"></a><span data-ttu-id="66103-144">Synthetische aanvragen</span><span class="sxs-lookup"><span data-stu-id="66103-144">Synthetic requests</span></span>
<span data-ttu-id="66103-145">Filter bots en web-tests.</span><span class="sxs-lookup"><span data-stu-id="66103-145">Filter out bots and web tests.</span></span> <span data-ttu-id="66103-146">Hoewel Metrics Explorer geeft u de optie toofilter uit synthetische bronnen Hallo, deze optie verkeer beperkt door ze te filteren op Hallo SDK.</span><span class="sxs-lookup"><span data-stu-id="66103-146">Although Metrics Explorer gives you hello option toofilter out synthetic sources, this option reduces traffic by filtering them at hello SDK.</span></span>

``` C#

    public void Process(ITelemetry item)
    {
      if (!string.IsNullOrEmpty(item.Context.Operation.SyntheticSource)) {return;}

      // Send everything else:
      this.Next.Process(item);
    }

```

#### <a name="failed-authentication"></a><span data-ttu-id="66103-147">Mislukte verificatiepogingen</span><span class="sxs-lookup"><span data-stu-id="66103-147">Failed authentication</span></span>
<span data-ttu-id="66103-148">Filteren van aanvragen met een '401'-respons.</span><span class="sxs-lookup"><span data-stu-id="66103-148">Filter out requests with a "401" response.</span></span>

```C#

public void Process(ITelemetry item)
{
    var request = item as RequestTelemetry;

    if (request != null &&
    request.ResponseCode.Equals("401", StringComparison.OrdinalIgnoreCase))
    {
        // toofilter out an item, just terminate hello chain:
        return;
    }
    // Send everything else:
    this.Next.Process(item);
}

```

#### <a name="filter-out-fast-remote-dependency-calls"></a><span data-ttu-id="66103-149">Snel externe afhankelijkheidsaanroepen uitfilteren</span><span class="sxs-lookup"><span data-stu-id="66103-149">Filter out fast remote dependency calls</span></span>
<span data-ttu-id="66103-150">Als u wilt dat alleen toodiagnose aanroepen die traag, filter Hallo fast die zijn.</span><span class="sxs-lookup"><span data-stu-id="66103-150">If you only want toodiagnose calls that are slow, filter out hello fast ones.</span></span>

> [!NOTE]
> <span data-ttu-id="66103-151">Hiermee wordt een verkeerd Hallo statistieken u op Hallo-portal ziet.</span><span class="sxs-lookup"><span data-stu-id="66103-151">This will skew hello statistics you see on hello portal.</span></span> <span data-ttu-id="66103-152">Hallo afhankelijkheid grafiek ziet er als Hallo afhankelijkheidsaanroepen alle fouten zijn.</span><span class="sxs-lookup"><span data-stu-id="66103-152">hello dependency chart will look as if hello dependency calls are all failures.</span></span>
>
>

``` C#

public void Process(ITelemetry item)
{
    var request = item as DependencyTelemetry;

    if (request != null && request.Duration.TotalMilliseconds < 100)
    {
        return;
    }
    this.Next.Process(item);
}

```

#### <a name="diagnose-dependency-issues"></a><span data-ttu-id="66103-153">Problemen als gevolg van diagnoseafhankelijkheid</span><span class="sxs-lookup"><span data-stu-id="66103-153">Diagnose dependency issues</span></span>
<span data-ttu-id="66103-154">[Deze blog](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) beschrijft een project toodiagnose afhankelijkheidsproblemen door reguliere pings toodependencies automatisch verzenden.</span><span class="sxs-lookup"><span data-stu-id="66103-154">[This blog](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) describes a project toodiagnose dependency issues by automatically sending regular pings toodependencies.</span></span>


<a name="add-properties"></a>

## <a name="add-properties-itelemetryinitializer"></a><span data-ttu-id="66103-155">Eigenschappen toevoegen: ITelemetryInitializer</span><span class="sxs-lookup"><span data-stu-id="66103-155">Add properties: ITelemetryInitializer</span></span>
<span data-ttu-id="66103-156">Telemetrie initalisatiefuncties toodefine globale eigenschappen gebruiken die worden verzonden met alle telemetrie; en toooverride gedrag van Hallo standaard telemetrie modules geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="66103-156">Use telemetry initializers toodefine global properties that are sent with all telemetry; and toooverride selected behavior of hello standard telemetry modules.</span></span>

<span data-ttu-id="66103-157">Hallo Application Insights voor Web-pakket verzamelt bijvoorbeeld telemetrie over HTTP-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="66103-157">For example, hello Application Insights for Web package collects telemetry about HTTP requests.</span></span> <span data-ttu-id="66103-158">Standaard worden gemarkeerd als een aanvraag met een antwoordcode mislukt > = 400.</span><span class="sxs-lookup"><span data-stu-id="66103-158">By default, it flags as failed any request with a response code >= 400.</span></span> <span data-ttu-id="66103-159">Maar als u wilt dat tootreat 400 een geslaagde test, kunt u een initialisatiefunctie voor telemetrie waarmee Hallo geslaagd eigenschap wordt ingesteld opgeven.</span><span class="sxs-lookup"><span data-stu-id="66103-159">But if you want tootreat 400 as a success, you can provide a telemetry initializer that sets hello Success property.</span></span>

<span data-ttu-id="66103-160">Als u een initialisatiefunctie telemetrie opgeeft, wordt aangeroepen wanneer een van de Track*() Hallo methoden wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="66103-160">If you provide a telemetry initializer, it is called whenever any of hello Track*() methods is called.</span></span> <span data-ttu-id="66103-161">Dit omvat de methoden die worden aangeroepen door Hallo standaard telemetrie modules.</span><span class="sxs-lookup"><span data-stu-id="66103-161">This includes methods called by hello standard telemetry modules.</span></span> <span data-ttu-id="66103-162">Volgens de conventies worden alle eigenschappen die al is ingesteld door een initialisatiefunctie voor objecten in deze modules niet ingesteld.</span><span class="sxs-lookup"><span data-stu-id="66103-162">By convention, these modules do not set any property that has already been set by an initializer.</span></span>

<span data-ttu-id="66103-163">**De initialisatiefunctie definiëren**</span><span class="sxs-lookup"><span data-stu-id="66103-163">**Define your initializer**</span></span>

<span data-ttu-id="66103-164">*C#*</span><span class="sxs-lookup"><span data-stu-id="66103-164">*C#*</span></span>

```C#

    using System;
    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.DataContracts;
    using Microsoft.ApplicationInsights.Extensibility;

    namespace MvcWebRole.Telemetry
    {
      /*
       * Custom TelemetryInitializer that overrides hello default SDK
       * behavior of treating response codes >= 400 as failed requests
       *
       */
      public class MyTelemetryInitializer : ITelemetryInitializer
      {
        public void Initialize(ITelemetry telemetry)
        {
            var requestTelemetry = telemetry as RequestTelemetry;
            // Is this a TrackRequest() ?
            if (requestTelemetry == null) return;
            int code;
            bool parsed = Int32.TryParse(requestTelemetry.ResponseCode, out code);
            if (!parsed) return;
            if (code >= 400 && code < 500)
            {
                // If we set hello Success property, hello SDK won't change it:
                requestTelemetry.Success = true;
                // Allow us toofilter these requests in hello portal:
                requestTelemetry.Context.Properties["Overridden400s"] = "true";
            }
            // else leave hello SDK tooset hello Success property      
        }
      }
    }
```

<span data-ttu-id="66103-165">**De initialisatiefunctie laden**</span><span class="sxs-lookup"><span data-stu-id="66103-165">**Load your initializer**</span></span>

<span data-ttu-id="66103-166">In ApplicationInsights.config:</span><span class="sxs-lookup"><span data-stu-id="66103-166">In ApplicationInsights.config:</span></span>

    <ApplicationInsights>
      <TelemetryInitializers>
        <!-- Fully qualified type name, assembly name: -->
        <Add Type="MvcWebRole.Telemetry.MyTelemetryInitializer, MvcWebRole"/>
        ...
      </TelemetryInitializers>
    </ApplicationInsights>

<span data-ttu-id="66103-167">*U kunt ook* u Hallo initialisatiefunctie in code, bijvoorbeeld in Global.aspx.cs kunt instantiëren:</span><span class="sxs-lookup"><span data-stu-id="66103-167">*Alternatively,* you can instantiate hello initializer in code, for example in Global.aspx.cs:</span></span>

```C#
    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```


[<span data-ttu-id="66103-168">Zie voor meer informatie in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="66103-168">See more of this sample.</span></span>](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/MvcWebRole)

<a name="js-initializer"></a>

### <a name="javascript-telemetry-initializers"></a><span data-ttu-id="66103-169">JavaScript telemetrie initalisatiefuncties</span><span class="sxs-lookup"><span data-stu-id="66103-169">JavaScript telemetry initializers</span></span>
<span data-ttu-id="66103-170">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="66103-170">*JavaScript*</span></span>

<span data-ttu-id="66103-171">Voeg een initialisatiefunctie telemetrie direct na Hallo initialisatie van de code die u hebt verkregen via de portal Hallo:</span><span class="sxs-lookup"><span data-stu-id="66103-171">Insert a telemetry initializer immediately after hello initialization code that you got from hello portal:</span></span>

```JS

    <script type="text/javascript">
        // ... initialization code
        ...({
            instrumentationKey: "your instrumentation key"
        });
        window.appInsights = appInsights;


        // Adding telemetry initializer.
        // This is called whenever a new telemetry item
        // is created.

        appInsights.queue.push(function () {
            appInsights.context.addTelemetryInitializer(function (envelope) {
                var telemetryItem = envelope.data.baseData;

                // toocheck hello telemetry item’s type - for example PageView:
                if (envelope.name == Microsoft.ApplicationInsights.Telemetry.PageView.envelopeType) {
                    // this statement removes url from all page view documents
                    telemetryItem.url = "URL CENSORED";
                }

                // tooset custom properties:
                telemetryItem.properties = telemetryItem.properties || {};
                telemetryItem.properties["globalProperty"] = "boo";

                // tooset custom metrics:
                telemetryItem.measurements = telemetryItem.measurements || {};
                telemetryItem.measurements["globalMetric"] = 100;
            });
        });

        // End of inserted code.

        appInsights.trackPageView();
    </script>
```

<span data-ttu-id="66103-172">Zie voor een overzicht van Hallo niet aangepaste eigenschappen beschikbaar zijn op Hallo telemetryItem [Application Insights-exporteren gegevensmodel](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="66103-172">For a summary of hello non-custom properties available on hello telemetryItem, see [Application Insights Export Data Model](app-insights-export-data-model.md).</span></span>

<span data-ttu-id="66103-173">U kunt zoveel initalisatiefuncties als u wilt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="66103-173">You can add as many initializers as you like.</span></span>

## <a name="itelemetryprocessor-and-itelemetryinitializer"></a><span data-ttu-id="66103-174">ITelemetryProcessor en ITelemetryInitializer</span><span class="sxs-lookup"><span data-stu-id="66103-174">ITelemetryProcessor and ITelemetryInitializer</span></span>
<span data-ttu-id="66103-175">Wat is Hallo verschil tussen de telemetrie processors en telemetrie initalisatiefuncties?</span><span class="sxs-lookup"><span data-stu-id="66103-175">What's hello difference between telemetry processors and telemetry initializers?</span></span>

* <span data-ttu-id="66103-176">Er zijn enkele overlappingen in wat u ermee kunt doen: beide gebruikte tooadd eigenschappen tootelemetry kunnen zijn.</span><span class="sxs-lookup"><span data-stu-id="66103-176">There are some overlaps in what you can do with them: both can be used tooadd properties tootelemetry.</span></span>
* <span data-ttu-id="66103-177">TelemetryInitializers wordt altijd uitgevoerd voordat TelemetryProcessors.</span><span class="sxs-lookup"><span data-stu-id="66103-177">TelemetryInitializers always run before TelemetryProcessors.</span></span>
* <span data-ttu-id="66103-178">TelemetryProcessors kunt u toocompletely vervangen of een telemetrie-item te negeren.</span><span class="sxs-lookup"><span data-stu-id="66103-178">TelemetryProcessors allow you toocompletely replace or discard a telemetry item.</span></span>
* <span data-ttu-id="66103-179">TelemetryProcessors niet prestatietelemetrie prestatiemeteritem niet verwerken.</span><span class="sxs-lookup"><span data-stu-id="66103-179">TelemetryProcessors don't process performance counter telemetry.</span></span>


## <a name="reference-docs"></a><span data-ttu-id="66103-180">Referentiedocumenten</span><span class="sxs-lookup"><span data-stu-id="66103-180">Reference docs</span></span>
* [<span data-ttu-id="66103-181">API-overzicht</span><span class="sxs-lookup"><span data-stu-id="66103-181">API Overview</span></span>](app-insights-api-custom-events-metrics.md)
* [<span data-ttu-id="66103-182">ASP.NET-verwijzing</span><span class="sxs-lookup"><span data-stu-id="66103-182">ASP.NET reference</span></span>](https://msdn.microsoft.com/library/dn817570.aspx)

## <a name="sdk-code"></a><span data-ttu-id="66103-183">SDK-Code</span><span class="sxs-lookup"><span data-stu-id="66103-183">SDK Code</span></span>
* [<span data-ttu-id="66103-184">ASP.NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="66103-184">ASP.NET Core SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [<span data-ttu-id="66103-185">ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="66103-185">ASP.NET 5</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [<span data-ttu-id="66103-186">JavaScript SDK</span><span class="sxs-lookup"><span data-stu-id="66103-186">JavaScript SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-JS)

## <span data-ttu-id="66103-187"><a name="next"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="66103-187"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="66103-188">Zoekopdracht gebeurtenissen en Logboeken</span><span class="sxs-lookup"><span data-stu-id="66103-188">Search events and logs</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="66103-189">Steekproeven</span><span class="sxs-lookup"><span data-stu-id="66103-189">Sampling</span></span>](app-insights-sampling.md)
* [<span data-ttu-id="66103-190">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="66103-190">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)
