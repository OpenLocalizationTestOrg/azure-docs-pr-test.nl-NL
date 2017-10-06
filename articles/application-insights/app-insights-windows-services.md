---
title: aaaAzure Application Insights voor Windows server- en werkrollen rollen | Microsoft Docs
description: Handmatig toevoegen Hallo Application Insights-SDK tooyour ASP.NET-toepassing tooanalyze gebruik, beschikbaarheid en prestaties.
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 106ba99b-b57a-43b8-8866-e02f626c8190
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: 64643ef637195d10f87fc6020a77169bca66c1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manually-configure-application-insights-for-net-applications"></a><span data-ttu-id="a5b05-103">Application Insights handmatig configureren voor .NET-toepassingen</span><span class="sxs-lookup"><span data-stu-id="a5b05-103">Manually configure Application Insights for .NET applications</span></span>

<span data-ttu-id="a5b05-104">U kunt configureren [Application Insights](app-insights-overview.md) toomonitor tal van toepassingen of toepassing functies, onderdelen of microservices.</span><span class="sxs-lookup"><span data-stu-id="a5b05-104">You can configure [Application Insights](app-insights-overview.md) toomonitor a wide variety of applications or application roles, components, or microservices.</span></span> <span data-ttu-id="a5b05-105">Voor web-apps en services biedt Visual Studio [configuratie in één stap](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="a5b05-105">For web apps and services, Visual Studio offers [one-step configuration](app-insights-asp-net.md).</span></span> <span data-ttu-id="a5b05-106">Voor andere typen .NET-toepassingen, zoals back-end-serverfuncties of -desktoptoepassingen, kunt u Application Insights handmatig configureren.</span><span class="sxs-lookup"><span data-stu-id="a5b05-106">For other types of .NET application, such as backend server roles or desktop applications, you can configure Application Insights manually.</span></span>

![Voorbeeld van grafieken met prestatiebewaking](./media/app-insights-windows-services/10-perf.png)

#### <a name="before-you-start"></a><span data-ttu-id="a5b05-108">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="a5b05-108">Before you start</span></span>

<span data-ttu-id="a5b05-109">U hebt de volgende zaken nodig:</span><span class="sxs-lookup"><span data-stu-id="a5b05-109">You need:</span></span>

* <span data-ttu-id="a5b05-110">Een abonnement te[Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="a5b05-110">A subscription too[Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="a5b05-111">Als uw team of organisatie een Azure-abonnement heeft, Hallo kan eigenaar u toevoegen tooit, met behulp van uw [Microsoft-account](http://live.com).</span><span class="sxs-lookup"><span data-stu-id="a5b05-111">If your team or organization has an Azure subscription, hello owner can add you tooit, using your [Microsoft account](http://live.com).</span></span>
* <span data-ttu-id="a5b05-112">Visual Studio 2013 of later.</span><span class="sxs-lookup"><span data-stu-id="a5b05-112">Visual Studio 2013 or later.</span></span>

## <span data-ttu-id="a5b05-113"><a name="add"></a>1. Een Application Insights-resource kiezen</span><span class="sxs-lookup"><span data-stu-id="a5b05-113"><a name="add"></a>1. Choose an Application Insights resource</span></span>

<span data-ttu-id="a5b05-114">Hallo 'resource' is waar uw gegevens worden verzameld en weergegeven in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a5b05-114">hello 'resource' is where your data is collected and displayed in hello Azure portal.</span></span> <span data-ttu-id="a5b05-115">Moet u toodecide of toocreate een nieuwe, of een bestaande bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="a5b05-115">You need toodecide whether toocreate a new one, or share an existing one.</span></span>

### <a name="part-of-a-larger-app-use-existing-resource"></a><span data-ttu-id="a5b05-116">Onderdeel van een grotere app: bestaande resource gebruiken</span><span class="sxs-lookup"><span data-stu-id="a5b05-116">Part of a larger app: Use existing resource</span></span>

<span data-ttu-id="a5b05-117">Als uw webtoepassing verschillende onderdelen - bijvoorbeeld een front-web-app en een of meer back-end-services heeft - er moet voor het verzenden van telemetrie vanaf alle Hallo onderdelen toohello dezelfde resource.</span><span class="sxs-lookup"><span data-stu-id="a5b05-117">If your web application has several components - for example, a front-end web app and one or more back-end services - then you should send telemetry from all hello components toohello same resource.</span></span> <span data-ttu-id="a5b05-118">Dit wordt deze weergegeven op een enkele toepassing kaart toobe inschakelen en maken het mogelijk tootrace een aanvraag van een onderdeel tooanother.</span><span class="sxs-lookup"><span data-stu-id="a5b05-118">This will enable them toobe displayed on a single Application Map, and make it possible tootrace a request from one component tooanother.</span></span>

<span data-ttu-id="a5b05-119">Dus als u bent al andere onderdelen van deze app bewaken, klikt u vervolgens alleen gebruik Hallo dezelfde resource.</span><span class="sxs-lookup"><span data-stu-id="a5b05-119">So, if you're already monitoring other components of this app, then just use hello same resource.</span></span>

<span data-ttu-id="a5b05-120">Hallo-resource openen in Hallo [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a5b05-120">Open hello resource in hello [Azure portal](https://portal.azure.com/).</span></span> 

### <a name="self-contained-app-create-a-new-resource"></a><span data-ttu-id="a5b05-121">Zelfstandige app: nieuwe resource maken</span><span class="sxs-lookup"><span data-stu-id="a5b05-121">Self-contained app: Create a new resource</span></span>

<span data-ttu-id="a5b05-122">Als nieuwe Hallo-app niet van belang tooother toepassingen is, moet dit een eigen resource hebben.</span><span class="sxs-lookup"><span data-stu-id="a5b05-122">If hello new app is unrelated tooother applications, then it should have its own resource.</span></span>

<span data-ttu-id="a5b05-123">Meld u aan toohello [Azure-portal](https://portal.azure.com/), en maak een nieuwe Application Insights-resource.</span><span class="sxs-lookup"><span data-stu-id="a5b05-123">Sign in toohello [Azure portal](https://portal.azure.com/), and create a new Application Insights resource.</span></span> <span data-ttu-id="a5b05-124">Kies ASP.NET als Hallo toepassingstype.</span><span class="sxs-lookup"><span data-stu-id="a5b05-124">Choose ASP.NET as hello application type.</span></span>

![Klik op Nieuw > Application Insights](./media/app-insights-windows-services/01-new-asp.png)

<span data-ttu-id="a5b05-126">Hallo gekozen toepassingstype wordt de Standaardinhoud Hallo van Hallo resourceblades.</span><span class="sxs-lookup"><span data-stu-id="a5b05-126">hello choice of application type sets hello default content of hello resource blades.</span></span>

## <a name="2-copy-hello-instrumentation-key"></a><span data-ttu-id="a5b05-127">2. Hallo Instrumentatiesleutel kopiëren</span><span class="sxs-lookup"><span data-stu-id="a5b05-127">2. Copy hello Instrumentation Key</span></span>
<span data-ttu-id="a5b05-128">Hallo sleutel identificeert Hallo resource.</span><span class="sxs-lookup"><span data-stu-id="a5b05-128">hello key identifies hello resource.</span></span> <span data-ttu-id="a5b05-129">U hebt deze snel installeren in Hallo SDK, in volgorde toodirect gegevens toohello resource.</span><span class="sxs-lookup"><span data-stu-id="a5b05-129">You'll install it soon in hello SDK, in order toodirect data toohello resource.</span></span>

![Klik op eigenschappen en druk op ctrl + C Hallo sleutel selecteren](./media/app-insights-windows-services/02-props-asp.png)

## <span data-ttu-id="a5b05-131"><a name="sdk"></a>3. Hallo Application Insights-pakket installeren in uw toepassing</span><span class="sxs-lookup"><span data-stu-id="a5b05-131"><a name="sdk"></a>3. Install hello Application Insights package in your application</span></span>
<span data-ttu-id="a5b05-132">Installeren en configureren van Hallo Application Insights wordt pakket varieert afhankelijk van Hallo platform waarmee u werkt.</span><span class="sxs-lookup"><span data-stu-id="a5b05-132">Installing and configuring hello Application Insights package varies depending on hello platform you're working on.</span></span> 

1. <span data-ttu-id="a5b05-133">Klik in Visual Studio met de rechtermuisknop op het project en kies **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="a5b05-133">In Visual Studio, right-click your project and choose **Manage Nuget Packages**.</span></span>
   
    ![Met de rechtermuisknop op het Hallo-project en selecteer Nuget-pakketten beheren](./media/app-insights-windows-services/03-nuget.png)
2. <span data-ttu-id="a5b05-135">Application Insights-pakket voor Windows server-apps, 'Microsoft.ApplicationInsights.WindowsServer.' hello installeren</span><span class="sxs-lookup"><span data-stu-id="a5b05-135">Install hello Application Insights package for Windows server apps, "Microsoft.ApplicationInsights.WindowsServer."</span></span>
   
    ![Naar Application Insights zoeken](./media/app-insights-windows-services/04-ai-nuget.png)
   
    <span data-ttu-id="a5b05-137">*Welke versie?*</span><span class="sxs-lookup"><span data-stu-id="a5b05-137">*Which version?*</span></span>

    <span data-ttu-id="a5b05-138">Controleer **Include prerelease** desgewenst tootry onze nieuwste functies.</span><span class="sxs-lookup"><span data-stu-id="a5b05-138">Check **Include prerelease** if you want tootry our latest features.</span></span> <span data-ttu-id="a5b05-139">Hallo relevante documenten of blogs opmerking of u een prerelease-versie moet.</span><span class="sxs-lookup"><span data-stu-id="a5b05-139">hello relevant documents or blogs note whether you need a prerelease version.</span></span>
    
    <span data-ttu-id="a5b05-140">*Kan ik andere pakketten gebruiken?*</span><span class="sxs-lookup"><span data-stu-id="a5b05-140">*Can I use other packages?*</span></span>
   
    <span data-ttu-id="a5b05-141">Ja.</span><span class="sxs-lookup"><span data-stu-id="a5b05-141">Yes.</span></span> <span data-ttu-id="a5b05-142">Kies 'Microsoft.ApplicationInsights' als u wilt dat alleen toouse Hallo API toosend uw eigen telemetrie.</span><span class="sxs-lookup"><span data-stu-id="a5b05-142">Choose "Microsoft.ApplicationInsights" if you only want toouse hello API toosend your own telemetry.</span></span> <span data-ttu-id="a5b05-143">Hallo-pakket voor Windows Server omvat Hallo API plus een aantal andere pakketten zoals het verzamelen van prestatiemeteritems en bewaking van afhankelijkheid.</span><span class="sxs-lookup"><span data-stu-id="a5b05-143">hello Windows Server package includes hello API plus a number of other packages such as performance counter collection and dependency monitoring.</span></span> 

### <a name="tooupgrade-toofuture-package-versions"></a><span data-ttu-id="a5b05-144">tooupgrade toofuture pakketversies</span><span class="sxs-lookup"><span data-stu-id="a5b05-144">tooupgrade toofuture package versions</span></span>
<span data-ttu-id="a5b05-145">Brengen we een nieuwe versie van Hallo SDK van tijd tootime.</span><span class="sxs-lookup"><span data-stu-id="a5b05-145">We release a new version of hello SDK from time tootime.</span></span>

<span data-ttu-id="a5b05-146">tooupgrade tooa [nieuwe release van Hallo pakket](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/), opent u NuGet-Pakketbeheer opnieuw en filtert u op geïnstalleerde pakketten.</span><span class="sxs-lookup"><span data-stu-id="a5b05-146">tooupgrade tooa [new release of hello package](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/), open NuGet package manager again and filter on installed packages.</span></span> <span data-ttu-id="a5b05-147">Selecteer **Microsoft.ApplicationInsights.WindowsServer** en kies **Upgraden**.</span><span class="sxs-lookup"><span data-stu-id="a5b05-147">Select **Microsoft.ApplicationInsights.WindowsServer** and choose **Upgrade**.</span></span>

<span data-ttu-id="a5b05-148">Als u alle aanpassingen tooApplicationInsights.config genomen, een kopie van deze opslaan voordat u bijwerken en vervolgens uw wijzigingen in de nieuwe versie Hallo samen.</span><span class="sxs-lookup"><span data-stu-id="a5b05-148">If you made any customizations tooApplicationInsights.config, save a copy of it before you upgrade, and afterwards merge your changes into hello new version.</span></span>

## <a name="4-send-telemetry"></a><span data-ttu-id="a5b05-149">4. Telemetrie verzenden</span><span class="sxs-lookup"><span data-stu-id="a5b05-149">4. Send telemetry</span></span>
<span data-ttu-id="a5b05-150">**Als u alleen Hallo API-pakket geïnstalleerd:**</span><span class="sxs-lookup"><span data-stu-id="a5b05-150">**If you installed only hello API package:**</span></span>

* <span data-ttu-id="a5b05-151">De instrumentatiesleutel Hallo in code, bijvoorbeeld ingesteld in `main()`:</span><span class="sxs-lookup"><span data-stu-id="a5b05-151">Set hello instrumentation key in code, for example in `main()`:</span></span> 
  
    <span data-ttu-id="a5b05-152">`TelemetryConfiguration.Active.InstrumentationKey = "` *uw sleutel* `";`</span><span class="sxs-lookup"><span data-stu-id="a5b05-152">`TelemetryConfiguration.Active.InstrumentationKey = "` *your key* `";`</span></span> 
* <span data-ttu-id="a5b05-153">[Uw eigen telemetrie met Hallo API schrijven](app-insights-api-custom-events-metrics.md#ikey).</span><span class="sxs-lookup"><span data-stu-id="a5b05-153">[Write your own telemetry using hello API](app-insights-api-custom-events-metrics.md#ikey).</span></span>

<span data-ttu-id="a5b05-154">**Als u andere pakketten Application Insights geïnstalleerd** kunt, als u liever, u Hallo .config-bestand tooset hello instrumentatiesleutel:</span><span class="sxs-lookup"><span data-stu-id="a5b05-154">**If you installed other Application Insights packages,** you can, if you prefer, use hello .config file tooset hello instrumentation key:</span></span>

* <span data-ttu-id="a5b05-155">Bewerk ApplicationInsights.config (die is toegevoegd door Hallo NuGet installeren).</span><span class="sxs-lookup"><span data-stu-id="a5b05-155">Edit ApplicationInsights.config (which was added by hello NuGet install).</span></span> <span data-ttu-id="a5b05-156">Voeg dit vlak vóór Hallo afsluitcode:</span><span class="sxs-lookup"><span data-stu-id="a5b05-156">Insert this just before hello closing tag:</span></span>
  
    <span data-ttu-id="a5b05-157">`<InstrumentationKey>`*Hallo-instrumentatiesleutel die u hebt gekopieerd*`</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="a5b05-157">`<InstrumentationKey>` *hello instrumentation key you copied* `</InstrumentationKey>`</span></span>
* <span data-ttu-id="a5b05-158">Zorg ervoor dat de eigenschappen van ApplicationInsights.config in Solution Explorer hello te worden ingesteld**Build Action = inhoud, kopie tooOutput Directory = kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="a5b05-158">Make sure that hello properties of ApplicationInsights.config in Solution Explorer are set too**Build Action = Content, Copy tooOutput Directory = Copy**.</span></span>

<span data-ttu-id="a5b05-159">Het is nuttig tooset hello instrumentatiesleutel in de code als u wilt dat te[switch Hallo sleutel voor ander buildnummer configuraties](app-insights-separate-resources.md).</span><span class="sxs-lookup"><span data-stu-id="a5b05-159">It's useful tooset hello instrumentation key in code if you want too[switch hello key for different build configurations](app-insights-separate-resources.md).</span></span> <span data-ttu-id="a5b05-160">Als u Hallo-sleutel in de code hebt ingesteld, hebt u niet tooset in Hallo `.config` bestand.</span><span class="sxs-lookup"><span data-stu-id="a5b05-160">If you set hello key in code, you don't have tooset it in hello `.config` file.</span></span>

## <span data-ttu-id="a5b05-161"><a name="run"></a> Uw project uitvoeren</span><span class="sxs-lookup"><span data-stu-id="a5b05-161"><a name="run"></a> Run your project</span></span>
<span data-ttu-id="a5b05-162">Gebruik Hallo **F5** toorun uw toepassing en probeer deze uit: open verschillende pagina's toogenerate telemetrie.</span><span class="sxs-lookup"><span data-stu-id="a5b05-162">Use hello **F5** toorun your application and try it out: open different pages toogenerate some telemetry.</span></span>

<span data-ttu-id="a5b05-163">In Visual Studio ziet u een aantal Hallo-gebeurtenissen die zijn verzonden.</span><span class="sxs-lookup"><span data-stu-id="a5b05-163">In Visual Studio, you'll see a count of hello events that have been sent.</span></span>

![Het aantal gebeurtenissen in Visual Studio](./media/app-insights-windows-services/appinsights-09eventcount.png)

## <span data-ttu-id="a5b05-165"><a name="monitor"></a> Uw telemetrie weergeven</span><span class="sxs-lookup"><span data-stu-id="a5b05-165"><a name="monitor"></a> View your telemetry</span></span>
<span data-ttu-id="a5b05-166">Retourneren van toohello [Azure-portal](https://portal.azure.com/) en blader tooyour Application Insights-resource.</span><span class="sxs-lookup"><span data-stu-id="a5b05-166">Return toohello [Azure portal](https://portal.azure.com/) and browse tooyour Application Insights resource.</span></span>

<span data-ttu-id="a5b05-167">Zoek naar gegevens in de overzichtsgrafieken Hallo.</span><span class="sxs-lookup"><span data-stu-id="a5b05-167">Look for data in hello Overview charts.</span></span> <span data-ttu-id="a5b05-168">Aanvankelijk ziet u slechts één of twee punten.</span><span class="sxs-lookup"><span data-stu-id="a5b05-168">At first, you'll just see one or two points.</span></span> <span data-ttu-id="a5b05-169">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="a5b05-169">For example:</span></span>

![Klik door toomore gegevens](./media/app-insights-windows-services/12-first-perf.png)

<span data-ttu-id="a5b05-171">Klik op via een grafiek toosee gedetailleerdere metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="a5b05-171">Click through any chart toosee more detailed metrics.</span></span> [<span data-ttu-id="a5b05-172">Meer informatie over metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="a5b05-172">Learn more about metrics.</span></span>](app-insights-web-monitor-performance.md)

### <a name="no-data"></a><span data-ttu-id="a5b05-173">Zijn er geen gegevens?</span><span class="sxs-lookup"><span data-stu-id="a5b05-173">No data?</span></span>
* <span data-ttu-id="a5b05-174">Gebruik Hallo toepassing om verschillende pagina's te openen zodat er telemetrie wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="a5b05-174">Use hello application, opening different pages so that it generates some telemetry.</span></span>
* <span data-ttu-id="a5b05-175">Open Hallo [Search](app-insights-diagnostic-search.md) tegel, toosee afzonderlijke gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="a5b05-175">Open hello [Search](app-insights-diagnostic-search.md) tile, toosee individual events.</span></span> <span data-ttu-id="a5b05-176">Het duurt soms een beetje terwijl langer tooget via Hallo metrische gegevens pipeline gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="a5b05-176">Sometimes it takes events a little while longer tooget through hello metrics pipeline.</span></span>
* <span data-ttu-id="a5b05-177">Wacht een paar seconden en klik op **Vernieuwen**.</span><span class="sxs-lookup"><span data-stu-id="a5b05-177">Wait a few seconds and click **Refresh**.</span></span> <span data-ttu-id="a5b05-178">Grafieken worden regelmatig vernieuwd, maar u kunt handmatig vernieuwen als u voor sommige gegevens tooshow up wacht.</span><span class="sxs-lookup"><span data-stu-id="a5b05-178">Charts refresh themselves periodically, but you can refresh manually if you're waiting for some data tooshow up.</span></span>
* <span data-ttu-id="a5b05-179">Zie [Probleemoplossing](app-insights-troubleshoot-faq.md).</span><span class="sxs-lookup"><span data-stu-id="a5b05-179">See [Troubleshooting](app-insights-troubleshoot-faq.md).</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="a5b05-180">Uw app publiceren</span><span class="sxs-lookup"><span data-stu-id="a5b05-180">Publish your app</span></span>
<span data-ttu-id="a5b05-181">Nu uw toepassing tooyour server implementeren of tooAzure en bekijk Hallo-gegevens worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="a5b05-181">Now deploy your application tooyour server or tooAzure and watch hello data accumulate.</span></span>

![Visual Studio toopublish uw app gebruiken](./media/app-insights-windows-services/15-publish.png)

<span data-ttu-id="a5b05-183">Wanneer u in de foutopsporingsmodus uitvoert, wordt de telemetrie direct via Hallo pipeline, zodat u gegevens ziet verschijnen binnen enkele seconden.</span><span class="sxs-lookup"><span data-stu-id="a5b05-183">When you run in debug mode, telemetry is expedited through hello pipeline, so that you should see data appearing within seconds.</span></span> <span data-ttu-id="a5b05-184">Wanneer u uw app in de Release-configuratie implementeert, duurt het langer om gegevens te verzamelen.</span><span class="sxs-lookup"><span data-stu-id="a5b05-184">When you deploy your app in Release configuration, data accumulates more slowly.</span></span>

### <a name="no-data-after-you-publish-tooyour-server"></a><span data-ttu-id="a5b05-185">Er zijn geen gegevens nadat u tooyour server hebt gepubliceerd?</span><span class="sxs-lookup"><span data-stu-id="a5b05-185">No data after you publish tooyour server?</span></span>
<span data-ttu-id="a5b05-186">Open poorten voor uitgaand verkeer in de firewall van uw server.</span><span class="sxs-lookup"><span data-stu-id="a5b05-186">Open ports for outgoing traffic in your server's firewall.</span></span> <span data-ttu-id="a5b05-187">Zie [deze pagina](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses) voor Hallo lijst met vereiste adressen</span><span class="sxs-lookup"><span data-stu-id="a5b05-187">See [this page](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses) for hello list of required addresses</span></span> 

### <a name="trouble-on-your-build-server"></a><span data-ttu-id="a5b05-188">Problemen op uw buildserver?</span><span class="sxs-lookup"><span data-stu-id="a5b05-188">Trouble on your build server?</span></span>
<span data-ttu-id="a5b05-189">Raadpleeg dit artikel voor [Probleemoplossing](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild).</span><span class="sxs-lookup"><span data-stu-id="a5b05-189">Please see [this Troubleshooting item](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild).</span></span>

> [!NOTE]
> <span data-ttu-id="a5b05-190">Als uw app veel telemetrie genereert, beperkt Hallo adaptieve steekproeven module automatisch Hallo volume dat toohello portal wordt verzonden door alleen een representatieve fractie van gebeurtenissen verzenden.</span><span class="sxs-lookup"><span data-stu-id="a5b05-190">If your app generates a lot of telemetry, hello adaptive sampling module will automatically reduce hello volume that is sent toohello portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="a5b05-191">Gebeurtenissen die zijn echter gerelateerde toohello dezelfde aanvraag worden geselecteerd of gedeselecteerd als groep, zodat u tussen gerelateerde gebeurtenissen kunt navigeren.</span><span class="sxs-lookup"><span data-stu-id="a5b05-191">However, events that are related toohello same request will be selected or deselected as a group, so that you can navigate between related events.</span></span> 
> <span data-ttu-id="a5b05-192">[Meer informatie over steekproeven](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="a5b05-192">[Learn about sampling](app-insights-sampling.md).</span></span>
> 
> 

## <a name="video"></a><span data-ttu-id="a5b05-193">Video</span><span class="sxs-lookup"><span data-stu-id="a5b05-193">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="a5b05-194">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a5b05-194">Next steps</span></span>
* <span data-ttu-id="a5b05-195">[Voeg meer telemetrie](app-insights-asp-net-more.md) tooget Hallo 360-graden weergave van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="a5b05-195">[Add more telemetry](app-insights-asp-net-more.md) tooget hello full 360-degree view of your application.</span></span>

