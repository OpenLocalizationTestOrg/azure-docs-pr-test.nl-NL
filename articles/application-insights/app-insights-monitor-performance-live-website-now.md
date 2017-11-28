---
title: aaaMonitor een live ASP.NET web-app met Azure Application Insights | Microsoft Docs
description: Bewaak de prestaties van een website zonder de website opnieuw te implementeren. Werkt met ASP.NET-web-apps die on-premises worden gehost, die in virtuele machines worden gehost en die via Azure worden gehost.
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 769a5ea4-a8c6-4c18-b46c-657e864e24de
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: 0d53f0a59974f40767fae681bafc4f358d1283a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="instrument-web-apps-at-runtime-with-application-insights"></a><span data-ttu-id="f565f-104">Web-apps tijdens runtime instrumenteren met Application Insights</span><span class="sxs-lookup"><span data-stu-id="f565f-104">Instrument web apps at runtime with Application Insights</span></span>


<span data-ttu-id="f565f-105">U kunt een live web-app met Azure Application Insights, zonder toomodify softwareontwikkelaars of implementeren van uw code.</span><span class="sxs-lookup"><span data-stu-id="f565f-105">You can instrument a live web app with Azure Application Insights, without having toomodify or redeploy your code.</span></span> <span data-ttu-id="f565f-106">Als uw apps worden gehost op een on-premises IIS-server, installeert u Status Monitor.</span><span class="sxs-lookup"><span data-stu-id="f565f-106">If your apps are hosted by an on-premises IIS server, install Status Monitor.</span></span> <span data-ttu-id="f565f-107">Als ze nu Azure-web-apps of in een virtuele machine in Azure worden uitgevoerd, kunt u overschakelen op de bewaking van Application Insights in hello Azure het Configuratiescherm.</span><span class="sxs-lookup"><span data-stu-id="f565f-107">If they're Azure web apps or run in an Azure VM, you can switch on Application Insights monitoring from hello Azure control panel.</span></span> <span data-ttu-id="f565f-108">(Er zijn ook afzonderlijke artikelen over het instrumenteren van [live J2EE-web-apps](app-insights-java-live.md) en [Azure Cloud Services](app-insights-cloudservices.md).) U hebt een [Microsoft Azure](http://azure.com)-abonnement nodig.</span><span class="sxs-lookup"><span data-stu-id="f565f-108">(There are also separate articles about instrumenting [live J2EE web apps](app-insights-java-live.md) and [Azure Cloud Services](app-insights-cloudservices.md).) You need a [Microsoft Azure](http://azure.com) subscription.</span></span>

![voorbeeldgrafieken](./media/app-insights-monitor-performance-live-website-now/10-intro.png)

<span data-ttu-id="f565f-110">Hebt u een keuze uit drie routes tooapply Application Insights tooyour .NET-webtoepassingen:</span><span class="sxs-lookup"><span data-stu-id="f565f-110">You have a choice of three routes tooapply Application Insights tooyour .NET web applications:</span></span>

* <span data-ttu-id="f565f-111">**Bouwen:** [Hallo Add Application Insights-SDK] [ greenbrown] tooyour web-app-code.</span><span class="sxs-lookup"><span data-stu-id="f565f-111">**Build time:** [Add hello Application Insights SDK][greenbrown] tooyour web app code.</span></span>
* <span data-ttu-id="f565f-112">**Uitvoeringstijd:** Instrumenteren van uw web-app op Hallo van server, zoals hieronder, zonder opnieuw te bouwen en opnieuw distribueren Hallo code wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="f565f-112">**Run time:** Instrument your web app on hello server, as described below, without rebuilding and redeploying hello code.</span></span>
* <span data-ttu-id="f565f-113">**Beide:** Hallo SDK bouwen in uw web-app-code en ook van toepassing hello runtime-extensies.</span><span class="sxs-lookup"><span data-stu-id="f565f-113">**Both:** Build hello SDK into your web app code, and also apply hello run-time extensions.</span></span> <span data-ttu-id="f565f-114">Hallo beste van beide opties worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="f565f-114">Get hello best of both options.</span></span>

<span data-ttu-id="f565f-115">Hier volgt een samenvatting van wat elke route u biedt:</span><span class="sxs-lookup"><span data-stu-id="f565f-115">Here's a summary of what you get by each route:</span></span>

|  | <span data-ttu-id="f565f-116">Tijdens het bouwen</span><span class="sxs-lookup"><span data-stu-id="f565f-116">Build time</span></span> | <span data-ttu-id="f565f-117">Tijdens het gebruik</span><span class="sxs-lookup"><span data-stu-id="f565f-117">Run time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f565f-118">Aanvragen en uitzonderingen</span><span class="sxs-lookup"><span data-stu-id="f565f-118">Requests & exceptions</span></span> |<span data-ttu-id="f565f-119">Ja</span><span class="sxs-lookup"><span data-stu-id="f565f-119">Yes</span></span> |<span data-ttu-id="f565f-120">Ja</span><span class="sxs-lookup"><span data-stu-id="f565f-120">Yes</span></span> |
| [<span data-ttu-id="f565f-121">Meer gedetailleerde uitzonderingen</span><span class="sxs-lookup"><span data-stu-id="f565f-121">More detailed exceptions</span></span>](app-insights-asp-net-exceptions.md) | |<span data-ttu-id="f565f-122">Ja</span><span class="sxs-lookup"><span data-stu-id="f565f-122">Yes</span></span> |
| [<span data-ttu-id="f565f-123">Diagnostische gegevens over afhankelijkheid</span><span class="sxs-lookup"><span data-stu-id="f565f-123">Dependency diagnostics</span></span>](app-insights-asp-net-dependencies.md) |<span data-ttu-id="f565f-124">Op .NET 4.6+, maar minder details</span><span class="sxs-lookup"><span data-stu-id="f565f-124">On .NET 4.6+, but less detail</span></span> |<span data-ttu-id="f565f-125">Ja, volledige details: resultaatcodes, SQL-opdrachttekst, HTTP-woord</span><span class="sxs-lookup"><span data-stu-id="f565f-125">Yes, full detail: result codes, SQL command text, HTTP verb</span></span>|
| [<span data-ttu-id="f565f-126">Systeemprestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="f565f-126">System performance counters</span></span>](app-insights-performance-counters.md) |<span data-ttu-id="f565f-127">Ja</span><span class="sxs-lookup"><span data-stu-id="f565f-127">Yes</span></span> |<span data-ttu-id="f565f-128">Ja</span><span class="sxs-lookup"><span data-stu-id="f565f-128">Yes</span></span> |
| <span data-ttu-id="f565f-129">[API voor aangepaste telemetrie][api]</span><span class="sxs-lookup"><span data-stu-id="f565f-129">[API for custom telemetry][api]</span></span> |<span data-ttu-id="f565f-130">Ja</span><span class="sxs-lookup"><span data-stu-id="f565f-130">Yes</span></span> |<span data-ttu-id="f565f-131">Nee</span><span class="sxs-lookup"><span data-stu-id="f565f-131">No</span></span> |
| [<span data-ttu-id="f565f-132">Integratie traceerlogboeken</span><span class="sxs-lookup"><span data-stu-id="f565f-132">Trace log integration</span></span>](app-insights-asp-net-trace-logs.md) |<span data-ttu-id="f565f-133">Ja</span><span class="sxs-lookup"><span data-stu-id="f565f-133">Yes</span></span> |<span data-ttu-id="f565f-134">Nee</span><span class="sxs-lookup"><span data-stu-id="f565f-134">No</span></span> |
| [<span data-ttu-id="f565f-135">Paginaweergave en gebruikersgegevens</span><span class="sxs-lookup"><span data-stu-id="f565f-135">Page view & user data</span></span>](app-insights-javascript.md) |<span data-ttu-id="f565f-136">Ja</span><span class="sxs-lookup"><span data-stu-id="f565f-136">Yes</span></span> |<span data-ttu-id="f565f-137">Nee</span><span class="sxs-lookup"><span data-stu-id="f565f-137">No</span></span> |
| <span data-ttu-id="f565f-138">Toorebuild code nodig</span><span class="sxs-lookup"><span data-stu-id="f565f-138">Need toorebuild code</span></span> |<span data-ttu-id="f565f-139">Ja</span><span class="sxs-lookup"><span data-stu-id="f565f-139">Yes</span></span> | <span data-ttu-id="f565f-140">Nee</span><span class="sxs-lookup"><span data-stu-id="f565f-140">No</span></span> |


## <a name="monitor-a-live-azure-web-app"></a><span data-ttu-id="f565f-141">Een live Azure-web-app bewaken</span><span class="sxs-lookup"><span data-stu-id="f565f-141">Monitor a live Azure web app</span></span>

<span data-ttu-id="f565f-142">Als uw toepassing wordt uitgevoerd als een Azure-web-service, hier van hoe tooswitch over het controleren van:</span><span class="sxs-lookup"><span data-stu-id="f565f-142">If your application is running as an Azure web service, here's how tooswitch on monitoring:</span></span>

* <span data-ttu-id="f565f-143">Selecteer Application Insights in het Configuratiescherm Hallo-app in Azure.</span><span class="sxs-lookup"><span data-stu-id="f565f-143">Select Application Insights on hello app's control panel in Azure.</span></span>

    ![Application Insights instellen voor een Azure-web-app](./media/app-insights-monitor-performance-live-website-now/azure-web-setup.png)
* <span data-ttu-id="f565f-145">Wanneer Hallo Application Insights-overzichtspagina wordt geopend, klikt u op Hallo koppeling Hallo onder tooopen Hallo volledige Application Insights-resource.</span><span class="sxs-lookup"><span data-stu-id="f565f-145">When hello Application Insights summary page opens, click hello link at hello bottom tooopen hello full Application Insights resource.</span></span>

    ![Klik door tooApplication Insights](./media/app-insights-monitor-performance-live-website-now/azure-web-view-more.png)

<span data-ttu-id="f565f-147">[Cloud- en VM-apps bewaken](app-insights-azure.md).</span><span class="sxs-lookup"><span data-stu-id="f565f-147">[Monitoring Cloud and VM apps](app-insights-azure.md).</span></span>

### <a name="enable-client-side-monitoring-in-azure"></a><span data-ttu-id="f565f-148">Bewaking aan clientzijde in Azure inschakelen</span><span class="sxs-lookup"><span data-stu-id="f565f-148">Enable client-side monitoring in Azure</span></span>

<span data-ttu-id="f565f-149">Als u Application Insights in Azure hebt ingeschakeld, kunt u de paginaweergave en gebruikerstelemetrie toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f565f-149">If you have enabled Application Insights in Azure, you can add page view and user telemetry.</span></span>

1. <span data-ttu-id="f565f-150">Selecteer Instellingen > Toepassingsinstellingen</span><span class="sxs-lookup"><span data-stu-id="f565f-150">Select Settings > Application Settings</span></span>
2.  <span data-ttu-id="f565f-151">Voeg een nieuw sleutelwaardepaar toe bij App-instellingen:</span><span class="sxs-lookup"><span data-stu-id="f565f-151">Under App Settings, add a new key value pair:</span></span> 
   
    <span data-ttu-id="f565f-152">Sleutel: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span><span class="sxs-lookup"><span data-stu-id="f565f-152">Key: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span></span> 
    
    <span data-ttu-id="f565f-153">Waarde:`true`</span><span class="sxs-lookup"><span data-stu-id="f565f-153">Value: `true`</span></span>
3. <span data-ttu-id="f565f-154">**Sla** Hallo instellingen en **opnieuw** uw app.</span><span class="sxs-lookup"><span data-stu-id="f565f-154">**Save** hello settings and **Restart** your app.</span></span>

<span data-ttu-id="f565f-155">Hallo Application Insights JavaScript SDK is nu opgenomen in elke webpagina.</span><span class="sxs-lookup"><span data-stu-id="f565f-155">hello Application Insights JavaScript SDK is now injected into each web page.</span></span>

## <a name="monitor-a-live-iis-web-app"></a><span data-ttu-id="f565f-156">Een live IIS-web-app bewaken</span><span class="sxs-lookup"><span data-stu-id="f565f-156">Monitor a live IIS web app</span></span>

<span data-ttu-id="f565f-157">Als uw app wordt gehost op een IIS-server, kunt u Application Insights inschakelen met Status Monitor.</span><span class="sxs-lookup"><span data-stu-id="f565f-157">If your app is hosted on an IIS server, enable Application Insights by using Status Monitor.</span></span>

1. <span data-ttu-id="f565f-158">Meld u op uw IIS-webserver aan met beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="f565f-158">On your IIS web server, sign in with administrator credentials.</span></span>
2. <span data-ttu-id="f565f-159">Als de Application Insights Status Monitor nog niet is geïnstalleerd, downloaden en uitvoeren van Hallo [Status Monitor-installatieprogramma](http://go.microsoft.com/fwlink/?LinkId=506648) (of uit te voeren [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) en zoekt u in het Application Insights Status Monitor).</span><span class="sxs-lookup"><span data-stu-id="f565f-159">If Application Insights Status Monitor is not already installed, download and run hello [Status Monitor installer](http://go.microsoft.com/fwlink/?LinkId=506648) (or run [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) and search in it for Application Insights Status Monitor).</span></span>
3. <span data-ttu-id="f565f-160">Selecteer in de Status Monitor Hallo geïnstalleerd webtoepassing of website die u toomonitor wilt.</span><span class="sxs-lookup"><span data-stu-id="f565f-160">In Status Monitor, select hello installed web application or website that you want toomonitor.</span></span> <span data-ttu-id="f565f-161">Meld u aan met uw Azure-referenties.</span><span class="sxs-lookup"><span data-stu-id="f565f-161">Sign in with your Azure credentials.</span></span>

    <span data-ttu-id="f565f-162">Hallo-resource waar u toosee Hallo resulteert in Application Insights-portal hello wilt configureren.</span><span class="sxs-lookup"><span data-stu-id="f565f-162">Configure hello resource where you want toosee hello results in hello Application Insights portal.</span></span> <span data-ttu-id="f565f-163">(Normaal gesproken het is aanbevolen toocreate een nieuwe resource.</span><span class="sxs-lookup"><span data-stu-id="f565f-163">(Normally, it's best toocreate a new resource.</span></span> <span data-ttu-id="f565f-164">Selecteer een bestaande resource als u al [webtests][availability] of [clientbewaking][client] hebt voor deze app.)</span><span class="sxs-lookup"><span data-stu-id="f565f-164">Select an existing resource if you already have [web tests][availability] or [client monitoring][client] for this app.)</span></span> 

    ![Kies een app en een resource.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-configAIC.png)

4. <span data-ttu-id="f565f-166">Start IIS opnieuw.</span><span class="sxs-lookup"><span data-stu-id="f565f-166">Restart IIS.</span></span>

    ![Opnieuw opstarten boven Hallo van Hallo dialoogvenster kiezen.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-restart.png)

    <span data-ttu-id="f565f-168">Uw webservice wordt enkele ogenblikken onderbroken.</span><span class="sxs-lookup"><span data-stu-id="f565f-168">Your web service is interrupted for a short while.</span></span>

## <a name="customize-monitoring-options"></a><span data-ttu-id="f565f-169">Bewakingsopties aanpassen</span><span class="sxs-lookup"><span data-stu-id="f565f-169">Customize monitoring options</span></span>

<span data-ttu-id="f565f-170">Application Insights inschakelen voegt dll's en ApplicationInsights.config tooyour web-app.</span><span class="sxs-lookup"><span data-stu-id="f565f-170">Enabling Application Insights adds DLLs and ApplicationInsights.config tooyour web app.</span></span> <span data-ttu-id="f565f-171">U kunt [Hallo .config-bestand bewerken](app-insights-configuration-with-applicationinsights-config.md) toochange aantal Hallo-opties.</span><span class="sxs-lookup"><span data-stu-id="f565f-171">You can [edit hello .config file](app-insights-configuration-with-applicationinsights-config.md) toochange some of hello options.</span></span>

## <a name="when-you-re-publish-your-app-re-enable-application-insights"></a><span data-ttu-id="f565f-172">Wanneer u uw app opnieuw publiceert, schakelt u Application Insights opnieuw in</span><span class="sxs-lookup"><span data-stu-id="f565f-172">When you re-publish your app, re-enable Application Insights</span></span>

<span data-ttu-id="f565f-173">Voordat u uw app opnieuw publiceert, rekening houden met [Application Insights toohello code toe te voegen in Visual Studio][greenbrown].</span><span class="sxs-lookup"><span data-stu-id="f565f-173">Before you re-publish your app, consider [adding Application Insights toohello code in Visual Studio][greenbrown].</span></span> <span data-ttu-id="f565f-174">U krijgt meer gedetailleerde Telemetrie en Hallo mogelijkheid toowrite aangepaste telemetrie.</span><span class="sxs-lookup"><span data-stu-id="f565f-174">You'll get more detailed telemetry and hello ability toowrite custom telemetry.</span></span>

<span data-ttu-id="f565f-175">Als u wilt dat toore-publiceren zonder Application Insights toohello code toe te voegen, houd er rekening mee dat implementatieproces Hallo Hallo dll-bestanden te verwijderen en ApplicationInsights.config van Hallo website gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="f565f-175">If you want toore-publish without adding Application Insights toohello code, be aware that hello deployment process may delete hello DLLs and ApplicationInsights.config from hello published web site.</span></span> <span data-ttu-id="f565f-176">Daarom:</span><span class="sxs-lookup"><span data-stu-id="f565f-176">Therefore:</span></span>

1. <span data-ttu-id="f565f-177">Als u ApplicationInsights.config hebt bewerkt, maakt u er een kopie van voordat u de app opnieuw publiceert.</span><span class="sxs-lookup"><span data-stu-id="f565f-177">If you edited ApplicationInsights.config, take a copy of it before you re-publish your app.</span></span>
2. <span data-ttu-id="f565f-178">Publiceer uw app opnieuw.</span><span class="sxs-lookup"><span data-stu-id="f565f-178">Republish your app.</span></span>
3. <span data-ttu-id="f565f-179">Schakel Application Insights-bewaking opnieuw in.</span><span class="sxs-lookup"><span data-stu-id="f565f-179">Re-enable Application Insights monitoring.</span></span> <span data-ttu-id="f565f-180">(Gebruik de juiste methode Hallo: hello Azure-web-app van het Configuratiescherm of Hallo Status Monitor op een IIS-host.)</span><span class="sxs-lookup"><span data-stu-id="f565f-180">(Use hello appropriate method: either hello Azure web app control panel, or hello Status Monitor on an IIS host.)</span></span>
4. <span data-ttu-id="f565f-181">Alle bewerkingen die u hebt uitgevoerd op Hallo .config-bestand opnieuw.</span><span class="sxs-lookup"><span data-stu-id="f565f-181">Reinstate any edits you performed on hello .config file.</span></span>


## <a name="troubleshooting-runtime-configuration-of-application-insights"></a><span data-ttu-id="f565f-182">Problemen met de runtimeconfiguratie van Application Insights oplossen</span><span class="sxs-lookup"><span data-stu-id="f565f-182">Troubleshooting runtime configuration of Application Insights</span></span>

### <a name="cant-connect-no-telemetry"></a><span data-ttu-id="f565f-183">Kunt u geen verbinding maken?</span><span class="sxs-lookup"><span data-stu-id="f565f-183">Can't connect?</span></span> <span data-ttu-id="f565f-184">Geen telemetrie?</span><span class="sxs-lookup"><span data-stu-id="f565f-184">No telemetry?</span></span>

* <span data-ttu-id="f565f-185">Open [Hallo nodig uitgaande poorten](app-insights-ip-addresses.md#outgoing-ports) in uw server firewall tooallow Status Monitor toowork.</span><span class="sxs-lookup"><span data-stu-id="f565f-185">Open [hello necessary outgoing ports](app-insights-ip-addresses.md#outgoing-ports) in your server's firewall tooallow Status Monitor toowork.</span></span>

* <span data-ttu-id="f565f-186">Open Status Monitor en selecteer in het linkerdeelvenster uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="f565f-186">Open Status Monitor and select your application on left pane.</span></span> <span data-ttu-id="f565f-187">Controleer of er diagnostische meldingen voor deze toepassing in de sectie 'Configuration notifications' hello zijn:</span><span class="sxs-lookup"><span data-stu-id="f565f-187">Check if there are any diagnostics messages for this application in hello "Configuration notifications" section:</span></span>

  ![Open Hallo prestaties blade toosee aanvraag, reactietijden, afhankelijkheden en andere gegevens](./media/app-insights-monitor-performance-live-website-now/appinsights-status-monitor-diagnostics-message.png)
* <span data-ttu-id="f565f-189">Op Hallo van server, als er een bericht over 'onvoldoende machtigingen', voer een Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="f565f-189">On hello server, if you see a message about "insufficient permissions", try hello following:</span></span>
  * <span data-ttu-id="f565f-190">In de IIS-beheer, selecteer uw groep van toepassingen, open **geavanceerde instellingen**, en klikt u onder **procesmodel** Noteer Hallo identiteit.</span><span class="sxs-lookup"><span data-stu-id="f565f-190">In IIS Manager, select your application pool, open **Advanced Settings**, and under **Process Model** note hello identity.</span></span>
  * <span data-ttu-id="f565f-191">In het Configuratiescherm voor Computerbeheer, voeg deze identiteit toohello Prestatiemetergebruikers.</span><span class="sxs-lookup"><span data-stu-id="f565f-191">In Computer management control panel, add this identity toohello Performance Monitor Users group.</span></span>
* <span data-ttu-id="f565f-192">Als op uw server MMA/SCOM (Systems Center Operations Manager) is geïnstalleerd, kan er een conflict optreden met sommige versies.</span><span class="sxs-lookup"><span data-stu-id="f565f-192">If you have MMA/SCOM (Systems Center Operations Manager) installed on your server, some versions can conflict.</span></span> <span data-ttu-id="f565f-193">Verwijder zowel SCOM als Status Monitor en installeer opnieuw de meest recente versies Hallo.</span><span class="sxs-lookup"><span data-stu-id="f565f-193">Uninstall both SCOM and Status Monitor, and re-install hello latest versions.</span></span>
* <span data-ttu-id="f565f-194">Zie [Probleemoplossing][qna].</span><span class="sxs-lookup"><span data-stu-id="f565f-194">See [Troubleshooting][qna].</span></span>

## <a name="system-requirements"></a><span data-ttu-id="f565f-195">Systeemvereisten</span><span class="sxs-lookup"><span data-stu-id="f565f-195">System Requirements</span></span>
<span data-ttu-id="f565f-196">Ondersteuning van het besturingssysteem voor Application Insights Status Monitor op de server:</span><span class="sxs-lookup"><span data-stu-id="f565f-196">OS support for Application Insights Status Monitor on Server:</span></span>

* <span data-ttu-id="f565f-197">Windows Server 2008</span><span class="sxs-lookup"><span data-stu-id="f565f-197">Windows Server 2008</span></span>
* <span data-ttu-id="f565f-198">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="f565f-198">Windows Server 2008 R2</span></span>
* <span data-ttu-id="f565f-199">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="f565f-199">Windows Server 2012</span></span>
* <span data-ttu-id="f565f-200">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="f565f-200">Windows server 2012 R2</span></span>
* <span data-ttu-id="f565f-201">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="f565f-201">Windows Server 2016</span></span>

<span data-ttu-id="f565f-202">met het nieuwste SP en .NET-framework 4.5</span><span class="sxs-lookup"><span data-stu-id="f565f-202">with latest SP and .NET Framework 4.5</span></span>

<span data-ttu-id="f565f-203">Aan de clientzijde Hallo: Windows 7, 8, 8.1 en 10, opnieuw met .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="f565f-203">On hello client side: Windows 7, 8, 8.1 and 10, again with .NET Framework 4.5</span></span>

<span data-ttu-id="f565f-204">Ondersteuning voor IIS is: IIS 7, 7.5, 8, 8.5 (IIS is vereist)</span><span class="sxs-lookup"><span data-stu-id="f565f-204">IIS support is: IIS 7, 7.5, 8, 8.5 (IIS is required)</span></span>

## <a name="automation-with-powershell"></a><span data-ttu-id="f565f-205">Automatisering met PowerShell</span><span class="sxs-lookup"><span data-stu-id="f565f-205">Automation with PowerShell</span></span>
<span data-ttu-id="f565f-206">Met PowerShell kunt u de bewaking op de IIS-server starten en stoppen.</span><span class="sxs-lookup"><span data-stu-id="f565f-206">You can start and stop monitoring by using PowerShell on your IIS server.</span></span>

<span data-ttu-id="f565f-207">Eerst Hallo Application Insights-module importeren:</span><span class="sxs-lookup"><span data-stu-id="f565f-207">First import hello Application Insights module:</span></span>

`Import-Module 'C:\Program Files\Microsoft Application Insights\Status Monitor\PowerShell\Microsoft.Diagnostics.Agent.StatusMonitor.PowerShell.dll'`

<span data-ttu-id="f565f-208">Controleer welke apps worden bewaakt:</span><span class="sxs-lookup"><span data-stu-id="f565f-208">Find out which apps are being monitored:</span></span>

`Get-ApplicationInsightsMonitoringStatus [-Name appName]`

* <span data-ttu-id="f565f-209">`-Name`(Optioneel) Hallo-naam van een web-app.</span><span class="sxs-lookup"><span data-stu-id="f565f-209">`-Name` (Optional) hello name of a web app.</span></span>
* <span data-ttu-id="f565f-210">Geeft Hallo Application Insights-bewakingsstatus voor elke web-app (of met de naam app Hallo) in deze IIS-server.</span><span class="sxs-lookup"><span data-stu-id="f565f-210">Displays hello Application Insights monitoring status for each web app (or hello named app) in this IIS server.</span></span>
* <span data-ttu-id="f565f-211">Retourneert `ApplicationInsightsApplication` voor elke app:</span><span class="sxs-lookup"><span data-stu-id="f565f-211">Returns `ApplicationInsightsApplication` for each app:</span></span>

  * <span data-ttu-id="f565f-212">`SdkState==EnabledAfterDeployment`: De app wordt bewaakt en is tijdens de uitvoering geïnstrumenteerd door hulpprogramma Hallo-Status Monitor of door `Start-ApplicationInsightsMonitoring`.</span><span class="sxs-lookup"><span data-stu-id="f565f-212">`SdkState==EnabledAfterDeployment`: App is being monitored, and was instrumented at run time, either by hello Status Monitor tool, or by `Start-ApplicationInsightsMonitoring`.</span></span>
  * <span data-ttu-id="f565f-213">`SdkState==Disabled`: Hallo app is niet geïnstrumenteerd voor Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f565f-213">`SdkState==Disabled`: hello app is not instrumented for Application Insights.</span></span> <span data-ttu-id="f565f-214">Deze App is niet geïnstrumenteerd, hetzij runtime-controle is uitgeschakeld met hulpprogramma voor Hallo Status Monitor of met `Stop-ApplicationInsightsMonitoring`.</span><span class="sxs-lookup"><span data-stu-id="f565f-214">Either it was never instrumented, or run-time monitoring was disabled with hello Status Monitor tool or with `Stop-ApplicationInsightsMonitoring`.</span></span>
  * <span data-ttu-id="f565f-215">`SdkState==EnabledByCodeInstrumentation`: Hallo app is geïnstrumenteerd door Hallo SDK toohello broncode toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="f565f-215">`SdkState==EnabledByCodeInstrumentation`: hello app was instrumented by adding hello SDK toohello source code.</span></span> <span data-ttu-id="f565f-216">De SDK kan niet worden bijgewerkt of gestopt.</span><span class="sxs-lookup"><span data-stu-id="f565f-216">Its SDK cannot be updated or stopped.</span></span>
  * <span data-ttu-id="f565f-217">`SdkVersion`Hallo versie bevat gebruikt voor het bewaken van deze app.</span><span class="sxs-lookup"><span data-stu-id="f565f-217">`SdkVersion` shows hello version in use for monitoring this app.</span></span>
  * <span data-ttu-id="f565f-218">`LatestAvailableSdkVersion`bevat Hallo-versie die momenteel beschikbaar op Hallo NuGet-galerie.</span><span class="sxs-lookup"><span data-stu-id="f565f-218">`LatestAvailableSdkVersion`shows hello version currently available on hello NuGet gallery.</span></span> <span data-ttu-id="f565f-219">tooupgrade hello app toothis versie, gebruik `Update-ApplicationInsightsMonitoring`.</span><span class="sxs-lookup"><span data-stu-id="f565f-219">tooupgrade hello app toothis version, use `Update-ApplicationInsightsMonitoring`.</span></span>

`Start-ApplicationInsightsMonitoring -Name appName -InstrumentationKey 00000000-000-000-000-0000000`

* <span data-ttu-id="f565f-220">`-Name`Hallo-naam van Hallo-app in IIS</span><span class="sxs-lookup"><span data-stu-id="f565f-220">`-Name` hello name of hello app in IIS</span></span>
* <span data-ttu-id="f565f-221">`-InstrumentationKey`Hallo ikey Hallo Application Insights-resource waar u Hallo resultaten toobe weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f565f-221">`-InstrumentationKey` hello ikey of hello Application Insights resource where you want hello results toobe displayed.</span></span>
* <span data-ttu-id="f565f-222">Deze cmdlet geldt alleen voor apps die niet al zijn geïnstrumenteerd, dus SdkState==NotInstrumented.</span><span class="sxs-lookup"><span data-stu-id="f565f-222">This cmdlet only affects apps that are not already instrumented - that is, SdkState==NotInstrumented.</span></span>

    <span data-ttu-id="f565f-223">Hallo-cmdlet heeft geen invloed op een app die al zijn geïnstrumenteerd.</span><span class="sxs-lookup"><span data-stu-id="f565f-223">hello cmdlet does not affect an app that is already instrumented.</span></span> <span data-ttu-id="f565f-224">Het niet belangrijk te weten dat het Hallo-app is geïnstrumenteerd build gelijktijdig door Hallo SDK toohello code toevoegen of tijdens runtime met gebruik van deze cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f565f-224">It does not matter whether hello app was instrumented at build time by adding hello SDK toohello code, or at run time by a previous use of this cmdlet.</span></span>

    <span data-ttu-id="f565f-225">Hallo SDK versie die wordt gebruikt tooinstrument Hallo-app is Hallo-versie die het laatst toothis server hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="f565f-225">hello SDK version used tooinstrument hello app is hello version that was most recently downloaded toothis server.</span></span>

    <span data-ttu-id="f565f-226">meest recente versie toodownload hello, Update-ApplicationInsightsVersion gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f565f-226">toodownload hello latest version, use Update-ApplicationInsightsVersion.</span></span>
* <span data-ttu-id="f565f-227">Retourneert `ApplicationInsightsApplication` wanneer het is gelukt.</span><span class="sxs-lookup"><span data-stu-id="f565f-227">Returns `ApplicationInsightsApplication` on success.</span></span> <span data-ttu-id="f565f-228">Als dit mislukt, wordt een toostderr trace gelogd.</span><span class="sxs-lookup"><span data-stu-id="f565f-228">If it fails, it logs a trace toostderr.</span></span>

          Name                      : Default Web Site/WebApp1
          InstrumentationKey        : 00000000-0000-0000-0000-000000000000
          ProfilerState             : ApplicationInsights
          SdkState                  : EnabledAfterDeployment
          SdkVersion                : 1.2.1
          LatestAvailableSdkVersion : 1.2.3

`Stop-ApplicationInsightsMonitoring [-Name appName | -All]`

* <span data-ttu-id="f565f-229">`-Name`Hallo-naam van een app in IIS</span><span class="sxs-lookup"><span data-stu-id="f565f-229">`-Name` hello name of an app in IIS</span></span>
* <span data-ttu-id="f565f-230">`-All` Stopt het bewaken van alle apps op deze IIS-server waarvoor `SdkState==EnabledAfterDeployment`</span><span class="sxs-lookup"><span data-stu-id="f565f-230">`-All` Stops monitoring all apps in this IIS server for which `SdkState==EnabledAfterDeployment`</span></span>
* <span data-ttu-id="f565f-231">Stopt de bewaking van Hallo opgegeven apps en verwijdert instrumentatie.</span><span class="sxs-lookup"><span data-stu-id="f565f-231">Stops monitoring hello specified apps and removes instrumentation.</span></span> <span data-ttu-id="f565f-232">Deze functie werkt alleen voor apps die op het gebruik van de runtime-zijn geïnstrumenteerd Hallo hulpprogramma Status of Start-ApplicationInsightsApplication.</span><span class="sxs-lookup"><span data-stu-id="f565f-232">It only works for apps that have been instrumented at run-time using hello Status Monitoring tool or Start-ApplicationInsightsApplication.</span></span> <span data-ttu-id="f565f-233">(`SdkState==EnabledAfterDeployment`)</span><span class="sxs-lookup"><span data-stu-id="f565f-233">(`SdkState==EnabledAfterDeployment`)</span></span>
* <span data-ttu-id="f565f-234">Retourneert ApplicationInsightsApplication.</span><span class="sxs-lookup"><span data-stu-id="f565f-234">Returns ApplicationInsightsApplication.</span></span>

<span data-ttu-id="f565f-235">`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]</span><span class="sxs-lookup"><span data-stu-id="f565f-235">`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]</span></span>

* <span data-ttu-id="f565f-236">`-Name`: Hallo-naam van een web-app in IIS.</span><span class="sxs-lookup"><span data-stu-id="f565f-236">`-Name`: hello name of a web app in IIS.</span></span>
* <span data-ttu-id="f565f-237">`-InstrumentationKey` (Optioneel.) Gebruik die deze toochange Hallo resource toowhich Hallo van app telemetrie wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="f565f-237">`-InstrumentationKey` (Optional.) Use this toochange hello resource toowhich hello app's telemetry is sent.</span></span>
* <span data-ttu-id="f565f-238">Deze cmdlet:</span><span class="sxs-lookup"><span data-stu-id="f565f-238">This cmdlet:</span></span>
  * <span data-ttu-id="f565f-239">Upgrades Hallo app toohello-versie van Hallo SDK met de naam gedownload meest recent toothis machine.</span><span class="sxs-lookup"><span data-stu-id="f565f-239">Upgrades hello named app toohello version of hello SDK most recently downloaded toothis machine.</span></span> <span data-ttu-id="f565f-240">(Werkt alleen als `SdkState==EnabledAfterDeployment`)</span><span class="sxs-lookup"><span data-stu-id="f565f-240">(Only works if `SdkState==EnabledAfterDeployment`)</span></span>
  * <span data-ttu-id="f565f-241">Als u een instrumentatiesleutel opgeeft, is met de naam app Hallo opnieuw geconfigureerde toosend telemetrie toohello bron met die sleutel.</span><span class="sxs-lookup"><span data-stu-id="f565f-241">If you provide an instrumentation key, hello named app is reconfigured toosend telemetry toohello resource with that key.</span></span> <span data-ttu-id="f565f-242">(Werkt als `SdkState != Disabled`)</span><span class="sxs-lookup"><span data-stu-id="f565f-242">(Works if `SdkState != Disabled`)</span></span>

`Update-ApplicationInsightsVersion`

* <span data-ttu-id="f565f-243">Hallo nieuwste Application Insights-SDK toohello server downloadt.</span><span class="sxs-lookup"><span data-stu-id="f565f-243">Downloads hello latest Application Insights SDK toohello server.</span></span>

## <span data-ttu-id="f565f-244"><a name="questions"></a>Vragen over Status Monitor</span><span class="sxs-lookup"><span data-stu-id="f565f-244"><a name="questions"></a>Questions about Status Monitor</span></span>

### <a name="what-is-status-monitor"></a><span data-ttu-id="f565f-245">Wat is Status Monitor?</span><span class="sxs-lookup"><span data-stu-id="f565f-245">What is Status Monitor?</span></span>

<span data-ttu-id="f565f-246">Een bureaubladtoepassing die u op uw IIS-webserver kunt installeren.</span><span class="sxs-lookup"><span data-stu-id="f565f-246">A desktop application that you install in your IIS web server.</span></span> <span data-ttu-id="f565f-247">Hiermee kunt u web-apps instrumenteren en configureren.</span><span class="sxs-lookup"><span data-stu-id="f565f-247">It helps you instrument and configure web apps.</span></span> 

### <a name="when-do-i-use-status-monitor"></a><span data-ttu-id="f565f-248">Wanneer maak ik gebruik van Status Monitor?</span><span class="sxs-lookup"><span data-stu-id="f565f-248">When do I use Status Monitor?</span></span>

* <span data-ttu-id="f565f-249">tooinstrument een web-app die wordt uitgevoerd op uw IIS-server - zelfs als het al wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f565f-249">tooinstrument any web app that is running on your IIS server - even if it is already running.</span></span>
* <span data-ttu-id="f565f-250">aanvullende telemetrie voor web-apps die zijn tooenable [gebouwd met Application Insights-SDK Hallo](app-insights-asp-net.md) tijdens de compilatie.</span><span class="sxs-lookup"><span data-stu-id="f565f-250">tooenable additional telemetry for web apps that have been [built with hello Application Insights SDK](app-insights-asp-net.md) at compile time.</span></span> 

### <a name="can-i-close-it-after-it-runs"></a><span data-ttu-id="f565f-251">Kan ik de applicatie sluiten nadat deze is uitgevoerd?</span><span class="sxs-lookup"><span data-stu-id="f565f-251">Can I close it after it runs?</span></span>

<span data-ttu-id="f565f-252">Ja.</span><span class="sxs-lookup"><span data-stu-id="f565f-252">Yes.</span></span> <span data-ttu-id="f565f-253">Nadat deze is geïnstrumenteerd Hallo websites die u selecteert, kunt u deze sluiten.</span><span class="sxs-lookup"><span data-stu-id="f565f-253">After it has instrumented hello websites you select, you can close it.</span></span>

<span data-ttu-id="f565f-254">Status Monitor verzamelt niet zelf telemetrie.</span><span class="sxs-lookup"><span data-stu-id="f565f-254">It doesn't collect telemetry by itself.</span></span> <span data-ttu-id="f565f-255">Gewoon configureert Hallo web-apps en sommige machtigingen ingesteld.</span><span class="sxs-lookup"><span data-stu-id="f565f-255">It just configures hello web apps and sets some permissions.</span></span>

### <a name="what-does-status-monitor-do"></a><span data-ttu-id="f565f-256">Wat doet Status Monitor?</span><span class="sxs-lookup"><span data-stu-id="f565f-256">What does Status Monitor do?</span></span>

<span data-ttu-id="f565f-257">Wanneer u een web-app voor statuscontrole tooinstrument selecteren:</span><span class="sxs-lookup"><span data-stu-id="f565f-257">When you select a web app for Status Monitor tooinstrument:</span></span>

* <span data-ttu-id="f565f-258">Downloadt en plaatst Hallo Application Insights-assembly's en .config-bestand in map met binaire Hallo van web-app.</span><span class="sxs-lookup"><span data-stu-id="f565f-258">Downloads and places hello Application Insights assemblies and .config file in hello web app's binaries folder.</span></span>
* <span data-ttu-id="f565f-259">Hiermee wijzigt u `web.config` tooadd Hallo Application Insights HTTP bijhouden-module.</span><span class="sxs-lookup"><span data-stu-id="f565f-259">Modifies `web.config` tooadd hello Application Insights HTTP tracking module.</span></span>
* <span data-ttu-id="f565f-260">Kan CLR toocollect afhankelijkheidsaanroepen profilering.</span><span class="sxs-lookup"><span data-stu-id="f565f-260">Enables CLR profiling toocollect dependency calls.</span></span>

### <a name="do-i-need-toorun-status-monitor-whenever-i-update-hello-app"></a><span data-ttu-id="f565f-261">Moet ik toorun Status Monitor wanneer ik Hallo app bijwerken?</span><span class="sxs-lookup"><span data-stu-id="f565f-261">Do I need toorun Status Monitor whenever I update hello app?</span></span>

<span data-ttu-id="f565f-262">Niet als u deze stapsgewijs opnieuw implementeert.</span><span class="sxs-lookup"><span data-stu-id="f565f-262">Not if you redeploy incrementally.</span></span> 

<span data-ttu-id="f565f-263">Als u optie Hallo 'delete bestaande bestanden' in hello proces publiceren, moet u toore-run Status Monitor tooconfigure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f565f-263">If you select hello 'delete existing files' option in hello publish process, you would need toore-run Status Monitor tooconfigure Application Insights.</span></span>

### <a name="what-telemetry-is-collected"></a><span data-ttu-id="f565f-264">Welke telemetrie wordt verzameld?</span><span class="sxs-lookup"><span data-stu-id="f565f-264">What telemetry is collected?</span></span>

<span data-ttu-id="f565f-265">Voor toepassingen die u met behulp van de Status Monitor bij het uitvoeren instrumenteert:</span><span class="sxs-lookup"><span data-stu-id="f565f-265">For applications that you instrument only at run-time by using Status Monitor:</span></span>

* <span data-ttu-id="f565f-266">HTTP-aanvragen</span><span class="sxs-lookup"><span data-stu-id="f565f-266">HTTP requests</span></span>
* <span data-ttu-id="f565f-267">Aanroepen toodependencies</span><span class="sxs-lookup"><span data-stu-id="f565f-267">Calls toodependencies</span></span>
* <span data-ttu-id="f565f-268">Uitzonderingen</span><span class="sxs-lookup"><span data-stu-id="f565f-268">Exceptions</span></span>
* <span data-ttu-id="f565f-269">Prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="f565f-269">Performance counters</span></span>

<span data-ttu-id="f565f-270">Voor toepassingen die bij het compileren al zijn geïnstrumenteerd:</span><span class="sxs-lookup"><span data-stu-id="f565f-270">For applications already instrumented at compile time:</span></span>

 * <span data-ttu-id="f565f-271">Procestellers.</span><span class="sxs-lookup"><span data-stu-id="f565f-271">Process counters.</span></span>
 * <span data-ttu-id="f565f-272">Afhankelijkheidsaanroepen (.NET 4.5); retourwaarden in afhankelijkheidsaanroepen (.NET 4.6).</span><span class="sxs-lookup"><span data-stu-id="f565f-272">Dependency calls (.NET 4.5); return values in dependency calls (.NET 4.6).</span></span>
 * <span data-ttu-id="f565f-273">Stack-tracewaarden van uitzonderingen.</span><span class="sxs-lookup"><span data-stu-id="f565f-273">Exception stack trace values.</span></span>

[<span data-ttu-id="f565f-274">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="f565f-274">Learn more</span></span>](http://apmtips.com/blog/2016/11/18/how-application-insights-status-monitor-not-monitors-dependencies/)

## <a name="video"></a><span data-ttu-id="f565f-275">Video</span><span class="sxs-lookup"><span data-stu-id="f565f-275">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <span data-ttu-id="f565f-276"><a name="next"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f565f-276"><a name="next"></a>Next steps</span></span>

<span data-ttu-id="f565f-277">Uw telemetrie weergeven:</span><span class="sxs-lookup"><span data-stu-id="f565f-277">View your telemetry:</span></span>

* <span data-ttu-id="f565f-278">[Verkennen van metrische gegevens](app-insights-metrics-explorer.md) toomonitor prestaties en gebruik</span><span class="sxs-lookup"><span data-stu-id="f565f-278">[Explore metrics](app-insights-metrics-explorer.md) toomonitor performance and usage</span></span>
* <span data-ttu-id="f565f-279">[Zoek naar gebeurtenissen en logboeken] [ diagnostic] toodiagnose problemen</span><span class="sxs-lookup"><span data-stu-id="f565f-279">[Search events and logs][diagnostic] toodiagnose problems</span></span>
* <span data-ttu-id="f565f-280">[Gebruik analyses](app-insights-analytics.md) voor meer geavanceerde query's</span><span class="sxs-lookup"><span data-stu-id="f565f-280">[Analytics](app-insights-analytics.md) for more advanced queries</span></span>
* [<span data-ttu-id="f565f-281">Maak dashboards</span><span class="sxs-lookup"><span data-stu-id="f565f-281">Create dashboards</span></span>](app-insights-dashboards.md)

<span data-ttu-id="f565f-282">Meer telemetrie toevoegen:</span><span class="sxs-lookup"><span data-stu-id="f565f-282">Add more telemetry:</span></span>

* <span data-ttu-id="f565f-283">[Maak webtests] [ availability] toomake zorgen dat uw site actief blijft.</span><span class="sxs-lookup"><span data-stu-id="f565f-283">[Create web tests][availability] toomake sure your site stays live.</span></span>
* <span data-ttu-id="f565f-284">[Voeg telemetrie van de webclient] [ usage] toosee uitzonderingen op de webpagina code en toolet u invoegen aanroepen traceren.</span><span class="sxs-lookup"><span data-stu-id="f565f-284">[Add web client telemetry][usage] toosee exceptions from web page code and toolet you insert trace calls.</span></span>
* <span data-ttu-id="f565f-285">[Application Insights-SDK tooyour code toevoegen] [ greenbrown] zodat u kunt trace invoegen en meld u aanroepen</span><span class="sxs-lookup"><span data-stu-id="f565f-285">[Add Application Insights SDK tooyour code][greenbrown] so that you can insert trace and log calls</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[availability]: app-insights-monitor-web-app-availability.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[roles]: app-insights-resources-roles-access-control.md
[usage]: app-insights-javascript.md
