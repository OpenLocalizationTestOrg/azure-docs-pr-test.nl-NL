---
title: Azure Application Insights foutopsporingsprogramma momentopname voor de .NET-toepassingen | Microsoft Docs
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
ms.openlocfilehash: 56eba2ff7af228b3c44354ad43b384288b4e1972
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="debug-snapshots-on-exceptions-in-net-apps"></a><span data-ttu-id="66eb4-103">Fouten opsporen in momentopnamen op uitzonderingen in .NET-toepassingen</span><span class="sxs-lookup"><span data-stu-id="66eb4-103">Debug snapshots on exceptions in .NET apps</span></span>

<span data-ttu-id="66eb4-104">Wanneer er een uitzondering optreedt, kunt u automatisch een debug-momentopname verzamelen van uw live-webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="66eb4-104">When an exception occurs, you can automatically collect a debug snapshot from your live web application.</span></span> <span data-ttu-id="66eb4-105">De momentopname toont de status van de broncode en variabelen op het moment dat de uitzondering is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="66eb4-105">The snapshot shows the state of source code and variables at the moment the exception was thrown.</span></span> <span data-ttu-id="66eb4-106">De momentopname-foutopsporing (preview) in [Azure Application Insights](app-insights-overview.md) uitzonderingstelemetrie van uw web-app wordt bewaakt.</span><span class="sxs-lookup"><span data-stu-id="66eb4-106">The Snapshot Debugger (preview) in [Azure Application Insights](app-insights-overview.md) monitors exception telemetry from your web app.</span></span> <span data-ttu-id="66eb4-107">Deze verzamelt momentopnamen op uw eerste ArgumentOutOfRangeException uitzonderingen zodat u de informatie die u nodig hebt voor het vaststellen van problemen in productie hebt.</span><span class="sxs-lookup"><span data-stu-id="66eb4-107">It collects snapshots on your top-throwing exceptions so that you have the information you need to diagnose issues in production.</span></span> <span data-ttu-id="66eb4-108">Bevatten de [momentopname collector NuGet-pakket](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) in uw toepassing, en desgewenst verzameling parameters in configureren [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Momentopnamen worden weergegeven op [uitzonderingen](app-insights-asp-net-exceptions.md) in de Application Insights-portal.</span><span class="sxs-lookup"><span data-stu-id="66eb4-108">Include the [Snapshot collector NuGet package](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) in your application, and optionally configure collection parameters in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Snapshots appear on [exceptions](app-insights-asp-net-exceptions.md) in the Application Insights portal.</span></span>

<span data-ttu-id="66eb4-109">U kunt momentopnamen foutopsporing weergeven in de portal om te zien van de aanroep stapelen en variabelen op elke aanroepstackframe controleren.</span><span class="sxs-lookup"><span data-stu-id="66eb4-109">You can view debug snapshots in the portal to see the call stack and inspect variables at each call stack frame.</span></span> <span data-ttu-id="66eb4-110">Als u een krachtigere foutopsporing ervaring met broncode, opent u momentopnamen met Visual Studio 2017 Enterprise door [downloaden van de momentopname Debugger-extensie voor Visual Studio](https://aka.ms/snapshotdebugger).</span><span class="sxs-lookup"><span data-stu-id="66eb4-110">To get a more powerful debugging experience with source code, open snapshots with Visual Studio 2017 Enterprise by [downloading the Snapshot Debugger extension for Visual Studio](https://aka.ms/snapshotdebugger).</span></span>

<span data-ttu-id="66eb4-111">Verzameling van de momentopname is beschikbaar voor:</span><span class="sxs-lookup"><span data-stu-id="66eb4-111">Snapshot collection is available for:</span></span>
* <span data-ttu-id="66eb4-112">.NET framework en ASP.NET-toepassingen met .NET Framework 4.5 of hoger.</span><span class="sxs-lookup"><span data-stu-id="66eb4-112">.NET Framework and ASP.NET applications running .NET Framework 4.5 or later.</span></span>
* <span data-ttu-id="66eb4-113">.NET core 2.0 en ASP.NET Core 2.0-toepassingen worden uitgevoerd op Windows.</span><span class="sxs-lookup"><span data-stu-id="66eb4-113">.NET Core 2.0 and ASP.NET Core 2.0 applications running on Windows.</span></span>

### <a name="configure-snapshot-collection-for-aspnet-applications"></a><span data-ttu-id="66eb4-114">Momentopname verzamelen voor ASP.NET-toepassingen configureren</span><span class="sxs-lookup"><span data-stu-id="66eb4-114">Configure snapshot collection for ASP.NET applications</span></span>

1. <span data-ttu-id="66eb4-115">[Application Insights inschakelen in uw web-app](app-insights-asp-net.md), als u dit nog niet hebt gedaan.</span><span class="sxs-lookup"><span data-stu-id="66eb4-115">[Enable Application Insights in your web app](app-insights-asp-net.md), if you haven't done it yet.</span></span>

2. <span data-ttu-id="66eb4-116">Bevatten de [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet-pakket in uw app.</span><span class="sxs-lookup"><span data-stu-id="66eb4-116">Include the [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span> 

3. <span data-ttu-id="66eb4-117">Bekijk de standaardopties te gebruiken die het pakket worden toegevoegd aan [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="66eb4-117">Review the default options that the package added to [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span>

    ```xml
    <TelemetryProcessors>
        <Add Type="Microsoft.ApplicationInsights.SnapshotCollector.SnapshotCollectorTelemetryProcessor, Microsoft.ApplicationInsights.SnapshotCollector">
        <!-- The default is true, but you can disable Snapshot Debugging by setting it to false -->
        <IsEnabled>true</IsEnabled>
        <!-- Snapshot Debugging is usually disabled in developer mode, but you can enable it by setting this to true. -->
        <!-- DeveloperMode is a property on the active TelemetryChannel. -->
        <IsEnabledInDeveloperMode>false</IsEnabledInDeveloperMode>
        <!-- How many times we need to see an exception before we ask for snapshots. -->
        <ThresholdForSnapshotting>5</ThresholdForSnapshotting>
        <!-- The maximum number of examples we create for a single problem. -->
        <MaximumSnapshotsRequired>3</MaximumSnapshotsRequired>
        <!-- The maximum number of problems that we can be tracking at any time. -->
        <MaximumCollectionPlanSize>50</MaximumCollectionPlanSize>
        <!-- How often to reset problem counters. -->
        <ProblemCounterResetInterval>06:00:00</ProblemCounterResetInterval>
        <!-- The maximum number of snapshots allowed in one minute. -->
        <SnapshotsPerMinuteLimit>2</SnapshotsPerMinuteLimit>
        <!-- The maximum number of snapshots allowed per day. -->
        <SnapshotsPerDayLimit>50</SnapshotsPerDayLimit>
        </Add>
    </TelemetryProcessors>
    ```

4. <span data-ttu-id="66eb4-118">Momentopnamen worden verzameld alleen op uitzonderingen die worden gerapporteerd aan de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="66eb4-118">Snapshots are collected only on exceptions that are reported to Application Insights.</span></span> <span data-ttu-id="66eb4-119">In sommige gevallen (bijvoorbeeld oudere versies van het .NET-platform), moet u mogelijk [uitzondering verzamelen configureren](app-insights-asp-net-exceptions.md#exceptions) om uitzonderingen met momentopnamen in de portal te bekijken.</span><span class="sxs-lookup"><span data-stu-id="66eb4-119">In some cases (for example, older versions of the .NET platform), you might need to [configure exception collection](app-insights-asp-net-exceptions.md#exceptions) to see exceptions with snapshots in the portal.</span></span>


### <a name="configure-snapshot-collection-for-aspnet-core-20-applications"></a><span data-ttu-id="66eb4-120">Momentopname verzamelen voor ASP.NET Core 2.0-toepassingen configureren</span><span class="sxs-lookup"><span data-stu-id="66eb4-120">Configure snapshot collection for ASP.NET Core 2.0 applications</span></span>

1. <span data-ttu-id="66eb4-121">[Application Insights inschakelen in uw web-app van ASP.NET Core](app-insights-asp-net-core.md), als u dit nog niet hebt gedaan.</span><span class="sxs-lookup"><span data-stu-id="66eb4-121">[Enable Application Insights in your ASP.NET Core web app](app-insights-asp-net-core.md), if you haven't done it yet.</span></span>

2. <span data-ttu-id="66eb4-122">Bevatten de [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet-pakket in uw app.</span><span class="sxs-lookup"><span data-stu-id="66eb4-122">Include the [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span>

3. <span data-ttu-id="66eb4-123">Wijzig de `ConfigureServices` methode in uw toepassing `Startup` toe te voegen van de momentopname-Collector telemetrie processor klasse.</span><span class="sxs-lookup"><span data-stu-id="66eb4-123">Modify the `ConfigureServices` method in your application's `Startup` class to add the Snapshot Collector's telemetry processor.</span></span> <span data-ttu-id="66eb4-124">De code die toe te voegen, is afhankelijk van de waarnaar wordt verwezen versie van het Microsoft.ApplicationInsights.ASPNETCore NuGet-pakket.</span><span class="sxs-lookup"><span data-stu-id="66eb4-124">The code you should add depends on the referenced version of the Microsoft.ApplicationInsights.ASPNETCore NuGet package.</span></span>

   <span data-ttu-id="66eb4-125">Voeg voor Microsoft.ApplicationInsights.AspNetCore 2.1.0 toe:</span><span class="sxs-lookup"><span data-stu-id="66eb4-125">For Microsoft.ApplicationInsights.AspNetCore 2.1.0 add:</span></span>
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       // This method is called by the runtime. Use it to add services to the container.
       public void ConfigureServices(IServiceCollection services)
       {
           services.AddSingleton<Func<ITelemetryProcessor, ITelemetryProcessor>>(next => new SnapshotCollectorTelemetryProcessor(next));
           // TODO: Add any other services your application needs here.
       }
   }
   ```

   <span data-ttu-id="66eb4-126">Voeg voor Microsoft.ApplicationInsights.AspNetCore 2.1.1 toe:</span><span class="sxs-lookup"><span data-stu-id="66eb4-126">For Microsoft.ApplicationInsights.AspNetCore 2.1.1 add:</span></span>
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

       // This method is called by the runtime. Use it to add services to the container.
       public void ConfigureServices(IServiceCollection services)
       {
            services.AddSingleton<ITelemetryProcessorFactory>(new SnapshotCollectorTelemetryProcessorFactory());
           // TODO: Add any other services your application needs here.
       }
   }
   ```

### <a name="configure-snapshot-collection-for-other-net-applications"></a><span data-ttu-id="66eb4-127">Momentopname verzamelen voor andere .NET-toepassingen configureren</span><span class="sxs-lookup"><span data-stu-id="66eb4-127">Configure snapshot collection for other .NET applications</span></span>

1. <span data-ttu-id="66eb4-128">Als uw toepassing is niet al zijn geïnstrumenteerd met Application Insights, aan de slag door [Application Insights inschakelen en instellen van de instrumentatiesleutel](app-insights-windows-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="66eb4-128">If your application is not already instrumented with Application Insights, get started by [enabling Application Insights and setting the instrumentation key](app-insights-windows-desktop.md).</span></span>

2. <span data-ttu-id="66eb4-129">Voeg de [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet-pakket in uw app.</span><span class="sxs-lookup"><span data-stu-id="66eb4-129">Add the [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span>

3. <span data-ttu-id="66eb4-130">Momentopnamen worden verzameld alleen op uitzonderingen die worden gerapporteerd aan de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="66eb4-130">Snapshots are collected only on exceptions that are reported to Application Insights.</span></span> <span data-ttu-id="66eb4-131">U wilt wijzigen van uw code om te rapporteren.</span><span class="sxs-lookup"><span data-stu-id="66eb4-131">You may need to modify your code to report them.</span></span> <span data-ttu-id="66eb4-132">De verwerking van de code van uitzonderingen, is afhankelijk van de structuur van uw toepassing, maar een voorbeeld lager is dan:</span><span class="sxs-lookup"><span data-stu-id="66eb4-132">The exception handling code depends on the structure of your application, but an example is below:</span></span>
    ```C#
   TelemetryClient _telemetryClient = new TelemetryClient();

   void ExampleRequest()
   {
        try
        {
            // TODO: Handle the request.
        }
        catch (Exception ex)
        {
            // Report the exception to Application Insights.
            _telemetryClient.TrackException(ex);

            // TODO: Rethrow the exception if desired.
        }
   }
    ```
    
## <a name="grant-permissions"></a><span data-ttu-id="66eb4-133">Machtigingen toekennen</span><span class="sxs-lookup"><span data-stu-id="66eb4-133">Grant permissions</span></span>

<span data-ttu-id="66eb4-134">Eigenaars van het Azure-abonnement kunnen inspecteren momentopnamen.</span><span class="sxs-lookup"><span data-stu-id="66eb4-134">Owners of the Azure subscription can inspect snapshots.</span></span> <span data-ttu-id="66eb4-135">Andere gebruikers moet machtiging worden verleend door een eigenaar.</span><span class="sxs-lookup"><span data-stu-id="66eb4-135">Other users must be granted permission by an owner.</span></span>

<span data-ttu-id="66eb4-136">Als u wilt machtigen, wijzen de `Application Insights Snapshot Debugger` rol aan gebruikers die momentopnamen inspecteert.</span><span class="sxs-lookup"><span data-stu-id="66eb4-136">To grant permission, assign the `Application Insights Snapshot Debugger` role to users who will inspect snapshots.</span></span> <span data-ttu-id="66eb4-137">Deze rol kan worden toegewezen aan individuele gebruikers of groepen door abonnementseigenaren voor de Application Insights-resource van het doel of de resourcegroep of abonnement.</span><span class="sxs-lookup"><span data-stu-id="66eb4-137">This role can be assigned to individual users or groups by subscription owners for the target Application Insights resource or its resource group or subscription.</span></span>

1. <span data-ttu-id="66eb4-138">Open de blade Access Control (IAM).</span><span class="sxs-lookup"><span data-stu-id="66eb4-138">Open the Access Control (IAM) blade.</span></span>
1. <span data-ttu-id="66eb4-139">Klik op de knop toevoegen +.</span><span class="sxs-lookup"><span data-stu-id="66eb4-139">Click the +Add button.</span></span>
1. <span data-ttu-id="66eb4-140">Selecteer Application Insights momentopname foutopsporingsprogramma in de vervolgkeuzelijst rollen.</span><span class="sxs-lookup"><span data-stu-id="66eb4-140">Select Application Insights Snapshot Debugger from the Roles drop-down list.</span></span>
1. <span data-ttu-id="66eb4-141">Zoeken en geef een naam voor de gebruiker toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="66eb4-141">Search for and enter a name for the user to add.</span></span>
1. <span data-ttu-id="66eb4-142">Klik op de knop Opslaan om de gebruiker toevoegen aan de rol.</span><span class="sxs-lookup"><span data-stu-id="66eb4-142">Click the Save button to add the user to the role.</span></span>


[!IMPORTANT]
    <span data-ttu-id="66eb4-143">Momentopnamen kunnen mogelijk persoonlijke en andere gevoelige gegevens in waarden van variabelen en parameter bevatten.</span><span class="sxs-lookup"><span data-stu-id="66eb4-143">Snapshots can potentially contain personal and other sensitive information in variable and parameter values.</span></span>

## <a name="debug-snapshots-in-the-application-insights-portal"></a><span data-ttu-id="66eb4-144">Fouten opsporen in momentopnamen in de Application Insights-portal</span><span class="sxs-lookup"><span data-stu-id="66eb4-144">Debug snapshots in the Application Insights portal</span></span>

<span data-ttu-id="66eb4-145">Als een momentopname beschikbaar voor een bepaalde uitzondering of een probleem-ID is, een **fouten opsporen in momentopname openen** knop wordt weergegeven op de [uitzondering](app-insights-asp-net-exceptions.md) in de Application Insights-portal.</span><span class="sxs-lookup"><span data-stu-id="66eb4-145">If a snapshot is available for a given exception or a problem ID, an **Open Debug Snapshot** button appears on the [exception](app-insights-asp-net-exceptions.md) in the Application Insights portal.</span></span>

![De knop openen fouten opsporen in momentopname op uitzondering](./media/app-insights-snapshot-debugger/snapshot-on-exception.png)

<span data-ttu-id="66eb4-147">In de weergave fouten opsporen in momentopname ziet u een aanroepstack en een deelvenster Variabelen.</span><span class="sxs-lookup"><span data-stu-id="66eb4-147">In the Debug Snapshot view, you see a call stack and a variables pane.</span></span> <span data-ttu-id="66eb4-148">Wanneer u frames aanroepstack in het deelvenster van de stack aanroep selecteert, kunt u lokale variabelen weergeven en parameters voor die functie-aanroep in het deelvenster Variabelen.</span><span class="sxs-lookup"><span data-stu-id="66eb4-148">When you select frames of the call stack in the call stack pane, you can view local variables and parameters for that function call in the variables pane.</span></span>

![Weergave fouten opsporen in momentopname in de portal](./media/app-insights-snapshot-debugger/open-snapshot-portal.png)

<span data-ttu-id="66eb4-150">Momentopnamen kunnen gevoelige gegevens bevatten, en ze zijn standaard niet zichtbaar.</span><span class="sxs-lookup"><span data-stu-id="66eb4-150">Snapshots might contain sensitive information, and by default they are not viewable.</span></span> <span data-ttu-id="66eb4-151">Momentopnamen kunnen weergeven, hebt u de `Application Insights Snapshot Debugger` rol aan u toegewezen.</span><span class="sxs-lookup"><span data-stu-id="66eb4-151">To view snapshots, you must have the `Application Insights Snapshot Debugger` role assigned to you.</span></span>

## <a name="debug-snapshots-with-visual-studio-2017-enterprise"></a><span data-ttu-id="66eb4-152">Fouten opsporen in momentopnamen met Visual Studio 2017 Enterprise</span><span class="sxs-lookup"><span data-stu-id="66eb4-152">Debug snapshots with Visual Studio 2017 Enterprise</span></span>
1. <span data-ttu-id="66eb4-153">Klik op de **momentopname downloaden** knop voor het downloaden van een `.diagsession` bestand, dat kan worden geopend door Visual Studio 2017 Enterprise.</span><span class="sxs-lookup"><span data-stu-id="66eb4-153">Click the **Download Snapshot** button to download a `.diagsession` file, which can be opened by Visual Studio 2017 Enterprise.</span></span> 

2. <span data-ttu-id="66eb4-154">Openen van de `.diagsession` -bestand, moet u eerst [downloaden en installeren van de momentopname Debugger-extensie voor Visual Studio](https://aka.ms/snapshotdebugger).</span><span class="sxs-lookup"><span data-stu-id="66eb4-154">To open the `.diagsession` file, you must first [download and install the Snapshot Debugger extension for Visual Studio](https://aka.ms/snapshotdebugger).</span></span>

3. <span data-ttu-id="66eb4-155">Nadat u de momentopnamebestand opent, verschijnt de pagina met Mini-geheugendump foutopsporing in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="66eb4-155">After you open the snapshot file, the Minidump Debugging page in Visual Studio appears.</span></span> <span data-ttu-id="66eb4-156">Klik op **fouten opsporen in beheerde Code** momentopname van de foutopsporing te starten.</span><span class="sxs-lookup"><span data-stu-id="66eb4-156">Click **Debug Managed Code** to start debugging the snapshot.</span></span> <span data-ttu-id="66eb4-157">De momentopname is geopend met de coderegel waar de uitzondering is opgetreden, zodat u fouten in de huidige status van het proces opsporen kunt.</span><span class="sxs-lookup"><span data-stu-id="66eb4-157">The snapshot opens to the line of code where the exception was thrown so that you can debug the current state of the process.</span></span>

    ![Weergave foutopsporing momentopname in Visual Studio](./media/app-insights-snapshot-debugger/open-snapshot-visualstudio.png)

<span data-ttu-id="66eb4-159">De gedownloade momentopname bevat symboolbestanden die zijn gevonden op de webserver van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="66eb4-159">The downloaded snapshot contains any symbol files that were found on your web application server.</span></span> <span data-ttu-id="66eb4-160">Deze symboolbestanden zijn om momentopnamegegevens te koppelen met broncode vereist.</span><span class="sxs-lookup"><span data-stu-id="66eb4-160">These symbol files are required to associate snapshot data with source code.</span></span> <span data-ttu-id="66eb4-161">Zorg dat u de implementatie van het symbool in te schakelen wanneer u uw web-apps publiceren voor App Service-apps.</span><span class="sxs-lookup"><span data-stu-id="66eb4-161">For App Service apps, make sure to enable symbol deployment when you publish your web apps.</span></span>

## <a name="how-snapshots-work"></a><span data-ttu-id="66eb4-162">De werking van momentopnamen</span><span class="sxs-lookup"><span data-stu-id="66eb4-162">How snapshots work</span></span>

<span data-ttu-id="66eb4-163">Wanneer uw toepassing wordt gestart, moet op een afzonderlijke momentopname uploader proces dat uw toepassing voor aanvragen van de momentopname bewaakt wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="66eb4-163">When your application starts, a separate snapshot uploader process is created that monitors your application for snapshot requests.</span></span> <span data-ttu-id="66eb4-164">Wanneer een momentopname wordt aangevraagd, wordt een schaduwkopie van het actieve proces aangebracht in ongeveer 10 tot 20 minuten.</span><span class="sxs-lookup"><span data-stu-id="66eb4-164">When a snapshot is requested, a shadow copy of the running process is made in about 10 to 20 minutes.</span></span> <span data-ttu-id="66eb4-165">Het proces van de schaduw wordt vervolgens geanalyseerd en een momentopname wordt gemaakt terwijl het hoofdproces nog steeds worden uitgevoerd en verkeer leveren aan gebruikers.</span><span class="sxs-lookup"><span data-stu-id="66eb4-165">The shadow process is then analyzed, and a snapshot is created while the main process continues to run and serve traffic to users.</span></span> <span data-ttu-id="66eb4-166">De momentopname wordt vervolgens geüpload naar Application Insights samen met eventuele relevante (.pdb)-symboolbestanden die nodig zijn om de momentopname weer te geven.</span><span class="sxs-lookup"><span data-stu-id="66eb4-166">The snapshot is then uploaded to Application Insights along with any relevant symbol (.pdb) files that are needed to view the snapshot.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="66eb4-167">Huidige beperkingen</span><span class="sxs-lookup"><span data-stu-id="66eb4-167">Current limitations</span></span>

### <a name="publish-symbols"></a><span data-ttu-id="66eb4-168">Symbolen publiceren</span><span class="sxs-lookup"><span data-stu-id="66eb4-168">Publish symbols</span></span>
<span data-ttu-id="66eb4-169">Het foutopsporingsprogramma momentopname vereist symboolbestanden op de productieserver variabelen decoderen en om een foutopsporing ervaring in Visual Studio te bieden.</span><span class="sxs-lookup"><span data-stu-id="66eb4-169">The Snapshot Debugger requires symbol files on the production server to decode variables and to provide a debugging experience in Visual Studio.</span></span> <span data-ttu-id="66eb4-170">De 15.2 versie van Visual Studio 2017 publiceert symbolen voor release builds standaard wanneer deze wordt gepubliceerd naar App Service.</span><span class="sxs-lookup"><span data-stu-id="66eb4-170">The 15.2 release of Visual Studio 2017 publishes symbols for release builds by default when it publishes to App Service.</span></span> <span data-ttu-id="66eb4-171">In eerdere versies, moet u de volgende regel toevoegen aan uw publicatieprofiel `.pubxml` zodat symbolen zijn gepubliceerd in de releasemodus bestand:</span><span class="sxs-lookup"><span data-stu-id="66eb4-171">In prior versions, you need to add the following line to your publish profile `.pubxml` file so that symbols are published in release mode:</span></span>

```xml
    <ExcludeGeneratedDebugSymbol>False</ExcludeGeneratedDebugSymbol>
```

<span data-ttu-id="66eb4-172">Voor Azure Compute en andere typen, zorg ervoor dat de symboolbestanden in dezelfde map van de hoofdtoepassing .dll (meestal `wwwroot/bin`) of zijn beschikbaar op het huidige pad.</span><span class="sxs-lookup"><span data-stu-id="66eb4-172">For Azure Compute and other types, ensure that the symbol files are in the same folder of the main application .dll (typically, `wwwroot/bin`) or are available on the current path.</span></span>

### <a name="optimized-builds"></a><span data-ttu-id="66eb4-173">Geoptimaliseerde builds</span><span class="sxs-lookup"><span data-stu-id="66eb4-173">Optimized builds</span></span>
<span data-ttu-id="66eb4-174">In sommige gevallen kunnen niet lokale variabelen worden weergegeven in de release builds vanwege optimalisaties die worden toegepast tijdens het maken.</span><span class="sxs-lookup"><span data-stu-id="66eb4-174">In some cases, local variables cannot be viewed in release builds because of optimizations that are applied during the build process.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="66eb4-175">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="66eb4-175">Troubleshooting</span></span>

<span data-ttu-id="66eb4-176">De volgende tips helpen u problemen oplossen met de momentopname-foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="66eb4-176">These tips help you troubleshoot problems with the Snapshot Debugger.</span></span>

### <a name="verify-the-instrumentation-key"></a><span data-ttu-id="66eb4-177">Controleer of de instrumentatiesleutel</span><span class="sxs-lookup"><span data-stu-id="66eb4-177">Verify the instrumentation key</span></span>

<span data-ttu-id="66eb4-178">Zorg ervoor dat u de juiste instrumentatiesleutel in uw gepubliceerde toepassing.</span><span class="sxs-lookup"><span data-stu-id="66eb4-178">Make sure that you're using the correct instrumentation key in your published application.</span></span> <span data-ttu-id="66eb4-179">Application Insights wordt normaal gesproken de instrumentatiesleutel gelezen uit het bestand ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="66eb4-179">Usually, Application Insights reads the instrumentation key from the ApplicationInsights.config file.</span></span> <span data-ttu-id="66eb4-180">Controleer of de waarde is hetzelfde als de instrumentatiesleutel voor de Application Insights-resource die u in de portal ziet.</span><span class="sxs-lookup"><span data-stu-id="66eb4-180">Verify that the value is the same as the instrumentation key for the Application Insights resource that you see in the portal.</span></span>

### <a name="check-the-uploader-logs"></a><span data-ttu-id="66eb4-181">Raadpleeg de logboeken uploader</span><span class="sxs-lookup"><span data-stu-id="66eb4-181">Check the uploader logs</span></span>

<span data-ttu-id="66eb4-182">Nadat een momentopname is gemaakt, wordt een bestand met Mini-geheugendump (dmp) op schijf gemaakt.</span><span class="sxs-lookup"><span data-stu-id="66eb4-182">After a snapshot is created, a minidump file (.dmp) is created on disk.</span></span> <span data-ttu-id="66eb4-183">Een afzonderlijke uploader proces duurt dat minidump-bestand en uploadt, samen met eventuele bijbehorende-PDB-bestanden naar Application Insights momentopname foutopsporingsprogramma opslag.</span><span class="sxs-lookup"><span data-stu-id="66eb4-183">A separate uploader process takes that minidump file and uploads it, along with any associated PDBs, to Application Insights Snapshot Debugger storage.</span></span> <span data-ttu-id="66eb4-184">Nadat de minidump heeft geüpload, wordt deze verwijderd van de schijf.</span><span class="sxs-lookup"><span data-stu-id="66eb4-184">After the minidump has uploaded successfully, it is deleted from disk.</span></span> <span data-ttu-id="66eb4-185">De logboekbestanden voor de uploader minidump worden bewaard op de schijf.</span><span class="sxs-lookup"><span data-stu-id="66eb4-185">The log files for the minidump uploader are retained on disk.</span></span> <span data-ttu-id="66eb4-186">In een App Service-omgeving vindt u deze logboeken in `D:\Home\LogFiles\Uploader_*.log`.</span><span class="sxs-lookup"><span data-stu-id="66eb4-186">In an App Service environment, you can find these logs in `D:\Home\LogFiles\Uploader_*.log`.</span></span> <span data-ttu-id="66eb4-187">Met de site voor het beheer van Kudu voor App Service kunt u deze logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="66eb4-187">Use the Kudu management site for App Service to find these log files.</span></span>

1. <span data-ttu-id="66eb4-188">Open uw App Service-toepassing in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="66eb4-188">Open your App Service application in the Azure portal.</span></span>

2. <span data-ttu-id="66eb4-189">Selecteer de **geavanceerde hulpmiddelen** blade of zoeken naar **Kudu**.</span><span class="sxs-lookup"><span data-stu-id="66eb4-189">Select the **Advanced Tools** blade, or search for **Kudu**.</span></span>
3. <span data-ttu-id="66eb4-190">Klik op **gaat**.</span><span class="sxs-lookup"><span data-stu-id="66eb4-190">Click **Go**.</span></span>
4. <span data-ttu-id="66eb4-191">In de **-console voor foutopsporing** vervolgkeuzelijst de optie **CMD**.</span><span class="sxs-lookup"><span data-stu-id="66eb4-191">In the **Debug console** drop-down list box, select **CMD**.</span></span>
5. <span data-ttu-id="66eb4-192">Klik op **logboekbestanden**.</span><span class="sxs-lookup"><span data-stu-id="66eb4-192">Click **LogFiles**.</span></span>

<span data-ttu-id="66eb4-193">Er is ten minste één bestand met een naam die met begint `Uploader_` en een `.log` extensie.</span><span class="sxs-lookup"><span data-stu-id="66eb4-193">You should see at least one file with a name that begins with `Uploader_` and a `.log` extension.</span></span> <span data-ttu-id="66eb4-194">Klik op het juiste pictogram om te downloaden van alle logboekbestanden of in een browser openen.</span><span class="sxs-lookup"><span data-stu-id="66eb4-194">Click the appropriate icon to download any log files or open them in a browser.</span></span>
<span data-ttu-id="66eb4-195">De bestandsnaam bevat de naam van de machine.</span><span class="sxs-lookup"><span data-stu-id="66eb4-195">The file name includes the machine name.</span></span> <span data-ttu-id="66eb4-196">Als uw App Service-exemplaar wordt gehost op meer dan één computer, moet u er aparte logboekbestanden voor elke computer zijn.</span><span class="sxs-lookup"><span data-stu-id="66eb4-196">If your App Service instance is hosted on more than one machine, there are separate log files for each machine.</span></span> <span data-ttu-id="66eb4-197">Wanneer de uploader een nieuw minidump-bestand detecteert, wordt deze vastgelegd in het logboekbestand.</span><span class="sxs-lookup"><span data-stu-id="66eb4-197">When the uploader detects a new minidump file, it is recorded in the log file.</span></span> <span data-ttu-id="66eb4-198">Hier volgt een voorbeeld van een geslaagde upload:</span><span class="sxs-lookup"><span data-stu-id="66eb4-198">Here's an example of a successful upload:</span></span>

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

<span data-ttu-id="66eb4-199">In het vorige voorbeeld de instrumentatiesleutel wordt `c12a605e73c44346a984e00000000000`.</span><span class="sxs-lookup"><span data-stu-id="66eb4-199">In the previous example, the instrumentation key is `c12a605e73c44346a984e00000000000`.</span></span> <span data-ttu-id="66eb4-200">Deze waarde moet overeenkomen met de instrumentatiesleutel voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="66eb4-200">This value should match the instrumentation key for your application.</span></span>
<span data-ttu-id="66eb4-201">De minidump is gekoppeld aan een momentopname met de ID `139e411a23934dc0b9ea08a626db16c5`.</span><span class="sxs-lookup"><span data-stu-id="66eb4-201">The minidump is associated with a snapshot with the ID `139e411a23934dc0b9ea08a626db16c5`.</span></span> <span data-ttu-id="66eb4-202">U kunt deze ID later te vinden van de bijbehorende uitzonderingstelemetrie in Application Insights Analytics gebruiken.</span><span class="sxs-lookup"><span data-stu-id="66eb4-202">You can use this ID later to locate the associated exception telemetry in Application Insights Analytics.</span></span>

<span data-ttu-id="66eb4-203">De uploader scant op nieuwe-PDB-bestanden over om de 15 minuten.</span><span class="sxs-lookup"><span data-stu-id="66eb4-203">The uploader scans for new PDBs about once every 15 minutes.</span></span> <span data-ttu-id="66eb4-204">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="66eb4-204">Here's an example:</span></span>

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

<span data-ttu-id="66eb4-205">Voor toepassingen die zijn _niet_ gehost in App Service, de uploader-logboeken zijn in dezelfde map als de minidumps: `%TEMP%\Dumps\<ikey>` (waarbij `<ikey>` is uw instrumentatiesleutel).</span><span class="sxs-lookup"><span data-stu-id="66eb4-205">For applications that are _not_ hosted in App Service, the uploader logs are in the same folder as the minidumps: `%TEMP%\Dumps\<ikey>` (where `<ikey>` is your instrumentation key).</span></span>

### <a name="use-application-insights-search-to-find-exceptions-with-snapshots"></a><span data-ttu-id="66eb4-206">Gebruik Application Insights zoeken uitzonderingen met momentopnamen</span><span class="sxs-lookup"><span data-stu-id="66eb4-206">Use Application Insights search to find exceptions with snapshots</span></span>

<span data-ttu-id="66eb4-207">Wanneer een momentopname wordt gemaakt, is de activerend uitzondering gemarkeerd met een momentopname-ID.</span><span class="sxs-lookup"><span data-stu-id="66eb4-207">When a snapshot is created, the throwing exception is tagged with a snapshot ID.</span></span> <span data-ttu-id="66eb4-208">Wanneer de uitzonderingstelemetrie wordt gemeld naar Application Insights dat momentopname-ID is opgenomen als een aangepaste eigenschap.</span><span class="sxs-lookup"><span data-stu-id="66eb4-208">When the exception telemetry is reported to Application Insights, that snapshot ID is included as a custom property.</span></span> <span data-ttu-id="66eb4-209">Met de Search-blade in Application Insights en u vindt alle telemetrie met de `ai.snapshot.id` aangepaste eigenschap.</span><span class="sxs-lookup"><span data-stu-id="66eb4-209">Using the Search blade in Application Insights, you can find all telemetry with the `ai.snapshot.id` custom property.</span></span>

1. <span data-ttu-id="66eb4-210">Blader naar uw Application Insights-resource in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="66eb4-210">Browse to your Application Insights resource in the Azure portal.</span></span>
2. <span data-ttu-id="66eb4-211">Klik op **Search**.</span><span class="sxs-lookup"><span data-stu-id="66eb4-211">Click **Search**.</span></span>
3. <span data-ttu-id="66eb4-212">Type `ai.snapshot.id` in het zoekvak en druk op Enter.</span><span class="sxs-lookup"><span data-stu-id="66eb4-212">Type `ai.snapshot.id` in the Search text box and press Enter.</span></span>

![Zoeken naar telemetrie met een momentopname-ID in de portal](./media/app-insights-snapshot-debugger/search-snapshot-portal.png)

<span data-ttu-id="66eb4-214">Als deze zoekopdracht geen resultaten oplevert, zijn wordt er zijn geen momentopnamen gerapporteerd, naar Application Insights voor uw toepassing in de geselecteerde periode.</span><span class="sxs-lookup"><span data-stu-id="66eb4-214">If this search returns no results, then no snapshots were reported to Application Insights for your application in the selected time range.</span></span>

<span data-ttu-id="66eb4-215">Als u wilt zoeken naar een specifieke momentopname-ID van de logboeken Uploader, typt u die ID in het zoekvak.</span><span class="sxs-lookup"><span data-stu-id="66eb4-215">To search for a specific snapshot ID from the Uploader logs, type that ID in the Search box.</span></span> <span data-ttu-id="66eb4-216">Als u geen telemetrie voor een momentopname waarvan u weet dat is geüpload vinden, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="66eb4-216">If you can't find telemetry for a snapshot that you know was uploaded, follow these steps:</span></span>

1. <span data-ttu-id="66eb4-217">Controleer dat u op zoek bent op de juiste Application Insights-resource door te controleren of de instrumentatiesleutel.</span><span class="sxs-lookup"><span data-stu-id="66eb4-217">Double-check that you're looking at the right Application Insights resource by verifying the instrumentation key.</span></span>

2. <span data-ttu-id="66eb4-218">Met behulp van de tijdstempel van het logboek Uploader, het filter tijdsbereik van de zoekopdracht omvatten die tijdsbereik aanpassen.</span><span class="sxs-lookup"><span data-stu-id="66eb4-218">Using the timestamp from the Uploader log, adjust the Time Range filter of the search to cover that time range.</span></span>

<span data-ttu-id="66eb4-219">Als u een uitzondering met die ID momentopname niet ziet, is niet de uitzonderingstelemetrie gerapporteerd naar Application Insights.</span><span class="sxs-lookup"><span data-stu-id="66eb4-219">If you still don't see an exception with that snapshot ID, then the exception telemetry wasn't reported to Application Insights.</span></span> <span data-ttu-id="66eb4-220">Deze situatie kan zich voordoen als uw toepassing is vastgelopen nadat de momentopname die het heeft, maar voordat de uitzonderingstelemetrie gemeld.</span><span class="sxs-lookup"><span data-stu-id="66eb4-220">This situation can happen if your application crashed after it took the snapshot but before it reported the exception telemetry.</span></span> <span data-ttu-id="66eb4-221">In dit geval, controleert u de App Service-Logboeken onder `Diagnose and solve problems` om te zien of er onverwachte opnieuw wordt opgestart zijn of onverwerkte uitzonderingen.</span><span class="sxs-lookup"><span data-stu-id="66eb4-221">In this case, check the App Service logs under `Diagnose and solve problems` to see if there were unexpected restarts or unhandled exceptions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66eb4-222">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="66eb4-222">Next steps</span></span>

* <span data-ttu-id="66eb4-223">[Snappoints instellen in uw code](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/) momentopnamen ophalen zonder te wachten op een uitzondering.</span><span class="sxs-lookup"><span data-stu-id="66eb4-223">[Set snappoints in your code](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/) to get snapshots without waiting for an exception.</span></span>
* <span data-ttu-id="66eb4-224">[Diagnose van uitzonderingen in uw web-apps](app-insights-asp-net-exceptions.md) wordt uitgelegd hoe u meer uitzonderingen zichtbaar maken voor Application Insights.</span><span class="sxs-lookup"><span data-stu-id="66eb4-224">[Diagnose exceptions in your web apps](app-insights-asp-net-exceptions.md) explains how to make more exceptions visible to Application Insights.</span></span> 
* <span data-ttu-id="66eb4-225">[Detectie van smartcard](app-insights-proactive-diagnostics.md) detecteert automatisch afwijkingen.</span><span class="sxs-lookup"><span data-stu-id="66eb4-225">[Smart Detection](app-insights-proactive-diagnostics.md) automatically discovers performance anomalies.</span></span>
