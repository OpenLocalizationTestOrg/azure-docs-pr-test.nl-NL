---
title: aaaExport logboekanalyse gegevens tooPower BI | Microsoft Docs
description: "Power BI is een cloudgebaseerde business analytics-service van Microsoft die uitgebreide visualisaties en rapporten voor analyse van verschillende sets van gegevens biedt.  Log Analytics kunt continu gegevens exporteren vanuit Hallo OMS-opslagplaats in Power BI zodat u van de vorm van visualisaties en hulpmiddelen voor analyse gebruikmaken kunt.  Dit artikel wordt beschreven hoe tooconfigure query's in logboekanalyse die automatisch geëxporteerd tooPower BI met regelmatige tussenpozen."
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
ms.openlocfilehash: 4822f99677e5d1080c72e95cda410da81615bac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="export-log-analytics-data-toopower-bi"></a><span data-ttu-id="0bab3-105">Log Analytics gegevens tooPower BI exporteren</span><span class="sxs-lookup"><span data-stu-id="0bab3-105">Export Log Analytics data tooPower BI</span></span>

>[!NOTE]
> <span data-ttu-id="0bab3-106">Als uw werkruimte bijgewerkte toohello is [nieuwe logboekanalyse querytaal](log-analytics-log-search-upgrade.md), en vervolgens dit proces voor het exporteren van logboekanalyse gegevens tooPower BI niet meer werken.</span><span class="sxs-lookup"><span data-stu-id="0bab3-106">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then this process for exporting Log Analytics data tooPower BI will no longer work.</span></span>  <span data-ttu-id="0bab3-107">Eventuele bestaande schema's die u hebt gemaakt voordat u de upgrade wordt uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="0bab3-107">Any existing schedules that you created before upgrading will become disabled.</span></span> 
>
> <span data-ttu-id="0bab3-108">Na de upgrade hello Azure Log Analytics gebruikt hetzelfde platform als Application Insights en gebruik van dezelfde tooexport Log Analytics-query's tooPower BI als verwerken Hallo [Hallo proces tooexport Application Insights tooPower BI query](../application-insights/app-insights-export-power-bi.md#export-analytics-queries).</span><span class="sxs-lookup"><span data-stu-id="0bab3-108">After upgrade, Azure Log Analytics uses hello same platform as Application Insights, and you use hello same process tooexport Log Analytics queries tooPower BI as [hello process tooexport Application Insights queries tooPower BI](../application-insights/app-insights-export-power-bi.md#export-analytics-queries).</span></span>  <span data-ttu-id="0bab3-109">Kunt u met behulp van Hallo Analytics console zoals beschreven in dit artikel Hallo-query exporteren of kunt u Hallo **Power BI** knop Hallo boven aan het welkomstscherm in Hallo logboek Search-portal.</span><span class="sxs-lookup"><span data-stu-id="0bab3-109">You can either export hello query using hello Analytics console as described in that article, or you can select hello **Power BI** button at hello top of hello screen in hello Log Search portal.</span></span>



<span data-ttu-id="0bab3-110">[Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/) is een service in de cloud business analytics van Microsoft die uitgebreide visualisaties en rapporten voor analyse van verschillende sets van gegevens biedt.</span><span class="sxs-lookup"><span data-stu-id="0bab3-110">[Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/) is a cloud based business analytics service from Microsoft that provides rich visualizations and reports for analysis of different sets of data.</span></span>  <span data-ttu-id="0bab3-111">Log Analytics kunt automatisch gegevens exporteren vanuit Hallo OMS-opslagplaats in Power BI zodat u van de vorm van visualisaties en hulpmiddelen voor analyse gebruikmaken kunt.</span><span class="sxs-lookup"><span data-stu-id="0bab3-111">Log Analytics can automatically export data from hello OMS repository into Power BI so you can leverage its visualizations and analysis tools.</span></span>

<span data-ttu-id="0bab3-112">Wanneer u Power BI met logboekanalyse configureert, maakt u log-query's die hun resultaten toocorresponding gegevenssets in Power BI exporteren.</span><span class="sxs-lookup"><span data-stu-id="0bab3-112">When you configure Power BI with Log Analytics, you create log queries that export their results toocorresponding datasets in Power BI.</span></span>  <span data-ttu-id="0bab3-113">blijft tooautomatically uitvoeren volgens een schema dat u tookeep Hallo gegevensset up toodate met de meest recente gegevens Hallo verzameld door logboekanalyse definiëren Hallo query en exporteren.</span><span class="sxs-lookup"><span data-stu-id="0bab3-113">hello query and export continues tooautomatically run on a schedule that you define tookeep hello dataset up toodate with hello latest data collected by Log Analytics.</span></span>

![Log Analytics tooPower BI](media/log-analytics-powerbi/overview.png)

## <a name="power-bi-schedules"></a><span data-ttu-id="0bab3-115">Power BI-schema 's</span><span class="sxs-lookup"><span data-stu-id="0bab3-115">Power BI Schedules</span></span>
<span data-ttu-id="0bab3-116">Een *Power BI planning* bevat een logboek zoekopdracht die een set gegevens exporteert van Hallo OMS-opslagplaats tooa bijbehorende gegevensset in Power BI en een planning die definieert hoe vaak deze zoekopdracht tookeep Hallo gegevensset huidige wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0bab3-116">A *Power BI Schedule* includes a log search that exports a set of data from hello OMS repository tooa corresponding dataset in Power BI and a schedule that defines how often this search is run tookeep hello dataset current.</span></span>

<span data-ttu-id="0bab3-117">Hallo velden in de gegevensset Hallo komt overeen met de Hallo eigenschappen van Hallo records geretourneerd door Hallo logboek zoeken.</span><span class="sxs-lookup"><span data-stu-id="0bab3-117">hello fields in hello dataset will match hello properties of hello records returned by hello log search.</span></span>  <span data-ttu-id="0bab3-118">Als Hallo search records van verschillende typen retourneert en vervolgens Hallo gegevensset alle bevat opgenomen eigenschappen van elk van de Hallo Hallo recordtypen.</span><span class="sxs-lookup"><span data-stu-id="0bab3-118">If hello search returns records of different types then hello dataset will include all of hello properties from each of hello included record types.</span></span>  

> [!NOTE]
> <span data-ttu-id="0bab3-119">Het is een best practice toouse een zoekquery logboek die onbewerkte gegevens retourneert als tegengestelde tooperforming een consolidatie met opdrachten zoals [meting](log-analytics-search-reference.md#measure).</span><span class="sxs-lookup"><span data-stu-id="0bab3-119">It is a best practice toouse a log search query that returns raw data as opposed tooperforming any consolidation using commands such as [Measure](log-analytics-search-reference.md#measure).</span></span>  <span data-ttu-id="0bab3-120">U kunt een aggregatie en berekeningen in Power BI van ruwe gegevens Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="0bab3-120">You can perform any aggregation and calculations in Power BI from hello raw data.</span></span>
>
>

## <a name="connecting-oms-workspace-toopower-bi"></a><span data-ttu-id="0bab3-121">Verbinding maken met OMS-werkruimte tooPower BI</span><span class="sxs-lookup"><span data-stu-id="0bab3-121">Connecting OMS workspace tooPower BI</span></span>
<span data-ttu-id="0bab3-122">Voordat u van logboekanalyse tooPower BI exporteren kunt, moet u verbinding maken met uw OMS werkruimte tooyour Power BI-account met Hallo procedure te volgen.</span><span class="sxs-lookup"><span data-stu-id="0bab3-122">Before you can export from Log Analytics tooPower BI, you must connect your OMS workspace tooyour Power BI account using hello following procedure.</span></span>  

1. <span data-ttu-id="0bab3-123">Klik in Hallo OMS-console op Hallo **instellingen** tegel.</span><span class="sxs-lookup"><span data-stu-id="0bab3-123">In hello OMS console click hello **Settings** tile.</span></span>
2. <span data-ttu-id="0bab3-124">Selecteer **Accounts**.</span><span class="sxs-lookup"><span data-stu-id="0bab3-124">Select **Accounts**.</span></span>
3. <span data-ttu-id="0bab3-125">In Hallo **werkruimte** sectie Klik **tooPower BI-Account verbinding**.</span><span class="sxs-lookup"><span data-stu-id="0bab3-125">In hello **Workspace Information** section click **Connect tooPower BI Account**.</span></span>
4. <span data-ttu-id="0bab3-126">Geef Hallo referenties voor uw Power BI-account.</span><span class="sxs-lookup"><span data-stu-id="0bab3-126">Enter hello credentials for your Power BI account.</span></span>

## <a name="create-a-power-bi-schedule"></a><span data-ttu-id="0bab3-127">Maak een planning van Power BI</span><span class="sxs-lookup"><span data-stu-id="0bab3-127">Create a Power BI Schedule</span></span>
<span data-ttu-id="0bab3-128">Maak een Power BI-schema voor elke gegevensset met Hallo procedure te volgen.</span><span class="sxs-lookup"><span data-stu-id="0bab3-128">Create a Power BI Schedule for each dataset using hello following procedure.</span></span>

1. <span data-ttu-id="0bab3-129">Klik in Hallo OMS-console op Hallo **logboek zoeken** tegel.</span><span class="sxs-lookup"><span data-stu-id="0bab3-129">In hello OMS console click hello **Log Search** tile.</span></span>
2. <span data-ttu-id="0bab3-130">Typ in een nieuwe query of Selecteer een opgeslagen zoekopdracht dat retourneert gegevens dat u wilt dat tooexport te Hallo**Power BI**.</span><span class="sxs-lookup"><span data-stu-id="0bab3-130">Type in a new query or select a saved search that returns hello data that you want tooexport too**Power BI**.</span></span>  
3. <span data-ttu-id="0bab3-131">Klik op Hallo **Power BI** knop bovenaan Hallo Hallo pagina tooopen hello **Power BI** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="0bab3-131">Click hello **Power BI** button at hello top of hello page tooopen hello **Power BI** dialog.</span></span>
4. <span data-ttu-id="0bab3-132">Geef informatie op Hallo in Hallo hieronder tabel en klik **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="0bab3-132">Provide hello information in hello following table and click **Save**.</span></span>

| <span data-ttu-id="0bab3-133">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="0bab3-133">Property</span></span> | <span data-ttu-id="0bab3-134">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0bab3-134">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="0bab3-135">Naam</span><span class="sxs-lookup"><span data-stu-id="0bab3-135">Name</span></span> |<span data-ttu-id="0bab3-136">Naam tooidentify Hallo plannen wanneer u Hallo lijst met Power BI-schema's weergeven.</span><span class="sxs-lookup"><span data-stu-id="0bab3-136">Name tooidentify hello schedule when you view hello list of Power BI schedules.</span></span> |
| <span data-ttu-id="0bab3-137">Opgeslagen zoekopdracht</span><span class="sxs-lookup"><span data-stu-id="0bab3-137">Saved Search</span></span> |<span data-ttu-id="0bab3-138">Hallo logboek zoeken toorun.</span><span class="sxs-lookup"><span data-stu-id="0bab3-138">hello log search toorun.</span></span>  <span data-ttu-id="0bab3-139">Selecteer de huidige query Hallo of Selecteer een bestaande opgeslagen zoekopdracht uit de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="0bab3-139">You can either select hello current query or select an existing saved search from hello dropdown box.</span></span> |
| <span data-ttu-id="0bab3-140">Planning</span><span class="sxs-lookup"><span data-stu-id="0bab3-140">Schedule</span></span> |<span data-ttu-id="0bab3-141">Hoe vaak toorun Hallo opgeslagen zoeken en te exporteren toohello Power BI-gegevensset.</span><span class="sxs-lookup"><span data-stu-id="0bab3-141">How often toorun hello saved search and export toohello Power BI dataset.</span></span>  <span data-ttu-id="0bab3-142">Hallo-waarde moet tussen 15 minuten en 24 uur.</span><span class="sxs-lookup"><span data-stu-id="0bab3-142">hello value must be between 15 minutes and 24 hours.</span></span> |
| <span data-ttu-id="0bab3-143">De naam van de gegevensset</span><span class="sxs-lookup"><span data-stu-id="0bab3-143">Dataset Name</span></span> |<span data-ttu-id="0bab3-144">Hallo-naam van de gegevensset Hallo in Power BI.</span><span class="sxs-lookup"><span data-stu-id="0bab3-144">hello name of hello dataset in Power BI.</span></span>  <span data-ttu-id="0bab3-145">Deze wordt gemaakt als deze niet bestaat en wordt bijgewerkt als het bestand bestaat.</span><span class="sxs-lookup"><span data-stu-id="0bab3-145">It will be created if it doesn’t exist and updated if it does exist.</span></span> |

## <a name="viewing-and-removing-power-bi-schedules"></a><span data-ttu-id="0bab3-146">Weergeven en verwijderen van Power BI-schema 's</span><span class="sxs-lookup"><span data-stu-id="0bab3-146">Viewing and Removing Power BI Schedules</span></span>
<span data-ttu-id="0bab3-147">Hallo-lijst weergeven van de bestaande planningen van Power BI Hello procedure te volgen.</span><span class="sxs-lookup"><span data-stu-id="0bab3-147">View hello list of existing Power BI Schedules with hello following procedure.</span></span>

1. <span data-ttu-id="0bab3-148">Klik in Hallo OMS-console op Hallo **instellingen** tegel.</span><span class="sxs-lookup"><span data-stu-id="0bab3-148">In hello OMS console click hello **Settings** tile.</span></span>
2. <span data-ttu-id="0bab3-149">Selecteer **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="0bab3-149">Select **Power BI**.</span></span>

<span data-ttu-id="0bab3-150">Bovendien toohello details van Hallo plannen, Hallo aantal keren dat planning Hallo afgelopen week in Hallo is uitgevoerd en Hallo status van de laatste synchronisatie Hallo worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0bab3-150">In addition toohello details of hello schedule, hello number of times that hello schedule has run in hello past week and hello status of hello last sync are displayed.</span></span>  <span data-ttu-id="0bab3-151">Hallo-synchronisatie aangetroffen fouten, u kunt klikken op Hallo koppeling toorun logboek zoekt records met details van Hallo-fout.</span><span class="sxs-lookup"><span data-stu-id="0bab3-151">If hello sync encountered errors, you can click hello link toorun a log search for records with details of hello error.</span></span>

<span data-ttu-id="0bab3-152">U kunt een schema verwijderen door te klikken op Hallo **X** in Hallo **verwijderen kolom**.</span><span class="sxs-lookup"><span data-stu-id="0bab3-152">You can remove a schedule by clicking on hello **X** in hello **Remove column**.</span></span>  <span data-ttu-id="0bab3-153">U kunt een planning uitschakelen door het selecteren van **uit**.</span><span class="sxs-lookup"><span data-stu-id="0bab3-153">You can disable a schedule by selecting **Off**.</span></span>  <span data-ttu-id="0bab3-154">toomodify een schema moet u deze verwijderen en maak deze opnieuw met de nieuwe instellingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="0bab3-154">toomodify a schedule you must remove it and recreate it with hello new settings.</span></span>

![Power BI-schema 's](media/log-analytics-powerbi/schedules.png)

## <a name="sample-walkthrough"></a><span data-ttu-id="0bab3-156">Voorbeeld-overzicht</span><span class="sxs-lookup"><span data-stu-id="0bab3-156">Sample walkthrough</span></span>
<span data-ttu-id="0bab3-157">Hallo volgende sectie wordt uitgelegd een voorbeeld van een Power BI-schema maken en gebruiken van de gegevensset toocreate een eenvoudig rapport.</span><span class="sxs-lookup"><span data-stu-id="0bab3-157">hello following section walks through an example of creating a Power BI Schedule and using its dataset toocreate a simple report.</span></span>  <span data-ttu-id="0bab3-158">In dit voorbeeld alle prestatiegegevens voor een set computers is geëxporteerde tooPower BI en vervolgens een lijngrafiek toodisplay processorgebruik is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0bab3-158">In this example, all performance data for a set of computers is exported tooPower BI and then a line graph is created toodisplay processor utilization.</span></span>

### <a name="create-log-search"></a><span data-ttu-id="0bab3-159">Logboek zoekopdracht maken</span><span class="sxs-lookup"><span data-stu-id="0bab3-159">Create log search</span></span>
<span data-ttu-id="0bab3-160">Begin met het maken van een zoekopdracht logboek voor Hallo gegevens willen we toosend toohello gegevensset.</span><span class="sxs-lookup"><span data-stu-id="0bab3-160">We start by creating a log search for hello data that we want toosend toohello dataset.</span></span>  <span data-ttu-id="0bab3-161">In dit voorbeeld gebruiken we een query alle prestatiegegevens voor computers met een naam die begint retourneert met *srv*.</span><span class="sxs-lookup"><span data-stu-id="0bab3-161">In this example, we’ll use a query that returns all performance data for computers with a name that starts with *srv*.</span></span>  

![Power BI-schema 's](media/log-analytics-powerbi/walkthrough-query.png)

### <a name="create-power-bi-search"></a><span data-ttu-id="0bab3-163">Zoeken met Power BI maken</span><span class="sxs-lookup"><span data-stu-id="0bab3-163">Create Power BI Search</span></span>
<span data-ttu-id="0bab3-164">We klikt u op Hallo **Power BI** tooopen Hallo Power BI dialoogvenster knop en Hallo vereist informatie te bieden.</span><span class="sxs-lookup"><span data-stu-id="0bab3-164">We click hello **Power BI** button tooopen hello Power BI dialog and provide hello required information.</span></span>  <span data-ttu-id="0bab3-165">We wilt dat deze zoekopdracht toorun één keer per uur en maken van een gegevensset met de naam *Contoso Perf*.</span><span class="sxs-lookup"><span data-stu-id="0bab3-165">We want this search toorun once per hour and create a dataset called *Contoso Perf*.</span></span>  <span data-ttu-id="0bab3-166">Aangezien we Hallo zoeken openen die Hallo gegevens we willen maakt al hebt, wij houden Hallo standaardwaarde *huidige zoekquery gebruiken* voor **opgeslagen zoekopdrachten**.</span><span class="sxs-lookup"><span data-stu-id="0bab3-166">Since we already have hello search open that creates hello data we want, we keep hello default of *Use current search query* for **Saved Search**.</span></span>

![Zoeken met Power BI](media/log-analytics-powerbi/walkthrough-schedule.png)

### <a name="verify-power-bi-search"></a><span data-ttu-id="0bab3-168">Controleer of zoeken met Power BI</span><span class="sxs-lookup"><span data-stu-id="0bab3-168">Verify Power BI Search</span></span>
<span data-ttu-id="0bab3-169">tooverify dat we Hallo planning correct hebt gemaakt, we Hallo lijst weergeven met Power BI zoekopdrachten onder Hallo **instellingen** -tegel in Hallo OMS-dashboard.</span><span class="sxs-lookup"><span data-stu-id="0bab3-169">tooverify that we created hello schedule correctly, we view hello list of Power BI Searches under hello **Settings** tile in hello OMS dashboard.</span></span>  <span data-ttu-id="0bab3-170">Er wacht een paar minuten en vernieuw deze weergave totdat deze rapporteert dat Hallo synchronisatie is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0bab3-170">We wait several minutes and refresh this view until it reports that hello sync has been run.</span></span>

![Zoeken met Power BI](media/log-analytics-powerbi/walkthrough-schedules.png)

### <a name="verify-hello-dataset-in-power-bi"></a><span data-ttu-id="0bab3-172">Controleer of de gegevensset Hallo in Power BI</span><span class="sxs-lookup"><span data-stu-id="0bab3-172">Verify hello dataset in Power BI</span></span>
<span data-ttu-id="0bab3-173">We Meld u aan bij onze account bij [powerbi.microsoft.com](http://powerbi.microsoft.com/) en schuif te**gegevenssets** Hallo onder het linkerdeelvenster Hallo aan.</span><span class="sxs-lookup"><span data-stu-id="0bab3-173">We log into our account at [powerbi.microsoft.com](http://powerbi.microsoft.com/) and scroll too**Datasets** at hello bottom of hello left pane.</span></span>  <span data-ttu-id="0bab3-174">Zien we dat Hallo *Contoso Perf* gegevensset wordt vermeld die aangeeft dat de export is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0bab3-174">We can see that hello *Contoso Perf* dataset is listed indicating that our export has run successfully.</span></span>

![Power BI-gegevensset](media/log-analytics-powerbi/walkthrough-datasets.png)

### <a name="create-report-based-on-dataset"></a><span data-ttu-id="0bab3-176">Maken op basis van gegevensset</span><span class="sxs-lookup"><span data-stu-id="0bab3-176">Create report based on dataset</span></span>
<span data-ttu-id="0bab3-177">U selecteert Hallo **Contoso Perf** gegevensset en klik vervolgens op **resultaten** in Hallo **velden** deelvenster op Hallo rechts tooview Hallo velden die deel van deze dataset uitmaken.</span><span class="sxs-lookup"><span data-stu-id="0bab3-177">We select hello **Contoso Perf** dataset and then click on **Results** in hello **Fields** pane on hello right tooview hello fields that are part of this dataset.</span></span>  <span data-ttu-id="0bab3-178">toocreate een processorgebruik regel grafiek weergeven voor elke computer, we Hallo van de volgende activiteiten uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="0bab3-178">toocreate a line graph showing processor utilization for each computer, we perform hello following actions.</span></span>

1. <span data-ttu-id="0bab3-179">Selecteert u grafiekweergave Hallo-regel.</span><span class="sxs-lookup"><span data-stu-id="0bab3-179">Select hello Line chart visualization.</span></span>
2. <span data-ttu-id="0bab3-180">Sleep **ObjectName** te**rapport niveau filter** en Controleer **Processor**.</span><span class="sxs-lookup"><span data-stu-id="0bab3-180">Drag **ObjectName** too**Report level filter** and check **Processor**.</span></span>
3. <span data-ttu-id="0bab3-181">Sleep **CounterName** te**rapport niveau filter** en Controleer **percentage processortijd**.</span><span class="sxs-lookup"><span data-stu-id="0bab3-181">Drag **CounterName** too**Report level filter** and check **% Processor Time**.</span></span>
4. <span data-ttu-id="0bab3-182">Sleep **tegenwaarde** te**waarden**.</span><span class="sxs-lookup"><span data-stu-id="0bab3-182">Drag **CounterValue** too**Values**.</span></span>
5. <span data-ttu-id="0bab3-183">Sleep **Computer** te**legenda**.</span><span class="sxs-lookup"><span data-stu-id="0bab3-183">Drag **Computer** too**Legend**.</span></span>
6. <span data-ttu-id="0bab3-184">Sleep **TimeGenerated** te**as**.</span><span class="sxs-lookup"><span data-stu-id="0bab3-184">Drag **TimeGenerated** too**Axis**.</span></span>

<span data-ttu-id="0bab3-185">U ziet dat Hallo resulterende lijngrafiek met Hallo gegevens van onze gegevensset wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0bab3-185">We can see that hello resulting line graph is displayed with hello data from our dataset.</span></span>

![Power BI-lijndiagram](media/log-analytics-powerbi/walkthrough-linegraph.png)

### <a name="save-hello-report"></a><span data-ttu-id="0bab3-187">Hallo rapport opslaan</span><span class="sxs-lookup"><span data-stu-id="0bab3-187">Save hello report</span></span>
<span data-ttu-id="0bab3-188">We opslaan Hallo rapport door te klikken op Hallo knop Hallo boven aan het welkomstscherm opslaan en het is nu opgenomen in Hallo rapporten sectie in het linkerdeelvenster Hallo valideren.</span><span class="sxs-lookup"><span data-stu-id="0bab3-188">We save hello report by clicking on hello Save button at hello top of hello screen and validate that it is now listed in hello Reports section in hello left pane.</span></span>

![Power BI-rapporten](media/log-analytics-powerbi/walkthrough-report.png)

## <a name="next-steps"></a><span data-ttu-id="0bab3-190">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0bab3-190">Next steps</span></span>
* <span data-ttu-id="0bab3-191">Meer informatie over [Meld zoekopdrachten](log-analytics-log-searches.md) toobuild-query's die kunnen worden geëxporteerd tooPower BI.</span><span class="sxs-lookup"><span data-stu-id="0bab3-191">Learn about [log searches](log-analytics-log-searches.md) toobuild queries that can be exported tooPower BI.</span></span>
* <span data-ttu-id="0bab3-192">Meer informatie over [Power BI](http://powerbi.microsoft.com) toobuild visualisaties op basis van logboekanalyse uitvoer.</span><span class="sxs-lookup"><span data-stu-id="0bab3-192">Learn more about [Power BI](http://powerbi.microsoft.com) toobuild visualizations based on Log Analytics exports.</span></span>
