---
title: prestaties van aaaImprove columnstore-index in Azure SQL | Microsoft Docs
description: Verminder de geheugenvereisten of Hallo beschikbaar geheugen toomaximize Hallo aantal rijen comprimeren van een columnstore-index in elke rijgroep vergroot.
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
ms.openlocfilehash: 2c5a68435aa200236a2dc8538aa4638b52a59093
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="maximizing-rowgroup-quality-for-columnstore"></a><span data-ttu-id="58845-103">Het optimaliseren van rijgroep kwaliteit voor columnstore</span><span class="sxs-lookup"><span data-stu-id="58845-103">Maximizing rowgroup quality for columnstore</span></span>

<span data-ttu-id="58845-104">Rijgroep kwaliteit wordt bepaald door het aantal rijen in een rijgroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="58845-104">Rowgroup quality is determined by hello number of rows in a rowgroup.</span></span> <span data-ttu-id="58845-105">Verminder de geheugenvereisten of Hallo beschikbaar geheugen toomaximize Hallo aantal rijen comprimeren van een columnstore-index in elke rijgroep vergroot.</span><span class="sxs-lookup"><span data-stu-id="58845-105">Reduce memory requirements or increase hello available memory toomaximize hello number of rows a columnstore index compresses into each rowgroup.</span></span>  <span data-ttu-id="58845-106">Gebruik deze methoden tooimprove compressie tarieven en prestaties van query's voor columnstore-indexen.</span><span class="sxs-lookup"><span data-stu-id="58845-106">Use these methods tooimprove compression rates and query performance for columnstore indexes.</span></span>

## <a name="why-hello-rowgroup-size-matters"></a><span data-ttu-id="58845-107">Waarom Hallo rijgroep grootte van belang is</span><span class="sxs-lookup"><span data-stu-id="58845-107">Why hello rowgroup size matters</span></span>
<span data-ttu-id="58845-108">Omdat een columnstore-index een tabel scant door kolomsegmenten van afzonderlijke rowgroups scannen, verbetert het optimaliseren van het aantal rijen in elke rijgroep Hallo de queryprestaties.</span><span class="sxs-lookup"><span data-stu-id="58845-108">Since a columnstore index scans a table by scanning column segments of individual rowgroups, maximizing hello number of rows in each rowgroup enhances query performance.</span></span> <span data-ttu-id="58845-109">Wanneer rowgroups hebt een groot aantal rijen, verbetert wat betekent dat er minder tooread gegevens vanaf schijf is gegevenscompressie de.</span><span class="sxs-lookup"><span data-stu-id="58845-109">When rowgroups have a high number of rows, data compression improves which means there is less data tooread from disk.</span></span>

<span data-ttu-id="58845-110">Zie voor meer informatie over rowgroups [Columnstore-indexen handleiding](https://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="58845-110">For more information about rowgroups, see [Columnstore Indexes Guide](https://msdn.microsoft.com/library/gg492088.aspx).</span></span>

## <a name="target-size-for-rowgroups"></a><span data-ttu-id="58845-111">Doelgrootte voor rowgroups</span><span class="sxs-lookup"><span data-stu-id="58845-111">Target size for rowgroups</span></span>
<span data-ttu-id="58845-112">Hallo-doel is voor de beste queryprestaties toomaximize Hallo aantal rijen per rijgroep in een columnstore-index.</span><span class="sxs-lookup"><span data-stu-id="58845-112">For best query performance, hello goal is toomaximize hello number of rows per rowgroup in a columnstore index.</span></span> <span data-ttu-id="58845-113">Een rijgroep kan een maximum van 1.048.576 rijen hebben.</span><span class="sxs-lookup"><span data-stu-id="58845-113">A rowgroup can have a maximum of 1,048,576 rows.</span></span> <span data-ttu-id="58845-114">De orde toonot Hallo kunt u het maximale aantal rijen per rijgroep hebben.</span><span class="sxs-lookup"><span data-stu-id="58845-114">It's okay toonot have hello maximum number of rows per rowgroup.</span></span> <span data-ttu-id="58845-115">Columnstore-indexen bereiken van goede prestaties wanneer rowgroups ten minste 100.000 rijen hebben.</span><span class="sxs-lookup"><span data-stu-id="58845-115">Columnstore indexes achieve good performance when rowgroups have at least 100,000 rows.</span></span>

## <a name="rowgroups-can-get-trimmed-during-compression"></a><span data-ttu-id="58845-116">Rowgroups kunt ophalen afgekapte tijdens compressie</span><span class="sxs-lookup"><span data-stu-id="58845-116">Rowgroups can get trimmed during compression</span></span>

<span data-ttu-id="58845-117">Tijdens het bulksgewijs laden of columnstore-index opnieuw opbouwen, soms er niet voldoende geheugen beschikbaar toocompress die alle rijen die zijn aangewezen voor elke rijgroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="58845-117">During a bulk load or columnstore index rebuild, sometimes there isn't enough memory available toocompress all hello rows designated for each rowgroup.</span></span> <span data-ttu-id="58845-118">Wanneer er geheugendruk, trim columnstore-indexen Hallo rijgroep grootten compressie in Hallo columnstore kan wel.</span><span class="sxs-lookup"><span data-stu-id="58845-118">When there is memory pressure, columnstore indexes trim hello rowgroup sizes so compression into hello columnstore can succeed.</span></span> 

<span data-ttu-id="58845-119">Wanneer er onvoldoende geheugen toocompress minimaal 10.000 rijen in elke rijgroep, wordt er een fout gegenereerd in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="58845-119">When there is insufficient memory toocompress at least 10,000 rows into each rowgroup, SQL Data Warehouse generates an error.</span></span>

<span data-ttu-id="58845-120">Zie voor meer informatie over bulksgewijs laden [bulksgewijs laden in een geclusterde columnstore-index](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).</span><span class="sxs-lookup"><span data-stu-id="58845-120">For more information on bulk loading, see [Bulk load into a clustered columnstore index](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).</span></span>

## <a name="how-toomonitor-rowgroup-quality"></a><span data-ttu-id="58845-121">Hoe toomonitor rijgroep kwaliteit</span><span class="sxs-lookup"><span data-stu-id="58845-121">How toomonitor rowgroup quality</span></span>

<span data-ttu-id="58845-122">Er is een DMV (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats) die nuttige informatie zoals het aantal rijen in rowgroups en Hallo reden voor bijsnijden beschikbaar worden gesteld als er was u.</span><span class="sxs-lookup"><span data-stu-id="58845-122">There is a DMV (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats) that exposes useful information such as number of rows in rowgroups and hello reason for trimming if there was trimming.</span></span> <span data-ttu-id="58845-123">U kunt de volgende weergave als een handige manier tooquery Hallo deze DMV tooget informatie maken op rijgroep bijsnijden.</span><span class="sxs-lookup"><span data-stu-id="58845-123">You can create hello following view as a handy way tooquery this DMV tooget information on rowgroup trimming.</span></span>

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

<span data-ttu-id="58845-124">Hallo trim_reason_desc vertelt of Hallo rijgroep is verkleind (trim_reason_desc = NO_TRIM impliceert er is geen inkorten en rijgroep van optimale kwaliteit is).</span><span class="sxs-lookup"><span data-stu-id="58845-124">hello trim_reason_desc tells whether hello rowgroup was trimmed(trim_reason_desc = NO_TRIM implies there was no trimming and row group is of optimal quality).</span></span> <span data-ttu-id="58845-125">Hallo vermeld trim oorzaken voortijdige worden ingekort door Hallo rijgroep:</span><span class="sxs-lookup"><span data-stu-id="58845-125">hello following trim reasons indicate premature trimming of hello rowgroup:</span></span>
- <span data-ttu-id="58845-126">BULKLOAD: Deze trim reden wordt gebruikt wanneer Hallo binnenkomende batch rijen voor Hallo load minder dan 1 miljoen rijen heeft.</span><span class="sxs-lookup"><span data-stu-id="58845-126">BULKLOAD: This trim reason is used when hello incoming batch of rows for hello load had less than 1 million rows.</span></span> <span data-ttu-id="58845-127">Hallo-engine maakt gecomprimeerde Rijgroepen als er zijn meer dan 100.000 rijen worden ingevoegd (als tegengestelde tooinserting in Hallo delta archief) maar sets Hallo trim reden tooBULKLOAD.</span><span class="sxs-lookup"><span data-stu-id="58845-127">hello engine will create compressed row groups if there are greater than 100,000 rows being inserted (as opposed tooinserting into hello delta store) but sets hello trim reason tooBULKLOAD.</span></span> <span data-ttu-id="58845-128">In dit scenario kunt u uw batch load venster tooaccumulate verhogen meer rijen.</span><span class="sxs-lookup"><span data-stu-id="58845-128">In this scenario, consider increasing your batch load window tooaccumulate more rows.</span></span> <span data-ttu-id="58845-129">Herzie ook uw partitionering schema tooensure is niet te gedetailleerde zoals Rijgroepen niet meerdere grenzen van partities omvatten.</span><span class="sxs-lookup"><span data-stu-id="58845-129">Also, reevaluate your partitioning scheme tooensure it is not too granular as row groups cannot span partition boundaries.</span></span>
- <span data-ttu-id="58845-130">MEMORY_LIMITATION: toocreate Rijgroepen met een bepaalde hoeveelheid werkende geheugen van 1 miljoen rijen is vereist door Hallo-engine.</span><span class="sxs-lookup"><span data-stu-id="58845-130">MEMORY_LIMITATION: toocreate row groups with 1 million rows, a certain amount of working memory is required by hello engine.</span></span> <span data-ttu-id="58845-131">Wanneer het beschikbare geheugen van Hallo sessie laden is lager dan het Hallo vereist geheugen werkt, krijgen voortijdig Rijgroepen bijgesneden.</span><span class="sxs-lookup"><span data-stu-id="58845-131">When available memory of hello loading session is less than hello required working memory, row groups get prematurely trimmed.</span></span> <span data-ttu-id="58845-132">Hallo volgende secties wordt uitgelegd hoe tooestimate geheugen vereist en meer geheugen toewijzen.</span><span class="sxs-lookup"><span data-stu-id="58845-132">hello following sections explain how tooestimate memory required and allocate more memory.</span></span>
- <span data-ttu-id="58845-133">DICTIONARY_SIZE: Voor deze trim reden geeft aan dat rijgroep bijsnijden omdat er ten minste één kolom met tekenreeksen met een hoge en/of hoge kardinaliteit tekenreeks is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="58845-133">DICTIONARY_SIZE: This trim reason indicates that rowgroup trimming occurred because there was at least one string column with wide and/or high cardinality strings.</span></span> <span data-ttu-id="58845-134">Hallo woordenlijst grootte is beperkt too16 MB in het geheugen en wanneer deze limiet is bereikt Hallo rijgroep worden gecomprimeerd.</span><span class="sxs-lookup"><span data-stu-id="58845-134">hello dictionary size is limited too16 MB in memory and once this limit is reached hello row group is compressed.</span></span> <span data-ttu-id="58845-135">Als u in deze situatie uitvoert, kunt u overwegen isoleren Hallo problematisch kolom in een afzonderlijke tabel.</span><span class="sxs-lookup"><span data-stu-id="58845-135">If you do run into this situation, consider isolating hello problematic column into a separate table.</span></span>

## <a name="how-tooestimate-memory-requirements"></a><span data-ttu-id="58845-136">Hoe tooestimate geheugenvereisten</span><span class="sxs-lookup"><span data-stu-id="58845-136">How tooestimate memory requirements</span></span>

<!--
tooview an estimate of hello memory requirements toocompress a rowgroup of maximum size into a columnstore index, download and run hello view [dbo.vCS_mon_mem_grant](). This view shows hello size of hello memory grant that a rowgroup requires for compression in toohello columnstore.
-->

<span data-ttu-id="58845-137">Hallo vereist Maximumgeheugen toocompress één rijgroep is ongeveer</span><span class="sxs-lookup"><span data-stu-id="58845-137">hello maximum required memory toocompress one rowgroup is approximately</span></span>

- <span data-ttu-id="58845-138">72 MB +</span><span class="sxs-lookup"><span data-stu-id="58845-138">72 MB +</span></span>
- <span data-ttu-id="58845-139">\#rijen \* \#kolommen \* 8 bytes +</span><span class="sxs-lookup"><span data-stu-id="58845-139">\#rows \* \#columns \* 8 bytes +</span></span>
- <span data-ttu-id="58845-140">\#rijen \* \#korte tekenreekskolommen \* 32 bytes +</span><span class="sxs-lookup"><span data-stu-id="58845-140">\#rows \* \#short-string-columns \* 32 bytes +</span></span>
- <span data-ttu-id="58845-141">\#lange tekenreekskolommen \* 16 MB voor compressiebibliotheek</span><span class="sxs-lookup"><span data-stu-id="58845-141">\#long-string-columns \* 16 MB for compression dictionary</span></span>

<span data-ttu-id="58845-142">waar korte tekenreekskolommen gebruiken voor de gegevenstypen string van < = 32 bytes en het gebruik van lange tekenreekskolommen tekenreeks gegevenstypen > 32 bytes.</span><span class="sxs-lookup"><span data-stu-id="58845-142">where short-string-columns use string data types of <= 32 bytes and long-string-columns use string data types of > 32 bytes.</span></span>

<span data-ttu-id="58845-143">Lange tekenreeksen zijn gecomprimeerd met een compressiemethode die is ontworpen voor het comprimeren van tekst.</span><span class="sxs-lookup"><span data-stu-id="58845-143">Long strings are compressed with a compression method designed for compressing text.</span></span> <span data-ttu-id="58845-144">Deze compressiemethode gebruikt een *woordenlijst* toostore alleen tekstpatronen.</span><span class="sxs-lookup"><span data-stu-id="58845-144">This compression method uses a *dictionary* toostore text patterns.</span></span> <span data-ttu-id="58845-145">Hallo maximale grootte van een woordenboek is 16 MB.</span><span class="sxs-lookup"><span data-stu-id="58845-145">hello maximum size of a dictionary is 16 MB.</span></span> <span data-ttu-id="58845-146">Er is slechts één woordenlijst voor elke kolom lange tekenreeks in Hallo rijgroep.</span><span class="sxs-lookup"><span data-stu-id="58845-146">There is only one dictionary for each long string column in hello rowgroup.</span></span>

<span data-ttu-id="58845-147">Zie de video voor een gedetailleerdere beschrijving van de geheugenvereisten columnstore [Azure SQL Data Warehouse schalen: configuratie en richtlijnen](https://myignite.microsoft.com/videos/14822).</span><span class="sxs-lookup"><span data-stu-id="58845-147">For an in-depth discussion of columnstore memory requirements, see the video [Azure SQL Data Warehouse scaling: configuration and guidance](https://myignite.microsoft.com/videos/14822).</span></span>

## <a name="ways-tooreduce-memory-requirements"></a><span data-ttu-id="58845-148">Manieren tooreduce geheugenvereisten</span><span class="sxs-lookup"><span data-stu-id="58845-148">Ways tooreduce memory requirements</span></span>

<span data-ttu-id="58845-149">Gebruik hello technieken tooreduce Hallo geheugenvereisten voor rowgroups comprimeren en columnstore-indexen te volgen.</span><span class="sxs-lookup"><span data-stu-id="58845-149">Use hello following techniques tooreduce hello memory requirements for compressing rowgroups into columnstore indexes.</span></span>

### <a name="use-fewer-columns"></a><span data-ttu-id="58845-150">Gebruik minder kolommen</span><span class="sxs-lookup"><span data-stu-id="58845-150">Use fewer columns</span></span>
<span data-ttu-id="58845-151">Indien mogelijk ontwerp Hallo tabel met minder kolommen.</span><span class="sxs-lookup"><span data-stu-id="58845-151">If possible, design hello table with fewer columns.</span></span> <span data-ttu-id="58845-152">Wanneer een rijgroep in Hallo columnstore is gecomprimeerd, Hallo columnstore-index elk kolomsegment afzonderlijk gecomprimeerd.</span><span class="sxs-lookup"><span data-stu-id="58845-152">When a rowgroup is compressed into hello columnstore, hello columnstore index compresses each column segment separately.</span></span> <span data-ttu-id="58845-153">Daarom Hallo geheugenvereisten toocompress een rijgroep als Hallo aantal kolommen toeneemt verhogen.</span><span class="sxs-lookup"><span data-stu-id="58845-153">Therefore hello memory requirements toocompress a rowgroup increase as hello number of columns increases.</span></span>


### <a name="use-fewer-string-columns"></a><span data-ttu-id="58845-154">Gebruik minder tekenreekskolommen</span><span class="sxs-lookup"><span data-stu-id="58845-154">Use fewer string columns</span></span>
<span data-ttu-id="58845-155">Kolommen van de gegevenstypen string vereisen meer geheugen dan numerieke en datum-gegevenstypen.</span><span class="sxs-lookup"><span data-stu-id="58845-155">Columns of string data types require more memory than numeric and date data types.</span></span> <span data-ttu-id="58845-156">tooreduce geheugenvereisten, overweeg dan tekenreekskolommen verwijderen uit feitentabellen en ze in kleinere dimensietabellen te plaatsen.</span><span class="sxs-lookup"><span data-stu-id="58845-156">tooreduce memory requirements, consider removing string columns from fact tables and putting them in smaller dimension tables.</span></span>

<span data-ttu-id="58845-157">Extra geheugen nodig voor de compressie van de tekenreeks:</span><span class="sxs-lookup"><span data-stu-id="58845-157">Additional memory requirements for string compression:</span></span>

- <span data-ttu-id="58845-158">De gegevenstypen String up too32 tekens kunnen 32 aanvullende bytes per waarde vereisen.</span><span class="sxs-lookup"><span data-stu-id="58845-158">String data types up too32 characters can require 32 additional bytes per value.</span></span>
- <span data-ttu-id="58845-159">De gegevenstypen String met meer dan 32 tekens zijn gecomprimeerd met behulp van methoden van de woordenlijst.</span><span class="sxs-lookup"><span data-stu-id="58845-159">String data types with more than 32 characters are compressed using dictionary methods.</span></span>  <span data-ttu-id="58845-160">Elke kolom in Hallo rijgroep kunt vereisen van tooan aanvullende 16 MB toobuild Hallo-woordenlijst.</span><span class="sxs-lookup"><span data-stu-id="58845-160">Each column in hello rowgroup can require up tooan additional 16 MB toobuild hello dictionary.</span></span>

### <a name="avoid-over-partitioning"></a><span data-ttu-id="58845-161">Te veel partitioneren voorkomen</span><span class="sxs-lookup"><span data-stu-id="58845-161">Avoid over-partitioning</span></span>

<span data-ttu-id="58845-162">Columnstore-indexen maken een of meer rowgroups per partitie.</span><span class="sxs-lookup"><span data-stu-id="58845-162">Columnstore indexes create one or more rowgroups per partition.</span></span> <span data-ttu-id="58845-163">In SQL Data Warehouse groeit het aantal partities Hallo snel omdat Hallo gegevens wordt gedistribueerd en elke distributie is gepartitioneerd.</span><span class="sxs-lookup"><span data-stu-id="58845-163">In SQL Data Warehouse, hello number of partitions grows quickly because hello data is distributed and each distribution is partitioned.</span></span> <span data-ttu-id="58845-164">Als Hallo tabel te veel partities heeft, er mogelijk niet voldoende rijen toofill hello rowgroups.</span><span class="sxs-lookup"><span data-stu-id="58845-164">If hello table has too many partitions, there might not be enough rows toofill hello rowgroups.</span></span> <span data-ttu-id="58845-165">Hallo gebrek aan rijen maakt geen geheugendruk tijdens compressie, maar dit leidt toorowgroups die Voer geen controles door Hallo beste columnstore queryprestaties.</span><span class="sxs-lookup"><span data-stu-id="58845-165">hello lack of rows does not create memory pressure during compression, but it leads toorowgroups that do not achieve hello best columnstore query performance.</span></span>

<span data-ttu-id="58845-166">Een andere reden tooavoid te veel partitioneren is er een geheugen overhead voor het laden van rijen in een columnstore-index in een gepartitioneerde tabel.</span><span class="sxs-lookup"><span data-stu-id="58845-166">Another reason tooavoid over-partitioning is there is a memory overhead for loading rows into a columnstore index on a partitioned table.</span></span> <span data-ttu-id="58845-167">Tijdens een werklast kunnen veel partities Hallo binnenkomende rijen, wat in het geheugen worden bewaard totdat elke partitie onvoldoende rijen toobe gecomprimeerd heeft ontvangen.</span><span class="sxs-lookup"><span data-stu-id="58845-167">During a load, many partitions could receive hello incoming rows, which are held in memory until each partition has enough rows toobe compressed.</span></span> <span data-ttu-id="58845-168">Aanvullende geheugendruk met te veel partities worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="58845-168">Having too many partitions creates additional memory pressure.</span></span>

### <a name="simplify-hello-load-query"></a><span data-ttu-id="58845-169">Hallo load query vereenvoudigen</span><span class="sxs-lookup"><span data-stu-id="58845-169">Simplify hello load query</span></span>

<span data-ttu-id="58845-170">Hallo database deelt Hallo geheugentoekenning voor een query tussen alle Hallo operators in Hallo-query.</span><span class="sxs-lookup"><span data-stu-id="58845-170">hello database shares hello memory grant for a query among all hello operators in hello query.</span></span> <span data-ttu-id="58845-171">Wanneer een load-query complexe sorteerbewerkingen en joins heeft, is Hallo geheugen beschikbaar is voor compressie verminderd.</span><span class="sxs-lookup"><span data-stu-id="58845-171">When a load query has complex sorts and joins, hello memory available for compression is reduced.</span></span>

<span data-ttu-id="58845-172">Ontwerp Hallo load query toofocus alleen voor het laden van Hallo-query.</span><span class="sxs-lookup"><span data-stu-id="58845-172">Design hello load query toofocus only on loading hello query.</span></span> <span data-ttu-id="58845-173">Als u toorun transformaties op Hallo gegevens nodig, gescheiden van Hallo load query uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="58845-173">If you need toorun transformations on hello data, run them separate from hello load query.</span></span> <span data-ttu-id="58845-174">Bijvoorbeeld, fase Hallo gegevens in een tabel heap Hallo transformaties uitvoeren en vervolgens laden Hallo faseringstabel in Hallo columnstore-index.</span><span class="sxs-lookup"><span data-stu-id="58845-174">For example, stage hello data in a heap table, run hello transformations, and then load hello staging table into hello columnstore index.</span></span> <span data-ttu-id="58845-175">U kunt ook eerst laden Hallo gegevens en gebruik vervolgens Hallo MPP tootransform Hallo systeemgegevens.</span><span class="sxs-lookup"><span data-stu-id="58845-175">You can also load hello data first and then use hello MPP system tootransform hello data.</span></span>

### <a name="adjust-maxdop"></a><span data-ttu-id="58845-176">MAXDOP aanpassen</span><span class="sxs-lookup"><span data-stu-id="58845-176">Adjust MAXDOP</span></span>

<span data-ttu-id="58845-177">Elk distributiepunt comprimeert rowgroups in Hallo columnstore parallel wanneer er meer dan één CPU-kern beschikbaar per distributiepunt.</span><span class="sxs-lookup"><span data-stu-id="58845-177">Each distribution compresses rowgroups into hello columnstore in parallel when there is more than one CPU core available per distribution.</span></span> <span data-ttu-id="58845-178">Hallo parallelle uitvoering vereist extra geheugenbronnen, wat toomemory druk en rijgroep bijsnijden leiden kunnen.</span><span class="sxs-lookup"><span data-stu-id="58845-178">hello parallelism requires additional memory resources, which can lead toomemory pressure and rowgroup trimming.</span></span>

<span data-ttu-id="58845-179">tooreduce geheugendruk, kunt u Hallo MAXDOP query hint tooforce Hallo load bewerking toorun in de modus seriële binnen elk distributiepunt.</span><span class="sxs-lookup"><span data-stu-id="58845-179">tooreduce memory pressure, you can use hello MAXDOP query hint tooforce hello load operation toorun in serial mode within each distribution.</span></span>

```
CREATE TABLE MyFactSalesQuota
WITH (DISTRIBUTION = ROUND_ROBIN)
AS SELECT * FROM FactSalesQUota
OPTION (MAXDOP 1);
```

## <a name="ways-tooallocate-more-memory"></a><span data-ttu-id="58845-180">Manieren tooallocate meer geheugen</span><span class="sxs-lookup"><span data-stu-id="58845-180">Ways tooallocate more memory</span></span>

<span data-ttu-id="58845-181">DWU grootte en Hallo gebruiker bronklasse samen bepalen hoeveel geheugen beschikbaar is voor de aanvraag voor een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="58845-181">DWU size and hello user resource class together determine how much memory is available for a user query.</span></span> <span data-ttu-id="58845-182">tooincrease hello geheugen verlenen voor een load-query, kunt u Verhoog het aantal dwu's Hallo of Hallo bronklasse verhogen.</span><span class="sxs-lookup"><span data-stu-id="58845-182">tooincrease hello memory grant for a load query, you can either increase hello number of DWUs or increase hello resource class.</span></span>

- <span data-ttu-id="58845-183">tooincrease hello dwu's, Zie [hoe schalen prestaties?](sql-data-warehouse-manage-compute-overview.md#scale-compute)</span><span class="sxs-lookup"><span data-stu-id="58845-183">tooincrease hello DWUs, see [How do I scale performance?](sql-data-warehouse-manage-compute-overview.md#scale-compute)</span></span>
- <span data-ttu-id="58845-184">Zie toochange Hallo bronklasse voor een query [wijzigen van een voorbeeld van een gebruiker resource klasse](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="58845-184">toochange hello resource class for a query, see [Change a user resource class example](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>

<span data-ttu-id="58845-185">Bijvoorbeeld op DWU 100 kunt een gebruiker in Hallo smallrc bronklasse 100 MB aan geheugen voor elk distributiepunt.</span><span class="sxs-lookup"><span data-stu-id="58845-185">For example, on DWU 100 a user in hello smallrc resource class can use 100 MB of memory for each distribution.</span></span> <span data-ttu-id="58845-186">Zie voor meer informatie Hallo [gelijktijdigheid in SQL Data Warehouse](sql-data-warehouse-develop-concurrency.md).</span><span class="sxs-lookup"><span data-stu-id="58845-186">For hello details, see [Concurrency in SQL Data Warehouse](sql-data-warehouse-develop-concurrency.md).</span></span>

<span data-ttu-id="58845-187">Stel dat u vastgesteld dat er 700 MB aan geheugen tooget rijgroep van hoge kwaliteit grootten.</span><span class="sxs-lookup"><span data-stu-id="58845-187">Suppose you determine that you need 700 MB of memory tooget high-quality rowgroup sizes.</span></span> <span data-ttu-id="58845-188">Deze voorbeelden laten zien hoe u Hallo load query kunt uitvoeren met onvoldoende geheugen.</span><span class="sxs-lookup"><span data-stu-id="58845-188">These examples show how you can run hello load query with enough memory.</span></span>

- <span data-ttu-id="58845-189">DWU-1000 en mediumrc gebruikt, is uw geheugentoekenning 800 MB</span><span class="sxs-lookup"><span data-stu-id="58845-189">Using DWU 1000 and mediumrc, your memory grant is 800 MB</span></span>
- <span data-ttu-id="58845-190">DWU 600 en largerc gebruikt, is uw geheugentoekenning 800 MB.</span><span class="sxs-lookup"><span data-stu-id="58845-190">Using DWU 600 and largerc, your memory grant is 800 MB.</span></span>


## <a name="next-steps"></a><span data-ttu-id="58845-191">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="58845-191">Next steps</span></span>

<span data-ttu-id="58845-192">toofind meer manieren tooimprove prestaties in SQL Data Warehouse, Zie Hallo [prestatieoverzicht](sql-data-warehouse-overview-manage-user-queries.md).</span><span class="sxs-lookup"><span data-stu-id="58845-192">toofind more ways tooimprove performance in SQL Data Warehouse, see hello [Performance overview](sql-data-warehouse-overview-manage-user-queries.md).</span></span>

<!--Image references-->

<!--Article references-->


<!--MSDN references-->

<!--Other Web references-->
