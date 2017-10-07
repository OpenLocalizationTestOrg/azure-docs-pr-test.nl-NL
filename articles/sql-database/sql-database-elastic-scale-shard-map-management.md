---
title: aaaScale uit een Azure SQL database | Microsoft Docs
description: Hoe toouse Hallo ShardMapManager, clientbibliotheek voor elastische database
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 0e9d647a-9ba9-4875-aa22-662d01283439
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 4cf670d42ad7ded98fb8d6f0830154587dd2c6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-out-databases-with-hello-shard-map-manager"></a><span data-ttu-id="e3460-103">Databases met Hallo shard-toewijzing manager uitbreiden</span><span class="sxs-lookup"><span data-stu-id="e3460-103">Scale out databases with hello shard map manager</span></span>
<span data-ttu-id="e3460-104">tooeasily scale-out-databases op SQL Azure gebruiken een manager shard-toewijzing.</span><span class="sxs-lookup"><span data-stu-id="e3460-104">tooeasily scale out databases on SQL Azure, use a shard map manager.</span></span> <span data-ttu-id="e3460-105">Hallo shard-toewijzing manager is een speciale database waarin gegevens over alle shards (databases) in een set shard globale toewijzing worden bijgehouden.</span><span class="sxs-lookup"><span data-stu-id="e3460-105">hello shard map manager is a special database that maintains global mapping information about all shards (databases) in a shard set.</span></span> <span data-ttu-id="e3460-106">Hallo metagegevens kan een tooconnect toohello juiste toepassingsdatabase op basis van de waarde Hallo Hallo **sharding sleutel**.</span><span class="sxs-lookup"><span data-stu-id="e3460-106">hello metadata allows an application tooconnect toohello correct database based upon hello value of hello **sharding key**.</span></span> <span data-ttu-id="e3460-107">Bovendien elke shard in Hallo set bevat kaarten die Hallo lokale shard-gegevens bijhouden (ook wel **shardlets**).</span><span class="sxs-lookup"><span data-stu-id="e3460-107">In addition, every shard in hello set contains maps that track hello local shard data (known as **shardlets**).</span></span> 

![Beheer van shard-kaart](./media/sql-database-elastic-scale-shard-map-management/glossary.png)

<span data-ttu-id="e3460-109">Inzicht in hoe deze toewijzingen worden opgebouwd is essentieel tooshard kaart management.</span><span class="sxs-lookup"><span data-stu-id="e3460-109">Understanding how these maps are constructed is essential tooshard map management.</span></span> <span data-ttu-id="e3460-110">Dit wordt gedaan met behulp van Hallo [ShardMapManager klasse](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)vindt u in Hallo [clientbibliotheek voor elastische Database](sql-database-elastic-database-client-library.md) toomanage shard wordt toegewezen.</span><span class="sxs-lookup"><span data-stu-id="e3460-110">This is done using hello [ShardMapManager class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx), found in hello [Elastic Database client library](sql-database-elastic-database-client-library.md) toomanage shard maps.</span></span>  

## <a name="shard-maps-and-shard-mappings"></a><span data-ttu-id="e3460-111">Shard-kaarten en shard-toewijzingen</span><span class="sxs-lookup"><span data-stu-id="e3460-111">Shard maps and shard mappings</span></span>
<span data-ttu-id="e3460-112">U moet voor elke shard Hallo type shard-toewijzing toocreate selecteren.</span><span class="sxs-lookup"><span data-stu-id="e3460-112">For each shard, you must select hello type of shard map toocreate.</span></span> <span data-ttu-id="e3460-113">Hallo keuze is afhankelijk van Hallo database-architectuur:</span><span class="sxs-lookup"><span data-stu-id="e3460-113">hello choice depends on hello database architecture:</span></span> 

1. <span data-ttu-id="e3460-114">Één tenant per database</span><span class="sxs-lookup"><span data-stu-id="e3460-114">Single tenant per database</span></span>  
2. <span data-ttu-id="e3460-115">Meerdere tenants per database (twee typen):</span><span class="sxs-lookup"><span data-stu-id="e3460-115">Multiple tenants per database (two types):</span></span>
   1. <span data-ttu-id="e3460-116">Toewijzing van de lijst</span><span class="sxs-lookup"><span data-stu-id="e3460-116">List mapping</span></span>
   2. <span data-ttu-id="e3460-117">Bereik toewijzing</span><span class="sxs-lookup"><span data-stu-id="e3460-117">Range mapping</span></span>

<span data-ttu-id="e3460-118">Voor een model voor één tenant, maakt u een **lijst toewijzing** shard-toewijzing.</span><span class="sxs-lookup"><span data-stu-id="e3460-118">For a single-tenant model, create a **list mapping** shard map.</span></span> <span data-ttu-id="e3460-119">Hallo één tenant model wijst één database per tenant.</span><span class="sxs-lookup"><span data-stu-id="e3460-119">hello single-tenant model assigns one database per tenant.</span></span> <span data-ttu-id="e3460-120">Dit is een doeltreffend model voor SaaS-ontwikkelaars aangezien vereenvoudigt het beheer.</span><span class="sxs-lookup"><span data-stu-id="e3460-120">This is an effective model for SaaS developers as it simplifies management.</span></span>

![Toewijzing van de lijst][1]

<span data-ttu-id="e3460-122">Hallo multitenant model wijst verschillende tenants tooa één database (en u kunt groepen van tenants verdelen over meerdere databases).</span><span class="sxs-lookup"><span data-stu-id="e3460-122">hello multi-tenant model assigns several tenants tooa single database (and you can distribute groups of tenants across multiple databases).</span></span> <span data-ttu-id="e3460-123">Dit model gebruiken wanneer u verwacht dat elke tenant toohave kleine hoeveelheden gegevens nodig heeft.</span><span class="sxs-lookup"><span data-stu-id="e3460-123">Use this model when you expect each tenant toohave small data needs.</span></span> <span data-ttu-id="e3460-124">In dit model we een bereik van het gebruik van tenants tooa database toewijzen **bereik toewijzing**.</span><span class="sxs-lookup"><span data-stu-id="e3460-124">In this model, we assign a range of tenants tooa database using **range mapping**.</span></span> 

![Bereik toewijzing][2]

<span data-ttu-id="e3460-126">Of u kunt implementeren met een multitenant database model met een *lijst toewijzing* tooassign meerdere tenants tooa één database.</span><span class="sxs-lookup"><span data-stu-id="e3460-126">Or you can implement a multi-tenant database model using a *list mapping* tooassign multiple tenants tooa single database.</span></span> <span data-ttu-id="e3460-127">Bijvoorbeeld, DB1 is gebruikte toostore informatie over de tenant-id 1 en 5 en DB2 slaat gegevens voor de tenant 7- en 10.</span><span class="sxs-lookup"><span data-stu-id="e3460-127">For example, DB1 is used toostore information about tenant id 1 and 5, and DB2 stores data for tenant 7 and tenant 10.</span></span> 

![Muliple tenants in één DB][3] 

### <a name="supported-net-types-for-sharding-keys"></a><span data-ttu-id="e3460-129">Ondersteunde .net-typen voor sharding-sleutels</span><span class="sxs-lookup"><span data-stu-id="e3460-129">Supported .Net types for sharding keys</span></span>
<span data-ttu-id="e3460-130">Elastische Scale ondersteuning Hallo volgende .net Framework-typen als sharding sleutels:</span><span class="sxs-lookup"><span data-stu-id="e3460-130">Elastic Scale support hello following .Net Framework types as sharding keys:</span></span>

* <span data-ttu-id="e3460-131">geheel getal</span><span class="sxs-lookup"><span data-stu-id="e3460-131">integer</span></span>
* <span data-ttu-id="e3460-132">lang</span><span class="sxs-lookup"><span data-stu-id="e3460-132">long</span></span>
* <span data-ttu-id="e3460-133">GUID</span><span class="sxs-lookup"><span data-stu-id="e3460-133">guid</span></span>
* <span data-ttu-id="e3460-134">Byte]</span><span class="sxs-lookup"><span data-stu-id="e3460-134">byte[]</span></span>  
* <span data-ttu-id="e3460-135">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="e3460-135">datetime</span></span>
* <span data-ttu-id="e3460-136">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="e3460-136">timespan</span></span>
* <span data-ttu-id="e3460-137">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="e3460-137">datetimeoffset</span></span>

### <a name="list-and-range-shard-maps"></a><span data-ttu-id="e3460-138">Lijst met en bereik shard-kaarten</span><span class="sxs-lookup"><span data-stu-id="e3460-138">List and range shard maps</span></span>
<span data-ttu-id="e3460-139">Shard maps kunnen worden opgesteld met **lijsten met afzonderlijke sharding waarden sleutel**, of ze kunnen worden opgesteld met **bereiken van sharding waarden sleutel**.</span><span class="sxs-lookup"><span data-stu-id="e3460-139">Shard maps can be constructed using **lists of individual sharding key values**, or they can be constructed using **ranges of sharding key values**.</span></span> 

### <a name="list-shard-maps"></a><span data-ttu-id="e3460-140">Lijst shard maps</span><span class="sxs-lookup"><span data-stu-id="e3460-140">List shard maps</span></span>
<span data-ttu-id="e3460-141">**Shards** bevatten **shardlets** en Hallo toewijzing van shardlets tooshards wordt onderhouden door een shard-toewijzing.</span><span class="sxs-lookup"><span data-stu-id="e3460-141">**Shards** contain **shardlets** and hello mapping of shardlets tooshards is maintained by a shard map.</span></span> <span data-ttu-id="e3460-142">Een **lijst shard-toewijzing** is een koppeling tussen Hallo afzonderlijke sleutelwaarden die Hallo shardlets identificeren en Hallo-databases die als shards fungeren.</span><span class="sxs-lookup"><span data-stu-id="e3460-142">A **list shard map** is an association between hello individual key values that identify hello shardlets and hello databases that serve as shards.</span></span>  <span data-ttu-id="e3460-143">**Lijst met toewijzingen** zijn expliciete en andere sleutelwaarden kunnen worden toegewezen toohello dezelfde database.</span><span class="sxs-lookup"><span data-stu-id="e3460-143">**List mappings** are explicit and different key values can be mapped toohello same database.</span></span> <span data-ttu-id="e3460-144">Bijvoorbeeld: sleutel 1 toegewezen tooDatabase A en sleutelwaarden 3 en 6 verwijst naar Database B.</span><span class="sxs-lookup"><span data-stu-id="e3460-144">For example, key 1 maps tooDatabase A, and key values 3 and 6 both reference Database B.</span></span>

| <span data-ttu-id="e3460-145">Sleutel</span><span class="sxs-lookup"><span data-stu-id="e3460-145">Key</span></span> | <span data-ttu-id="e3460-146">Shard-locatie</span><span class="sxs-lookup"><span data-stu-id="e3460-146">Shard Location</span></span> |
| --- | --- |
| <span data-ttu-id="e3460-147">1</span><span class="sxs-lookup"><span data-stu-id="e3460-147">1</span></span> |<span data-ttu-id="e3460-148">Database_A</span><span class="sxs-lookup"><span data-stu-id="e3460-148">Database_A</span></span> |
| <span data-ttu-id="e3460-149">3</span><span class="sxs-lookup"><span data-stu-id="e3460-149">3</span></span> |<span data-ttu-id="e3460-150">Database_B</span><span class="sxs-lookup"><span data-stu-id="e3460-150">Database_B</span></span> |
| <span data-ttu-id="e3460-151">4</span><span class="sxs-lookup"><span data-stu-id="e3460-151">4</span></span> |<span data-ttu-id="e3460-152">Database_C</span><span class="sxs-lookup"><span data-stu-id="e3460-152">Database_C</span></span> |
| <span data-ttu-id="e3460-153">6</span><span class="sxs-lookup"><span data-stu-id="e3460-153">6</span></span> |<span data-ttu-id="e3460-154">Database_B</span><span class="sxs-lookup"><span data-stu-id="e3460-154">Database_B</span></span> |
| <span data-ttu-id="e3460-155">...</span><span class="sxs-lookup"><span data-stu-id="e3460-155">...</span></span> |<span data-ttu-id="e3460-156">...</span><span class="sxs-lookup"><span data-stu-id="e3460-156">...</span></span> |

### <a name="range-shard-maps"></a><span data-ttu-id="e3460-157">Bereik shard maps</span><span class="sxs-lookup"><span data-stu-id="e3460-157">Range shard maps</span></span>
<span data-ttu-id="e3460-158">In een **bereik shard-toewijzing**, Hallo sleutel bereik is beschreven door een combinatie van **[lage waarde, hoogwaardige)** waar Hallo *lage waarde* is de minimale sleutel Hallo in Hallo bereik en Hallo *Waardevolle* Hallo eerste waarde hoger is dan Hallo bereik.</span><span class="sxs-lookup"><span data-stu-id="e3460-158">In a **range shard map**, hello key range is described by a pair **[Low Value, High Value)** where hello *Low Value* is hello minimum key in hello range, and hello *High Value* is hello first value higher than hello range.</span></span> 

<span data-ttu-id="e3460-159">Bijvoorbeeld: **[0, 100)** bestaat uit alle gehele getallen groter dan of gelijk 0 en kleiner dan 100.</span><span class="sxs-lookup"><span data-stu-id="e3460-159">For example, **[0, 100)** includes all integers greater than or equal 0 and less than 100.</span></span> <span data-ttu-id="e3460-160">Houd er rekening mee dat meerdere adresbereiken kunnen punt toohello dezelfde database en niet-aaneengesloten bereiken wordt uitgevoerd, worden ondersteund (bijvoorbeeld [100,200) en [400,600) beide C punt tooDatabase in Hallo voorbeeld hieronder.)</span><span class="sxs-lookup"><span data-stu-id="e3460-160">Note that multiple ranges can point toohello same database, and disjoint ranges are supported (e.g., [100,200) and [400,600) both point tooDatabase C in hello example below.)</span></span>

| <span data-ttu-id="e3460-161">Sleutel</span><span class="sxs-lookup"><span data-stu-id="e3460-161">Key</span></span> | <span data-ttu-id="e3460-162">Shard-locatie</span><span class="sxs-lookup"><span data-stu-id="e3460-162">Shard Location</span></span> |
| --- | --- |
| <span data-ttu-id="e3460-163">[1,50)</span><span class="sxs-lookup"><span data-stu-id="e3460-163">[1,50)</span></span> |<span data-ttu-id="e3460-164">Database_A</span><span class="sxs-lookup"><span data-stu-id="e3460-164">Database_A</span></span> |
| <span data-ttu-id="e3460-165">[50,100)</span><span class="sxs-lookup"><span data-stu-id="e3460-165">[50,100)</span></span> |<span data-ttu-id="e3460-166">Database_B</span><span class="sxs-lookup"><span data-stu-id="e3460-166">Database_B</span></span> |
| <span data-ttu-id="e3460-167">[100,200)</span><span class="sxs-lookup"><span data-stu-id="e3460-167">[100,200)</span></span> |<span data-ttu-id="e3460-168">Database_C</span><span class="sxs-lookup"><span data-stu-id="e3460-168">Database_C</span></span> |
| <span data-ttu-id="e3460-169">[400,600)</span><span class="sxs-lookup"><span data-stu-id="e3460-169">[400,600)</span></span> |<span data-ttu-id="e3460-170">Database_C</span><span class="sxs-lookup"><span data-stu-id="e3460-170">Database_C</span></span> |
| <span data-ttu-id="e3460-171">...</span><span class="sxs-lookup"><span data-stu-id="e3460-171">...</span></span> |<span data-ttu-id="e3460-172">...</span><span class="sxs-lookup"><span data-stu-id="e3460-172">...</span></span> |

<span data-ttu-id="e3460-173">Hallo-tabellen die hierboven is een conceptueel voorbeeld van een **ShardMap** object.</span><span class="sxs-lookup"><span data-stu-id="e3460-173">Each of hello tables shown above is a conceptual example of a **ShardMap** object.</span></span> <span data-ttu-id="e3460-174">Elke rij is een eenvoudig voorbeeld van een persoon **PointMapping** (voor Hallo lijst shard-toewijzing) of **RangeMapping** (voor Hallo bereik shard-toewijzing) object.</span><span class="sxs-lookup"><span data-stu-id="e3460-174">Each row is a simplified example of an individual **PointMapping** (for hello list shard map) or **RangeMapping** (for hello range shard map) object.</span></span>

## <a name="shard-map-manager"></a><span data-ttu-id="e3460-175">Beheer van shard-kaart</span><span class="sxs-lookup"><span data-stu-id="e3460-175">Shard map manager</span></span>
<span data-ttu-id="e3460-176">In het Hallo-clientbibliotheek is Hallo shard-toewijzing manager een verzameling van shard-kaarten.</span><span class="sxs-lookup"><span data-stu-id="e3460-176">In hello client library, hello shard map  manager is a collection of shard maps.</span></span> <span data-ttu-id="e3460-177">Hallo gegevens die worden beheerd door een **ShardMapManager** exemplaar wordt opgeslagen op drie locaties:</span><span class="sxs-lookup"><span data-stu-id="e3460-177">hello data managed by a **ShardMapManager** instance is kept in three places:</span></span> 

1. <span data-ttu-id="e3460-178">**Globale Shard-toewijzing (GSM)**: U een database tooserve opgeven als Hallo-opslagplaats voor alle shard-kaarten en toewijzingen.</span><span class="sxs-lookup"><span data-stu-id="e3460-178">**Global Shard Map (GSM)**: You specify a database tooserve as hello repository for all of its shard maps and mappings.</span></span> <span data-ttu-id="e3460-179">Speciale tabellen en opgeslagen procedures worden automatisch gemaakt voor toomanage Hallo informatie.</span><span class="sxs-lookup"><span data-stu-id="e3460-179">Special tables and stored procedures are automatically created toomanage hello information.</span></span> <span data-ttu-id="e3460-180">Dit is meestal een kleine database en licht geopend en mag niet worden gebruikt voor andere behoeften van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="e3460-180">This is typically a small database and lightly accessed, and it should not be used for other needs of hello application.</span></span> <span data-ttu-id="e3460-181">Hallo tabellen zijn in een speciale schema met de naam **__ShardManagement**.</span><span class="sxs-lookup"><span data-stu-id="e3460-181">hello tables are in a special schema named **__ShardManagement**.</span></span> 
2. <span data-ttu-id="e3460-182">**Lokale Shard-toewijzing (LSM)**: elke database die u opgeeft toobe een shard is gewijzigd toocontain verschillende kleine tabellen en speciale opgeslagen procedures die bevatten en shard kaart informatie specifieke toothat shard beheren.</span><span class="sxs-lookup"><span data-stu-id="e3460-182">**Local Shard Map (LSM)**: Every database that you specify toobe a shard is modified toocontain several small tables and special stored procedures that contain and manage shard map information specific toothat shard.</span></span> <span data-ttu-id="e3460-183">Deze informatie is redundant met Hallo-informatie in Hallo GSM en kunnen Hallo toovalidate in de cache opgeslagen shard kaart toepassingsinformatie zonder belasting op Hallo GSM; worden geplaatst Hallo-toepassing gebruikt Hallo LSM toodetermine als een toewijzing in de cache nog geldig is.</span><span class="sxs-lookup"><span data-stu-id="e3460-183">This information is redundant with hello information in hello GSM, and it allows hello application toovalidate cached shard map information without placing any load on hello GSM; hello application uses hello LSM toodetermine if a cached mapping is still valid.</span></span> <span data-ttu-id="e3460-184">Hallo tabellen bijbehorende toohello LSM op elke shard bevinden zich ook in Hallo schema **__ShardManagement**.</span><span class="sxs-lookup"><span data-stu-id="e3460-184">hello tables corresponding toohello LSM on each shard are also in hello schema **__ShardManagement**.</span></span>
3. <span data-ttu-id="e3460-185">**Toepassingscache**: elke toepassing exemplaar toegang tot een **ShardMapManager** object onderhoudt een lokale cache in het geheugen van de toewijzingen.</span><span class="sxs-lookup"><span data-stu-id="e3460-185">**Application cache**: Each application instance accessing a **ShardMapManager** object maintains a local in-memory cache of its mappings.</span></span> <span data-ttu-id="e3460-186">Routinggegevens die onlangs zijn opgehaald worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="e3460-186">It stores routing information that has recently been retrieved.</span></span> 

## <a name="constructing-a-shardmapmanager"></a><span data-ttu-id="e3460-187">Een ShardMapManager maken</span><span class="sxs-lookup"><span data-stu-id="e3460-187">Constructing a ShardMapManager</span></span>
<span data-ttu-id="e3460-188">Een **ShardMapManager** -object is gemaakt met behulp van een [factory](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx) patroon.</span><span class="sxs-lookup"><span data-stu-id="e3460-188">A **ShardMapManager** object is constructed using a [factory](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx) pattern.</span></span> <span data-ttu-id="e3460-189">Hallo  **[ShardMapManagerFactory.GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**  methode heeft referenties (inclusief Hallo-servernaam en databasenaam houden Hallo GSM) in Hallo vorm van een  **ConnectionString** en retourneert een exemplaar van een **ShardMapManager**.</span><span class="sxs-lookup"><span data-stu-id="e3460-189">hello **[ShardMapManagerFactory.GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)** method takes credentials (including hello server name and database name holding hello GSM) in hello form of a **ConnectionString** and returns an instance of a **ShardMapManager**.</span></span>  

<span data-ttu-id="e3460-190">**Opmerking:** hello **ShardMapManager** slechts één keer per app-domein, Hallo initialisatie van de code voor een toepassing moet worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e3460-190">**Please Note:** hello **ShardMapManager** should be instantiated only once per app domain, within hello initialization code for an application.</span></span> <span data-ttu-id="e3460-191">Het maken van extra exemplaren van ShardMapManager in Hallo hetzelfde appdomain resulteert in meer geheugen en CPU-gebruik van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="e3460-191">Creation of additional instances of ShardMapManager in hello same appdomain, will result in increased memory and CPU utilization of hello application.</span></span> <span data-ttu-id="e3460-192">Een **ShardMapManager** mag een onbeperkt aantal shard-kaarten.</span><span class="sxs-lookup"><span data-stu-id="e3460-192">A **ShardMapManager** can contain any number of shard maps.</span></span> <span data-ttu-id="e3460-193">Bij een enkele shard-toewijzing is mogelijk niet voldoende is voor veel toepassingen, zijn er keer wanneer verschillende sets van databases worden gebruikt voor verschillende schema of voor unieke doeleinden; in deze gevallen mogelijk meerdere shard-kaarten beter.</span><span class="sxs-lookup"><span data-stu-id="e3460-193">While a single shard map may be sufficient for many applications, there are times when different sets of databases are used for different schema or for unique purposes; in those cases multiple shard maps may be preferable.</span></span> 

<span data-ttu-id="e3460-194">In deze code probeert een toepassing een bestaande tooopen **ShardMapManager** Hello [TryGetSqlShardMapManager methode](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx).</span><span class="sxs-lookup"><span data-stu-id="e3460-194">In this code, an application tries tooopen an existing **ShardMapManager** with hello [TryGetSqlShardMapManager method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx).</span></span>  <span data-ttu-id="e3460-195">Als objecten die een Global **ShardMapManager** (GSM) nog niet bestaat in de database hello, Hallo-clientbibliotheek maakt ze er met Hallo [CreateSqlShardMapManager methode](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx).</span><span class="sxs-lookup"><span data-stu-id="e3460-195">If objects representing a Global **ShardMapManager** (GSM) do not yet exist inside hello database, hello client library creates them there using hello [CreateSqlShardMapManager method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx).</span></span>

    // Try tooget a reference toohello Shard Map Manager 
     // via hello Shard Map Manager database.  
    // If it doesn't already exist, then create it. 
    ShardMapManager shardMapManager; 
    bool shardMapManagerExists = ShardMapManagerFactory.TryGetSqlShardMapManager(
                                        connectionString, 
                                        ShardMapManagerLoadPolicy.Lazy, 
                                        out shardMapManager); 

    if (shardMapManagerExists) 
     { 
        Console.WriteLine("Shard Map Manager already exists");
    } 
    else
    {
        // Create hello Shard Map Manager. 
        ShardMapManagerFactory.CreateSqlShardMapManager(connectionString);
        Console.WriteLine("Created SqlShardMapManager"); 

        shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager(
            connectionString, 
            ShardMapManagerLoadPolicy.Lazy);

        // hello connectionString contains server name, database name, and admin credentials 
        // for privileges on both hello GSM and hello shards themselves.
    } 

<span data-ttu-id="e3460-196">Als alternatief kunt u Powershell toocreate een nieuwe Manager van de Shard-toewijzing.</span><span class="sxs-lookup"><span data-stu-id="e3460-196">As an alternative, you can use Powershell toocreate a new Shard Map Manager.</span></span> <span data-ttu-id="e3460-197">Een voorbeeld is beschikbaar [hier](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="e3460-197">An example is available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

## <a name="get-a-rangeshardmap-or-listshardmap"></a><span data-ttu-id="e3460-198">Een RangeShardMap of ListShardMap ophalen</span><span class="sxs-lookup"><span data-stu-id="e3460-198">Get a RangeShardMap or ListShardMap</span></span>
<span data-ttu-id="e3460-199">Na het maken van een shard kaart manager, kunt u krijgen Hallo [RangeShardMap](https://msdn.microsoft.com/library/azure/dn807318.aspx) of [ListShardMap](https://msdn.microsoft.com/library/azure/dn807370.aspx) met Hallo [TryGetRangeShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), Hallo [ TryGetListShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), of Hallo [GetShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) methode.</span><span class="sxs-lookup"><span data-stu-id="e3460-199">After creating a shard map manager, you can get hello [RangeShardMap](https://msdn.microsoft.com/library/azure/dn807318.aspx) or [ListShardMap](https://msdn.microsoft.com/library/azure/dn807370.aspx) using hello [TryGetRangeShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), hello [TryGetListShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), or hello [GetShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) method.</span></span>

    /// <summary>
    /// Creates a new Range Shard Map with hello specified name, or gets hello Range Shard Map if it already exists.
    /// </summary>
    public static RangeShardMap<T> CreateOrGetRangeShardMap<T>(ShardMapManager shardMapManager, string shardMapName)
    {
        // Try tooget a reference toohello Shard Map.
        RangeShardMap<T> shardMap;
        bool shardMapExists = shardMapManager.TryGetRangeShardMap(shardMapName, out shardMap);

        if (shardMapExists)
        {
            ConsoleUtils.WriteInfo("Shard Map {0} already exists", shardMap.Name);
        }
        else
        {
            // hello Shard Map does not exist, so create it
            shardMap = shardMapManager.CreateRangeShardMap<T>(shardMapName);
            ConsoleUtils.WriteInfo("Created Shard Map {0}", shardMap.Name);
        }

        return shardMap;
    } 

### <a name="shard-map-administration-credentials"></a><span data-ttu-id="e3460-200">Beheerdersrechten shard-kaart</span><span class="sxs-lookup"><span data-stu-id="e3460-200">Shard map administration credentials</span></span>
<span data-ttu-id="e3460-201">Toepassingen beheren en manipuleren van shard-kaarten zijn anders dan die Hallo shard maps tooroute verbindingen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e3460-201">Applications that administer and manipulate shard maps are different from those that use hello shard maps tooroute connections.</span></span> 

<span data-ttu-id="e3460-202">tooadminister shard-toewijzingen (toevoegen of wijzigen shards, shard-kaarten, shard-toewijzingen, enz.) moet u Hallo instantiëren **ShardMapManager** met **referenties die lezen/schrijven-bevoegdheden op beide Hallo GSM-database en op elk database die als een shard fungeert**.</span><span class="sxs-lookup"><span data-stu-id="e3460-202">tooadminister shard maps (add or change shards, shard maps, shard mappings, etc.) you must instantiate hello **ShardMapManager** using **credentials that have read/write privileges on both hello GSM database and on each database that serves as a shard**.</span></span> <span data-ttu-id="e3460-203">Hallo referenties moeten ervoor zorgen dat voor schrijfacties tegen Hallo tabellen in beide Hallo GSM en LSM shard kaart informatie wordt ingevoerd of gewijzigd, ook als voor het maken van tabellen LSM op nieuwe shards.</span><span class="sxs-lookup"><span data-stu-id="e3460-203">hello credentials must allow for writes against hello tables in both hello GSM and LSM as shard map information is entered or changed, as well as for creating LSM tables on new shards.</span></span>  

<span data-ttu-id="e3460-204">Zie [referenties gebruikt tooaccess Hallo elastische Database-clientbibliotheek](sql-database-elastic-scale-manage-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="e3460-204">See [Credentials used tooaccess hello Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span>

### <a name="only-metadata-affected"></a><span data-ttu-id="e3460-205">Alleen de metagegevens die van invloed op een</span><span class="sxs-lookup"><span data-stu-id="e3460-205">Only metadata affected</span></span>
<span data-ttu-id="e3460-206">Methoden voor het invullen van of het wijzigen van Hallo **ShardMapManager** gegevens Hallo gebruikersgegevens opgeslagen in Hallo shards zelf niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="e3460-206">Methods used for populating or changing hello **ShardMapManager** data do not alter hello user data stored in hello shards themselves.</span></span> <span data-ttu-id="e3460-207">Bijvoorbeeld, methoden zoals **CreateShard**, **DeleteShard**, **UpdateMapping**, enzovoort. invloed hebben op Hallo shard kaart bestaan alleen uit metagegevens.</span><span class="sxs-lookup"><span data-stu-id="e3460-207">For example, methods such as **CreateShard**, **DeleteShard**, **UpdateMapping**, etc. affect hello shard map metadata only.</span></span> <span data-ttu-id="e3460-208">Ze niet verwijdert, toevoegen of wijzigen van de gebruikersgegevens in Hallo shards.</span><span class="sxs-lookup"><span data-stu-id="e3460-208">They do not remove, add, or alter user data contained in hello shards.</span></span> <span data-ttu-id="e3460-209">In plaats daarvan deze methoden zijn ontworpen toobe gebruikt in combinatie met afzonderlijke bewerkingen u toocreate uitvoeren of werkelijke databases verwijderen of verplaatsen rijen uit één shard tooanother toorebalance een shard-omgeving.</span><span class="sxs-lookup"><span data-stu-id="e3460-209">Instead, these methods are designed toobe used in conjunction with separate operations you perform toocreate or remove actual databases, or that move rows from one shard tooanother toorebalance a sharded environment.</span></span>  <span data-ttu-id="e3460-210">(Hallo **gesplitste samenvoegen** hulpprogramma dat wordt geleverd met hulpprogramma's voor elastische database wordt gebruikgemaakt van deze API's samen met het organiseren van de daadwerkelijke gegevensverplaatsing tussen shards.) Zie [vergroten/verkleinen met Hallo elastische Database split-samenvoegen hulpprogramma](sql-database-elastic-scale-overview-split-and-merge.md).</span><span class="sxs-lookup"><span data-stu-id="e3460-210">(hello **split-merge** tool included with elastic database tools makes use of these APIs along with orchestrating actual data movement between shards.) See [Scaling using hello Elastic Database split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md).</span></span>

## <a name="populating-a-shard-map-example"></a><span data-ttu-id="e3460-211">Voorbeeld van een shard-toewijzing in te vullen</span><span class="sxs-lookup"><span data-stu-id="e3460-211">Populating a shard map example</span></span>
<span data-ttu-id="e3460-212">Een van de voorbeeldreeks bewerkingen toopopulate een specifieke shard-toewijzing wordt hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e3460-212">An example sequence of operations toopopulate a specific shard map is shown below.</span></span> <span data-ttu-id="e3460-213">Hallo code voert de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="e3460-213">hello code performs these steps:</span></span> 

1. <span data-ttu-id="e3460-214">Een nieuwe shard-toewijzing wordt gemaakt binnen een manager shard-toewijzing.</span><span class="sxs-lookup"><span data-stu-id="e3460-214">A new shard map is created within a shard map manager.</span></span> 
2. <span data-ttu-id="e3460-215">Hallo-metagegevens voor twee verschillende shards toegevoegd toohello shard-toewijzing.</span><span class="sxs-lookup"><span data-stu-id="e3460-215">hello metadata for two different shards is added toohello shard map.</span></span> 
3. <span data-ttu-id="e3460-216">Een aantal belangrijke bereik toewijzingen worden toegevoegd en hello algehele inhoud van Hallo shard-toewijzing wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e3460-216">A variety of key range mappings are added, and hello overall contents of hello shard map are displayed.</span></span> 

<span data-ttu-id="e3460-217">Hallo-code wordt geschreven, zodat het Hallo-methode kan opnieuw worden gestart als er een fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="e3460-217">hello code is written so that hello method can be rerun if an error occurs.</span></span> <span data-ttu-id="e3460-218">Elke aanvraag wordt gecontroleerd of een shard of toewijzing al bestaat, voordat u probeert toocreate deze.</span><span class="sxs-lookup"><span data-stu-id="e3460-218">Each request tests whether a shard or mapping already exists, before attempting toocreate it.</span></span> <span data-ttu-id="e3460-219">Hallo code wordt ervan uitgegaan dat de naam van databases **sample_shard_0**, **sample_shard_1** en **sample_shard_2** al zijn gemaakt in Hallo server waarnaar wordt verwezen door de tekenreeks **shardServer**.</span><span class="sxs-lookup"><span data-stu-id="e3460-219">hello code assumes that databases named **sample_shard_0**, **sample_shard_1** and **sample_shard_2** have already been created in hello server referenced by string **shardServer**.</span></span> 

    public void CreatePopulatedRangeMap(ShardMapManager smm, string mapName) 
        {            
            RangeShardMap<long> sm = null; 

            // check if shardmap exists and if not, create it 
            if (!smm.TryGetRangeShardMap(mapName, out sm)) 
            { 
                sm = smm.CreateRangeShardMap<long>(mapName); 
            } 

            Shard shard0 = null, shard1=null; 
            // Check if shard exists and if not, 
            // create it (Idempotent / tolerant of re-execute) 
            if (!sm.TryGetShard(new ShardLocation(
                                     shardServer, 
                                     "sample_shard_0"), 
                                     out shard0)) 
            { 
                Shard0 = sm.CreateShard(new ShardLocation(
                                            shardServer, 
                                            "sample_shard_0")); 
            } 

            if (!sm.TryGetShard(new ShardLocation(
                                    shardServer, 
                                    "sample_shard_1"), 
                                    out shard1)) 
            { 
                Shard1 = sm.CreateShard(new ShardLocation(
                                             shardServer, 
                                            "sample_shard_1"));  
            } 

            RangeMapping<long> rmpg=null; 

            // Check if mapping exists and if not,
            // create it (Idempotent / tolerant of re-execute) 
            if (!sm.TryGetMappingForKey(0, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                          new RangeMappingCreationInfo<long>
                          (new Range<long>(0, 50), 
                          shard0, 
                          MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(50, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(50, 100), 
                         shard1, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(100, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long>
                         (new Range<long>(100, 150), 
                         shard0, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(150, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(150, 200), 
                         shard1, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(200, out rmpg)) 
            { 
               sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(200, 300), 
                         shard0, 
                         MappingStatus.Online)); 
            } 

            // List hello shards and mappings 
            foreach (Shard s in sm.GetShards()
                         .OrderBy(s => s.Location.DataSource)
                         .ThenBy(s => s.Location.Database))
            { 
               Console.WriteLine("shard: "+ s.Location); 
            } 

            foreach (RangeMapping<long> rm in sm.GetMappings()) 
            { 
                Console.WriteLine("range: [" + rm.Value.Low.ToString() + ":" 
                        + rm.Value.High.ToString()+ ")  ==>" +rm.Shard.Location); 
            } 
        } 

<span data-ttu-id="e3460-220">Als alternatief kunt u PowerShell-scripts tooachieve Hallo resultaat hetzelfde.</span><span class="sxs-lookup"><span data-stu-id="e3460-220">As an alternative you can use PowerShell scripts tooachieve hello same result.</span></span> <span data-ttu-id="e3460-221">Sommige Hallo voorbeeld PowerShell-voorbeelden zijn beschikbaar [hier](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="e3460-221">Some of hello sample PowerShell examples are available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>     

<span data-ttu-id="e3460-222">Zodra de shard-kaarten zijn ingevuld, wordt data access-toepassingen kunnen worden gemaakt of aangepast toowork met Hallo maps.</span><span class="sxs-lookup"><span data-stu-id="e3460-222">Once shard maps have been populated, data access applications can be created or adapted toowork with hello maps.</span></span> <span data-ttu-id="e3460-223">In te vullen of manipuleren van Hallo maps moet zich niet voor pas weer **kaart indeling** moet toochange.</span><span class="sxs-lookup"><span data-stu-id="e3460-223">Populating or manipulating hello maps need not occur again until **map layout** needs toochange.</span></span>  

## <a name="data-dependent-routing"></a><span data-ttu-id="e3460-224">Gegevensafhankelijke routering</span><span class="sxs-lookup"><span data-stu-id="e3460-224">Data dependent routing</span></span>
<span data-ttu-id="e3460-225">Hallo shard-toewijzing manager zal meest worden gebruikt in toepassingen waarvoor verbindingen tooperform Hallo app-specifieke gegevens databasebewerkingen.</span><span class="sxs-lookup"><span data-stu-id="e3460-225">hello shard map manager will be most used in applications that require database connections tooperform hello app-specific data operations.</span></span> <span data-ttu-id="e3460-226">Deze verbindingen moeten worden gekoppeld aan de juiste database Hallo.</span><span class="sxs-lookup"><span data-stu-id="e3460-226">Those connections must be associated with hello correct database.</span></span> <span data-ttu-id="e3460-227">Dit staat bekend als **gegevensafhankelijke routering**.</span><span class="sxs-lookup"><span data-stu-id="e3460-227">This is known as **Data Dependent Routing**.</span></span> <span data-ttu-id="e3460-228">Exemplaar maken van een object shard kaart manager van Hallo-factory met referenties die alleen-lezen toegang op Hallo GSM database hebben voor deze toepassingen.</span><span class="sxs-lookup"><span data-stu-id="e3460-228">For these applications, instantiate a shard map manager object from hello factory using credentials that have read-only access on hello GSM database.</span></span> <span data-ttu-id="e3460-229">Afzonderlijke aanvragen voor latere verbindingen Geef referenties op die nodig zijn voor het verbinden van toohello juiste shard-database.</span><span class="sxs-lookup"><span data-stu-id="e3460-229">Individual requests for later connections supply credentials necessary for connecting toohello appropriate shard database.</span></span>

<span data-ttu-id="e3460-230">Houd er rekening mee dat deze toepassingen (met behulp van **ShardMapManager** geopend met alleen-lezen referenties) kan geen wijzigingen aanbrengen toohello maps of toewijzingen.</span><span class="sxs-lookup"><span data-stu-id="e3460-230">Note that these applications (using **ShardMapManager** opened with read-only credentials) cannot make changes toohello maps or mappings.</span></span> <span data-ttu-id="e3460-231">Maak voor die behoeften beheerdersrechten-specifieke toepassingen of PowerShell-scripts die hogere bevoegdheden referenties opgeven, zoals eerder besproken.</span><span class="sxs-lookup"><span data-stu-id="e3460-231">For those needs, create administrative-specific applications or PowerShell scripts that supply higher-privileged credentials as discussed earlier.</span></span> <span data-ttu-id="e3460-232">Zie [referenties gebruikt tooaccess Hallo elastische Database-clientbibliotheek](sql-database-elastic-scale-manage-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="e3460-232">See [Credentials used tooaccess hello Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span>

<span data-ttu-id="e3460-233">Zie voor meer informatie [gegevensafhankelijke routering](sql-database-elastic-scale-data-dependent-routing.md).</span><span class="sxs-lookup"><span data-stu-id="e3460-233">For more details, see [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md).</span></span> 

## <a name="modifying-a-shard-map"></a><span data-ttu-id="e3460-234">Wijzigen van een shard-toewijzing</span><span class="sxs-lookup"><span data-stu-id="e3460-234">Modifying a shard map</span></span>
<span data-ttu-id="e3460-235">Een shard-toewijzing kan op verschillende manieren worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="e3460-235">A shard map can be changed in different ways.</span></span> <span data-ttu-id="e3460-236">Alle van de volgende methoden Hallo Hallo metagegevens beschrijven Hallo shards en hun toewijzingen wijzigen maar ze gegevens binnen Hallo shards niet fysiek aanpassen, of komen ze maken of verwijderen van de werkelijke Hallo-databases.</span><span class="sxs-lookup"><span data-stu-id="e3460-236">All of hello following methods modify hello metadata describing hello shards and their mappings, but they do not physically modify data within hello shards, nor do they create or delete hello actual databases.</span></span>  <span data-ttu-id="e3460-237">Aantal Hallo-bewerkingen op Hallo shard-toewijzing die hieronder worden beschreven wellicht toobe coördinatie met beheeracties die gegevens fysiek verplaatsen of die toevoegen en verwijderen van de databases die fungeren als shards.</span><span class="sxs-lookup"><span data-stu-id="e3460-237">Some of hello operations on hello shard map described below may need toobe coordinated with administrative actions that physically move data or that add and remove databases serving as shards.</span></span>

<span data-ttu-id="e3460-238">Deze methoden samenwerken als bouwstenen Hallo beschikbaar voor het wijzigen van Hallo algemene distributie van gegevens in uw databaseomgeving shard-.</span><span class="sxs-lookup"><span data-stu-id="e3460-238">These methods work together as hello building blocks available for modifying hello overall distribution of data in your sharded database environment.</span></span>  

* <span data-ttu-id="e3460-239">tooadd of verwijder shards: Gebruik  **[CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)**  en  **[DeleteShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)**  Hallo [Shardmap klasse](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx).</span><span class="sxs-lookup"><span data-stu-id="e3460-239">tooadd or remove shards: use **[CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)** and **[DeleteShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)** of hello [Shardmap class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx).</span></span> 
  
    <span data-ttu-id="e3460-240">Hallo moeten-server en database die vertegenwoordigt Hallo doel shard al bestaan voor deze bewerkingen tooexecute.</span><span class="sxs-lookup"><span data-stu-id="e3460-240">hello server and database representing hello target shard must already exist for these operations tooexecute.</span></span> <span data-ttu-id="e3460-241">Deze methoden geen invloed heeft op Hallo databases zelf, alleen op metagegevens in Hallo shard-toewijzing.</span><span class="sxs-lookup"><span data-stu-id="e3460-241">These methods do not have any impact on hello databases themselves, only on metadata in hello shard map.</span></span>
* <span data-ttu-id="e3460-242">toocreate of verwijder punten of adresbereiken die zijn toegewezen toohello shards: Gebruik  **[CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn841993.aspx)**,  **[DeleteMapping](https://msdn.microsoft.com/library/azure/dn824200.aspx)**  Hallo [RangeShardMapping klasse](https://msdn.microsoft.com/library/azure/dn807318.aspx), en  **[CreatePointMapping](https://msdn.microsoft.com/library/azure/dn807218.aspx)**  Hallo [ListShardMap](https://msdn.microsoft.com/library/azure/dn842123.aspx)</span><span class="sxs-lookup"><span data-stu-id="e3460-242">toocreate or remove points or ranges that are mapped toohello shards: use **[CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn841993.aspx)**, **[DeleteMapping](https://msdn.microsoft.com/library/azure/dn824200.aspx)** of hello [RangeShardMapping class](https://msdn.microsoft.com/library/azure/dn807318.aspx), and **[CreatePointMapping](https://msdn.microsoft.com/library/azure/dn807218.aspx)** of hello [ListShardMap](https://msdn.microsoft.com/library/azure/dn842123.aspx)</span></span>
  
    <span data-ttu-id="e3460-243">Veel verschillende punten of adresbereiken kunnen worden toegewezen toohello dezelfde shard.</span><span class="sxs-lookup"><span data-stu-id="e3460-243">Many different points or ranges can be mapped toohello same shard.</span></span> <span data-ttu-id="e3460-244">Deze methoden zijn alleen van invloed op de metagegevens - ze hebben geen invloed op alle gegevens die al aanwezig in shards.</span><span class="sxs-lookup"><span data-stu-id="e3460-244">These methods only affect metadata - they do not affect any data that may already be present in shards.</span></span> <span data-ttu-id="e3460-245">Als gegevens verwijderd uit de database Hallo in volgorde toobe consistent zijn met toobe moeten **DeleteMapping** bewerkingen, moet u tooperform deze bewerkingen afzonderlijk, maar in combinatie met behulp van deze methoden.</span><span class="sxs-lookup"><span data-stu-id="e3460-245">If data needs toobe removed from hello database in order toobe consistent with **DeleteMapping** operations, you will need tooperform those operations separately but in conjunction with using these methods.</span></span>  
* <span data-ttu-id="e3460-246">de bestaande bereiken toosplit in twee of aangrenzende bereiken samenvoegen tot één: Gebruik  **[SplitMapping](https://msdn.microsoft.com/library/azure/dn824205.aspx)**  en  **[MergeMappings](https://msdn.microsoft.com/library/azure/dn824201.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="e3460-246">toosplit existing ranges into two, or merge adjacent ranges into one: use **[SplitMapping](https://msdn.microsoft.com/library/azure/dn824205.aspx)** and **[MergeMappings](https://msdn.microsoft.com/library/azure/dn824201.aspx)**.</span></span>  
  
    <span data-ttu-id="e3460-247">Let op te splitsen en samenvoegen van bewerkingen **veranderen niet Hallo shard toowhich sleutel waarden worden toegewezen**.</span><span class="sxs-lookup"><span data-stu-id="e3460-247">Note that split and merge operations **do not change hello shard toowhich key values are mapped**.</span></span> <span data-ttu-id="e3460-248">Een splitsing, een bestaand bereik opgesplitst in twee delen, maar blijft beide als toegewezen toohello dezelfde shard.</span><span class="sxs-lookup"><span data-stu-id="e3460-248">A split breaks an existing range into two parts, but leaves both as mapped toohello same shard.</span></span> <span data-ttu-id="e3460-249">Een samenvoeging is van invloed op twee aangrenzende bereiken die al toegewezen toohello zijn dezelfde shard, ze samenvoegen tot een enkel bereik.</span><span class="sxs-lookup"><span data-stu-id="e3460-249">A merge operates on two adjacent ranges that are already mapped toohello same shard, coalescing them into a single range.</span></span>  <span data-ttu-id="e3460-250">Hallo verkeer van punten of bereiken zelf tussen shards moet toobe gecoördineerd door middel van **UpdateMapping** in combinatie met de daadwerkelijke gegevensverplaatsing.</span><span class="sxs-lookup"><span data-stu-id="e3460-250">hello movement of points or ranges themselves between shards needs toobe coordinated by using **UpdateMapping** in conjunction with actual data movement.</span></span>  <span data-ttu-id="e3460-251">U kunt Hallo **gesplitste/Merge** service die deel uitmaakt van de elastische database toocoordinate shard-toewijzing wijzigingen met gegevensverplaatsing, hulpprogramma's voor wanneer verkeer nodig is.</span><span class="sxs-lookup"><span data-stu-id="e3460-251">You can use hello **Split/Merge** service that is part of elastic database tools toocoordinate shard map changes with data movement, when movement is needed.</span></span> 
* <span data-ttu-id="e3460-252">toore-kaart (of verplaatsen) afzonderlijke punten of bereiken toodifferent shards: Gebruik  **[UpdateMapping](https://msdn.microsoft.com/library/azure/dn824207.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="e3460-252">toore-map (or move) individual points or ranges toodifferent shards: use **[UpdateMapping](https://msdn.microsoft.com/library/azure/dn824207.aspx)**.</span></span>  
  
    <span data-ttu-id="e3460-253">Omdat de gegevens wellicht toobe verplaatst van één shard tooanother in volgorde toobe consistent zijn met **UpdateMapping** bewerkingen, moet u tooperform beweging die afzonderlijk, maar in combinatie met behulp van deze methoden.</span><span class="sxs-lookup"><span data-stu-id="e3460-253">Since data may need toobe moved from one shard tooanother in order toobe consistent with **UpdateMapping** operations, you will need tooperform that movement separately but in conjunction with using these methods.</span></span>
* <span data-ttu-id="e3460-254">tootake toewijzingen online als offline: Gebruik  **[MarkMappingOffline](https://msdn.microsoft.com/library/azure/dn824202.aspx)**  en  **[MarkMappingOnline](https://msdn.microsoft.com/library/azure/dn807225.aspx)**  toocontrol Hallo online status van een toewijzing.</span><span class="sxs-lookup"><span data-stu-id="e3460-254">tootake mappings online and offline: use **[MarkMappingOffline](https://msdn.microsoft.com/library/azure/dn824202.aspx)** and **[MarkMappingOnline](https://msdn.microsoft.com/library/azure/dn807225.aspx)** toocontrol hello online state of a mapping.</span></span> 
  
    <span data-ttu-id="e3460-255">Bepaalde bewerkingen op de shard-toewijzingen zijn alleen toegestaan als een toewijzing in een 'offline' staat, met inbegrip van **UpdateMapping** en **DeleteMapping**.</span><span class="sxs-lookup"><span data-stu-id="e3460-255">Certain operations on shard mappings are only allowed when a mapping is in an “offline” state, including **UpdateMapping** and **DeleteMapping**.</span></span> <span data-ttu-id="e3460-256">Als een toewijzing offline is, wordt een gegevens-afhankelijke aanvraag op basis van een sleutel die is opgenomen in de toewijzing een fout geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="e3460-256">When a mapping is offline, a data-dependent request based on a key included in that mapping will return an error.</span></span> <span data-ttu-id="e3460-257">Bovendien wanneer een bereik is eerst offline gehaald, wordt alle verbindingen toohello van invloed op een shard worden automatisch in volgorde tooprevent inconsistente of onvolledige resultaten voor query's die zijn gericht tegen bereiken wordt gewijzigd afgebroken.</span><span class="sxs-lookup"><span data-stu-id="e3460-257">In addition, when a range is first taken offline, all connections toohello affected shard are automatically killed in order tooprevent inconsistent or incomplete results for queries directed against ranges being changed.</span></span> 

<span data-ttu-id="e3460-258">Toewijzingen zijn niet-wijzigbaar objecten in .net.</span><span class="sxs-lookup"><span data-stu-id="e3460-258">Mappings are immutable objects in .Net.</span></span>  <span data-ttu-id="e3460-259">Alle Hallo methoden bovenstaande Wijzig toewijzingen ongeldig ook eventuele verwijzingen toothem in uw code.</span><span class="sxs-lookup"><span data-stu-id="e3460-259">All of hello methods above that change mappings also invalidate any references toothem in your code.</span></span> <span data-ttu-id="e3460-260">toomake it eenvoudiger tooperform reeksen van bewerkingen die in een statuswijziging van een toewijzing, alle Hallo-methoden die een-toewijzing gewijzigd een nieuwe retourneren toewijzing-verwijzing, zodat bewerkingen kunnen worden gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="e3460-260">toomake it easier tooperform sequences of operations that change a mapping’s state, all of hello methods that change a mapping return a new mapping reference, so operations can be chained.</span></span> <span data-ttu-id="e3460-261">Bijvoorbeeld, toodelete een bestaande toewijzing in shardmap sm dat Hallo sleutel 25 bevat, kunt u uitvoeren hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="e3460-261">For example, toodelete an existing mapping in shardmap sm that contains hello key 25, you can execute hello following:</span></span> 

        sm.DeleteMapping(sm.MarkMappingOffline(sm.GetMappingForKey(25)));

## <a name="adding-a-shard"></a><span data-ttu-id="e3460-262">Toevoegen van een shard</span><span class="sxs-lookup"><span data-stu-id="e3460-262">Adding a shard</span></span>
<span data-ttu-id="e3460-263">Toepassingen vaak moet toosimply nieuwe shards toohandle gegevens toevoegen die wordt verwacht van de nieuwe sleutels of sleutelbereiken, voor een shard-toewijzing die al bestaat.</span><span class="sxs-lookup"><span data-stu-id="e3460-263">Applications often need toosimply add new shards toohandle data that is expected from new keys or key ranges, for a shard map that already exists.</span></span> <span data-ttu-id="e3460-264">Bijvoorbeeld, een toepassing shard door Tenant-ID moet mogelijk een nieuwe shard tooprovision voor een nieuwe tenant of gegevens shard maandelijks moet mogelijk een nieuwe shard ingericht voordat Hallo begin van elke nieuwe maand.</span><span class="sxs-lookup"><span data-stu-id="e3460-264">For example, an application sharded by Tenant ID may need tooprovision a new shard for a new tenant, or data sharded monthly may need a new shard provisioned before hello start of each new month.</span></span> 

<span data-ttu-id="e3460-265">Als nieuw bereik Hallo sleutelwaarden nog niet is onderdeel van een bestaande toewijzing en geen gegevensverplaatsing nodig, het is zeer eenvoudig tooadd Hallo nieuwe shard en Hallo nieuwe sleutel of bereik toothat shard koppelen.</span><span class="sxs-lookup"><span data-stu-id="e3460-265">If hello new range of key values is not already part of an existing mapping and no data movement is necessary, it is very simple tooadd hello new shard and associate hello new key or range toothat shard.</span></span> <span data-ttu-id="e3460-266">Zie voor meer informatie over het toevoegen van nieuwe shards [toevoegen van een nieuwe shard](sql-database-elastic-scale-add-a-shard.md).</span><span class="sxs-lookup"><span data-stu-id="e3460-266">For details on adding new shards, see [Adding a new shard](sql-database-elastic-scale-add-a-shard.md).</span></span>

<span data-ttu-id="e3460-267">Voor scenario's waarvoor de verplaatsing van gegevens, is Hallo gesplitste merge tool echter benodigde tooorchestrate Hallo verplaatsing van gegevens tussen shards in combinatie met Hallo nodig shard toewijzingen worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="e3460-267">For scenarios that require data movement, however, hello split-merge tool is needed tooorchestrate hello data movement between shards in combination with hello necessary shard map updates.</span></span> <span data-ttu-id="e3460-268">Zie voor meer informatie over het gebruik van hello gesplitste samenvoegen yool, [overzicht van de gesplitste samenvoegen](sql-database-elastic-scale-overview-split-and-merge.md)</span><span class="sxs-lookup"><span data-stu-id="e3460-268">For details on using hello split-merge yool, see [Overview of split-merge](sql-database-elastic-scale-overview-split-and-merge.md)</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-shard-map-management/listmapping.png
[2]: ./media/sql-database-elastic-scale-shard-map-management/rangemapping.png
[3]: ./media/sql-database-elastic-scale-shard-map-management/multipleonsingledb.png
