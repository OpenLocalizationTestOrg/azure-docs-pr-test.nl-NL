---
title: "aaaAzure SQL Database In het geheugen technologieën | Microsoft Docs"
description: "Azure SQL Database In het geheugen technologieën verbeteren aanzienlijk Hallo prestaties van transactionele en analytics werkbelastingen. Meer informatie over hoe tootake profiteren van deze technologieën."
services: sql-database
documentationCenter: 
author: jodebrui
manager: jhubbard
editor: 
ms.assetid: 250ef341-90e5-492f-b075-b4750d237c05
ms.service: sql-database
ms.custom: develop databases
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jodebrui
ms.openlocfilehash: 1bacd7297b2f9b018853088eabf2a2ee66a9cb43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-performance-by-using-in-memory-technologies-in-sql-database"></a><span data-ttu-id="7d3a7-104">Prestaties optimaliseren door technologieën voor In-Memory in SQL-Database</span><span class="sxs-lookup"><span data-stu-id="7d3a7-104">Optimize performance by using In-Memory technologies in SQL Database</span></span>

<span data-ttu-id="7d3a7-105">In-Memory technologieën in Azure SQL Database gebruikt, kunt u met verschillende workloads voor verbeterde prestaties bereiken: transactionele (online transactionele verwerking (OLTP)), analytics (online analytical processing (OLAP)), en gemengde (hybride transactie/analytische verwerking (HTAP)).</span><span class="sxs-lookup"><span data-stu-id="7d3a7-105">By using In-Memory technologies in Azure SQL Database, you can achieve performance improvements with various workloads: transactional (online transactional processing (OLTP)), analytics (online analytical processing (OLAP)), and mixed (hybrid transaction/analytical processing (HTAP)).</span></span> <span data-ttu-id="7d3a7-106">Omdat Hallo efficiënter query en transactieverwerking, In-Memory-technologieën kunnen u ook tooreduce kosten.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-106">Because of hello more efficient query and transaction processing, In-Memory technologies also help you tooreduce cost.</span></span> <span data-ttu-id="7d3a7-107">U nodig tooupgrade Hallo prijscategorie van Hallo database tooachieve prestatiewinst doorgaans niet.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-107">You typically don't need tooupgrade hello pricing tier of hello database tooachieve performance gains.</span></span> <span data-ttu-id="7d3a7-108">In sommige gevallen u zelfs mogelijk Hallo prijscategorie tijdens steeds prestatieverbeteringen met technologieën In het geheugen te verminderen.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-108">In some cases, you might even be able reduce hello pricing tier, while still seeing performance improvements with In-Memory technologies.</span></span>

<span data-ttu-id="7d3a7-109">Hier vindt u twee voorbeelden van hoe In het geheugen OLTP geholpen toosignificantly de prestaties verbeteren:</span><span class="sxs-lookup"><span data-stu-id="7d3a7-109">Here are two examples of how In-Memory OLTP helped toosignificantly improve performance:</span></span>

- <span data-ttu-id="7d3a7-110">Met behulp van de In-geheugen OLTP [Quorum bedrijfsoplossingen kunnen toodouble van hun werkbelasting is tijdens het aantal dtu's verbeteren met 70%](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).</span><span class="sxs-lookup"><span data-stu-id="7d3a7-110">By using In-Memory OLTP, [Quorum Business Solutions was able toodouble their workload while improving DTUs by 70%](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).</span></span>
    - <span data-ttu-id="7d3a7-111">DTU betekent *dtu*, en bevat een mesurement van resourceverbruik.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-111">DTU means *database throughput unit*, and it includes a mesurement of resource consumption.</span></span>
- <span data-ttu-id="7d3a7-112">Hallo volgende video toont aanzienlijke verbetering in het verbruik van met een werklast voorbeeld: [In het geheugen OLTP in Azure SQL Database Video](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB).</span><span class="sxs-lookup"><span data-stu-id="7d3a7-112">hello following video demonstrates significant improvement in resource consumption with a sample workload: [In-Memory OLTP in Azure SQL Database Video](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB).</span></span>
    - <span data-ttu-id="7d3a7-113">Zie voor meer informatie Hallo blogbericht: [In het geheugen OLTP in Azure SQL Database-blogberichten](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)</span><span class="sxs-lookup"><span data-stu-id="7d3a7-113">For more details, see hello blog post: [In-Memory OLTP in Azure SQL Database Blog Post](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)</span></span>

<span data-ttu-id="7d3a7-114">In het geheugen technologieën zijn beschikbaar in alle databases in Hallo Premium-laag, met inbegrip van databases in Premium elastische pools.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-114">In-Memory technologies are available in all databases in hello Premium tier, including databases in Premium elastic pools.</span></span>

<span data-ttu-id="7d3a7-115">Hallo volgende video wordt uitgelegd mogelijke prestatieverbeteringen met technologieën in Azure SQL Database In het geheugen.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-115">hello following video explains potential performance gains with In-Memory technologies in Azure SQL Database.</span></span> <span data-ttu-id="7d3a7-116">Houd er rekening mee dat Hallo prestatieverbetering te bereiken die u altijd ziet afhankelijk is van veel factoren, onder andere Hallo aard van Hallo werkbelasting en gegevens, toegangstijden van Hallo-database, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-116">Remember that hello performance gain that you see always depends on many factors, including hello nature of hello workload and data, access pattern of hello database, and so on.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-In-Memory-Technologies/player]
>
>

<span data-ttu-id="7d3a7-117">Azure SQL-Database heeft Hallo technologieën In het geheugen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7d3a7-117">Azure SQL Database has hello following In-Memory technologies:</span></span>

- <span data-ttu-id="7d3a7-118">*In het geheugen OLTP* verhoogt de doorvoer en vermindert de latentie voor de transactieverwerking.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-118">*In-Memory OLTP* increases throughput and reduces latency for transaction processing.</span></span> <span data-ttu-id="7d3a7-119">Scenario's die van de In-geheugen OLTP profiteren zijn: hoge gegevensdoorvoer transactieverwerking zoals handelspartners en games, gegevensopname uit gebeurtenissen of IoT-apparaten, opslaan in cache laden van gegevens en de tijdelijke tabel en de variabele scenario's voor een tabel.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-119">Scenarios that benefit from In-Memory OLTP are: high-throughput transaction processing such as trading and gaming, data ingestion from events or IoT devices, caching, data load, and temporary table and table variable scenarios.</span></span>
- <span data-ttu-id="7d3a7-120">*Geclusterde columnstore-indexen* verminderen van de opslag van kooldioxide (omhoog too10 keren) en verbeterde prestaties voor query's voor rapportage en analyse.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-120">*Clustered columnstore indexes* reduce your storage footprint (up too10 times) and improve performance for reporting and analytics queries.</span></span> <span data-ttu-id="7d3a7-121">U kunt deze gebruiken met feitentabellen in uw gegevens datamarts toofit meer gegevens in uw database en de prestaties verbeteren.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-121">You can use it with fact tables in your data marts toofit more data in your database and improve performance.</span></span> <span data-ttu-id="7d3a7-122">U kunt ook met historische gegevens worden gebruikt in uw tooarchive operationele database en kunnen tooquery van too10 tijden meer gegevens zijn.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-122">Also, you can use it with historical data in your operational database tooarchive and be able tooquery up too10 times more data.</span></span>
- <span data-ttu-id="7d3a7-123">*Niet-geclusterde columnstore-indexen* voor HTAP help u toogain realtime-inzichten in uw bedrijf door het uitvoeren van query's Hallo operationele database rechtstreeks zonder Hallo nodig toorun een dure uitpakken, transformeren en laden (ETL)-proces en wacht voor Hallo datawarehouse toobe ingevuld.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-123">*Nonclustered columnstore indexes* for HTAP help you toogain real-time insights into your business through querying hello operational database directly, without hello need toorun an expensive extract, transform, and load (ETL) process and wait for hello data warehouse toobe populated.</span></span> <span data-ttu-id="7d3a7-124">Niet-geclusterde columnstore-indexen kunnen zeer snel uitvoering van analysequery's op Hallo OLTP-database, terwijl het Hallo gevolgen voor de operationele werkbelasting Hallo verminderen.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-124">Nonclustered columnstore indexes allow very fast execution of analytics queries on hello OLTP database, while reducing hello impact on hello operational workload.</span></span>
- <span data-ttu-id="7d3a7-125">U kunt ook Hallo combinatie van een tabel geoptimaliseerd voor geheugen met een columnstore-index hebben.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-125">You can also have hello combination of a memory-optimized table with a columnstore index.</span></span> <span data-ttu-id="7d3a7-126">Deze combinatie kunt u tooperform zeer snel transactieverwerking, en te*gelijktijdig* uitvoeren analytics query zeer snel op Hallo dezelfde gegevens.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-126">This combination enables you tooperform very fast transaction processing, and too*concurrently* run analytics queries very quickly on hello same data.</span></span>

<span data-ttu-id="7d3a7-127">Columnstore-indexen zowel In-geheugen OLTP is onderdeel van de SQL Server-product Hallo sinds 2012 en 2014, respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-127">Both columnstore indexes and In-Memory OLTP have been part of hello SQL Server product since 2012 and 2014, respectively.</span></span> <span data-ttu-id="7d3a7-128">Azure SQL Database en SQL Server delen Hallo dezelfde implementatie van de technologieën In het geheugen.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-128">Azure SQL Database and SQL Server share hello same implementation of In-Memory technologies.</span></span> <span data-ttu-id="7d3a7-129">Voortaan kunt zijn nieuwe mogelijkheden voor deze technologieën uitgebracht in Azure SQL Database eerst voordat ze worden vrijgegeven in SQL Server.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-129">Going forward, new capabilities for these technologies are released in Azure SQL Database first, before they are released in SQL Server.</span></span>

<span data-ttu-id="7d3a7-130">Dit onderwerp wordt beschreven aspecten van de In-geheugen OLTP en columnstore-indexen die specifieke tooAzure SQL-Database en tevens voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="7d3a7-130">This topic describes aspects of In-Memory OLTP and columnstore indexes that are specific tooAzure SQL Database and also includes samples:</span></span>
- <span data-ttu-id="7d3a7-131">Hallo-impact van deze technologieën ziet u op de opslag- en maximale grootte ervan.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-131">You'll see hello impact of these technologies on storage and data size limits.</span></span>
- <span data-ttu-id="7d3a7-132">U ziet hoe toomanage verkeer van de databases die gebruikmaken van deze technologieën tussen verschillende Prijscategorieën Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-132">You'll see how toomanage hello movement of databases that use these technologies between hello different pricing tiers.</span></span>
- <span data-ttu-id="7d3a7-133">Hier ziet u twee voorbeelden die Hallo gebruik van de In-geheugen OLTP, evenals de columnstore-indexen in Azure SQL Database aangeven.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-133">You'll see two samples that illustrate hello use of In-Memory OLTP, as well as columnstore indexes in Azure SQL Database.</span></span>

<span data-ttu-id="7d3a7-134">Zie Hallo volgende bronnen voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-134">See hello following resources for more information.</span></span>

<span data-ttu-id="7d3a7-135">Gedetailleerde informatie over Hallo-technologieën:</span><span class="sxs-lookup"><span data-stu-id="7d3a7-135">In-depth information about hello technologies:</span></span>

- <span data-ttu-id="7d3a7-136">[In het geheugen OLTP-overzicht en gebruiksscenario's](https://msdn.microsoft.com/library/mt774593.aspx) (inclusief verwijzingen toocustomer casestudy's en informatie tooget gestart)</span><span class="sxs-lookup"><span data-stu-id="7d3a7-136">[In-Memory OLTP Overview and Usage Scenarios](https://msdn.microsoft.com/library/mt774593.aspx) (includes references toocustomer case studies and information tooget started)</span></span>
- [<span data-ttu-id="7d3a7-137">Documentatie voor In-geheugen OLTP</span><span class="sxs-lookup"><span data-stu-id="7d3a7-137">Documentation for In-Memory OLTP</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)
- [<span data-ttu-id="7d3a7-138">Handleiding voor Columnstore-indexen</span><span class="sxs-lookup"><span data-stu-id="7d3a7-138">Columnstore Indexes Guide</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)
- <span data-ttu-id="7d3a7-139">Hybride transactionele/analytische verwerking (HTAP), ook wel bekend als [operationele realtime-analyses](https://msdn.microsoft.com/library/dn817827.aspx)</span><span class="sxs-lookup"><span data-stu-id="7d3a7-139">Hybrid transactional/analytical processing (HTAP), also known as [real-time operational analytics](https://msdn.microsoft.com/library/dn817827.aspx)</span></span>

<span data-ttu-id="7d3a7-140">Een snelle introductie op In het geheugen OLTP: [snel starten 1: In het geheugen OLTP-technologieën voor sneller T-SQL-prestaties](http://msdn.microsoft.com/library/mt694156.aspx) (een ander artikel toohelp u aan de slag)</span><span class="sxs-lookup"><span data-stu-id="7d3a7-140">A quick primer on In-Memory OLTP: [Quick Start 1: In-Memory OLTP Technologies for Faster T-SQL Performance](http://msdn.microsoft.com/library/mt694156.aspx) (another article toohelp you get started)</span></span>

<span data-ttu-id="7d3a7-141">Gedetailleerde video's over Hallo-technologieën:</span><span class="sxs-lookup"><span data-stu-id="7d3a7-141">In-depth videos about hello technologies:</span></span>

- <span data-ttu-id="7d3a7-142">[In het geheugen OLTP in Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (die een demonstratie van de prestaties van bevat voordelen en stappen tooreproduce deze resultaten zelf)</span><span class="sxs-lookup"><span data-stu-id="7d3a7-142">[In-Memory OLTP in Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (which contains a demo of performance benefits and steps tooreproduce these results yourself)</span></span>
- [<span data-ttu-id="7d3a7-143">In het geheugen OLTP-video's: Wat is en wanneer en hoe toouse deze</span><span class="sxs-lookup"><span data-stu-id="7d3a7-143">In-Memory OLTP Videos: What it is and When/How toouse it</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/03/in-memory-oltp-video-what-it-is-and-whenhow-to-use-it/)
- [<span data-ttu-id="7d3a7-144">Columnstore-Index: In het geheugen Analytics video's van Ignite 2016</span><span class="sxs-lookup"><span data-stu-id="7d3a7-144">Columnstore Index: In-Memory Analytics Videos from Ignite 2016</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/04/columnstore-index-in-memory-analytics-i-e-columnstore-index-videos-from-ignite-2016/)

## <a name="storage-and-data-size"></a><span data-ttu-id="7d3a7-145">De grootte van opslag en gegevens</span><span class="sxs-lookup"><span data-stu-id="7d3a7-145">Storage and data size</span></span>

### <a name="data-size-and-storage-cap-for-in-memory-oltp"></a><span data-ttu-id="7d3a7-146">Grootte en opslag cap voor In-geheugen OLTP</span><span class="sxs-lookup"><span data-stu-id="7d3a7-146">Data size and storage cap for In-Memory OLTP</span></span>

<span data-ttu-id="7d3a7-147">In het geheugen OLTP bevat geheugen geoptimaliseerde tabellen die worden gebruikt voor het opslaan van gebruikersgegevens.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-147">In-Memory OLTP includes memory-optimized tables, which are used for storing user data.</span></span> <span data-ttu-id="7d3a7-148">Deze tabellen zijn vereiste toofit in het geheugen.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-148">These tables are required toofit in memory.</span></span> <span data-ttu-id="7d3a7-149">Aangezien u geheugen rechtstreeks in Hallo SQL Database-service beheert, hebben we Hallo concept van een quotum voor gebruikersgegevens.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-149">Because you manage memory directly in hello SQL Database service, we have hello  concept of a quota for user data.</span></span> <span data-ttu-id="7d3a7-150">Dit idee is waarnaar wordt verwezen tooas *In het geheugen OLTP-opslag*.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-150">This idea is referred tooas *In-Memory OLTP storage*.</span></span>

<span data-ttu-id="7d3a7-151">Elke prijscategorie en elke elastische pool prijscategorie ondersteunde zelfstandige-database bevat een bepaalde hoeveelheid In het geheugen OLTP-opslag.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-151">Each supported standalone database pricing tier and each elastic pool pricing tier includes a certain amount of In-Memory OLTP storage.</span></span> <span data-ttu-id="7d3a7-152">Bij Hallo schrijven krijgt u een gigabyte van opslag van elke 125 database transactie-eenheden (dtu's) of een elastische database transactie-eenheden (edtu's).</span><span class="sxs-lookup"><span data-stu-id="7d3a7-152">At hello time of writing, you get a gigabyte of storage for every 125 database transaction units (DTUs) or elastic database transaction units (eDTUs).</span></span>

<span data-ttu-id="7d3a7-153">Hallo [SQL Database Servicelagen](sql-database-service-tiers.md) artikel heeft de officiële lijst Hallo Hallo-geheugen OLTP opslag die beschikbaar is voor elke ondersteunde zelfstandige database en de elastische groep prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-153">hello [SQL Database service tiers](sql-database-service-tiers.md) article has hello official list of hello In-Memory OLTP storage that is available for each supported standalone database and elastic pool pricing tier.</span></span>

<span data-ttu-id="7d3a7-154">Hallo aantal items naar uw opslagruimte In het geheugen OLTP cap te volgen:</span><span class="sxs-lookup"><span data-stu-id="7d3a7-154">hello following items count toward your In-Memory OLTP storage cap:</span></span>

- <span data-ttu-id="7d3a7-155">Rijen van de actieve gebruiker gegevens in tabellen geoptimaliseerd voor geheugen en tabelvariabelen.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-155">Active user data rows in memory-optimized tables and table variables.</span></span> <span data-ttu-id="7d3a7-156">Houd er rekening mee dat de oude rij versies niet voor Hallo cap meetellen.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-156">Note that old row versions don't count toward hello cap.</span></span>
- <span data-ttu-id="7d3a7-157">Indexen op tabellen geoptimaliseerd voor geheugen.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-157">Indexes on memory-optimized tables.</span></span>
- <span data-ttu-id="7d3a7-158">Operationele overhead van ALTER TABLE-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-158">Operational overhead of ALTER TABLE operations.</span></span>

<span data-ttu-id="7d3a7-159">Als u Hallo cap raakt, er een foutbericht out van quota en bent u niet langer kunnen tooinsert of update-gegevens.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-159">If you hit hello cap, you receive an out-of-quota error, and you are no longer able tooinsert or update data.</span></span> <span data-ttu-id="7d3a7-160">toomitigate deze fout gegevens verwijderen of vergroot Hallo prijscategorie Hallo database of groep.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-160">toomitigate this error, delete data or increase hello pricing tier of hello database or pool.</span></span>

<span data-ttu-id="7d3a7-161">Zie voor meer informatie over het gebruik van de opslag In het geheugen OLTP controleren en waarschuwingen te configureren als u bijna Hallo cap raakt [Monitor In-Memory opslag](sql-database-in-memory-oltp-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="7d3a7-161">For details about monitoring In-Memory OLTP storage utilization and configuring alerts when you almost hit hello cap, see [Monitor In-Memory storage](sql-database-in-memory-oltp-monitoring.md).</span></span>

#### <a name="about-elastic-pools"></a><span data-ttu-id="7d3a7-162">Over elastische pools</span><span class="sxs-lookup"><span data-stu-id="7d3a7-162">About elastic pools</span></span>

<span data-ttu-id="7d3a7-163">Hallo-geheugen OLTP-opslag wordt met elastische pools gedeeld voor alle databases in Hallo van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-163">With elastic pools, hello In-Memory OLTP storage is shared across all databases in hello pool.</span></span> <span data-ttu-id="7d3a7-164">Daarom Hallo gebruik in één database kan van invloed andere databases.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-164">Therefore, hello usage in one database can potentially affect other databases.</span></span> <span data-ttu-id="7d3a7-165">Er zijn twee oplossingen voor deze:</span><span class="sxs-lookup"><span data-stu-id="7d3a7-165">Two mitigations for this are:</span></span>

- <span data-ttu-id="7d3a7-166">Configureer een Max-aantal edtu's voor databases die lager is dan Hallo eDTU aantal voor Hallo pool als geheel.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-166">Configure a Max-eDTU for databases that is lower than hello eDTU count for hello pool as a whole.</span></span> <span data-ttu-id="7d3a7-167">Dit maximum caps Hallo-geheugen OLTP gebruik van de opslag, in een database in Hallo groep, toohello grootte die overeenkomt met toohello eDTU count.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-167">This maximum caps hello In-Memory OLTP storage utilization, in any database in hello pool, toohello size that corresponds toohello eDTU count.</span></span>
- <span data-ttu-id="7d3a7-168">Configureer een minimum-aantal edtu's die groter is dan 0.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-168">Configure a Min-eDTU that is greater than 0.</span></span> <span data-ttu-id="7d3a7-169">Deze minimale garanties dat elke database in de groep Hallo Hallo en de hoeveelheid beschikbaar In het geheugen OLTP-opslag die overeenkomt met toohello heeft geconfigureerd Min eDTU.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-169">This minimum guarantees that each database in hello pool has hello amount of available In-Memory OLTP storage that corresponds toohello configured Min-eDTU.</span></span>

### <a name="data-size-and-storage-for-columnstore-indexes"></a><span data-ttu-id="7d3a7-170">De gegevensgrootte van en opslag voor de columnstore-indexen</span><span class="sxs-lookup"><span data-stu-id="7d3a7-170">Data size and storage for columnstore indexes</span></span>

<span data-ttu-id="7d3a7-171">Columnstore-indexen zijn niet vereist toofit in het geheugen.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-171">Columnstore indexes aren't required toofit in memory.</span></span> <span data-ttu-id="7d3a7-172">Hallo daarom alleen cap op Hallo grootte van de indexen Hallo Hallo maximale totale grootte van de database die wordt beschreven in Hallo [SQL Database Servicelagen](sql-database-service-tiers.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-172">Therefore, hello only cap on hello size of hello indexes is hello maximum overall database size, which is documented in hello [SQL Database service tiers](sql-database-service-tiers.md) article.</span></span>

<span data-ttu-id="7d3a7-173">Wanneer u een geclusterde columnstore-indexen gebruikt, wordt voor de opslag van de basistabel Hallo kolommen compressie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-173">When you use clustered columnstore indexes, columnar compression is used for hello base table storage.</span></span> <span data-ttu-id="7d3a7-174">Deze compressie kan Hallo opslag voetafdruk van uw gebruikersgegevens, wat betekent dat u meer gegevens in de database Hallo past aanzienlijk verminderen.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-174">This compression can significantly reduce hello storage footprint of your user data, which means that you can fit more data in hello database.</span></span> <span data-ttu-id="7d3a7-175">En Hallo compressie kan worden verhoogd met [kolommen archivering compressie](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression).</span><span class="sxs-lookup"><span data-stu-id="7d3a7-175">And hello compression can be further increased with [columnar archival compression](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression).</span></span> <span data-ttu-id="7d3a7-176">Hallo hoeveelheid compressie die u kunt bereiken, is afhankelijk van Hallo aard van Hallo gegevens, maar 10 keer Hallo compressie is niet ongewoon.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-176">hello amount of compression that you can achieve depends on hello nature of hello data, but 10 times hello compression is not uncommon.</span></span>

<span data-ttu-id="7d3a7-177">Als u een database met een maximale grootte van 1 terabyte (TB hebt) en u 10 keer Hallo compressie bereiken met columnstore-indexen, kunt u een totaal van 10 TB gebruikersgegevens inpassen in Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-177">For example, if you have a database with a maximum size of 1 terabyte (TB) and you achieve 10 times hello compression by using columnstore indexes, you can fit a total of 10 TB of user data in hello database.</span></span>

<span data-ttu-id="7d3a7-178">Wanneer u niet-geclusterde columnstore-indexen gebruikt, wordt de basistabel Hallo nog steeds in Hallo traditionele rowstore indeling opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-178">When you use nonclustered columnstore indexes, hello base table is still stored in hello traditional rowstore format.</span></span> <span data-ttu-id="7d3a7-179">Hallo opslagbesparing zijn daarom niet zo groot als met geclusterde columnstore-indexen.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-179">Therefore, hello storage savings aren't as big as with clustered columnstore indexes.</span></span> <span data-ttu-id="7d3a7-180">Echter, als u een aantal niet-geclusterde indexen traditionele met een enkele columnstore-index vervangt, nog steeds ziet u een algemene besparingen in Hallo opslag footprint voor Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-180">However, if you're replacing a number of traditional nonclustered indexes with a single columnstore index, you can still see an overall savings in hello storage footprint for hello table.</span></span>

## <a name="moving-databases-that-use-in-memory-technologies-between-pricing-tiers"></a><span data-ttu-id="7d3a7-181">Verplaatsen van databases die gebruikmaken van technologieën tussen Prijscategorieën In het geheugen</span><span class="sxs-lookup"><span data-stu-id="7d3a7-181">Moving databases that use In-Memory technologies between pricing tiers</span></span>

<span data-ttu-id="7d3a7-182">Er zijn nooit eventuele incompatibiliteiten of andere problemen bij het upgraden van een hogere prijscategorie, zoals van standaard tooPremium tooa.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-182">There are never any incompatibilities or other problems when you upgrade tooa higher pricing tier, such as from Standard tooPremium.</span></span> <span data-ttu-id="7d3a7-183">Hallo beschikbaar functionaliteit en resources alleen verhogen.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-183">hello available functionality and resources only increase.</span></span>

<span data-ttu-id="7d3a7-184">Maar downgraden Hallo prijscategorie kan een negatieve invloed hebben op uw database.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-184">But downgrading hello pricing tier can negatively impact your database.</span></span> <span data-ttu-id="7d3a7-185">Hallo impact is vooral duidelijk wanneer u van tooStandard Premium downgraden of Basic wanneer uw database In het geheugen OLTP-objecten bevat.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-185">hello impact is especially apparent when you downgrade from Premium tooStandard or Basic when your database contains In-Memory OLTP objects.</span></span> <span data-ttu-id="7d3a7-186">Tabellen geoptimaliseerd voor geheugen en columnstore-indexen zijn niet beschikbaar na Hallo downgrade (zelfs als ze zichtbaar blijft).</span><span class="sxs-lookup"><span data-stu-id="7d3a7-186">Memory-optimized tables, and columnstore indexes, are unavailable after hello downgrade (even if they remain visible).</span></span> <span data-ttu-id="7d3a7-187">Hallo dezelfde overwegingen van toepassing wanneer u bij het verlagen van Hallo prijscategorie van een pool voor elastische of verplaatsen van een database met technologieën In het geheugen, in een standaard of Basic elastische pool.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-187">hello same considerations apply when you're lowering hello pricing tier of an elastic pool, or moving a database with In-Memory technologies, into a Standard or Basic elastic pool.</span></span>

### <a name="in-memory-oltp"></a><span data-ttu-id="7d3a7-188">OLTP in het geheugen</span><span class="sxs-lookup"><span data-stu-id="7d3a7-188">In-Memory OLTP</span></span>

<span data-ttu-id="7d3a7-189">*TooBasic/Standard downgraden*: In het geheugen OLTP-databases in de categorie Standard of Basic Hallo wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-189">*Downgrading tooBasic/Standard*: In-Memory OLTP isn't supported in databases in hello Standard or Basic tier.</span></span> <span data-ttu-id="7d3a7-190">Bovendien is het niet mogelijk toomove een database met een In-geheugen OLTP objecten toohello categorie Standard of Basic.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-190">In addition, it isn't possible toomove a database that has any In-Memory OLTP objects toohello Standard or Basic tier.</span></span>

<span data-ttu-id="7d3a7-191">Voordat u Hallo database tooStandard/Basic gedowngraded, verwijdert u alle tabellen geoptimaliseerd voor geheugen en tabeltypen, evenals alle modules met systeemeigen compilatie T-SQL.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-191">Before you downgrade hello database tooStandard/Basic, remove all memory-optimized tables and table types, as well as all natively compiled T-SQL modules.</span></span>

<span data-ttu-id="7d3a7-192">Er is een programmatische manier toounderstand of een bepaalde database In het geheugen OLTP ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-192">There is a programmatic way toounderstand whether a given database supports In-Memory OLTP.</span></span> <span data-ttu-id="7d3a7-193">U kunt de Hallo volgende Transact-SQL-query uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="7d3a7-193">You can execute hello following Transact-SQL query:</span></span>

```
SELECT DatabasePropertyEx(DB_NAME(), 'IsXTPSupported');
```

<span data-ttu-id="7d3a7-194">Als het resultaat Hallo query **1**, In het geheugen OLTP wordt ondersteund in deze database.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-194">If hello query returns **1**, In-Memory OLTP is supported in this database.</span></span>


<span data-ttu-id="7d3a7-195">*Lagere Premium-laag tooa downgraden*: gegevens in tabellen geoptimaliseerd voor geheugen moet in het Hallo-geheugen OLTP opslag die is gekoppeld aan de prijscategorie van de database Hallo Hallo of beschikbaar is in Hallo elastische pool passen.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-195">*Downgrading tooa lower Premium tier*: Data in memory-optimized tables must fit within hello In-Memory OLTP storage that is associated with hello pricing tier of hello database or is available in hello elastic pool.</span></span> <span data-ttu-id="7d3a7-196">Als u probeert toolower Hallo prijscategorie of verplaatst Hallo-database naar een groep die beschikt niet over voldoende opslagruimte beschikbaar In het geheugen OLTP, Hallo-bewerking is mislukt.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-196">If you try toolower hello pricing tier or move hello database into a pool that doesn't have enough available In-Memory OLTP storage, hello operation fails.</span></span>

### <a name="columnstore-indexes"></a><span data-ttu-id="7d3a7-197">Columnstore-indexen</span><span class="sxs-lookup"><span data-stu-id="7d3a7-197">Columnstore indexes</span></span>

<span data-ttu-id="7d3a7-198">*Downgraden tooBasic of standaard*: Columnstore-indexen worden ondersteund, alleen op Hallo Premium-prijscategorie en niet op Hallo Standard- of Basic-lagen.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-198">*Downgrading tooBasic or Standard*: Columnstore indexes are supported only on hello Premium pricing tier, and not on hello Standard or Basic tiers.</span></span> <span data-ttu-id="7d3a7-199">Wanneer u uw database tooStandard of Basic gedowngraded, columnstore-index niet meer beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-199">When you downgrade your database tooStandard or Basic, your columnstore index becomes unavailable.</span></span> <span data-ttu-id="7d3a7-200">Hallo system onderhoudt columnstore-index, maar deze nooit maakt gebruik van Hallo index.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-200">hello system maintains your columnstore index, but it never leverages hello index.</span></span> <span data-ttu-id="7d3a7-201">Als u later terug tooPremium bijwerkt, wordt de columnstore-index onmiddellijk gereed toobe opnieuw gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-201">If you later upgrade back tooPremium, your columnstore index is immediately ready toobe leveraged again.</span></span>

<span data-ttu-id="7d3a7-202">Als u hebt een **geclusterde** columnstore-index Hallo hele tabel niet meer beschikbaar is na een downgrade van laag.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-202">If you have a **clustered** columnstore index, hello whole table becomes unavailable after tier downgrade.</span></span> <span data-ttu-id="7d3a7-203">Daarom raden we aan dat u alle neerzetten *geclusterde* columnstore-indexen voordat u uw database hieronder de Premium-laag Hallo downgraden.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-203">Therefore we recommend that you drop all *clustered* columnstore indexes before you downgrade your database below hello Premium tier.</span></span>

<span data-ttu-id="7d3a7-204">*Lagere Premium-laag tooa downgraden*: deze downgrade is geslaagd als de gehele database Hallo past binnen de maximale databasegrootte Hallo voor Hallo doel prijscategorie of binnen Hallo beschikbare opslagruimte in de elastische groep Hallo.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-204">*Downgrading tooa lower Premium tier*: This downgrade succeeds if hello whole database fits within hello maximum database size for hello target pricing tier, or within hello available storage in hello elastic pool.</span></span> <span data-ttu-id="7d3a7-205">Er zijn geen specifieke gevolgen van Hallo columnstore-indexen.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-205">There is no specific impact from hello columnstore indexes.</span></span>


<a id="install_oltp_manuallink" name="install_oltp_manuallink"></a>

&nbsp;

## <a name="1-install-hello-in-memory-oltp-sample"></a><span data-ttu-id="7d3a7-206">1. Hallo-geheugen OLTP-voorbeeld installeren</span><span class="sxs-lookup"><span data-stu-id="7d3a7-206">1. Install hello In-Memory OLTP sample</span></span>

<span data-ttu-id="7d3a7-207">U kunt Hallo de voorbeelddatabase van AdventureWorksLT maken met een paar muisklikken in Hallo [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="7d3a7-207">You can create hello AdventureWorksLT sample database with a few clicks in hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="7d3a7-208">Vervolgens hello in deze sectie wordt uitgelegd hoe u uw database AdventureWorksLT met In-geheugen OLTP-objecten aanvullen en prestatievoordelen demonstreren.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-208">Then, hello steps in this section explain how you can enrich your AdventureWorksLT database with In-Memory OLTP objects and demonstrate performance benefits.</span></span>

<span data-ttu-id="7d3a7-209">Zie voor een meer eenvoudig, maar meer aantrekkelijk prestaties demo voor In-geheugen OLTP:</span><span class="sxs-lookup"><span data-stu-id="7d3a7-209">For a more simplistic, but more visually appealing performance demo for In-Memory OLTP, see:</span></span>

- <span data-ttu-id="7d3a7-210">De versie: [in-memory-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)</span><span class="sxs-lookup"><span data-stu-id="7d3a7-210">Release: [in-memory-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)</span></span>
- <span data-ttu-id="7d3a7-211">Broncode: [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)</span><span class="sxs-lookup"><span data-stu-id="7d3a7-211">Source code: [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)</span></span>

#### <a name="installation-steps"></a><span data-ttu-id="7d3a7-212">Installatiestappen</span><span class="sxs-lookup"><span data-stu-id="7d3a7-212">Installation steps</span></span>

1. <span data-ttu-id="7d3a7-213">In Hallo [Azure-portal](https://portal.azure.com/), een Premium-database maken op een server.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-213">In hello [Azure portal](https://portal.azure.com/), create a Premium database on a server.</span></span> <span data-ttu-id="7d3a7-214">Set Hallo **bron** toohello de voorbeelddatabase van AdventureWorksLT.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-214">Set hello **Source** toohello AdventureWorksLT sample database.</span></span> <span data-ttu-id="7d3a7-215">Zie voor gedetailleerde instructies [uw eerste Azure SQL-database maken](sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7d3a7-215">For detailed instructions, see [Create your first Azure SQL database](sql-database-get-started-portal.md).</span></span>

2. <span data-ttu-id="7d3a7-216">Verbinding maken met toohello database met SQL Server Management Studio [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="7d3a7-216">Connect toohello database with SQL Server Management Studio [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

3. <span data-ttu-id="7d3a7-217">Kopiëren Hallo [In het geheugen OLTP Transact-SQL-script](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) tooyour Klembord.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-217">Copy hello [In-Memory OLTP Transact-SQL script](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) tooyour clipboard.</span></span> <span data-ttu-id="7d3a7-218">Hallo T-SQL-script maakt Hallo nodig In het geheugen objecten in de voorbeelddatabase van Hallo AdventureWorksLT die u in stap 1 hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-218">hello T-SQL script creates hello necessary In-Memory objects in hello AdventureWorksLT sample database that you created in step 1.</span></span>

4. <span data-ttu-id="7d3a7-219">Hallo T-SQL-script in SSMS te plakken en vervolgens Hallo script wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-219">Paste hello T-SQL script into SSMS, and then execute hello script.</span></span> <span data-ttu-id="7d3a7-220">Hallo `MEMORY_OPTIMIZED = ON` component CREATE TABLE-instructies zijn essentieel.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-220">hello `MEMORY_OPTIMIZED = ON` clause CREATE TABLE statements are crucial.</span></span> <span data-ttu-id="7d3a7-221">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="7d3a7-221">For example:</span></span>


```
CREATE TABLE [SalesLT].[SalesOrderHeader_inmem](
    [SalesOrderID] int IDENTITY NOT NULL PRIMARY KEY NONCLUSTERED ...,
    ...
) WITH (MEMORY_OPTIMIZED = ON);
```


#### <a name="error-40536"></a><span data-ttu-id="7d3a7-222">Fout 40536</span><span class="sxs-lookup"><span data-stu-id="7d3a7-222">Error 40536</span></span>


<span data-ttu-id="7d3a7-223">Als u fout 40536 krijgt wanneer u Hallo T-SQL-script uitvoert, voert u Hallo T-SQL-script tooverify of Hallo database biedt ondersteuning voor In het geheugen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7d3a7-223">If you get error 40536 when you run hello T-SQL script, run hello following T-SQL script tooverify whether hello database supports In-Memory:</span></span>


```
SELECT DatabasePropertyEx(DB_Name(), 'IsXTPSupported');
```


<span data-ttu-id="7d3a7-224">Een resultaat van **0** betekent dat In het geheugen wordt niet ondersteund, en **1** betekent dat wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-224">A result of **0** means that In-Memory isn't supported, and **1** means that it is supported.</span></span> <span data-ttu-id="7d3a7-225">toodiagnose hello probleem, zorg ervoor dat Hallo-database op Hallo Premium servicecategorie.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-225">toodiagnose hello problem, ensure that hello database is at hello Premium service tier.</span></span>


#### <a name="about-hello-created-memory-optimized-items"></a><span data-ttu-id="7d3a7-226">Over Hallo items geoptimaliseerd voor geheugen gemaakt</span><span class="sxs-lookup"><span data-stu-id="7d3a7-226">About hello created memory-optimized items</span></span>

<span data-ttu-id="7d3a7-227">**Tabellen**: Hallo voorbeeld bevat Hallo geheugen geoptimaliseerde tabellen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7d3a7-227">**Tables**: hello sample contains hello following memory-optimized tables:</span></span>

- <span data-ttu-id="7d3a7-228">SalesLT.Product_inmem</span><span class="sxs-lookup"><span data-stu-id="7d3a7-228">SalesLT.Product_inmem</span></span>
- <span data-ttu-id="7d3a7-229">SalesLT.SalesOrderHeader_inmem</span><span class="sxs-lookup"><span data-stu-id="7d3a7-229">SalesLT.SalesOrderHeader_inmem</span></span>
- <span data-ttu-id="7d3a7-230">SalesLT.SalesOrderDetail_inmem</span><span class="sxs-lookup"><span data-stu-id="7d3a7-230">SalesLT.SalesOrderDetail_inmem</span></span>
- <span data-ttu-id="7d3a7-231">Demo.DemoSalesOrderHeaderSeed</span><span class="sxs-lookup"><span data-stu-id="7d3a7-231">Demo.DemoSalesOrderHeaderSeed</span></span>
- <span data-ttu-id="7d3a7-232">Demo.DemoSalesOrderDetailSeed</span><span class="sxs-lookup"><span data-stu-id="7d3a7-232">Demo.DemoSalesOrderDetailSeed</span></span>


<span data-ttu-id="7d3a7-233">U kunt inspecteren tabellen geoptimaliseerd voor geheugen via Hallo **Objectverkenner** in SSMS.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-233">You can inspect memory-optimized tables through hello **Object Explorer** in SSMS.</span></span> <span data-ttu-id="7d3a7-234">Met de rechtermuisknop op **tabellen** > **Filter** > **filterinstellingen** > **Is geoptimaliseerd voor geheugen**.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-234">Right-click **Tables** > **Filter** > **Filter Settings** > **Is Memory Optimized**.</span></span> <span data-ttu-id="7d3a7-235">Hallo-waarde is gelijk aan 1.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-235">hello value equals 1.</span></span>


<span data-ttu-id="7d3a7-236">Of u kunt een Hallo catalogusweergaven, zoals query:</span><span class="sxs-lookup"><span data-stu-id="7d3a7-236">Or you can query hello catalog views, such as:</span></span>


```
SELECT is_memory_optimized, name, type_desc, durability_desc
    FROM sys.tables
    WHERE is_memory_optimized = 1;
```


<span data-ttu-id="7d3a7-237">**Systeemeigen, gecompileerde opgeslagen procedure**: U kunt SalesLT.usp_InsertSalesOrder_inmem inspecteren via een weergave catalogus query:</span><span class="sxs-lookup"><span data-stu-id="7d3a7-237">**Natively compiled stored procedure**: You can inspect SalesLT.usp_InsertSalesOrder_inmem through a catalog view query:</span></span>


```
SELECT uses_native_compilation, OBJECT_NAME(object_id), definition
    FROM sys.sql_modules
    WHERE uses_native_compilation = 1;
```


&nbsp;

### <a name="run-hello-sample-oltp-workload"></a><span data-ttu-id="7d3a7-238">Hallo voorbeeld OLTP-werkbelasting uitvoeren</span><span class="sxs-lookup"><span data-stu-id="7d3a7-238">Run hello sample OLTP workload</span></span>

<span data-ttu-id="7d3a7-239">het enige verschil tussen de twee volgende Hallo Hallo *opgeslagen procedures* is dat de eerste procedure Hallo versies van Hallo tabellen geoptimaliseerd voor geheugen wordt gebruikt tijdens het Hallo tweede procedure Hallo normale op schijf tabellen gebruikt:</span><span class="sxs-lookup"><span data-stu-id="7d3a7-239">hello only difference between hello following two *stored procedures* is that hello first procedure uses memory-optimized versions of hello tables, while hello second procedure uses hello regular on-disk tables:</span></span>

- <span data-ttu-id="7d3a7-240">SalesLT**.** usp_InsertSalesOrder**_inmem**</span><span class="sxs-lookup"><span data-stu-id="7d3a7-240">SalesLT**.**usp_InsertSalesOrder**_inmem**</span></span>
- <span data-ttu-id="7d3a7-241">SalesLT**.** usp_InsertSalesOrder**_ondisk**</span><span class="sxs-lookup"><span data-stu-id="7d3a7-241">SalesLT**.**usp_InsertSalesOrder**_ondisk**</span></span>


<span data-ttu-id="7d3a7-242">In deze sectie ziet u hoe toouse Hallo handige **ostress.exe** hulpprogramma tooexecute Hallo twee opgeslagen procedures op stress niveaus.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-242">In this section, you see how toouse hello handy **ostress.exe** utility tooexecute hello two stored procedures at stressful levels.</span></span> <span data-ttu-id="7d3a7-243">U kunt vergelijken hoe lang het duurt voor toofinish van Hallo twee stress wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-243">You can compare how long it takes for hello two stress runs toofinish.</span></span>


<span data-ttu-id="7d3a7-244">Wanneer u ostress.exe uitvoert, wordt u aangeraden dat u de parameterwaarden die zijn ontworpen voor beide volgende Hallo doorgeven:</span><span class="sxs-lookup"><span data-stu-id="7d3a7-244">When you run ostress.exe, we recommend that you pass parameter values designed for both of hello following:</span></span>

- <span data-ttu-id="7d3a7-245">Uitvoeren van een groot aantal gelijktijdige verbindingen met behulp - n100.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-245">Run a large number of concurrent connections, by using -n100.</span></span>
- <span data-ttu-id="7d3a7-246">Hebt u elke lus verbinding honderden tijdstippen, door met de parameter - r500.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-246">Have each connection loop hundreds of times, by using -r500.</span></span>


<span data-ttu-id="7d3a7-247">U kunt echter toostart met veel kleiner waarden zoals - n10 en -r50 tooensure dat alles werkt.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-247">However, you might want toostart with much smaller values like -n10 and -r50 tooensure that everything is working.</span></span>


### <a name="script-for-ostressexe"></a><span data-ttu-id="7d3a7-248">Script voor ostress.exe</span><span class="sxs-lookup"><span data-stu-id="7d3a7-248">Script for ostress.exe</span></span>


<span data-ttu-id="7d3a7-249">Deze sectie vindt Hallo T-SQL-script dat is ingesloten in onze ostress.exe vanaf de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-249">This section displays hello T-SQL script that is embedded in our ostress.exe command line.</span></span> <span data-ttu-id="7d3a7-250">Hallo script maakt gebruik van items die zijn gemaakt door Hallo T-SQL-script dat u eerder hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-250">hello script uses items that were created by hello T-SQL script that you installed earlier.</span></span>


<span data-ttu-id="7d3a7-251">Hallo volgende script voegt een verkoop volgorde voorbeeld met vijf artikelen in Hallo volgende geoptimaliseerd voor geheugen *tabellen*:</span><span class="sxs-lookup"><span data-stu-id="7d3a7-251">hello following script inserts a sample sales order with five line items into hello following memory-optimized *tables*:</span></span>

- <span data-ttu-id="7d3a7-252">SalesLT.SalesOrderHeader_inmem</span><span class="sxs-lookup"><span data-stu-id="7d3a7-252">SalesLT.SalesOrderHeader_inmem</span></span>
- <span data-ttu-id="7d3a7-253">SalesLT.SalesOrderDetail_inmem</span><span class="sxs-lookup"><span data-stu-id="7d3a7-253">SalesLT.SalesOrderDetail_inmem</span></span>


```
DECLARE
    @i int = 0,
    @od SalesLT.SalesOrderDetailType_inmem,
    @SalesOrderID int,
    @DueDate datetime2 = sysdatetime(),
    @CustomerID int = rand() * 8000,
    @BillToAddressID int = rand() * 10000,
    @ShipToAddressID int = rand() * 10000;

INSERT INTO @od
    SELECT OrderQty, ProductID
    FROM Demo.DemoSalesOrderDetailSeed
    WHERE OrderID= cast((rand()*60) as int);

WHILE (@i < 20)
begin;
    EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT,
        @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od;
    SET @i = @i + 1;
end
```


<span data-ttu-id="7d3a7-254">Hallo toomake *_ondisk* versie van Hallo voorgaande T-SQL-script voor ostress.exe, vervangt u beide exemplaren van Hallo *_inmem* subtekenreeks met *_ondisk*.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-254">toomake hello *_ondisk* version of hello preceding T-SQL script for ostress.exe, you would replace both occurrences of hello *_inmem* substring with *_ondisk*.</span></span> <span data-ttu-id="7d3a7-255">Deze vervangingen van invloed op Hallo namen van tabellen en opgeslagen procedures.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-255">These replacements affect hello names of tables and stored procedures.</span></span>


### <a name="install-rml-utilities-and-ostress"></a><span data-ttu-id="7d3a7-256">Hulpprogramma's voor RML en ostress installeren</span><span class="sxs-lookup"><span data-stu-id="7d3a7-256">Install RML utilities and ostress</span></span>


<span data-ttu-id="7d3a7-257">In het ideale geval zou u toorun ostress.exe plannen op Azure een virtuele machine (VM).</span><span class="sxs-lookup"><span data-stu-id="7d3a7-257">Ideally, you would plan toorun ostress.exe on an Azure virtual machine (VM).</span></span> <span data-ttu-id="7d3a7-258">Maakt u een [Azure VM](https://azure.microsoft.com/documentation/services/virtual-machines/) in Hallo dezelfde Azure geografische regio waarin uw AdventureWorksLT-database zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-258">You would create an [Azure VM](https://azure.microsoft.com/documentation/services/virtual-machines/) in hello same Azure geographic region where your AdventureWorksLT database resides.</span></span> <span data-ttu-id="7d3a7-259">Maar u kunt in plaats daarvan ostress.exe op uw laptop uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-259">But you can run ostress.exe on your laptop instead.</span></span>


<span data-ttu-id="7d3a7-260">Op Hallo VM of op wat u host kiezen, Hallo Replay Markup Language (RML)-hulpprogramma's installeren.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-260">On hello VM, or on whatever host you choose, install hello Replay Markup Language (RML) utilities.</span></span> <span data-ttu-id="7d3a7-261">Hallo-hulpprogramma's omvatten ostress.exe.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-261">hello utilities include ostress.exe.</span></span>

<span data-ttu-id="7d3a7-262">Zie voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="7d3a7-262">For more information, see:</span></span>
- <span data-ttu-id="7d3a7-263">Hallo ostress.exe discussie in [voorbeelddatabase voor In-geheugen OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span><span class="sxs-lookup"><span data-stu-id="7d3a7-263">hello ostress.exe discussion in [Sample Database for In-Memory OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span></span>
- <span data-ttu-id="7d3a7-264">[De voorbeelddatabase voor In-geheugen OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span><span class="sxs-lookup"><span data-stu-id="7d3a7-264">[Sample Database for In-Memory OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span></span>
- <span data-ttu-id="7d3a7-265">Hallo [blog voor het installeren van ostress.exe](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx).</span><span class="sxs-lookup"><span data-stu-id="7d3a7-265">hello [blog for installing ostress.exe](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx).</span></span>



<!--
dn511655.aspx is for SQL 2014,
[Extensions tooAdventureWorks tooDemonstrate In-Memory OLTP]
(http://msdn.microsoft.com/library/dn511655&#x28;v=sql.120&#x29;.aspx)

whereas for SQL 2016+
[Sample Database for In-Memory OLTP]
(http://msdn.microsoft.com/library/mt465764.aspx)
-->



### <a name="run-hello-inmem-stress-workload-first"></a><span data-ttu-id="7d3a7-266">Voer Hallo *_inmem* eerst stresstest voor de werkbelasting</span><span class="sxs-lookup"><span data-stu-id="7d3a7-266">Run hello *_inmem* stress workload first</span></span>


<span data-ttu-id="7d3a7-267">U kunt een *RML Cmd vragen* venster toorun onze ostress.exe vanaf de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-267">You can use an *RML Cmd Prompt* window toorun our ostress.exe command line.</span></span> <span data-ttu-id="7d3a7-268">Hallo opdrachtregelparameters direct ostress naar:</span><span class="sxs-lookup"><span data-stu-id="7d3a7-268">hello command-line parameters direct ostress to:</span></span>

- <span data-ttu-id="7d3a7-269">100 verbindingen gelijktijdig worden uitgevoerd (-n100).</span><span class="sxs-lookup"><span data-stu-id="7d3a7-269">Run 100 connections concurrently (-n100).</span></span>
- <span data-ttu-id="7d3a7-270">Elke verbinding 50 keer Hallo T-SQL-script uitvoeren (-r50).</span><span class="sxs-lookup"><span data-stu-id="7d3a7-270">Have each connection run hello T-SQL script 50 times (-r50).</span></span>


```
ostress.exe -n100 -r50 -S<servername>.database.windows.net -U<login> -P<password> -d<database> -q -Q"DECLARE @i int = 0, @od SalesLT.SalesOrderDetailType_inmem, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand()* 10000; INSERT INTO @od SELECT OrderQty, ProductID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*60) as int); WHILE (@i < 20) begin; EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od; set @i += 1; end"
```


<span data-ttu-id="7d3a7-271">toorun hello voorgaande ostress.exe vanaf de opdrachtregel:</span><span class="sxs-lookup"><span data-stu-id="7d3a7-271">toorun hello preceding ostress.exe command line:</span></span>


1. <span data-ttu-id="7d3a7-272">Hallo database gegevens inhoud herstellen door het uitvoeren van volgende opdracht in SSMS, toodelete Hallo alle Hallo-gegevens die door een eerder uitgevoerde wordt ingevoegd:</span><span class="sxs-lookup"><span data-stu-id="7d3a7-272">Reset hello database data content by running hello following command in SSMS, toodelete all hello data that was inserted by any previous runs:</span></span>

    ``` tsql
    EXECUTE Demo.usp_DemoReset;
    ```

2. <span data-ttu-id="7d3a7-273">De tekst hello Hallo voorgaande ostress.exe opdrachtregel tooyour Klembord kopiëren.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-273">Copy hello text of hello preceding ostress.exe command line tooyour clipboard.</span></span>

3. <span data-ttu-id="7d3a7-274">Vervang Hallo `<placeholders>` voor Hallo parameters -S - u. -P -d Hello echte waarden te corrigeren.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-274">Replace hello `<placeholders>` for hello parameters -S -U -P -d with hello correct real values.</span></span>

4. <span data-ttu-id="7d3a7-275">De bewerkte opdrachtregel uitvoeren in een venster RML Cmd.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-275">Run your edited command line in an RML Cmd window.</span></span>


#### <a name="result-is-a-duration"></a><span data-ttu-id="7d3a7-276">Resultaat is een duur</span><span class="sxs-lookup"><span data-stu-id="7d3a7-276">Result is a duration</span></span>


<span data-ttu-id="7d3a7-277">Wanneer ostress.exe is voltooid, schrijft de front-end Hallo duur uitvoeren als de laatste regel van uitvoer in Hallo RML Cmd-venster.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-277">When ostress.exe finishes, it writes hello run duration as its final line of output in hello RML Cmd window.</span></span> <span data-ttu-id="7d3a7-278">Bijvoorbeeld, een kortere testuitvoering geduurd ongeveer 1,5 minuten:</span><span class="sxs-lookup"><span data-stu-id="7d3a7-278">For example, a shorter test run lasted about 1.5 minutes:</span></span>

`11/12/15 00:35:00.873 [0x000030A8] OSTRESS exiting normally, elapsed time: 00:01:31.867`


#### <a name="reset-edit-for-ondisk-then-rerun"></a><span data-ttu-id="7d3a7-279">Opnieuw instellen en bewerken voor *_ondisk*, vervolgens opnieuw uitvoeren</span><span class="sxs-lookup"><span data-stu-id="7d3a7-279">Reset, edit for *_ondisk*, then rerun</span></span>


<span data-ttu-id="7d3a7-280">Nadat u Hallo resultaat van Hallo hebt *_inmem* uitvoeren, uitvoeren van de volgende stappen uit voor Hallo Hallo *_ondisk* uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="7d3a7-280">After you have hello result from hello *_inmem* run, perform hello following steps for hello *_ondisk* run:</span></span>


1. <span data-ttu-id="7d3a7-281">Hallo-database opnieuw instellen door te voeren na de opdracht in SSMS toodelete Hallo alle Hallo gegevens dat is ingevoegd door Hallo vorige uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="7d3a7-281">Reset hello database by running hello following command in SSMS toodelete all hello data that was inserted by hello previous run:</span></span>
```
EXECUTE Demo.usp_DemoReset;
```

2. <span data-ttu-id="7d3a7-282">Hallo ostress.exe opdrachtregel tooreplace alle bewerken *_inmem* met *_ondisk*.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-282">Edit hello ostress.exe command line tooreplace all *_inmem* with *_ondisk*.</span></span>

3. <span data-ttu-id="7d3a7-283">Ostress.exe voor Hallo tweede keer opnieuw en Hallo duur resultaat vast te leggen.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-283">Rerun ostress.exe for hello second time, and capture hello duration result.</span></span>

4. <span data-ttu-id="7d3a7-284">Hallo-database (voor voorzichtig te verwijderen welke een grote hoeveelheid testgegevens kunnen worden) opnieuw opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-284">Again, reset hello database (for responsibly deleting what can be a large amount of test data).</span></span>


#### <a name="expected-comparison-results"></a><span data-ttu-id="7d3a7-285">Van de verwachte vergelijkingsresultaten</span><span class="sxs-lookup"><span data-stu-id="7d3a7-285">Expected comparison results</span></span>

<span data-ttu-id="7d3a7-286">Onze tests In het geheugen is gebleken dat prestaties verbeterd door **negen keer** voor deze eenvoudig werkbelasting met ostress uitgevoerd op een virtuele machine van Azure in Hallo dezelfde Azure-regio als Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-286">Our In-Memory tests have shown that performance improved by **nine times** for this simplistic workload, with ostress running on an Azure VM in hello same Azure region as hello database.</span></span>

<a id="install_analytics_manuallink" name="install_analytics_manuallink"></a>

&nbsp;

## <a name="2-install-hello-in-memory-analytics-sample"></a><span data-ttu-id="7d3a7-287">2. Hallo In-Memory Analytics voorbeeld installeren</span><span class="sxs-lookup"><span data-stu-id="7d3a7-287">2. Install hello In-Memory Analytics sample</span></span>


<span data-ttu-id="7d3a7-288">In deze sectie maakt vergelijken u hello i/o- en statistieken resultaten wanneer u een columnstore-index ten opzichte van een traditionele b-tree-index.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-288">In this section, you compare hello IO and statistics results when you're using a columnstore index versus a traditional b-tree index.</span></span>


<span data-ttu-id="7d3a7-289">Voor realtime analyses op een OLTP-werkbelasting is het vaak best toouse een niet-geclusterde columnstore-index.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-289">For real-time analytics on an OLTP workload, it's often best toouse a nonclustered columnstore index.</span></span> <span data-ttu-id="7d3a7-290">Zie voor meer informatie [Columnstore-indexen beschreven](http://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="7d3a7-290">For details, see [Columnstore Indexes Described](http://msdn.microsoft.com/library/gg492088.aspx).</span></span>



### <a name="prepare-hello-columnstore-analytics-test"></a><span data-ttu-id="7d3a7-291">Hallo columnstore analytics test voorbereiden</span><span class="sxs-lookup"><span data-stu-id="7d3a7-291">Prepare hello columnstore analytics test</span></span>


1. <span data-ttu-id="7d3a7-292">Hallo toocreate met Azure portal een nieuwe database AdventureWorksLT van Hallo voorbeeld gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-292">Use hello Azure portal toocreate a fresh AdventureWorksLT database from hello sample.</span></span>
 - <span data-ttu-id="7d3a7-293">Gebruikt u de exacte naam.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-293">Use that exact name.</span></span>
 - <span data-ttu-id="7d3a7-294">Kies een Premium servicecategorie.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-294">Choose any Premium service tier.</span></span>

2. <span data-ttu-id="7d3a7-295">Kopiëren Hallo [sql_in memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) tooyour Klembord.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-295">Copy hello [sql_in-memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) tooyour clipboard.</span></span>
 - <span data-ttu-id="7d3a7-296">Hallo T-SQL-script maakt Hallo nodig In het geheugen objecten in de voorbeelddatabase van Hallo AdventureWorksLT die u in stap 1 hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-296">hello T-SQL script creates hello necessary In-Memory objects in hello AdventureWorksLT sample database that you created in step 1.</span></span>
 - <span data-ttu-id="7d3a7-297">Hallo script maakt Hallo dimensietabel en twee feitentabellen.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-297">hello script creates hello Dimension table and two fact tables.</span></span> <span data-ttu-id="7d3a7-298">Hallo feitentabellen worden ingevuld met 3.5 miljoen rijen.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-298">hello fact tables are populated with 3.5 million rows each.</span></span>
 - <span data-ttu-id="7d3a7-299">Hallo-script kan toocomplete 15 minuten duren.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-299">hello script might take 15 minutes toocomplete.</span></span>

3. <span data-ttu-id="7d3a7-300">Hallo T-SQL-script in SSMS te plakken en vervolgens Hallo script wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-300">Paste hello T-SQL script into SSMS, and then execute hello script.</span></span> <span data-ttu-id="7d3a7-301">Hallo **COLUMNSTORE** -sleutelwoord in Hallo **CREATE INDEX** instructie is van cruciaal belang, zoals in:</span><span class="sxs-lookup"><span data-stu-id="7d3a7-301">hello **COLUMNSTORE** keyword in hello **CREATE INDEX** statement is crucial, as in:</span></span><br/>`CREATE NONCLUSTERED COLUMNSTORE INDEX ...;`

4. <span data-ttu-id="7d3a7-302">AdventureWorksLT toocompatibility niveau 130 instellen:</span><span class="sxs-lookup"><span data-stu-id="7d3a7-302">Set AdventureWorksLT toocompatibility level 130:</span></span><br/>`ALTER DATABASE AdventureworksLT SET compatibility_level = 130;`

    <span data-ttu-id="7d3a7-303">Niveau 130 is niet direct gerelateerd tooIn geheugen functies.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-303">Level 130 is not directly related tooIn-Memory features.</span></span> <span data-ttu-id="7d3a7-304">Maar niveau 130 biedt doorgaans sneller queryprestaties dan 120.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-304">But level 130 generally provides faster query performance than 120.</span></span>


#### <a name="key-tables-and-columnstore-indexes"></a><span data-ttu-id="7d3a7-305">Belangrijkste tabellen en columnstore-indexen</span><span class="sxs-lookup"><span data-stu-id="7d3a7-305">Key tables and columnstore indexes</span></span>


- <span data-ttu-id="7d3a7-306">dbo. FactResellerSalesXL_CCI is een tabel die een geclusterde columnstore-index die over compressie op Hallo geavanceerde beschikt *gegevens* niveau.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-306">dbo.FactResellerSalesXL_CCI is a table that has a clustered columnstore index, which has advanced compression at hello *data* level.</span></span>

- <span data-ttu-id="7d3a7-307">dbo. FactResellerSalesXL_PageCompressed is een tabel met een equivalent reguliere geclusterde index, die alleen op Hallo is gecomprimeerd *pagina* niveau.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-307">dbo.FactResellerSalesXL_PageCompressed is a table that has an equivalent regular clustered index, which is compressed only at hello *page* level.</span></span>


#### <a name="key-queries-toocompare-hello-columnstore-index"></a><span data-ttu-id="7d3a7-308">Sleutel query's toocompare hello columnstore-index</span><span class="sxs-lookup"><span data-stu-id="7d3a7-308">Key queries toocompare hello columnstore index</span></span>


<span data-ttu-id="7d3a7-309">Er zijn [verschillende typen van de T-SQL-query die u kunt uitvoeren](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql) toosee voor verbeterde prestaties.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-309">There are [several T-SQL query types that you can run](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql) toosee performance improvements.</span></span> <span data-ttu-id="7d3a7-310">In stap 2 van Hallo T-SQL-script, betaalt u aandacht toothis paar van query's.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-310">In step 2 in hello T-SQL script, pay attention toothis pair of queries.</span></span> <span data-ttu-id="7d3a7-311">Verschillen slechts op één regel:</span><span class="sxs-lookup"><span data-stu-id="7d3a7-311">They differ only on one line:</span></span>


- `FROM FactResellerSalesXL_PageCompressed a`
- `FROM FactResellerSalesXL_CCI a`


<span data-ttu-id="7d3a7-312">Een geclusterde columnstore-index wordt in Hallo FactResellerSalesXL\_CCI tabel.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-312">A clustered columnstore index is in hello FactResellerSalesXL\_CCI table.</span></span>

<span data-ttu-id="7d3a7-313">Hallo volgende T-SQL-script fragment wordt afgedrukt statistieken voor i/o en tijd voor de query Hallo van elke tabel.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-313">hello following T-SQL script excerpt prints statistics for IO and TIME for hello query of each table.</span></span>


```
/*********************************************************************
Step 2 -- Overview
-- Page Compressed BTree table v/s Columnstore table performance differences
-- Enable actual Query Plan in order toosee Plan differences when Executing
*/
-- Ensure Database is in 130 compatibility mode
ALTER DATABASE AdventureworksLT SET compatibility_level = 130
GO

-- Execute a typical query that joins hello Fact Table with dimension tables
-- Note this query will run on hello Page Compressed table, Note down hello time
SET STATISTICS IO ON
SET STATISTICS TIME ON
GO

SELECT c.Year
    ,e.ProductCategoryKey
    ,FirstName + ' ' + LastName AS FullName
    ,count(SalesOrderNumber) AS NumSales
    ,sum(SalesAmount) AS TotalSalesAmt
    ,Avg(SalesAmount) AS AvgSalesAmt
    ,count(DISTINCT SalesOrderNumber) AS NumOrders
    ,count(DISTINCT a.CustomerKey) AS CountCustomers
FROM FactResellerSalesXL_PageCompressed a
INNER JOIN DimProduct b ON b.ProductKey = a.ProductKey
INNER JOIN DimCustomer d ON d.CustomerKey = a.CustomerKey
Inner JOIN DimProductSubCategory e on e.ProductSubcategoryKey = b.ProductSubcategoryKey
INNER JOIN DimDate c ON c.DateKey = a.OrderDateKey
GROUP BY e.ProductCategoryKey,c.Year,d.CustomerKey,d.FirstName,d.LastName
GO
SET STATISTICS IO OFF
SET STATISTICS TIME OFF
GO


-- This is hello same Prior query on a table with a clustered columnstore index CCI
-- hello comparison numbers are even more dramatic hello larger hello table is (this is an 11 million row table only)
SET STATISTICS IO ON
SET STATISTICS TIME ON
GO
SELECT c.Year
    ,e.ProductCategoryKey
    ,FirstName + ' ' + LastName AS FullName
    ,count(SalesOrderNumber) AS NumSales
    ,sum(SalesAmount) AS TotalSalesAmt
    ,Avg(SalesAmount) AS AvgSalesAmt
    ,count(DISTINCT SalesOrderNumber) AS NumOrders
    ,count(DISTINCT a.CustomerKey) AS CountCustomers
FROM FactResellerSalesXL_CCI a
INNER JOIN DimProduct b ON b.ProductKey = a.ProductKey
INNER JOIN DimCustomer d ON d.CustomerKey = a.CustomerKey
Inner JOIN DimProductSubCategory e on e.ProductSubcategoryKey = b.ProductSubcategoryKey
INNER JOIN DimDate c ON c.DateKey = a.OrderDateKey
GROUP BY e.ProductCategoryKey,c.Year,d.CustomerKey,d.FirstName,d.LastName
GO

SET STATISTICS IO OFF
SET STATISTICS TIME OFF
GO
```

<span data-ttu-id="7d3a7-314">In een database met Hallo P2 prijscategorie verwacht u dat ongeveer negen keer Hallo prestatieverbetering te bereiken voor deze query met behulp van de geclusterde columnstore-index Hallo vergeleken met traditionele Hallo-index.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-314">In a database with hello P2 pricing tier, you can expect about nine times hello performance gain for this query by using hello clustered columnstore index compared with hello traditional index.</span></span> <span data-ttu-id="7d3a7-315">Met P15, verwacht u dat ongeveer 57 maal Hallo prestatieverbetering te bereiken met behulp van Hallo columnstore-index.</span><span class="sxs-lookup"><span data-stu-id="7d3a7-315">With P15, you can expect about 57 times hello performance gain by using hello columnstore index.</span></span>



## <a name="next-steps"></a><span data-ttu-id="7d3a7-316">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7d3a7-316">Next steps</span></span>

- [<span data-ttu-id="7d3a7-317">1 voor snel starten: In het geheugen OLTP-technologieën voor betere prestaties van de T-SQL</span><span class="sxs-lookup"><span data-stu-id="7d3a7-317">Quick Start 1: In-Memory OLTP Technologies for Faster T-SQL Performance</span></span>](http://msdn.microsoft.com/library/mt694156.aspx)

- [<span data-ttu-id="7d3a7-318">Gebruik In het geheugen OLTP in een bestaande Azure SQL-toepassing</span><span class="sxs-lookup"><span data-stu-id="7d3a7-318">Use In-Memory OLTP in an existing Azure SQL application</span></span>](sql-database-in-memory-oltp-migration.md)

- <span data-ttu-id="7d3a7-319">[Opslag van de monitor In-geheugen OLTP](sql-database-in-memory-oltp-monitoring.md) voor In-geheugen OLTP</span><span class="sxs-lookup"><span data-stu-id="7d3a7-319">[Monitor In-Memory OLTP storage](sql-database-in-memory-oltp-monitoring.md) for In-Memory OLTP</span></span>


## <a name="additional-resources"></a><span data-ttu-id="7d3a7-320">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="7d3a7-320">Additional resources</span></span>

#### <a name="deeper-information"></a><span data-ttu-id="7d3a7-321">Meer gedetailleerde informatie</span><span class="sxs-lookup"><span data-stu-id="7d3a7-321">Deeper information</span></span>

- [<span data-ttu-id="7d3a7-322">Meer informatie over hoe Quorum wordt verdubbeld sleutel database werkbelasting tijdens DTU verlagen door 70% met In-geheugen OLTP in SQL-Database</span><span class="sxs-lookup"><span data-stu-id="7d3a7-322">Learn how Quorum doubles key database’s workload while lowering DTU by 70% with In-Memory OLTP in SQL Database</span></span>](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)

- [<span data-ttu-id="7d3a7-323">In het geheugen OLTP in Azure SQL Database-blogbericht</span><span class="sxs-lookup"><span data-stu-id="7d3a7-323">In-Memory OLTP in Azure SQL Database Blog Post</span></span>](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)

- [<span data-ttu-id="7d3a7-324">Meer informatie over In-geheugen OLTP</span><span class="sxs-lookup"><span data-stu-id="7d3a7-324">Learn about In-Memory OLTP</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)

- [<span data-ttu-id="7d3a7-325">Meer informatie over de columnstore-indexen</span><span class="sxs-lookup"><span data-stu-id="7d3a7-325">Learn about columnstore indexes</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)

- [<span data-ttu-id="7d3a7-326">Meer informatie over realtime operationele analytics</span><span class="sxs-lookup"><span data-stu-id="7d3a7-326">Learn about real-time operational analytics</span></span>](http://msdn.microsoft.com/library/dn817827.aspx)

- <span data-ttu-id="7d3a7-327">Zie [algemene patronen van de werkbelasting en overwegingen bij migratie](http://msdn.microsoft.com/library/dn673538.aspx) (waarin wordt beschreven werkbelasting patronen In het geheugen OLTP waarin vaak aanzienlijke prestatieverbeteringen biedt)</span><span class="sxs-lookup"><span data-stu-id="7d3a7-327">See [Common Workload Patterns and Migration Considerations](http://msdn.microsoft.com/library/dn673538.aspx) (which describes workload patterns where In-Memory OLTP commonly provides significant performance gains)</span></span>

#### <a name="application-design"></a><span data-ttu-id="7d3a7-328">Het ontwerp van toepassing</span><span class="sxs-lookup"><span data-stu-id="7d3a7-328">Application design</span></span>

- [<span data-ttu-id="7d3a7-329">In het geheugen OLTP (optimalisatie In het geheugen)</span><span class="sxs-lookup"><span data-stu-id="7d3a7-329">In-Memory OLTP (In-Memory Optimization)</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)

- [<span data-ttu-id="7d3a7-330">Gebruik In het geheugen OLTP in een bestaande Azure SQL-toepassing</span><span class="sxs-lookup"><span data-stu-id="7d3a7-330">Use In-Memory OLTP in an existing Azure SQL application</span></span>](sql-database-in-memory-oltp-migration.md)

#### <a name="tools"></a><span data-ttu-id="7d3a7-331">Hulpprogramma's</span><span class="sxs-lookup"><span data-stu-id="7d3a7-331">Tools</span></span>

- [<span data-ttu-id="7d3a7-332">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7d3a7-332">Azure portal</span></span>](https://portal.azure.com/)

- [<span data-ttu-id="7d3a7-333">SQL Server Management Studio (SSMS)</span><span class="sxs-lookup"><span data-stu-id="7d3a7-333">SQL Server Management Studio (SSMS)</span></span>](https://msdn.microsoft.com/library/mt238290.aspx)

- [<span data-ttu-id="7d3a7-334">SQL Server Data Tools (SSDT)</span><span class="sxs-lookup"><span data-stu-id="7d3a7-334">SQL Server Data Tools (SSDT)</span></span>](http://msdn.microsoft.com/library/mt204009.aspx)
