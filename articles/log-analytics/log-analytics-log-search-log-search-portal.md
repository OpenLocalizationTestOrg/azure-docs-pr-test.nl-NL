---
title: Met behulp van de portal logboek zoeken in Azure Log Analytics | Microsoft Docs
description: Dit artikel bevat een zelfstudie waarin wordt beschreven hoe maken zoekopdrachten logboek en analyseren van gegevens die zijn opgeslagen in de werkruimte voor logboekanalyse via de portal logboek zoeken.  De zelfstudie omvat het uitvoeren van enkele eenvoudige query's voor verschillende soorten gegevens en analyseren van resultaten retourneren.
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: 6fc556ceb34cde26d5f3789a2397cdaa34b0b84d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-log-searches-in-azure-log-analytics-using-the-log-search-portal"></a><span data-ttu-id="0f1fd-104">Logboek zoekopdrachten maken in Azure-logboekanalyse via de portal logboek zoeken</span><span class="sxs-lookup"><span data-stu-id="0f1fd-104">Create log searches in Azure Log Analytics using the Log Search portal</span></span>

> [!NOTE]
> <span data-ttu-id="0f1fd-105">Dit artikel wordt beschreven in de Azure-logboekanalyse met behulp van de nieuwe query language van de portal logboek zoeken.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-105">This article describes the Log Search portal in Azure Log Analytics using the new query language.</span></span>  <span data-ttu-id="0f1fd-106">U kunt meer informatie over de nieuwe taal en ophalen van de procedure voor het bijwerken van de werkruimte op [Upgrade van uw Azure-logboekanalyse-werkruimte naar nieuwe logboek zoekopdracht](log-analytics-log-search-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="0f1fd-106">You can learn more about the new language and get the procedure to upgrade your workspace at [Upgrade your Azure Log Analytics workspace to new log search](log-analytics-log-search-upgrade.md).</span></span>  
>
> <span data-ttu-id="0f1fd-107">Als uw werkruimte is niet naar de nieuwe query language bijgewerkt, moet u verwijzen naar [vinden van gegevens met behulp van logboek zoekopdrachten in logboekanalyse](log-analytics-log-searches.md) voor meer informatie over de huidige versie van de portal logboek zoeken.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-107">If your workspace hasn't been upgraded to the new query language, you should refer to [Find data using log searches in Log Analytics](log-analytics-log-searches.md) for information on the current version of the Log Search portal.</span></span>

<span data-ttu-id="0f1fd-108">Dit artikel bevat een zelfstudie waarin wordt beschreven hoe maken zoekopdrachten logboek en analyseren van gegevens die zijn opgeslagen in de werkruimte voor logboekanalyse via de portal logboek zoeken.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-108">This article includes a tutorial that describes how to create log searches and analyze data stored in your Log Analytics workspace using the Log Search portal.</span></span>  <span data-ttu-id="0f1fd-109">De zelfstudie omvat het uitvoeren van enkele eenvoudige query's voor verschillende soorten gegevens en analyseren van resultaten retourneren.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-109">The tutorial includes running some simple queries to return different types of data and analyzing results.</span></span>  <span data-ttu-id="0f1fd-110">Dit artikel gaat over functies in de portal logboek zoeken voor de query te wijzigen in plaats van rechtstreeks wijzigen.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-110">It focuses on features in the Log Search portal for modifying the query rather than modifying it directly.</span></span>  <span data-ttu-id="0f1fd-111">Zie voor meer informatie over het rechtstreeks bewerken van de query de [Query Language reference](https://go.microsoft.com/fwlink/?linkid=856079).</span><span class="sxs-lookup"><span data-stu-id="0f1fd-111">For details on directly editing the query, see the [Query Language reference](https://go.microsoft.com/fwlink/?linkid=856079).</span></span>

<span data-ttu-id="0f1fd-112">Zie voor informatie over het maken van zoekopdrachten in de portal Advanced Analytics in plaats van de portal zoeken logboek [aan de slag met de Portal Analytics](https://go.microsoft.com/fwlink/?linkid=856587).</span><span class="sxs-lookup"><span data-stu-id="0f1fd-112">To create searches in the Advanced Analytics portal instead of the Log Search portal, see [Getting Started with the Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856587).</span></span>  <span data-ttu-id="0f1fd-113">Beide portals gebruiken dezelfde querytaal voor toegang tot dezelfde gegevens in de werkruimte voor logboekanalyse.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-113">Both portals use the same query language to access the same data in the Log Analytics workspace.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0f1fd-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="0f1fd-114">Prerequisites</span></span>
<span data-ttu-id="0f1fd-115">Deze zelfstudie wordt ervan uitgegaan dat u al een werkruimte voor logboekanalyse met ten minste één verbonden bron die gegevens voor de query's hebt genereert te analyseren.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-115">This tutorial assumes that you already have a Log Analytics workspace with at least one connected source that generates data for the queries to analyze.</span></span>  

- <span data-ttu-id="0f1fd-116">Als u een werkruimte geen hebt, kunt u een gratis abonnement met de procedure op [aan de slag met een werkruimte voor logboekanalyse](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0f1fd-116">If you don't have a workspace, you can create a free one using the procedure at [Get started with a Log Analytics workspace](log-analytics-get-started.md).</span></span>
- <span data-ttu-id="0f1fd-117">Verbinding maken met ten minste één [Windows-agent](log-analytics-windows-agents.md) of één [Linux-agent](log-analytics-linux-agents.md) naar de werkruimte.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-117">Connect least one [Windows agent](log-analytics-windows-agents.md) or one [Linux agent](log-analytics-linux-agents.md) to the workspace.</span></span>  

## <a name="open-the-log-search-portal"></a><span data-ttu-id="0f1fd-118">De portal logboek zoeken openen</span><span class="sxs-lookup"><span data-stu-id="0f1fd-118">Open the Log Search portal</span></span>
<span data-ttu-id="0f1fd-119">Start via de portal logboek zoeken.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-119">Start by opening the Log Search portal.</span></span>  <span data-ttu-id="0f1fd-120">U kunt openen in de Azure-portal of de OMS-portal.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-120">You can access it in either the Azure portal or the OMS portal.</span></span>

1. <span data-ttu-id="0f1fd-121">Open de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-121">Open the Azure portal.</span></span>
2. <span data-ttu-id="0f1fd-122">Navigeer met logboekanalyse en selecteer uw werkruimte.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-122">Navigate to Log Analytics and select your workspace.</span></span>
3. <span data-ttu-id="0f1fd-123">Selecteer **logboek zoeken** blijven in de Azure portal of start de OMS-portal door te selecteren **OMS-Portal** en vervolgens te klikken op de knop logboek zoeken.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-123">Either select **Log Search** to stay in the Azure portal or launch the OMS portal by selecting **OMS Portal** and then clicking the Log Search button.</span></span>

![Meld u knop Zoeken](media/log-analytics-log-search-log-search-portal/log-search-button.png)

## <a name="create-a-simple-search"></a><span data-ttu-id="0f1fd-125">Maken van een eenvoudige zoekopdrachten</span><span class="sxs-lookup"><span data-stu-id="0f1fd-125">Create a simple search</span></span>
<span data-ttu-id="0f1fd-126">De snelste manier om op te halen van sommige gegevens voor gebruik met is een eenvoudige query die als resultaat alle records in de tabel geeft.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-126">The quickest way to retrieve some data to work with is a simple query that returns all records in table.</span></span>  <span data-ttu-id="0f1fd-127">Als u hebt een Windows- of Linux-clients die zijn verbonden met uw werkruimte vervolgens hebt u gegevens in de gebeurtenis (Windows) of de tabel Syslog (Linux).</span><span class="sxs-lookup"><span data-stu-id="0f1fd-127">If you have any Windows or Linux clients connected to your workspace, then you'll have data in either the Event (Windows) or Syslog (Linux) table.</span></span>

<span data-ttu-id="0f1fd-128">Typ een de volgende query's in het zoekvak en klik op de zoekknop.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-128">Type one the following queries in the search box and click the search button.</span></span>  

```
Event
```
```
Syslog
```

<span data-ttu-id="0f1fd-129">Gegevens worden geretourneerd in de standaardlijstweergave en kunt u zien hoeveel totale records geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-129">Data is returned in the default list view, and you can see how many total records were returned.</span></span>

![Eenvoudige query](media/log-analytics-log-search-log-search-portal/log-search-portal-01.png)

<span data-ttu-id="0f1fd-131">Alleen de eerste enkele eigenschappen van elke record worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-131">Only the first few properties of each record are displayed.</span></span>  <span data-ttu-id="0f1fd-132">Klik op **meer** om alle eigenschappen voor een bepaalde record weer te geven.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-132">Click **show more** to display all properties for a particular record.</span></span>

![Details van de records](media/log-analytics-log-search-log-search-portal/log-search-portal-02.png)

## <a name="set-the-time-scope"></a><span data-ttu-id="0f1fd-134">Het bereik van de tijd instellen</span><span class="sxs-lookup"><span data-stu-id="0f1fd-134">Set the time scope</span></span>
<span data-ttu-id="0f1fd-135">Elke record die is verzameld door Log Analytics is een **TimeGenerated** eigenschap met de datum en tijd waarop de record is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-135">Every record collected by Log Analytics has a **TimeGenerated** property that contains the date and time that the record was created.</span></span>  <span data-ttu-id="0f1fd-136">Een query in de portal logboek Search retourneert alleen records met een **TimeGenerated** binnen het bereik voor tijd die aan de linkerkant van het scherm wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-136">A query in the Log Search portal only returns records with a **TimeGenerated** within the time scope that's displayed on the left side of the screen.</span></span>  

<span data-ttu-id="0f1fd-137">U kunt de tijdfilter wijzigen door de vervolgkeuzelijst selecteren of door het wijzigen van de schuifregelaar.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-137">You can change the time filter either by selecting the dropdown or by modifying the slider.</span></span>  <span data-ttu-id="0f1fd-138">De schuifregelaar wordt weergegeven een staafdiagram waarin het relatieve aantal records voor elk segment tijd binnen het bereik.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-138">The slider displays a bar graph that shows the relative number of records for each time segment within the range.</span></span>  <span data-ttu-id="0f1fd-139">Dit segment is afhankelijk van het bereik.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-139">This segment will vary depending on the range.</span></span>

<span data-ttu-id="0f1fd-140">Het standaardbereik van de tijd is **1 dag**.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-140">The default time scope is **1 day**.</span></span>  <span data-ttu-id="0f1fd-141">Wijzig deze waarde in **7 dagen**, en het totale aantal records moet verhogen.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-141">Change this value to **7 days**, and the total number of records should increase.</span></span>

![Datum tijd bereik](media/log-analytics-log-search-log-search-portal/log-search-portal-03.png)

## <a name="filter-results-of-the-query"></a><span data-ttu-id="0f1fd-143">Filteren van resultaten van de query</span><span class="sxs-lookup"><span data-stu-id="0f1fd-143">Filter results of the query</span></span>
<span data-ttu-id="0f1fd-144">Is het filterdeelvenster dat kunt u filteren op in de query zonder het te wijzigen rechtstreeks toevoegen aan de linkerkant van het scherm.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-144">On the left side of the screen is the filter pane which allows you to add filtering to the query without modifying it directly.</span></span>  <span data-ttu-id="0f1fd-145">Verschillende eigenschappen van de records geretourneerd worden met de top 10 van waarden met hun aantal records weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-145">Several properties of the records returned are displayed with their top ten values with their record count.</span></span>

<span data-ttu-id="0f1fd-146">Als u met werkt **gebeurtenis**, schakel het selectievakje in naast **fout** onder **EVENTLEVELNAME**.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-146">If you're working with **Event**, select the checkbox next to **Error** under **EVENTLEVELNAME**.</span></span>   <span data-ttu-id="0f1fd-147">Als u met werkt **Syslog**, schakel het selectievakje in naast **err** onder **FOUTCODE**.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-147">If you're working with **Syslog**, select the checkbox next to **err** under **SEVERITYLEVEL**.</span></span>  <span data-ttu-id="0f1fd-148">Hiermee wordt de query gewijzigd in een van de volgende om de resultaten op foutgebeurtenissen te beperken.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-148">This changes the query to one of the following to limit the results to error events.</span></span>

```
Event | where (EventLevelName == "Error")
```
```
Syslog | where (SeverityLevel == "err")
```

![Filteren](media/log-analytics-log-search-log-search-portal/log-search-portal-04.png)

<span data-ttu-id="0f1fd-150">Eigenschappen voor het filterdeelvenster toevoegen door te selecteren **toevoegen aan filters** vanuit het menu van de eigenschap op een van de records.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-150">Add properties to the filter pane by selecting **Add to filters** from the property menu on one of the records.</span></span>

![Toevoegen aan het filtermenu](media/log-analytics-log-search-log-search-portal/log-search-portal-02a.png)

<span data-ttu-id="0f1fd-152">U kunt hetzelfde filter instellen door het selecteren van **Filter** in het menu van de eigenschap voor een record met de waarde die u wilt filteren.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-152">You can set the same filter by selecting **Filter** from the property menu for a record with the value you want to filter.</span></span>  

<span data-ttu-id="0f1fd-153">U hoeft alleen de **Filter** optie voor eigenschappen met de naam in blauw.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-153">You only have the **Filter** option for properties with their name in blue.</span></span>  <span data-ttu-id="0f1fd-154">Dit zijn *doorzoekbare* velden die zijn geïndexeerd voor voorwaarden zoeken.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-154">These are *searchable* fields which are indexed for search conditions.</span></span>  <span data-ttu-id="0f1fd-155">Velden grijs zijn *vrije tekst doorzoekbare* velden die alleen de **verwijzingen** optie.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-155">Fields in grey are *free text searchable* fields which only have the **Show references** option.</span></span>  <span data-ttu-id="0f1fd-156">Deze optie retourneert records die deze waarde in een eigenschap.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-156">This option returns records that have that value in any property.</span></span>

![Filtermenu](media/log-analytics-log-search-log-search-portal/log-search-portal-01a.png)

<span data-ttu-id="0f1fd-158">U kunt de resultaten op één eigenschap groeperen door het selecteren van de **groeperen op** optie in het menu record.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-158">You can group the results on a single property by selecting the **Group by** option in the record menu.</span></span>  <span data-ttu-id="0f1fd-159">Hiermee voegt u toe een [samenvatten](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) operator aan de query die de resultaten in een grafiek weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-159">This will add a [summarize](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) operator to your query that displays the results in a chart.</span></span>  <span data-ttu-id="0f1fd-160">U kunt groeperen op meer dan één eigenschap, maar u moet de query rechtstreeks bewerken.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-160">You can group on more than one property, but you would need to edit the query directly.</span></span>  <span data-ttu-id="0f1fd-161">Selecteer het menu record naast de de **Computer** eigenschap en selecteer **groeperen op 'Computer'**.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-161">Select the record menu next the the **Computer** property and select **Group by 'Computer'**.</span></span>  

![Groeperen op computer](media/log-analytics-log-search-log-search-portal/log-search-portal-10.png)

## <a name="work-with-results"></a><span data-ttu-id="0f1fd-163">Werken met resultaten</span><span class="sxs-lookup"><span data-stu-id="0f1fd-163">Work with results</span></span>
<span data-ttu-id="0f1fd-164">De portal zoeken logboek heeft een aantal functies voor het werken met de resultaten van een query.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-164">The Log Search portal has a variety of features for working with the results of a query.</span></span>  <span data-ttu-id="0f1fd-165">U kunt sorteren, filter en de resultaten van Groepsbeleid voor het analyseren van de gegevens zonder de werkelijke query te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-165">You can sort, filter, and group results to analyze the data without modifying the actual query.</span></span>  <span data-ttu-id="0f1fd-166">Resultaten van een query worden niet standaard gesorteerd.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-166">Results of a query are not sorted by default.</span></span>

<span data-ttu-id="0f1fd-167">Bekijk de gegevens in tabelvorm, wat zorgt voor extra opties voor filteren en sorteren, klikt u op **tabel**.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-167">To view the data in table form which provides additional options for filtering and sorting, click **Table**.</span></span>  

![Tabelweergave](media/log-analytics-log-search-log-search-portal/log-search-portal-05.png)

<span data-ttu-id="0f1fd-169">Klik op de pijl door een record weergeven van de details voor deze record.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-169">Click the arrow by a record to view the details for that record.</span></span>

![Resultaten sorteren](media/log-analytics-log-search-log-search-portal/log-search-portal-06.png)

<span data-ttu-id="0f1fd-171">Sorteren op elk veld door te klikken op de kolomkop.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-171">Sort on any field by clicking on its column header.</span></span>

![Resultaten sorteren](media/log-analytics-log-search-log-search-portal/log-search-portal-07.png)

<span data-ttu-id="0f1fd-173">De resultaten van een specifieke waarde in de kolom door te klikken op de filterknop en het leveren van een filtervoorwaarde filteren.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-173">Filter the results on a specific value in the column by clicking the filter button and providing a filter condition.</span></span>

![Resultaten filteren](media/log-analytics-log-search-log-search-portal/log-search-portal-08.png)

<span data-ttu-id="0f1fd-175">Groeperen op een kolom met de kolomkop naar de bovenkant van de resultaten te slepen.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-175">Group on a column by dragging its column header to the top of the results.</span></span>  <span data-ttu-id="0f1fd-176">U kunt meerdere velden groeperen door meerdere kolommen naar boven te slepen.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-176">You can group on multiple fields by dragging multiple columns to the top.</span></span>

![Resultaten van Groepsbeleid](media/log-analytics-log-search-log-search-portal/log-search-portal-09.png)



## <a name="work-with-performance-data"></a><span data-ttu-id="0f1fd-178">Werken met prestatiegegevens</span><span class="sxs-lookup"><span data-stu-id="0f1fd-178">Work with performance data</span></span>
<span data-ttu-id="0f1fd-179">Prestatiegegevens voor Windows- en Linux-agents wordt opgeslagen in de werkruimte voor logboekanalyse in de **Perf** tabel.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-179">Performance data for both Windows and Linux agents is stored in the Log Analytics workspace in the **Perf** table.</span></span>  <span data-ttu-id="0f1fd-180">Prestatiegegevens net als elke andere record zoeken en we een eenvoudige query waarin retourneert dat alle records van de prestaties op dezelfde manier als met gebeurtenissen kunt schrijven.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-180">Performance records look just like any other record, and we can write a simple query that returns all performance records just like with events.</span></span>

```
Perf
```

![Prestatiegegevens](media/log-analytics-log-search-log-search-portal/log-search-portal-11.png)

<span data-ttu-id="0f1fd-182">Hoewel miljoenen records voor alle prestatieobjecten en prestatiemeteritems retourneren is niet erg nuttig.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-182">Returning millions of records for all performance objects and counters though isn't very useful.</span></span>  <span data-ttu-id="0f1fd-183">U kunt de methodes die u hierboven hebt gebruikt voor het filter de gegevens of typ de volgende query rechtstreeks in het zoekvak van het logboek.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-183">You can use the same methods you used above to filter the data or just type the following query directly into the log search box.</span></span>  <span data-ttu-id="0f1fd-184">Hiermee wordt alleen processor gebruik records voor zowel Windows- en Linux-computers.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-184">This returns only processor utilization records for both Windows and Linux computers.</span></span>

```
Perf | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time")
```

![Processorgebruik](media/log-analytics-log-search-log-search-portal/log-search-portal-12.png)

<span data-ttu-id="0f1fd-186">Dit beperkt de gegevens naar een bepaald item, maar deze nog niet plaatsen in een formulier dat is bijzonder nuttig.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-186">This limits the data to a particular counter, but it still doesn't put it in a form that's particularly useful.</span></span>  <span data-ttu-id="0f1fd-187">U kunt de gegevens in een lijndiagram worden weergegeven, maar u moet eerst het groeperen van Computer- en TimeGenerated.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-187">You can display the data in a line chart, but first need to group it by Computer and TimeGenerated.</span></span>  <span data-ttu-id="0f1fd-188">Als u wilt groeperen op meerdere velden, moet u de query rechtstreeks wijzigen, zodat de query met de volgende wijzigen.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-188">To group on multiple fields, you need to modify the query directly, so modify the query to the following.</span></span>  <span data-ttu-id="0f1fd-189">Dit maakt gebruik van de [Gem](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) functioneren in de **tegenwaarde** eigenschap bij de berekening van de gemiddelde waarde voor elk uur.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-189">This uses the [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) function on the **CounterValue** property to calculate the average value over each hour.</span></span>

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated
```

![Prestaties van een grafiek gegevensbron](media/log-analytics-log-search-log-search-portal/log-search-portal-13.png)

<span data-ttu-id="0f1fd-191">Nu dat de gegevens worden naar behoren gegroepeerd, kunt u deze weergeven in een grafiek visual door toe te voegen de [renderen](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator) operator.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-191">Now that the data is suitably grouped, you can display it in a visual chart by adding the [render](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator) operator.</span></span>  

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated | render timechart
```

![Lijndiagram](media/log-analytics-log-search-log-search-portal/log-search-portal-14.png)

## <a name="next-steps"></a><span data-ttu-id="0f1fd-193">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0f1fd-193">Next steps</span></span>

- <span data-ttu-id="0f1fd-194">Meer informatie over de Log Analytics query language op [aan de slag met de Portal Analytics](https://go.microsoft.com/fwlink/?linkid=856079).</span><span class="sxs-lookup"><span data-stu-id="0f1fd-194">Learn more about the Log Analytics query language at [Getting Started with the Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856079).</span></span>
- <span data-ttu-id="0f1fd-195">Een zelfstudie met Doorloop de [Advanced Analytics-portal](https://go.microsoft.com/fwlink/?linkid=856587) waarmee u de dezelfde query's uitvoeren en toegang hebben tot dezelfde gegevens als de portal logboek zoeken.</span><span class="sxs-lookup"><span data-stu-id="0f1fd-195">Walk through a tutorial using the [Advanced Analytics portal](https://go.microsoft.com/fwlink/?linkid=856587) which allows you to run the same queries and access the same data as the Log Search portal.</span></span>
