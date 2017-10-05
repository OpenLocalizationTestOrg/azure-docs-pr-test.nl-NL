---
title: Verklarende woordenlijst voor elastische Database extra | Microsoft Docs
description: Uitleg van termen die worden gebruikt voor hulpprogramma's van elastische database
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: a23a4e81-6706-452d-afc1-a550e5e47af9
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 0fda4bb948bbed1c14d468519ba67cce9bc4e6c3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="elastic-database-tools-glossary"></a><span data-ttu-id="28bc3-103">Elastische Database extra verklarende woordenlijst</span><span class="sxs-lookup"><span data-stu-id="28bc3-103">Elastic Database tools glossary</span></span>
<span data-ttu-id="28bc3-104">De volgende voorwaarden zijn gedefinieerd voor de [hulpmiddelen voor elastische databases](sql-database-elastic-scale-introduction.md), een functie van Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="28bc3-104">The following terms are defined for the [Elastic Database tools](sql-database-elastic-scale-introduction.md), a feature of Azure SQL Database.</span></span> <span data-ttu-id="28bc3-105">De hulpprogramma's worden gebruikt voor het beheren van [shard toegewezen](sql-database-elastic-scale-shard-map-management.md), en bevatten de [clientbibliotheek](sql-database-elastic-database-client-library.md), wordt de [gesplitste merge tool](sql-database-elastic-scale-overview-split-and-merge.md), [elastische pools](sql-database-elastic-pool.md), en [query's](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="28bc3-105">The tools are used to manage [shard maps](sql-database-elastic-scale-shard-map-management.md), and include the [client library](sql-database-elastic-database-client-library.md), the [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md), [elastic pools](sql-database-elastic-pool.md), and [queries](sql-database-elastic-query-overview.md).</span></span> 

<span data-ttu-id="28bc3-106">Deze termen worden gebruikt [toevoegen van een shard met hulpprogramma's van elastische Database](sql-database-elastic-scale-add-a-shard.md) en [shard kaart problemen op te lossen met behulp van de klasse RecoveryManager](sql-database-elastic-database-recovery-manager.md).</span><span class="sxs-lookup"><span data-stu-id="28bc3-106">These terms are used in [Adding a shard using Elastic Database tools](sql-database-elastic-scale-add-a-shard.md) and [Using the RecoveryManager class to fix shard map problems](sql-database-elastic-database-recovery-manager.md).</span></span>

![Elastische Scale voorwaarden][1]

<span data-ttu-id="28bc3-108">**Database**: een Azure SQL-database.</span><span class="sxs-lookup"><span data-stu-id="28bc3-108">**Database**: An Azure SQL database.</span></span> 

<span data-ttu-id="28bc3-109">**Gegevensafhankelijke routering**: de functionaliteit waarmee een toepassing verbinding maken met een shard krijgt een specifieke sharding-sleutel.</span><span class="sxs-lookup"><span data-stu-id="28bc3-109">**Data dependent routing**: The functionality that enables an application to connect to a shard given a specific sharding key.</span></span> <span data-ttu-id="28bc3-110">Zie [gegevensafhankelijke routering](sql-database-elastic-scale-data-dependent-routing.md).</span><span class="sxs-lookup"><span data-stu-id="28bc3-110">See [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md).</span></span> <span data-ttu-id="28bc3-111">Vergelijken met  **[Query meerdere Shard](sql-database-elastic-scale-multishard-querying.md)**.</span><span class="sxs-lookup"><span data-stu-id="28bc3-111">Compare to **[Multi-Shard Query](sql-database-elastic-scale-multishard-querying.md)**.</span></span>

<span data-ttu-id="28bc3-112">**Globale shard-toewijzing**: de toewijzing tussen sharding-sleutels en hun respectieve shards binnen een **shard set**.</span><span class="sxs-lookup"><span data-stu-id="28bc3-112">**Global shard map**: The map between sharding keys and their respective shards within a **shard set**.</span></span> <span data-ttu-id="28bc3-113">De globale shard-toewijzing is opgeslagen de **shard kaart manager**.</span><span class="sxs-lookup"><span data-stu-id="28bc3-113">The global shard map is stored in the **shard map manager**.</span></span> <span data-ttu-id="28bc3-114">Vergelijken met **lokale shard-toewijzing**.</span><span class="sxs-lookup"><span data-stu-id="28bc3-114">Compare to **local shard map**.</span></span>

<span data-ttu-id="28bc3-115">**Lijst shard-toewijzing**: een shard-toewijzing in welke sharding sleutels afzonderlijk zijn toegewezen.</span><span class="sxs-lookup"><span data-stu-id="28bc3-115">**List shard map**: A shard map in which sharding keys are mapped individually.</span></span> <span data-ttu-id="28bc3-116">Vergelijken met **Shard-toewijzing bereik**.</span><span class="sxs-lookup"><span data-stu-id="28bc3-116">Compare to **Range Shard Map**.</span></span>   

<span data-ttu-id="28bc3-117">**Lokale shard-toewijzing**: opgeslagen op een shard, de lokale shard-toewijzing toewijzingen voor de shardlets die zich op de shard bevinden bevat.</span><span class="sxs-lookup"><span data-stu-id="28bc3-117">**Local shard map**: Stored on a shard, the local shard map contains mappings for the shardlets that reside on the shard.</span></span>

<span data-ttu-id="28bc3-118">**Meerdere shard query**: de mogelijkheid om uit te geven van een query op meerdere shards; resultatensets worden geretourneerd met UNION ALL semantiek (ook wel bekend als ' fan-out query').</span><span class="sxs-lookup"><span data-stu-id="28bc3-118">**Multi-shard query**: The ability to issue a query against multiple shards; results sets are returned using UNION ALL semantics (also known as “fan-out query”).</span></span> <span data-ttu-id="28bc3-119">Vergelijken met **gegevensafhankelijke routering**.</span><span class="sxs-lookup"><span data-stu-id="28bc3-119">Compare to **data dependent routing**.</span></span>

<span data-ttu-id="28bc3-120">**Multitenant** en **één tenant**: dit betekent dat een single-tenant-database en een multitenant-database:</span><span class="sxs-lookup"><span data-stu-id="28bc3-120">**Multi-tenant** and **Single-tenant**: This shows a single-tenant database and a multi-tenant database:</span></span>

![Één en multitenant-databases](./media/sql-database-elastic-scale-glossary/multi-single-simple.png)

<span data-ttu-id="28bc3-122">Hier volgt een weergave van **shard** één en multitenant-databases.</span><span class="sxs-lookup"><span data-stu-id="28bc3-122">Here is a representation of **sharded** single and multi-tenant databases.</span></span> 

![Één en multitenant-databases](./media/sql-database-elastic-scale-glossary/shards-single-multi.png)

<span data-ttu-id="28bc3-124">**Bereik shard-toewijzing**: een shard-toewijzing waarin de shard-distributie-strategie is gebaseerd op meerdere bereiken met opeenvolgende waarden.</span><span class="sxs-lookup"><span data-stu-id="28bc3-124">**Range shard map**: A shard map in which the shard distribution strategy is based on multiple ranges of contiguous values.</span></span> 

<span data-ttu-id="28bc3-125">**Verwijzen naar tabellen**: tabellen die zijn niet shard maar zijn gerepliceerd in shards.</span><span class="sxs-lookup"><span data-stu-id="28bc3-125">**Reference tables**: Tables that are not sharded but are replicated across shards.</span></span> <span data-ttu-id="28bc3-126">Zip-codes kunnen bijvoorbeeld worden opgeslagen in een tabel.</span><span class="sxs-lookup"><span data-stu-id="28bc3-126">For example, zip codes can be stored in a reference table.</span></span> 

<span data-ttu-id="28bc3-127">**Shard**: een Azure SQL-database waarin gegevens uit een gegevensset shard wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="28bc3-127">**Shard**: An Azure SQL database that stores data from a sharded data set.</span></span> 

<span data-ttu-id="28bc3-128">**Elasticiteit shard**: de mogelijkheid om uit te voeren beide **horizontaal schalen** en **verticaal schalen**.</span><span class="sxs-lookup"><span data-stu-id="28bc3-128">**Shard elasticity**: The ability to perform both **horizontal scaling** and **vertical scaling**.</span></span>

<span data-ttu-id="28bc3-129">**Shard tabellen**: tabellen die zijn shard, dat wil zeggen, waarvan de gegevens is verdeeld over de shards op basis van hun sharding-sleutelwaarden.</span><span class="sxs-lookup"><span data-stu-id="28bc3-129">**Sharded tables**: Tables that are sharded, i.e., whose data is distributed across shards based on their sharding key values.</span></span> 

<span data-ttu-id="28bc3-130">**Sharding sleutel**: een waarde in de kolom die bepaalt hoe de gegevens is verdeeld over shards.</span><span class="sxs-lookup"><span data-stu-id="28bc3-130">**Sharding key**: A column value that determines how data is distributed across shards.</span></span> <span data-ttu-id="28bc3-131">Het waardetype kan een van de volgende zijn: **int**, **bigint**, **varbinary**, of **uniqueidentifier**.</span><span class="sxs-lookup"><span data-stu-id="28bc3-131">The value type can be one of the following: **int**, **bigint**, **varbinary**, or **uniqueidentifier**.</span></span> 

<span data-ttu-id="28bc3-132">**Shard set**: de verzameling van shards dat worden toegeschreven aan dezelfde shard-toewijzing in de shard-toewijzing manager.</span><span class="sxs-lookup"><span data-stu-id="28bc3-132">**Shard set**: The collection of shards that are attributed to the same shard map in the shard map manager.</span></span>  

<span data-ttu-id="28bc3-133">**Shardlet**: alle gegevens die zijn gekoppeld aan een enkele waarde van een sharding-sleutel op een shard.</span><span class="sxs-lookup"><span data-stu-id="28bc3-133">**Shardlet**: All of the data associated with a single value of a sharding key on a shard.</span></span> <span data-ttu-id="28bc3-134">Een shardlet is de kleinste eenheid van de verplaatsing van gegevens mogelijk wanneer herdistribueren shard tabellen.</span><span class="sxs-lookup"><span data-stu-id="28bc3-134">A shardlet is the smallest unit of data movement possible when redistributing sharded tables.</span></span> 

<span data-ttu-id="28bc3-135">**Shard-toewijzing**: de verzameling toewijzingen tussen sharding-sleutels en hun respectieve shards.</span><span class="sxs-lookup"><span data-stu-id="28bc3-135">**Shard map**: The set of mappings between sharding keys and their respective shards.</span></span>

<span data-ttu-id="28bc3-136">**Beheer van shard-toewijzing**: een store, management object en gegevens die de shard-toewijzing(en), shard-locaties en toewijzingen voor een of meer sets van shard bevat.</span><span class="sxs-lookup"><span data-stu-id="28bc3-136">**Shard map manager**: A management object and data store that contains the shard map(s), shard locations, and mappings for one or more shard sets.</span></span>

![Toewijzingen][2]

## <a name="verbs"></a><span data-ttu-id="28bc3-138">Termen</span><span class="sxs-lookup"><span data-stu-id="28bc3-138">Verbs</span></span>
<span data-ttu-id="28bc3-139">**Horizontaal schalen**: de handeling schalen uit (of in) een verzameling van shards door toe te voegen of te verwijderen van shards naar een shard-kaart, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="28bc3-139">**Horizontal scaling**: The act of scaling out (or in) a collection of shards by adding or removing shards to a shard map, as shown below.</span></span>

![Horizontale en verticale schalen][3]

<span data-ttu-id="28bc3-141">**Samenvoegen**: de handeling waarbij shardlets van twee shards verplaatst naar één shard en de shard-toewijzing dienovereenkomstig bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="28bc3-141">**Merge**: The act of moving shardlets from two shards to one shard and updating the shard map accordingly.</span></span>

<span data-ttu-id="28bc3-142">**Shardlet verplaatsen**: de act van een enkele shardlet verplaatsen naar een andere shard.</span><span class="sxs-lookup"><span data-stu-id="28bc3-142">**Shardlet move**: The act of moving a single shardlet to a different shard.</span></span> 

<span data-ttu-id="28bc3-143">**Shard**: de handeling horizontaal partitioneren identiek gestructureerde gegevens over meerdere databases op basis van een sharding-sleutel.</span><span class="sxs-lookup"><span data-stu-id="28bc3-143">**Shard**: The act of horizontally partitioning identically structured data across multiple databases based on a sharding key.</span></span>

<span data-ttu-id="28bc3-144">**Gesplitste**: de handeling waarbij verschillende shardlets van één shard verplaatst naar een andere (meestal nieuwe) shard.</span><span class="sxs-lookup"><span data-stu-id="28bc3-144">**Split**: The act of moving several shardlets from one shard to another (typically new) shard.</span></span> <span data-ttu-id="28bc3-145">Een sharding-sleutel wordt opgegeven door de gebruiker als de splitspunt.</span><span class="sxs-lookup"><span data-stu-id="28bc3-145">A sharding key is provided by the user as the split point.</span></span>

<span data-ttu-id="28bc3-146">**Verticale schaal**: de handeling schaal omhoog (of omlaag) het prestatieniveau van een afzonderlijke shard.</span><span class="sxs-lookup"><span data-stu-id="28bc3-146">**Vertical Scaling**: The act of scaling up (or down) the performance level of an individual shard.</span></span> <span data-ttu-id="28bc3-147">Bijvoorbeeld, het wijzigen van een shard van standaard naar Premium (die resulteert in meer bronnen).</span><span class="sxs-lookup"><span data-stu-id="28bc3-147">For example, changing a shard from Standard to Premium (which results in more computing resources).</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-glossary/glossary.png
[2]: ./media/sql-database-elastic-scale-glossary/mappings.png
[3]: ./media/sql-database-elastic-scale-glossary/h_versus_vert.png

