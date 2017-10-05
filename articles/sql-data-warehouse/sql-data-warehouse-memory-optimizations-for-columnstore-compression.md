---
title: Columnstore-index de prestaties verbeteren in Azure SQL | Microsoft Docs
description: Verminder de geheugenvereisten of vergroot de hoeveelheid beschikbaar geheugen om het aantal rijen comprimeren van een columnstore-index in elke rijgroep maximaliseren.
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: ef170f39-ae24-4b04-af76-53bb4c4d16d3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 6/2/2017
ms.author: shigu;barbkess
ms.openlocfilehash: f0e0b839b4a0c216eee2eb5134d43b91d8f83289
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="maximizing-rowgroup-quality-for-columnstore"></a><span data-ttu-id="7e042-103">Het optimaliseren van rijgroep kwaliteit voor columnstore</span><span class="sxs-lookup"><span data-stu-id="7e042-103">Maximizing rowgroup quality for columnstore</span></span>

<span data-ttu-id="7e042-104">Rijgroep kwaliteit wordt bepaald door het aantal rijen in een rijgroep.</span><span class="sxs-lookup"><span data-stu-id="7e042-104">Rowgroup quality is determined by the number of rows in a rowgroup.</span></span> <span data-ttu-id="7e042-105">Verminder de geheugenvereisten of vergroot de hoeveelheid beschikbaar geheugen om het aantal rijen comprimeren van een columnstore-index in elke rijgroep maximaliseren.</span><span class="sxs-lookup"><span data-stu-id="7e042-105">Reduce memory requirements or increase the available memory to maximize the number of rows a columnstore index compresses into each rowgroup.</span></span>  <span data-ttu-id="7e042-106">Deze methoden gebruiken compressie tarieven verbeteren en prestaties voor columnstore-indexen opvragen.</span><span class="sxs-lookup"><span data-stu-id="7e042-106">Use these methods to improve compression rates and query performance for columnstore indexes.</span></span>

## <a name="why-the-rowgroup-size-matters"></a><span data-ttu-id="7e042-107">Waarom de rijgroep-grootte van belang is</span><span class="sxs-lookup"><span data-stu-id="7e042-107">Why the rowgroup size matters</span></span>
<span data-ttu-id="7e042-108">Omdat een columnstore-index een tabel scant door kolomsegmenten van afzonderlijke rowgroups scannen, verbetert het optimaliseren van het aantal rijen in elke rijgroep de prestaties van query's.</span><span class="sxs-lookup"><span data-stu-id="7e042-108">Since a columnstore index scans a table by scanning column segments of individual rowgroups, maximizing the number of rows in each rowgroup enhances query performance.</span></span> <span data-ttu-id="7e042-109">Wanneer rowgroups hebt een groot aantal rijen, verbetert wat betekent dat er minder gegevens te lezen van de schijf is gegevenscompressie de.</span><span class="sxs-lookup"><span data-stu-id="7e042-109">When rowgroups have a high number of rows, data compression improves which means there is less data to read from disk.</span></span>

<span data-ttu-id="7e042-110">Zie voor meer informatie over rowgroups [Columnstore-indexen handleiding](https://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="7e042-110">For more information about rowgroups, see [Columnstore Indexes Guide](https://msdn.microsoft.com/library/gg492088.aspx).</span></span>

## <a name="target-size-for-rowgroups"></a><span data-ttu-id="7e042-111">Doelgrootte voor rowgroups</span><span class="sxs-lookup"><span data-stu-id="7e042-111">Target size for rowgroups</span></span>
<span data-ttu-id="7e042-112">Voor optimale queryprestaties is het doel om te maximaliseren van het aantal rijen per rijgroep in een columnstore-index.</span><span class="sxs-lookup"><span data-stu-id="7e042-112">For best query performance, the goal is to maximize the number of rows per rowgroup in a columnstore index.</span></span> <span data-ttu-id="7e042-113">Een rijgroep kan een maximum van 1.048.576 rijen hebben.</span><span class="sxs-lookup"><span data-stu-id="7e042-113">A rowgroup can have a maximum of 1,048,576 rows.</span></span> <span data-ttu-id="7e042-114">Dit klopt niet het maximum aantal rijen per rijgroep hebben.</span><span class="sxs-lookup"><span data-stu-id="7e042-114">It's okay to not have the maximum number of rows per rowgroup.</span></span> <span data-ttu-id="7e042-115">Columnstore-indexen bereiken van goede prestaties wanneer rowgroups ten minste 100.000 rijen hebben.</span><span class="sxs-lookup"><span data-stu-id="7e042-115">Columnstore indexes achieve good performance when rowgroups have at least 100,000 rows.</span></span>

## <a name="rowgroups-can-get-trimmed-during-compression"></a><span data-ttu-id="7e042-116">Rowgroups kunt ophalen afgekapte tijdens compressie</span><span class="sxs-lookup"><span data-stu-id="7e042-116">Rowgroups can get trimmed during compression</span></span>

<span data-ttu-id="7e042-117">Tijdens het bulksgewijs laden of columnstore-index opnieuw opbouwen is soms er onvoldoende geheugen beschikbaar is voor het comprimeren van de rijen die zijn aangewezen voor elke rijgroep.</span><span class="sxs-lookup"><span data-stu-id="7e042-117">During a bulk load or columnstore index rebuild, sometimes there isn't enough memory available to compress all the rows designated for each rowgroup.</span></span> <span data-ttu-id="7e042-118">Wanneer er geheugendruk, trim columnstore-indexen de grootten rijgroep compressie in de columnstore kan wel.</span><span class="sxs-lookup"><span data-stu-id="7e042-118">When there is memory pressure, columnstore indexes trim the rowgroup sizes so compression into the columnstore can succeed.</span></span> 

<span data-ttu-id="7e042-119">Wanneer er onvoldoende geheugen voor het comprimeren van minimaal 10.000 rijen in elke rijgroep, wordt er een fout gegenereerd in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="7e042-119">When there is insufficient memory to compress at least 10,000 rows into each rowgroup, SQL Data Warehouse generates an error.</span></span>

<span data-ttu-id="7e042-120">Zie voor meer informatie over bulksgewijs laden [bulksgewijs laden in een geclusterde columnstore-index](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).</span><span class="sxs-lookup"><span data-stu-id="7e042-120">For more information on bulk loading, see [Bulk load into a clustered columnstore index](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).</span></span>

## <a name="how-to-monitor-rowgroup-quality"></a><span data-ttu-id="7e042-121">Het bewaken van rijgroep kwaliteit</span><span class="sxs-lookup"><span data-stu-id="7e042-121">How to monitor rowgroup quality</span></span>

<span data-ttu-id="7e042-122">Er is een DMV (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats) die nuttige informatie zoals het aantal rijen in rowgroups en de reden voor bijsnijden als er was u beschikbaar maakt.</span><span class="sxs-lookup"><span data-stu-id="7e042-122">There is a DMV (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats) that exposes useful information such as number of rows in rowgroups and the reason for trimming if there was trimming.</span></span> <span data-ttu-id="7e042-123">U kunt de volgende weergave maken als een handige manier om op te vragen deze DMV om informatie over hoe rijgroep worden ingekort.</span><span class="sxs-lookup"><span data-stu-id="7e042-123">You can create the following view as a handy way to query this DMV to get information on rowgroup trimming.</span></span>

```sql
create view dbo.vCS_rg_physical_stats
as 
with cte
as
(
select   tb.[name]                    AS [logical_table_name]
,        rg.[row_group_id]            AS [row_group_id]
,        rg.[state]                   AS [state]
,        rg.[state_desc]              AS [state_desc]
,        rg.[total_rows]              AS [total_rows]
,        rg.[trim_reason_desc]        AS trim_reason_desc
,        mp.[physical_name]           AS physical_name
FROM    sys.[schemas] sm
JOIN    sys.[tables] tb               ON  sm.[schema_id]          = tb.[schema_id]                             
JOIN    sys.[pdw_table_mappings] mp   ON  tb.[object_id]          = mp.[object_id]
JOIN    sys.[pdw_nodes_tables] nt     ON  nt.[name]               = mp.[physical_name]
JOIN    sys.[dm_pdw_nodes_db_column_store_row_group_physical_stats] rg      ON  rg.[object_id]     = nt.[object_id]
                                                                            AND rg.[pdw_node_id]   = nt.[pdw_node_id]
                                        AND rg.[distribution_id]    = nt.[distribution_id]                                          
)
select *
from cte;
```

<span data-ttu-id="7e042-124">De trim_reason_desc geeft aan of de rijgroep is verkleind (trim_reason_desc = NO_TRIM impliceert er is geen inkorten en rijgroep van optimale kwaliteit is).</span><span class="sxs-lookup"><span data-stu-id="7e042-124">The trim_reason_desc tells whether the rowgroup was trimmed(trim_reason_desc = NO_TRIM implies there was no trimming and row group is of optimal quality).</span></span> <span data-ttu-id="7e042-125">De volgende redenen voor het vrijmaken van opslagruimte voortijdige worden ingekort door de rijgroep aangeven:</span><span class="sxs-lookup"><span data-stu-id="7e042-125">The following trim reasons indicate premature trimming of the rowgroup:</span></span>
- <span data-ttu-id="7e042-126">BULKLOAD: Deze trim reden wordt gebruikt wanneer de binnenkomende batch rijen voor de belasting van minder dan 1 miljoen rijen heeft.</span><span class="sxs-lookup"><span data-stu-id="7e042-126">BULKLOAD: This trim reason is used when the incoming batch of rows for the load had less than 1 million rows.</span></span> <span data-ttu-id="7e042-127">De engine voor het gecomprimeerde Rijgroepen maakt als er meer dan 100.000 rijen worden ingevoegd (in plaats van in het archief delta invoegen), maar stelt de beperkende reden op BULKLOAD.</span><span class="sxs-lookup"><span data-stu-id="7e042-127">The engine will create compressed row groups if there are greater than 100,000 rows being inserted (as opposed to inserting into the delta store) but sets the trim reason to BULKLOAD.</span></span> <span data-ttu-id="7e042-128">In dit scenario kunt u uw venster voor het laden van batch opzij meer rijen verhogen.</span><span class="sxs-lookup"><span data-stu-id="7e042-128">In this scenario, consider increasing your batch load window to accumulate more rows.</span></span> <span data-ttu-id="7e042-129">Herzie ook uw partitieschema om te controleren of dat het is niet te gedetailleerde zoals Rijgroepen niet meerdere grenzen van partities omvatten.</span><span class="sxs-lookup"><span data-stu-id="7e042-129">Also, reevaluate your partitioning scheme to ensure it is not too granular as row groups cannot span partition boundaries.</span></span>
- <span data-ttu-id="7e042-130">MEMORY_LIMITATION: Rijgroepen maakt met 1 miljoen rijen, een bepaalde hoeveelheid werkende geheugen is vereist door de engine.</span><span class="sxs-lookup"><span data-stu-id="7e042-130">MEMORY_LIMITATION: To create row groups with 1 million rows, a certain amount of working memory is required by the engine.</span></span> <span data-ttu-id="7e042-131">Wanneer het beschikbare geheugen van de sessie laden kleiner is dan het vereiste werkende geheugen, krijgen voortijdig Rijgroepen bijgesneden.</span><span class="sxs-lookup"><span data-stu-id="7e042-131">When available memory of the loading session is less than the required working memory, row groups get prematurely trimmed.</span></span> <span data-ttu-id="7e042-132">De volgende secties wordt uitgelegd hoe schatten geheugen vereist en meer geheugen toewijzen.</span><span class="sxs-lookup"><span data-stu-id="7e042-132">The following sections explain how to estimate memory required and allocate more memory.</span></span>
- <span data-ttu-id="7e042-133">DICTIONARY_SIZE: Voor deze trim reden geeft aan dat rijgroep bijsnijden omdat er ten minste één kolom met tekenreeksen met een hoge en/of hoge kardinaliteit tekenreeks is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="7e042-133">DICTIONARY_SIZE: This trim reason indicates that rowgroup trimming occurred because there was at least one string column with wide and/or high cardinality strings.</span></span> <span data-ttu-id="7e042-134">Grootte van de bibliotheek is beperkt tot 16 MB in het geheugen en als deze limiet is bereikt de rijgroep is gecomprimeerd.</span><span class="sxs-lookup"><span data-stu-id="7e042-134">The dictionary size is limited to 16 MB in memory and once this limit is reached the row group is compressed.</span></span> <span data-ttu-id="7e042-135">Als u in deze situatie uitvoert, kunt u overwegen de problematisch kolom in een afzonderlijke tabel isoleren.</span><span class="sxs-lookup"><span data-stu-id="7e042-135">If you do run into this situation, consider isolating the problematic column into a separate table.</span></span>

## <a name="how-to-estimate-memory-requirements"></a><span data-ttu-id="7e042-136">Hoe u schat geheugenvereisten</span><span class="sxs-lookup"><span data-stu-id="7e042-136">How to estimate memory requirements</span></span>

<!--
To view an estimate of the memory requirements to compress a rowgroup of maximum size into a columnstore index, download and run the view [dbo.vCS_mon_mem_grant](). This view shows the size of the memory grant that a rowgroup requires for compression in to the columnstore.
-->

<span data-ttu-id="7e042-137">De maximale hoeveelheid vereiste geheugen moeten worden gecomprimeerd één rijgroep is ongeveer</span><span class="sxs-lookup"><span data-stu-id="7e042-137">The maximum required memory to compress one rowgroup is approximately</span></span>

- <span data-ttu-id="7e042-138">72 MB +</span><span class="sxs-lookup"><span data-stu-id="7e042-138">72 MB +</span></span>
- <span data-ttu-id="7e042-139">\#rijen \* \#kolommen \* 8 bytes +</span><span class="sxs-lookup"><span data-stu-id="7e042-139">\#rows \* \#columns \* 8 bytes +</span></span>
- <span data-ttu-id="7e042-140">\#rijen \* \#korte tekenreekskolommen \* 32 bytes +</span><span class="sxs-lookup"><span data-stu-id="7e042-140">\#rows \* \#short-string-columns \* 32 bytes +</span></span>
- <span data-ttu-id="7e042-141">\#lange tekenreekskolommen \* 16 MB voor compressiebibliotheek</span><span class="sxs-lookup"><span data-stu-id="7e042-141">\#long-string-columns \* 16 MB for compression dictionary</span></span>

<span data-ttu-id="7e042-142">waar korte tekenreekskolommen gebruiken voor de gegevenstypen string van < = 32 bytes en het gebruik van lange tekenreekskolommen tekenreeks gegevenstypen > 32 bytes.</span><span class="sxs-lookup"><span data-stu-id="7e042-142">where short-string-columns use string data types of <= 32 bytes and long-string-columns use string data types of > 32 bytes.</span></span>

<span data-ttu-id="7e042-143">Lange tekenreeksen zijn gecomprimeerd met een compressiemethode die is ontworpen voor het comprimeren van tekst.</span><span class="sxs-lookup"><span data-stu-id="7e042-143">Long strings are compressed with a compression method designed for compressing text.</span></span> <span data-ttu-id="7e042-144">Deze compressiemethode gebruikt een *woordenlijst* voor het opslaan van tekstpatronen.</span><span class="sxs-lookup"><span data-stu-id="7e042-144">This compression method uses a *dictionary* to store text patterns.</span></span> <span data-ttu-id="7e042-145">De maximale grootte van een woordenboek is 16 MB.</span><span class="sxs-lookup"><span data-stu-id="7e042-145">The maximum size of a dictionary is 16 MB.</span></span> <span data-ttu-id="7e042-146">Er is slechts één woordenlijst voor elke kolom lange tekenreeks in de rijgroep.</span><span class="sxs-lookup"><span data-stu-id="7e042-146">There is only one dictionary for each long string column in the rowgroup.</span></span>

<span data-ttu-id="7e042-147">Zie de video voor een gedetailleerdere beschrijving van de geheugenvereisten columnstore [Azure SQL Data Warehouse schalen: configuratie en richtlijnen](https://myignite.microsoft.com/videos/14822).</span><span class="sxs-lookup"><span data-stu-id="7e042-147">For an in-depth discussion of columnstore memory requirements, see the video [Azure SQL Data Warehouse scaling: configuration and guidance](https://myignite.microsoft.com/videos/14822).</span></span>

## <a name="ways-to-reduce-memory-requirements"></a><span data-ttu-id="7e042-148">Manieren om te verminderen geheugenvereisten</span><span class="sxs-lookup"><span data-stu-id="7e042-148">Ways to reduce memory requirements</span></span>

<span data-ttu-id="7e042-149">De volgende technieken gebruiken om te beperken van de geheugenvereisten voor rowgroups comprimeren en columnstore-indexen.</span><span class="sxs-lookup"><span data-stu-id="7e042-149">Use the following techniques to reduce the memory requirements for compressing rowgroups into columnstore indexes.</span></span>

### <a name="use-fewer-columns"></a><span data-ttu-id="7e042-150">Gebruik minder kolommen</span><span class="sxs-lookup"><span data-stu-id="7e042-150">Use fewer columns</span></span>
<span data-ttu-id="7e042-151">Ontwerp, indien mogelijk, de tabel met minder kolommen.</span><span class="sxs-lookup"><span data-stu-id="7e042-151">If possible, design the table with fewer columns.</span></span> <span data-ttu-id="7e042-152">Wanneer een rijgroep in de columnstore is gecomprimeerd, de columnstore-index elk kolomsegment afzonderlijk gecomprimeerd.</span><span class="sxs-lookup"><span data-stu-id="7e042-152">When a rowgroup is compressed into the columnstore, the columnstore index compresses each column segment separately.</span></span> <span data-ttu-id="7e042-153">Daarom is de geheugenvereisten voor het comprimeren van een rijgroep verhogen als het aantal kolommen toeneemt.</span><span class="sxs-lookup"><span data-stu-id="7e042-153">Therefore the memory requirements to compress a rowgroup increase as the number of columns increases.</span></span>


### <a name="use-fewer-string-columns"></a><span data-ttu-id="7e042-154">Gebruik minder tekenreekskolommen</span><span class="sxs-lookup"><span data-stu-id="7e042-154">Use fewer string columns</span></span>
<span data-ttu-id="7e042-155">Kolommen van de gegevenstypen string vereisen meer geheugen dan numerieke en datum-gegevenstypen.</span><span class="sxs-lookup"><span data-stu-id="7e042-155">Columns of string data types require more memory than numeric and date data types.</span></span> <span data-ttu-id="7e042-156">Overweeg om te beperken geheugenvereisten, tekenreekskolommen verwijderen uit feitentabellen en ze in kleinere dimensietabellen te plaatsen.</span><span class="sxs-lookup"><span data-stu-id="7e042-156">To reduce memory requirements, consider removing string columns from fact tables and putting them in smaller dimension tables.</span></span>

<span data-ttu-id="7e042-157">Extra geheugen nodig voor de compressie van de tekenreeks:</span><span class="sxs-lookup"><span data-stu-id="7e042-157">Additional memory requirements for string compression:</span></span>

- <span data-ttu-id="7e042-158">De gegevenstypen String maximaal 32 tekens kunnen 32 aanvullende bytes per waarde vereisen.</span><span class="sxs-lookup"><span data-stu-id="7e042-158">String data types up to 32 characters can require 32 additional bytes per value.</span></span>
- <span data-ttu-id="7e042-159">De gegevenstypen String met meer dan 32 tekens zijn gecomprimeerd met behulp van methoden van de woordenlijst.</span><span class="sxs-lookup"><span data-stu-id="7e042-159">String data types with more than 32 characters are compressed using dictionary methods.</span></span>  <span data-ttu-id="7e042-160">Elke kolom in de rijgroep kan maximaal 16 MB extra vereisen voor het bouwen van de woordenlijst.</span><span class="sxs-lookup"><span data-stu-id="7e042-160">Each column in the rowgroup can require up to an additional 16 MB to build the dictionary.</span></span>

### <a name="avoid-over-partitioning"></a><span data-ttu-id="7e042-161">Te veel partitioneren voorkomen</span><span class="sxs-lookup"><span data-stu-id="7e042-161">Avoid over-partitioning</span></span>

<span data-ttu-id="7e042-162">Columnstore-indexen maken een of meer rowgroups per partitie.</span><span class="sxs-lookup"><span data-stu-id="7e042-162">Columnstore indexes create one or more rowgroups per partition.</span></span> <span data-ttu-id="7e042-163">In SQL Data Warehouse groeit het aantal partities snel omdat de gegevens wordt gedistribueerd en elke distributie is gepartitioneerd.</span><span class="sxs-lookup"><span data-stu-id="7e042-163">In SQL Data Warehouse, the number of partitions grows quickly because the data is distributed and each distribution is partitioned.</span></span> <span data-ttu-id="7e042-164">Als de tabel te veel partities heeft, er mogelijk niet voldoende rijen voor het vervullen van de rowgroups.</span><span class="sxs-lookup"><span data-stu-id="7e042-164">If the table has too many partitions, there might not be enough rows to fill the rowgroups.</span></span> <span data-ttu-id="7e042-165">Het ontbreken van rijen maakt geen geheugendruk tijdens compressie, maar dit leidt tot rowgroups die de beste prestaties van de columnstore-query kan niet worden bereikt.</span><span class="sxs-lookup"><span data-stu-id="7e042-165">The lack of rows does not create memory pressure during compression, but it leads to rowgroups that do not achieve the best columnstore query performance.</span></span>

<span data-ttu-id="7e042-166">Een andere reden om te voorkomen dat te veel partitionering is er een geheugen overhead voor het laden van rijen in een columnstore-index in een gepartitioneerde tabel.</span><span class="sxs-lookup"><span data-stu-id="7e042-166">Another reason to avoid over-partitioning is there is a memory overhead for loading rows into a columnstore index on a partitioned table.</span></span> <span data-ttu-id="7e042-167">Tijdens een werklast kunnen veel partities ontvangen de binnenkomende rijen die in het geheugen worden bewaard totdat elke partitie onvoldoende rijen heeft moeten worden gecomprimeerd.</span><span class="sxs-lookup"><span data-stu-id="7e042-167">During a load, many partitions could receive the incoming rows, which are held in memory until each partition has enough rows to be compressed.</span></span> <span data-ttu-id="7e042-168">Aanvullende geheugendruk met te veel partities worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7e042-168">Having too many partitions creates additional memory pressure.</span></span>

### <a name="simplify-the-load-query"></a><span data-ttu-id="7e042-169">Vereenvoudig de query laden</span><span class="sxs-lookup"><span data-stu-id="7e042-169">Simplify the load query</span></span>

<span data-ttu-id="7e042-170">De database deelt de geheugentoekenning voor een query tussen de operators in de query.</span><span class="sxs-lookup"><span data-stu-id="7e042-170">The database shares the memory grant for a query among all the operators in the query.</span></span> <span data-ttu-id="7e042-171">Wanneer een query load complexe sorteerbewerkingen en joins heeft, wordt het geheugen dat beschikbaar is voor de compressie verlaagd.</span><span class="sxs-lookup"><span data-stu-id="7e042-171">When a load query has complex sorts and joins, the memory available for compression is reduced.</span></span>

<span data-ttu-id="7e042-172">Ontwerp van de load-query om zich te richten alleen voor het laden van de query.</span><span class="sxs-lookup"><span data-stu-id="7e042-172">Design the load query to focus only on loading the query.</span></span> <span data-ttu-id="7e042-173">Als u wilt de transformaties uitvoeren op de gegevens, los van de load-query uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="7e042-173">If you need to run transformations on the data, run them separate from the load query.</span></span> <span data-ttu-id="7e042-174">Bijvoorbeeld, fase van de gegevens in een tabel heap, de transformaties uitvoeren en vervolgens de faseringstabel in de columnstore-index te laden.</span><span class="sxs-lookup"><span data-stu-id="7e042-174">For example, stage the data in a heap table, run the transformations, and then load the staging table into the columnstore index.</span></span> <span data-ttu-id="7e042-175">U kunt ook de gegevens eerst laden en gebruik vervolgens de MPP-systeem om de gegevens te transformeren.</span><span class="sxs-lookup"><span data-stu-id="7e042-175">You can also load the data first and then use the MPP system to transform the data.</span></span>

### <a name="adjust-maxdop"></a><span data-ttu-id="7e042-176">MAXDOP aanpassen</span><span class="sxs-lookup"><span data-stu-id="7e042-176">Adjust MAXDOP</span></span>

<span data-ttu-id="7e042-177">Elk distributiepunt comprimeert rowgroups in de columnstore parallel wanneer er meer dan één CPU-kern beschikbaar per distributiepunt.</span><span class="sxs-lookup"><span data-stu-id="7e042-177">Each distribution compresses rowgroups into the columnstore in parallel when there is more than one CPU core available per distribution.</span></span> <span data-ttu-id="7e042-178">De parallelle uitvoering vereist extra geheugenbronnen, wat tot geheugendruk en rijgroep bijsnijden leiden kunnen.</span><span class="sxs-lookup"><span data-stu-id="7e042-178">The parallelism requires additional memory resources, which can lead to memory pressure and rowgroup trimming.</span></span>

<span data-ttu-id="7e042-179">Als u geheugendruk, kunt u de query MAXDOP hint om af te dwingen de laadbewerking worden uitgevoerd in seriële modus binnen elk distributiepunt.</span><span class="sxs-lookup"><span data-stu-id="7e042-179">To reduce memory pressure, you can use the MAXDOP query hint to force the load operation to run in serial mode within each distribution.</span></span>

```
CREATE TABLE MyFactSalesQuota
WITH (DISTRIBUTION = ROUND_ROBIN)
AS SELECT * FROM FactSalesQUota
OPTION (MAXDOP 1);
```

## <a name="ways-to-allocate-more-memory"></a><span data-ttu-id="7e042-180">Manieren om meer geheugen toewijzen</span><span class="sxs-lookup"><span data-stu-id="7e042-180">Ways to allocate more memory</span></span>

<span data-ttu-id="7e042-181">DWU-grootte en de resource gebruikersklasse samen bepalen hoeveel geheugen beschikbaar is voor de aanvraag voor een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="7e042-181">DWU size and the user resource class together determine how much memory is available for a user query.</span></span> <span data-ttu-id="7e042-182">Voor een verhoging van de geheugentoekenning voor een load-query kunt u Verhoog het aantal dwu's of vergroot de bronklasse.</span><span class="sxs-lookup"><span data-stu-id="7e042-182">To increase the memory grant for a load query, you can either increase the number of DWUs or increase the resource class.</span></span>

- <span data-ttu-id="7e042-183">Zie voor een verhoging van het aantal dwu's [hoe schalen prestaties?](sql-data-warehouse-manage-compute-overview.md#scale-compute)</span><span class="sxs-lookup"><span data-stu-id="7e042-183">To increase the DWUs, see [How do I scale performance?](sql-data-warehouse-manage-compute-overview.md#scale-compute)</span></span>
- <span data-ttu-id="7e042-184">Zie het wijzigen van de bronklasse voor een query [wijzigen van een voorbeeld van een gebruiker resource klasse](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="7e042-184">To change the resource class for a query, see [Change a user resource class example](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>

<span data-ttu-id="7e042-185">Bijvoorbeeld op DWU 100 kunt een gebruiker in de bronklasse smallrc 100 MB aan geheugen voor elk distributiepunt.</span><span class="sxs-lookup"><span data-stu-id="7e042-185">For example, on DWU 100 a user in the smallrc resource class can use 100 MB of memory for each distribution.</span></span> <span data-ttu-id="7e042-186">Zie voor meer informatie, [gelijktijdigheid in SQL Data Warehouse](sql-data-warehouse-develop-concurrency.md).</span><span class="sxs-lookup"><span data-stu-id="7e042-186">For the details, see [Concurrency in SQL Data Warehouse](sql-data-warehouse-develop-concurrency.md).</span></span>

<span data-ttu-id="7e042-187">Stel dat u vastgesteld dat er 700 MB geheugen voor het ophalen van hoge kwaliteit rijgroep grootten.</span><span class="sxs-lookup"><span data-stu-id="7e042-187">Suppose you determine that you need 700 MB of memory to get high-quality rowgroup sizes.</span></span> <span data-ttu-id="7e042-188">Deze voorbeelden laten zien hoe u de load-query kunt uitvoeren met onvoldoende geheugen.</span><span class="sxs-lookup"><span data-stu-id="7e042-188">These examples show how you can run the load query with enough memory.</span></span>

- <span data-ttu-id="7e042-189">DWU-1000 en mediumrc gebruikt, is uw geheugentoekenning 800 MB</span><span class="sxs-lookup"><span data-stu-id="7e042-189">Using DWU 1000 and mediumrc, your memory grant is 800 MB</span></span>
- <span data-ttu-id="7e042-190">DWU 600 en largerc gebruikt, is uw geheugentoekenning 800 MB.</span><span class="sxs-lookup"><span data-stu-id="7e042-190">Using DWU 600 and largerc, your memory grant is 800 MB.</span></span>


## <a name="next-steps"></a><span data-ttu-id="7e042-191">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7e042-191">Next steps</span></span>

<span data-ttu-id="7e042-192">Ga voor meer manieren om de prestaties verbeteren in SQL Data Warehouse, Zie de [prestatieoverzicht](sql-data-warehouse-overview-manage-user-queries.md).</span><span class="sxs-lookup"><span data-stu-id="7e042-192">To find more ways to improve performance in SQL Data Warehouse, see the [Performance overview](sql-data-warehouse-overview-manage-user-queries.md).</span></span>

<!--Image references-->

<!--Article references-->


<!--MSDN references-->

<!--Other Web references-->
