---
title: Query performance insights voor Azure SQL Database | Microsoft Docs
description: Query-prestaties bewaken, identificeert de meeste CPU verbruikt query's voor een Azure SQL Database.
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: c2f580b2-3835-453f-89f5-140e02dd2ea7
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 1925d4ff8f5b16a0df56de987f8653cfd8441c52
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-sql-database-query-performance-insight"></a><span data-ttu-id="6ecd2-103">Azure SQL Database Query Performance Insight</span><span class="sxs-lookup"><span data-stu-id="6ecd2-103">Azure SQL Database Query Performance Insight</span></span>
<span data-ttu-id="6ecd2-104">Is een uitdaging waarvoor aanzienlijke expertise en investeringen tijd beheren en het afstemmen van de prestaties van relationele databases.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-104">Managing and tuning the performance of relational databases is a challenging task that requires significant expertise and time investment.</span></span> <span data-ttu-id="6ecd2-105">Inzicht in queryprestaties kunt u minder tijd databaseprestaties oplossen door het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="6ecd2-105">Query Performance Insight allows you to spend less time troubleshooting database performance by providing the following:</span></span>

* <span data-ttu-id="6ecd2-106">Dieper inzicht in uw databases brongebruik (DTU).</span><span class="sxs-lookup"><span data-stu-id="6ecd2-106">Deeper insight into your databases resource (DTU) consumption.</span></span> 
* <span data-ttu-id="6ecd2-107">De top-query's op het aantal CPU/duur/uitvoering, die mogelijk voor verbeterde prestaties kunnen worden afgestemd.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-107">The top queries by CPU/Duration/Execution count, which can potentially be tuned for improved performance.</span></span>
* <span data-ttu-id="6ecd2-108">De mogelijkheid om in te zoomen naar de details van een query de tekst en de geschiedenis van Resourcegebruik weergeven.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-108">The ability to drill down into the details of a query, view its text and history of resource utilization.</span></span> 
* <span data-ttu-id="6ecd2-109">Prestaties afstemmen aantekeningen die acties uitgevoerd door weergeven [SQL Azure Database Advisor](sql-database-advisor.md)</span><span class="sxs-lookup"><span data-stu-id="6ecd2-109">Performance tuning annotations that show actions performed by [SQL Azure Database Advisor](sql-database-advisor.md)</span></span>  



## <a name="prerequisites"></a><span data-ttu-id="6ecd2-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6ecd2-110">Prerequisites</span></span>
* <span data-ttu-id="6ecd2-111">Query Performance Insight vereist dat [Query Store](https://msdn.microsoft.com/library/dn817826.aspx) actief is op uw database.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-111">Query Performance Insight requires that [Query Store](https://msdn.microsoft.com/library/dn817826.aspx) is active on your database.</span></span> <span data-ttu-id="6ecd2-112">Als de Query Store niet wordt uitgevoerd, wordt de portal vraagt u te schakelen.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-112">If Query Store is not running, the portal prompts you to turn it on.</span></span>

## <a name="permissions"></a><span data-ttu-id="6ecd2-113">Machtigingen</span><span class="sxs-lookup"><span data-stu-id="6ecd2-113">Permissions</span></span>
<span data-ttu-id="6ecd2-114">De volgende [toegangsbeheer op basis van rollen](../active-directory/role-based-access-control-what-is.md) machtigingen zijn vereist voor Query Performance Insight gebruiken:</span><span class="sxs-lookup"><span data-stu-id="6ecd2-114">The following [role-based access control](../active-directory/role-based-access-control-what-is.md) permissions are required to use Query Performance Insight:</span></span> 

* <span data-ttu-id="6ecd2-115">**Lezer**, **eigenaar**, **Inzender**, **SQL DB Contributor**, of **SQL Server Inzender** machtigingen zijn vereist de bovenste bron verbruikt query's en grafieken weer te geven.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-115">**Reader**, **Owner**, **Contributor**, **SQL DB Contributor**, or **SQL Server Contributor** permissions are required to view the top resource consuming queries and charts.</span></span> 
* <span data-ttu-id="6ecd2-116">**Eigenaar**, **Inzender**, **SQL DB Contributor**, of **SQL Server Inzender** machtigingen zijn vereist om querytekst weer te geven.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-116">**Owner**, **Contributor**, **SQL DB Contributor**, or **SQL Server Contributor** permissions are required to view query text.</span></span>

## <a name="using-query-performance-insight"></a><span data-ttu-id="6ecd2-117">Met behulp van de Query Performance Insight</span><span class="sxs-lookup"><span data-stu-id="6ecd2-117">Using Query Performance Insight</span></span>
<span data-ttu-id="6ecd2-118">Inzicht in queryprestaties is eenvoudig te gebruiken:</span><span class="sxs-lookup"><span data-stu-id="6ecd2-118">Query Performance Insight is easy to use:</span></span>

* <span data-ttu-id="6ecd2-119">Open [Azure-portal](https://portal.azure.com/) en zoeken naar database die u wilt onderzoeken.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-119">Open [Azure portal](https://portal.azure.com/) and find database that you want to examine.</span></span> 
  * <span data-ttu-id="6ecd2-120">Selecteer in de linkerkant menu onder ondersteuning en het oplossen van problemen 'Query Performance Insight'.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-120">From left-hand side menu, under support and troubleshooting, select “Query Performance Insight”.</span></span>
* <span data-ttu-id="6ecd2-121">Bekijk de lijst met de top-resource verbruikende query's op het eerste tabblad.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-121">On the first tab, review the list of top resource-consuming queries.</span></span>
* <span data-ttu-id="6ecd2-122">Selecteer een afzonderlijke query om de details ervan weer te geven.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-122">Select an individual query to view its details.</span></span>
* <span data-ttu-id="6ecd2-123">Open [SQL Azure Database Advisor](sql-database-advisor.md) en controleer of er geen aanbevelingen beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-123">Open [SQL Azure Database Advisor](sql-database-advisor.md) and check if any recommendations are available.</span></span>
* <span data-ttu-id="6ecd2-124">Schuifregelaars gebruiken of zoomen pictogrammen om geobserveerde interval te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-124">Use sliders or zoom icons to change observed interval.</span></span>
  
    ![Prestatiedashboard](./media/sql-database-query-performance/performance.png)

> [!NOTE]
> <span data-ttu-id="6ecd2-126">Een paar uur van gegevens moet worden vastgelegd door het Queryarchief van de SQL Database een inzichten voor queryprestaties.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-126">A couple hours of data needs to be captured by Query Store for SQL Database to provide query performance insights.</span></span> <span data-ttu-id="6ecd2-127">Als de database geen activiteiten heeft of Query Store gedurende een bepaalde periode niet actief was, de grafieken worden leeg om deze periode weer te geven.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-127">If the database has no activity or Query Store was not active during a certain time period, the charts will be empty when displaying that time period.</span></span> <span data-ttu-id="6ecd2-128">U kunt Query Store op elk gewenst moment inschakelen als deze niet wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-128">You may enable Query Store at any time if it is not running.</span></span>   
> 
> 

## <a name="review-top-cpu-consuming-queries"></a><span data-ttu-id="6ecd2-129">Bekijk de hoogste CPU verbruikt query 's</span><span class="sxs-lookup"><span data-stu-id="6ecd2-129">Review top CPU consuming queries</span></span>
<span data-ttu-id="6ecd2-130">In de [portal](http://portal.azure.com) het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="6ecd2-130">In the [portal](http://portal.azure.com) do the following:</span></span>

1. <span data-ttu-id="6ecd2-131">Blader naar een SQL-database en klik op **alle instellingen** > **ondersteuning + probleemoplossing** > **Query performance insight**.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-131">Browse to a SQL database and click **All settings** > **Support + Troubleshooting** > **Query performance insight**.</span></span> 
   
    ![Inzicht in queryprestaties][1]
   
    <span data-ttu-id="6ecd2-133">De weergave van de meest gebruikte query's wordt geopend en de hoogste CPU in beslag neemt query's worden vermeld.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-133">The top queries view opens and the top CPU consuming queries are listed.</span></span>
2. <span data-ttu-id="6ecd2-134">Klik op rond de grafiek voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-134">Click around the chart for details.</span></span><br><span data-ttu-id="6ecd2-135">De bovenste regel bevat algemene DTU % voor de database, terwijl de balken die door de geselecteerde query's worden gebruikt tijdens de geselecteerde interval CPU-percentage weergeven (bijvoorbeeld als **afgelopen week** is geselecteerd elke balk vertegenwoordigt één dag).</span><span class="sxs-lookup"><span data-stu-id="6ecd2-135">The top line shows overall DTU% for the database, while the bars show CPU% consumed by the selected queries during the selected interval (for example, if **Past week** is selected each bar represents one day).</span></span>
   
    ![Top-query 's][2]
   
    <span data-ttu-id="6ecd2-137">Het raster onder vertegenwoordigt verzamelde informatie voor de zichtbare query's.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-137">The bottom grid represents aggregated information for the visible queries.</span></span>
   
   * <span data-ttu-id="6ecd2-138">Query-ID - de unieke id van de query in de database.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-138">Query ID - unique identifier of query inside database.</span></span>
   * <span data-ttu-id="6ecd2-139">CPU per query tijdens waarneembare interval (afhankelijk van statistische functie).</span><span class="sxs-lookup"><span data-stu-id="6ecd2-139">CPU per query during observable interval (depends on aggregation function).</span></span>
   * <span data-ttu-id="6ecd2-140">Duur per query (afhankelijk van statistische functie).</span><span class="sxs-lookup"><span data-stu-id="6ecd2-140">Duration per query (depends on aggregation function).</span></span>
   * <span data-ttu-id="6ecd2-141">Totaal aantal uitvoeringen voor een bepaalde query.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-141">Total number of executions for a particular query.</span></span>
     
     <span data-ttu-id="6ecd2-142">Schakel of afzonderlijke query's wilt opnemen of uitsluiten van de grafiek met behulp van de selectievakjes uit.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-142">Select or clear individual queries to include or exclude them from the chart using checkboxes.</span></span>
3. <span data-ttu-id="6ecd2-143">Als uw gegevens verlopen is, klikt u op de **vernieuwen** knop.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-143">If your data becomes stale, click the **Refresh** button.</span></span>
4. <span data-ttu-id="6ecd2-144">U kunt gebruiken schuifregelaars en knoppen observatie-interval wijzigen en onderzoeken pieken inzoomen en uitzoomen: ![instellingen](./media/sql-database-query-performance/zoom.png)</span><span class="sxs-lookup"><span data-stu-id="6ecd2-144">You can use sliders and zoom buttons to change observation interval and investigate spikes:  ![settings](./media/sql-database-query-performance/zoom.png)</span></span>
5. <span data-ttu-id="6ecd2-145">Als u een andere weergave wilt, u kunt eventueel selecteren **aangepaste** tabblad en ingesteld:</span><span class="sxs-lookup"><span data-stu-id="6ecd2-145">Optionally, if you want a different view, you can select **Custom** tab and set:</span></span>
   
   * <span data-ttu-id="6ecd2-146">Metrische gegevens (CPU, duur, het aantal keer uitgevoerd)</span><span class="sxs-lookup"><span data-stu-id="6ecd2-146">Metric (CPU, duration, execution count)</span></span>
   * <span data-ttu-id="6ecd2-147">Tijdsinterval (afgelopen week afgelopen maand afgelopen 24 uur).</span><span class="sxs-lookup"><span data-stu-id="6ecd2-147">Time interval (Last 24 hours, Past week, Past month).</span></span> 
   * <span data-ttu-id="6ecd2-148">Aantal query's.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-148">Number of queries.</span></span>
   * <span data-ttu-id="6ecd2-149">Statistische functie.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-149">Aggregation function.</span></span>
     
     ![instellingen](./media/sql-database-query-performance/custom-tab.png)

## <a name="viewing-individual-query-details"></a><span data-ttu-id="6ecd2-151">Details van de afzonderlijke query's weergeven</span><span class="sxs-lookup"><span data-stu-id="6ecd2-151">Viewing individual query details</span></span>
<span data-ttu-id="6ecd2-152">Om Querydetails te bekijken:</span><span class="sxs-lookup"><span data-stu-id="6ecd2-152">To view query details:</span></span>

1. <span data-ttu-id="6ecd2-153">Klik op een query in de lijst met de meest gebruikte query's.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-153">Click any query in the list of top queries.</span></span>
   
    ![Meer informatie](./media/sql-database-query-performance/details.png)
2. <span data-ttu-id="6ecd2-155">De detailweergave wordt geopend en het aantal query's CPU-verbruik/duur/uitvoering is onderverdeeld gedurende een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-155">The details view opens and the queries CPU consumption/Duration/Execution count is broken down over time.</span></span>
3. <span data-ttu-id="6ecd2-156">Klik op rond de grafiek voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-156">Click around the chart for details.</span></span>
   
   * <span data-ttu-id="6ecd2-157">Bovenste diagram toont de regel met algemene database DTU % en de balken zijn CPU-percentage gebruikt door de geselecteerde query.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-157">Top chart shows line with overall database DTU%, and the bars are CPU% consumed by the selected query.</span></span>
   * <span data-ttu-id="6ecd2-158">Tweede diagram toont de totale duur door de geselecteerde query.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-158">Second chart shows total duration by the selected query.</span></span>
   * <span data-ttu-id="6ecd2-159">Onder diagram toont het aantal uitvoeringen door de geselecteerde query.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-159">Bottom chart shows total number of executions by the selected query.</span></span>
     
     ![Querydetails][3]
4. <span data-ttu-id="6ecd2-161">Optioneel gebruik schuifregelaars, knoppen Inzoomen en uitzoomen of klik op **instellingen** aanpassen hoe querygegevens worden weergegeven, of kies een andere periode.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-161">Optionally, use sliders, zoom buttons or click **Settings** to customize how query data is displayed, or to pick a different time period.</span></span>

## <a name="review-top-queries-per-duration"></a><span data-ttu-id="6ecd2-162">Bekijk meest gebruikte query's per duur</span><span class="sxs-lookup"><span data-stu-id="6ecd2-162">Review top queries per duration</span></span>
<span data-ttu-id="6ecd2-163">In de recente update van de Query Performance Insight, er zijn twee nieuwe metrische gegevens kunt u potentiële knelpunten geïntroduceerd: aantal duur en uitvoering.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-163">In the recent update of Query Performance Insight, we introduced two new metrics that can help you identify potential bottlenecks: duration and execution count.</span></span><br>

<span data-ttu-id="6ecd2-164">Langlopende query's hebben de grootste kans dat langer resources vergrendelen, andere gebruikers worden geblokkeerd en schaalbaarheid te beperken.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-164">Long-running queries have the greatest potential for locking resources longer, blocking other users, and limiting scalability.</span></span> <span data-ttu-id="6ecd2-165">Ze zijn ook het meest in aanmerking voor optimalisatie.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-165">They are also the best candidates for optimization.</span></span><br>

<span data-ttu-id="6ecd2-166">Langdurige query's identificeren:</span><span class="sxs-lookup"><span data-stu-id="6ecd2-166">To identify long running queries:</span></span>

1. <span data-ttu-id="6ecd2-167">Open **aangepaste** tabblad in de Query Performance Insight voor de geselecteerde database</span><span class="sxs-lookup"><span data-stu-id="6ecd2-167">Open **Custom** tab in Query Performance Insight for selected database</span></span>
2. <span data-ttu-id="6ecd2-168">Metrische gegevens moet wijzigen **duur**</span><span class="sxs-lookup"><span data-stu-id="6ecd2-168">Change metrics to be **duration**</span></span>
3. <span data-ttu-id="6ecd2-169">Selecteer het aantal query's en observatie-interval</span><span class="sxs-lookup"><span data-stu-id="6ecd2-169">Select number of queries and observation interval</span></span>
4. <span data-ttu-id="6ecd2-170">Selecteer de statistische functie</span><span class="sxs-lookup"><span data-stu-id="6ecd2-170">Select aggregation function</span></span>
   
   * <span data-ttu-id="6ecd2-171">**Som** tijdens de gehele observatie-interval is de som van alle uitvoeringstijd van de query.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-171">**Sum** adds up all query execution time during whole observation interval.</span></span>
   * <span data-ttu-id="6ecd2-172">**Maximale** vindt u query's welke uitvoeringstijd maximale was op de hele observatie-interval.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-172">**Max** finds queries which execution time was maximum at whole observation interval.</span></span>
   * <span data-ttu-id="6ecd2-173">**Gem.** gezocht gemiddelde uitvoeringstijd van alle query uitvoeringen en ziet u boven buiten deze gemiddelden.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-173">**Avg** finds average execution time of all query executions and show you the top out of these averages.</span></span> 
     
     ![duur van de query][4]

## <a name="review-top-queries-per-execution-count"></a><span data-ttu-id="6ecd2-175">Bekijk meest gebruikte query's per aantal keer uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="6ecd2-175">Review top queries per execution count</span></span>
<span data-ttu-id="6ecd2-176">Hoog aantal uitvoeringen mogelijk niet beïnvloeden database zelf en gebruik van bronnen kan lage, maar algemene toepassing, haalt traag.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-176">High number of executions might not be affecting database itself and resources usage can be low, but overall application might get slow.</span></span>

<span data-ttu-id="6ecd2-177">In sommige gevallen zeer hoge uitvoering count kan leiden tot het vergroten van retouren netwerk.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-177">In some cases, very high execution count may lead to increase of network round trips.</span></span> <span data-ttu-id="6ecd2-178">Retouren aanzienlijk beïnvloeden.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-178">Round trips significantly affect performance.</span></span> <span data-ttu-id="6ecd2-179">Ze zijn onderworpen aan netwerklatentie en de latentie downstream-server.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-179">They are subject to network latency and to downstream server latency.</span></span> 

<span data-ttu-id="6ecd2-180">Bijvoorbeeld: veel gegevensgestuurde websites sterk toegang krijgen tot de database voor elke aanvraag van gebruiker.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-180">For example, many data-driven Web sites heavily access the database for every user request.</span></span> <span data-ttu-id="6ecd2-181">Tijdens het verbinding helpt, het toegenomen verkeer groeperen en verwerken van de belasting van de database-server kan de prestaties nadelig beïnvloeden.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-181">While connection pooling helps, the increased network traffic and processing load on the database server can adversely affect performance.</span></span>  <span data-ttu-id="6ecd2-182">Algemeen advies is om retouren tot een absoluut minimum te beperken.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-182">General advice is to keep round trips to an absolute minimum.</span></span>

<span data-ttu-id="6ecd2-183">Uitgevoerd om te identificeren vaak query's ('chatty') query's:</span><span class="sxs-lookup"><span data-stu-id="6ecd2-183">To identify frequently executed queries (“chatty”) queries:</span></span>

1. <span data-ttu-id="6ecd2-184">Open **aangepaste** tabblad in de Query Performance Insight voor de geselecteerde database</span><span class="sxs-lookup"><span data-stu-id="6ecd2-184">Open **Custom** tab in Query Performance Insight for selected database</span></span>
2. <span data-ttu-id="6ecd2-185">Metrische gegevens moet wijzigen **aantal keer uitgevoerd**</span><span class="sxs-lookup"><span data-stu-id="6ecd2-185">Change metrics to be **execution count**</span></span>
3. <span data-ttu-id="6ecd2-186">Selecteer het aantal query's en observatie-interval</span><span class="sxs-lookup"><span data-stu-id="6ecd2-186">Select number of queries and observation interval</span></span>
   
    ![uitvoering van het aantal query 's][5]

## <a name="understanding-performance-tuning-annotations"></a><span data-ttu-id="6ecd2-188">Inzicht in prestaties afstemmen aantekeningen</span><span class="sxs-lookup"><span data-stu-id="6ecd2-188">Understanding performance tuning annotations</span></span>
<span data-ttu-id="6ecd2-189">Tijdens het verkennen van de werkbelasting in Query Performance Insight, ziet u mogelijk pictogrammen met verticale lijn boven op de grafiek.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-189">While exploring your workload in Query Performance Insight, you might notice icons with vertical line on top of the chart.</span></span><br>

<span data-ttu-id="6ecd2-190">Deze pictogrammen zijn aantekeningen; ze hebben betrekking op prestaties beïnvloeden bewerkingen worden uitgevoerd door [SQL Azure Database Advisor](sql-database-advisor.md).</span><span class="sxs-lookup"><span data-stu-id="6ecd2-190">These icons are annotations; they represent performance affecting actions performed by [SQL Azure Database Advisor](sql-database-advisor.md).</span></span> <span data-ttu-id="6ecd2-191">Door zwevende aantekening krijgen u algemene informatie over de actie:</span><span class="sxs-lookup"><span data-stu-id="6ecd2-191">By hovering annotation, you get basic information about the action:</span></span>

![query aantekening][6]

<span data-ttu-id="6ecd2-193">Als u wilt meer weten of de aanbeveling advisor toepassen, klikt u op het pictogram.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-193">If you want to know more or apply advisor recommendation, click the icon.</span></span> <span data-ttu-id="6ecd2-194">Details van de actie wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-194">It will open details of action.</span></span> <span data-ttu-id="6ecd2-195">Als een actieve bevelen kunt u meteen met behulp van opdracht toepassen.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-195">If it’s an active recommendation you can apply it straight away using command.</span></span>

![details van de aantekening query][7]

### <a name="multiple-annotations"></a><span data-ttu-id="6ecd2-197">Meerdere aantekeningen.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-197">Multiple annotations.</span></span>
<span data-ttu-id="6ecd2-198">Het is mogelijk dat vanwege zoomniveau, aantekeningen die zich dicht bij elkaar ophalen tot één samengevouwen zullen.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-198">It’s possible, that because of zoom level, annotations that are close to each other will get collapsed into one.</span></span> <span data-ttu-id="6ecd2-199">Hiermee wordt aangegeven door speciale pictogram, erop te klikken wordt geopend nieuwe blade waarin de lijst met aantekeningen gegroepeerd worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-199">This will be represented by special icon, clicking it will open new blade where list of grouped annotations will be shown.</span></span>
<span data-ttu-id="6ecd2-200">Correleren van query's en -prestaties afstemmen acties kan helpen om uw werkbelasting beter te begrijpen.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-200">Correlating queries and performance tuning actions can help to better understand your workload.</span></span> 

## <a name="optimizing-the-query-store-configuration-for-query-performance-insight"></a><span data-ttu-id="6ecd2-201">De Query Store-configuratie voor Query Performance Insight optimaliseren</span><span class="sxs-lookup"><span data-stu-id="6ecd2-201">Optimizing the Query Store configuration for Query Performance Insight</span></span>
<span data-ttu-id="6ecd2-202">U kunt de volgende Query Store-berichten tegenkomen tijdens het gebruik van de Query Performance Insight:</span><span class="sxs-lookup"><span data-stu-id="6ecd2-202">During your use of Query Performance Insight, you might encounter the following Query Store messages:</span></span>

* <span data-ttu-id="6ecd2-203">'Query Store is niet goed geconfigureerd op deze database.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-203">"Query Store is not properly configured on this database.</span></span> <span data-ttu-id="6ecd2-204">Klik hier voor meer informatie."</span><span class="sxs-lookup"><span data-stu-id="6ecd2-204">Click here to learn more."</span></span>
* <span data-ttu-id="6ecd2-205">'Query Store is niet goed geconfigureerd op deze database.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-205">"Query Store is not properly configured on this database.</span></span> <span data-ttu-id="6ecd2-206">Klik hier om instellingen te wijzigen."</span><span class="sxs-lookup"><span data-stu-id="6ecd2-206">Click here to change settings."</span></span> 

<span data-ttu-id="6ecd2-207">Deze berichten worden doorgaans weergegeven wanneer het Queryarchief kan geen nieuwe gegevens verzamelen.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-207">These messages usually appear when Query Store is not able to collect new data.</span></span> 

<span data-ttu-id="6ecd2-208">Eerste geval gebeurt wanneer Query Store in alleen-lezen status en parameters optimaal zijn ingesteld.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-208">First case happens when Query Store is in Read-Only state and parameters are set optimally.</span></span> <span data-ttu-id="6ecd2-209">U kunt dit oplossen door het vergroten van de Query Store of Query Store uit te schakelen.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-209">You can fix this by increasing size of Query Store or clearing Query Store.</span></span>

![knop qds][8]

<span data-ttu-id="6ecd2-211">Tweede geval gebeurt wanneer de Query Store is uitgeschakeld of de parameters zijn niet optimaal ingesteld.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-211">Second case happens when Query Store is Off or parameters aren’t set optimally.</span></span> <br><span data-ttu-id="6ecd2-212">U kunt het beleid bewaren en vastleggen wijzigen en Query Store inschakelen door het uitvoeren van de onderstaande opdrachten of rechtstreeks vanuit de portal:</span><span class="sxs-lookup"><span data-stu-id="6ecd2-212">You can change the Retention and Capture policy and enable Query Store by executing commands below or directly from portal:</span></span>

![knop qds][9]

### <a name="recommended-retention-and-capture-policy"></a><span data-ttu-id="6ecd2-214">Aanbevolen bewaren en vastleggen beleid</span><span class="sxs-lookup"><span data-stu-id="6ecd2-214">Recommended retention and capture policy</span></span>
<span data-ttu-id="6ecd2-215">Er zijn twee soorten bewaarbeleidsregels:</span><span class="sxs-lookup"><span data-stu-id="6ecd2-215">There are two types of retention policies:</span></span>

* <span data-ttu-id="6ecd2-216">Op de basis - grootte als ingesteld op AUTO deze worden schoongemaakt gegevens automatisch wanneer bijna de maximale grootte is bereikt.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-216">Size based - if set to AUTO it will clean data automatically when near max size is reached.</span></span>
* <span data-ttu-id="6ecd2-217">Op basis van tijd - standaard die we deze wordt ingesteld op 30 dagen, wat betekent dat, als de Query Store is geen ruimte meer wordt uitgevoerd, querygegevens ouder dan 30 dagen wordt verwijderd</span><span class="sxs-lookup"><span data-stu-id="6ecd2-217">Time based - by default we will set it to 30 days, which means, if Query Store will run out of space, it will delete query information older than 30 days</span></span>

<span data-ttu-id="6ecd2-218">Vastleggen van beleid kan worden ingesteld op:</span><span class="sxs-lookup"><span data-stu-id="6ecd2-218">Capture policy could be set to:</span></span>

* <span data-ttu-id="6ecd2-219">**Alle** -alle query's worden vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-219">**All** - Captures all queries.</span></span>
* <span data-ttu-id="6ecd2-220">**Automatische** -incidentele's en query's met verwaarlozen compileren en uitvoering duur worden genegeerd.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-220">**Auto** - Infrequent queries and queries with insignificant compile and execution duration are ignored.</span></span> <span data-ttu-id="6ecd2-221">Drempelwaarden voor de duur voor het aantal, compileren en runtime uitvoeren worden intern bepaald.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-221">Thresholds for execution count, compile and runtime duration are internally determined.</span></span> <span data-ttu-id="6ecd2-222">Dit is de standaardoptie.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-222">This is the default option.</span></span>
* <span data-ttu-id="6ecd2-223">**Geen** -Query Store stopt u het vastleggen nieuwe query's, maar de runtime-statistieken voor al vastgelegde query's worden nog steeds verzameld.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-223">**None** - Query Store stops capturing new queries, however runtime stats for already captured queries are still collected.</span></span>

<span data-ttu-id="6ecd2-224">U wordt aangeraden alle beleidsregels instellen op automatisch en schone beleid tot 30 dagen:</span><span class="sxs-lookup"><span data-stu-id="6ecd2-224">We recommend setting all policies to AUTO and clean policy to 30 days:</span></span>

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (SIZE_BASED_CLEANUP_MODE = AUTO);

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 30));

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (QUERY_CAPTURE_MODE = AUTO);

<span data-ttu-id="6ecd2-225">Verhoog de grootte van de Query Store.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-225">Increase size of Query Store.</span></span> <span data-ttu-id="6ecd2-226">Dit kan worden uitgevoerd door verbinding te maken met een database en het uitgeven van volgende query:</span><span class="sxs-lookup"><span data-stu-id="6ecd2-226">This could be performed by connecting to a database and issuing following query:</span></span>

    ALTER DATABASE [YourDB]
    SET QUERY_STORE (MAX_STORAGE_SIZE_MB = 1024);

<span data-ttu-id="6ecd2-227">Deze instellingen zijn toegepast brengt uiteindelijk Query Store verzamelen van de nieuwe query's, maar als u niet wilt wachten voordat u Query Store kunt wissen.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-227">Applying these settings will eventually make Query Store collecting new queries, however if you don’t want to wait you can clear Query Store.</span></span> 

> [!NOTE]
> <span data-ttu-id="6ecd2-228">Uitvoeren van de volgende query worden alle huidige gegevens in het Queryarchief verwijderd.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-228">Executing following query will delete all current information in the Query Store.</span></span> 
> 
> 

    ALTER DATABASE [YourDB] SET QUERY_STORE CLEAR;


## <a name="summary"></a><span data-ttu-id="6ecd2-229">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="6ecd2-229">Summary</span></span>
<span data-ttu-id="6ecd2-230">Inzicht in queryprestaties vindt u informatie over het effect van uw workload van query's en hoe deze zich verhoudt tot brongebruik van de database.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-230">Query Performance Insight helps you understand the impact of your query workload and how it relates to database resource consumption.</span></span> <span data-ttu-id="6ecd2-231">Met deze functie wordt u meer informatie over het grootste verbruik van query's en gemakkelijk herkennen die om op te lossen voordat ze een probleem.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-231">With this feature, you will learn about the top consuming queries, and easily identify the ones to fix before they become a problem.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ecd2-232">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6ecd2-232">Next steps</span></span>
<span data-ttu-id="6ecd2-233">Extra aanbevelingen over het verbeteren van de prestaties van uw SQL-database, klikt u op [aanbevelingen](sql-database-advisor.md) op de **Query Performance Insight** blade.</span><span class="sxs-lookup"><span data-stu-id="6ecd2-233">For additional recommendations about improving the performance of your SQL database, click [Recommendations](sql-database-advisor.md) on the **Query Performance Insight** blade.</span></span>

![Performance Advisor](./media/sql-database-query-performance/ia.png)

<!--Image references-->
[1]: ./media/sql-database-query-performance/tile.png
[2]: ./media/sql-database-query-performance/top-queries.png
[3]: ./media/sql-database-query-performance/query-details.png
[4]: ./media/sql-database-query-performance/top-duration.png
[5]: ./media/sql-database-query-performance/top-execution.png
[6]: ./media/sql-database-query-performance/annotation.png
[7]: ./media/sql-database-query-performance/annotation-details.png
[8]: ./media/sql-database-query-performance/qds-off.png
[9]: ./media/sql-database-query-performance/qds-button.png

