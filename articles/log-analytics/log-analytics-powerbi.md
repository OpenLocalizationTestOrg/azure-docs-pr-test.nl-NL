---
title: Log Analytics-gegevens exporteren naar Power BI | Microsoft Docs
description: "Power BI is een cloudgebaseerde business analytics-service van Microsoft die uitgebreide visualisaties en rapporten voor analyse van verschillende sets van gegevens biedt.  Log Analytics kunt continu gegevens exporteren uit de OMS-opslagplaats in Power BI zodat u van de vorm van visualisaties en hulpmiddelen voor analyse gebruikmaken kunt.  Dit artikel wordt beschreven hoe u query's in logboekanalyse die automatisch worden geëxporteerd naar Power BI met regelmatige tussenpozen configureert."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 83edc411-6886-4de1-aadd-33982147b9c3
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: bwren
ms.openlocfilehash: 98befb16d27387e8f65a27771a2a32c264119d74
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="export-log-analytics-data-to-power-bi"></a><span data-ttu-id="ead01-105">Log Analytics-gegevens exporteren naar Power BI</span><span class="sxs-lookup"><span data-stu-id="ead01-105">Export Log Analytics data to Power BI</span></span>

>[!NOTE]
> <span data-ttu-id="ead01-106">Als uw werkruimte is bijgewerkt naar de [nieuwe logboekanalyse querytaal](log-analytics-log-search-upgrade.md), en vervolgens dit proces voor het exporteren van logboekanalyse gegevens met Power BI niet meer werken.</span><span class="sxs-lookup"><span data-stu-id="ead01-106">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then this process for exporting Log Analytics data to Power BI will no longer work.</span></span>  <span data-ttu-id="ead01-107">Eventuele bestaande schema's die u hebt gemaakt voordat u de upgrade wordt uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="ead01-107">Any existing schedules that you created before upgrading will become disabled.</span></span> 
>
> <span data-ttu-id="ead01-108">Na de upgrade, wordt Azure Log Analytics hetzelfde platform als Application Insights en u hetzelfde proces gebruiken om te exporteren Log Analytics-query's naar Power BI als [het proces voor het exporteren van Application Insights-query's naar Power BI](../application-insights/app-insights-export-power-bi.md#export-analytics-queries).</span><span class="sxs-lookup"><span data-stu-id="ead01-108">After upgrade, Azure Log Analytics uses the same platform as Application Insights, and you use the same process to export Log Analytics queries to Power BI as [the process to export Application Insights queries to Power BI](../application-insights/app-insights-export-power-bi.md#export-analytics-queries).</span></span>  <span data-ttu-id="ead01-109">U kunt exporteren van de query met de console Analytics, zoals beschreven in dit artikel of kunt u de **Power BI** knop aan de bovenkant van het scherm in de portal logboek zoeken.</span><span class="sxs-lookup"><span data-stu-id="ead01-109">You can either export the query using the Analytics console as described in that article, or you can select the **Power BI** button at the top of the screen in the Log Search portal.</span></span>



<span data-ttu-id="ead01-110">[Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/) is een service in de cloud business analytics van Microsoft die uitgebreide visualisaties en rapporten voor analyse van verschillende sets van gegevens biedt.</span><span class="sxs-lookup"><span data-stu-id="ead01-110">[Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/) is a cloud based business analytics service from Microsoft that provides rich visualizations and reports for analysis of different sets of data.</span></span>  <span data-ttu-id="ead01-111">Log Analytics kunt automatisch gegevens exporteren uit de OMS-opslagplaats in Power BI zodat u van de vorm van visualisaties en hulpmiddelen voor analyse gebruikmaken kunt.</span><span class="sxs-lookup"><span data-stu-id="ead01-111">Log Analytics can automatically export data from the OMS repository into Power BI so you can leverage its visualizations and analysis tools.</span></span>

<span data-ttu-id="ead01-112">Wanneer u Power BI met logboekanalyse configureert, maakt u log-query's die hun resultaten naar de bijbehorende gegevenssets in Power BI exporteren.</span><span class="sxs-lookup"><span data-stu-id="ead01-112">When you configure Power BI with Log Analytics, you create log queries that export their results to corresponding datasets in Power BI.</span></span>  <span data-ttu-id="ead01-113">De query en uitvoer blijft automatisch moet worden uitgevoerd volgens een planning die u definieert voor de gegevensset up-to-date te houden met de meest recente gegevens verzameld door logboekanalyse.</span><span class="sxs-lookup"><span data-stu-id="ead01-113">The query and export continues to automatically run on a schedule that you define to keep the dataset up to date with the latest data collected by Log Analytics.</span></span>

![Log Analytics naar Power BI](media/log-analytics-powerbi/overview.png)

## <a name="power-bi-schedules"></a><span data-ttu-id="ead01-115">Power BI-schema 's</span><span class="sxs-lookup"><span data-stu-id="ead01-115">Power BI Schedules</span></span>
<span data-ttu-id="ead01-116">Een *Power BI planning* bevat een logboek zoekopdracht die een set gegevens worden geëxporteerd vanuit de OMS-opslagplaats naar de bijbehorende gegevensset in Power BI en een planning die hoe vaak deze zoekopdracht wordt uitgevoerd definieert voor de gegevensset actueel te houden.</span><span class="sxs-lookup"><span data-stu-id="ead01-116">A *Power BI Schedule* includes a log search that exports a set of data from the OMS repository to a corresponding dataset in Power BI and a schedule that defines how often this search is run to keep the dataset current.</span></span>

<span data-ttu-id="ead01-117">De velden in de gegevensset komt overeen met de eigenschappen van de records geretourneerd door het logboek zoeken.</span><span class="sxs-lookup"><span data-stu-id="ead01-117">The fields in the dataset will match the properties of the records returned by the log search.</span></span>  <span data-ttu-id="ead01-118">Als de zoekopdracht records van verschillende typen retourneert vervolgens bevat de gegevensset alle eigenschappen van elk van de opgenomen recordtypen.</span><span class="sxs-lookup"><span data-stu-id="ead01-118">If the search returns records of different types then the dataset will include all of the properties from each of the included record types.</span></span>  

> [!NOTE]
> <span data-ttu-id="ead01-119">Het is een best practice gebruik van een zoekquery logboek die als resultaat geeft onbewerkte gegevens in plaats van een consolidatie met opdrachten zoals uitvoert [meting](log-analytics-search-reference.md#measure).</span><span class="sxs-lookup"><span data-stu-id="ead01-119">It is a best practice to use a log search query that returns raw data as opposed to performing any consolidation using commands such as [Measure](log-analytics-search-reference.md#measure).</span></span>  <span data-ttu-id="ead01-120">U kunt een aggregatie en berekeningen in Power BI uitvoeren vanaf de onbewerkte gegevens.</span><span class="sxs-lookup"><span data-stu-id="ead01-120">You can perform any aggregation and calculations in Power BI from the raw data.</span></span>
>
>

## <a name="connecting-oms-workspace-to-power-bi"></a><span data-ttu-id="ead01-121">OMS-werkruimte verbinding met Power BI</span><span class="sxs-lookup"><span data-stu-id="ead01-121">Connecting OMS workspace to Power BI</span></span>
<span data-ttu-id="ead01-122">Voordat u van logboekanalyse naar Power BI exporteren kunt, moet u de OMS-werkruimte verbinden met uw Power BI-account met de volgende procedure.</span><span class="sxs-lookup"><span data-stu-id="ead01-122">Before you can export from Log Analytics to Power BI, you must connect your OMS workspace to your Power BI account using the following procedure.</span></span>  

1. <span data-ttu-id="ead01-123">Klik in de OMS-console op de **instellingen** tegel.</span><span class="sxs-lookup"><span data-stu-id="ead01-123">In the OMS console click the **Settings** tile.</span></span>
2. <span data-ttu-id="ead01-124">Selecteer **Accounts**.</span><span class="sxs-lookup"><span data-stu-id="ead01-124">Select **Accounts**.</span></span>
3. <span data-ttu-id="ead01-125">In de **werkruimte** sectie Klik **verbinding maken met Power BI-Account**.</span><span class="sxs-lookup"><span data-stu-id="ead01-125">In the **Workspace Information** section click **Connect to Power BI Account**.</span></span>
4. <span data-ttu-id="ead01-126">Voer de referenties voor uw Power BI-account.</span><span class="sxs-lookup"><span data-stu-id="ead01-126">Enter the credentials for your Power BI account.</span></span>

## <a name="create-a-power-bi-schedule"></a><span data-ttu-id="ead01-127">Maak een planning van Power BI</span><span class="sxs-lookup"><span data-stu-id="ead01-127">Create a Power BI Schedule</span></span>
<span data-ttu-id="ead01-128">Maak een Power BI-schema voor elke gegevensset met de volgende procedure.</span><span class="sxs-lookup"><span data-stu-id="ead01-128">Create a Power BI Schedule for each dataset using the following procedure.</span></span>

1. <span data-ttu-id="ead01-129">Klik in de OMS-console op de **logboek zoeken** tegel.</span><span class="sxs-lookup"><span data-stu-id="ead01-129">In the OMS console click the **Log Search** tile.</span></span>
2. <span data-ttu-id="ead01-130">Typ in een nieuwe query of Selecteer een opgeslagen zoekopdracht die de gegevens waarop u exporteren retourneert wilt naar **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="ead01-130">Type in a new query or select a saved search that returns the data that you want to export to **Power BI**.</span></span>  
3. <span data-ttu-id="ead01-131">Klik op de **Power BI** knop aan de bovenkant van de pagina opent de **Power BI** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ead01-131">Click the **Power BI** button at the top of the page to open the **Power BI** dialog.</span></span>
4. <span data-ttu-id="ead01-132">Geef de informatie in de volgende tabel en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="ead01-132">Provide the information in the following table and click **Save**.</span></span>

| <span data-ttu-id="ead01-133">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="ead01-133">Property</span></span> | <span data-ttu-id="ead01-134">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ead01-134">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ead01-135">Naam</span><span class="sxs-lookup"><span data-stu-id="ead01-135">Name</span></span> |<span data-ttu-id="ead01-136">De naam om het schema te identificeren wanneer u de lijst met Power BI-schema's weergeven.</span><span class="sxs-lookup"><span data-stu-id="ead01-136">Name to identify the schedule when you view the list of Power BI schedules.</span></span> |
| <span data-ttu-id="ead01-137">Opgeslagen zoekopdracht</span><span class="sxs-lookup"><span data-stu-id="ead01-137">Saved Search</span></span> |<span data-ttu-id="ead01-138">De zoekopdracht logboek om uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="ead01-138">The log search to run.</span></span>  <span data-ttu-id="ead01-139">Selecteer de huidige query of Selecteer een bestaande opgeslagen zoekopdracht in de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="ead01-139">You can either select the current query or select an existing saved search from the dropdown box.</span></span> |
| <span data-ttu-id="ead01-140">Planning</span><span class="sxs-lookup"><span data-stu-id="ead01-140">Schedule</span></span> |<span data-ttu-id="ead01-141">Hoe vaak de opgeslagen zoekopdracht uitvoeren en exporteren met de Power BI-gegevensset.</span><span class="sxs-lookup"><span data-stu-id="ead01-141">How often to run the saved search and export to the Power BI dataset.</span></span>  <span data-ttu-id="ead01-142">De waarde moet tussen 15 minuten en 24 uur.</span><span class="sxs-lookup"><span data-stu-id="ead01-142">The value must be between 15 minutes and 24 hours.</span></span> |
| <span data-ttu-id="ead01-143">De naam van de gegevensset</span><span class="sxs-lookup"><span data-stu-id="ead01-143">Dataset Name</span></span> |<span data-ttu-id="ead01-144">De naam van de gegevensset in Power BI.</span><span class="sxs-lookup"><span data-stu-id="ead01-144">The name of the dataset in Power BI.</span></span>  <span data-ttu-id="ead01-145">Deze wordt gemaakt als deze niet bestaat en wordt bijgewerkt als het bestand bestaat.</span><span class="sxs-lookup"><span data-stu-id="ead01-145">It will be created if it doesn’t exist and updated if it does exist.</span></span> |

## <a name="viewing-and-removing-power-bi-schedules"></a><span data-ttu-id="ead01-146">Weergeven en verwijderen van Power BI-schema 's</span><span class="sxs-lookup"><span data-stu-id="ead01-146">Viewing and Removing Power BI Schedules</span></span>
<span data-ttu-id="ead01-147">De lijst met bestaande Power BI-schema's met de volgende procedure weergeven.</span><span class="sxs-lookup"><span data-stu-id="ead01-147">View the list of existing Power BI Schedules with the following procedure.</span></span>

1. <span data-ttu-id="ead01-148">Klik in de OMS-console op de **instellingen** tegel.</span><span class="sxs-lookup"><span data-stu-id="ead01-148">In the OMS console click the **Settings** tile.</span></span>
2. <span data-ttu-id="ead01-149">Selecteer **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="ead01-149">Select **Power BI**.</span></span>

<span data-ttu-id="ead01-150">Naast de details van de planning, worden het aantal keren dat met de planning wordt uitgevoerd in de afgelopen week en de status van de laatste synchronisatie weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ead01-150">In addition to the details of the schedule, the number of times that the schedule has run in the past week and the status of the last sync are displayed.</span></span>  <span data-ttu-id="ead01-151">Als de synchronisatie fouten optreden, kunt u de koppeling om uit te voeren een zoekopdracht logboek voor records met gegevens over de fout kunt klikken.</span><span class="sxs-lookup"><span data-stu-id="ead01-151">If the sync encountered errors, you can click the link to run a log search for records with details of the error.</span></span>

<span data-ttu-id="ead01-152">U kunt een schema verwijderen door te klikken op de **X** in de **verwijderen kolom**.</span><span class="sxs-lookup"><span data-stu-id="ead01-152">You can remove a schedule by clicking on the **X** in the **Remove column**.</span></span>  <span data-ttu-id="ead01-153">U kunt een planning uitschakelen door het selecteren van **uit**.</span><span class="sxs-lookup"><span data-stu-id="ead01-153">You can disable a schedule by selecting **Off**.</span></span>  <span data-ttu-id="ead01-154">Voor het wijzigen van een schema moet u deze verwijderen en maak deze opnieuw met de nieuwe instellingen.</span><span class="sxs-lookup"><span data-stu-id="ead01-154">To modify a schedule you must remove it and recreate it with the new settings.</span></span>

![Power BI-schema 's](media/log-analytics-powerbi/schedules.png)

## <a name="sample-walkthrough"></a><span data-ttu-id="ead01-156">Voorbeeld-overzicht</span><span class="sxs-lookup"><span data-stu-id="ead01-156">Sample walkthrough</span></span>
<span data-ttu-id="ead01-157">De volgende sectie wordt een voorbeeld van een Power BI-schema maken en de bijbehorende gegevensset gebruiken voor het maken van een eenvoudig rapport uitgelegd.</span><span class="sxs-lookup"><span data-stu-id="ead01-157">The following section walks through an example of creating a Power BI Schedule and using its dataset to create a simple report.</span></span>  <span data-ttu-id="ead01-158">In dit voorbeeld alle prestatiegegevens voor een set computers wordt geëxporteerd naar Power BI en vervolgens een lijngrafiek gemaakt om processorgebruik weer te geven.</span><span class="sxs-lookup"><span data-stu-id="ead01-158">In this example, all performance data for a set of computers is exported to Power BI and then a line graph is created to display processor utilization.</span></span>

### <a name="create-log-search"></a><span data-ttu-id="ead01-159">Logboek zoekopdracht maken</span><span class="sxs-lookup"><span data-stu-id="ead01-159">Create log search</span></span>
<span data-ttu-id="ead01-160">Begin met het maken van een zoekopdracht logboek voor de gegevens die we willen verzenden naar de gegevensset.</span><span class="sxs-lookup"><span data-stu-id="ead01-160">We start by creating a log search for the data that we want to send to the dataset.</span></span>  <span data-ttu-id="ead01-161">In dit voorbeeld gebruiken we een query alle prestatiegegevens voor computers met een naam die begint retourneert met *srv*.</span><span class="sxs-lookup"><span data-stu-id="ead01-161">In this example, we’ll use a query that returns all performance data for computers with a name that starts with *srv*.</span></span>  

![Power BI-schema 's](media/log-analytics-powerbi/walkthrough-query.png)

### <a name="create-power-bi-search"></a><span data-ttu-id="ead01-163">Zoeken met Power BI maken</span><span class="sxs-lookup"><span data-stu-id="ead01-163">Create Power BI Search</span></span>
<span data-ttu-id="ead01-164">We klikt u op de **Power BI** knop opent u het dialoogvenster Power BI en geef de vereiste gegevens.</span><span class="sxs-lookup"><span data-stu-id="ead01-164">We click the **Power BI** button to open the Power BI dialog and provide the required information.</span></span>  <span data-ttu-id="ead01-165">We willen dat deze zoekopdracht uitvoeren één keer per uur en maken van een gegevensset met de naam *Contoso Perf*.</span><span class="sxs-lookup"><span data-stu-id="ead01-165">We want this search to run once per hour and create a dataset called *Contoso Perf*.</span></span>  <span data-ttu-id="ead01-166">Aangezien we al de zoekopdracht openen die de gegevens die we willen maakt hebben, wordt de standaardwaarde van houden *huidige zoekquery gebruiken* voor **opgeslagen zoekopdrachten**.</span><span class="sxs-lookup"><span data-stu-id="ead01-166">Since we already have the search open that creates the data we want, we keep the default of *Use current search query* for **Saved Search**.</span></span>

![Zoeken met Power BI](media/log-analytics-powerbi/walkthrough-schedule.png)

### <a name="verify-power-bi-search"></a><span data-ttu-id="ead01-168">Controleer of zoeken met Power BI</span><span class="sxs-lookup"><span data-stu-id="ead01-168">Verify Power BI Search</span></span>
<span data-ttu-id="ead01-169">Om te controleren of we de planning correct hebt gemaakt, wordt de lijst weergeven met Power BI zoekopdrachten op het **instellingen** -tegel in het dashboard OMS.</span><span class="sxs-lookup"><span data-stu-id="ead01-169">To verify that we created the schedule correctly, we view the list of Power BI Searches under the **Settings** tile in the OMS dashboard.</span></span>  <span data-ttu-id="ead01-170">Er wacht een paar minuten en vernieuw deze weergave totdat deze rapporteert dat de synchronisatie is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ead01-170">We wait several minutes and refresh this view until it reports that the sync has been run.</span></span>

![Zoeken met Power BI](media/log-analytics-powerbi/walkthrough-schedules.png)

### <a name="verify-the-dataset-in-power-bi"></a><span data-ttu-id="ead01-172">Controleer of de gegevensset in Power BI</span><span class="sxs-lookup"><span data-stu-id="ead01-172">Verify the dataset in Power BI</span></span>
<span data-ttu-id="ead01-173">We Meld u aan bij onze account bij [powerbi.microsoft.com](http://powerbi.microsoft.com/) en schuif naar **gegevenssets** onderaan in het linkerdeelvenster.</span><span class="sxs-lookup"><span data-stu-id="ead01-173">We log into our account at [powerbi.microsoft.com](http://powerbi.microsoft.com/) and scroll to **Datasets** at the bottom of the left pane.</span></span>  <span data-ttu-id="ead01-174">U ziet dat de *Contoso Perf* gegevensset wordt vermeld die aangeeft dat de export is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ead01-174">We can see that the *Contoso Perf* dataset is listed indicating that our export has run successfully.</span></span>

![Power BI-gegevensset](media/log-analytics-powerbi/walkthrough-datasets.png)

### <a name="create-report-based-on-dataset"></a><span data-ttu-id="ead01-176">Maken op basis van gegevensset</span><span class="sxs-lookup"><span data-stu-id="ead01-176">Create report based on dataset</span></span>
<span data-ttu-id="ead01-177">U selecteert de **Contoso Perf** gegevensset en klik vervolgens op **resultaten** in de **velden** deelvenster op het recht om de velden die deel van deze gegevensset uitmaken te bekijken.</span><span class="sxs-lookup"><span data-stu-id="ead01-177">We select the **Contoso Perf** dataset and then click on **Results** in the **Fields** pane on the right to view the fields that are part of this dataset.</span></span>  <span data-ttu-id="ead01-178">We uitvoeren de volgende acties voor het maken van een lijngrafiek processorgebruik voor elke computer weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ead01-178">To create a line graph showing processor utilization for each computer, we perform the following actions.</span></span>

1. <span data-ttu-id="ead01-179">Selecteer de regel grafiek visualisatie.</span><span class="sxs-lookup"><span data-stu-id="ead01-179">Select the Line chart visualization.</span></span>
2. <span data-ttu-id="ead01-180">Sleep **ObjectName** naar **rapport niveau filter** en Controleer **Processor**.</span><span class="sxs-lookup"><span data-stu-id="ead01-180">Drag **ObjectName** to **Report level filter** and check **Processor**.</span></span>
3. <span data-ttu-id="ead01-181">Sleep **CounterName** naar **rapport niveau filter** en Controleer **percentage processortijd**.</span><span class="sxs-lookup"><span data-stu-id="ead01-181">Drag **CounterName** to **Report level filter** and check **% Processor Time**.</span></span>
4. <span data-ttu-id="ead01-182">Sleep **tegenwaarde** naar **waarden**.</span><span class="sxs-lookup"><span data-stu-id="ead01-182">Drag **CounterValue** to **Values**.</span></span>
5. <span data-ttu-id="ead01-183">Sleep **Computer** naar **legenda**.</span><span class="sxs-lookup"><span data-stu-id="ead01-183">Drag **Computer** to **Legend**.</span></span>
6. <span data-ttu-id="ead01-184">Sleep **TimeGenerated** naar **as**.</span><span class="sxs-lookup"><span data-stu-id="ead01-184">Drag **TimeGenerated** to **Axis**.</span></span>

<span data-ttu-id="ead01-185">U ziet dat de resulterende lijngrafiek wordt weergegeven met de gegevens van onze gegevensset.</span><span class="sxs-lookup"><span data-stu-id="ead01-185">We can see that the resulting line graph is displayed with the data from our dataset.</span></span>

![Power BI-lijndiagram](media/log-analytics-powerbi/walkthrough-linegraph.png)

### <a name="save-the-report"></a><span data-ttu-id="ead01-187">Het rapport opslaan</span><span class="sxs-lookup"><span data-stu-id="ead01-187">Save the report</span></span>
<span data-ttu-id="ead01-188">We het rapport door te klikken op de knop opslaan boven aan het scherm opslaan en valideren nu wordt vermeld in de sectie rapporten in het linkerdeelvenster.</span><span class="sxs-lookup"><span data-stu-id="ead01-188">We save the report by clicking on the Save button at the top of the screen and validate that it is now listed in the Reports section in the left pane.</span></span>

![Power BI-rapporten](media/log-analytics-powerbi/walkthrough-report.png)

## <a name="next-steps"></a><span data-ttu-id="ead01-190">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ead01-190">Next steps</span></span>
* <span data-ttu-id="ead01-191">Meer informatie over [Meld zoekopdrachten](log-analytics-log-searches.md) voor query's opbouwen die kunnen worden geëxporteerd naar Power BI.</span><span class="sxs-lookup"><span data-stu-id="ead01-191">Learn about [log searches](log-analytics-log-searches.md) to build queries that can be exported to Power BI.</span></span>
* <span data-ttu-id="ead01-192">Meer informatie over [Power BI](http://powerbi.microsoft.com) visualisaties op basis van logboekanalyse uitvoer bouwen.</span><span class="sxs-lookup"><span data-stu-id="ead01-192">Learn more about [Power BI](http://powerbi.microsoft.com) to build visualizations based on Log Analytics exports.</span></span>
