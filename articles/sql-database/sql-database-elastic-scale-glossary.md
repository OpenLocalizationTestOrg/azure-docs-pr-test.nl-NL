---
title: verklarende woordenlijst aaaElastic Database extra | Microsoft Docs
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
ms.openlocfilehash: d6573aad9a097e07135b0a64d1dafec19bb8cc7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-database-tools-glossary"></a><span data-ttu-id="bb089-103">Elastische Database extra verklarende woordenlijst</span><span class="sxs-lookup"><span data-stu-id="bb089-103">Elastic Database tools glossary</span></span>
<span data-ttu-id="bb089-104">Hallo volgende termen gedefinieerd voor Hallo [hulpmiddelen voor elastische databases](sql-database-elastic-scale-introduction.md), een functie van Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="bb089-104">hello following terms are defined for hello [Elastic Database tools](sql-database-elastic-scale-introduction.md), a feature of Azure SQL Database.</span></span> <span data-ttu-id="bb089-105">Hallo hulpprogramma's zijn gebruikte toomanage [shard toegewezen](sql-database-elastic-scale-shard-map-management.md), en bevatten Hallo [clientbibliotheek](sql-database-elastic-database-client-library.md), Hallo [gesplitste merge tool](sql-database-elastic-scale-overview-split-and-merge.md), [elastische pools](sql-database-elastic-pool.md), en [query's](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bb089-105">hello tools are used toomanage [shard maps](sql-database-elastic-scale-shard-map-management.md), and include hello [client library](sql-database-elastic-database-client-library.md), hello [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md), [elastic pools](sql-database-elastic-pool.md), and [queries](sql-database-elastic-query-overview.md).</span></span> 

<span data-ttu-id="bb089-106">Deze termen worden gebruikt [toevoegen van een shard met hulpprogramma's van elastische Database](sql-database-elastic-scale-add-a-shard.md) en [hello RecoveryManager klasse toofix shard kaart problemen met](sql-database-elastic-database-recovery-manager.md).</span><span class="sxs-lookup"><span data-stu-id="bb089-106">These terms are used in [Adding a shard using Elastic Database tools](sql-database-elastic-scale-add-a-shard.md) and [Using hello RecoveryManager class toofix shard map problems](sql-database-elastic-database-recovery-manager.md).</span></span>

![Elastische Scale voorwaarden][1]

<span data-ttu-id="bb089-108">**Database**: een Azure SQL-database.</span><span class="sxs-lookup"><span data-stu-id="bb089-108">**Database**: An Azure SQL database.</span></span> 

<span data-ttu-id="bb089-109">**Gegevensafhankelijke routering**: Hallo functionaliteit waarmee een toepassing tooconnect tooa shard krijgt een specifieke sharding-sleutel.</span><span class="sxs-lookup"><span data-stu-id="bb089-109">**Data dependent routing**: hello functionality that enables an application tooconnect tooa shard given a specific sharding key.</span></span> <span data-ttu-id="bb089-110">Zie [gegevensafhankelijke routering](sql-database-elastic-scale-data-dependent-routing.md).</span><span class="sxs-lookup"><span data-stu-id="bb089-110">See [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md).</span></span> <span data-ttu-id="bb089-111">Te vergelijken**[Query meerdere Shard](sql-database-elastic-scale-multishard-querying.md)**.</span><span class="sxs-lookup"><span data-stu-id="bb089-111">Compare too**[Multi-Shard Query](sql-database-elastic-scale-multishard-querying.md)**.</span></span>

<span data-ttu-id="bb089-112">**Globale shard-toewijzing**: Hallo toewijzing tussen sharding-sleutels en hun respectieve shards binnen een **shard set**.</span><span class="sxs-lookup"><span data-stu-id="bb089-112">**Global shard map**: hello map between sharding keys and their respective shards within a **shard set**.</span></span> <span data-ttu-id="bb089-113">Hallo globale shard-toewijzing wordt opgeslagen in Hallo **shard kaart manager**.</span><span class="sxs-lookup"><span data-stu-id="bb089-113">hello global shard map is stored in hello **shard map manager**.</span></span> <span data-ttu-id="bb089-114">Te vergelijken**lokale shard-toewijzing**.</span><span class="sxs-lookup"><span data-stu-id="bb089-114">Compare too**local shard map**.</span></span>

<span data-ttu-id="bb089-115">**Lijst shard-toewijzing**: een shard-toewijzing in welke sharding sleutels afzonderlijk zijn toegewezen.</span><span class="sxs-lookup"><span data-stu-id="bb089-115">**List shard map**: A shard map in which sharding keys are mapped individually.</span></span> <span data-ttu-id="bb089-116">Te vergelijken**bereik Shard-toewijzing**.</span><span class="sxs-lookup"><span data-stu-id="bb089-116">Compare too**Range Shard Map**.</span></span>   

<span data-ttu-id="bb089-117">**Lokale shard-toewijzing**: opgeslagen op een shard, Hallo lokale shard-toewijzing toewijzingen voor Hallo shardlets die zich op Hallo shard bevinden bevat.</span><span class="sxs-lookup"><span data-stu-id="bb089-117">**Local shard map**: Stored on a shard, hello local shard map contains mappings for hello shardlets that reside on hello shard.</span></span>

<span data-ttu-id="bb089-118">**Meerdere shard query**: mogelijkheid tooissue een query op meerdere shards Hallo; resultatensets worden geretourneerd met UNION ALL semantiek (ook wel bekend als ' fan-out query').</span><span class="sxs-lookup"><span data-stu-id="bb089-118">**Multi-shard query**: hello ability tooissue a query against multiple shards; results sets are returned using UNION ALL semantics (also known as “fan-out query”).</span></span> <span data-ttu-id="bb089-119">Te vergelijken**gegevensafhankelijke routering**.</span><span class="sxs-lookup"><span data-stu-id="bb089-119">Compare too**data dependent routing**.</span></span>

<span data-ttu-id="bb089-120">**Multitenant** en **één tenant**: dit betekent dat een single-tenant-database en een multitenant-database:</span><span class="sxs-lookup"><span data-stu-id="bb089-120">**Multi-tenant** and **Single-tenant**: This shows a single-tenant database and a multi-tenant database:</span></span>

![Één en multitenant-databases](./media/sql-database-elastic-scale-glossary/multi-single-simple.png)

<span data-ttu-id="bb089-122">Hier volgt een weergave van **shard** één en multitenant-databases.</span><span class="sxs-lookup"><span data-stu-id="bb089-122">Here is a representation of **sharded** single and multi-tenant databases.</span></span> 

![Één en multitenant-databases](./media/sql-database-elastic-scale-glossary/shards-single-multi.png)

<span data-ttu-id="bb089-124">**Bereik shard-toewijzing**: een shard-toewijzing in welke Hallo shard-strategie voor distributie is gebaseerd op meerdere bereiken met opeenvolgende waarden.</span><span class="sxs-lookup"><span data-stu-id="bb089-124">**Range shard map**: A shard map in which hello shard distribution strategy is based on multiple ranges of contiguous values.</span></span> 

<span data-ttu-id="bb089-125">**Verwijzen naar tabellen**: tabellen die zijn niet shard maar zijn gerepliceerd in shards.</span><span class="sxs-lookup"><span data-stu-id="bb089-125">**Reference tables**: Tables that are not sharded but are replicated across shards.</span></span> <span data-ttu-id="bb089-126">Zip-codes kunnen bijvoorbeeld worden opgeslagen in een tabel.</span><span class="sxs-lookup"><span data-stu-id="bb089-126">For example, zip codes can be stored in a reference table.</span></span> 

<span data-ttu-id="bb089-127">**Shard**: een Azure SQL-database waarin gegevens uit een gegevensset shard wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="bb089-127">**Shard**: An Azure SQL database that stores data from a sharded data set.</span></span> 

<span data-ttu-id="bb089-128">**Elasticiteit shard**: Hallo mogelijkheid tooperform beide **horizontaal schalen** en **verticaal schalen**.</span><span class="sxs-lookup"><span data-stu-id="bb089-128">**Shard elasticity**: hello ability tooperform both **horizontal scaling** and **vertical scaling**.</span></span>

<span data-ttu-id="bb089-129">**Shard tabellen**: tabellen die zijn shard, dat wil zeggen, waarvan de gegevens is verdeeld over de shards op basis van hun sharding-sleutelwaarden.</span><span class="sxs-lookup"><span data-stu-id="bb089-129">**Sharded tables**: Tables that are sharded, i.e., whose data is distributed across shards based on their sharding key values.</span></span> 

<span data-ttu-id="bb089-130">**Sharding sleutel**: een waarde in de kolom die bepaalt hoe de gegevens is verdeeld over shards.</span><span class="sxs-lookup"><span data-stu-id="bb089-130">**Sharding key**: A column value that determines how data is distributed across shards.</span></span> <span data-ttu-id="bb089-131">Hallo waardetype kan bestaan uit een van de volgende Hallo: **int**, **bigint**, **varbinary**, of **uniqueidentifier**.</span><span class="sxs-lookup"><span data-stu-id="bb089-131">hello value type can be one of hello following: **int**, **bigint**, **varbinary**, or **uniqueidentifier**.</span></span> 

<span data-ttu-id="bb089-132">**Shard set**: Hallo verzameling shards die toegewezen toohello zijn dezelfde shard-toewijzing in Hallo shard-toewijzing beheer.</span><span class="sxs-lookup"><span data-stu-id="bb089-132">**Shard set**: hello collection of shards that are attributed toohello same shard map in hello shard map manager.</span></span>  

<span data-ttu-id="bb089-133">**Shardlet**: alle Hallo gegevens die zijn gekoppeld aan een enkele waarde van een sharding-sleutel op een shard.</span><span class="sxs-lookup"><span data-stu-id="bb089-133">**Shardlet**: All of hello data associated with a single value of a sharding key on a shard.</span></span> <span data-ttu-id="bb089-134">Een shardlet is Hallo kleinste eenheid van de verplaatsing van gegevens mogelijk wanneer herdistribueren shard tabellen.</span><span class="sxs-lookup"><span data-stu-id="bb089-134">A shardlet is hello smallest unit of data movement possible when redistributing sharded tables.</span></span> 

<span data-ttu-id="bb089-135">**Shard-toewijzing**: Hallo verzameling toewijzingen tussen sharding-sleutels en hun respectieve shards.</span><span class="sxs-lookup"><span data-stu-id="bb089-135">**Shard map**: hello set of mappings between sharding keys and their respective shards.</span></span>

<span data-ttu-id="bb089-136">**Beheer van shard-toewijzing**: een store, management-object en gegevens die Hallo shard toewijzing(en), shard-locaties en toewijzingen voor een of meer sets van shard bevat.</span><span class="sxs-lookup"><span data-stu-id="bb089-136">**Shard map manager**: A management object and data store that contains hello shard map(s), shard locations, and mappings for one or more shard sets.</span></span>

![Toewijzingen][2]

## <a name="verbs"></a><span data-ttu-id="bb089-138">Termen</span><span class="sxs-lookup"><span data-stu-id="bb089-138">Verbs</span></span>
<span data-ttu-id="bb089-139">**Horizontaal schalen**: Hallo act van schaling uit (of in) een verzameling van shards door toe te voegen of te verwijderen van shards tooa shard-kaart, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="bb089-139">**Horizontal scaling**: hello act of scaling out (or in) a collection of shards by adding or removing shards tooa shard map, as shown below.</span></span>

![Horizontale en verticale schalen][3]

<span data-ttu-id="bb089-141">**Samenvoegen**: Hallo handeling shardlets verplaatsen van twee shards tooone shard en Hallo shard-toewijzing dienovereenkomstig bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="bb089-141">**Merge**: hello act of moving shardlets from two shards tooone shard and updating hello shard map accordingly.</span></span>

<span data-ttu-id="bb089-142">**Shardlet verplaatsen**: Hallo act van een andere shard van één shardlet tooa verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="bb089-142">**Shardlet move**: hello act of moving a single shardlet tooa different shard.</span></span> 

<span data-ttu-id="bb089-143">**Shard**: Hallo act van het partitioneren van horizontaal identiek gestructureerde gegevens over meerdere databases op basis van een sharding-sleutel.</span><span class="sxs-lookup"><span data-stu-id="bb089-143">**Shard**: hello act of horizontally partitioning identically structured data across multiple databases based on a sharding key.</span></span>

<span data-ttu-id="bb089-144">**Gesplitste**: Hallo act van verschillende shardlets verplaatsen van één shard tooanother (meestal nieuwe) shard.</span><span class="sxs-lookup"><span data-stu-id="bb089-144">**Split**: hello act of moving several shardlets from one shard tooanother (typically new) shard.</span></span> <span data-ttu-id="bb089-145">Een sharding-sleutel wordt geleverd door de gebruiker Hallo huidige Hallo punt splitsen.</span><span class="sxs-lookup"><span data-stu-id="bb089-145">A sharding key is provided by hello user as hello split point.</span></span>

<span data-ttu-id="bb089-146">**Verticale schaal**: Hallo act van schaal omhoog (of omlaag) Hallo prestatieniveau van een afzonderlijke shard.</span><span class="sxs-lookup"><span data-stu-id="bb089-146">**Vertical Scaling**: hello act of scaling up (or down) hello performance level of an individual shard.</span></span> <span data-ttu-id="bb089-147">Bijvoorbeeld, een shard wordt gewijzigd van standaard tooPremium (die resulteert in meer bronnen).</span><span class="sxs-lookup"><span data-stu-id="bb089-147">For example, changing a shard from Standard tooPremium (which results in more computing resources).</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-glossary/glossary.png
[2]: ./media/sql-database-elastic-scale-glossary/mappings.png
[3]: ./media/sql-database-elastic-scale-glossary/h_versus_vert.png

