---
title: Web-app-analyse voor ASP.NET instellen met Azure Application Insights | Microsoft Docs
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
ms.openlocfilehash: cb247ee68da88265f7c51258644064463d44f8b5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="set-up-application-insights-for-your-aspnet-website"></a><span data-ttu-id="fb8a8-103">Application Insights instellen voor uw ASP.NET-website</span><span class="sxs-lookup"><span data-stu-id="fb8a8-103">Set up Application Insights for your ASP.NET website</span></span>

<span data-ttu-id="fb8a8-104">Met deze procedure wordt uw ASP.NET web-app zo geconfigureerd dat telemetrie wordt verzonden naar de [Azure Application Insights](app-insights-overview.md)-service.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-104">This procedure configures your ASP.NET web app to send telemetry to the [Azure Application Insights](app-insights-overview.md) service.</span></span> <span data-ttu-id="fb8a8-105">Dit werkt voor ASP.NET-apps die worden gehost op uw eigen IIS-server of in de cloud.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-105">It works for ASP.NET apps that are hosted either in your own IIS server or in the Cloud.</span></span> <span data-ttu-id="fb8a8-106">U beschikt over grafieken en een krachtige querytaal waarmee u meer inzicht krijgt in de prestaties van uw app en hoe mensen deze gebruiken. Daarnaast ontvangt u meldingen over fouten of prestatieproblemen.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-106">You get charts and a powerful query language that help you understand the performance of your app and how people are using it, plus automatic alerts on failures or performance issues.</span></span> <span data-ttu-id="fb8a8-107">Veel ontwikkelaars gebruiken deze functies graag, maar u kunt de telemetrie desgewenst uitbreiden en aanpassen.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-107">Many developers find these features great as they are, but you can also extend and customize the telemetry if you need to.</span></span>

<span data-ttu-id="fb8a8-108">Voor de Setup zijn maar een paar klikken nodig in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-108">Setup takes just a few clicks in Visual Studio.</span></span> <span data-ttu-id="fb8a8-109">U kunt kosten besparen door de hoeveelheid telemetrie te beperken.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-109">You have the option to avoid charges by limiting the volume of telemetry.</span></span> <span data-ttu-id="fb8a8-110">Hiermee kunt u experimenteren en fouten opsporen of een site met weinig gebruikers bewaken.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-110">This allows you to experiment and debug, or to monitor a site with not many users.</span></span> <span data-ttu-id="fb8a8-111">Wanneer u besluit dat u de productiesite wilt bewaken, kunt u de limiet later eenvoudig verhogen.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-111">When you decide you want to go ahead and monitor your production site, it's easy to raise the limit later.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="fb8a8-112">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="fb8a8-112">Before you start</span></span>
<span data-ttu-id="fb8a8-113">U hebt de volgende zaken nodig:</span><span class="sxs-lookup"><span data-stu-id="fb8a8-113">You need:</span></span>

* <span data-ttu-id="fb8a8-114">Visual Studio 2013 update 3 of later.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-114">Visual Studio 2013 update 3 or later.</span></span> <span data-ttu-id="fb8a8-115">Later is beter.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-115">Later is better.</span></span>
* <span data-ttu-id="fb8a8-116">Een abonnement op [Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="fb8a8-116">A subscription to [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="fb8a8-117">Als uw team of organisatie een Azure-abonnement heeft, kan de eigenaar u toevoegen met behulp van uw [Microsoft-account](http://live.com).</span><span class="sxs-lookup"><span data-stu-id="fb8a8-117">If your team or organization has an Azure subscription, the owner can add you to it, by using your [Microsoft account](http://live.com).</span></span>

<span data-ttu-id="fb8a8-118">Er zijn ook andere onderwerpen die u kunt bekijken als u geïnteresseerd bent in:</span><span class="sxs-lookup"><span data-stu-id="fb8a8-118">There are alternative topics to look at if you are interested in:</span></span>

* [<span data-ttu-id="fb8a8-119">Een web-app instrumenteren tijdens runtime</span><span class="sxs-lookup"><span data-stu-id="fb8a8-119">Instrumenting a web app at runtime</span></span>](app-insights-monitor-performance-live-website-now.md)
* [<span data-ttu-id="fb8a8-120">Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="fb8a8-120">Azure Cloud Services</span></span>](app-insights-cloudservices.md)

## <span data-ttu-id="fb8a8-121"><a name="ide"></a> Stap 1: de Application Insights-SDK toevoegen</span><span class="sxs-lookup"><span data-stu-id="fb8a8-121"><a name="ide"></a> Step 1: Add the Application Insights SDK</span></span>

<span data-ttu-id="fb8a8-122">Klik in Solution Explorer met de rechtermuisknop op het web-app-project. Kies **Toevoegen** > **Application Insights Telemetry...** of **Application Insights configureren**.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-122">Right-click your web app project in Solution Explorer, and choose **Add** > **Application Insights Telemetry...** or **Configure Application Insights**.</span></span>

![Schermopname van Solution Explorer waarin Application Insights Telemetry toevoegen is gemarkeerd](./media/app-insights-asp-net/appinsights-03-addExisting.png)

<span data-ttu-id="fb8a8-124">(In Visual Studio 2015 is er ook een optie om Application Insights toe te voegen aan het dialoogvenster Nieuw project.)</span><span class="sxs-lookup"><span data-stu-id="fb8a8-124">(In Visual Studio 2015, there's also an option to add Application Insights in the New Project dialog.)</span></span>

<span data-ttu-id="fb8a8-125">Ga door naar de pagina voor Application Insights-configuratie:</span><span class="sxs-lookup"><span data-stu-id="fb8a8-125">Continue to the Application Insights configuration page:</span></span>

![Schermopname van de pagina Uw app registreren bij Application Insights](./media/app-insights-asp-net/visual-studio-register-dialog.png)

<span data-ttu-id="fb8a8-127">**a.**</span><span class="sxs-lookup"><span data-stu-id="fb8a8-127">**a.**</span></span> <span data-ttu-id="fb8a8-128">Selecteer het account en het abonnement die u gebruikt voor toegang tot Azure.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-128">Select the account and subscription that you use to access Azure.</span></span>

<span data-ttu-id="fb8a8-129">**b.**</span><span class="sxs-lookup"><span data-stu-id="fb8a8-129">**b.**</span></span> <span data-ttu-id="fb8a8-130">Selecteer de resource in Azure die u wilt gebruiken om de gegevens van uw app te bekijken.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-130">Select the resource in Azure where you want to see the data from your app.</span></span> <span data-ttu-id="fb8a8-131">Meestal:</span><span class="sxs-lookup"><span data-stu-id="fb8a8-131">Usually:</span></span>

* <span data-ttu-id="fb8a8-132">Gebruik [één resource voor verschillende onderdelen](app-insights-monitor-multi-role-apps.md) van één toepassing.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-132">Use a [single resource for different components](app-insights-monitor-multi-role-apps.md) of a single application.</span></span> 
* <span data-ttu-id="fb8a8-133">Maak afzonderlijke resources voor niet-gerelateerde toepassingen.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-133">Create separate resources for unrelated applications.</span></span>
 
<span data-ttu-id="fb8a8-134">Als u een resourcegroep of locatie wilt instellen voor het opslaan van uw gegevens, klikt u op **Instellingen configureren**.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-134">If you want to set the resource group or the location where your data is stored, click **Configure settings**.</span></span> <span data-ttu-id="fb8a8-135">Resourcegroepen worden gebruikt om toegang tot gegevens te beheren.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-135">Resource groups are used to control access to data.</span></span> <span data-ttu-id="fb8a8-136">Als u verschillende apps hebt die deel uitmaken van hetzelfde systeem, kunt u hun Application Insights-gegevens in dezelfde resourcegroep plaatsen.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-136">For example, if you have several apps that form part of the same system, you might put their Application Insights data in the same resource group.</span></span>

<span data-ttu-id="fb8a8-137">**c.**</span><span class="sxs-lookup"><span data-stu-id="fb8a8-137">**c.**</span></span> <span data-ttu-id="fb8a8-138">Stel de limiet in op het gratis gegevensvolume om kosten te voorkomen.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-138">Set a cap at the free data volume limit, to avoid charges.</span></span> <span data-ttu-id="fb8a8-139">Application Insights is gratis te gebruiken, tot een bepaald telemetrievolume.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-139">Application Insights is free up to a certain volume of telemetry.</span></span> <span data-ttu-id="fb8a8-140">Wanneer de resource is gemaakt, kunt u de selectie in de portal wijzigen door naar **Functies en prijzen** > **Gegevensvolumebeheer** > **Dagelijkse volumelimiet** te gaan.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-140">After the resource is created, you can change your selection in the portal by opening  **Features + pricing** > **Data volume management** > **Daily volume cap**.</span></span>

<span data-ttu-id="fb8a8-141">**d.**</span><span class="sxs-lookup"><span data-stu-id="fb8a8-141">**d.**</span></span> <span data-ttu-id="fb8a8-142">Klik op **Registreren** om Application Insights te configureren voor uw web-app.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-142">Click **Register** to go ahead and configure Application Insights for your web app.</span></span> <span data-ttu-id="fb8a8-143">Er wordt telemetrie verzonden naar [Azure Portal](https://portal.azure.com), zowel tijdens de foutopsporing als na het publiceren van de app.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-143">Telemetry will be sent to the [Azure portal](https://portal.azure.com), both during debugging and after you have published your app.</span></span>

<span data-ttu-id="fb8a8-144">**e.**</span><span class="sxs-lookup"><span data-stu-id="fb8a8-144">**e.**</span></span> <span data-ttu-id="fb8a8-145">Als u geen telemetrie naar de portal wilt verzenden tijdens de foutopsporing, voegt u de Application Insights SDK toe aan de app, maar configureert u geen resource in de portal.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-145">If you don't want to send telemetry to the portal while you're debugging, just add the Application Insights SDK to your app but don't configure a resource in the portal.</span></span> <span data-ttu-id="fb8a8-146">U kunt de telemetrie in Visual Studio bekijken tijdens de foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-146">You will be able to see telemetry in Visual Studio while you are debugging.</span></span> <span data-ttu-id="fb8a8-147">U kunt later terugkeren naar deze configuratiepagina, of u kunt wachten tot de app is geïmplementeerd en [telemetrie inschakelen tijdens runtime](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="fb8a8-147">Later, you can return to this configuration page, or you could wait until after you have deployed your app and [switch on telemetry at run time](app-insights-monitor-performance-live-website-now.md).</span></span>


## <span data-ttu-id="fb8a8-148"><a name="run"></a> Stap 2: uw app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="fb8a8-148"><a name="run"></a> Step 2: Run your app</span></span>
<span data-ttu-id="fb8a8-149">Voer uw app uit met F5.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-149">Run your app with F5.</span></span> <span data-ttu-id="fb8a8-150">Open verschillende pagina's om telemetrie te genereren.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-150">Open different pages to generate some telemetry.</span></span>

<span data-ttu-id="fb8a8-151">In Visual Studio ziet u het aantal gebeurtenissen dat is geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-151">In Visual Studio, you see a count of the events that have been logged.</span></span>

![Schermopname van Visual Studio.](./media/app-insights-asp-net/54.png)

## <a name="step-3-see-your-telemetry"></a><span data-ttu-id="fb8a8-154">Stap 3: uw telemetrie weergeven</span><span class="sxs-lookup"><span data-stu-id="fb8a8-154">Step 3: See your telemetry</span></span>
<span data-ttu-id="fb8a8-155">U ziet uw telemetrie in Visual Studio of in de Application Insights-webportal.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-155">You can see your telemetry either in Visual Studio or in the Application Insights web portal.</span></span> <span data-ttu-id="fb8a8-156">Zoek telemetrie in Visual Studio om fouten in de app op te sporen.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-156">Search telemetry in Visual Studio to help you debug your app.</span></span> <span data-ttu-id="fb8a8-157">Bewaak de prestaties en het gebruik in de webportal wanneer het systeem live is.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-157">Monitor performance and usage in the web portal when your system is live.</span></span> 

### <a name="see-your-telemetry-in-visual-studio"></a><span data-ttu-id="fb8a8-158">De telemetrie bekijken in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fb8a8-158">See your telemetry in Visual Studio</span></span>

<span data-ttu-id="fb8a8-159">Open het venster Application Insights in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-159">In Visual Studio, open the Application Insights window.</span></span> <span data-ttu-id="fb8a8-160">Klik op de knop **Application Insights** of klik met de rechtermuisknop op uw project in Solution Explorer, selecteer vervolgens **Application Insights** en klik daarna op **Search Live Telemetry** (Live telemetrie zoeken).</span><span class="sxs-lookup"><span data-stu-id="fb8a8-160">Either click the **Application Insights** button, or right-click your project in Solution Explorer, select **Application Insights**, and then click **Search Live Telemetry**.</span></span>

<span data-ttu-id="fb8a8-161">Ga in het venster Visual Studio Application Insights naar de weergave **Gegevens van foutopsporingssessie** voor telemetrie die is gegenereerd aan de serverzijde van uw app.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-161">In the Visual Studio Application Insights Search window, see the **Data from Debug session** view for telemetry generated in the server side of your app.</span></span> <span data-ttu-id="fb8a8-162">Experimenteer met de filters en klik op een gebeurtenis voor meer details.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-162">Experiment with the filters, and click any event to see more detail.</span></span>

![Schermopname van de weergave Gegevens van foutopsporingssessie in het venster Application Insights.](./media/app-insights-asp-net/55.png)

> [!NOTE]
> <span data-ttu-id="fb8a8-164">Als u geen gegevens ziet, controleert u of het tijdsbereik correct is en klikt u op het pictogram Zoeken.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-164">If you don't see any data, make sure the time range is correct, and click the Search icon.</span></span>

<span data-ttu-id="fb8a8-165">[Meer informatie over Application Insights-hulpprogramma's in Visual Studio](app-insights-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="fb8a8-165">[Learn more about Application Insights tools in Visual Studio](app-insights-visual-studio.md).</span></span>

<a name="monitor"></a>
### <a name="see-telemetry-in-web-portal"></a><span data-ttu-id="fb8a8-166">Telemetrie bekijken in de webportal</span><span class="sxs-lookup"><span data-stu-id="fb8a8-166">See telemetry in web portal</span></span>

<span data-ttu-id="fb8a8-167">U kunt de telemetrie ook in de Application Insights-webportal bekijken (tenzij u ervoor hebt gekozen alleen de SDK te installeren).</span><span class="sxs-lookup"><span data-stu-id="fb8a8-167">You can also see telemetry in the Application Insights web portal (unless you chose to install only the SDK).</span></span> <span data-ttu-id="fb8a8-168">De portal bevat meer grafieken, analysefuncties en weergaven met meerdere onderdelen dan Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-168">The portal has more charts, analytic tools, and cross-component views than Visual Studio.</span></span> <span data-ttu-id="fb8a8-169">De portal bevat ook waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-169">The portal also provides alerts.</span></span>

<span data-ttu-id="fb8a8-170">Open uw Application Insights-resource.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-170">Open your Application Insights resource.</span></span> <span data-ttu-id="fb8a8-171">Meld u aan bij [Azure Portal](https://portal.azure.com/) en zoek de resource daar of klik met de rechtermuisknop op het project in Visual Studio en laat u daarheen brengen.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-171">Either sign in to the [Azure portal](https://portal.azure.com/) and find it there, or right-click the project in Visual Studio, and let it take you there.</span></span>

![Schermopname van Visual Studio die toont hoe u de Application Insights-portal kunt openen](./media/app-insights-asp-net/appinsights-04-openPortal.png)

> [!NOTE]
> <span data-ttu-id="fb8a8-173">Als u een toegangsfout ontvangt: hebt u meer dan één set Microsoft-referenties en bent u aangemeld met de verkeerde set?</span><span class="sxs-lookup"><span data-stu-id="fb8a8-173">If you get an access error: Do you have more than one set of Microsoft credentials, and are you signed in with the wrong set?</span></span> <span data-ttu-id="fb8a8-174">Meld u af en opnieuw aan in de portal.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-174">In the portal, sign out and sign in again.</span></span>

<span data-ttu-id="fb8a8-175">De portal wordt geopend met een weergave van de telemetrie van uw app.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-175">The portal opens on a view of the telemetry from your app.</span></span>

![Schermopname van Application Insights-overzichtspagina](./media/app-insights-asp-net/66.png)

<span data-ttu-id="fb8a8-177">Klik in de portal op een tegel of grafiek om meer details te bekijken.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-177">In the portal, click any tile or chart to see more detail.</span></span>

<span data-ttu-id="fb8a8-178">[Meer informatie over het gebruik van Application Insights in Azure Portal](app-insights-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="fb8a8-178">[Learn more about using Application Insights in the Azure portal](app-insights-dashboards.md).</span></span>

## <a name="step-4-publish-your-app"></a><span data-ttu-id="fb8a8-179">Stap 4: uw app publiceren</span><span class="sxs-lookup"><span data-stu-id="fb8a8-179">Step 4: Publish your app</span></span>
<span data-ttu-id="fb8a8-180">Publiceer uw app op de IIS-server of op Azure.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-180">Publish your app to your IIS server or to Azure.</span></span> <span data-ttu-id="fb8a8-181">Bekijk de livestream met metrische gegevens in [Live Metrics Stream](app-insights-metrics-explorer.md#live-metrics-stream) om te controleren of alles goed werkt.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-181">Watch [Live Metrics Stream](app-insights-metrics-explorer.md#live-metrics-stream) to make sure everything is running smoothly.</span></span>

<span data-ttu-id="fb8a8-182">Uw telemetrie wordt opgebouwd in de Application Insights-portal, waar u metrische gegevens kunt controleren, uw telemetrie kunt doorzoeken en [dashboards](app-insights-dashboards.md) kunt instellen.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-182">Your telemetry builds up in the Application Insights portal, where you can monitor metrics, search your telemetry, and set up [dashboards](app-insights-dashboards.md).</span></span> <span data-ttu-id="fb8a8-183">U kunt ook de krachtige [querytaal van Log Analytics](https://docs.loganalytics.io/) gebruiken om gebruik en prestaties te analyseren of om specifieke gebeurtenissen te zoeken.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-183">You can also use the powerful [Log Analytics query language](https://docs.loganalytics.io/) to analyze usage and performance, or to find specific events.</span></span>

<span data-ttu-id="fb8a8-184">U kunt uw telemetrie ook blijven analyseren in [Visual Studio](app-insights-visual-studio.md) met hulpprogramma's voor diagnostisch zoeken en [Trends](app-insights-visual-studio-trends.md).</span><span class="sxs-lookup"><span data-stu-id="fb8a8-184">You can also continue to analyze your telemetry in [Visual Studio](app-insights-visual-studio.md), with tools such as diagnostic search and [trends](app-insights-visual-studio-trends.md).</span></span>

> [!NOTE]
> <span data-ttu-id="fb8a8-185">Als uw app zoveel telemetrie verzendt dat de[beperkingslimieten](app-insights-pricing.md#limits-summary) worden benaderd, worden automatisch [steekproeven](app-insights-sampling.md) ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-185">If your app sends enough telemetry to approach the [throttling limits](app-insights-pricing.md#limits-summary), automatic [sampling](app-insights-sampling.md) switches on.</span></span> <span data-ttu-id="fb8a8-186">Met steekproeven vermindert u de hoeveelheid telemetrie die vanuit uw app wordt verzonden, maar behoudt u gecorreleerde gegevens voor diagnostische doeleinden.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-186">Sampling reduces the quantity of telemetry sent from your app, while preserving correlated data for diagnostic purposes.</span></span>
>
>

## <span data-ttu-id="fb8a8-187"><a name="land"></a> U bent nu klaar</span><span class="sxs-lookup"><span data-stu-id="fb8a8-187"><a name="land"></a> You're all set</span></span>

<span data-ttu-id="fb8a8-188">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-188">Congratulations!</span></span> <span data-ttu-id="fb8a8-189">U hebt het pakket Application Insights geïnstalleerd in uw app en dit zo geconfigureerd dat telemetrie wordt verzonden naar de Application Insights-service in Azure.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-189">You installed the Application Insights package in your app, and configured it to send telemetry to the Application Insights service on Azure.</span></span>

![Diagram van verplaatsing van telemetrie](./media/app-insights-asp-net/01-scheme.png)

<span data-ttu-id="fb8a8-191">De Azure-resource die de telemetrie van uw app ontvangt, wordt aangeduid met een *instrumentatiesleutel*.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-191">The Azure resource that receives your app's telemetry is identified by an *instrumentation key*.</span></span> <span data-ttu-id="fb8a8-192">U vindt deze sleutel in het bestand ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-192">You'll find this key in the ApplicationInsights.config file.</span></span>


## <a name="upgrade-to-future-sdk-versions"></a><span data-ttu-id="fb8a8-193">Upgraden naar toekomstige SDK-versies</span><span class="sxs-lookup"><span data-stu-id="fb8a8-193">Upgrade to future SDK versions</span></span>
<span data-ttu-id="fb8a8-194">Als u wilt upgraden naar een [nieuwe release van de SDK](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases), opent u **NuGet-pakketbeheer** opnieuw en filtert u op geïnstalleerde pakketten.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-194">To upgrade to a [new release of the SDK](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases), open the **NuGet package manager** again, and filter on installed packages.</span></span> <span data-ttu-id="fb8a8-195">Selecteer **Microsoft.ApplicationInsights.Web** en kies **Upgraden**.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-195">Select **Microsoft.ApplicationInsights.Web**, and choose **Upgrade**.</span></span>

<span data-ttu-id="fb8a8-196">Als u aanpassingen in ApplicationInsights.config hebt aangebracht, slaat u hiervan een kopie op voordat u de upgrade uitvoert.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-196">If you made any customizations to ApplicationInsights.config, save a copy of it before you upgrade.</span></span> <span data-ttu-id="fb8a8-197">Voeg de wijzigingen vervolgens samen in de nieuwe versie.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-197">Then, merge your changes into the new version.</span></span>

## <a name="video"></a><span data-ttu-id="fb8a8-198">Video</span><span class="sxs-lookup"><span data-stu-id="fb8a8-198">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="fb8a8-199">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fb8a8-199">Next steps</span></span>

### <a name="more-telemetry"></a><span data-ttu-id="fb8a8-200">Meer telemetrie</span><span class="sxs-lookup"><span data-stu-id="fb8a8-200">More telemetry</span></span>

* <span data-ttu-id="fb8a8-201">**[Laadgegevens voor browser en pagina](app-insights-javascript.md)**: voeg een codefragment in uw webpagina's in.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-201">**[Browser and page load data](app-insights-javascript.md)** - Insert a code snippet in your web pages.</span></span>
* <span data-ttu-id="fb8a8-202">**[Gedetailleerde bewaking van afhankelijkheid en uitzonderingen](app-insights-monitor-performance-live-website-now.md)**: installeer Status Monitor op uw server.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-202">**[Get more detailed dependency and exception monitoring](app-insights-monitor-performance-live-website-now.md)** - Install Status Monitor on your server.</span></span>
* <span data-ttu-id="fb8a8-203">**[Codeer aangepaste gebeurtenissen](app-insights-api-custom-events-metrics.md)** om gebruikersacties te tellen, te meten of de tijdsduur hiervan te bepalen.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-203">**[Code custom events](app-insights-api-custom-events-metrics.md)** to count, time, or measure user actions.</span></span>
* <span data-ttu-id="fb8a8-204">**[Haal logboekgegevens op](app-insights-asp-net-trace-logs.md)**: koppel logboekgegevens aan uw telemetrie.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-204">**[Get log data](app-insights-asp-net-trace-logs.md)** - Correlate log data with your telemetry.</span></span>

### <a name="analysis"></a><span data-ttu-id="fb8a8-205">Analyse</span><span class="sxs-lookup"><span data-stu-id="fb8a8-205">Analysis</span></span>

* <span data-ttu-id="fb8a8-206">**[Met Application Insights werken in Visual Studio](app-insights-visual-studio.md)**</span><span class="sxs-lookup"><span data-stu-id="fb8a8-206">**[Working with Application Insights in Visual Studio](app-insights-visual-studio.md)**</span></span><br/><span data-ttu-id="fb8a8-207">Bevat informatie over foutopsporing met telemetrie, het doorzoeken van diagnostische gegevens en het in detail analyseren van code.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-207">Includes information about debugging with telemetry, diagnostic search, and drill through to code.</span></span>
* <span data-ttu-id="fb8a8-208">**[Werken met de Application Insights-portal](app-insights-dashboards.md)**</span><span class="sxs-lookup"><span data-stu-id="fb8a8-208">**[Working with the Application Insights portal](app-insights-dashboards.md)**</span></span><br/> <span data-ttu-id="fb8a8-209">Bevat informatie over dashboards, krachtige hulpprogramma's voor diagnose en analyse, waarschuwingen, een live afhankelijkheidskaart van uw toepassing en exportmogelijkheden voor telemetrie.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-209">Includes information about dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and telemetry export.</span></span>
* <span data-ttu-id="fb8a8-210">**[Analyse](app-insights-analytics-tour.md)**: de krachtige querytaal.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-210">**[Analytics](app-insights-analytics-tour.md)** - The powerful query language.</span></span>

### <a name="alerts"></a><span data-ttu-id="fb8a8-211">Waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="fb8a8-211">Alerts</span></span>

* <span data-ttu-id="fb8a8-212">[Beschikbaarheidstests](app-insights-monitor-web-app-availability.md): maak tests om ervoor te zorgen dat uw site zichtbaar is op internet.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-212">[Availability tests](app-insights-monitor-web-app-availability.md): Create tests to make sure your site is visible on the web.</span></span>
* <span data-ttu-id="fb8a8-213">[Slimme diagnostische gegevens](app-insights-proactive-diagnostics.md): deze tests worden automatisch uitgevoerd, zodat u niets hoeft te doen om ze in te stellen.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-213">[Smart diagnostics](app-insights-proactive-diagnostics.md): These tests run automatically, so you don't have to do anything to set them up.</span></span> <span data-ttu-id="fb8a8-214">Deze geeft aan of een app een ongebruikelijk aantal mislukte aanvragen heeft.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-214">They tell you if your app has an unusual rate of failed requests.</span></span>
* <span data-ttu-id="fb8a8-215">[Metrische waarschuwingen](app-insights-alerts.md): stel deze in om u te waarschuwen als een metriek een drempelwaarde overschrijdt.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-215">[Metric alerts](app-insights-alerts.md): Set these to warn you if a metric crosses a threshold.</span></span> <span data-ttu-id="fb8a8-216">U kunt deze instellen op aangepaste metrische gegevens die u in uw app codeert.</span><span class="sxs-lookup"><span data-stu-id="fb8a8-216">You can set them on custom metrics that you code into your app.</span></span>

### <a name="automation"></a><span data-ttu-id="fb8a8-217">Automation</span><span class="sxs-lookup"><span data-stu-id="fb8a8-217">Automation</span></span>

* [<span data-ttu-id="fb8a8-218">Het maken van een Application Insights-resource automatiseren</span><span class="sxs-lookup"><span data-stu-id="fb8a8-218">Automate creating an Application Insights resource</span></span>](app-insights-powershell.md)
