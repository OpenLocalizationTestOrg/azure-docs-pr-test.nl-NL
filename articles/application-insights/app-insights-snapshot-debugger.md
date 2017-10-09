---
title: aaaAzure Application Insights momentopname foutopsporingsprogramma voor .NET-toepassingen | Microsoft Docs
description: Fouten opsporen in momentopnamen worden automatisch verzameld wanneer uitzonderingen worden veroorzaakt in productie .NET-toepassingen
services: application-insights
documentationcenter: 
author: qubitron
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: bwren
ms.openlocfilehash: f0173a752b5795d934fbab1bd53eb077433edc90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="debug-snapshots-on-exceptions-in-net-apps"></a><span data-ttu-id="f1979-103">Fouten opsporen in momentopnamen op uitzonderingen in .NET-toepassingen</span><span class="sxs-lookup"><span data-stu-id="f1979-103">Debug snapshots on exceptions in .NET apps</span></span>

<span data-ttu-id="f1979-104">Wanneer er een uitzondering optreedt, kunt u automatisch een debug-momentopname verzamelen van uw live-webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="f1979-104">When an exception occurs, you can automatically collect a debug snapshot from your live web application.</span></span> <span data-ttu-id="f1979-105">Hallo momentopname toont Hallo status van de broncode en variabelen op Hallo momenteel Hallo uitzondering is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="f1979-105">hello snapshot shows hello state of source code and variables at hello moment hello exception was thrown.</span></span> <span data-ttu-id="f1979-106">Hallo momentopname foutopsporingsprogramma (preview) in [Azure Application Insights](app-insights-overview.md) uitzonderingstelemetrie van uw web-app wordt bewaakt.</span><span class="sxs-lookup"><span data-stu-id="f1979-106">hello Snapshot Debugger (preview) in [Azure Application Insights](app-insights-overview.md) monitors exception telemetry from your web app.</span></span> <span data-ttu-id="f1979-107">Deze verzamelt momentopnamen op uw eerste ArgumentOutOfRangeException uitzonderingen zodat u Hallo-informatie die u toodiagnose problemen in productie nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="f1979-107">It collects snapshots on your top-throwing exceptions so that you have hello information you need toodiagnose issues in production.</span></span> <span data-ttu-id="f1979-108">Hallo omvatten [momentopname collector NuGet-pakket](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) in uw toepassing, en desgewenst verzameling parameters in configureren [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Momentopnamen worden weergegeven op [uitzonderingen](app-insights-asp-net-exceptions.md) in Hallo Application Insights-portal.</span><span class="sxs-lookup"><span data-stu-id="f1979-108">Include hello [Snapshot collector NuGet package](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) in your application, and optionally configure collection parameters in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Snapshots appear on [exceptions](app-insights-asp-net-exceptions.md) in hello Application Insights portal.</span></span>

<span data-ttu-id="f1979-109">U kunt momentopnamen voor foutopsporing weergeven in Hallo portal toosee Hallo aanroepstack en variabelen op elke aanroepstackframe controleren.</span><span class="sxs-lookup"><span data-stu-id="f1979-109">You can view debug snapshots in hello portal toosee hello call stack and inspect variables at each call stack frame.</span></span> <span data-ttu-id="f1979-110">een krachtigere foutopsporing ervaring met broncode, open momentopnamen met Visual Studio 2017 Enterprise door tooget [Hallo momentopname Debugger-extensie voor Visual Studio downloaden](https://aka.ms/snapshotdebugger).</span><span class="sxs-lookup"><span data-stu-id="f1979-110">tooget a more powerful debugging experience with source code, open snapshots with Visual Studio 2017 Enterprise by [downloading hello Snapshot Debugger extension for Visual Studio](https://aka.ms/snapshotdebugger).</span></span>

<span data-ttu-id="f1979-111">Verzameling van de momentopname is beschikbaar voor:</span><span class="sxs-lookup"><span data-stu-id="f1979-111">Snapshot collection is available for:</span></span>
* <span data-ttu-id="f1979-112">.NET framework en ASP.NET-toepassingen met .NET Framework 4.5 of hoger.</span><span class="sxs-lookup"><span data-stu-id="f1979-112">.NET Framework and ASP.NET applications running .NET Framework 4.5 or later.</span></span>
* <span data-ttu-id="f1979-113">.NET core 2.0 en ASP.NET Core 2.0-toepassingen worden uitgevoerd op Windows.</span><span class="sxs-lookup"><span data-stu-id="f1979-113">.NET Core 2.0 and ASP.NET Core 2.0 applications running on Windows.</span></span>

### <a name="configure-snapshot-collection-for-aspnet-applications"></a><span data-ttu-id="f1979-114">Momentopname verzamelen voor ASP.NET-toepassingen configureren</span><span class="sxs-lookup"><span data-stu-id="f1979-114">Configure snapshot collection for ASP.NET applications</span></span>

1. <span data-ttu-id="f1979-115">[Application Insights inschakelen in uw web-app](app-insights-asp-net.md), als u dit nog niet hebt gedaan.</span><span class="sxs-lookup"><span data-stu-id="f1979-115">[Enable Application Insights in your web app](app-insights-asp-net.md), if you haven't done it yet.</span></span>

2. <span data-ttu-id="f1979-116">Hallo omvatten [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet-pakket in uw app.</span><span class="sxs-lookup"><span data-stu-id="f1979-116">Include hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span> 

3. <span data-ttu-id="f1979-117">Hallo standaardopties die Hallo pakket toegevoegd te bekijken[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="f1979-117">Review hello default options that hello package added too[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span>

    ```xml
    <TelemetryProcessors>
        <Add Type="Microsoft.ApplicationInsights.SnapshotCollector.SnapshotCollectorTelemetryProcessor, Microsoft.ApplicationInsights.SnapshotCollector">
        <!-- hello default is true, but you can disable Snapshot Debugging by setting it toofalse -->
        <IsEnabled>true</IsEnabled>
        <!-- Snapshot Debugging is usually disabled in developer mode, but you can enable it by setting this tootrue. -->
        <!-- DeveloperMode is a property on hello active TelemetryChannel. -->
        <IsEnabledInDeveloperMode>false</IsEnabledInDeveloperMode>
        <!-- How many times we need toosee an exception before we ask for snapshots. -->
        <ThresholdForSnapshotting>5</ThresholdForSnapshotting>
        <!-- hello maximum number of examples we create for a single problem. -->
        <MaximumSnapshotsRequired>3</MaximumSnapshotsRequired>
        <!-- hello maximum number of problems that we can be tracking at any time. -->
        <MaximumCollectionPlanSize>50</MaximumCollectionPlanSize>
        <!-- How often tooreset problem counters. -->
        <ProblemCounterResetInterval>06:00:00</ProblemCounterResetInterval>
        <!-- hello maximum number of snapshots allowed in one minute. -->
        <SnapshotsPerMinuteLimit>2</SnapshotsPerMinuteLimit>
        <!-- hello maximum number of snapshots allowed per day. -->
        <SnapshotsPerDayLimit>50</SnapshotsPerDayLimit>
        </Add>
    </TelemetryProcessors>
    ```

4. <span data-ttu-id="f1979-118">Momentopnamen worden verzameld alleen op uitzonderingen die gemeld tooApplication Insights worden.</span><span class="sxs-lookup"><span data-stu-id="f1979-118">Snapshots are collected only on exceptions that are reported tooApplication Insights.</span></span> <span data-ttu-id="f1979-119">In sommige gevallen (bijvoorbeeld oudere versies van .NET-platform Hallo), moet u wellicht te[uitzondering verzamelen configureren](app-insights-asp-net-exceptions.md#exceptions) toosee uitzonderingen met momentopnamen in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="f1979-119">In some cases (for example, older versions of hello .NET platform), you might need too[configure exception collection](app-insights-asp-net-exceptions.md#exceptions) toosee exceptions with snapshots in hello portal.</span></span>


### <a name="configure-snapshot-collection-for-aspnet-core-20-applications"></a><span data-ttu-id="f1979-120">Momentopname verzamelen voor ASP.NET Core 2.0-toepassingen configureren</span><span class="sxs-lookup"><span data-stu-id="f1979-120">Configure snapshot collection for ASP.NET Core 2.0 applications</span></span>

1. <span data-ttu-id="f1979-121">[Application Insights inschakelen in uw web-app van ASP.NET Core](app-insights-asp-net-core.md), als u dit nog niet hebt gedaan.</span><span class="sxs-lookup"><span data-stu-id="f1979-121">[Enable Application Insights in your ASP.NET Core web app](app-insights-asp-net-core.md), if you haven't done it yet.</span></span>

2. <span data-ttu-id="f1979-122">Hallo omvatten [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet-pakket in uw app.</span><span class="sxs-lookup"><span data-stu-id="f1979-122">Include hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span>

3. <span data-ttu-id="f1979-123">Hallo wijzigen `ConfigureServices` methode in uw toepassing `Startup` tooadd Hallo momentopname van Collector telemetrie processor klasse.</span><span class="sxs-lookup"><span data-stu-id="f1979-123">Modify hello `ConfigureServices` method in your application's `Startup` class tooadd hello Snapshot Collector's telemetry processor.</span></span> <span data-ttu-id="f1979-124">Hallo-code die moet worden toegevoegd, is afhankelijk van Hallo waarnaar wordt verwezen versie Hallo Microsoft.ApplicationInsights.ASPNETCore NuGet-pakket.</span><span class="sxs-lookup"><span data-stu-id="f1979-124">hello code you should add depends on hello referenced version of hello Microsoft.ApplicationInsights.ASPNETCore NuGet package.</span></span>

   <span data-ttu-id="f1979-125">Voeg voor Microsoft.ApplicationInsights.AspNetCore 2.1.0 toe:</span><span class="sxs-lookup"><span data-stu-id="f1979-125">For Microsoft.ApplicationInsights.AspNetCore 2.1.0 add:</span></span>
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       // This method is called by hello runtime. Use it tooadd services toohello container.
       public void ConfigureServices(IServiceCollection services)
       {
           services.AddSingleton<Func<ITelemetryProcessor, ITelemetryProcessor>>(next => new SnapshotCollectorTelemetryProcessor(next));
           // TODO: Add any other services your application needs here.
       }
   }
   ```

   <span data-ttu-id="f1979-126">Voeg voor Microsoft.ApplicationInsights.AspNetCore 2.1.1 toe:</span><span class="sxs-lookup"><span data-stu-id="f1979-126">For Microsoft.ApplicationInsights.AspNetCore 2.1.1 add:</span></span>
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       private class SnapshotCollectorTelemetryProcessorFactory : ITelemetryProcessorFactory
       {
           public ITelemetryProcessor Create(ITelemetryProcessor next) =>
               new SnapshotCollectorTelemetryProcessor(next);
       }

       // This method is called by hello runtime. Use it tooadd services toohello container.
       public void ConfigureServices(IServiceCollection services)
       {
            services.AddSingleton<ITelemetryProcessorFactory>(new SnapshotCollectorTelemetryProcessorFactory());
           // TODO: Add any other services your application needs here.
       }
   }
   ```

### <a name="configure-snapshot-collection-for-other-net-applications"></a><span data-ttu-id="f1979-127">Momentopname verzamelen voor andere .NET-toepassingen configureren</span><span class="sxs-lookup"><span data-stu-id="f1979-127">Configure snapshot collection for other .NET applications</span></span>

1. <span data-ttu-id="f1979-128">Als uw toepassing is niet al zijn geïnstrumenteerd met Application Insights, aan de slag door [inschakelen van Application Insights en instelling Hallo instrumentatiesleutel](app-insights-windows-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="f1979-128">If your application is not already instrumented with Application Insights, get started by [enabling Application Insights and setting hello instrumentation key](app-insights-windows-desktop.md).</span></span>

2. <span data-ttu-id="f1979-129">Hallo toevoegen [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet-pakket in uw app.</span><span class="sxs-lookup"><span data-stu-id="f1979-129">Add hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span>

3. <span data-ttu-id="f1979-130">Momentopnamen worden verzameld alleen op uitzonderingen die gemeld tooApplication Insights worden.</span><span class="sxs-lookup"><span data-stu-id="f1979-130">Snapshots are collected only on exceptions that are reported tooApplication Insights.</span></span> <span data-ttu-id="f1979-131">Mogelijk moet u toomodify uw code tooreport ze.</span><span class="sxs-lookup"><span data-stu-id="f1979-131">You may need toomodify your code tooreport them.</span></span> <span data-ttu-id="f1979-132">Hallo uitzonderingsverwerking-code is afhankelijk van Hallo-structuur van uw toepassing, maar een voorbeeld lager is dan:</span><span class="sxs-lookup"><span data-stu-id="f1979-132">hello exception handling code depends on hello structure of your application, but an example is below:</span></span>
    ```C#
   TelemetryClient _telemetryClient = new TelemetryClient();

   void ExampleRequest()
   {
        try
        {
            // TODO: Handle hello request.
        }
        catch (Exception ex)
        {
            // Report hello exception tooApplication Insights.
            _telemetryClient.TrackException(ex);

            // TODO: Rethrow hello exception if desired.
        }
   }
    ```
    
## <a name="grant-permissions"></a><span data-ttu-id="f1979-133">Machtigingen toekennen</span><span class="sxs-lookup"><span data-stu-id="f1979-133">Grant permissions</span></span>

<span data-ttu-id="f1979-134">Eigenaren van hello Azure-abonnement kunnen inspecteren momentopnamen.</span><span class="sxs-lookup"><span data-stu-id="f1979-134">Owners of hello Azure subscription can inspect snapshots.</span></span> <span data-ttu-id="f1979-135">Andere gebruikers moet machtiging worden verleend door een eigenaar.</span><span class="sxs-lookup"><span data-stu-id="f1979-135">Other users must be granted permission by an owner.</span></span>

<span data-ttu-id="f1979-136">toogrant machtiging toewijzen Hallo `Application Insights Snapshot Debugger` rol toousers die momentopnamen inspecteert.</span><span class="sxs-lookup"><span data-stu-id="f1979-136">toogrant permission, assign hello `Application Insights Snapshot Debugger` role toousers who will inspect snapshots.</span></span> <span data-ttu-id="f1979-137">Deze rol kan worden toegewezen tooindividual gebruikers of groepen door abonnementseigenaren voor Hallo doel Application Insights-resource of de resourcegroep of abonnement.</span><span class="sxs-lookup"><span data-stu-id="f1979-137">This role can be assigned tooindividual users or groups by subscription owners for hello target Application Insights resource or its resource group or subscription.</span></span>

1. <span data-ttu-id="f1979-138">Hallo Access Control (IAM) blade geopend.</span><span class="sxs-lookup"><span data-stu-id="f1979-138">Open hello Access Control (IAM) blade.</span></span>
1. <span data-ttu-id="f1979-139">Klik op Hallo + knop toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f1979-139">Click hello +Add button.</span></span>
1. <span data-ttu-id="f1979-140">Selecteer Application Insights momentopname foutopsporingsprogramma van Hallo rollen vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="f1979-140">Select Application Insights Snapshot Debugger from hello Roles drop-down list.</span></span>
1. <span data-ttu-id="f1979-141">Zoeken en geef een naam voor Hallo gebruiker tooadd.</span><span class="sxs-lookup"><span data-stu-id="f1979-141">Search for and enter a name for hello user tooadd.</span></span>
1. <span data-ttu-id="f1979-142">Klik op Hallo opslaan knop tooadd hello toohello gebruikersrol.</span><span class="sxs-lookup"><span data-stu-id="f1979-142">Click hello Save button tooadd hello user toohello role.</span></span>


[!IMPORTANT]
    <span data-ttu-id="f1979-143">Momentopnamen kunnen mogelijk persoonlijke en andere gevoelige gegevens in waarden van variabelen en parameter bevatten.</span><span class="sxs-lookup"><span data-stu-id="f1979-143">Snapshots can potentially contain personal and other sensitive information in variable and parameter values.</span></span>

## <a name="debug-snapshots-in-hello-application-insights-portal"></a><span data-ttu-id="f1979-144">Fouten opsporen in momentopnamen in Hallo Application Insights-portal</span><span class="sxs-lookup"><span data-stu-id="f1979-144">Debug snapshots in hello Application Insights portal</span></span>

<span data-ttu-id="f1979-145">Als een momentopname beschikbaar voor een bepaalde uitzondering of een probleem-ID is, een **fouten opsporen in momentopname openen** knop wordt weergegeven op Hallo [uitzondering](app-insights-asp-net-exceptions.md) in Hallo Application Insights-portal.</span><span class="sxs-lookup"><span data-stu-id="f1979-145">If a snapshot is available for a given exception or a problem ID, an **Open Debug Snapshot** button appears on hello [exception](app-insights-asp-net-exceptions.md) in hello Application Insights portal.</span></span>

![De knop openen fouten opsporen in momentopname op uitzondering](./media/app-insights-snapshot-debugger/snapshot-on-exception.png)

<span data-ttu-id="f1979-147">In de weergave fouten opsporen in momentopname hello ziet u een aanroepstack en een deelvenster Variabelen.</span><span class="sxs-lookup"><span data-stu-id="f1979-147">In hello Debug Snapshot view, you see a call stack and a variables pane.</span></span> <span data-ttu-id="f1979-148">Wanneer u selecteert frames van Hallo aanroep op Hallo call stack deelvenster geplaatst, kunt u lokale variabelen weergeven en parameters voor die functie-aanroep in Hallo variabelen deelvenster.</span><span class="sxs-lookup"><span data-stu-id="f1979-148">When you select frames of hello call stack in hello call stack pane, you can view local variables and parameters for that function call in hello variables pane.</span></span>

![Weergave fouten opsporen in momentopname in Hallo-portal](./media/app-insights-snapshot-debugger/open-snapshot-portal.png)

<span data-ttu-id="f1979-150">Momentopnamen kunnen gevoelige gegevens bevatten, en ze zijn standaard niet zichtbaar.</span><span class="sxs-lookup"><span data-stu-id="f1979-150">Snapshots might contain sensitive information, and by default they are not viewable.</span></span> <span data-ttu-id="f1979-151">tooview momentopnamen, moet u Hallo hebben `Application Insights Snapshot Debugger` tooyou rol die is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="f1979-151">tooview snapshots, you must have hello `Application Insights Snapshot Debugger` role assigned tooyou.</span></span>

## <a name="debug-snapshots-with-visual-studio-2017-enterprise"></a><span data-ttu-id="f1979-152">Fouten opsporen in momentopnamen met Visual Studio 2017 Enterprise</span><span class="sxs-lookup"><span data-stu-id="f1979-152">Debug snapshots with Visual Studio 2017 Enterprise</span></span>
1. <span data-ttu-id="f1979-153">Klik op Hallo **momentopname downloaden** knop toodownload een `.diagsession` bestand, dat kan worden geopend door Visual Studio 2017 Enterprise.</span><span class="sxs-lookup"><span data-stu-id="f1979-153">Click hello **Download Snapshot** button toodownload a `.diagsession` file, which can be opened by Visual Studio 2017 Enterprise.</span></span> 

2. <span data-ttu-id="f1979-154">Hallo tooopen `.diagsession` -bestand, moet u eerst [downloaden en installeren van Hallo momentopname Debugger-extensie voor Visual Studio](https://aka.ms/snapshotdebugger).</span><span class="sxs-lookup"><span data-stu-id="f1979-154">tooopen hello `.diagsession` file, you must first [download and install hello Snapshot Debugger extension for Visual Studio](https://aka.ms/snapshotdebugger).</span></span>

3. <span data-ttu-id="f1979-155">Nadat u Hallo momentopnamebestand opent, Hallo Minidump foutopsporing pagina in Visual Studio geopend.</span><span class="sxs-lookup"><span data-stu-id="f1979-155">After you open hello snapshot file, hello Minidump Debugging page in Visual Studio appears.</span></span> <span data-ttu-id="f1979-156">Klik op **fouten opsporen in beheerde Code** toostart Hallo momentopname foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="f1979-156">Click **Debug Managed Code** toostart debugging hello snapshot.</span></span> <span data-ttu-id="f1979-157">Hallo momentopname wordt geopend toohello coderegel waar Hallo uitzondering is opgetreden, zodat u fouten Hallo huidige status van het Hallo-proces opsporen kunt.</span><span class="sxs-lookup"><span data-stu-id="f1979-157">hello snapshot opens toohello line of code where hello exception was thrown so that you can debug hello current state of hello process.</span></span>

    ![Weergave foutopsporing momentopname in Visual Studio](./media/app-insights-snapshot-debugger/open-snapshot-visualstudio.png)

<span data-ttu-id="f1979-159">Hallo gedownloade momentopname bevat symboolbestanden die zijn gevonden op de webserver van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="f1979-159">hello downloaded snapshot contains any symbol files that were found on your web application server.</span></span> <span data-ttu-id="f1979-160">Deze symboolbestanden zijn vereiste tooassociate momentopnamegegevens met broncode.</span><span class="sxs-lookup"><span data-stu-id="f1979-160">These symbol files are required tooassociate snapshot data with source code.</span></span> <span data-ttu-id="f1979-161">Voor App Service-apps, zorg ervoor dat tooenable symbool implementatie wanneer u uw web-apps publiceren.</span><span class="sxs-lookup"><span data-stu-id="f1979-161">For App Service apps, make sure tooenable symbol deployment when you publish your web apps.</span></span>

## <a name="how-snapshots-work"></a><span data-ttu-id="f1979-162">De werking van momentopnamen</span><span class="sxs-lookup"><span data-stu-id="f1979-162">How snapshots work</span></span>

<span data-ttu-id="f1979-163">Wanneer uw toepassing wordt gestart, moet op een afzonderlijke momentopname uploader proces dat uw toepassing voor aanvragen van de momentopname bewaakt wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f1979-163">When your application starts, a separate snapshot uploader process is created that monitors your application for snapshot requests.</span></span> <span data-ttu-id="f1979-164">Wanneer een momentopname wordt aangevraagd, wordt een schaduwkopie van Hallo process uitgevoerd aangebracht in ongeveer 10 too20 minuten.</span><span class="sxs-lookup"><span data-stu-id="f1979-164">When a snapshot is requested, a shadow copy of hello running process is made in about 10 too20 minutes.</span></span> <span data-ttu-id="f1979-165">Hallo shadow proces vervolgens wordt geanalyseerd en een momentopname wordt gemaakt terwijl de Hallo hoofdproces nog steeds toorun en verkeer toousers fungeren.</span><span class="sxs-lookup"><span data-stu-id="f1979-165">hello shadow process is then analyzed, and a snapshot is created while hello main process continues toorun and serve traffic toousers.</span></span> <span data-ttu-id="f1979-166">Hallo momentopname is vervolgens geüploade tooApplication Insights samen met eventuele relevante (.pdb)-symboolbestanden die zijn vereist tooview Hallo momentopname.</span><span class="sxs-lookup"><span data-stu-id="f1979-166">hello snapshot is then uploaded tooApplication Insights along with any relevant symbol (.pdb) files that are needed tooview hello snapshot.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="f1979-167">Huidige beperkingen</span><span class="sxs-lookup"><span data-stu-id="f1979-167">Current limitations</span></span>

### <a name="publish-symbols"></a><span data-ttu-id="f1979-168">Symbolen publiceren</span><span class="sxs-lookup"><span data-stu-id="f1979-168">Publish symbols</span></span>
<span data-ttu-id="f1979-169">Hallo momentopname foutopsporingsprogramma vereist symboolbestanden op Hallo productie-toodecode servervariabelen en tooprovide een foutopsporing ervaring in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f1979-169">hello Snapshot Debugger requires symbol files on hello production server toodecode variables and tooprovide a debugging experience in Visual Studio.</span></span> <span data-ttu-id="f1979-170">Hallo 15.2 versie van Visual Studio 2017 publiceert symbolen voor release builds standaard, wanneer het tooApp Service publiceert.</span><span class="sxs-lookup"><span data-stu-id="f1979-170">hello 15.2 release of Visual Studio 2017 publishes symbols for release builds by default when it publishes tooApp Service.</span></span> <span data-ttu-id="f1979-171">In eerdere versies, moet u tooadd Hallo volgende regel tooyour publicatieprofiel `.pubxml` zodat symbolen zijn gepubliceerd in de releasemodus bestand:</span><span class="sxs-lookup"><span data-stu-id="f1979-171">In prior versions, you need tooadd hello following line tooyour publish profile `.pubxml` file so that symbols are published in release mode:</span></span>

```xml
    <ExcludeGeneratedDebugSymbol>False</ExcludeGeneratedDebugSymbol>
```

<span data-ttu-id="f1979-172">Voor Azure Compute en andere typen ervoor te zorgen dat de symboolbestanden Hallo Hallo dezelfde map van Hallo hoofdtoepassing .dll (meestal `wwwroot/bin`) of op het huidige pad Hallo beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="f1979-172">For Azure Compute and other types, ensure that hello symbol files are in hello same folder of hello main application .dll (typically, `wwwroot/bin`) or are available on hello current path.</span></span>

### <a name="optimized-builds"></a><span data-ttu-id="f1979-173">Geoptimaliseerde builds</span><span class="sxs-lookup"><span data-stu-id="f1979-173">Optimized builds</span></span>
<span data-ttu-id="f1979-174">In sommige gevallen kunnen geen lokale variabelen worden weergegeven in de release builds vanwege optimalisaties die worden toegepast tijdens het maken van een Hallo.</span><span class="sxs-lookup"><span data-stu-id="f1979-174">In some cases, local variables cannot be viewed in release builds because of optimizations that are applied during hello build process.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="f1979-175">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="f1979-175">Troubleshooting</span></span>

<span data-ttu-id="f1979-176">De volgende tips helpen u problemen oplossen met Hallo momentopname foutopsporingsprogramma.</span><span class="sxs-lookup"><span data-stu-id="f1979-176">These tips help you troubleshoot problems with hello Snapshot Debugger.</span></span>

### <a name="verify-hello-instrumentation-key"></a><span data-ttu-id="f1979-177">Controleer of de instrumentatiesleutel Hallo</span><span class="sxs-lookup"><span data-stu-id="f1979-177">Verify hello instrumentation key</span></span>

<span data-ttu-id="f1979-178">Zorg ervoor dat u de juiste instrumentatiesleutel Hallo in uw gepubliceerde toepassing.</span><span class="sxs-lookup"><span data-stu-id="f1979-178">Make sure that you're using hello correct instrumentation key in your published application.</span></span> <span data-ttu-id="f1979-179">Application Insights leest meestal Hallo instrumentatiesleutel van Hallo ApplicationInsights.config-bestand.</span><span class="sxs-lookup"><span data-stu-id="f1979-179">Usually, Application Insights reads hello instrumentation key from hello ApplicationInsights.config file.</span></span> <span data-ttu-id="f1979-180">Controleer of dat Hallo waarde dezelfde is Hallo als Hallo instrumentatiesleutel voor Hallo Application Insights-resource dat u in Hallo-portal ziet.</span><span class="sxs-lookup"><span data-stu-id="f1979-180">Verify that hello value is hello same as hello instrumentation key for hello Application Insights resource that you see in hello portal.</span></span>

### <a name="check-hello-uploader-logs"></a><span data-ttu-id="f1979-181">Hallo uploader logboeken controleren</span><span class="sxs-lookup"><span data-stu-id="f1979-181">Check hello uploader logs</span></span>

<span data-ttu-id="f1979-182">Nadat een momentopname is gemaakt, wordt een bestand met Mini-geheugendump (dmp) op schijf gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f1979-182">After a snapshot is created, a minidump file (.dmp) is created on disk.</span></span> <span data-ttu-id="f1979-183">Een afzonderlijke uploader proces duurt dat minidump-bestand en uploadt, samen met eventuele bijbehorende-PDB-bestanden, tooApplication Insights momentopname foutopsporingsprogramma opslag.</span><span class="sxs-lookup"><span data-stu-id="f1979-183">A separate uploader process takes that minidump file and uploads it, along with any associated PDBs, tooApplication Insights Snapshot Debugger storage.</span></span> <span data-ttu-id="f1979-184">Nadat het Hallo minidump heeft geüpload, wordt deze verwijderd van de schijf.</span><span class="sxs-lookup"><span data-stu-id="f1979-184">After hello minidump has uploaded successfully, it is deleted from disk.</span></span> <span data-ttu-id="f1979-185">Hallo-logboekbestanden voor Hallo minidump uploader worden bewaard op de schijf.</span><span class="sxs-lookup"><span data-stu-id="f1979-185">hello log files for hello minidump uploader are retained on disk.</span></span> <span data-ttu-id="f1979-186">In een App Service-omgeving vindt u deze logboeken in `D:\Home\LogFiles\Uploader_*.log`.</span><span class="sxs-lookup"><span data-stu-id="f1979-186">In an App Service environment, you can find these logs in `D:\Home\LogFiles\Uploader_*.log`.</span></span> <span data-ttu-id="f1979-187">Gebruik Hallo Kudu management site voor App Service-toofind deze logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="f1979-187">Use hello Kudu management site for App Service toofind these log files.</span></span>

1. <span data-ttu-id="f1979-188">Open uw App Service-toepassing hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f1979-188">Open your App Service application in hello Azure portal.</span></span>

2. <span data-ttu-id="f1979-189">Selecteer Hallo **geavanceerde hulpmiddelen** blade of zoeken naar **Kudu**.</span><span class="sxs-lookup"><span data-stu-id="f1979-189">Select hello **Advanced Tools** blade, or search for **Kudu**.</span></span>
3. <span data-ttu-id="f1979-190">Klik op **gaat**.</span><span class="sxs-lookup"><span data-stu-id="f1979-190">Click **Go**.</span></span>
4. <span data-ttu-id="f1979-191">In Hallo **-console voor foutopsporing** vervolgkeuzelijst de optie **CMD**.</span><span class="sxs-lookup"><span data-stu-id="f1979-191">In hello **Debug console** drop-down list box, select **CMD**.</span></span>
5. <span data-ttu-id="f1979-192">Klik op **logboekbestanden**.</span><span class="sxs-lookup"><span data-stu-id="f1979-192">Click **LogFiles**.</span></span>

<span data-ttu-id="f1979-193">Er is ten minste één bestand met een naam die met begint `Uploader_` en een `.log` extensie.</span><span class="sxs-lookup"><span data-stu-id="f1979-193">You should see at least one file with a name that begins with `Uploader_` and a `.log` extension.</span></span> <span data-ttu-id="f1979-194">Klik op Hallo juiste pictogram toodownload alle logboekbestanden of in een browser openen.</span><span class="sxs-lookup"><span data-stu-id="f1979-194">Click hello appropriate icon toodownload any log files or open them in a browser.</span></span>
<span data-ttu-id="f1979-195">Hallo-bestandsnaam bevat Hallo machine-naam.</span><span class="sxs-lookup"><span data-stu-id="f1979-195">hello file name includes hello machine name.</span></span> <span data-ttu-id="f1979-196">Als uw App Service-exemplaar wordt gehost op meer dan één computer, moet u er aparte logboekbestanden voor elke computer zijn.</span><span class="sxs-lookup"><span data-stu-id="f1979-196">If your App Service instance is hosted on more than one machine, there are separate log files for each machine.</span></span> <span data-ttu-id="f1979-197">Wanneer Hallo uploader een nieuw minidump-bestand detecteert, vastgelegd in het logboekbestand Hallo.</span><span class="sxs-lookup"><span data-stu-id="f1979-197">When hello uploader detects a new minidump file, it is recorded in hello log file.</span></span> <span data-ttu-id="f1979-198">Hier volgt een voorbeeld van een geslaagde upload:</span><span class="sxs-lookup"><span data-stu-id="f1979-198">Here's an example of a successful upload:</span></span>

```
MinidumpUploader.exe Information: 0 : Dump available 139e411a23934dc0b9ea08a626db16c5.dmp
    DateTime=2017-05-25T14:25:08.0349846Z
MinidumpUploader.exe Information: 0 : Uploading D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp, 329.12 MB
    DateTime=2017-05-25T14:25:16.0145444Z
MinidumpUploader.exe Information: 0 : Upload successful.
    DateTime=2017-05-25T14:25:42.9164120Z
MinidumpUploader.exe Information: 0 : Extracting PDB info from D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp.
    DateTime=2017-05-25T14:25:42.9164120Z
MinidumpUploader.exe Information: 0 : Matched 2 PDB(s) with local files.
    DateTime=2017-05-25T14:25:44.2310982Z
MinidumpUploader.exe Information: 0 : Stamp does not want any of our matched PDBs.
    DateTime=2017-05-25T14:25:44.5435948Z
MinidumpUploader.exe Information: 0 : Deleted D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp
    DateTime=2017-05-25T14:25:44.6095821Z
```

<span data-ttu-id="f1979-199">In het vorige voorbeeld Hallo Hallo instrumentatiesleutel is `c12a605e73c44346a984e00000000000`.</span><span class="sxs-lookup"><span data-stu-id="f1979-199">In hello previous example, hello instrumentation key is `c12a605e73c44346a984e00000000000`.</span></span> <span data-ttu-id="f1979-200">Deze waarde moet overeenkomen met de instrumentatiesleutel Hallo voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="f1979-200">This value should match hello instrumentation key for your application.</span></span>
<span data-ttu-id="f1979-201">Hallo minidump is gekoppeld aan een momentopname met de ID Hallo `139e411a23934dc0b9ea08a626db16c5`.</span><span class="sxs-lookup"><span data-stu-id="f1979-201">hello minidump is associated with a snapshot with hello ID `139e411a23934dc0b9ea08a626db16c5`.</span></span> <span data-ttu-id="f1979-202">U kunt deze ID hoger toolocate Hallo uitzonderingstelemetrie in Application Insights Analytics die is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="f1979-202">You can use this ID later toolocate hello associated exception telemetry in Application Insights Analytics.</span></span>

<span data-ttu-id="f1979-203">Hallo uploader scant op nieuwe-PDB-bestanden over om de 15 minuten.</span><span class="sxs-lookup"><span data-stu-id="f1979-203">hello uploader scans for new PDBs about once every 15 minutes.</span></span> <span data-ttu-id="f1979-204">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f1979-204">Here's an example:</span></span>

```
MinidumpUploader.exe Information: 0 : PDB rescan requested.
    DateTime=2017-05-25T15:11:38.8003886Z
MinidumpUploader.exe Information: 0 : Scanning D:\home\site\wwwroot\ for local PDBs.
    DateTime=2017-05-25T15:11:38.8003886Z
MinidumpUploader.exe Information: 0 : Scanning D:\local\Temporary ASP.NET Files\root\a6554c94\e3ad6f22\assembly\dl3\81d5008b\00b93cc8_dec5d201 for local PDBs.
    DateTime=2017-05-25T15:11:38.8160276Z
MinidumpUploader.exe Information: 0 : Local PDB scan complete. Found 2 PDB(s).
    DateTime=2017-05-25T15:11:38.8316450Z
MinidumpUploader.exe Information: 0 : Deleted PDB scan marker D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\.pdbscan.
    DateTime=2017-05-25T15:11:38.8316450Z
```

<span data-ttu-id="f1979-205">Voor toepassingen die zijn _niet_ Hallo uploader logboeken worden gehost in App Service, in Hallo dezelfde map als Hallo minidumps: `%TEMP%\Dumps\<ikey>` (waarbij `<ikey>` is uw instrumentatiesleutel).</span><span class="sxs-lookup"><span data-stu-id="f1979-205">For applications that are _not_ hosted in App Service, hello uploader logs are in hello same folder as hello minidumps: `%TEMP%\Dumps\<ikey>` (where `<ikey>` is your instrumentation key).</span></span>

### <a name="use-application-insights-search-toofind-exceptions-with-snapshots"></a><span data-ttu-id="f1979-206">Gebruik Application Insights zoeken toofind uitzonderingen met momentopnamen</span><span class="sxs-lookup"><span data-stu-id="f1979-206">Use Application Insights search toofind exceptions with snapshots</span></span>

<span data-ttu-id="f1979-207">Wanneer een momentopname wordt gemaakt, is er uitzondering is opgetreden Hallo gecodeerd met een momentopname-ID.</span><span class="sxs-lookup"><span data-stu-id="f1979-207">When a snapshot is created, hello throwing exception is tagged with a snapshot ID.</span></span> <span data-ttu-id="f1979-208">Wanneer Hallo-uitzonderingstelemetrie gemelde tooApplication inzichten, is die momentopname-ID opgenomen als een aangepaste eigenschap.</span><span class="sxs-lookup"><span data-stu-id="f1979-208">When hello exception telemetry is reported tooApplication Insights, that snapshot ID is included as a custom property.</span></span> <span data-ttu-id="f1979-209">Hallo Search-blade met in Application Insights kunt u alle telemetrie Hello vinden `ai.snapshot.id` aangepaste eigenschap.</span><span class="sxs-lookup"><span data-stu-id="f1979-209">Using hello Search blade in Application Insights, you can find all telemetry with hello `ai.snapshot.id` custom property.</span></span>

1. <span data-ttu-id="f1979-210">Blader tooyour Application Insights-resource in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f1979-210">Browse tooyour Application Insights resource in hello Azure portal.</span></span>
2. <span data-ttu-id="f1979-211">Klik op **Search**.</span><span class="sxs-lookup"><span data-stu-id="f1979-211">Click **Search**.</span></span>
3. <span data-ttu-id="f1979-212">Type `ai.snapshot.id` in Hallo zoekvak en druk op Enter.</span><span class="sxs-lookup"><span data-stu-id="f1979-212">Type `ai.snapshot.id` in hello Search text box and press Enter.</span></span>

![Zoeken naar telemetrie met een momentopname-ID in Hallo-portal](./media/app-insights-snapshot-debugger/search-snapshot-portal.png)

<span data-ttu-id="f1979-214">Als deze zoekopdracht geen resultaten oplevert, zijn er zijn geen momentopnamen gemelde tooApplication inzichten voor uw toepassing in het tijdsbereik Hallo geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="f1979-214">If this search returns no results, then no snapshots were reported tooApplication Insights for your application in hello selected time range.</span></span>

<span data-ttu-id="f1979-215">die ID toosearch voor een specifieke momentopname-ID van Hallo Uploader Logboeken, typ in het zoekvak Hallo.</span><span class="sxs-lookup"><span data-stu-id="f1979-215">toosearch for a specific snapshot ID from hello Uploader logs, type that ID in hello Search box.</span></span> <span data-ttu-id="f1979-216">Als u geen telemetrie voor een momentopname waarvan u weet dat is geüpload vinden, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="f1979-216">If you can't find telemetry for a snapshot that you know was uploaded, follow these steps:</span></span>

1. <span data-ttu-id="f1979-217">Controleer dat u hello rechts Application Insights-resource bekijkt door Hallo instrumentatiesleutel te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="f1979-217">Double-check that you're looking at hello right Application Insights resource by verifying hello instrumentation key.</span></span>

2. <span data-ttu-id="f1979-218">Met tijdstempel Hallo uit Hallo Uploader logboek, aanpassen Hallo tijdsbereik filter van Hallo zoeken toocover die tijdsbereik.</span><span class="sxs-lookup"><span data-stu-id="f1979-218">Using hello timestamp from hello Uploader log, adjust hello Time Range filter of hello search toocover that time range.</span></span>

<span data-ttu-id="f1979-219">Als u een uitzondering met die ID momentopname niet ziet, niet-uitzonderingstelemetrie Hallo gemelde tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="f1979-219">If you still don't see an exception with that snapshot ID, then hello exception telemetry wasn't reported tooApplication Insights.</span></span> <span data-ttu-id="f1979-220">Deze situatie kan zich voordoen als uw toepassing is vastgelopen na het heeft geduurd Hallo momentopname maar voordat het Hallo-uitzonderingstelemetrie gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="f1979-220">This situation can happen if your application crashed after it took hello snapshot but before it reported hello exception telemetry.</span></span> <span data-ttu-id="f1979-221">In dit geval controleren Hallo App Service-Logboeken onder `Diagnose and solve problems` toosee als er onverwacht opnieuw wordt opgestart of onverwerkte uitzonderingen.</span><span class="sxs-lookup"><span data-stu-id="f1979-221">In this case, check hello App Service logs under `Diagnose and solve problems` toosee if there were unexpected restarts or unhandled exceptions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f1979-222">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f1979-222">Next steps</span></span>

* <span data-ttu-id="f1979-223">[Snappoints instellen in uw code](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/) tooget momentopnamen zonder te wachten op een uitzondering.</span><span class="sxs-lookup"><span data-stu-id="f1979-223">[Set snappoints in your code](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/) tooget snapshots without waiting for an exception.</span></span>
* <span data-ttu-id="f1979-224">[Diagnose van uitzonderingen in uw web-apps](app-insights-asp-net-exceptions.md) wordt uitgelegd hoe toomake meer uitzonderingen zichtbaar tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="f1979-224">[Diagnose exceptions in your web apps](app-insights-asp-net-exceptions.md) explains how toomake more exceptions visible tooApplication Insights.</span></span> 
* <span data-ttu-id="f1979-225">[Detectie van smartcard](app-insights-proactive-diagnostics.md) detecteert automatisch afwijkingen.</span><span class="sxs-lookup"><span data-stu-id="f1979-225">[Smart Detection](app-insights-proactive-diagnostics.md) automatically discovers performance anomalies.</span></span>
