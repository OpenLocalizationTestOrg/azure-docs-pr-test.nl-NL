---
title: aaaQuery inzichten voor Azure SQL Database | Microsoft Docs
description: Query-prestaties controleren identificeert Hallo meeste CPU-verbruik wordt gevraagd om een Azure SQL Database.
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
ms.openlocfilehash: 01cca26f85193c679365585cd676449c9db00e1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-query-performance-insight"></a><span data-ttu-id="db3e7-103">Azure SQL Database Query Performance Insight</span><span class="sxs-lookup"><span data-stu-id="db3e7-103">Azure SQL Database Query Performance Insight</span></span>
<span data-ttu-id="db3e7-104">Is een uitdaging waarvoor aanzienlijke expertise en investeringen tijd beheren en optimaliseren van Hallo van relationele databases.</span><span class="sxs-lookup"><span data-stu-id="db3e7-104">Managing and tuning hello performance of relational databases is a challenging task that requires significant expertise and time investment.</span></span> <span data-ttu-id="db3e7-105">Inzicht in queryprestaties kunt u toospend minder tijd databaseprestaties oplossen door de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="db3e7-105">Query Performance Insight allows you toospend less time troubleshooting database performance by providing hello following:</span></span>

* <span data-ttu-id="db3e7-106">Dieper inzicht in uw databases brongebruik (DTU).</span><span class="sxs-lookup"><span data-stu-id="db3e7-106">Deeper insight into your databases resource (DTU) consumption.</span></span> 
* <span data-ttu-id="db3e7-107">Hallo top-query's op het aantal CPU/duur/uitvoering, die mogelijk voor verbeterde prestaties kunnen worden afgestemd.</span><span class="sxs-lookup"><span data-stu-id="db3e7-107">hello top queries by CPU/Duration/Execution count, which can potentially be tuned for improved performance.</span></span>
* <span data-ttu-id="db3e7-108">Hallo mogelijkheid toodrill omlaag op Hallo gegevens van een query, geven de tekst en de geschiedenis van bronnen beter worden benut.</span><span class="sxs-lookup"><span data-stu-id="db3e7-108">hello ability toodrill down into hello details of a query, view its text and history of resource utilization.</span></span> 
* <span data-ttu-id="db3e7-109">Prestaties afstemmen aantekeningen die acties uitgevoerd door weergeven [SQL Azure Database Advisor](sql-database-advisor.md)</span><span class="sxs-lookup"><span data-stu-id="db3e7-109">Performance tuning annotations that show actions performed by [SQL Azure Database Advisor](sql-database-advisor.md)</span></span>  



## <a name="prerequisites"></a><span data-ttu-id="db3e7-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="db3e7-110">Prerequisites</span></span>
* <span data-ttu-id="db3e7-111">Query Performance Insight vereist dat [Query Store](https://msdn.microsoft.com/library/dn817826.aspx) actief is op uw database.</span><span class="sxs-lookup"><span data-stu-id="db3e7-111">Query Performance Insight requires that [Query Store](https://msdn.microsoft.com/library/dn817826.aspx) is active on your database.</span></span> <span data-ttu-id="db3e7-112">Als de Query Store niet wordt uitgevoerd, Hallo portal wordt u gevraagd tooturn op.</span><span class="sxs-lookup"><span data-stu-id="db3e7-112">If Query Store is not running, hello portal prompts you tooturn it on.</span></span>

## <a name="permissions"></a><span data-ttu-id="db3e7-113">Machtigingen</span><span class="sxs-lookup"><span data-stu-id="db3e7-113">Permissions</span></span>
<span data-ttu-id="db3e7-114">Hallo volgende [toegangsbeheer op basis van rollen](../active-directory/role-based-access-control-what-is.md) machtigingen zijn vereist toouse Query Performance Insight:</span><span class="sxs-lookup"><span data-stu-id="db3e7-114">hello following [role-based access control](../active-directory/role-based-access-control-what-is.md) permissions are required toouse Query Performance Insight:</span></span> 

* <span data-ttu-id="db3e7-115">**Lezer**, **eigenaar**, **Inzender**, **SQL DB Contributor**, of **SQL Server Inzender** machtigingen zijn vereist tooview Hallo bovenste resource verbruikt query's en -grafieken.</span><span class="sxs-lookup"><span data-stu-id="db3e7-115">**Reader**, **Owner**, **Contributor**, **SQL DB Contributor**, or **SQL Server Contributor** permissions are required tooview hello top resource consuming queries and charts.</span></span> 
* <span data-ttu-id="db3e7-116">**Eigenaar**, **Inzender**, **SQL DB Contributor**, of **SQL Server Inzender** machtigingen zijn vereist tooview querytekst.</span><span class="sxs-lookup"><span data-stu-id="db3e7-116">**Owner**, **Contributor**, **SQL DB Contributor**, or **SQL Server Contributor** permissions are required tooview query text.</span></span>

## <a name="using-query-performance-insight"></a><span data-ttu-id="db3e7-117">Met behulp van de Query Performance Insight</span><span class="sxs-lookup"><span data-stu-id="db3e7-117">Using Query Performance Insight</span></span>
<span data-ttu-id="db3e7-118">Inzicht in queryprestaties is eenvoudig toouse:</span><span class="sxs-lookup"><span data-stu-id="db3e7-118">Query Performance Insight is easy toouse:</span></span>

* <span data-ttu-id="db3e7-119">Open [Azure-portal](https://portal.azure.com/) en zoeken naar database die u tooexamine wilt.</span><span class="sxs-lookup"><span data-stu-id="db3e7-119">Open [Azure portal](https://portal.azure.com/) and find database that you want tooexamine.</span></span> 
  * <span data-ttu-id="db3e7-120">Selecteer in de linkerkant menu onder ondersteuning en het oplossen van problemen 'Query Performance Insight'.</span><span class="sxs-lookup"><span data-stu-id="db3e7-120">From left-hand side menu, under support and troubleshooting, select “Query Performance Insight”.</span></span>
* <span data-ttu-id="db3e7-121">Op het eerste tabblad Hallo, bekijk Hallo-lijst van bovenste resource verbruikende query's.</span><span class="sxs-lookup"><span data-stu-id="db3e7-121">On hello first tab, review hello list of top resource-consuming queries.</span></span>
* <span data-ttu-id="db3e7-122">Selecteer een afzonderlijke query tooview de details ervan.</span><span class="sxs-lookup"><span data-stu-id="db3e7-122">Select an individual query tooview its details.</span></span>
* <span data-ttu-id="db3e7-123">Open [SQL Azure Database Advisor](sql-database-advisor.md) en controleer of er geen aanbevelingen beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="db3e7-123">Open [SQL Azure Database Advisor](sql-database-advisor.md) and check if any recommendations are available.</span></span>
* <span data-ttu-id="db3e7-124">Schuifregelaars gebruiken of zoomen pictogrammen toochange waargenomen-interval.</span><span class="sxs-lookup"><span data-stu-id="db3e7-124">Use sliders or zoom icons toochange observed interval.</span></span>
  
    ![Prestatiedashboard](./media/sql-database-query-performance/performance.png)

> [!NOTE]
> <span data-ttu-id="db3e7-126">Een paar uur van gegevens moet toobe voor SQL-Database tooprovide query performance insights wordt vastgelegd door de Query Store.</span><span class="sxs-lookup"><span data-stu-id="db3e7-126">A couple hours of data needs toobe captured by Query Store for SQL Database tooprovide query performance insights.</span></span> <span data-ttu-id="db3e7-127">Als Hallo-database geen activiteiten heeft of Query Store gedurende een bepaalde periode niet actief was, is Hallo grafieken leeg om deze periode weer te geven.</span><span class="sxs-lookup"><span data-stu-id="db3e7-127">If hello database has no activity or Query Store was not active during a certain time period, hello charts will be empty when displaying that time period.</span></span> <span data-ttu-id="db3e7-128">U kunt Query Store op elk gewenst moment inschakelen als deze niet wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="db3e7-128">You may enable Query Store at any time if it is not running.</span></span>   
> 
> 

## <a name="review-top-cpu-consuming-queries"></a><span data-ttu-id="db3e7-129">Bekijk de hoogste CPU verbruikt query 's</span><span class="sxs-lookup"><span data-stu-id="db3e7-129">Review top CPU consuming queries</span></span>
<span data-ttu-id="db3e7-130">In Hallo [portal](http://portal.azure.com) Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="db3e7-130">In hello [portal](http://portal.azure.com) do hello following:</span></span>

1. <span data-ttu-id="db3e7-131">Blader tooa SQL-database en klik op **alle instellingen** > **ondersteuning + probleemoplossing** > **Query performance insight**.</span><span class="sxs-lookup"><span data-stu-id="db3e7-131">Browse tooa SQL database and click **All settings** > **Support + Troubleshooting** > **Query performance insight**.</span></span> 
   
    ![Inzicht in queryprestaties][1]
   
    <span data-ttu-id="db3e7-133">Hallo top-query's weergeven wordt geopend en Hallo top CPU in beslag neemt-query's worden vermeld.</span><span class="sxs-lookup"><span data-stu-id="db3e7-133">hello top queries view opens and hello top CPU consuming queries are listed.</span></span>
2. <span data-ttu-id="db3e7-134">Klik op rond Hallo-grafiek voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="db3e7-134">Click around hello chart for details.</span></span><br><span data-ttu-id="db3e7-135">Hallo bovenlijn worden algemene DTU % voor Hallo-database, terwijl Hallo balken CPU-percentage verbruikt door query's Hallo geselecteerd tijdens de geselecteerde hello-interval weergeven (bijvoorbeeld als **afgelopen week** is geselecteerd elke balk vertegenwoordigt één dag).</span><span class="sxs-lookup"><span data-stu-id="db3e7-135">hello top line shows overall DTU% for hello database, while hello bars show CPU% consumed by hello selected queries during hello selected interval (for example, if **Past week** is selected each bar represents one day).</span></span>
   
    ![Top-query 's][2]
   
    <span data-ttu-id="db3e7-137">Hallo onder raster vertegenwoordigt de verzamelde informatie voor Hallo zichtbaar query's.</span><span class="sxs-lookup"><span data-stu-id="db3e7-137">hello bottom grid represents aggregated information for hello visible queries.</span></span>
   
   * <span data-ttu-id="db3e7-138">Query-ID - de unieke id van de query in de database.</span><span class="sxs-lookup"><span data-stu-id="db3e7-138">Query ID - unique identifier of query inside database.</span></span>
   * <span data-ttu-id="db3e7-139">CPU per query tijdens waarneembare interval (afhankelijk van statistische functie).</span><span class="sxs-lookup"><span data-stu-id="db3e7-139">CPU per query during observable interval (depends on aggregation function).</span></span>
   * <span data-ttu-id="db3e7-140">Duur per query (afhankelijk van statistische functie).</span><span class="sxs-lookup"><span data-stu-id="db3e7-140">Duration per query (depends on aggregation function).</span></span>
   * <span data-ttu-id="db3e7-141">Totaal aantal uitvoeringen voor een bepaalde query.</span><span class="sxs-lookup"><span data-stu-id="db3e7-141">Total number of executions for a particular query.</span></span>
     
     <span data-ttu-id="db3e7-142">Selecteren of wissen tooinclude afzonderlijke query's of uitsluiten Hallo grafiek met behulp van de selectievakjes uit.</span><span class="sxs-lookup"><span data-stu-id="db3e7-142">Select or clear individual queries tooinclude or exclude them from hello chart using checkboxes.</span></span>
3. <span data-ttu-id="db3e7-143">Als uw gegevens verlopen is, klikt u op Hallo **vernieuwen** knop.</span><span class="sxs-lookup"><span data-stu-id="db3e7-143">If your data becomes stale, click hello **Refresh** button.</span></span>
4. <span data-ttu-id="db3e7-144">U kunt gebruiken schuifregelaars en zoomen knoppen toochange observatie-interval en onderzoeken pieken: ![instellingen](./media/sql-database-query-performance/zoom.png)</span><span class="sxs-lookup"><span data-stu-id="db3e7-144">You can use sliders and zoom buttons toochange observation interval and investigate spikes:  ![settings](./media/sql-database-query-performance/zoom.png)</span></span>
5. <span data-ttu-id="db3e7-145">Als u een andere weergave wilt, u kunt eventueel selecteren **aangepaste** tabblad en ingesteld:</span><span class="sxs-lookup"><span data-stu-id="db3e7-145">Optionally, if you want a different view, you can select **Custom** tab and set:</span></span>
   
   * <span data-ttu-id="db3e7-146">Metrische gegevens (CPU, duur, het aantal keer uitgevoerd)</span><span class="sxs-lookup"><span data-stu-id="db3e7-146">Metric (CPU, duration, execution count)</span></span>
   * <span data-ttu-id="db3e7-147">Tijdsinterval (afgelopen week afgelopen maand afgelopen 24 uur).</span><span class="sxs-lookup"><span data-stu-id="db3e7-147">Time interval (Last 24 hours, Past week, Past month).</span></span> 
   * <span data-ttu-id="db3e7-148">Aantal query's.</span><span class="sxs-lookup"><span data-stu-id="db3e7-148">Number of queries.</span></span>
   * <span data-ttu-id="db3e7-149">Statistische functie.</span><span class="sxs-lookup"><span data-stu-id="db3e7-149">Aggregation function.</span></span>
     
     ![instellingen](./media/sql-database-query-performance/custom-tab.png)

## <a name="viewing-individual-query-details"></a><span data-ttu-id="db3e7-151">Details van de afzonderlijke query's weergeven</span><span class="sxs-lookup"><span data-stu-id="db3e7-151">Viewing individual query details</span></span>
<span data-ttu-id="db3e7-152">details van de query tooview:</span><span class="sxs-lookup"><span data-stu-id="db3e7-152">tooview query details:</span></span>

1. <span data-ttu-id="db3e7-153">Klik op een query in de lijst Hallo van top-query's.</span><span class="sxs-lookup"><span data-stu-id="db3e7-153">Click any query in hello list of top queries.</span></span>
   
    ![Meer informatie](./media/sql-database-query-performance/details.png)
2. <span data-ttu-id="db3e7-155">Hallo detailweergave wordt geopend en aantal Hallo query's CPU-verbruik/duur/uitvoering is onderverdeeld gedurende een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="db3e7-155">hello details view opens and hello queries CPU consumption/Duration/Execution count is broken down over time.</span></span>
3. <span data-ttu-id="db3e7-156">Klik op rond Hallo-grafiek voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="db3e7-156">Click around hello chart for details.</span></span>
   
   * <span data-ttu-id="db3e7-157">Bovenste diagram toont de regel met algemene database DTU % en Hallo balken zijn CPU-percentage verbruikt door Hallo geselecteerde query.</span><span class="sxs-lookup"><span data-stu-id="db3e7-157">Top chart shows line with overall database DTU%, and hello bars are CPU% consumed by hello selected query.</span></span>
   * <span data-ttu-id="db3e7-158">Tweede diagram toont de totale duur door Hallo geselecteerde query.</span><span class="sxs-lookup"><span data-stu-id="db3e7-158">Second chart shows total duration by hello selected query.</span></span>
   * <span data-ttu-id="db3e7-159">Onder diagram toont het aantal uitvoeringen door de geselecteerde query Hallo.</span><span class="sxs-lookup"><span data-stu-id="db3e7-159">Bottom chart shows total number of executions by hello selected query.</span></span>
     
     ![Querydetails][3]
4. <span data-ttu-id="db3e7-161">Optioneel gebruik schuifregelaars, knoppen Inzoomen en uitzoomen of klik op **instellingen** toocustomize hoe querygegevens worden weergegeven of een andere periode toopick.</span><span class="sxs-lookup"><span data-stu-id="db3e7-161">Optionally, use sliders, zoom buttons or click **Settings** toocustomize how query data is displayed, or toopick a different time period.</span></span>

## <a name="review-top-queries-per-duration"></a><span data-ttu-id="db3e7-162">Bekijk meest gebruikte query's per duur</span><span class="sxs-lookup"><span data-stu-id="db3e7-162">Review top queries per duration</span></span>
<span data-ttu-id="db3e7-163">In Hallo recente update van inzicht in queryprestaties, er zijn twee nieuwe metrische gegevens kunt u potentiële knelpunten identificeren geïntroduceerd: aantal duur en uitvoering.</span><span class="sxs-lookup"><span data-stu-id="db3e7-163">In hello recent update of Query Performance Insight, we introduced two new metrics that can help you identify potential bottlenecks: duration and execution count.</span></span><br>

<span data-ttu-id="db3e7-164">Langlopende query's hebben Hallo grootste kans dat er meer resources vergrendelen, andere gebruikers worden geblokkeerd en schaalbaarheid te beperken.</span><span class="sxs-lookup"><span data-stu-id="db3e7-164">Long-running queries have hello greatest potential for locking resources longer, blocking other users, and limiting scalability.</span></span> <span data-ttu-id="db3e7-165">Ze zijn ook Hallo beste kandidaten voor optimalisatie.</span><span class="sxs-lookup"><span data-stu-id="db3e7-165">They are also hello best candidates for optimization.</span></span><br>

<span data-ttu-id="db3e7-166">tooidentify langlopende query's:</span><span class="sxs-lookup"><span data-stu-id="db3e7-166">tooidentify long running queries:</span></span>

1. <span data-ttu-id="db3e7-167">Open **aangepaste** tabblad in de Query Performance Insight voor de geselecteerde database</span><span class="sxs-lookup"><span data-stu-id="db3e7-167">Open **Custom** tab in Query Performance Insight for selected database</span></span>
2. <span data-ttu-id="db3e7-168">Wijzigen van de metrische gegevens toobe **duur**</span><span class="sxs-lookup"><span data-stu-id="db3e7-168">Change metrics toobe **duration**</span></span>
3. <span data-ttu-id="db3e7-169">Selecteer het aantal query's en observatie-interval</span><span class="sxs-lookup"><span data-stu-id="db3e7-169">Select number of queries and observation interval</span></span>
4. <span data-ttu-id="db3e7-170">Selecteer de statistische functie</span><span class="sxs-lookup"><span data-stu-id="db3e7-170">Select aggregation function</span></span>
   
   * <span data-ttu-id="db3e7-171">**Som** tijdens de gehele observatie-interval is de som van alle uitvoeringstijd van de query.</span><span class="sxs-lookup"><span data-stu-id="db3e7-171">**Sum** adds up all query execution time during whole observation interval.</span></span>
   * <span data-ttu-id="db3e7-172">**Maximale** vindt u query's welke uitvoeringstijd maximale was op de hele observatie-interval.</span><span class="sxs-lookup"><span data-stu-id="db3e7-172">**Max** finds queries which execution time was maximum at whole observation interval.</span></span>
   * <span data-ttu-id="db3e7-173">**Gem.** vindt gemiddelde uitvoeringstijd van alle query uitvoeringen en ziet u boven buiten deze gemiddelden Hallo.</span><span class="sxs-lookup"><span data-stu-id="db3e7-173">**Avg** finds average execution time of all query executions and show you hello top out of these averages.</span></span> 
     
     ![duur van de query][4]

## <a name="review-top-queries-per-execution-count"></a><span data-ttu-id="db3e7-175">Bekijk meest gebruikte query's per aantal keer uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="db3e7-175">Review top queries per execution count</span></span>
<span data-ttu-id="db3e7-176">Hoog aantal uitvoeringen mogelijk niet beïnvloeden database zelf en gebruik van bronnen kan lage, maar algemene toepassing, haalt traag.</span><span class="sxs-lookup"><span data-stu-id="db3e7-176">High number of executions might not be affecting database itself and resources usage can be low, but overall application might get slow.</span></span>

<span data-ttu-id="db3e7-177">In sommige gevallen, zeer hoge uitvoering aantal tooincrease van het netwerk kan leiden retouren.</span><span class="sxs-lookup"><span data-stu-id="db3e7-177">In some cases, very high execution count may lead tooincrease of network round trips.</span></span> <span data-ttu-id="db3e7-178">Retouren aanzienlijk beïnvloeden.</span><span class="sxs-lookup"><span data-stu-id="db3e7-178">Round trips significantly affect performance.</span></span> <span data-ttu-id="db3e7-179">Ze zijn onderwerp toonetwork latentie en toodownstream server latentie.</span><span class="sxs-lookup"><span data-stu-id="db3e7-179">They are subject toonetwork latency and toodownstream server latency.</span></span> 

<span data-ttu-id="db3e7-180">Bijvoorbeeld: veel gegevensgestuurde websites sterk toegang krijgen tot Hallo-database voor elke aanvraag van gebruiker.</span><span class="sxs-lookup"><span data-stu-id="db3e7-180">For example, many data-driven Web sites heavily access hello database for every user request.</span></span> <span data-ttu-id="db3e7-181">Tijdens het groepsgewijze helpt, hello verhoogd kunnen netwerkverkeer en de verwerkingsbelasting op de databaseserver Hallo prestaties nadelig beïnvloeden.</span><span class="sxs-lookup"><span data-stu-id="db3e7-181">While connection pooling helps, hello increased network traffic and processing load on hello database server can adversely affect performance.</span></span>  <span data-ttu-id="db3e7-182">Algemeen advies is tookeep ronde reizen tooan absoluut minimum.</span><span class="sxs-lookup"><span data-stu-id="db3e7-182">General advice is tookeep round trips tooan absolute minimum.</span></span>

<span data-ttu-id="db3e7-183">tooidentify uitgevoerd vaak query's ('chatty') query's:</span><span class="sxs-lookup"><span data-stu-id="db3e7-183">tooidentify frequently executed queries (“chatty”) queries:</span></span>

1. <span data-ttu-id="db3e7-184">Open **aangepaste** tabblad in de Query Performance Insight voor de geselecteerde database</span><span class="sxs-lookup"><span data-stu-id="db3e7-184">Open **Custom** tab in Query Performance Insight for selected database</span></span>
2. <span data-ttu-id="db3e7-185">Wijzigen van de metrische gegevens toobe **aantal keer uitgevoerd**</span><span class="sxs-lookup"><span data-stu-id="db3e7-185">Change metrics toobe **execution count**</span></span>
3. <span data-ttu-id="db3e7-186">Selecteer het aantal query's en observatie-interval</span><span class="sxs-lookup"><span data-stu-id="db3e7-186">Select number of queries and observation interval</span></span>
   
    ![uitvoering van het aantal query 's][5]

## <a name="understanding-performance-tuning-annotations"></a><span data-ttu-id="db3e7-188">Inzicht in prestaties afstemmen aantekeningen</span><span class="sxs-lookup"><span data-stu-id="db3e7-188">Understanding performance tuning annotations</span></span>
<span data-ttu-id="db3e7-189">Tijdens het verkennen van de werkbelasting in Query Performance Insight, ziet u mogelijk pictogrammen met verticale lijn boven op het Hallo-grafiek.</span><span class="sxs-lookup"><span data-stu-id="db3e7-189">While exploring your workload in Query Performance Insight, you might notice icons with vertical line on top of hello chart.</span></span><br>

<span data-ttu-id="db3e7-190">Deze pictogrammen zijn aantekeningen; ze hebben betrekking op prestaties beïnvloeden bewerkingen worden uitgevoerd door [SQL Azure Database Advisor](sql-database-advisor.md).</span><span class="sxs-lookup"><span data-stu-id="db3e7-190">These icons are annotations; they represent performance affecting actions performed by [SQL Azure Database Advisor](sql-database-advisor.md).</span></span> <span data-ttu-id="db3e7-191">Door zwevende aantekening krijgen u algemene informatie over Hallo actie:</span><span class="sxs-lookup"><span data-stu-id="db3e7-191">By hovering annotation, you get basic information about hello action:</span></span>

![query aantekening][6]

<span data-ttu-id="db3e7-193">Als u meer tooknow of advisor aanbeveling toepassen, klikt u op Hallo-pictogram.</span><span class="sxs-lookup"><span data-stu-id="db3e7-193">If you want tooknow more or apply advisor recommendation, click hello icon.</span></span> <span data-ttu-id="db3e7-194">Details van de actie wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="db3e7-194">It will open details of action.</span></span> <span data-ttu-id="db3e7-195">Als een actieve bevelen kunt u meteen met behulp van opdracht toepassen.</span><span class="sxs-lookup"><span data-stu-id="db3e7-195">If it’s an active recommendation you can apply it straight away using command.</span></span>

![details van de aantekening query][7]

### <a name="multiple-annotations"></a><span data-ttu-id="db3e7-197">Meerdere aantekeningen.</span><span class="sxs-lookup"><span data-stu-id="db3e7-197">Multiple annotations.</span></span>
<span data-ttu-id="db3e7-198">Het is mogelijk dat vanwege zoomniveau, aantekeningen die andere sluiten tooeach ophalen tot één samengevouwen zullen.</span><span class="sxs-lookup"><span data-stu-id="db3e7-198">It’s possible, that because of zoom level, annotations that are close tooeach other will get collapsed into one.</span></span> <span data-ttu-id="db3e7-199">Hiermee wordt aangegeven door speciale pictogram, erop te klikken wordt geopend nieuwe blade waarin de lijst met aantekeningen gegroepeerd worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="db3e7-199">This will be represented by special icon, clicking it will open new blade where list of grouped annotations will be shown.</span></span>
<span data-ttu-id="db3e7-200">Query's en -prestaties afstemmen acties correleren kunt toobetter inzicht in uw workload.</span><span class="sxs-lookup"><span data-stu-id="db3e7-200">Correlating queries and performance tuning actions can help toobetter understand your workload.</span></span> 

## <a name="optimizing-hello-query-store-configuration-for-query-performance-insight"></a><span data-ttu-id="db3e7-201">Hallo Query Store-configuratie voor Query Performance Insight optimaliseren</span><span class="sxs-lookup"><span data-stu-id="db3e7-201">Optimizing hello Query Store configuration for Query Performance Insight</span></span>
<span data-ttu-id="db3e7-202">Tijdens het gebruik van de Query Performance Insight kunnen optreden Hallo Query Store-berichten te volgen:</span><span class="sxs-lookup"><span data-stu-id="db3e7-202">During your use of Query Performance Insight, you might encounter hello following Query Store messages:</span></span>

* <span data-ttu-id="db3e7-203">'Query Store is niet goed geconfigureerd op deze database.</span><span class="sxs-lookup"><span data-stu-id="db3e7-203">"Query Store is not properly configured on this database.</span></span> <span data-ttu-id="db3e7-204">Klik hier meer toolearn."</span><span class="sxs-lookup"><span data-stu-id="db3e7-204">Click here toolearn more."</span></span>
* <span data-ttu-id="db3e7-205">'Query Store is niet goed geconfigureerd op deze database.</span><span class="sxs-lookup"><span data-stu-id="db3e7-205">"Query Store is not properly configured on this database.</span></span> <span data-ttu-id="db3e7-206">Klik hier toochange instellingen."</span><span class="sxs-lookup"><span data-stu-id="db3e7-206">Click here toochange settings."</span></span> 

<span data-ttu-id="db3e7-207">Deze berichten worden doorgaans weergegeven wanneer Query Store niet kunnen toocollect nieuwe gegevens.</span><span class="sxs-lookup"><span data-stu-id="db3e7-207">These messages usually appear when Query Store is not able toocollect new data.</span></span> 

<span data-ttu-id="db3e7-208">Eerste geval gebeurt wanneer Query Store in alleen-lezen status en parameters optimaal zijn ingesteld.</span><span class="sxs-lookup"><span data-stu-id="db3e7-208">First case happens when Query Store is in Read-Only state and parameters are set optimally.</span></span> <span data-ttu-id="db3e7-209">U kunt dit oplossen door het vergroten van de Query Store of Query Store uit te schakelen.</span><span class="sxs-lookup"><span data-stu-id="db3e7-209">You can fix this by increasing size of Query Store or clearing Query Store.</span></span>

![knop qds][8]

<span data-ttu-id="db3e7-211">Tweede geval gebeurt wanneer de Query Store is uitgeschakeld of de parameters zijn niet optimaal ingesteld.</span><span class="sxs-lookup"><span data-stu-id="db3e7-211">Second case happens when Query Store is Off or parameters aren’t set optimally.</span></span> <br><span data-ttu-id="db3e7-212">U kunt Hallo bewaren en vastleggen beleid en schakel Query Store wijzigen door het uitvoeren van de onderstaande opdrachten of rechtstreeks vanuit de portal:</span><span class="sxs-lookup"><span data-stu-id="db3e7-212">You can change hello Retention and Capture policy and enable Query Store by executing commands below or directly from portal:</span></span>

![knop qds][9]

### <a name="recommended-retention-and-capture-policy"></a><span data-ttu-id="db3e7-214">Aanbevolen bewaren en vastleggen beleid</span><span class="sxs-lookup"><span data-stu-id="db3e7-214">Recommended retention and capture policy</span></span>
<span data-ttu-id="db3e7-215">Er zijn twee soorten bewaarbeleidsregels:</span><span class="sxs-lookup"><span data-stu-id="db3e7-215">There are two types of retention policies:</span></span>

* <span data-ttu-id="db3e7-216">Grootte gebaseerd - als set tooAUTO deze gegevens automatisch bijna maximale grootte wordt opschonen is bereikt.</span><span class="sxs-lookup"><span data-stu-id="db3e7-216">Size based - if set tooAUTO it will clean data automatically when near max size is reached.</span></span>
* <span data-ttu-id="db3e7-217">Op basis van de - standaard haaks het too30 dagen, wat betekent dat, als de Query Store wordt tekort aan ruimte, wordt verwijderd query uitvoeren op informatie die ouder zijn dan 30 dagen</span><span class="sxs-lookup"><span data-stu-id="db3e7-217">Time based - by default we will set it too30 days, which means, if Query Store will run out of space, it will delete query information older than 30 days</span></span>

<span data-ttu-id="db3e7-218">Vastleggen van beleid kan worden ingesteld op:</span><span class="sxs-lookup"><span data-stu-id="db3e7-218">Capture policy could be set to:</span></span>

* <span data-ttu-id="db3e7-219">**Alle** -alle query's worden vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="db3e7-219">**All** - Captures all queries.</span></span>
* <span data-ttu-id="db3e7-220">**Automatische** -incidentele's en query's met verwaarlozen compileren en uitvoering duur worden genegeerd.</span><span class="sxs-lookup"><span data-stu-id="db3e7-220">**Auto** - Infrequent queries and queries with insignificant compile and execution duration are ignored.</span></span> <span data-ttu-id="db3e7-221">Drempelwaarden voor de duur voor het aantal, compileren en runtime uitvoeren worden intern bepaald.</span><span class="sxs-lookup"><span data-stu-id="db3e7-221">Thresholds for execution count, compile and runtime duration are internally determined.</span></span> <span data-ttu-id="db3e7-222">Dit is de standaardoptie Hallo.</span><span class="sxs-lookup"><span data-stu-id="db3e7-222">This is hello default option.</span></span>
* <span data-ttu-id="db3e7-223">**Geen** -Query Store stopt u het vastleggen nieuwe query's, maar de runtime-statistieken voor al vastgelegde query's worden nog steeds verzameld.</span><span class="sxs-lookup"><span data-stu-id="db3e7-223">**None** - Query Store stops capturing new queries, however runtime stats for already captured queries are still collected.</span></span>

<span data-ttu-id="db3e7-224">U wordt aangeraden alle beleidsregels tooAUTO en schone beleid too30 dagen instellen:</span><span class="sxs-lookup"><span data-stu-id="db3e7-224">We recommend setting all policies tooAUTO and clean policy too30 days:</span></span>

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (SIZE_BASED_CLEANUP_MODE = AUTO);

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 30));

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (QUERY_CAPTURE_MODE = AUTO);

<span data-ttu-id="db3e7-225">Verhoog de grootte van de Query Store.</span><span class="sxs-lookup"><span data-stu-id="db3e7-225">Increase size of Query Store.</span></span> <span data-ttu-id="db3e7-226">Dit kan worden uitgevoerd door de verbindende tooa database- en verlenende volgende query:</span><span class="sxs-lookup"><span data-stu-id="db3e7-226">This could be performed by connecting tooa database and issuing following query:</span></span>

    ALTER DATABASE [YourDB]
    SET QUERY_STORE (MAX_STORAGE_SIZE_MB = 1024);

<span data-ttu-id="db3e7-227">Deze instellingen zijn toegepast brengt uiteindelijk Query Store verzamelen van de nieuwe query's, maar als u niet dat toowait wilt u Query Store schakelt.</span><span class="sxs-lookup"><span data-stu-id="db3e7-227">Applying these settings will eventually make Query Store collecting new queries, however if you don’t want toowait you can clear Query Store.</span></span> 

> [!NOTE]
> <span data-ttu-id="db3e7-228">Uitvoeren van de volgende query worden alle huidige gegevens in Query Store Hallo verwijderd.</span><span class="sxs-lookup"><span data-stu-id="db3e7-228">Executing following query will delete all current information in hello Query Store.</span></span> 
> 
> 

    ALTER DATABASE [YourDB] SET QUERY_STORE CLEAR;


## <a name="summary"></a><span data-ttu-id="db3e7-229">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="db3e7-229">Summary</span></span>
<span data-ttu-id="db3e7-230">Inzicht in queryprestaties helpt u begrijpen Hallo impact van uw workload van query's en hoe deze zich verhoudt toodatabase resourceverbruik.</span><span class="sxs-lookup"><span data-stu-id="db3e7-230">Query Performance Insight helps you understand hello impact of your query workload and how it relates toodatabase resource consumption.</span></span> <span data-ttu-id="db3e7-231">Met deze functie wordt u meer informatie over het Hallo-grootste verbruik van query's en eenvoudig hello die toofix identificeren voordat ze een probleem.</span><span class="sxs-lookup"><span data-stu-id="db3e7-231">With this feature, you will learn about hello top consuming queries, and easily identify hello ones toofix before they become a problem.</span></span>

## <a name="next-steps"></a><span data-ttu-id="db3e7-232">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="db3e7-232">Next steps</span></span>
<span data-ttu-id="db3e7-233">Extra aanbevelingen over het verbeteren van Hallo prestaties van uw SQL-database, klikt u op [aanbevelingen](sql-database-advisor.md) op Hallo **Query Performance Insight** blade.</span><span class="sxs-lookup"><span data-stu-id="db3e7-233">For additional recommendations about improving hello performance of your SQL database, click [Recommendations](sql-database-advisor.md) on hello **Query Performance Insight** blade.</span></span>

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

