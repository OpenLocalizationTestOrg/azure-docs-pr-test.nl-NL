---
title: Exporteren naar Power BI in Application Insights | Microsoft Docs
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
ms.openlocfilehash: 350a65b1c6432baf258e014c9e63133d2b29e34f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="feed-power-bi-from-application-insights"></a><span data-ttu-id="4f94b-103">Power BI feed vanuit Application Insights</span><span class="sxs-lookup"><span data-stu-id="4f94b-103">Feed Power BI from Application Insights</span></span>
<span data-ttu-id="4f94b-104">[Power BI](http://www.powerbi.com/) is een suite met business analytics hulpmiddelen waarmee u gegevens analyseren en inzichten te delen.</span><span class="sxs-lookup"><span data-stu-id="4f94b-104">[Power BI](http://www.powerbi.com/) is a suite of business analytics tools that help you analyze data and share insights.</span></span> <span data-ttu-id="4f94b-105">Uitgebreide dashboards zijn beschikbaar op elk apparaat.</span><span class="sxs-lookup"><span data-stu-id="4f94b-105">Rich dashboards are available on every device.</span></span> <span data-ttu-id="4f94b-106">U kunt gegevens uit diverse bronnen, met inbegrip van analysequery's van combineren [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4f94b-106">You can combine data from many sources, including Analytics queries from [Azure Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="4f94b-107">Er zijn drie aanbevolen methoden voor het exporteren van gegevens van de Application Insights naar Power BI.</span><span class="sxs-lookup"><span data-stu-id="4f94b-107">There are three recommended methods of exporting Application Insights data to Power BI.</span></span> <span data-ttu-id="4f94b-108">U kunt deze afzonderlijk of samen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4f94b-108">You can use them separately or together.</span></span>

* <span data-ttu-id="4f94b-109">[**Power BI adapter** ](#power-pi-adapter) -instellen van een volledig dashboard telemetrie van uw app.</span><span class="sxs-lookup"><span data-stu-id="4f94b-109">[**Power BI adapter**](#power-pi-adapter) - set up a complete dashboard of telemetry from your app.</span></span> <span data-ttu-id="4f94b-110">De reeks grafieken vooraf wordt gedefinieerd, maar u kunt uw eigen query's uit andere bronnen toevoegen.</span><span class="sxs-lookup"><span data-stu-id="4f94b-110">The set of charts is predefined, but you can add your own queries from any other sources.</span></span>
* <span data-ttu-id="4f94b-111">[**Exporteren van analysequery's** ](#export-analytics-queries) -schrijven van een query die u wilt met Analytics en exporteren naar Power BI.</span><span class="sxs-lookup"><span data-stu-id="4f94b-111">[**Export Analytics queries**](#export-analytics-queries) - write any query you want using Analytics, and export it to Power BI.</span></span> <span data-ttu-id="4f94b-112">U kunt deze query op een dashboard samen met andere gegevens plaatsen.</span><span class="sxs-lookup"><span data-stu-id="4f94b-112">You can place this query on a dashboard along with any other data.</span></span>
* <span data-ttu-id="4f94b-113">[**Continue export en Stream Analytics** ](app-insights-export-stream-analytics.md) -hierbij meer werk om in te stellen.</span><span class="sxs-lookup"><span data-stu-id="4f94b-113">[**Continuous export and Stream Analytics**](app-insights-export-stream-analytics.md) - This involves more work to set up.</span></span> <span data-ttu-id="4f94b-114">Dit is handig als u wilt uw gegevens behouden gedurende langere perioden.</span><span class="sxs-lookup"><span data-stu-id="4f94b-114">It is useful if you want to keep your data for long periods.</span></span> <span data-ttu-id="4f94b-115">Anders wordt worden de andere methoden aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="4f94b-115">Otherwise, the other methods are recommended.</span></span>

## <a name="power-bi-adapter"></a><span data-ttu-id="4f94b-116">Power BI-adapter</span><span class="sxs-lookup"><span data-stu-id="4f94b-116">Power BI adapter</span></span>
<span data-ttu-id="4f94b-117">Deze methode maakt u een volledig dashboard telemetrie voor u.</span><span class="sxs-lookup"><span data-stu-id="4f94b-117">This method creates a complete dashboard of telemetry for you.</span></span> <span data-ttu-id="4f94b-118">De initiële gegevensset is vooraf gedefinieerd, maar u kunt meer gegevens toevoegen aan deze.</span><span class="sxs-lookup"><span data-stu-id="4f94b-118">The initial data set is predefined, but you can add more data to it.</span></span>

### <a name="get-the-adapter"></a><span data-ttu-id="4f94b-119">De adapter ophalen</span><span class="sxs-lookup"><span data-stu-id="4f94b-119">Get the adapter</span></span>
1. <span data-ttu-id="4f94b-120">Aanmelden bij [Power BI](https://app.powerbi.com/).</span><span class="sxs-lookup"><span data-stu-id="4f94b-120">Sign in to [Power BI](https://app.powerbi.com/).</span></span>
2. <span data-ttu-id="4f94b-121">Open **gegevens ophalen**, **Services**, **Application Insights**</span><span class="sxs-lookup"><span data-stu-id="4f94b-121">Open **Get Data**, **Services**, **Application Insights**</span></span>
   
    ![Ophalen van Application Insights-gegevensbron](./media/app-insights-export-power-bi/power-bi-adapter.png)
3. <span data-ttu-id="4f94b-123">Geef de details van uw Application Insights-resource.</span><span class="sxs-lookup"><span data-stu-id="4f94b-123">Provide the details of your Application Insights resource.</span></span>
   
    ![Ophalen van Application Insights-gegevensbron](./media/app-insights-export-power-bi/azure-subscription-resource-group-name.png)
4. <span data-ttu-id="4f94b-125">Wacht enkele minuten duren om de gegevens te worden geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="4f94b-125">Wait a minute or two for the data to be imported.</span></span>
   
    ![Power BI-adapter](./media/app-insights-export-power-bi/010.png)

<span data-ttu-id="4f94b-127">U kunt het dashboard bewerken de Application Insights-grafieken combineren met die van andere bronnen en met Analytics query's.</span><span class="sxs-lookup"><span data-stu-id="4f94b-127">You can edit the dashboard, combining the Application Insights charts with those of other sources, and with Analytics queries.</span></span> <span data-ttu-id="4f94b-128">Er is een visualisatie galerie krijgt u meer grafieken, waarbij elke grafiek heeft een parameters die u kunt instellen.</span><span class="sxs-lookup"><span data-stu-id="4f94b-128">There's a visualization gallery where you can get more charts, and each chart has a parameters you can set.</span></span>

<span data-ttu-id="4f94b-129">Na de initiële import blijven het dashboard en de rapporten dagelijks bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="4f94b-129">After the initial import, the dashboard and the reports continue to update daily.</span></span> <span data-ttu-id="4f94b-130">U kunt het vernieuwingsschema op de gegevensset beheren.</span><span class="sxs-lookup"><span data-stu-id="4f94b-130">You can control the refresh schedule on the dataset.</span></span>

## <a name="export-analytics-queries"></a><span data-ttu-id="4f94b-131">Analysequery's exporteren</span><span class="sxs-lookup"><span data-stu-id="4f94b-131">Export Analytics queries</span></span>
<span data-ttu-id="4f94b-132">Deze route kunt u elke gewenste Analytics-query schrijven en die vervolgens exporteren naar een Power BI-dashboard.</span><span class="sxs-lookup"><span data-stu-id="4f94b-132">This route allows you to write any Analytics query you like, and then export that to a Power BI dashboard.</span></span> <span data-ttu-id="4f94b-133">(U kunt toevoegen aan het dashboard is gemaakt door de adapter.)</span><span class="sxs-lookup"><span data-stu-id="4f94b-133">(You can add to the dashboard created by the adapter.)</span></span>

### <a name="one-time-install-power-bi-desktop"></a><span data-ttu-id="4f94b-134">Eén keer: Installeer Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="4f94b-134">One time: install Power BI Desktop</span></span>
<span data-ttu-id="4f94b-135">Als u wilt uw Application Insights-query importeren, moet u de bureaubladversie van Power BI gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4f94b-135">To import your Application Insights query, you use the desktop version of Power BI.</span></span> <span data-ttu-id="4f94b-136">Maar vervolgens kunt u deze publiceren naar het web of naar uw Power BI-cloud-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="4f94b-136">But then you can publish it to the web or to your Power BI cloud workspace.</span></span> 

<span data-ttu-id="4f94b-137">Installeer [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/).</span><span class="sxs-lookup"><span data-stu-id="4f94b-137">Install [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/).</span></span>

### <a name="export-an-analytics-query"></a><span data-ttu-id="4f94b-138">Exporteren van een query Analytics</span><span class="sxs-lookup"><span data-stu-id="4f94b-138">Export an Analytics query</span></span>
1. <span data-ttu-id="4f94b-139">[Open Analytics en uw query schrijven](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="4f94b-139">[Open Analytics and write your query](app-insights-analytics-tour.md).</span></span>
2. <span data-ttu-id="4f94b-140">Testen en de query te verfijnen totdat u tevreden met de resultaten bent.</span><span class="sxs-lookup"><span data-stu-id="4f94b-140">Test and refine the query until you're happy with the results.</span></span>

   <span data-ttu-id="4f94b-141">**Zorg ervoor dat de query correct wordt uitgevoerd in Analytics voordat u deze exporteert.**</span><span class="sxs-lookup"><span data-stu-id="4f94b-141">**Make sure that the query runs correctly in Analytics before you export it.**</span></span>
3. <span data-ttu-id="4f94b-142">Op de **exporteren** menu kiezen **Power BI (M)**.</span><span class="sxs-lookup"><span data-stu-id="4f94b-142">On the **Export** menu, choose **Power BI (M)**.</span></span> <span data-ttu-id="4f94b-143">Bewaar het tekstbestand.</span><span class="sxs-lookup"><span data-stu-id="4f94b-143">Save the text file.</span></span>
   
    ![Power BI query exporteren](./media/app-insights-export-power-bi/analytics-export-power-bi.png)
4. <span data-ttu-id="4f94b-145">In Power BI Desktop selecteer **gegevens ophalen, lege Query** en klik in de query-editor, onder **weergave** Selecteer **geavanceerde Query-Editor**.</span><span class="sxs-lookup"><span data-stu-id="4f94b-145">In Power BI Desktop select **Get Data, Blank Query** and then in the query editor, under **View** select **Advanced Query Editor**.</span></span>

    <span data-ttu-id="4f94b-146">Plak het geëxporteerde M taal script in de geavanceerde Query-Editor.</span><span class="sxs-lookup"><span data-stu-id="4f94b-146">Paste the exported M Language script into the Advanced Query Editor.</span></span>

    ![Geavanceerde query-editor](./media/app-insights-export-power-bi/power-bi-import-analytics-query.png)

1. <span data-ttu-id="4f94b-148">Mogelijk moet referenties opgeven voor het toestaan van Power BI voor toegang tot Azure.</span><span class="sxs-lookup"><span data-stu-id="4f94b-148">You might have to provide credentials to allow Power BI to access Azure.</span></span> <span data-ttu-id="4f94b-149">Gebruik 'organisatieaccount' zich kunnen aanmelden met je Microsoft-account.</span><span class="sxs-lookup"><span data-stu-id="4f94b-149">Use 'organizational account' to sign in with your Microsoft account.</span></span>
   
    ![Azure-referenties om in te schakelen van Power BI voor uw Application Insights-query opgeven](./media/app-insights-export-power-bi/power-bi-import-sign-in.png)

    <span data-ttu-id="4f94b-151">(Als u controleren of de referenties wilt, gebruiken de menuopdracht instellingen voor de gegevensbron in de Query-Editor.</span><span class="sxs-lookup"><span data-stu-id="4f94b-151">(If you need to verify the credentials, use the Data Source Settings menu command in the Query Editor.</span></span> <span data-ttu-id="4f94b-152">Wees voorzichtig om op te geven de referenties die u gebruikt voor Azure, dit van uw referenties voor Power BI afwijken kan.)</span><span class="sxs-lookup"><span data-stu-id="4f94b-152">Take care to specify the credentials you use for Azure, which might be different from your credentials for Power BI.)</span></span>
2. <span data-ttu-id="4f94b-153">Kies een visualisatie in voor uw query en selecteer de velden voor x-as, y-as en dimensie segmenteren.</span><span class="sxs-lookup"><span data-stu-id="4f94b-153">Choose a visualization for your query and select the fields for x-axis, y-axis, and segmenting dimension.</span></span>
   
    ![Visualisatie selecteren](./media/app-insights-export-power-bi/power-bi-analytics-visualize.png)
3. <span data-ttu-id="4f94b-155">Uw rapport publiceren op uw Power BI-cloud-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="4f94b-155">Publish your report to your Power BI cloud workspace.</span></span> <span data-ttu-id="4f94b-156">Daar kunt u een gesynchroniseerde versie insluiten in andere webpagina's.</span><span class="sxs-lookup"><span data-stu-id="4f94b-156">From there, you can embed a synchronized version into other web pages.</span></span>
   
    ![Visualisatie selecteren](./media/app-insights-export-power-bi/publish-power-bi.png)
4. <span data-ttu-id="4f94b-158">Het rapport handmatig vernieuwen met tussenpozen of een geplande vernieuwing op de optiepagina instellen.</span><span class="sxs-lookup"><span data-stu-id="4f94b-158">Refresh the report manually at intervals, or set up a scheduled refresh on the options page.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="4f94b-159">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="4f94b-159">Troubleshooting</span></span>

### <a name="401-or-403-unauthorized"></a><span data-ttu-id="4f94b-160">401- of 403 niet geautoriseerd</span><span class="sxs-lookup"><span data-stu-id="4f94b-160">401 or 403 Unauthorized</span></span> 
<span data-ttu-id="4f94b-161">Dit kan gebeuren als uw refesh-token is niet bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="4f94b-161">This can happen if your refesh token has not been updated.</span></span> <span data-ttu-id="4f94b-162">Probeer de volgende stappen om te controleren of dat u nog steeds toegang hebben.</span><span class="sxs-lookup"><span data-stu-id="4f94b-162">Try these steps to ensure you still have access.</span></span> <span data-ttu-id="4f94b-163">Als u hebt toegang tot en refershing de referenties niet werkt, opent u een ondersteuningsticket.</span><span class="sxs-lookup"><span data-stu-id="4f94b-163">If you do have access and refershing the credentials does not work, please open a support ticket.</span></span>

1. <span data-ttu-id="4f94b-164">Meld u aan bij de Azure-Portal en controleer of dat u toegang hebt tot de resource</span><span class="sxs-lookup"><span data-stu-id="4f94b-164">Log into the Azure Portal and make sure you can access the resource</span></span>
2. <span data-ttu-id="4f94b-165">Probeer de referenties voor het Dashboard vernieuwen</span><span class="sxs-lookup"><span data-stu-id="4f94b-165">Try to refresh the credentials for the Dashboard</span></span>

### <a name="502-bad-gateway"></a><span data-ttu-id="4f94b-166">502 Slechte Gateway</span><span class="sxs-lookup"><span data-stu-id="4f94b-166">502 Bad Gateway</span></span>
<span data-ttu-id="4f94b-167">Dit wordt meestal veroorzaakt door een Analytics-query die te veel gegevens retourneert.</span><span class="sxs-lookup"><span data-stu-id="4f94b-167">This is usually caused by an Analytics query that returns too much data.</span></span> <span data-ttu-id="4f94b-168">U moet proberen met behulp van een kleinere tijdsbereik of met behulp van de [geleden](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#ago) of [startofweek/startofmonth](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#startofweek) werkt alleen [project](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#project-operator) de velden die u nodig.</span><span class="sxs-lookup"><span data-stu-id="4f94b-168">You should try using a smaller time range or by using the [ago](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#ago) or [startofweek/startofmonth](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#startofweek) functions only [project](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#project-operator) the fields you need.</span></span>

<span data-ttu-id="4f94b-169">Als de gegevensset die afkomstig zijn van de query Analytics verminderen niet voldoet aan uw vereisten moet u overwegen de [API](https://dev.applicationinsights.io/documentation/overview) voor het ophalen van een grotere gegevensset.</span><span class="sxs-lookup"><span data-stu-id="4f94b-169">If reducing the dataset coming from the Analytics query doesn't meet your requirements you should consider using the [API](https://dev.applicationinsights.io/documentation/overview) to pull a larger dataset.</span></span> <span data-ttu-id="4f94b-170">Hier vindt u instructies voor het converteren van de export M-Query voor het gebruik van de API.</span><span class="sxs-lookup"><span data-stu-id="4f94b-170">Here are instructions on how to convert the M-Query export to use the API.</span></span>

1. <span data-ttu-id="4f94b-171">Maak een [API-sleutel](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID)</span><span class="sxs-lookup"><span data-stu-id="4f94b-171">Create an [API Key](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID)</span></span>
2. <span data-ttu-id="4f94b-172">Bijwerken van het Power BI-M-script dat u hebt geëxporteerd van analytische gegevens door de ARM-URL vervangen door een AI-API (Zie onderstaand voorbeeld)</span><span class="sxs-lookup"><span data-stu-id="4f94b-172">Update the Power BI M script that you exported from Analytics by replacing the ARM URL with AI API (see example below)</span></span>
   * <span data-ttu-id="4f94b-173">Vervang **https://management.azure.com/subscriptions/...**</span><span class="sxs-lookup"><span data-stu-id="4f94b-173">Replace **https://management.azure.com/subscriptions/...**</span></span>
   * <span data-ttu-id="4f94b-174">met **https://api.applicationinsights.io/beta/apps/...**</span><span class="sxs-lookup"><span data-stu-id="4f94b-174">with, **https://api.applicationinsights.io/beta/apps/...**</span></span>
3. <span data-ttu-id="4f94b-175">Ten slotte referenties bijwerken op basis en gebruik van uw API-sleutel</span><span class="sxs-lookup"><span data-stu-id="4f94b-175">Finally, update credentials to basic, and use your API Key</span></span>
  

<span data-ttu-id="4f94b-176">**Bestaand Script**</span><span class="sxs-lookup"><span data-stu-id="4f94b-176">**Existing Script**</span></span>
 ```
 Source = Json.Document(Web.Contents("https://management.azure.com/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups//providers/microsoft.insights/components//api/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```
<span data-ttu-id="4f94b-177">**Bijgewerkte Script**</span><span class="sxs-lookup"><span data-stu-id="4f94b-177">**Updated Script**</span></span>
 ```
 Source = Json.Document(Web.Contents("https://api.applicationinsights.io/beta/apps/<APPLICATION_ID>/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```

## <a name="about-sampling"></a><span data-ttu-id="4f94b-178">Over steekproeven</span><span class="sxs-lookup"><span data-stu-id="4f94b-178">About sampling</span></span>
<span data-ttu-id="4f94b-179">Als uw toepassing grote hoeveelheden gegevens verzendt, wordt de functie voor adaptieve steekproeven werkt en wordt slechts een percentage van uw telemetrie verzenden.</span><span class="sxs-lookup"><span data-stu-id="4f94b-179">If your application sends a lot of data, the adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> <span data-ttu-id="4f94b-180">Hetzelfde geldt als u de samplingfrequentie handmatig hebt ingesteld in de SDK of op de opname.</span><span class="sxs-lookup"><span data-stu-id="4f94b-180">The same is true if you have manually set sampling either in the SDK or on ingestion.</span></span> [<span data-ttu-id="4f94b-181">Meer informatie over steekproeven.</span><span class="sxs-lookup"><span data-stu-id="4f94b-181">Learn more about sampling.</span></span>](app-insights-sampling.md)


## <a name="next-steps"></a><span data-ttu-id="4f94b-182">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4f94b-182">Next steps</span></span>
* [<span data-ttu-id="4f94b-183">Power BI - informatie</span><span class="sxs-lookup"><span data-stu-id="4f94b-183">Power BI - Learn</span></span>](http://www.powerbi.com/learning/)
* [<span data-ttu-id="4f94b-184">Analytics-zelfstudie</span><span class="sxs-lookup"><span data-stu-id="4f94b-184">Analytics tutorial</span></span>](app-insights-analytics-tour.md)

