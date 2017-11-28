---
title: aaaExport tooPower BI van Application Insights | Microsoft Docs
description: Analytics-query's kunnen worden weergegeven in Power BI.
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 7f13ea66-09dc-450f-b8f9-f40fdad239f2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: 6668cd7f4e0fbf41695972617f5f8ec207356659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="feed-power-bi-from-application-insights"></a><span data-ttu-id="5f4fd-103">Power BI feed vanuit Application Insights</span><span class="sxs-lookup"><span data-stu-id="5f4fd-103">Feed Power BI from Application Insights</span></span>
<span data-ttu-id="5f4fd-104">[Power BI](http://www.powerbi.com/) is een suite met business analytics hulpmiddelen waarmee u gegevens analyseren en inzichten te delen.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-104">[Power BI](http://www.powerbi.com/) is a suite of business analytics tools that help you analyze data and share insights.</span></span> <span data-ttu-id="5f4fd-105">Uitgebreide dashboards zijn beschikbaar op elk apparaat.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-105">Rich dashboards are available on every device.</span></span> <span data-ttu-id="5f4fd-106">U kunt gegevens uit diverse bronnen, met inbegrip van analysequery's van combineren [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5f4fd-106">You can combine data from many sources, including Analytics queries from [Azure Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="5f4fd-107">Er zijn drie aanbevolen methoden voor het exporteren van Application Insights gegevens tooPower BI.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-107">There are three recommended methods of exporting Application Insights data tooPower BI.</span></span> <span data-ttu-id="5f4fd-108">U kunt deze afzonderlijk of samen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-108">You can use them separately or together.</span></span>

* <span data-ttu-id="5f4fd-109">[**Power BI adapter** ](#power-pi-adapter) -instellen van een volledig dashboard telemetrie van uw app.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-109">[**Power BI adapter**](#power-pi-adapter) - set up a complete dashboard of telemetry from your app.</span></span> <span data-ttu-id="5f4fd-110">Hallo set grafieken vooraf wordt gedefinieerd, maar u kunt uw eigen query's uit andere bronnen toevoegen.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-110">hello set of charts is predefined, but you can add your own queries from any other sources.</span></span>
* <span data-ttu-id="5f4fd-111">[**Exporteren van analysequery's** ](#export-analytics-queries) -schrijven van een query die u wilt met Analytics en tooPower BI exporteren.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-111">[**Export Analytics queries**](#export-analytics-queries) - write any query you want using Analytics, and export it tooPower BI.</span></span> <span data-ttu-id="5f4fd-112">U kunt deze query op een dashboard samen met andere gegevens plaatsen.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-112">You can place this query on a dashboard along with any other data.</span></span>
* <span data-ttu-id="5f4fd-113">[**Continue export en Stream Analytics** ](app-insights-export-stream-analytics.md) -hierbij meer werk tooset up.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-113">[**Continuous export and Stream Analytics**](app-insights-export-stream-analytics.md) - This involves more work tooset up.</span></span> <span data-ttu-id="5f4fd-114">Dit is handig als u wilt dat tookeep gegevens gedurende langere perioden.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-114">It is useful if you want tookeep your data for long periods.</span></span> <span data-ttu-id="5f4fd-115">Anders worden hello andere methoden aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-115">Otherwise, hello other methods are recommended.</span></span>

## <a name="power-bi-adapter"></a><span data-ttu-id="5f4fd-116">Power BI-adapter</span><span class="sxs-lookup"><span data-stu-id="5f4fd-116">Power BI adapter</span></span>
<span data-ttu-id="5f4fd-117">Deze methode maakt u een volledig dashboard telemetrie voor u.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-117">This method creates a complete dashboard of telemetry for you.</span></span> <span data-ttu-id="5f4fd-118">Hallo initiële gegevensset is vooraf gedefinieerd, maar u kunt meer gegevens tooit toevoegen.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-118">hello initial data set is predefined, but you can add more data tooit.</span></span>

### <a name="get-hello-adapter"></a><span data-ttu-id="5f4fd-119">Hallo adapter ophalen</span><span class="sxs-lookup"><span data-stu-id="5f4fd-119">Get hello adapter</span></span>
1. <span data-ttu-id="5f4fd-120">Aanmelden te[Power BI](https://app.powerbi.com/).</span><span class="sxs-lookup"><span data-stu-id="5f4fd-120">Sign in too[Power BI](https://app.powerbi.com/).</span></span>
2. <span data-ttu-id="5f4fd-121">Open **gegevens ophalen**, **Services**, **Application Insights**</span><span class="sxs-lookup"><span data-stu-id="5f4fd-121">Open **Get Data**, **Services**, **Application Insights**</span></span>
   
    ![Ophalen van Application Insights-gegevensbron](./media/app-insights-export-power-bi/power-bi-adapter.png)
3. <span data-ttu-id="5f4fd-123">Geef details op Hallo van uw Application Insights-resource.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-123">Provide hello details of your Application Insights resource.</span></span>
   
    ![Ophalen van Application Insights-gegevensbron](./media/app-insights-export-power-bi/azure-subscription-resource-group-name.png)
4. <span data-ttu-id="5f4fd-125">Wacht een minuut of twee Hallo gegevens toobe geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-125">Wait a minute or two for hello data toobe imported.</span></span>
   
    ![Power BI-adapter](./media/app-insights-export-power-bi/010.png)

<span data-ttu-id="5f4fd-127">U kunt dashboard Hallo Hallo Application Insights grafieken combineren met die van andere bronnen en met analysequery's bewerken.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-127">You can edit hello dashboard, combining hello Application Insights charts with those of other sources, and with Analytics queries.</span></span> <span data-ttu-id="5f4fd-128">Er is een visualisatie galerie krijgt u meer grafieken, waarbij elke grafiek heeft een parameters die u kunt instellen.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-128">There's a visualization gallery where you can get more charts, and each chart has a parameters you can set.</span></span>

<span data-ttu-id="5f4fd-129">Na Hallo blijven importeren in eerste instantie, Hallo dashboard en rapporten Hallo tooupdate dagelijks.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-129">After hello initial import, hello dashboard and hello reports continue tooupdate daily.</span></span> <span data-ttu-id="5f4fd-130">U kunt het schema voor gegevensvernieuwing Hallo op Hallo gegevensset beheren.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-130">You can control hello refresh schedule on hello dataset.</span></span>

## <a name="export-analytics-queries"></a><span data-ttu-id="5f4fd-131">Analysequery's exporteren</span><span class="sxs-lookup"><span data-stu-id="5f4fd-131">Export Analytics queries</span></span>
<span data-ttu-id="5f4fd-132">Deze route kunt u toowrite eventuele Analytics query u zoals en exporteert u dat tooa Power BI-dashboard.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-132">This route allows you toowrite any Analytics query you like, and then export that tooa Power BI dashboard.</span></span> <span data-ttu-id="5f4fd-133">(U kunt toohello dashboard dat is gemaakt door Hallo-adapter toevoegen).</span><span class="sxs-lookup"><span data-stu-id="5f4fd-133">(You can add toohello dashboard created by hello adapter.)</span></span>

### <a name="one-time-install-power-bi-desktop"></a><span data-ttu-id="5f4fd-134">Eén keer: Installeer Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="5f4fd-134">One time: install Power BI Desktop</span></span>
<span data-ttu-id="5f4fd-135">tooimport uw query Application Insights u Hallo bureaubladversie van Power BI gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-135">tooimport your Application Insights query, you use hello desktop version of Power BI.</span></span> <span data-ttu-id="5f4fd-136">Maar vervolgens kunt u deze publiceren toohello web- of tooyour Power BI cloud werkruimte.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-136">But then you can publish it toohello web or tooyour Power BI cloud workspace.</span></span> 

<span data-ttu-id="5f4fd-137">Installeer [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/).</span><span class="sxs-lookup"><span data-stu-id="5f4fd-137">Install [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/).</span></span>

### <a name="export-an-analytics-query"></a><span data-ttu-id="5f4fd-138">Exporteren van een query Analytics</span><span class="sxs-lookup"><span data-stu-id="5f4fd-138">Export an Analytics query</span></span>
1. <span data-ttu-id="5f4fd-139">[Open Analytics en uw query schrijven](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="5f4fd-139">[Open Analytics and write your query](app-insights-analytics-tour.md).</span></span>
2. <span data-ttu-id="5f4fd-140">Testen en Hallo-query te verfijnen totdat u tevreden met Hallo resultaten bent.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-140">Test and refine hello query until you're happy with hello results.</span></span>

   <span data-ttu-id="5f4fd-141">**Zorg ervoor dat deze Hallo-query wordt uitgevoerd correct in Analytics voordat u dit exporteren.**</span><span class="sxs-lookup"><span data-stu-id="5f4fd-141">**Make sure that hello query runs correctly in Analytics before you export it.**</span></span>
3. <span data-ttu-id="5f4fd-142">Op Hallo **exporteren** menu kiezen **Power BI (M)**.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-142">On hello **Export** menu, choose **Power BI (M)**.</span></span> <span data-ttu-id="5f4fd-143">Hallo-tekstbestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-143">Save hello text file.</span></span>
   
    ![Power BI query exporteren](./media/app-insights-export-power-bi/analytics-export-power-bi.png)
4. <span data-ttu-id="5f4fd-145">In Power BI Desktop selecteer **gegevens ophalen, lege Query** en klik vervolgens in Hallo-query-editor, onder **weergave** Selecteer **geavanceerde Query-Editor**.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-145">In Power BI Desktop select **Get Data, Blank Query** and then in hello query editor, under **View** select **Advanced Query Editor**.</span></span>

    <span data-ttu-id="5f4fd-146">Plakken Hallo geëxporteerd M taal script in Hallo geavanceerde Query-Editor.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-146">Paste hello exported M Language script into hello Advanced Query Editor.</span></span>

    ![Geavanceerde query-editor](./media/app-insights-export-power-bi/power-bi-import-analytics-query.png)

1. <span data-ttu-id="5f4fd-148">Mogelijk hebt u tooprovide referenties tooallow Power BI tooaccess Azure.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-148">You might have tooprovide credentials tooallow Power BI tooaccess Azure.</span></span> <span data-ttu-id="5f4fd-149">Gebruik 'organisatieaccount' toosign met uw Microsoft-account.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-149">Use 'organizational account' toosign in with your Microsoft account.</span></span>
   
    ![Azure-referenties tooenable Power BI toorun uw Application Insights-query opgeven](./media/app-insights-export-power-bi/power-bi-import-sign-in.png)

    <span data-ttu-id="5f4fd-151">(Als u tooverify Hallo referenties nodig hebt, gebruik Hallo Gegevensbroninstellingen menuopdracht in Hallo Query-Editor.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-151">(If you need tooverify hello credentials, use hello Data Source Settings menu command in hello Query Editor.</span></span> <span data-ttu-id="5f4fd-152">Maatregelen treffen toospecify Hallo referenties voor Azure, dit van uw referenties voor Power BI afwijken kan.)</span><span class="sxs-lookup"><span data-stu-id="5f4fd-152">Take care toospecify hello credentials you use for Azure, which might be different from your credentials for Power BI.)</span></span>
2. <span data-ttu-id="5f4fd-153">Kies een visualisatie in voor uw query en selecteer de velden Hallo voor x-as, y-as en dimensie segmenteren.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-153">Choose a visualization for your query and select hello fields for x-axis, y-axis, and segmenting dimension.</span></span>
   
    ![Visualisatie selecteren](./media/app-insights-export-power-bi/power-bi-analytics-visualize.png)
3. <span data-ttu-id="5f4fd-155">Publiceren van uw rapport tooyour Power BI cloud-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-155">Publish your report tooyour Power BI cloud workspace.</span></span> <span data-ttu-id="5f4fd-156">Daar kunt u een gesynchroniseerde versie insluiten in andere webpagina's.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-156">From there, you can embed a synchronized version into other web pages.</span></span>
   
    ![Visualisatie selecteren](./media/app-insights-export-power-bi/publish-power-bi.png)
4. <span data-ttu-id="5f4fd-158">Hallo rapport handmatig vernieuwen met tussenpozen of een geplande vernieuwing op de optiepagina voor Hallo instelt.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-158">Refresh hello report manually at intervals, or set up a scheduled refresh on hello options page.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="5f4fd-159">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="5f4fd-159">Troubleshooting</span></span>

### <a name="401-or-403-unauthorized"></a><span data-ttu-id="5f4fd-160">401- of 403 niet geautoriseerd</span><span class="sxs-lookup"><span data-stu-id="5f4fd-160">401 or 403 Unauthorized</span></span> 
<span data-ttu-id="5f4fd-161">Dit kan gebeuren als uw refesh-token is niet bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-161">This can happen if your refesh token has not been updated.</span></span> <span data-ttu-id="5f4fd-162">Probeer deze stappen tooensure u nog steeds toegang hebben.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-162">Try these steps tooensure you still have access.</span></span> <span data-ttu-id="5f4fd-163">Als u toegang hebt en refershing Hallo referenties niet werkt, opent u een ondersteuningsticket.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-163">If you do have access and refershing hello credentials does not work, please open a support ticket.</span></span>

1. <span data-ttu-id="5f4fd-164">Meld u aan bij hello Azure-Portal en controleer of dat u toegang hebt tot Hallo resource</span><span class="sxs-lookup"><span data-stu-id="5f4fd-164">Log into hello Azure Portal and make sure you can access hello resource</span></span>
2. <span data-ttu-id="5f4fd-165">Probeer toorefresh Hallo referenties voor Hallo Dashboard</span><span class="sxs-lookup"><span data-stu-id="5f4fd-165">Try toorefresh hello credentials for hello Dashboard</span></span>

### <a name="502-bad-gateway"></a><span data-ttu-id="5f4fd-166">502 Slechte Gateway</span><span class="sxs-lookup"><span data-stu-id="5f4fd-166">502 Bad Gateway</span></span>
<span data-ttu-id="5f4fd-167">Dit wordt meestal veroorzaakt door een Analytics-query die te veel gegevens retourneert.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-167">This is usually caused by an Analytics query that returns too much data.</span></span> <span data-ttu-id="5f4fd-168">Moet u proberen met behulp van een kleinere tijdsbereik of met behulp van Hallo [geleden](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#ago) of [startofweek/startofmonth](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#startofweek) werkt alleen [project](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#project-operator) Hallo velden die u nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-168">You should try using a smaller time range or by using hello [ago](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#ago) or [startofweek/startofmonth](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#startofweek) functions only [project](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#project-operator) hello fields you need.</span></span>

<span data-ttu-id="5f4fd-169">Als verminderen Hallo gegevensset afkomstig is van Hallo Analytics query niet voldoet aan uw vereisten moet u overwegen Hallo [API](https://dev.applicationinsights.io/documentation/overview) toopull een grotere gegevensset.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-169">If reducing hello dataset coming from hello Analytics query doesn't meet your requirements you should consider using hello [API](https://dev.applicationinsights.io/documentation/overview) toopull a larger dataset.</span></span> <span data-ttu-id="5f4fd-170">Hier vindt u instructies over hoe de toouse Hallo API voor het exporteren van tooconvert Hallo M-Query.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-170">Here are instructions on how tooconvert hello M-Query export toouse hello API.</span></span>

1. <span data-ttu-id="5f4fd-171">Maak een [API-sleutel](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID)</span><span class="sxs-lookup"><span data-stu-id="5f4fd-171">Create an [API Key](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID)</span></span>
2. <span data-ttu-id="5f4fd-172">Update Hallo Power BI-M-script dat u hebt geëxporteerd van analytische gegevens door te vervangen Hallo ARM-URL met AI-API (Zie onderstaand voorbeeld)</span><span class="sxs-lookup"><span data-stu-id="5f4fd-172">Update hello Power BI M script that you exported from Analytics by replacing hello ARM URL with AI API (see example below)</span></span>
   * <span data-ttu-id="5f4fd-173">Vervang **https://management.azure.com/subscriptions/...**</span><span class="sxs-lookup"><span data-stu-id="5f4fd-173">Replace **https://management.azure.com/subscriptions/...**</span></span>
   * <span data-ttu-id="5f4fd-174">met **https://api.applicationinsights.io/beta/apps/...**</span><span class="sxs-lookup"><span data-stu-id="5f4fd-174">with, **https://api.applicationinsights.io/beta/apps/...**</span></span>
3. <span data-ttu-id="5f4fd-175">Ten slotte toobasic referenties bijwerken en gebruik van uw API-sleutel</span><span class="sxs-lookup"><span data-stu-id="5f4fd-175">Finally, update credentials toobasic, and use your API Key</span></span>
  

<span data-ttu-id="5f4fd-176">**Bestaand Script**</span><span class="sxs-lookup"><span data-stu-id="5f4fd-176">**Existing Script**</span></span>
 ```
 Source = Json.Document(Web.Contents("https://management.azure.com/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups//providers/microsoft.insights/components//api/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```
<span data-ttu-id="5f4fd-177">**Bijgewerkte Script**</span><span class="sxs-lookup"><span data-stu-id="5f4fd-177">**Updated Script**</span></span>
 ```
 Source = Json.Document(Web.Contents("https://api.applicationinsights.io/beta/apps/<APPLICATION_ID>/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```

## <a name="about-sampling"></a><span data-ttu-id="5f4fd-178">Over steekproeven</span><span class="sxs-lookup"><span data-stu-id="5f4fd-178">About sampling</span></span>
<span data-ttu-id="5f4fd-179">Als uw toepassing grote hoeveelheden gegevens verzendt, mag de functie voor adaptieve steekproeven Hallo werkt en slechts een percentage van uw telemetrie verzenden.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-179">If your application sends a lot of data, hello adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> <span data-ttu-id="5f4fd-180">Hallo geldt ook als u hebt de steekproef nemen handmatig ingesteld in Hallo SDK of op de opname.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-180">hello same is true if you have manually set sampling either in hello SDK or on ingestion.</span></span> [<span data-ttu-id="5f4fd-181">Meer informatie over steekproeven.</span><span class="sxs-lookup"><span data-stu-id="5f4fd-181">Learn more about sampling.</span></span>](app-insights-sampling.md)


## <a name="next-steps"></a><span data-ttu-id="5f4fd-182">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5f4fd-182">Next steps</span></span>
* [<span data-ttu-id="5f4fd-183">Power BI - informatie</span><span class="sxs-lookup"><span data-stu-id="5f4fd-183">Power BI - Learn</span></span>](http://www.powerbi.com/learning/)
* [<span data-ttu-id="5f4fd-184">Analytics-zelfstudie</span><span class="sxs-lookup"><span data-stu-id="5f4fd-184">Analytics tutorial</span></span>](app-insights-analytics-tour.md)

