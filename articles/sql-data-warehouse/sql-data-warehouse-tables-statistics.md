---
title: aaaManaging statistieken over tabellen in SQL Data Warehouse | Microsoft Docs
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
ms.openlocfilehash: c9521dc47891f68d124e77a53e2e15d03275caaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-statistics-on-tables-in-sql-data-warehouse"></a><span data-ttu-id="e99e1-103">Het beheren van statistieken over tabellen in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e99e1-103">Managing statistics on tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="e99e1-104">[Overzicht][Overview]</span><span class="sxs-lookup"><span data-stu-id="e99e1-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="e99e1-105">[Gegevenstypen][Data Types]</span><span class="sxs-lookup"><span data-stu-id="e99e1-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="e99e1-106">[Distribueren][Distribute]</span><span class="sxs-lookup"><span data-stu-id="e99e1-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="e99e1-107">[Index][Index]</span><span class="sxs-lookup"><span data-stu-id="e99e1-107">[Index][Index]</span></span>
> * <span data-ttu-id="e99e1-108">[Partitie][Partition]</span><span class="sxs-lookup"><span data-stu-id="e99e1-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="e99e1-109">[Statistieken][Statistics]</span><span class="sxs-lookup"><span data-stu-id="e99e1-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="e99e1-110">[Tijdelijke][Temporary]</span><span class="sxs-lookup"><span data-stu-id="e99e1-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="e99e1-111">Hallo meer SQL Data Warehouse weet over uw gegevens hello sneller kunnen worden uitgevoerd een query uitgevoerd op uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="e99e1-111">hello more SQL Data Warehouse knows about your data, hello faster it can execute queries against your data.</span></span>  <span data-ttu-id="e99e1-112">Hallo-manier waarop u SQL Data Warehouse vertellen over uw gegevens, is door het verzamelen van statistieken over uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="e99e1-112">hello way that you tell SQL Data Warehouse about your data, is by collecting statistics about your data.</span></span>  <span data-ttu-id="e99e1-113">Statistieken over voor uw gegevens is een van de belangrijkste zaken Hallo kunt u toooptimize uw query's uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="e99e1-113">Having statistics on your data is one of hello most important things you can do toooptimize your queries.</span></span>  <span data-ttu-id="e99e1-114">Statistieken helpen SQL Data Warehouse Hallo optimale plan voor uw query's maken.</span><span class="sxs-lookup"><span data-stu-id="e99e1-114">Statistics help SQL Data Warehouse create hello most optimal plan for your queries.</span></span>  <span data-ttu-id="e99e1-115">Dit is omdat Hallo SQL Data Warehouse query optimaliseren is kosten op basis van optimaliseren.</span><span class="sxs-lookup"><span data-stu-id="e99e1-115">This is because hello SQL Data Warehouse query optimizer is a cost based optimizer.</span></span>  <span data-ttu-id="e99e1-116">Dat wil zeggen, het Hallo kosten van verschillende queryplannen vergelijkt en vervolgens kiest Hallo plan met de laagste kosten hello, moet ook Hallo-plan dat Hallo snelste wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e99e1-116">That is, it compares hello cost of various query plans and then chooses hello plan with hello lowest cost, which should also be hello plan that will execute hello fastest.</span></span>

<span data-ttu-id="e99e1-117">Statistieken kunnen worden gemaakt op één kolom, meerdere kolommen of op een index van een tabel.</span><span class="sxs-lookup"><span data-stu-id="e99e1-117">Statistics can be created on a single column, multiple columns or on an index of a table.</span></span>  <span data-ttu-id="e99e1-118">Statistieken worden opgeslagen in een histogram Hallo bereik en selectiviteit van waarden bevat.</span><span class="sxs-lookup"><span data-stu-id="e99e1-118">Statistics are stored in a histogram which captures hello range and selectivity of values.</span></span>  <span data-ttu-id="e99e1-119">Dit is met name van belang wanneer Hallo optimaliseren tooevaluate JOINs, GROUP BY, HAVING moet en WHERE-componenten in een query.</span><span class="sxs-lookup"><span data-stu-id="e99e1-119">This is of particular interest when hello optimizer needs tooevaluate JOINs, GROUP BY, HAVING and WHERE clauses in a query.</span></span>  <span data-ttu-id="e99e1-120">Bijvoorbeeld als Hallo optimaliseren maakt een schatting van dat Hallo datum die u hebt gefilterd in uw query retourneert 1 rij, kunnen ervoor kiezen een heel andere plannen dan als deze maakt een schatting datum die u hebt geselecteerd wordt 1 miljoen rijen worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="e99e1-120">For example, if hello optimizer estimates that hello date you are filtering in your query will return 1 row, it may choose a very different plan than if it estimates that they date you have selected will return 1 million rows.</span></span>  <span data-ttu-id="e99e1-121">Tijdens het maken van statistieken is zeer belangrijk, is het belangrijk dat statistieken *nauwkeurig* Hallo huidige status van de tabel Hallo weerspiegelen.</span><span class="sxs-lookup"><span data-stu-id="e99e1-121">While creating statistics is extremely important, it is equally important that statistics *accurately* reflect hello current state of hello table.</span></span>  <span data-ttu-id="e99e1-122">Met up-to-date statistieken zorgt ervoor dat het een goed plan is geselecteerd door Hallo optimaliseren.</span><span class="sxs-lookup"><span data-stu-id="e99e1-122">Having up-to-date statistics ensures that a good plan is selected by hello optimizer.</span></span>  <span data-ttu-id="e99e1-123">Hallo plannen die zijn gemaakt door optimalisatie van Hallo zijn alleen nuttig als Hallo statistieken over uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="e99e1-123">hello plans created by hello optimizer are only as good as hello statistics on your data.</span></span>

<span data-ttu-id="e99e1-124">Hallo-proces van het maken en bijwerken van statistieken is op dit moment een handmatig proces, maar het is zeer eenvoudig toodo.</span><span class="sxs-lookup"><span data-stu-id="e99e1-124">hello process of creating and updating statistics is currently a manual process, but is very simple toodo.</span></span>  <span data-ttu-id="e99e1-125">Dit is in tegenstelling tot SQL Server die automatisch wordt gemaakt en statistieken over één kolommen en indexen bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="e99e1-125">This is unlike SQL Server which automatically creates and updates statistics on single columns and indexes.</span></span>  <span data-ttu-id="e99e1-126">Met behulp van Hallo informatie hieronder kunt u aanzienlijk Hallo beheer van Hallo statistieken automatiseren voor uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="e99e1-126">By using hello information below, you can greatly automate hello management of hello statistics on your data.</span></span> 

## <a name="getting-started-with-statistics"></a><span data-ttu-id="e99e1-127">Aan de slag met statistieken</span><span class="sxs-lookup"><span data-stu-id="e99e1-127">Getting started with statistics</span></span>
 <span data-ttu-id="e99e1-128">Steekproef statistieken maken voor elke kolom is een eenvoudige manier tooget gestart met statistieken.</span><span class="sxs-lookup"><span data-stu-id="e99e1-128">Creating sampled statistics on every column is an easy way tooget started with statistics.</span></span>  <span data-ttu-id="e99e1-129">Omdat het even belangrijk tookeep statistieken up-to-date voorzichtig kan worden tooupdate uw statistieken dagelijks of na elke load.</span><span class="sxs-lookup"><span data-stu-id="e99e1-129">Since it is equally important tookeep statistics up-to-date, a conservative approach may be tooupdate your statistics daily or after each load.</span></span> <span data-ttu-id="e99e1-130">Er zijn altijd verschillen tussen de prestaties en Hallo kosten toocreate en update statistics.</span><span class="sxs-lookup"><span data-stu-id="e99e1-130">There are always trade-offs between performance and hello cost toocreate and update statistics.</span></span>  <span data-ttu-id="e99e1-131">Als u dat het duurt te lang toomaintain alle van de statistieken vindt, kunt u tootry toobe meer selectieve over welke kolommen hebben statistieken of welke kolommen regelmatig hoeft te worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="e99e1-131">If you find it is taking too long toomaintain all of your statistics, you may want tootry toobe more selective about which columns have statistics or which columns need frequent updating.</span></span>  <span data-ttu-id="e99e1-132">Bijvoorbeeld, kunt u tooupdate datumkolommen dagelijks nieuwe waarden kunnen worden toegevoegd in plaats van na elke load.</span><span class="sxs-lookup"><span data-stu-id="e99e1-132">For example, you might want tooupdate date columns daily, as new values may be added rather than after every load.</span></span> <span data-ttu-id="e99e1-133">Opnieuw, krijgt u Hallo profiteren doordat de statistieken voor kolommen die zijn betrokken in JOINs, GROUP BY, HAVING en de component WHERE.</span><span class="sxs-lookup"><span data-stu-id="e99e1-133">Again, you will gain hello most benefit by having statistics on columns involved in JOINs, GROUP BY, HAVING and WHERE clauses.</span></span>  <span data-ttu-id="e99e1-134">Als u een tabel met een groot aantal hebt kolommen die alleen worden gebruikt in Hallo SELECT-component, statistieken voor deze kolommen kunnen niet help en nog iets meer moeite tooidentify uitgaven alleen Hallo kolommen waarin statistieken helpt, inkorten Hallo tijd toomaintain uw statistieken .</span><span class="sxs-lookup"><span data-stu-id="e99e1-134">If you have a table with a lot of columns which are only used in hello SELECT clause, statistics on these columns may not help, and spending a little more effort tooidentify only hello columns where statistics will help, can reduce hello time toomaintain your statistics.</span></span>

## <a name="multi-column-statistics"></a><span data-ttu-id="e99e1-135">Statistieken met meerdere kolommen</span><span class="sxs-lookup"><span data-stu-id="e99e1-135">Multi-column statistics</span></span>
<span data-ttu-id="e99e1-136">Bovendien toocreating statistieken voor één kolommen, merkt u dat uw query's van meerdere kolomstatistieken profiteren.</span><span class="sxs-lookup"><span data-stu-id="e99e1-136">In addition toocreating statistics on single columns, you may find that your queries will benefit from multi-column statistics.</span></span>  <span data-ttu-id="e99e1-137">Statistieken met meerdere kolommen worden statistieken gemaakt op een lijst met kolommen.</span><span class="sxs-lookup"><span data-stu-id="e99e1-137">Multi-column statistics are statistics created on a list of columns.</span></span>  <span data-ttu-id="e99e1-138">Ze één kolomstatistieken over de eerste kolom Hallo opnemen in lijst hello, plus informatie cross-kolom correlatie dichtheden aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="e99e1-138">They include single column statistics on hello first column in hello list, plus some cross-column correlation information called densities.</span></span>  <span data-ttu-id="e99e1-139">Bijvoorbeeld, als er een tabel met twee kolommen tooanother koppelt, wellicht dat SQL Data Warehouse beter Hallo plan optimaliseren kunt wordt begrepen Hallo relatie tussen twee kolommen.</span><span class="sxs-lookup"><span data-stu-id="e99e1-139">For example, if you have a table that joins tooanother on two columns, you may find that SQL Data Warehouse can better optimize hello plan if it understands hello relationship between two columns.</span></span>   <span data-ttu-id="e99e1-140">Statistieken met meerdere kolommen kunnen query's sneller voor bepaalde bewerkingen zoals joins samengestelde en gegroepeerd.</span><span class="sxs-lookup"><span data-stu-id="e99e1-140">Multi-column statistics can improve query performance for some operations such as composite joins and group by.</span></span>

## <a name="updating-statistics"></a><span data-ttu-id="e99e1-141">Bijwerken van statistieken</span><span class="sxs-lookup"><span data-stu-id="e99e1-141">Updating statistics</span></span>
<span data-ttu-id="e99e1-142">Bijwerken van statistieken is een belangrijk onderdeel van uw database management routine.</span><span class="sxs-lookup"><span data-stu-id="e99e1-142">Updating statistics is an important part of your database management routine.</span></span>  <span data-ttu-id="e99e1-143">Als de distributie van gegevens in de database Hallo Hallo verandert, moeten statistieken toobe bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="e99e1-143">When hello distribution of data in hello database changes, statistics need toobe updated.</span></span>  <span data-ttu-id="e99e1-144">Verouderde statistieken leidt toosub optimale query-prestaties.</span><span class="sxs-lookup"><span data-stu-id="e99e1-144">Out-of-date statistics will lead toosub-optimal query performance.</span></span>

<span data-ttu-id="e99e1-145">Een aanbevolen procedure is tooupdate statistieken over datumkolommen elke dag als nieuwe datums worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="e99e1-145">One best practice is tooupdate statistics on date columns each day as new dates are added.</span></span>  <span data-ttu-id="e99e1-146">Elke keer nieuwe rijen zijn geladen in het datawarehouse hello, worden nieuwe load datums of transactiedatums toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="e99e1-146">Each time new rows are loaded into hello data warehouse, new load dates or transaction dates are added.</span></span> <span data-ttu-id="e99e1-147">Deze wijzigen Hallo gegevensdistributie en Hallo statistieken verouderd wilt maken.</span><span class="sxs-lookup"><span data-stu-id="e99e1-147">These change hello data distribution and make hello statistics out-of-date.</span></span> <span data-ttu-id="e99e1-148">Als u daarentegen statistieken over een land-kolom in een tabel van de klant nooit moet mogelijk toobe bijgewerkt, zoals Hallo distributie van de waarden in het algemeen niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="e99e1-148">Conversely, statistics on a country column in a customer table might never need toobe updated, as hello distribution of values doesn’t generally change.</span></span> <span data-ttu-id="e99e1-149">Ervan uitgaande dat Hallo distributie constant tussen klanten, het toevoegen van nieuwe rijen toohello tabel variatie is niet op het punt toochange Hallo gegevensdistributie.</span><span class="sxs-lookup"><span data-stu-id="e99e1-149">Assuming hello distribution is constant between customers, adding new rows toohello table variation isn't going toochange hello data distribution.</span></span> <span data-ttu-id="e99e1-150">Echter, als uw datawarehouse alleen een bepaald land bevat en u Importeer gegevens vanuit een nieuw land, wat resulteert in gegevens uit meerdere landen worden opgeslagen, zeker moet u tooupdate statistieken op Hallo land kolom.</span><span class="sxs-lookup"><span data-stu-id="e99e1-150">However, if your data warehouse only contains one country and you bring in data from a new country, resulting in data from multiple countries being stored, then you definitely need tooupdate statistics on hello country column.</span></span>

<span data-ttu-id="e99e1-151">Een van de Hallo eerste vragen tooask wanneer het oplossen van een query, 'Hallo statistieken actueel zijn?"</span><span class="sxs-lookup"><span data-stu-id="e99e1-151">One of hello first questions tooask when troubleshooting a query is, "Are hello statistics up-to-date?"</span></span>

<span data-ttu-id="e99e1-152">Deze vraag is niet een die kunnen worden beantwoord door Hallo leeftijd van de Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="e99e1-152">This question is not one that can be answered by hello age of hello data.</span></span> <span data-ttu-id="e99e1-153">Een up-to-date toodate statistieken-object kan worden oude als er is geen aanzienlijke wijzigingen toohello onderliggende gegevens.</span><span class="sxs-lookup"><span data-stu-id="e99e1-153">An up toodate statistics object could be very old if there's been no material change toohello underlying data.</span></span> <span data-ttu-id="e99e1-154">Wanneer het aantal rijen Hallo aanzienlijk is gewijzigd of er is een belangrijke wijziging in Hallo verdeling van waarden voor een bepaalde kolom *vervolgens* tooupdate statistieken is.</span><span class="sxs-lookup"><span data-stu-id="e99e1-154">When hello number of rows has changed substantially or there is a material change in hello distribution of values for a given column *then* it's time tooupdate statistics.</span></span>  

<span data-ttu-id="e99e1-155">Ter referentie: **SQL Server** (geen SQL Data Warehouse) automatisch bijgewerkt statistieken voor deze situaties:</span><span class="sxs-lookup"><span data-stu-id="e99e1-155">For reference, **SQL Server** (not SQL Data Warehouse) automatically updates statistics for these situations:</span></span>

* <span data-ttu-id="e99e1-156">Als er geen rijen in de tabel hello, wanneer u rijen toevoegt, krijgt u een automatische update van statistieken</span><span class="sxs-lookup"><span data-stu-id="e99e1-156">If you have zero rows in hello table, when you add rows, you’ll get an automatic update of statistics</span></span>
* <span data-ttu-id="e99e1-157">Wanneer u meer dan 500 rijen tooa tabel beginnen met minder dan 500 rijen toevoegen (bijvoorbeeld aan begin u 499 hebben en voegt vervolgens 500 rijen tooa totaal 999 rijen), krijgt u een automatische update</span><span class="sxs-lookup"><span data-stu-id="e99e1-157">When you add more than 500 rows tooa table starting with less than 500 rows (e.g. at start you have 499 and then add 500 rows tooa total of 999 rows), you’ll get an automatic update</span></span> 
* <span data-ttu-id="e99e1-158">Als u meer dan 500 rijen klaar hebt uitgevoerd, 500 extra rijen tooadd + 20% van de grootte van tabel Hallo Hallo voordat u een automatische update op Hallo-statistieken ziet</span><span class="sxs-lookup"><span data-stu-id="e99e1-158">Once you’re over 500 rows you will have tooadd 500 additional rows + 20% of hello size of hello table before you’ll see an automatic update on hello stats</span></span>

<span data-ttu-id="e99e1-159">Omdat er geen toodetermine DMV als gegevens binnen het Hallo-tabel is gewijzigd sinds de laatste tijdstatistieken Hallo zijn bijgewerkt, kunt weten Hallo leeftijd van de statistieken u kennismaken met onderdeel van Hallo-afbeelding.</span><span class="sxs-lookup"><span data-stu-id="e99e1-159">Since there is no DMV toodetermine if data within hello table has changed since hello last time statistics were updated, knowing hello age of your statistics can provide you with part of hello picture.</span></span>  <span data-ttu-id="e99e1-160">Kunt u Hallo query toodetermine Hallo laatste keer dat de statistieken te volgen waarbij bijgewerkt op elke tabel.</span><span class="sxs-lookup"><span data-stu-id="e99e1-160">You can use hello following query toodetermine hello last time your statistics where updated on each table.</span></span>  

> [!NOTE]
> <span data-ttu-id="e99e1-161">Vergeet niet dat als er een aanzienlijke wijzigingen in Hallo verdeling van waarden voor een bepaalde kolom, moet u bijwerken statistieken ongeacht Hallo laatste keer dat ze zijn bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="e99e1-161">Remember if there is a material change in hello distribution of values for a given column, you should update statistics regardless of hello last time they were updated.</span></span>  
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

<span data-ttu-id="e99e1-162">Datumkolommen in een datawarehouse bijvoorbeeld meestal regelmatig hoeft te worden statistieken updates.</span><span class="sxs-lookup"><span data-stu-id="e99e1-162">Date columns in a data warehouse, for example, usually need frequent statistics updates.</span></span> <span data-ttu-id="e99e1-163">Elke keer nieuwe rijen zijn geladen in het datawarehouse hello, worden nieuwe load datums of transactiedatums toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="e99e1-163">Each time new rows are loaded into hello data warehouse, new load dates or transaction dates are added.</span></span> <span data-ttu-id="e99e1-164">Deze wijzigen Hallo gegevensdistributie en Hallo statistieken verouderd wilt maken.</span><span class="sxs-lookup"><span data-stu-id="e99e1-164">These change hello data distribution and make hello statistics out-of-date.</span></span>  <span data-ttu-id="e99e1-165">Als u daarentegen statistieken voor een kolom geslacht in een klantentabel mogelijk nooit toobe bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="e99e1-165">Conversely, statistics on a gender column on a customer table might never need toobe updated.</span></span> <span data-ttu-id="e99e1-166">Ervan uitgaande dat Hallo distributie constant tussen klanten, het toevoegen van nieuwe rijen toohello tabel variatie is niet op het punt toochange Hallo gegevensdistributie.</span><span class="sxs-lookup"><span data-stu-id="e99e1-166">Assuming hello distribution is constant between customers, adding new rows toohello table variation isn't going toochange hello data distribution.</span></span> <span data-ttu-id="e99e1-167">Echter als uw datawarehouse slechts één geslacht en een nieuwe vereiste resultaten in meerdere geslachten bevat moet beslist u tooupdate statistieken op Hallo geslacht kolom.</span><span class="sxs-lookup"><span data-stu-id="e99e1-167">However, if your data warehouse only contains one gender and a new requirement results in multiple genders then you definitely need tooupdate statistics on hello gender column.</span></span>

<span data-ttu-id="e99e1-168">Zie voor verdere uitleg [statistieken] [ Statistics] op MSDN.</span><span class="sxs-lookup"><span data-stu-id="e99e1-168">For further explanation, see [Statistics][Statistics] on MSDN.</span></span>

## <a name="implementing-statistics-management"></a><span data-ttu-id="e99e1-169">Implementatie van statistieken management</span><span class="sxs-lookup"><span data-stu-id="e99e1-169">Implementing statistics management</span></span>
<span data-ttu-id="e99e1-170">Het is vaak een goed idee tooextend uw gegevens te laden proces tooensure die statistieken worden bijgewerkt op Hallo end Hallo belast.</span><span class="sxs-lookup"><span data-stu-id="e99e1-170">It is often a good idea tooextend your data loading process tooensure that statistics are updated at hello end of hello load.</span></span> <span data-ttu-id="e99e1-171">laden van gegevens Hallo is wanneer tabellen meest hun grootte en/of de distributie van de waarden wijzigen.</span><span class="sxs-lookup"><span data-stu-id="e99e1-171">hello data load is when tables most frequently change their size and/or their distribution of values.</span></span> <span data-ttu-id="e99e1-172">Daarom is dit een logische plaats tooimplement bepaalde processen voor Apparaatbeheer.</span><span class="sxs-lookup"><span data-stu-id="e99e1-172">Therefore, this is a logical place tooimplement some management processes.</span></span>

<span data-ttu-id="e99e1-173">Sommige principes zijn hieronder beschikbaar voor het bijwerken van de statistieken tijdens het laden van Hallo:</span><span class="sxs-lookup"><span data-stu-id="e99e1-173">Some guiding principles are provided below for updating your statistics during hello load process:</span></span>

* <span data-ttu-id="e99e1-174">Zorg ervoor dat elke geladen tabel ten minste één statistieken-object bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="e99e1-174">Ensure that each loaded table has at least one statistics object updated.</span></span> <span data-ttu-id="e99e1-175">Deze updates Hallo-informatie over de grootte (aantal rijen en aantal pagina's) als onderdeel van Hallo statistieken update tabellen.</span><span class="sxs-lookup"><span data-stu-id="e99e1-175">This updates hello tables size (row count and page count) information as part of hello stats update.</span></span>
* <span data-ttu-id="e99e1-176">Richt u op de kolommen die deel uitmaken van JOIN, GROUP BY, ORDER BY en DISTINCT-componenten</span><span class="sxs-lookup"><span data-stu-id="e99e1-176">Focus on columns participating in JOIN, GROUP BY, ORDER BY and DISTINCT clauses</span></span>
* <span data-ttu-id="e99e1-177">Houd rekening met het bijwerken van kolommen 'oplopende sleutel' zoals transactie vaker als deze waarden niet in Hallo statistieken histogram opgenomen worden datums.</span><span class="sxs-lookup"><span data-stu-id="e99e1-177">Consider updating "ascending key" columns such as transaction dates more frequently as these values will not be included in hello statistics histogram.</span></span>
* <span data-ttu-id="e99e1-178">U kunt statische distributiekolommen minder vaak bijwerken.</span><span class="sxs-lookup"><span data-stu-id="e99e1-178">Consider updating static distribution columns less frequently.</span></span>
* <span data-ttu-id="e99e1-179">Vergeet niet dat elk object statistiek is bijgewerkt in de reeks.</span><span class="sxs-lookup"><span data-stu-id="e99e1-179">Remember each statistic object is updated in series.</span></span> <span data-ttu-id="e99e1-180">Gewoon implementeren `UPDATE STATISTICS <TABLE_NAME>` mogelijk niet ideaal - vooral voor grote tabellen met veel objecten zijn statistieken.</span><span class="sxs-lookup"><span data-stu-id="e99e1-180">Simply implementing `UPDATE STATISTICS <TABLE_NAME>` may not be ideal - especially for wide tables with lots of statistics objects.</span></span>

> [!NOTE]
> <span data-ttu-id="e99e1-181">Raadpleeg voor meer informatie over [sleutel oplopende] toohello SQL Server 2014 kardinaliteitsschatting model technisch document.</span><span class="sxs-lookup"><span data-stu-id="e99e1-181">For more details on [ascending key] please refer toohello SQL Server 2014 cardinality estimation model whitepaper.</span></span>
> 
> 

<span data-ttu-id="e99e1-182">Zie voor verdere uitleg [Kardinaliteitsschatting] [ Cardinality Estimation] op MSDN.</span><span class="sxs-lookup"><span data-stu-id="e99e1-182">For further explanation, see  [Cardinality Estimation][Cardinality Estimation] on MSDN.</span></span>

## <a name="examples-create-statistics"></a><span data-ttu-id="e99e1-183">Voorbeelden: Statistieken maken</span><span class="sxs-lookup"><span data-stu-id="e99e1-183">Examples: Create statistics</span></span>
<span data-ttu-id="e99e1-184">Deze voorbeelden laten zien hoe toouse verschillende opties voor het maken van statistieken.</span><span class="sxs-lookup"><span data-stu-id="e99e1-184">These examples show how toouse various options for creating statistics.</span></span> <span data-ttu-id="e99e1-185">Hallo-opties die u voor elke kolom gebruiken, is afhankelijk van Hallo kenmerken van uw gegevens en hoe Hallo-kolom worden gebruikt in query's.</span><span class="sxs-lookup"><span data-stu-id="e99e1-185">hello options that you use for each column depend on hello characteristics of your data and how hello column will be used in queries.</span></span>

### <a name="a-create-single-column-statistics-with-default-options"></a><span data-ttu-id="e99e1-186">A.</span><span class="sxs-lookup"><span data-stu-id="e99e1-186">A.</span></span> <span data-ttu-id="e99e1-187">Statistieken voor één kolom maken met de standaardopties</span><span class="sxs-lookup"><span data-stu-id="e99e1-187">Create single-column statistics with default options</span></span>
<span data-ttu-id="e99e1-188">statistieken voor een kolom toocreate verstrek een naam voor Hallo statistieken object en het Hallo-naam van Hallo kolom.</span><span class="sxs-lookup"><span data-stu-id="e99e1-188">toocreate statistics on a column, simply provide a name for hello statistics object and hello name of hello column.</span></span>

<span data-ttu-id="e99e1-189">Deze syntaxis gebruikt alle Hallo standaardopties te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e99e1-189">This syntax uses all of hello default options.</span></span> <span data-ttu-id="e99e1-190">Standaard wordt in SQL Data Warehouse 20 procent van de tabel Hallo voorbeelden bij het maken van statistieken.</span><span class="sxs-lookup"><span data-stu-id="e99e1-190">By default, SQL Data Warehouse samples 20 percent of hello table when it creates statistics.</span></span>

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]);
```

<span data-ttu-id="e99e1-191">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e99e1-191">For example:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1);
```

### <a name="b-create-single-column-statistics-by-examining-every-row"></a><span data-ttu-id="e99e1-192">B.</span><span class="sxs-lookup"><span data-stu-id="e99e1-192">B.</span></span> <span data-ttu-id="e99e1-193">Maken van statistieken voor één kolom aan de hand van elke rij</span><span class="sxs-lookup"><span data-stu-id="e99e1-193">Create single-column statistics by examining every row</span></span>
<span data-ttu-id="e99e1-194">Hallo standaard samplefrequentie van 20 procent is voldoende voor de meeste situaties.</span><span class="sxs-lookup"><span data-stu-id="e99e1-194">hello default sampling rate of 20 percent is sufficient for most situations.</span></span> <span data-ttu-id="e99e1-195">U kunt echter Hallo samplingfrequentie aanpassen.</span><span class="sxs-lookup"><span data-stu-id="e99e1-195">However, you can adjust hello sampling rate.</span></span>

<span data-ttu-id="e99e1-196">toosample hello volledige tabel, gebruik de volgende syntaxis:</span><span class="sxs-lookup"><span data-stu-id="e99e1-196">toosample hello full table, use this syntax:</span></span>

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]) WITH FULLSCAN;
```

<span data-ttu-id="e99e1-197">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e99e1-197">For example:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH FULLSCAN;
```

### <a name="c-create-single-column-statistics-by-specifying-hello-sample-size"></a><span data-ttu-id="e99e1-198">C.</span><span class="sxs-lookup"><span data-stu-id="e99e1-198">C.</span></span> <span data-ttu-id="e99e1-199">Statistieken voor één kolom maken door te geven van de grootte van de steekproef Hallo</span><span class="sxs-lookup"><span data-stu-id="e99e1-199">Create single-column statistics by specifying hello sample size</span></span>
<span data-ttu-id="e99e1-200">U kunt ook de samplegrootte Hallo opgeven als een percentage:</span><span class="sxs-lookup"><span data-stu-id="e99e1-200">Alternatively, you can specify hello sample size as a percent:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH SAMPLE = 50 PERCENT;
```

### <a name="d-create-single-column-statistics-on-only-some-of-hello-rows"></a><span data-ttu-id="e99e1-201">D.</span><span class="sxs-lookup"><span data-stu-id="e99e1-201">D.</span></span> <span data-ttu-id="e99e1-202">Maken van statistieken voor één kolom op slechts een deel van Hallo rijen</span><span class="sxs-lookup"><span data-stu-id="e99e1-202">Create single-column statistics on only some of hello rows</span></span>
<span data-ttu-id="e99e1-203">Een andere optie kunt u statistieken op een gedeelte van Hallo rijen in de tabel.</span><span class="sxs-lookup"><span data-stu-id="e99e1-203">Another option, you can create statistics on a portion of hello rows in your table.</span></span> <span data-ttu-id="e99e1-204">Dit is een gefilterde statistieken genoemd.</span><span class="sxs-lookup"><span data-stu-id="e99e1-204">This is called a filtered statistic.</span></span>

<span data-ttu-id="e99e1-205">U kunt gefilterde statistieken bijvoorbeeld bij het plannen van een specifieke partitie van een grote gepartitioneerde tabel tooquery.</span><span class="sxs-lookup"><span data-stu-id="e99e1-205">For example, you could use filtered statistics when you plan tooquery a specific partition of a large partitioned table.</span></span> <span data-ttu-id="e99e1-206">Door het maken van statistieken op alleen Hallo partitie waarden, nauwkeurigheid Hallo Hallo statistieken wordt te verbeteren, en daarom queryprestaties verbeteren.</span><span class="sxs-lookup"><span data-stu-id="e99e1-206">By creating statistics on only hello partition values, hello accuracy of hello statistics will improve, and therefore improve query performance.</span></span>

<span data-ttu-id="e99e1-207">In dit voorbeeld maakt statistieken op een bereik met waarden.</span><span class="sxs-lookup"><span data-stu-id="e99e1-207">This example creates statistics on a range of values.</span></span> <span data-ttu-id="e99e1-208">Hallo-waarden kunnen eenvoudig worden gedefinieerd toomatch Hallo bereik van waarden in een partitie.</span><span class="sxs-lookup"><span data-stu-id="e99e1-208">hello values could easily be defined toomatch hello range of values in a partition.</span></span>

```sql
CREATE STATISTICS stats_col1 ON table1(col1) WHERE col1 > '2000101' AND col1 < '20001231';
```

> [!NOTE]
> <span data-ttu-id="e99e1-209">Voor Hallo query optimaliseren tooconsider met gefilterde statistieken wanneer het Hallo gedistribueerde queryplan kiest, moet de Hallo query binnen Hallo definitie van Hallo statistieken object passen.</span><span class="sxs-lookup"><span data-stu-id="e99e1-209">For hello query optimizer tooconsider using filtered statistics when it chooses hello distributed query plan, hello query must fit inside hello definition of hello statistics object.</span></span> <span data-ttu-id="e99e1-210">Hallo vorige voorbeeld Hallo van de query waarin component toospecify col1 waarden tussen 2000101 en 20001231 moet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e99e1-210">Using hello previous example, hello query's where clause needs toospecify col1 values between 2000101 and 20001231.</span></span>
> 
> 

### <a name="e-create-single-column-statistics-with-all-hello-options"></a><span data-ttu-id="e99e1-211">E.</span><span class="sxs-lookup"><span data-stu-id="e99e1-211">E.</span></span> <span data-ttu-id="e99e1-212">Statistieken voor één kolom maken met alle Hallo-opties</span><span class="sxs-lookup"><span data-stu-id="e99e1-212">Create single-column statistics with all hello options</span></span>
<span data-ttu-id="e99e1-213">U kunt, natuurlijk Hallo opties samen combineren.</span><span class="sxs-lookup"><span data-stu-id="e99e1-213">You can, of course, combine hello options together.</span></span> <span data-ttu-id="e99e1-214">Hallo in het volgende voorbeeld wordt een gefilterde statistieken-object gemaakt met een aangepaste samplegrootte:</span><span class="sxs-lookup"><span data-stu-id="e99e1-214">hello example below creates a filtered statistics object with a custom sample size:</span></span>

```sql
CREATE STATISTICS stats_col1 ON table1 (col1) WHERE col1 > '2000101' AND col1 < '20001231' WITH SAMPLE = 50 PERCENT;
```

<span data-ttu-id="e99e1-215">Zie voor volledige naslaginformatie Hallo [CREATE STATISTICS] [ CREATE STATISTICS] op MSDN.</span><span class="sxs-lookup"><span data-stu-id="e99e1-215">For hello full reference, see [CREATE STATISTICS][CREATE STATISTICS] on MSDN.</span></span>

### <a name="f-create-multi-column-statistics"></a><span data-ttu-id="e99e1-216">F.</span><span class="sxs-lookup"><span data-stu-id="e99e1-216">F.</span></span> <span data-ttu-id="e99e1-217">Statistieken met meerdere kolommen maken</span><span class="sxs-lookup"><span data-stu-id="e99e1-217">Create multi-column statistics</span></span>
<span data-ttu-id="e99e1-218">toocreate een statistieken met meerdere kolommen gewoon gebruiken Hallo eerdere voorbeelden, maar meer kolommen opgeven.</span><span class="sxs-lookup"><span data-stu-id="e99e1-218">toocreate a multi-column statistics, simply use hello previous examples, but specify more columns.</span></span>

> [!NOTE]
> <span data-ttu-id="e99e1-219">Hallo histogram die wordt gebruikt tooestimate aantal rijen in het queryresultaat hello, is alleen beschikbaar voor de eerste kolom Hallo die worden vermeld in de objectdefinitie van Hallo statistieken.</span><span class="sxs-lookup"><span data-stu-id="e99e1-219">hello histogram, which is used tooestimate number of rows in hello query result, is only available for hello first column listed in hello statistics object definition.</span></span>
> 
> 

<span data-ttu-id="e99e1-220">In dit voorbeeld Hallo histogram is op *product\_categorie*.</span><span class="sxs-lookup"><span data-stu-id="e99e1-220">In this example, hello histogram is on *product\_category*.</span></span> <span data-ttu-id="e99e1-221">Statistieken voor cross-kolom worden berekend op *product\_categorie* en *product\_sub_c\ategory*:</span><span class="sxs-lookup"><span data-stu-id="e99e1-221">Cross-column statistics are calculated on *product\_category* and *product\_sub_c\ategory*:</span></span>

```sql
CREATE STATISTICS stats_2cols ON table1 (product_category, product_sub_category) WHERE product_category > '2000101' AND product_category < '20001231' WITH SAMPLE = 50 PERCENT;
```

<span data-ttu-id="e99e1-222">Omdat er een correlatie tussen *product\_categorie* en *product\_sub\_categorie*, een stat met meerdere kolommen kan nuttig zijn als deze kolommen zijn toegankelijk op Hallo hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="e99e1-222">Since there is a correlation between *product\_category* and *product\_sub\_category*, a multi-column stat can be useful if these columns are accessed at hello same time.</span></span>

### <a name="g-create-statistics-on-all-hello-columns-in-a-table"></a><span data-ttu-id="e99e1-223">G.</span><span class="sxs-lookup"><span data-stu-id="e99e1-223">G.</span></span> <span data-ttu-id="e99e1-224">Statistieken maken voor alle Hallo kolommen in een tabel</span><span class="sxs-lookup"><span data-stu-id="e99e1-224">Create statistics on all hello columns in a table</span></span>
<span data-ttu-id="e99e1-225">Eenzijdige toocreate statistieken is tooissues CREATE STATISTICS opdrachten na het Hallo-tabel maken.</span><span class="sxs-lookup"><span data-stu-id="e99e1-225">One way toocreate statistics is tooissues CREATE STATISTICS commands after creating hello table.</span></span>

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

### <a name="h-use-a-stored-procedure-toocreate-statistics-on-all-columns-in-a-database"></a><span data-ttu-id="e99e1-226">H.</span><span class="sxs-lookup"><span data-stu-id="e99e1-226">H.</span></span> <span data-ttu-id="e99e1-227">Een opgeslagen procedure toocreate statistieken voor alle kolommen in een database gebruiken</span><span class="sxs-lookup"><span data-stu-id="e99e1-227">Use a stored procedure toocreate statistics on all columns in a database</span></span>
<span data-ttu-id="e99e1-228">SQL Data Warehouse heeft geen een equivalent van de opgeslagen procedure systeem te [sp_create_stats] [] in SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e99e1-228">SQL Data Warehouse does not have a system stored procedure equivalent too[sp_create_stats][] in SQL Server.</span></span> <span data-ttu-id="e99e1-229">Deze opgeslagen procedure maakt een object van de statistieken één kolom voor elke kolom van het Hallo-database die nog geen statistieken.</span><span class="sxs-lookup"><span data-stu-id="e99e1-229">This stored procedure creates a single column statistics object on every column of hello database that doesn't already have statistics.</span></span>

<span data-ttu-id="e99e1-230">Dit helpt u aan de slag met het ontwerp van de database.</span><span class="sxs-lookup"><span data-stu-id="e99e1-230">This will help you get started with your database design.</span></span> <span data-ttu-id="e99e1-231">Gratis tooadapt van mening bent dat deze tooyour nodig heeft.</span><span class="sxs-lookup"><span data-stu-id="e99e1-231">Feel free tooadapt it tooyour needs.</span></span>

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

<span data-ttu-id="e99e1-232">statistieken voor alle kolommen in tabel met deze procedure Hallo toocreate aanroep gewoon Hallo procedure.</span><span class="sxs-lookup"><span data-stu-id="e99e1-232">toocreate statistics on all columns in hello table with this procedure, simply call hello procedure.</span></span>

```sql
prc_sqldw_create_stats;
```

## <a name="examples-update-statistics"></a><span data-ttu-id="e99e1-233">Voorbeelden: update statistics</span><span class="sxs-lookup"><span data-stu-id="e99e1-233">Examples: update statistics</span></span>
<span data-ttu-id="e99e1-234">statistieken over tooupdate, kunt u:</span><span class="sxs-lookup"><span data-stu-id="e99e1-234">tooupdate statistics, you can:</span></span>

1. <span data-ttu-id="e99e1-235">Een object van de statistieken worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="e99e1-235">Update one statistics object.</span></span> <span data-ttu-id="e99e1-236">Hallo-naam van Hallo statistieken object dat u tooupdate wilt opgeven.</span><span class="sxs-lookup"><span data-stu-id="e99e1-236">Specify hello name of hello statistics object you wish tooupdate.</span></span>
2. <span data-ttu-id="e99e1-237">Werk alle statistieken objecten in een tabel.</span><span class="sxs-lookup"><span data-stu-id="e99e1-237">Update all statistics objects on a table.</span></span> <span data-ttu-id="e99e1-238">Hallo-naam van het Hallo-tabel in plaats van één specifieke statistieken-object opgeven.</span><span class="sxs-lookup"><span data-stu-id="e99e1-238">Specify hello name of hello table instead of one specific statistics object.</span></span>

### <a name="a-update-one-specific-statistics-object"></a><span data-ttu-id="e99e1-239">A.</span><span class="sxs-lookup"><span data-stu-id="e99e1-239">A.</span></span> <span data-ttu-id="e99e1-240">Object voor een specifieke statistieken bijwerken</span><span class="sxs-lookup"><span data-stu-id="e99e1-240">Update one specific statistics object</span></span>
<span data-ttu-id="e99e1-241">Gebruik Hallo syntaxis tooupdate een specifieke statistieken-object te volgen:</span><span class="sxs-lookup"><span data-stu-id="e99e1-241">Use hello following syntax tooupdate a specific statistics object:</span></span>

```sql
UPDATE STATISTICS [schema_name].[table_name]([stat_name]);
```

<span data-ttu-id="e99e1-242">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e99e1-242">For example:</span></span>

```sql
UPDATE STATISTICS [dbo].[table1] ([stats_col1]);
```

<span data-ttu-id="e99e1-243">Door het bijwerken van statistieken voor specifieke objecten, kunt u statistieken voor Hallo tijd en hulpbronnen vereist toomanage minimaliseren.</span><span class="sxs-lookup"><span data-stu-id="e99e1-243">By updating specific statistics objects, you can minimize hello time and resources required toomanage statistics.</span></span> <span data-ttu-id="e99e1-244">Hiervoor moet dat een aantal beschouwd, echter toochoose Hallo best statistieken objecten tooupdate.</span><span class="sxs-lookup"><span data-stu-id="e99e1-244">This requires some thought, though, toochoose hello best statistics objects tooupdate.</span></span>

### <a name="b-update-all-statistics-on-a-table"></a><span data-ttu-id="e99e1-245">B.</span><span class="sxs-lookup"><span data-stu-id="e99e1-245">B.</span></span> <span data-ttu-id="e99e1-246">Bijwerken van alle statistische gegevens in een tabel</span><span class="sxs-lookup"><span data-stu-id="e99e1-246">Update all statistics on a table</span></span>
<span data-ttu-id="e99e1-247">Hier wordt een eenvoudige methode voor het bijwerken van alle Hallo statistieken objecten in een tabel.</span><span class="sxs-lookup"><span data-stu-id="e99e1-247">This shows a simple method for updating all hello statistics objects on a table.</span></span>

```sql
UPDATE STATISTICS [schema_name].[table_name];
```

<span data-ttu-id="e99e1-248">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e99e1-248">For example:</span></span>

```sql
UPDATE STATISTICS dbo.table1;
```

<span data-ttu-id="e99e1-249">Deze instructie is eenvoudig toouse.</span><span class="sxs-lookup"><span data-stu-id="e99e1-249">This statement is easy toouse.</span></span> <span data-ttu-id="e99e1-250">Vergeet niet dit alle statistische gegevens op tabel Hallo-updates en meer werk dan noodzakelijk is daarom mogelijk uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="e99e1-250">Just remember this updates all statistics on hello table, and therefore might perform more work than is necessary.</span></span> <span data-ttu-id="e99e1-251">Als geen Hallo prestaties een probleem is, is dit zeker Hallo eenvoudigste en meest volledige manier tooguarantee statistieken bijgewerkt zijn.</span><span class="sxs-lookup"><span data-stu-id="e99e1-251">If hello performance is not an issue, this is definitely hello easiest and most complete way tooguarantee statistics are up-to-date.</span></span>

> [!NOTE]
> <span data-ttu-id="e99e1-252">Wanneer alle statistische gegevens in een tabel wordt bijgewerkt, wordt in SQL Data Warehouse scan toosample Hallo table voor elke statistieken bevat.</span><span class="sxs-lookup"><span data-stu-id="e99e1-252">When updating all statistics on a table, SQL Data Warehouse does a scan toosample hello table for each statistics.</span></span> <span data-ttu-id="e99e1-253">Als de tabel Hallo groot is, kan heeft veel kolommen en veel statistieken, dat efficiënter tooupdate afzonderlijke statistieken op basis van behoeften.</span><span class="sxs-lookup"><span data-stu-id="e99e1-253">If hello table is large, has many columns, and many statistics, it might be more efficient tooupdate individual statistics based on need.</span></span>
> 
> 

<span data-ttu-id="e99e1-254">Voor een implementatie van een `UPDATE STATISTICS` procedure Zie Hallo [tijdelijke tabellen] [ Temporary] artikel.</span><span class="sxs-lookup"><span data-stu-id="e99e1-254">For an implementation of an `UPDATE STATISTICS` procedure please see hello [Temporary Tables][Temporary] article.</span></span> <span data-ttu-id="e99e1-255">Hallo implementatie methode is iets anders toohello `CREATE STATISTICS` bovenstaande procedure maar Hallo eindresultaat is dezelfde Hallo.</span><span class="sxs-lookup"><span data-stu-id="e99e1-255">hello implementation method is slightly different toohello `CREATE STATISTICS` procedure above but hello end result is hello same.</span></span>

<span data-ttu-id="e99e1-256">Zie voor de volledige syntaxis hello, [Update Statistics] [ Update Statistics] op MSDN.</span><span class="sxs-lookup"><span data-stu-id="e99e1-256">For hello full syntax, see [Update Statistics][Update Statistics] on MSDN.</span></span>

## <a name="statistics-metadata"></a><span data-ttu-id="e99e1-257">Statistieken metagegevens</span><span class="sxs-lookup"><span data-stu-id="e99e1-257">Statistics metadata</span></span>
<span data-ttu-id="e99e1-258">Er zijn verschillende systeemweergave en functies waarmee u informatie over statistieken toofind kunt.</span><span class="sxs-lookup"><span data-stu-id="e99e1-258">There are several system view and functions that you can use toofind information about statistics.</span></span> <span data-ttu-id="e99e1-259">U kunt bijvoorbeeld zien als een object statistieken mogelijk verouderd met behulp van Hallo statistieken datum functie toosee wanneer statistieken laatste zijn gemaakt of bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="e99e1-259">For example, you can see if a statistics object might be out-of-date by using hello stats-date function toosee when statistics were last created or updated.</span></span>

### <a name="catalog-views-for-statistics"></a><span data-ttu-id="e99e1-260">Catalogusweergaven voor statistieken</span><span class="sxs-lookup"><span data-stu-id="e99e1-260">Catalog views for statistics</span></span>
<span data-ttu-id="e99e1-261">Deze systeemweergaven bevatten informatie over statistieken:</span><span class="sxs-lookup"><span data-stu-id="e99e1-261">These system views provide information about statistics:</span></span>

| <span data-ttu-id="e99e1-262">Catalogusweergave</span><span class="sxs-lookup"><span data-stu-id="e99e1-262">Catalog View</span></span> | <span data-ttu-id="e99e1-263">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="e99e1-263">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="e99e1-264">[sys.Columns][sys.columns]</span><span class="sxs-lookup"><span data-stu-id="e99e1-264">[sys.columns][sys.columns]</span></span> |<span data-ttu-id="e99e1-265">Een rij voor elke kolom.</span><span class="sxs-lookup"><span data-stu-id="e99e1-265">One row for each column.</span></span> |
| <span data-ttu-id="e99e1-266">[sys.Objects][sys.objects]</span><span class="sxs-lookup"><span data-stu-id="e99e1-266">[sys.objects][sys.objects]</span></span> |<span data-ttu-id="e99e1-267">Een rij voor elk object in het Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="e99e1-267">One row for each object in hello database.</span></span> |
| <span data-ttu-id="e99e1-268">[sys.schemas][sys.schemas]</span><span class="sxs-lookup"><span data-stu-id="e99e1-268">[sys.schemas][sys.schemas]</span></span> |<span data-ttu-id="e99e1-269">Een rij voor elk schema in Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="e99e1-269">One row for each schema in hello database.</span></span> |
| <span data-ttu-id="e99e1-270">[sys.Stats][sys.stats]</span><span class="sxs-lookup"><span data-stu-id="e99e1-270">[sys.stats][sys.stats]</span></span> |<span data-ttu-id="e99e1-271">Een rij voor elk object statistieken.</span><span class="sxs-lookup"><span data-stu-id="e99e1-271">One row for each statistics object.</span></span> |
| <span data-ttu-id="e99e1-272">[sys.stats_columns][sys.stats_columns]</span><span class="sxs-lookup"><span data-stu-id="e99e1-272">[sys.stats_columns][sys.stats_columns]</span></span> |<span data-ttu-id="e99e1-273">Een rij voor elke kolom in Hallo statistieken object.</span><span class="sxs-lookup"><span data-stu-id="e99e1-273">One row for each column in hello statistics object.</span></span> <span data-ttu-id="e99e1-274">Teruggekoppeld toosys.columns.</span><span class="sxs-lookup"><span data-stu-id="e99e1-274">Links back toosys.columns.</span></span> |
| <span data-ttu-id="e99e1-275">[sys.Tables][sys.tables]</span><span class="sxs-lookup"><span data-stu-id="e99e1-275">[sys.tables][sys.tables]</span></span> |<span data-ttu-id="e99e1-276">Een rij voor elke tabel (inclusief externe tabellen).</span><span class="sxs-lookup"><span data-stu-id="e99e1-276">One row for each table (includes external tables).</span></span> |
| <span data-ttu-id="e99e1-277">[sys.table_types][sys.table_types]</span><span class="sxs-lookup"><span data-stu-id="e99e1-277">[sys.table_types][sys.table_types]</span></span> |<span data-ttu-id="e99e1-278">Een rij voor elk gegevenstype.</span><span class="sxs-lookup"><span data-stu-id="e99e1-278">One row for each data type.</span></span> |

### <a name="system-functions-for-statistics"></a><span data-ttu-id="e99e1-279">Systeemfuncties voor statistieken</span><span class="sxs-lookup"><span data-stu-id="e99e1-279">System functions for statistics</span></span>
<span data-ttu-id="e99e1-280">Deze systeemfuncties zijn nuttig voor het werken met statistieken:</span><span class="sxs-lookup"><span data-stu-id="e99e1-280">These system functions are useful for working with statistics:</span></span>

| <span data-ttu-id="e99e1-281">De systeemfunctie</span><span class="sxs-lookup"><span data-stu-id="e99e1-281">System Function</span></span> | <span data-ttu-id="e99e1-282">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="e99e1-282">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="e99e1-283">[STATS_DATE][STATS_DATE]</span><span class="sxs-lookup"><span data-stu-id="e99e1-283">[STATS_DATE][STATS_DATE]</span></span> |<span data-ttu-id="e99e1-284">Datum Hallo statistieken object het laatst is bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="e99e1-284">Date hello statistics object was last updated.</span></span> |
| <span data-ttu-id="e99e1-285">[DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS]</span><span class="sxs-lookup"><span data-stu-id="e99e1-285">[DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS]</span></span> |<span data-ttu-id="e99e1-286">Samenvatting niveau en gedetailleerde informatie over de distributie van de waarden Hallo biedt begrepen door Hallo statistieken object.</span><span class="sxs-lookup"><span data-stu-id="e99e1-286">Provides summary level and detailed information about hello distribution of values as understood by hello statistics object.</span></span> |

### <a name="combine-statistics-columns-and-functions-into-one-view"></a><span data-ttu-id="e99e1-287">Functies en statistieken kolommen combineren in één weergave</span><span class="sxs-lookup"><span data-stu-id="e99e1-287">Combine statistics columns and functions into one view</span></span>
<span data-ttu-id="e99e1-288">Deze weergave worden de kolommen die betrekking toostatistics en de resultaten van Hallo [STATS_DATE()] [] functie samen hebben.</span><span class="sxs-lookup"><span data-stu-id="e99e1-288">This view brings columns that relate toostatistics, and results from hello [STATS_DATE()][]function together.</span></span>

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

## <a name="dbcc-showstatistics-examples"></a><span data-ttu-id="e99e1-289">DBCC SHOW_STATISTICS()-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="e99e1-289">DBCC SHOW_STATISTICS() examples</span></span>
<span data-ttu-id="e99e1-290">DBCC SHOW_STATISTICS() toont Hallo-gegevens die zijn opgeslagen in een object van statistieken.</span><span class="sxs-lookup"><span data-stu-id="e99e1-290">DBCC SHOW_STATISTICS() shows hello data held within a statistics object.</span></span> <span data-ttu-id="e99e1-291">Deze gegevens zijn afkomstig uit drie delen.</span><span class="sxs-lookup"><span data-stu-id="e99e1-291">This data comes in three parts.</span></span>

1. <span data-ttu-id="e99e1-292">Koptekst</span><span class="sxs-lookup"><span data-stu-id="e99e1-292">Header</span></span>
2. <span data-ttu-id="e99e1-293">Dichtheid Vector</span><span class="sxs-lookup"><span data-stu-id="e99e1-293">Density Vector</span></span>
3. <span data-ttu-id="e99e1-294">Histogram</span><span class="sxs-lookup"><span data-stu-id="e99e1-294">Histogram</span></span>

<span data-ttu-id="e99e1-295">Hallo-header metagegevens over Hallo statistieken.</span><span class="sxs-lookup"><span data-stu-id="e99e1-295">hello header metadata about hello statistics.</span></span> <span data-ttu-id="e99e1-296">Hallo histogram geeft Hallo distributie van de waarden in Hallo eerste sleutelkolom van Hallo statistieken object.</span><span class="sxs-lookup"><span data-stu-id="e99e1-296">hello histogram displays hello distribution of values in hello first key column of hello statistics object.</span></span> <span data-ttu-id="e99e1-297">Hallo dichtheid vector metingen cross-kolom correlatie.</span><span class="sxs-lookup"><span data-stu-id="e99e1-297">hello density vector measures cross-column correlation.</span></span> <span data-ttu-id="e99e1-298">SQLDW berekent kardinaliteit maakt een schatting met Hallo-gegevens in Hallo statistieken-object.</span><span class="sxs-lookup"><span data-stu-id="e99e1-298">SQLDW computes cardinality estimates with any of hello data in hello statistics object.</span></span>

### <a name="show-header-density-and-histogram"></a><span data-ttu-id="e99e1-299">Koptekst, dichtheid en histogram weergeven</span><span class="sxs-lookup"><span data-stu-id="e99e1-299">Show header, density, and histogram</span></span>
<span data-ttu-id="e99e1-300">Dit eenvoudige voorbeeld toont alle drie onderdelen van een object statistieken.</span><span class="sxs-lookup"><span data-stu-id="e99e1-300">This simple example shows all three parts of a statistics object.</span></span>

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>)
```

<span data-ttu-id="e99e1-301">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e99e1-301">For example:</span></span>

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1);
```

### <a name="show-one-or-more-parts-of-dbcc-showstatistics"></a><span data-ttu-id="e99e1-302">Een of meer onderdelen van DBCC SHOW_STATISTICS(); weergeven</span><span class="sxs-lookup"><span data-stu-id="e99e1-302">Show one or more parts of DBCC SHOW_STATISTICS();</span></span>
<span data-ttu-id="e99e1-303">Als u alleen geïnteresseerd bent in specifieke onderdelen weer te geven, gebruikt u Hallo `WITH` component en geef op welke onderdelen u wilt dat toosee:</span><span class="sxs-lookup"><span data-stu-id="e99e1-303">If you are only interested in viewing specific parts, use hello `WITH` clause and specify which parts you want toosee:</span></span>

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>) WITH stat_header, histogram, density_vector
```

<span data-ttu-id="e99e1-304">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e99e1-304">For example:</span></span>

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1) WITH histogram, density_vector
```

## <a name="dbcc-showstatistics-differences"></a><span data-ttu-id="e99e1-305">DBCC SHOW_STATISTICS() verschillen</span><span class="sxs-lookup"><span data-stu-id="e99e1-305">DBCC SHOW_STATISTICS() differences</span></span>
<span data-ttu-id="e99e1-306">DBCC SHOW_STATISTICS() is meer strikt in SQL Data Warehouse vergeleken tooSQL Server geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="e99e1-306">DBCC SHOW_STATISTICS() is more strictly implemented in SQL Data Warehouse compared tooSQL Server.</span></span>

1. <span data-ttu-id="e99e1-307">Niet-gedocumenteerde functies worden niet ondersteund</span><span class="sxs-lookup"><span data-stu-id="e99e1-307">Undocumented features are not supported</span></span>
2. <span data-ttu-id="e99e1-308">Stats_stream kan niet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e99e1-308">Cannot use Stats_stream</span></span>
3. <span data-ttu-id="e99e1-309">Resultaten voor specifieke subreeksen van statistische gegevens bijvoorbeeld niet koppelen (STAT_HEADER JOIN DENSITY_VECTOR)</span><span class="sxs-lookup"><span data-stu-id="e99e1-309">Cannot join results for specific subsets of statistics data e.g. (STAT_HEADER JOIN DENSITY_VECTOR)</span></span>
4. <span data-ttu-id="e99e1-310">NO_INFOMSGS kan niet worden ingesteld voor bericht onderdrukken</span><span class="sxs-lookup"><span data-stu-id="e99e1-310">NO_INFOMSGS cannot be set for message suppression</span></span>
5. <span data-ttu-id="e99e1-311">Vierkante haken om de namen van statistieken kan niet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e99e1-311">Square brackets around statistics names cannot be used</span></span>
6. <span data-ttu-id="e99e1-312">Kolom namen tooidentify statistieken objecten kan niet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e99e1-312">Cannot use column names tooidentify statistics objects</span></span>
7. <span data-ttu-id="e99e1-313">Aangepaste fout 2767 wordt niet ondersteund</span><span class="sxs-lookup"><span data-stu-id="e99e1-313">Custom error 2767 is not supported</span></span>

## <a name="next-steps"></a><span data-ttu-id="e99e1-314">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e99e1-314">Next steps</span></span>
<span data-ttu-id="e99e1-315">Zie voor meer informatie [DBCC SHOW_STATISTICS] [ DBCC SHOW_STATISTICS] op MSDN.</span><span class="sxs-lookup"><span data-stu-id="e99e1-315">For more details, see [DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS] on MSDN.</span></span>  <span data-ttu-id="e99e1-316">toolearn Zie meer Hallo artikelen op [tabel overzicht][Overview], [tabel gegevenstypen][Data Types], [distribueren van een tabel] [ Distribute], [Indexeren van een tabel][Index], [partitioneren van een tabel] [ Partition] en [ Tijdelijke tabellen][Temporary].</span><span class="sxs-lookup"><span data-stu-id="e99e1-316">toolearn more, see hello articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="e99e1-317">Zie voor meer informatie over best practices [aanbevolen procedures van SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="e99e1-317">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>  

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
