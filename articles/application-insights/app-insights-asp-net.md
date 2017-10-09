---
title: aaaSet van web-app-analyse voor ASP.NET met Azure Application Insights | Microsoft Docs
description: Configureer prestaties, beschikbaarheid en gebruiksanalyse voor uw ASP.NET-website die on-premises of in Azure wordt gehost.
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d0eee3c0-b328-448f-8123-f478052751db
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: 61a3cdce68da48bfb9450b1d296acc1535f50a38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-application-insights-for-your-aspnet-website"></a><span data-ttu-id="35475-103">Application Insights instellen voor uw ASP.NET-website</span><span class="sxs-lookup"><span data-stu-id="35475-103">Set up Application Insights for your ASP.NET website</span></span>

<span data-ttu-id="35475-104">Deze procedure configureert u uw ASP.NET web app toosend telemetrie toohello [Azure Application Insights](app-insights-overview.md) service.</span><span class="sxs-lookup"><span data-stu-id="35475-104">This procedure configures your ASP.NET web app toosend telemetry toohello [Azure Application Insights](app-insights-overview.md) service.</span></span> <span data-ttu-id="35475-105">De Tool werkt voor ASP.NET-apps die worden gehost in een eigen IIS-server of in Hallo Cloud.</span><span class="sxs-lookup"><span data-stu-id="35475-105">It works for ASP.NET apps that are hosted either in your own IIS server or in hello Cloud.</span></span> <span data-ttu-id="35475-106">Ophalen van grafieken en een krachtige querytaal die u helpen begrijpen Hallo prestaties van uw app en hoe mensen gebruikt, plus automatische waarschuwingen op fouten of prestatieproblemen.</span><span class="sxs-lookup"><span data-stu-id="35475-106">You get charts and a powerful query language that help you understand hello performance of your app and how people are using it, plus automatic alerts on failures or performance issues.</span></span> <span data-ttu-id="35475-107">Veel ontwikkelaars vinden deze functies geweldige zoals ze zijn, maar u kunt ook uitbreiden en aanpassen Hallo telemetrie als u wilt.</span><span class="sxs-lookup"><span data-stu-id="35475-107">Many developers find these features great as they are, but you can also extend and customize hello telemetry if you need to.</span></span>

<span data-ttu-id="35475-108">Voor de Setup zijn maar een paar klikken nodig in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="35475-108">Setup takes just a few clicks in Visual Studio.</span></span> <span data-ttu-id="35475-109">U hebt Hallo optie tooavoid kosten door te beperken Hallo volume telemetrie.</span><span class="sxs-lookup"><span data-stu-id="35475-109">You have hello option tooavoid charges by limiting hello volume of telemetry.</span></span> <span data-ttu-id="35475-110">Hiermee kunt u tooexperiment en foutopsporing of toomonitor een site met niet veel gebruikers.</span><span class="sxs-lookup"><span data-stu-id="35475-110">This allows you tooexperiment and debug, or toomonitor a site with not many users.</span></span> <span data-ttu-id="35475-111">Als u besluit dat u wilt toogo vooruit en controleren van uw productiesite, is het eenvoudig tooraise Hallo limiet later.</span><span class="sxs-lookup"><span data-stu-id="35475-111">When you decide you want toogo ahead and monitor your production site, it's easy tooraise hello limit later.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="35475-112">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="35475-112">Before you start</span></span>
<span data-ttu-id="35475-113">U hebt de volgende zaken nodig:</span><span class="sxs-lookup"><span data-stu-id="35475-113">You need:</span></span>

* <span data-ttu-id="35475-114">Visual Studio 2013 update 3 of later.</span><span class="sxs-lookup"><span data-stu-id="35475-114">Visual Studio 2013 update 3 or later.</span></span> <span data-ttu-id="35475-115">Later is beter.</span><span class="sxs-lookup"><span data-stu-id="35475-115">Later is better.</span></span>
* <span data-ttu-id="35475-116">Een abonnement te[Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="35475-116">A subscription too[Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="35475-117">Als uw team of organisatie een Azure-abonnement heeft, Hallo kan eigenaar u toevoegen tooit, met behulp van uw [Microsoft-account](http://live.com).</span><span class="sxs-lookup"><span data-stu-id="35475-117">If your team or organization has an Azure subscription, hello owner can add you tooit, by using your [Microsoft account](http://live.com).</span></span>

<span data-ttu-id="35475-118">Er zijn andere onderwerpen toolook op als u geïnteresseerd bent in:</span><span class="sxs-lookup"><span data-stu-id="35475-118">There are alternative topics toolook at if you are interested in:</span></span>

* [<span data-ttu-id="35475-119">Een web-app instrumenteren tijdens runtime</span><span class="sxs-lookup"><span data-stu-id="35475-119">Instrumenting a web app at runtime</span></span>](app-insights-monitor-performance-live-website-now.md)
* [<span data-ttu-id="35475-120">Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="35475-120">Azure Cloud Services</span></span>](app-insights-cloudservices.md)

## <span data-ttu-id="35475-121"><a name="ide"></a>Stap 1: Hallo Application Insights-SDK toevoegen</span><span class="sxs-lookup"><span data-stu-id="35475-121"><a name="ide"></a> Step 1: Add hello Application Insights SDK</span></span>

<span data-ttu-id="35475-122">Klik in Solution Explorer met de rechtermuisknop op het web-app-project. Kies **Toevoegen** > **Application Insights Telemetry...** of **Application Insights configureren**.</span><span class="sxs-lookup"><span data-stu-id="35475-122">Right-click your web app project in Solution Explorer, and choose **Add** > **Application Insights Telemetry...** or **Configure Application Insights**.</span></span>

![Schermopname van Solution Explorer waarin Application Insights Telemetry toevoegen is gemarkeerd](./media/app-insights-asp-net/appinsights-03-addExisting.png)

<span data-ttu-id="35475-124">(In Visual Studio 2015, er is ook een optie tooadd Application Insights in het dialoogvenster Nieuw Project Hallo.)</span><span class="sxs-lookup"><span data-stu-id="35475-124">(In Visual Studio 2015, there's also an option tooadd Application Insights in hello New Project dialog.)</span></span>

<span data-ttu-id="35475-125">Pagina toohello Application Insights-configuratie worden voortgezet:</span><span class="sxs-lookup"><span data-stu-id="35475-125">Continue toohello Application Insights configuration page:</span></span>

![Schermopname van de pagina Uw app registreren bij Application Insights](./media/app-insights-asp-net/visual-studio-register-dialog.png)

<span data-ttu-id="35475-127">**a.**</span><span class="sxs-lookup"><span data-stu-id="35475-127">**a.**</span></span> <span data-ttu-id="35475-128">Hallo-account en dat u tooaccess Azure-abonnement selecteren.</span><span class="sxs-lookup"><span data-stu-id="35475-128">Select hello account and subscription that you use tooaccess Azure.</span></span>

<span data-ttu-id="35475-129">**b.**</span><span class="sxs-lookup"><span data-stu-id="35475-129">**b.**</span></span> <span data-ttu-id="35475-130">Selecteer Hallo resource in Azure waar u toosee Hallo gegevens van uw app.</span><span class="sxs-lookup"><span data-stu-id="35475-130">Select hello resource in Azure where you want toosee hello data from your app.</span></span> <span data-ttu-id="35475-131">Meestal:</span><span class="sxs-lookup"><span data-stu-id="35475-131">Usually:</span></span>

* <span data-ttu-id="35475-132">Gebruik [één resource voor verschillende onderdelen](app-insights-monitor-multi-role-apps.md) van één toepassing.</span><span class="sxs-lookup"><span data-stu-id="35475-132">Use a [single resource for different components](app-insights-monitor-multi-role-apps.md) of a single application.</span></span> 
* <span data-ttu-id="35475-133">Maak afzonderlijke resources voor niet-gerelateerde toepassingen.</span><span class="sxs-lookup"><span data-stu-id="35475-133">Create separate resources for unrelated applications.</span></span>
 
<span data-ttu-id="35475-134">Als u wilt dat tooset Hallo groep of Hallo Resourcelocatie waar uw gegevens worden opgeslagen, klikt u op **configureren**.</span><span class="sxs-lookup"><span data-stu-id="35475-134">If you want tooset hello resource group or hello location where your data is stored, click **Configure settings**.</span></span> <span data-ttu-id="35475-135">Resourcegroepen zijn gebruikte toocontrol toegang toodata.</span><span class="sxs-lookup"><span data-stu-id="35475-135">Resource groups are used toocontrol access toodata.</span></span> <span data-ttu-id="35475-136">Bijvoorbeeld, als u verschillende web-apps die deel uitmaken van hebt Hallo dezelfde systeem, kunt u hun Application Insights-gegevens plaatsen dezelfde resourcegroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="35475-136">For example, if you have several apps that form part of hello same system, you might put their Application Insights data in hello same resource group.</span></span>

<span data-ttu-id="35475-137">**c.**</span><span class="sxs-lookup"><span data-stu-id="35475-137">**c.**</span></span> <span data-ttu-id="35475-138">Stel een limiet op Hallo-limiet voor het volume van beschikbare gegevens, tooavoid kosten.</span><span class="sxs-lookup"><span data-stu-id="35475-138">Set a cap at hello free data volume limit, tooavoid charges.</span></span> <span data-ttu-id="35475-139">Application Insights verkeert momenteel vrijmaken tooa bepaald volume van telemetrie.</span><span class="sxs-lookup"><span data-stu-id="35475-139">Application Insights is free up tooa certain volume of telemetry.</span></span> <span data-ttu-id="35475-140">Nadat Hallo resource is gemaakt, kunt u uw selectie in de portal Hallo wijzigen door het openen van **functies en prijzen** > **volume gegevensbeheer** > **per dag volume cap**.</span><span class="sxs-lookup"><span data-stu-id="35475-140">After hello resource is created, you can change your selection in hello portal by opening  **Features + pricing** > **Data volume management** > **Daily volume cap**.</span></span>

<span data-ttu-id="35475-141">**d.**</span><span class="sxs-lookup"><span data-stu-id="35475-141">**d.**</span></span> <span data-ttu-id="35475-142">Klik op **registreren** toogo vooruit en Application Insights configureren voor uw web-app.</span><span class="sxs-lookup"><span data-stu-id="35475-142">Click **Register** toogo ahead and configure Application Insights for your web app.</span></span> <span data-ttu-id="35475-143">Telemetrie verzonden toohello [Azure-portal](https://portal.azure.com), zowel tijdens de foutopsporing en nadat u uw app hebt gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="35475-143">Telemetry will be sent toohello [Azure portal](https://portal.azure.com), both during debugging and after you have published your app.</span></span>

<span data-ttu-id="35475-144">**e.**</span><span class="sxs-lookup"><span data-stu-id="35475-144">**e.**</span></span> <span data-ttu-id="35475-145">Als u niet dat toosend telemetrie toohello portal wilt terwijl u fouten opspoort, Hallo Application Insights-SDK tooyour app toevoegen maar een resource in Hallo portal niet configureren.</span><span class="sxs-lookup"><span data-stu-id="35475-145">If you don't want toosend telemetry toohello portal while you're debugging, just add hello Application Insights SDK tooyour app but don't configure a resource in hello portal.</span></span> <span data-ttu-id="35475-146">U zult kunnen toosee telemetrie in Visual Studio terwijl u fouten opspoort.</span><span class="sxs-lookup"><span data-stu-id="35475-146">You will be able toosee telemetry in Visual Studio while you are debugging.</span></span> <span data-ttu-id="35475-147">Later kunt u de configuratiepagina toothis retourneren, of u kan wachten totdat nadat u uw app hebt geïmplementeerd en [telemetrie inschakelen tijdens de uitvoering](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="35475-147">Later, you can return toothis configuration page, or you could wait until after you have deployed your app and [switch on telemetry at run time](app-insights-monitor-performance-live-website-now.md).</span></span>


## <span data-ttu-id="35475-148"><a name="run"></a> Stap 2: uw app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="35475-148"><a name="run"></a> Step 2: Run your app</span></span>
<span data-ttu-id="35475-149">Voer uw app uit met F5.</span><span class="sxs-lookup"><span data-stu-id="35475-149">Run your app with F5.</span></span> <span data-ttu-id="35475-150">Open verschillende pagina's toogenerate telemetrie.</span><span class="sxs-lookup"><span data-stu-id="35475-150">Open different pages toogenerate some telemetry.</span></span>

<span data-ttu-id="35475-151">In Visual Studio ziet u een aantal Hallo-gebeurtenissen die zijn geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="35475-151">In Visual Studio, you see a count of hello events that have been logged.</span></span>

![Schermopname van Visual Studio.](./media/app-insights-asp-net/54.png)

## <a name="step-3-see-your-telemetry"></a><span data-ttu-id="35475-154">Stap 3: uw telemetrie weergeven</span><span class="sxs-lookup"><span data-stu-id="35475-154">Step 3: See your telemetry</span></span>
<span data-ttu-id="35475-155">U ziet uw telemetrie in Visual Studio of in Hallo Application Insights-webportal.</span><span class="sxs-lookup"><span data-stu-id="35475-155">You can see your telemetry either in Visual Studio or in hello Application Insights web portal.</span></span> <span data-ttu-id="35475-156">Telemetrie zoeken in Visual Studio toohelp u uw app fouten opsporen.</span><span class="sxs-lookup"><span data-stu-id="35475-156">Search telemetry in Visual Studio toohelp you debug your app.</span></span> <span data-ttu-id="35475-157">Bewaak prestaties en gebruik in de webportal Hallo wanneer uw systeem live is.</span><span class="sxs-lookup"><span data-stu-id="35475-157">Monitor performance and usage in hello web portal when your system is live.</span></span> 

### <a name="see-your-telemetry-in-visual-studio"></a><span data-ttu-id="35475-158">De telemetrie bekijken in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="35475-158">See your telemetry in Visual Studio</span></span>

<span data-ttu-id="35475-159">Open in Visual Studio Hallo Application Insights-venster.</span><span class="sxs-lookup"><span data-stu-id="35475-159">In Visual Studio, open hello Application Insights window.</span></span> <span data-ttu-id="35475-160">Hallo klikt u op **Application Insights** knop of met de rechtermuisknop op het project in Solution Explorer, selecteer **Application Insights**, en klik vervolgens op **zoeken Live telemetrie**.</span><span class="sxs-lookup"><span data-stu-id="35475-160">Either click hello **Application Insights** button, or right-click your project in Solution Explorer, select **Application Insights**, and then click **Search Live Telemetry**.</span></span>

<span data-ttu-id="35475-161">Zie in Hallo Visual Studio Application Insights zoeken venster Hallo **gegevens van foutopsporingssessie** weergave voor de telemetrie die is gegenereerd in Hallo servergedeelte van uw app.</span><span class="sxs-lookup"><span data-stu-id="35475-161">In hello Visual Studio Application Insights Search window, see hello **Data from Debug session** view for telemetry generated in hello server side of your app.</span></span> <span data-ttu-id="35475-162">Experimenteren met Hallo filters en klikt u op een gebeurtenis toosee meer details.</span><span class="sxs-lookup"><span data-stu-id="35475-162">Experiment with hello filters, and click any event toosee more detail.</span></span>

![Schermopname van Hallo gegevens van foutopsporingssessie weergeven in Application Insights-venster Hallo.](./media/app-insights-asp-net/55.png)

> [!NOTE]
> <span data-ttu-id="35475-164">Als u niet alle gegevens ziet, zorg Hallo tijdsbereik juist is en klik op het zoekpictogram Hallo.</span><span class="sxs-lookup"><span data-stu-id="35475-164">If you don't see any data, make sure hello time range is correct, and click hello Search icon.</span></span>

<span data-ttu-id="35475-165">[Meer informatie over Application Insights-hulpprogramma's in Visual Studio](app-insights-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="35475-165">[Learn more about Application Insights tools in Visual Studio](app-insights-visual-studio.md).</span></span>

<a name="monitor"></a>
### <a name="see-telemetry-in-web-portal"></a><span data-ttu-id="35475-166">Telemetrie bekijken in de webportal</span><span class="sxs-lookup"><span data-stu-id="35475-166">See telemetry in web portal</span></span>

<span data-ttu-id="35475-167">U ziet ook telemetrie in Application Insights-webportal hello (tenzij u kiest voor tooinstall alleen Hallo SDK).</span><span class="sxs-lookup"><span data-stu-id="35475-167">You can also see telemetry in hello Application Insights web portal (unless you chose tooinstall only hello SDK).</span></span> <span data-ttu-id="35475-168">Hallo-portal biedt meer grafieken, hulpprogramma's voor analyse en weergaven voor cross-onderdeel dan Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="35475-168">hello portal has more charts, analytic tools, and cross-component views than Visual Studio.</span></span> <span data-ttu-id="35475-169">Hallo-portal biedt ook waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="35475-169">hello portal also provides alerts.</span></span>

<span data-ttu-id="35475-170">Open uw Application Insights-resource.</span><span class="sxs-lookup"><span data-stu-id="35475-170">Open your Application Insights resource.</span></span> <span data-ttu-id="35475-171">Een toohello aanmelden [Azure-portal](https://portal.azure.com/) en vinden er of met de rechtermuisknop op Hallo project in Visual Studio en laat deze te gaan.</span><span class="sxs-lookup"><span data-stu-id="35475-171">Either sign in toohello [Azure portal](https://portal.azure.com/) and find it there, or right-click hello project in Visual Studio, and let it take you there.</span></span>

![Schermopname van Visual Studio die laat zien hoe tooopen Hallo Application Insights-portal](./media/app-insights-asp-net/appinsights-04-openPortal.png)

> [!NOTE]
> <span data-ttu-id="35475-173">Als u een access-fout krijgt: hebt u meer dan één set referenties van Microsoft en u bent aangemeld met de verkeerde set Hallo?</span><span class="sxs-lookup"><span data-stu-id="35475-173">If you get an access error: Do you have more than one set of Microsoft credentials, and are you signed in with hello wrong set?</span></span> <span data-ttu-id="35475-174">In de portal Hallo afmelden en opnieuw aanmelden.</span><span class="sxs-lookup"><span data-stu-id="35475-174">In hello portal, sign out and sign in again.</span></span>

<span data-ttu-id="35475-175">Hallo wordt geopend in een weergave van Hallo telemetrie van uw app.</span><span class="sxs-lookup"><span data-stu-id="35475-175">hello portal opens on a view of hello telemetry from your app.</span></span>

![Schermopname van Application Insights-overzichtspagina](./media/app-insights-asp-net/66.png)

<span data-ttu-id="35475-177">Klik in Hallo portal op een tegel of grafiek toosee meer details.</span><span class="sxs-lookup"><span data-stu-id="35475-177">In hello portal, click any tile or chart toosee more detail.</span></span>

<span data-ttu-id="35475-178">[Meer informatie over het gebruik van Application Insights in hello Azure-portal](app-insights-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="35475-178">[Learn more about using Application Insights in hello Azure portal](app-insights-dashboards.md).</span></span>

## <a name="step-4-publish-your-app"></a><span data-ttu-id="35475-179">Stap 4: uw app publiceren</span><span class="sxs-lookup"><span data-stu-id="35475-179">Step 4: Publish your app</span></span>
<span data-ttu-id="35475-180">Uw app tooyour IIS-server of tooAzure publiceren.</span><span class="sxs-lookup"><span data-stu-id="35475-180">Publish your app tooyour IIS server or tooAzure.</span></span> <span data-ttu-id="35475-181">Bekijk [livestream metrische gegevens](app-insights-metrics-explorer.md#live-metrics-stream) toomake ervoor dat alles goed wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="35475-181">Watch [Live Metrics Stream](app-insights-metrics-explorer.md#live-metrics-stream) toomake sure everything is running smoothly.</span></span>

<span data-ttu-id="35475-182">Uw telemetrie wordt opgebouwd in Hallo Application Insights-portal, waar u kunt metrische gegevens controleren, doorzoeken uw Telemetrie en instellen van [dashboards](app-insights-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="35475-182">Your telemetry builds up in hello Application Insights portal, where you can monitor metrics, search your telemetry, and set up [dashboards](app-insights-dashboards.md).</span></span> <span data-ttu-id="35475-183">U kunt ook Hallo krachtige [querytaal van logboekanalyse](https://docs.loganalytics.io/) tooanalyze gebruik en prestaties of toofind specifieke gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="35475-183">You can also use hello powerful [Log Analytics query language](https://docs.loganalytics.io/) tooanalyze usage and performance, or toofind specific events.</span></span>

<span data-ttu-id="35475-184">U kunt tooanalyze ook blijven uw telemetrie in [Visual Studio](app-insights-visual-studio.md), met hulpprogramma's zoals diagnostische gegevens doorzoeken en [trends](app-insights-visual-studio-trends.md).</span><span class="sxs-lookup"><span data-stu-id="35475-184">You can also continue tooanalyze your telemetry in [Visual Studio](app-insights-visual-studio.md), with tools such as diagnostic search and [trends](app-insights-visual-studio-trends.md).</span></span>

> [!NOTE]
> <span data-ttu-id="35475-185">Als uw app voldoende telemetrie tooapproach hello verzendt [beperking limieten](app-insights-pricing.md#limits-summary), automatische [steekproeven](app-insights-sampling.md) switches op.</span><span class="sxs-lookup"><span data-stu-id="35475-185">If your app sends enough telemetry tooapproach hello [throttling limits](app-insights-pricing.md#limits-summary), automatic [sampling](app-insights-sampling.md) switches on.</span></span> <span data-ttu-id="35475-186">Steekproeven vermindert Hallo hoeveelheid telemetrie van uw app verzonden behoud gecorreleerde gegevens voor diagnostische doeleinden.</span><span class="sxs-lookup"><span data-stu-id="35475-186">Sampling reduces hello quantity of telemetry sent from your app, while preserving correlated data for diagnostic purposes.</span></span>
>
>

## <span data-ttu-id="35475-187"><a name="land"></a> U bent nu klaar</span><span class="sxs-lookup"><span data-stu-id="35475-187"><a name="land"></a> You're all set</span></span>

<span data-ttu-id="35475-188">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="35475-188">Congratulations!</span></span> <span data-ttu-id="35475-189">U Hallo Application Insights-pakket geïnstalleerd in uw app en het toosend telemetrie toohello Application Insights-service hebt geconfigureerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="35475-189">You installed hello Application Insights package in your app, and configured it toosend telemetry toohello Application Insights service on Azure.</span></span>

![Diagram van verplaatsing van telemetrie](./media/app-insights-asp-net/01-scheme.png)

<span data-ttu-id="35475-191">Hello Azure-resource die telemetrie van uw app ontvangt wordt geïdentificeerd door een *instrumentatiesleutel*.</span><span class="sxs-lookup"><span data-stu-id="35475-191">hello Azure resource that receives your app's telemetry is identified by an *instrumentation key*.</span></span> <span data-ttu-id="35475-192">U vindt deze sleutel in Hallo ApplicationInsights.config-bestand.</span><span class="sxs-lookup"><span data-stu-id="35475-192">You'll find this key in hello ApplicationInsights.config file.</span></span>


## <a name="upgrade-toofuture-sdk-versions"></a><span data-ttu-id="35475-193">De SDK-versies toofuture bijwerken</span><span class="sxs-lookup"><span data-stu-id="35475-193">Upgrade toofuture SDK versions</span></span>
<span data-ttu-id="35475-194">tooupgrade tooa [nieuwe release van Hallo SDK](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases)Open Hallo **NuGet-Pakketbeheer** opnieuw, en filteren op geïnstalleerde pakketten.</span><span class="sxs-lookup"><span data-stu-id="35475-194">tooupgrade tooa [new release of hello SDK](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases), open hello **NuGet package manager** again, and filter on installed packages.</span></span> <span data-ttu-id="35475-195">Selecteer **Microsoft.ApplicationInsights.Web** en kies **Upgraden**.</span><span class="sxs-lookup"><span data-stu-id="35475-195">Select **Microsoft.ApplicationInsights.Web**, and choose **Upgrade**.</span></span>

<span data-ttu-id="35475-196">Als u alle aanpassingen tooApplicationInsights.config genomen, een kopie van deze opslaan voordat u een upgrade.</span><span class="sxs-lookup"><span data-stu-id="35475-196">If you made any customizations tooApplicationInsights.config, save a copy of it before you upgrade.</span></span> <span data-ttu-id="35475-197">Vervolgens uw wijzigingen samen in de nieuwe versie Hallo.</span><span class="sxs-lookup"><span data-stu-id="35475-197">Then, merge your changes into hello new version.</span></span>

## <a name="video"></a><span data-ttu-id="35475-198">Video</span><span class="sxs-lookup"><span data-stu-id="35475-198">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="35475-199">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="35475-199">Next steps</span></span>

### <a name="more-telemetry"></a><span data-ttu-id="35475-200">Meer telemetrie</span><span class="sxs-lookup"><span data-stu-id="35475-200">More telemetry</span></span>

* <span data-ttu-id="35475-201">**[Laadgegevens voor browser en pagina](app-insights-javascript.md)**: voeg een codefragment in uw webpagina's in.</span><span class="sxs-lookup"><span data-stu-id="35475-201">**[Browser and page load data](app-insights-javascript.md)** - Insert a code snippet in your web pages.</span></span>
* <span data-ttu-id="35475-202">**[Gedetailleerde bewaking van afhankelijkheid en uitzonderingen](app-insights-monitor-performance-live-website-now.md)**: installeer Status Monitor op uw server.</span><span class="sxs-lookup"><span data-stu-id="35475-202">**[Get more detailed dependency and exception monitoring](app-insights-monitor-performance-live-website-now.md)** - Install Status Monitor on your server.</span></span>
* <span data-ttu-id="35475-203">**[Aangepaste gebeurtenissen code](app-insights-api-custom-events-metrics.md)**  toocount, tijd en acties van de gebruiker te meten.</span><span class="sxs-lookup"><span data-stu-id="35475-203">**[Code custom events](app-insights-api-custom-events-metrics.md)** toocount, time, or measure user actions.</span></span>
* <span data-ttu-id="35475-204">**[Haal logboekgegevens op](app-insights-asp-net-trace-logs.md)**: koppel logboekgegevens aan uw telemetrie.</span><span class="sxs-lookup"><span data-stu-id="35475-204">**[Get log data](app-insights-asp-net-trace-logs.md)** - Correlate log data with your telemetry.</span></span>

### <a name="analysis"></a><span data-ttu-id="35475-205">Analyse</span><span class="sxs-lookup"><span data-stu-id="35475-205">Analysis</span></span>

* <span data-ttu-id="35475-206">**[Met Application Insights werken in Visual Studio](app-insights-visual-studio.md)**</span><span class="sxs-lookup"><span data-stu-id="35475-206">**[Working with Application Insights in Visual Studio](app-insights-visual-studio.md)**</span></span><br/><span data-ttu-id="35475-207">Bevat informatie over foutopsporing met telemetrie, diagnostische gegevens doorzoeken en detailanalyse toocode.</span><span class="sxs-lookup"><span data-stu-id="35475-207">Includes information about debugging with telemetry, diagnostic search, and drill through toocode.</span></span>
* <span data-ttu-id="35475-208">**[Werken met Hallo Application Insights-portal](app-insights-dashboards.md)**</span><span class="sxs-lookup"><span data-stu-id="35475-208">**[Working with hello Application Insights portal](app-insights-dashboards.md)**</span></span><br/> <span data-ttu-id="35475-209">Bevat informatie over dashboards, krachtige hulpprogramma's voor diagnose en analyse, waarschuwingen, een live afhankelijkheidskaart van uw toepassing en exportmogelijkheden voor telemetrie.</span><span class="sxs-lookup"><span data-stu-id="35475-209">Includes information about dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and telemetry export.</span></span>
* <span data-ttu-id="35475-210">**[Analytics](app-insights-analytics-tour.md)**  -Hallo krachtige querytaal.</span><span class="sxs-lookup"><span data-stu-id="35475-210">**[Analytics](app-insights-analytics-tour.md)** - hello powerful query language.</span></span>

### <a name="alerts"></a><span data-ttu-id="35475-211">Waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="35475-211">Alerts</span></span>

* <span data-ttu-id="35475-212">[Beschikbaarheidstests](app-insights-monitor-web-app-availability.md): tests maken toomake ervoor dat uw site op Hallo web zichtbaar is.</span><span class="sxs-lookup"><span data-stu-id="35475-212">[Availability tests](app-insights-monitor-web-app-availability.md): Create tests toomake sure your site is visible on hello web.</span></span>
* <span data-ttu-id="35475-213">[Diagnostische gegevens van smartcard](app-insights-proactive-diagnostics.md): deze tests uitgevoerd automatisch, dus u geen toodo alles tooset hebt deze.</span><span class="sxs-lookup"><span data-stu-id="35475-213">[Smart diagnostics](app-insights-proactive-diagnostics.md): These tests run automatically, so you don't have toodo anything tooset them up.</span></span> <span data-ttu-id="35475-214">Deze geeft aan of een app een ongebruikelijk aantal mislukte aanvragen heeft.</span><span class="sxs-lookup"><span data-stu-id="35475-214">They tell you if your app has an unusual rate of failed requests.</span></span>
* <span data-ttu-id="35475-215">[Metrische waarschuwingen](app-insights-alerts.md): Stel deze toowarn u als een waarde een drempelwaarde overschrijdt.</span><span class="sxs-lookup"><span data-stu-id="35475-215">[Metric alerts](app-insights-alerts.md): Set these toowarn you if a metric crosses a threshold.</span></span> <span data-ttu-id="35475-216">U kunt deze instellen op aangepaste metrische gegevens die u in uw app codeert.</span><span class="sxs-lookup"><span data-stu-id="35475-216">You can set them on custom metrics that you code into your app.</span></span>

### <a name="automation"></a><span data-ttu-id="35475-217">Automation</span><span class="sxs-lookup"><span data-stu-id="35475-217">Automation</span></span>

* [<span data-ttu-id="35475-218">Het maken van een Application Insights-resource automatiseren</span><span class="sxs-lookup"><span data-stu-id="35475-218">Automate creating an Application Insights resource</span></span>](app-insights-powershell.md)
