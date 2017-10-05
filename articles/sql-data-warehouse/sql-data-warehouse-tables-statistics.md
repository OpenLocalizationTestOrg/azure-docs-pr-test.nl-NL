---
title: Het beheren van statistieken over tabellen in SQL Data Warehouse | Microsoft Docs
description: Aan de slag met statistieken over tabellen in Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: faa1034d-314c-4f9d-af81-f5a9aedf33e4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: 1d5ded69e394643ddfc3de0c6d30dbd30c8e848f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="managing-statistics-on-tables-in-sql-data-warehouse"></a><span data-ttu-id="f6f60-103">Het beheren van statistieken over tabellen in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="f6f60-103">Managing statistics on tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="f6f60-104">[Overzicht][Overview]</span><span class="sxs-lookup"><span data-stu-id="f6f60-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="f6f60-105">[Gegevenstypen][Data Types]</span><span class="sxs-lookup"><span data-stu-id="f6f60-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="f6f60-106">[Distribueren][Distribute]</span><span class="sxs-lookup"><span data-stu-id="f6f60-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="f6f60-107">[Index][Index]</span><span class="sxs-lookup"><span data-stu-id="f6f60-107">[Index][Index]</span></span>
> * <span data-ttu-id="f6f60-108">[Partitie][Partition]</span><span class="sxs-lookup"><span data-stu-id="f6f60-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="f6f60-109">[Statistieken][Statistics]</span><span class="sxs-lookup"><span data-stu-id="f6f60-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="f6f60-110">[Tijdelijke][Temporary]</span><span class="sxs-lookup"><span data-stu-id="f6f60-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="f6f60-111">Hoe meer SQL Data Warehouse weet over uw gegevens, hoe sneller een query uitgevoerd op uw gegevens kunnen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f6f60-111">The more SQL Data Warehouse knows about your data, the faster it can execute queries against your data.</span></span>  <span data-ttu-id="f6f60-112">De manier waarop u SQL Data Warehouse zien over uw gegevens is door het verzamelen van statistieken over uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="f6f60-112">The way that you tell SQL Data Warehouse about your data, is by collecting statistics about your data.</span></span>  <span data-ttu-id="f6f60-113">Statistieken over voor uw gegevens is een van de belangrijkste dingen die u doen kunt om uw query's optimaliseren.</span><span class="sxs-lookup"><span data-stu-id="f6f60-113">Having statistics on your data is one of the most important things you can do to optimize your queries.</span></span>  <span data-ttu-id="f6f60-114">Statistieken helpen bij het maken van de optimale planning van uw query's van SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f6f60-114">Statistics help SQL Data Warehouse create the most optimal plan for your queries.</span></span>  <span data-ttu-id="f6f60-115">Dit is omdat SQL Data Warehouse queryoptimalisatie optimalisatie van de kosten die zijn gebaseerd.</span><span class="sxs-lookup"><span data-stu-id="f6f60-115">This is because the SQL Data Warehouse query optimizer is a cost based optimizer.</span></span>  <span data-ttu-id="f6f60-116">Dat wil zeggen, vergelijkt de kosten van verschillende queryplannen en kiest vervolgens het plan met de laagste kosten, moet het plan dat de snelste wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f6f60-116">That is, it compares the cost of various query plans and then chooses the plan with the lowest cost, which should also be the plan that will execute the fastest.</span></span>

<span data-ttu-id="f6f60-117">Statistieken kunnen worden gemaakt op één kolom, meerdere kolommen of op een index van een tabel.</span><span class="sxs-lookup"><span data-stu-id="f6f60-117">Statistics can be created on a single column, multiple columns or on an index of a table.</span></span>  <span data-ttu-id="f6f60-118">Statistieken worden opgeslagen in een histogram die het bereik en selectiviteit van waarden vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="f6f60-118">Statistics are stored in a histogram which captures the range and selectivity of values.</span></span>  <span data-ttu-id="f6f60-119">Dit is met name van belang wanneer het optimalisatieprogramma moet evalueren JOINs, GROUP BY, HAVING en de component WHERE in een query.</span><span class="sxs-lookup"><span data-stu-id="f6f60-119">This is of particular interest when the optimizer needs to evaluate JOINs, GROUP BY, HAVING and WHERE clauses in a query.</span></span>  <span data-ttu-id="f6f60-120">Bijvoorbeeld als het optimalisatieprogramma maakt een schatting van dat de datum die u hebt gefilterd in uw query retourneert 1 rij, kunnen ervoor kiezen een heel andere plannen dan als deze maakt een schatting datum die u hebt geselecteerd wordt 1 miljoen rijen worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="f6f60-120">For example, if the optimizer estimates that the date you are filtering in your query will return 1 row, it may choose a very different plan than if it estimates that they date you have selected will return 1 million rows.</span></span>  <span data-ttu-id="f6f60-121">Tijdens het maken van statistieken is zeer belangrijk, is het belangrijk dat statistieken *nauwkeurig* overeenstemming met de huidige status van de tabel.</span><span class="sxs-lookup"><span data-stu-id="f6f60-121">While creating statistics is extremely important, it is equally important that statistics *accurately* reflect the current state of the table.</span></span>  <span data-ttu-id="f6f60-122">Up-to-date statistieken met zorgt ervoor dat het een goed plan is geselecteerd door de optimaliseren.</span><span class="sxs-lookup"><span data-stu-id="f6f60-122">Having up-to-date statistics ensures that a good plan is selected by the optimizer.</span></span>  <span data-ttu-id="f6f60-123">De abonnementen die zijn gemaakt door het optimalisatieprogramma zijn alleen nuttig als de statistieken voor uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="f6f60-123">The plans created by the optimizer are only as good as the statistics on your data.</span></span>

<span data-ttu-id="f6f60-124">Het proces van het maken en bijwerken van statistieken is op dit moment een handmatig proces, maar het is zeer eenvoudig doen.</span><span class="sxs-lookup"><span data-stu-id="f6f60-124">The process of creating and updating statistics is currently a manual process, but is very simple to do.</span></span>  <span data-ttu-id="f6f60-125">Dit is in tegenstelling tot SQL Server die automatisch wordt gemaakt en statistieken over één kolommen en indexen bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="f6f60-125">This is unlike SQL Server which automatically creates and updates statistics on single columns and indexes.</span></span>  <span data-ttu-id="f6f60-126">U kunt het beheer van de statistieken aanzienlijk voor uw gegevens automatiseren met behulp van de onderstaande informatie.</span><span class="sxs-lookup"><span data-stu-id="f6f60-126">By using the information below, you can greatly automate the management of the statistics on your data.</span></span> 

## <a name="getting-started-with-statistics"></a><span data-ttu-id="f6f60-127">Aan de slag met statistieken</span><span class="sxs-lookup"><span data-stu-id="f6f60-127">Getting started with statistics</span></span>
 <span data-ttu-id="f6f60-128">Steekproef statistieken maken voor elke kolom is een eenvoudige manier om te beginnen met statistieken.</span><span class="sxs-lookup"><span data-stu-id="f6f60-128">Creating sampled statistics on every column is an easy way to get started with statistics.</span></span>  <span data-ttu-id="f6f60-129">Aangezien is het belangrijk statistieken om up-to-date te houden, mogelijk uw statistieken bijwerken dagelijks of na elke load voorzichtig zijn.</span><span class="sxs-lookup"><span data-stu-id="f6f60-129">Since it is equally important to keep statistics up-to-date, a conservative approach may be to update your statistics daily or after each load.</span></span> <span data-ttu-id="f6f60-130">Het maken en bijwerken van statistieken kan ten koste gaan van prestaties en kosten.</span><span class="sxs-lookup"><span data-stu-id="f6f60-130">There are always trade-offs between performance and the cost to create and update statistics.</span></span>  <span data-ttu-id="f6f60-131">Als het te lang duurt om al uw statistieken bij te houden, kunt u overwegen selectiever te zijn in welke kolommen statistieken hebben of voor welke kolommen de statistieken regelmatig moeten worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="f6f60-131">If you find it is taking too long to maintain all of your statistics, you may want to try to be more selective about which columns have statistics or which columns need frequent updating.</span></span>  <span data-ttu-id="f6f60-132">U wilt bijwerken datumkolommen dagelijks nieuwe waarden kunnen worden toegevoegd in plaats van na elke load.</span><span class="sxs-lookup"><span data-stu-id="f6f60-132">For example, you might want to update date columns daily, as new values may be added rather than after every load.</span></span> <span data-ttu-id="f6f60-133">Opnieuw, krijgt u optimaal wilt profiteren doordat de statistieken voor kolommen die zijn betrokken in JOINs, GROUP BY, HAVING en de component WHERE.</span><span class="sxs-lookup"><span data-stu-id="f6f60-133">Again, you will gain the most benefit by having statistics on columns involved in JOINs, GROUP BY, HAVING and WHERE clauses.</span></span>  <span data-ttu-id="f6f60-134">Als u een tabel met een groot aantal kolommen die alleen worden gebruikt in de component SELECT hebt, statistieken voor deze kolommen niet kan helpen en uitgaven iets meer werk alleen de kolommen waarin statistieken helpt, identificeren inkorten de tijd voor het onderhouden van uw statistieken.</span><span class="sxs-lookup"><span data-stu-id="f6f60-134">If you have a table with a lot of columns which are only used in the SELECT clause, statistics on these columns may not help, and spending a little more effort to identify only the columns where statistics will help, can reduce the time to maintain your statistics.</span></span>

## <a name="multi-column-statistics"></a><span data-ttu-id="f6f60-135">Statistieken met meerdere kolommen</span><span class="sxs-lookup"><span data-stu-id="f6f60-135">Multi-column statistics</span></span>
<span data-ttu-id="f6f60-136">Naast het maken van statistieken voor één kolommen, merkt u dat uw query's van meerdere kolomstatistieken profiteren.</span><span class="sxs-lookup"><span data-stu-id="f6f60-136">In addition to creating statistics on single columns, you may find that your queries will benefit from multi-column statistics.</span></span>  <span data-ttu-id="f6f60-137">Statistieken met meerdere kolommen worden statistieken gemaakt op een lijst met kolommen.</span><span class="sxs-lookup"><span data-stu-id="f6f60-137">Multi-column statistics are statistics created on a list of columns.</span></span>  <span data-ttu-id="f6f60-138">Ze bevatten één kolomstatistieken voor de eerste kolom in de lijst, plus informatie cross-kolom correlatie dichtheden aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="f6f60-138">They include single column statistics on the first column in the list, plus some cross-column correlation information called densities.</span></span>  <span data-ttu-id="f6f60-139">Bijvoorbeeld, als er een tabel die samengevoegd op twee kolommen, wellicht dat SQL Data Warehouse beter het plan optimaliseren kunt wordt begrepen dat de relatie tussen de twee kolommen.</span><span class="sxs-lookup"><span data-stu-id="f6f60-139">For example, if you have a table that joins to another on two columns, you may find that SQL Data Warehouse can better optimize the plan if it understands the relationship between two columns.</span></span>   <span data-ttu-id="f6f60-140">Statistieken met meerdere kolommen kunnen query's sneller voor bepaalde bewerkingen zoals joins samengestelde en gegroepeerd.</span><span class="sxs-lookup"><span data-stu-id="f6f60-140">Multi-column statistics can improve query performance for some operations such as composite joins and group by.</span></span>

## <a name="updating-statistics"></a><span data-ttu-id="f6f60-141">Bijwerken van statistieken</span><span class="sxs-lookup"><span data-stu-id="f6f60-141">Updating statistics</span></span>
<span data-ttu-id="f6f60-142">Bijwerken van statistieken is een belangrijk onderdeel van uw database management routine.</span><span class="sxs-lookup"><span data-stu-id="f6f60-142">Updating statistics is an important part of your database management routine.</span></span>  <span data-ttu-id="f6f60-143">Wanneer de distributie van gegevens in de database wordt gewijzigd, moeten de statistieken worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="f6f60-143">When the distribution of data in the database changes, statistics need to be updated.</span></span>  <span data-ttu-id="f6f60-144">Verouderde statistieken zal leiden tot suboptimale queryprestaties.</span><span class="sxs-lookup"><span data-stu-id="f6f60-144">Out-of-date statistics will lead to sub-optimal query performance.</span></span>

<span data-ttu-id="f6f60-145">Een aanbevolen procedure is het bijwerken van statistieken over datumkolommen elke dag als nieuwe datums worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="f6f60-145">One best practice is to update statistics on date columns each day as new dates are added.</span></span>  <span data-ttu-id="f6f60-146">Elke keer nieuwe rijen in het datawarehouse zijn geladen, worden nieuwe load datums of transactiedatums toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="f6f60-146">Each time new rows are loaded into the data warehouse, new load dates or transaction dates are added.</span></span> <span data-ttu-id="f6f60-147">Deze de verdeling van de gegevens wijzigen en de statistieken verouderd wilt maken.</span><span class="sxs-lookup"><span data-stu-id="f6f60-147">These change the data distribution and make the statistics out-of-date.</span></span> <span data-ttu-id="f6f60-148">Als u daarentegen statistieken over een land-kolom in een tabel van de klant mogelijk nooit moeten worden bijgewerkt, zoals de verdeling van waarden in het algemeen niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="f6f60-148">Conversely, statistics on a country column in a customer table might never need to be updated, as the distribution of values doesn’t generally change.</span></span> <span data-ttu-id="f6f60-149">Ervan uitgaande dat de distributie constant tussen klanten, eens toevoegen van nieuwe rijen aan de tabel variatie niet te wijzigen van de gegevensdistributie.</span><span class="sxs-lookup"><span data-stu-id="f6f60-149">Assuming the distribution is constant between customers, adding new rows to the table variation isn't going to change the data distribution.</span></span> <span data-ttu-id="f6f60-150">Echter als uw datawarehouse alleen een bepaald land bevat en u Importeer gegevens vanuit een nieuw land, moet wat resulteert in gegevens uit meerdere landen worden opgeslagen, zeker u statistieken voor de kolom land moeten worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="f6f60-150">However, if your data warehouse only contains one country and you bring in data from a new country, resulting in data from multiple countries being stored, then you definitely need to update statistics on the country column.</span></span>

<span data-ttu-id="f6f60-151">Een van de eerste vragen stellen bij het oplossen van een query is 'Are de statistieken bijgewerkt?'</span><span class="sxs-lookup"><span data-stu-id="f6f60-151">One of the first questions to ask when troubleshooting a query is, "Are the statistics up-to-date?"</span></span>

<span data-ttu-id="f6f60-152">Deze vraag is niet een die door de leeftijd van de gegevens kunnen worden beantwoord.</span><span class="sxs-lookup"><span data-stu-id="f6f60-152">This question is not one that can be answered by the age of the data.</span></span> <span data-ttu-id="f6f60-153">Een object up-to-date statistieken kan worden oude als er geen belangrijke wijzigingen in de onderliggende gegevens zijn.</span><span class="sxs-lookup"><span data-stu-id="f6f60-153">An up to date statistics object could be very old if there's been no material change to the underlying data.</span></span> <span data-ttu-id="f6f60-154">Wanneer het aantal rijen aanzienlijk is gewijzigd of er is een belangrijke wijziging in de distributie van waarden voor een bepaalde kolom *vervolgens* is het tijd om het bijwerken van statistieken.</span><span class="sxs-lookup"><span data-stu-id="f6f60-154">When the number of rows has changed substantially or there is a material change in the distribution of values for a given column *then* it's time to update statistics.</span></span>  

<span data-ttu-id="f6f60-155">Ter referentie: **SQL Server** (geen SQL Data Warehouse) automatisch bijgewerkt statistieken voor deze situaties:</span><span class="sxs-lookup"><span data-stu-id="f6f60-155">For reference, **SQL Server** (not SQL Data Warehouse) automatically updates statistics for these situations:</span></span>

* <span data-ttu-id="f6f60-156">Als er geen rijen in de tabel wanneer u rijen toevoegt, krijgt u een automatische update van statistieken</span><span class="sxs-lookup"><span data-stu-id="f6f60-156">If you have zero rows in the table, when you add rows, you’ll get an automatic update of statistics</span></span>
* <span data-ttu-id="f6f60-157">Wanneer u meer dan 500 rijen toevoegen aan een tabel die beginnen met minder dan 500 rijen (bijvoorbeeld aan begin u hebt 499 en 500 rijen vervolgens toe te voegen aan een totaal van 999 rijen), krijgt u een automatische update</span><span class="sxs-lookup"><span data-stu-id="f6f60-157">When you add more than 500 rows to a table starting with less than 500 rows (e.g. at start you have 499 and then add 500 rows to a total of 999 rows), you’ll get an automatic update</span></span> 
* <span data-ttu-id="f6f60-158">Als u meer dan 500 rijen die u 500 extra rijen + 20% van de grootte van de tabel toevoegen moet voordat u een automatische update op de statistieken ziet klaar</span><span class="sxs-lookup"><span data-stu-id="f6f60-158">Once you’re over 500 rows you will have to add 500 additional rows + 20% of the size of the table before you’ll see an automatic update on the stats</span></span>

<span data-ttu-id="f6f60-159">Omdat er geen DMV om te bepalen of de gegevens in de tabel is gewijzigd sinds de laatste tijd statistieken zijn bijgewerkt, kunt weet de leeftijd van de statistieken u kennismaken met onderdeel van de afbeelding.</span><span class="sxs-lookup"><span data-stu-id="f6f60-159">Since there is no DMV to determine if data within the table has changed since the last time statistics were updated, knowing the age of your statistics can provide you with part of the picture.</span></span>  <span data-ttu-id="f6f60-160">U kunt de volgende query om te bepalen van de laatste keer dat de statistieken waar bijgewerkt op elke tabel.</span><span class="sxs-lookup"><span data-stu-id="f6f60-160">You can use the following query to determine the last time your statistics where updated on each table.</span></span>  

> [!NOTE]
> <span data-ttu-id="f6f60-161">Vergeet niet dat als er een aanzienlijke wijzigingen in de distributie van waarden voor een bepaalde kolom, moet u bijwerken statistieken ongeacht de laatste keer dat ze zijn bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="f6f60-161">Remember if there is a material change in the distribution of values for a given column, you should update statistics regardless of the last time they were updated.</span></span>  
> 
> 

```sql
SELECT
    sm.[name] AS [schema_name],
    tb.[name] AS [table_name],
    co.[name] AS [stats_column_name],
    st.[name] AS [stats_name],
    STATS_DATE(st.[object_id],st.[stats_id]) AS [stats_last_updated_date]
FROM
    sys.objects ob
    JOIN sys.stats st
        ON  ob.[object_id] = st.[object_id]
    JOIN sys.stats_columns sc    
        ON  st.[stats_id] = sc.[stats_id]
        AND st.[object_id] = sc.[object_id]
    JOIN sys.columns co    
        ON  sc.[column_id] = co.[column_id]
        AND sc.[object_id] = co.[object_id]
    JOIN sys.types  ty    
        ON  co.[user_type_id] = ty.[user_type_id]
    JOIN sys.tables tb    
        ON  co.[object_id] = tb.[object_id]
    JOIN sys.schemas sm    
        ON  tb.[schema_id] = sm.[schema_id]
WHERE
    st.[user_created] = 1;
```

<span data-ttu-id="f6f60-162">Datumkolommen in een datawarehouse bijvoorbeeld meestal regelmatig hoeft te worden statistieken updates.</span><span class="sxs-lookup"><span data-stu-id="f6f60-162">Date columns in a data warehouse, for example, usually need frequent statistics updates.</span></span> <span data-ttu-id="f6f60-163">Elke keer nieuwe rijen in het datawarehouse zijn geladen, worden nieuwe load datums of transactiedatums toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="f6f60-163">Each time new rows are loaded into the data warehouse, new load dates or transaction dates are added.</span></span> <span data-ttu-id="f6f60-164">Deze de verdeling van de gegevens wijzigen en de statistieken verouderd wilt maken.</span><span class="sxs-lookup"><span data-stu-id="f6f60-164">These change the data distribution and make the statistics out-of-date.</span></span>  <span data-ttu-id="f6f60-165">Als u daarentegen statistieken voor een kolom geslacht in een klantentabel mogelijk nooit moeten worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="f6f60-165">Conversely, statistics on a gender column on a customer table might never need to be updated.</span></span> <span data-ttu-id="f6f60-166">Ervan uitgaande dat de distributie constant tussen klanten, eens toevoegen van nieuwe rijen aan de tabel variatie niet te wijzigen van de gegevensdistributie.</span><span class="sxs-lookup"><span data-stu-id="f6f60-166">Assuming the distribution is constant between customers, adding new rows to the table variation isn't going to change the data distribution.</span></span> <span data-ttu-id="f6f60-167">Echter als uw datawarehouse slechts één geslacht en een nieuwe vereiste resultaten in meerdere geslachten bevat moet beslist u statistieken voor de kolom geslacht moeten worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="f6f60-167">However, if your data warehouse only contains one gender and a new requirement results in multiple genders then you definitely need to update statistics on the gender column.</span></span>

<span data-ttu-id="f6f60-168">Zie voor verdere uitleg [statistieken] [ Statistics] op MSDN.</span><span class="sxs-lookup"><span data-stu-id="f6f60-168">For further explanation, see [Statistics][Statistics] on MSDN.</span></span>

## <a name="implementing-statistics-management"></a><span data-ttu-id="f6f60-169">Implementatie van statistieken management</span><span class="sxs-lookup"><span data-stu-id="f6f60-169">Implementing statistics management</span></span>
<span data-ttu-id="f6f60-170">Het is vaak een goed idee om uw gegevens laadproces om ervoor te zorgen dat de statistieken worden bijgewerkt aan het einde van de belasting uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="f6f60-170">It is often a good idea to extend your data loading process to ensure that statistics are updated at the end of the load.</span></span> <span data-ttu-id="f6f60-171">Het laden van gegevens is wanneer tabellen meest hun grootte en/of de distributie van de waarden wijzigen.</span><span class="sxs-lookup"><span data-stu-id="f6f60-171">The data load is when tables most frequently change their size and/or their distribution of values.</span></span> <span data-ttu-id="f6f60-172">Daarom is dit een logische plaats voor het implementeren van een aantal processen.</span><span class="sxs-lookup"><span data-stu-id="f6f60-172">Therefore, this is a logical place to implement some management processes.</span></span>

<span data-ttu-id="f6f60-173">Sommige principes zijn hieronder beschikbaar voor het bijwerken van de statistieken tijdens het laadproces:</span><span class="sxs-lookup"><span data-stu-id="f6f60-173">Some guiding principles are provided below for updating your statistics during the load process:</span></span>

* <span data-ttu-id="f6f60-174">Zorg ervoor dat elke geladen tabel ten minste één statistieken-object bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="f6f60-174">Ensure that each loaded table has at least one statistics object updated.</span></span> <span data-ttu-id="f6f60-175">Hiermee wordt de informatie over de grootte (aantal rijen en aantal pagina's) van tabellen als onderdeel van de update van de statistieken bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="f6f60-175">This updates the tables size (row count and page count) information as part of the stats update.</span></span>
* <span data-ttu-id="f6f60-176">Richt u op de kolommen die deel uitmaken van JOIN, GROUP BY, ORDER BY en DISTINCT-componenten</span><span class="sxs-lookup"><span data-stu-id="f6f60-176">Focus on columns participating in JOIN, GROUP BY, ORDER BY and DISTINCT clauses</span></span>
* <span data-ttu-id="f6f60-177">Houd rekening met het bijwerken van kolommen 'oplopende sleutel' zoals transactie datums vaker als deze waarden niet in het histogram statistieken opgenomen worden.</span><span class="sxs-lookup"><span data-stu-id="f6f60-177">Consider updating "ascending key" columns such as transaction dates more frequently as these values will not be included in the statistics histogram.</span></span>
* <span data-ttu-id="f6f60-178">U kunt statische distributiekolommen minder vaak bijwerken.</span><span class="sxs-lookup"><span data-stu-id="f6f60-178">Consider updating static distribution columns less frequently.</span></span>
* <span data-ttu-id="f6f60-179">Vergeet niet dat elk object statistiek is bijgewerkt in de reeks.</span><span class="sxs-lookup"><span data-stu-id="f6f60-179">Remember each statistic object is updated in series.</span></span> <span data-ttu-id="f6f60-180">Gewoon implementeren `UPDATE STATISTICS <TABLE_NAME>` mogelijk niet ideaal - vooral voor grote tabellen met veel objecten zijn statistieken.</span><span class="sxs-lookup"><span data-stu-id="f6f60-180">Simply implementing `UPDATE STATISTICS <TABLE_NAME>` may not be ideal - especially for wide tables with lots of statistics objects.</span></span>

> [!NOTE]
> <span data-ttu-id="f6f60-181">Raadpleeg de SQL Server 2014 kardinaliteitsschatting model technisch document voor meer informatie over [sleutel oplopende].</span><span class="sxs-lookup"><span data-stu-id="f6f60-181">For more details on [ascending key] please refer to the SQL Server 2014 cardinality estimation model whitepaper.</span></span>
> 
> 

<span data-ttu-id="f6f60-182">Zie voor verdere uitleg [Kardinaliteitsschatting] [ Cardinality Estimation] op MSDN.</span><span class="sxs-lookup"><span data-stu-id="f6f60-182">For further explanation, see  [Cardinality Estimation][Cardinality Estimation] on MSDN.</span></span>

## <a name="examples-create-statistics"></a><span data-ttu-id="f6f60-183">Voorbeelden: Statistieken maken</span><span class="sxs-lookup"><span data-stu-id="f6f60-183">Examples: Create statistics</span></span>
<span data-ttu-id="f6f60-184">Deze voorbeelden laten zien hoe het gebruik van verschillende opties voor het maken van statistieken.</span><span class="sxs-lookup"><span data-stu-id="f6f60-184">These examples show how to use various options for creating statistics.</span></span> <span data-ttu-id="f6f60-185">De opties die u voor elke kolom gebruikt is afhankelijk van de kenmerken van uw gegevens en hoe u de kolom wordt gebruikt in query's.</span><span class="sxs-lookup"><span data-stu-id="f6f60-185">The options that you use for each column depend on the characteristics of your data and how the column will be used in queries.</span></span>

### <a name="a-create-single-column-statistics-with-default-options"></a><span data-ttu-id="f6f60-186">A.</span><span class="sxs-lookup"><span data-stu-id="f6f60-186">A.</span></span> <span data-ttu-id="f6f60-187">Statistieken voor één kolom maken met de standaardopties</span><span class="sxs-lookup"><span data-stu-id="f6f60-187">Create single-column statistics with default options</span></span>
<span data-ttu-id="f6f60-188">Verstrek voor statistieken maken voor een kolom, een naam voor het object statistieken en de naam van de kolom.</span><span class="sxs-lookup"><span data-stu-id="f6f60-188">To create statistics on a column, simply provide a name for the statistics object and the name of the column.</span></span>

<span data-ttu-id="f6f60-189">Deze syntaxis gebruikt alle standaardopties.</span><span class="sxs-lookup"><span data-stu-id="f6f60-189">This syntax uses all of the default options.</span></span> <span data-ttu-id="f6f60-190">SQL Data Warehouse voorbeelden standaard 20 procent van de tabel bij het maken van statistieken.</span><span class="sxs-lookup"><span data-stu-id="f6f60-190">By default, SQL Data Warehouse samples 20 percent of the table when it creates statistics.</span></span>

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]);
```

<span data-ttu-id="f6f60-191">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f6f60-191">For example:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1);
```

### <a name="b-create-single-column-statistics-by-examining-every-row"></a><span data-ttu-id="f6f60-192">B.</span><span class="sxs-lookup"><span data-stu-id="f6f60-192">B.</span></span> <span data-ttu-id="f6f60-193">Maken van statistieken voor één kolom aan de hand van elke rij</span><span class="sxs-lookup"><span data-stu-id="f6f60-193">Create single-column statistics by examining every row</span></span>
<span data-ttu-id="f6f60-194">De samplingfrequentie standaardwaarde van 20 procent is voldoende voor de meeste situaties.</span><span class="sxs-lookup"><span data-stu-id="f6f60-194">The default sampling rate of 20 percent is sufficient for most situations.</span></span> <span data-ttu-id="f6f60-195">U kunt echter de samplingfrequentie aanpassen.</span><span class="sxs-lookup"><span data-stu-id="f6f60-195">However, you can adjust the sampling rate.</span></span>

<span data-ttu-id="f6f60-196">Gebruik de volgende syntaxis om een voorbeeld van de volledige tabel:</span><span class="sxs-lookup"><span data-stu-id="f6f60-196">To sample the full table, use this syntax:</span></span>

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]) WITH FULLSCAN;
```

<span data-ttu-id="f6f60-197">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f6f60-197">For example:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH FULLSCAN;
```

### <a name="c-create-single-column-statistics-by-specifying-the-sample-size"></a><span data-ttu-id="f6f60-198">C.</span><span class="sxs-lookup"><span data-stu-id="f6f60-198">C.</span></span> <span data-ttu-id="f6f60-199">Maken van statistieken voor één kolom door te geven van de grootte van de steekproef</span><span class="sxs-lookup"><span data-stu-id="f6f60-199">Create single-column statistics by specifying the sample size</span></span>
<span data-ttu-id="f6f60-200">U kunt ook de grootte van de steekproef opgeven als een percentage:</span><span class="sxs-lookup"><span data-stu-id="f6f60-200">Alternatively, you can specify the sample size as a percent:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH SAMPLE = 50 PERCENT;
```

### <a name="d-create-single-column-statistics-on-only-some-of-the-rows"></a><span data-ttu-id="f6f60-201">D.</span><span class="sxs-lookup"><span data-stu-id="f6f60-201">D.</span></span> <span data-ttu-id="f6f60-202">Maken van statistieken voor één kolom op slechts een deel van de rijen</span><span class="sxs-lookup"><span data-stu-id="f6f60-202">Create single-column statistics on only some of the rows</span></span>
<span data-ttu-id="f6f60-203">Een andere optie kunt u statistieken op een gedeelte van de rijen in de tabel.</span><span class="sxs-lookup"><span data-stu-id="f6f60-203">Another option, you can create statistics on a portion of the rows in your table.</span></span> <span data-ttu-id="f6f60-204">Dit is een gefilterde statistieken genoemd.</span><span class="sxs-lookup"><span data-stu-id="f6f60-204">This is called a filtered statistic.</span></span>

<span data-ttu-id="f6f60-205">U kunt bijvoorbeeld gefilterde statistieken gebruiken als u van plan bent een query uitvoeren op een specifieke partitie van een grote gepartitioneerde tabel.</span><span class="sxs-lookup"><span data-stu-id="f6f60-205">For example, you could use filtered statistics when you plan to query a specific partition of a large partitioned table.</span></span> <span data-ttu-id="f6f60-206">Als u statistieken maakt op alleen de waarden van de partitie, de nauwkeurigheid van de statistieken wordt te verbeteren, en daarom queryprestaties verbeteren.</span><span class="sxs-lookup"><span data-stu-id="f6f60-206">By creating statistics on only the partition values, the accuracy of the statistics will improve, and therefore improve query performance.</span></span>

<span data-ttu-id="f6f60-207">In dit voorbeeld maakt statistieken op een bereik met waarden.</span><span class="sxs-lookup"><span data-stu-id="f6f60-207">This example creates statistics on a range of values.</span></span> <span data-ttu-id="f6f60-208">De waarden kunnen eenvoudig worden gedefinieerd zodat deze overeenkomt met het bereik van waarden in een partitie.</span><span class="sxs-lookup"><span data-stu-id="f6f60-208">The values could easily be defined to match the range of values in a partition.</span></span>

```sql
CREATE STATISTICS stats_col1 ON table1(col1) WHERE col1 > '2000101' AND col1 < '20001231';
```

> [!NOTE]
> <span data-ttu-id="f6f60-209">Voor queryoptimalisatie overwegen gefilterde statistieken wanneer deze het plan gedistribueerde query kiest, moet de query binnen de definitie van de statistieken object passen.</span><span class="sxs-lookup"><span data-stu-id="f6f60-209">For the query optimizer to consider using filtered statistics when it chooses the distributed query plan, the query must fit inside the definition of the statistics object.</span></span> <span data-ttu-id="f6f60-210">Met behulp van het vorige voorbeeld van de query waarin component moet col1 waarden tussen 2000101 en 20001231 opgeven.</span><span class="sxs-lookup"><span data-stu-id="f6f60-210">Using the previous example, the query's where clause needs to specify col1 values between 2000101 and 20001231.</span></span>
> 
> 

### <a name="e-create-single-column-statistics-with-all-the-options"></a><span data-ttu-id="f6f60-211">E.</span><span class="sxs-lookup"><span data-stu-id="f6f60-211">E.</span></span> <span data-ttu-id="f6f60-212">Statistieken voor één kolom maken met alle opties</span><span class="sxs-lookup"><span data-stu-id="f6f60-212">Create single-column statistics with all the options</span></span>
<span data-ttu-id="f6f60-213">U kunt de opties natuurlijk samen combineren.</span><span class="sxs-lookup"><span data-stu-id="f6f60-213">You can, of course, combine the options together.</span></span> <span data-ttu-id="f6f60-214">Het volgende voorbeeld wordt een gefilterde statistieken-object gemaakt met een aangepaste samplegrootte:</span><span class="sxs-lookup"><span data-stu-id="f6f60-214">The example below creates a filtered statistics object with a custom sample size:</span></span>

```sql
CREATE STATISTICS stats_col1 ON table1 (col1) WHERE col1 > '2000101' AND col1 < '20001231' WITH SAMPLE = 50 PERCENT;
```

<span data-ttu-id="f6f60-215">Zie voor de volledige verwijzing [CREATE STATISTICS] [ CREATE STATISTICS] op MSDN.</span><span class="sxs-lookup"><span data-stu-id="f6f60-215">For the full reference, see [CREATE STATISTICS][CREATE STATISTICS] on MSDN.</span></span>

### <a name="f-create-multi-column-statistics"></a><span data-ttu-id="f6f60-216">F.</span><span class="sxs-lookup"><span data-stu-id="f6f60-216">F.</span></span> <span data-ttu-id="f6f60-217">Statistieken met meerdere kolommen maken</span><span class="sxs-lookup"><span data-stu-id="f6f60-217">Create multi-column statistics</span></span>
<span data-ttu-id="f6f60-218">Voor het maken van een statistieken met meerdere kolommen gewoon gebruiken de eerdere voorbeelden, maar meer kolommen opgeven.</span><span class="sxs-lookup"><span data-stu-id="f6f60-218">To create a multi-column statistics, simply use the previous examples, but specify more columns.</span></span>

> [!NOTE]
> <span data-ttu-id="f6f60-219">Het histogram, wordt gebruikt om het aantal rijen in het queryresultaat schatten, is alleen beschikbaar voor de eerste kolom die worden vermeld in de objectdefinitie van statistieken.</span><span class="sxs-lookup"><span data-stu-id="f6f60-219">The histogram, which is used to estimate number of rows in the query result, is only available for the first column listed in the statistics object definition.</span></span>
> 
> 

<span data-ttu-id="f6f60-220">In dit voorbeeld wordt het histogram is op *product\_categorie*.</span><span class="sxs-lookup"><span data-stu-id="f6f60-220">In this example, the histogram is on *product\_category*.</span></span> <span data-ttu-id="f6f60-221">Statistieken voor cross-kolom worden berekend op *product\_categorie* en *product\_sub_c\ategory*:</span><span class="sxs-lookup"><span data-stu-id="f6f60-221">Cross-column statistics are calculated on *product\_category* and *product\_sub_c\ategory*:</span></span>

```sql
CREATE STATISTICS stats_2cols ON table1 (product_category, product_sub_category) WHERE product_category > '2000101' AND product_category < '20001231' WITH SAMPLE = 50 PERCENT;
```

<span data-ttu-id="f6f60-222">Omdat er een correlatie tussen *product\_categorie* en *product\_sub\_categorie*, een stat met meerdere kolommen kan nuttig zijn als deze kolommen zijn toegankelijk op hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="f6f60-222">Since there is a correlation between *product\_category* and *product\_sub\_category*, a multi-column stat can be useful if these columns are accessed at the same time.</span></span>

### <a name="g-create-statistics-on-all-the-columns-in-a-table"></a><span data-ttu-id="f6f60-223">G.</span><span class="sxs-lookup"><span data-stu-id="f6f60-223">G.</span></span> <span data-ttu-id="f6f60-224">Statistieken maken voor alle kolommen in een tabel</span><span class="sxs-lookup"><span data-stu-id="f6f60-224">Create statistics on all the columns in a table</span></span>
<span data-ttu-id="f6f60-225">Een manier om statistieken te maken is om problemen CREATE STATISTICS opdrachten na het maken van de tabel.</span><span class="sxs-lookup"><span data-stu-id="f6f60-225">One way to create statistics is to issues CREATE STATISTICS commands after creating the table.</span></span>

```sql
CREATE TABLE dbo.table1
(
   col1 int
,  col2 int
,  col3 int
)
WITH
  (
    CLUSTERED COLUMNSTORE INDEX
  )
;

CREATE STATISTICS stats_col1 on dbo.table1 (col1);
CREATE STATISTICS stats_col2 on dbo.table2 (col2);
CREATE STATISTICS stats_col3 on dbo.table3 (col3);
```

### <a name="h-use-a-stored-procedure-to-create-statistics-on-all-columns-in-a-database"></a><span data-ttu-id="f6f60-226">H.</span><span class="sxs-lookup"><span data-stu-id="f6f60-226">H.</span></span> <span data-ttu-id="f6f60-227">Een opgeslagen procedure gebruiken om statistieken te maken voor alle kolommen in een database</span><span class="sxs-lookup"><span data-stu-id="f6f60-227">Use a stored procedure to create statistics on all columns in a database</span></span>
<span data-ttu-id="f6f60-228">SQL Data Warehouse heeft geen een systeem opgeslagen procedure die gelijk is aan [sp_create_stats] [] in SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f6f60-228">SQL Data Warehouse does not have a system stored procedure equivalent to [sp_create_stats][] in SQL Server.</span></span> <span data-ttu-id="f6f60-229">Deze opgeslagen procedure maakt een object van de statistieken één kolom voor elke kolom van de database die nog geen statistieken.</span><span class="sxs-lookup"><span data-stu-id="f6f60-229">This stored procedure creates a single column statistics object on every column of the database that doesn't already have statistics.</span></span>

<span data-ttu-id="f6f60-230">Dit helpt u aan de slag met het ontwerp van de database.</span><span class="sxs-lookup"><span data-stu-id="f6f60-230">This will help you get started with your database design.</span></span> <span data-ttu-id="f6f60-231">U kunt deze aanpassen aan uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="f6f60-231">Feel free to adapt it to your needs.</span></span>

```sql
CREATE PROCEDURE    [dbo].[prc_sqldw_create_stats]
(   @create_type    tinyint -- 1 default 2 Fullscan 3 Sample
,   @sample_pct     tinyint
)
AS

IF @create_type NOT IN (1,2,3)
BEGIN
    THROW 151000,'Invalid value for @stats_type parameter. Valid range 1 (default), 2 (fullscan) or 3 (sample).',1;
END;

IF @sample_pct IS NULL
BEGIN;
    SET @sample_pct = 20;
END;

IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN;
    DROP TABLE #stats_ddl;
END;

CREATE TABLE #stats_ddl
WITH    (   DISTRIBUTION    = HASH([seq_nmbr])
        ,   LOCATION        = USER_DB
        )
AS
WITH T
AS
(
SELECT      t.[name]                        AS [table_name]
,           s.[name]                        AS [table_schema_name]
,           c.[name]                        AS [column_name]
,           c.[column_id]                   AS [column_id]
,           t.[object_id]                   AS [object_id]
,           ROW_NUMBER()
            OVER(ORDER BY (SELECT NULL))    AS [seq_nmbr]
FROM        sys.[tables] t
JOIN        sys.[schemas] s         ON  t.[schema_id]       = s.[schema_id]
JOIN        sys.[columns] c         ON  t.[object_id]       = c.[object_id]
LEFT JOIN   sys.[stats_columns] l   ON  l.[object_id]       = c.[object_id]
                                    AND l.[column_id]       = c.[column_id]
                                    AND l.[stats_column_id] = 1
LEFT JOIN    sys.[external_tables] e    ON    e.[object_id]        = t.[object_id]
WHERE       l.[object_id] IS NULL
AND            e.[object_id] IS NULL -- not an external table
)
SELECT  [table_schema_name]
,       [table_name]
,       [column_name]
,       [column_id]
,       [object_id]
,       [seq_nmbr]
,       CASE @create_type
        WHEN 1
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+')' AS VARCHAR(8000))
        WHEN 2
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+') WITH FULLSCAN' AS VARCHAR(8000))
        WHEN 3
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+') WITH SAMPLE '+@sample_pct+'PERCENT' AS VARCHAR(8000))
        END AS create_stat_ddl
FROM T
;

DECLARE @i INT              = 1
,       @t INT              = (SELECT COUNT(*) FROM #stats_ddl)
,       @s NVARCHAR(4000)   = N''
;

WHILE @i <= @t
BEGIN
    SET @s=(SELECT create_stat_ddl FROM #stats_ddl WHERE seq_nmbr = @i);

    PRINT @s
    EXEC sp_executesql @s
    SET @i+=1;
END

DROP TABLE #stats_ddl;
```

<span data-ttu-id="f6f60-232">Voor het maken van statistieken voor alle kolommen in de tabel met deze procedure, kunt u de procedure te roepen.</span><span class="sxs-lookup"><span data-stu-id="f6f60-232">To create statistics on all columns in the table with this procedure, simply call the procedure.</span></span>

```sql
prc_sqldw_create_stats;
```

## <a name="examples-update-statistics"></a><span data-ttu-id="f6f60-233">Voorbeelden: update statistics</span><span class="sxs-lookup"><span data-stu-id="f6f60-233">Examples: update statistics</span></span>
<span data-ttu-id="f6f60-234">Voor het bijwerken van statistieken, kunt u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="f6f60-234">To update statistics, you can:</span></span>

1. <span data-ttu-id="f6f60-235">Een object van de statistieken worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="f6f60-235">Update one statistics object.</span></span> <span data-ttu-id="f6f60-236">Geef de naam van de statistieken-object dat u wilt bijwerken.</span><span class="sxs-lookup"><span data-stu-id="f6f60-236">Specify the name of the statistics object you wish to update.</span></span>
2. <span data-ttu-id="f6f60-237">Werk alle statistieken objecten in een tabel.</span><span class="sxs-lookup"><span data-stu-id="f6f60-237">Update all statistics objects on a table.</span></span> <span data-ttu-id="f6f60-238">Geef de naam van de tabel in plaats van één specifieke statistieken-object.</span><span class="sxs-lookup"><span data-stu-id="f6f60-238">Specify the name of the table instead of one specific statistics object.</span></span>

### <a name="a-update-one-specific-statistics-object"></a><span data-ttu-id="f6f60-239">A.</span><span class="sxs-lookup"><span data-stu-id="f6f60-239">A.</span></span> <span data-ttu-id="f6f60-240">Object voor een specifieke statistieken bijwerken</span><span class="sxs-lookup"><span data-stu-id="f6f60-240">Update one specific statistics object</span></span>
<span data-ttu-id="f6f60-241">Gebruik de volgende syntaxis als u een object specifieke statistieken bij te werken:</span><span class="sxs-lookup"><span data-stu-id="f6f60-241">Use the following syntax to update a specific statistics object:</span></span>

```sql
UPDATE STATISTICS [schema_name].[table_name]([stat_name]);
```

<span data-ttu-id="f6f60-242">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f6f60-242">For example:</span></span>

```sql
UPDATE STATISTICS [dbo].[table1] ([stats_col1]);
```

<span data-ttu-id="f6f60-243">Door het bijwerken van statistieken voor specifieke objecten, minimaliseert u de tijd en resources die vereist zijn voor het beheren van statistieken.</span><span class="sxs-lookup"><span data-stu-id="f6f60-243">By updating specific statistics objects, you can minimize the time and resources required to manage statistics.</span></span> <span data-ttu-id="f6f60-244">Hiervoor moet voorzichtig, maar om de beste objecten statistieken bijwerken te kiezen.</span><span class="sxs-lookup"><span data-stu-id="f6f60-244">This requires some thought, though, to choose the best statistics objects to update.</span></span>

### <a name="b-update-all-statistics-on-a-table"></a><span data-ttu-id="f6f60-245">B.</span><span class="sxs-lookup"><span data-stu-id="f6f60-245">B.</span></span> <span data-ttu-id="f6f60-246">Bijwerken van alle statistische gegevens in een tabel</span><span class="sxs-lookup"><span data-stu-id="f6f60-246">Update all statistics on a table</span></span>
<span data-ttu-id="f6f60-247">Hier wordt een eenvoudige methode voor het bijwerken van de statistieken-objecten in een tabel.</span><span class="sxs-lookup"><span data-stu-id="f6f60-247">This shows a simple method for updating all the statistics objects on a table.</span></span>

```sql
UPDATE STATISTICS [schema_name].[table_name];
```

<span data-ttu-id="f6f60-248">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f6f60-248">For example:</span></span>

```sql
UPDATE STATISTICS dbo.table1;
```

<span data-ttu-id="f6f60-249">Deze instructie is eenvoudig te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f6f60-249">This statement is easy to use.</span></span> <span data-ttu-id="f6f60-250">Vergeet niet dit alle statistische gegevens voor de tabel wordt bijgewerkt en meer werk dan noodzakelijk is daarom mogelijk uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f6f60-250">Just remember this updates all statistics on the table, and therefore might perform more work than is necessary.</span></span> <span data-ttu-id="f6f60-251">Als de prestaties niet een probleem is, is dit zeker de eenvoudigste en meest volledige manier om te garanderen statistieken zijn bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="f6f60-251">If the performance is not an issue, this is definitely the easiest and most complete way to guarantee statistics are up-to-date.</span></span>

> [!NOTE]
> <span data-ttu-id="f6f60-252">Wanneer alle statistische gegevens in een tabel wordt bijgewerkt, wordt in SQL Data Warehouse een scan met het volgende voorbeeld de tabel voor elke statistieken bevat.</span><span class="sxs-lookup"><span data-stu-id="f6f60-252">When updating all statistics on a table, SQL Data Warehouse does a scan to sample the table for each statistics.</span></span> <span data-ttu-id="f6f60-253">Als de tabel groot is, heeft veel kolommen en meer statistische gegevens, mogelijk efficiënter afzonderlijke statistieken op basis van behoeften moeten worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="f6f60-253">If the table is large, has many columns, and many statistics, it might be more efficient to update individual statistics based on need.</span></span>
> 
> 

<span data-ttu-id="f6f60-254">Voor een implementatie van een `UPDATE STATISTICS` Zie de procedure de [tijdelijke tabellen] [ Temporary] artikel.</span><span class="sxs-lookup"><span data-stu-id="f6f60-254">For an implementation of an `UPDATE STATISTICS` procedure please see the [Temporary Tables][Temporary] article.</span></span> <span data-ttu-id="f6f60-255">De implementatie-methode is iets anders dan bij de `CREATE STATISTICS` bovenstaande procedure, maar het eindresultaat is hetzelfde.</span><span class="sxs-lookup"><span data-stu-id="f6f60-255">The implementation method is slightly different to the `CREATE STATISTICS` procedure above but the end result is the same.</span></span>

<span data-ttu-id="f6f60-256">Zie voor de volledige syntaxis [Update Statistics] [ Update Statistics] op MSDN.</span><span class="sxs-lookup"><span data-stu-id="f6f60-256">For the full syntax, see [Update Statistics][Update Statistics] on MSDN.</span></span>

## <a name="statistics-metadata"></a><span data-ttu-id="f6f60-257">Statistieken metagegevens</span><span class="sxs-lookup"><span data-stu-id="f6f60-257">Statistics metadata</span></span>
<span data-ttu-id="f6f60-258">Er zijn verschillende systeemweergave en functies die u gebruiken kunt om informatie over statistieken te vinden.</span><span class="sxs-lookup"><span data-stu-id="f6f60-258">There are several system view and functions that you can use to find information about statistics.</span></span> <span data-ttu-id="f6f60-259">U kunt bijvoorbeeld zien als een object statistieken mogelijk verouderd met behulp van de functie statistieken datum om te zien wanneer statistieken laatste zijn gemaakt of bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="f6f60-259">For example, you can see if a statistics object might be out-of-date by using the stats-date function to see when statistics were last created or updated.</span></span>

### <a name="catalog-views-for-statistics"></a><span data-ttu-id="f6f60-260">Catalogusweergaven voor statistieken</span><span class="sxs-lookup"><span data-stu-id="f6f60-260">Catalog views for statistics</span></span>
<span data-ttu-id="f6f60-261">Deze systeemweergaven bevatten informatie over statistieken:</span><span class="sxs-lookup"><span data-stu-id="f6f60-261">These system views provide information about statistics:</span></span>

| <span data-ttu-id="f6f60-262">Catalogusweergave</span><span class="sxs-lookup"><span data-stu-id="f6f60-262">Catalog View</span></span> | <span data-ttu-id="f6f60-263">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f6f60-263">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="f6f60-264">[sys.Columns][sys.columns]</span><span class="sxs-lookup"><span data-stu-id="f6f60-264">[sys.columns][sys.columns]</span></span> |<span data-ttu-id="f6f60-265">Een rij voor elke kolom.</span><span class="sxs-lookup"><span data-stu-id="f6f60-265">One row for each column.</span></span> |
| <span data-ttu-id="f6f60-266">[sys.Objects][sys.objects]</span><span class="sxs-lookup"><span data-stu-id="f6f60-266">[sys.objects][sys.objects]</span></span> |<span data-ttu-id="f6f60-267">Een rij voor elk object in de database.</span><span class="sxs-lookup"><span data-stu-id="f6f60-267">One row for each object in the database.</span></span> |
| <span data-ttu-id="f6f60-268">[sys.schemas][sys.schemas]</span><span class="sxs-lookup"><span data-stu-id="f6f60-268">[sys.schemas][sys.schemas]</span></span> |<span data-ttu-id="f6f60-269">Een rij voor elk schema in de database.</span><span class="sxs-lookup"><span data-stu-id="f6f60-269">One row for each schema in the database.</span></span> |
| <span data-ttu-id="f6f60-270">[sys.Stats][sys.stats]</span><span class="sxs-lookup"><span data-stu-id="f6f60-270">[sys.stats][sys.stats]</span></span> |<span data-ttu-id="f6f60-271">Een rij voor elk object statistieken.</span><span class="sxs-lookup"><span data-stu-id="f6f60-271">One row for each statistics object.</span></span> |
| <span data-ttu-id="f6f60-272">[sys.stats_columns][sys.stats_columns]</span><span class="sxs-lookup"><span data-stu-id="f6f60-272">[sys.stats_columns][sys.stats_columns]</span></span> |<span data-ttu-id="f6f60-273">Een rij voor elke kolom in het object statistieken.</span><span class="sxs-lookup"><span data-stu-id="f6f60-273">One row for each column in the statistics object.</span></span> <span data-ttu-id="f6f60-274">Koppelingen naar sys.columns.</span><span class="sxs-lookup"><span data-stu-id="f6f60-274">Links back to sys.columns.</span></span> |
| <span data-ttu-id="f6f60-275">[sys.Tables][sys.tables]</span><span class="sxs-lookup"><span data-stu-id="f6f60-275">[sys.tables][sys.tables]</span></span> |<span data-ttu-id="f6f60-276">Een rij voor elke tabel (inclusief externe tabellen).</span><span class="sxs-lookup"><span data-stu-id="f6f60-276">One row for each table (includes external tables).</span></span> |
| <span data-ttu-id="f6f60-277">[sys.table_types][sys.table_types]</span><span class="sxs-lookup"><span data-stu-id="f6f60-277">[sys.table_types][sys.table_types]</span></span> |<span data-ttu-id="f6f60-278">Een rij voor elk gegevenstype.</span><span class="sxs-lookup"><span data-stu-id="f6f60-278">One row for each data type.</span></span> |

### <a name="system-functions-for-statistics"></a><span data-ttu-id="f6f60-279">Systeemfuncties voor statistieken</span><span class="sxs-lookup"><span data-stu-id="f6f60-279">System functions for statistics</span></span>
<span data-ttu-id="f6f60-280">Deze systeemfuncties zijn nuttig voor het werken met statistieken:</span><span class="sxs-lookup"><span data-stu-id="f6f60-280">These system functions are useful for working with statistics:</span></span>

| <span data-ttu-id="f6f60-281">De systeemfunctie</span><span class="sxs-lookup"><span data-stu-id="f6f60-281">System Function</span></span> | <span data-ttu-id="f6f60-282">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f6f60-282">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="f6f60-283">[STATS_DATE][STATS_DATE]</span><span class="sxs-lookup"><span data-stu-id="f6f60-283">[STATS_DATE][STATS_DATE]</span></span> |<span data-ttu-id="f6f60-284">De datum is die het object statistieken voor het laatst is bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="f6f60-284">Date the statistics object was last updated.</span></span> |
| <span data-ttu-id="f6f60-285">[DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS]</span><span class="sxs-lookup"><span data-stu-id="f6f60-285">[DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS]</span></span> |<span data-ttu-id="f6f60-286">Biedt samenvatting niveau en gedetailleerde informatie over de distributie van de waarden zoals begrepen door het object statistieken.</span><span class="sxs-lookup"><span data-stu-id="f6f60-286">Provides summary level and detailed information about the distribution of values as understood by the statistics object.</span></span> |

### <a name="combine-statistics-columns-and-functions-into-one-view"></a><span data-ttu-id="f6f60-287">Functies en statistieken kolommen combineren in één weergave</span><span class="sxs-lookup"><span data-stu-id="f6f60-287">Combine statistics columns and functions into one view</span></span>
<span data-ttu-id="f6f60-288">Deze weergave biedt kolommen die betrekking op statistieken hebben en resultaat is van de functie samen [] van [STATS_DATE()].</span><span class="sxs-lookup"><span data-stu-id="f6f60-288">This view brings columns that relate to statistics, and results from the [STATS_DATE()][]function together.</span></span>

```sql
CREATE VIEW dbo.vstats_columns
AS
SELECT
        sm.[name]                           AS [schema_name]
,       tb.[name]                           AS [table_name]
,       st.[name]                           AS [stats_name]
,       st.[filter_definition]              AS [stats_filter_defiinition]
,       st.[has_filter]                     AS [stats_is_filtered]
,       STATS_DATE(st.[object_id],st.[stats_id])
                                            AS [stats_last_updated_date]
,       co.[name]                           AS [stats_column_name]
,       ty.[name]                           AS [column_type]
,       co.[max_length]                     AS [column_max_length]
,       co.[precision]                      AS [column_precision]
,       co.[scale]                          AS [column_scale]
,       co.[is_nullable]                    AS [column_is_nullable]
,       co.[collation_name]                 AS [column_collation_name]
,       QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])
                                            AS two_part_name
,       QUOTENAME(DB_NAME())+'.'+QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])
                                            AS three_part_name
FROM    sys.objects                         AS ob
JOIN    sys.stats           AS st ON    ob.[object_id]      = st.[object_id]
JOIN    sys.stats_columns   AS sc ON    st.[stats_id]       = sc.[stats_id]
                            AND         st.[object_id]      = sc.[object_id]
JOIN    sys.columns         AS co ON    sc.[column_id]      = co.[column_id]
                            AND         sc.[object_id]      = co.[object_id]
JOIN    sys.types           AS ty ON    co.[user_type_id]   = ty.[user_type_id]
JOIN    sys.tables          AS tb ON  co.[object_id]        = tb.[object_id]
JOIN    sys.schemas         AS sm ON  tb.[schema_id]        = sm.[schema_id]
WHERE   1=1
AND     st.[user_created] = 1
;
```

## <a name="dbcc-showstatistics-examples"></a><span data-ttu-id="f6f60-289">DBCC SHOW_STATISTICS()-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="f6f60-289">DBCC SHOW_STATISTICS() examples</span></span>
<span data-ttu-id="f6f60-290">DBCC SHOW_STATISTICS() bevat gegevens die zijn opgeslagen in een object van statistieken.</span><span class="sxs-lookup"><span data-stu-id="f6f60-290">DBCC SHOW_STATISTICS() shows the data held within a statistics object.</span></span> <span data-ttu-id="f6f60-291">Deze gegevens zijn afkomstig uit drie delen.</span><span class="sxs-lookup"><span data-stu-id="f6f60-291">This data comes in three parts.</span></span>

1. <span data-ttu-id="f6f60-292">Koptekst</span><span class="sxs-lookup"><span data-stu-id="f6f60-292">Header</span></span>
2. <span data-ttu-id="f6f60-293">Dichtheid Vector</span><span class="sxs-lookup"><span data-stu-id="f6f60-293">Density Vector</span></span>
3. <span data-ttu-id="f6f60-294">Histogram</span><span class="sxs-lookup"><span data-stu-id="f6f60-294">Histogram</span></span>

<span data-ttu-id="f6f60-295">De header-metagegevens over de statistieken.</span><span class="sxs-lookup"><span data-stu-id="f6f60-295">The header metadata about the statistics.</span></span> <span data-ttu-id="f6f60-296">Het histogram geeft de verdeling van waarden in de eerste kolom van de sleutel van het object statistieken.</span><span class="sxs-lookup"><span data-stu-id="f6f60-296">The histogram displays the distribution of values in the first key column of the statistics object.</span></span> <span data-ttu-id="f6f60-297">De dichtheid vector metingen cross-kolom correlatie.</span><span class="sxs-lookup"><span data-stu-id="f6f60-297">The density vector measures cross-column correlation.</span></span> <span data-ttu-id="f6f60-298">SQLDW berekent kardinaliteit maakt een schatting met een van de gegevens in de statistieken-object.</span><span class="sxs-lookup"><span data-stu-id="f6f60-298">SQLDW computes cardinality estimates with any of the data in the statistics object.</span></span>

### <a name="show-header-density-and-histogram"></a><span data-ttu-id="f6f60-299">Koptekst, dichtheid en histogram weergeven</span><span class="sxs-lookup"><span data-stu-id="f6f60-299">Show header, density, and histogram</span></span>
<span data-ttu-id="f6f60-300">Dit eenvoudige voorbeeld toont alle drie onderdelen van een object statistieken.</span><span class="sxs-lookup"><span data-stu-id="f6f60-300">This simple example shows all three parts of a statistics object.</span></span>

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>)
```

<span data-ttu-id="f6f60-301">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f6f60-301">For example:</span></span>

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1);
```

### <a name="show-one-or-more-parts-of-dbcc-showstatistics"></a><span data-ttu-id="f6f60-302">Een of meer onderdelen van DBCC SHOW_STATISTICS(); weergeven</span><span class="sxs-lookup"><span data-stu-id="f6f60-302">Show one or more parts of DBCC SHOW_STATISTICS();</span></span>
<span data-ttu-id="f6f60-303">Als u alleen geïnteresseerd bent in specifieke onderdelen weer te geven, gebruikt u de `WITH` component en opgeven welke onderdelen die u wilt zien:</span><span class="sxs-lookup"><span data-stu-id="f6f60-303">If you are only interested in viewing specific parts, use the `WITH` clause and specify which parts you want to see:</span></span>

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>) WITH stat_header, histogram, density_vector
```

<span data-ttu-id="f6f60-304">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f6f60-304">For example:</span></span>

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1) WITH histogram, density_vector
```

## <a name="dbcc-showstatistics-differences"></a><span data-ttu-id="f6f60-305">DBCC SHOW_STATISTICS() verschillen</span><span class="sxs-lookup"><span data-stu-id="f6f60-305">DBCC SHOW_STATISTICS() differences</span></span>
<span data-ttu-id="f6f60-306">DBCC SHOW_STATISTICS() is meer strikt in SQL Data Warehouse vergeleken met SQL Server geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="f6f60-306">DBCC SHOW_STATISTICS() is more strictly implemented in SQL Data Warehouse compared to SQL Server.</span></span>

1. <span data-ttu-id="f6f60-307">Niet-gedocumenteerde functies worden niet ondersteund</span><span class="sxs-lookup"><span data-stu-id="f6f60-307">Undocumented features are not supported</span></span>
2. <span data-ttu-id="f6f60-308">Stats_stream kan niet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f6f60-308">Cannot use Stats_stream</span></span>
3. <span data-ttu-id="f6f60-309">Resultaten voor specifieke subreeksen van statistische gegevens bijvoorbeeld niet koppelen (STAT_HEADER JOIN DENSITY_VECTOR)</span><span class="sxs-lookup"><span data-stu-id="f6f60-309">Cannot join results for specific subsets of statistics data e.g. (STAT_HEADER JOIN DENSITY_VECTOR)</span></span>
4. <span data-ttu-id="f6f60-310">NO_INFOMSGS kan niet worden ingesteld voor bericht onderdrukken</span><span class="sxs-lookup"><span data-stu-id="f6f60-310">NO_INFOMSGS cannot be set for message suppression</span></span>
5. <span data-ttu-id="f6f60-311">Vierkante haken om de namen van statistieken kan niet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f6f60-311">Square brackets around statistics names cannot be used</span></span>
6. <span data-ttu-id="f6f60-312">Kan geen kolomnamen gebruiken om statistieken objecten te identificeren</span><span class="sxs-lookup"><span data-stu-id="f6f60-312">Cannot use column names to identify statistics objects</span></span>
7. <span data-ttu-id="f6f60-313">Aangepaste fout 2767 wordt niet ondersteund</span><span class="sxs-lookup"><span data-stu-id="f6f60-313">Custom error 2767 is not supported</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6f60-314">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f6f60-314">Next steps</span></span>
<span data-ttu-id="f6f60-315">Zie voor meer informatie [DBCC SHOW_STATISTICS] [ DBCC SHOW_STATISTICS] op MSDN.</span><span class="sxs-lookup"><span data-stu-id="f6f60-315">For more details, see [DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS] on MSDN.</span></span>  <span data-ttu-id="f6f60-316">Zie voor meer informatie de artikelen op [tabel overzicht][Overview], [tabel gegevenstypen][Data Types], [distribueren van een tabel] [ Distribute], [Indexeren van een tabel][Index], [partitioneren van een tabel] [ Partition] en [Tijdelijke tabellen][Temporary].</span><span class="sxs-lookup"><span data-stu-id="f6f60-316">To learn more, see the articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="f6f60-317">Zie voor meer informatie over best practices [aanbevolen procedures van SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="f6f60-317">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>  

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->  
[Cardinality Estimation]: https://msdn.microsoft.com/library/dn600374.aspx
[CREATE STATISTICS]: https://msdn.microsoft.com/library/ms188038.aspx
[DBCC SHOW_STATISTICS]:https://msdn.microsoft.com/library/ms174384.aspx
[Statistics]: https://msdn.microsoft.com/library/ms190397.aspx
[STATS_DATE]: https://msdn.microsoft.com/library/ms190330.aspx
[sys.columns]: https://msdn.microsoft.com/library/ms176106.aspx
[sys.objects]: https://msdn.microsoft.com/library/ms190324.aspx
[sys.schemas]: https://msdn.microsoft.com/library/ms190324.aspx
[sys.stats]: https://msdn.microsoft.com/library/ms177623.aspx
[sys.stats_columns]: https://msdn.microsoft.com/library/ms187340.aspx
[sys.tables]: https://msdn.microsoft.com/library/ms187406.aspx
[sys.table_types]: https://msdn.microsoft.com/library/bb510623.aspx
[UPDATE STATISTICS]: https://msdn.microsoft.com/library/ms187348.aspx

<!--Other Web references-->  
