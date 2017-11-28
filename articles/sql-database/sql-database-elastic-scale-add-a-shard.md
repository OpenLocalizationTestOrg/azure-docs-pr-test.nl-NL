---
title: aaaAdding een shard met hulpprogramma's van elastische database | Microsoft Docs
description: Hoe Elastic Scale API's tooadd nieuwe shards tooa shard toouse instelt.
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 62a349db-bebe-406f-a120-2f1986f2b286
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: f44b59578376d1238b3012a3cb52339978079f0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="adding-a-shard-using-elastic-database-tools"></a><span data-ttu-id="884cd-103">Toevoegen van een shard met hulpprogramma's van elastische Database</span><span class="sxs-lookup"><span data-stu-id="884cd-103">Adding a shard using Elastic Database tools</span></span>
## <a name="tooadd-a-shard-for-a-new-range-or-key"></a><span data-ttu-id="884cd-104">tooadd een shard voor een nieuw bereik of de sleutel</span><span class="sxs-lookup"><span data-stu-id="884cd-104">tooadd a shard for a new range or key</span></span>
<span data-ttu-id="884cd-105">Toepassingen vaak moet toosimply nieuwe shards toohandle gegevens toevoegen die wordt verwacht van de nieuwe sleutels of sleutelbereiken, voor een shard-toewijzing die al bestaat.</span><span class="sxs-lookup"><span data-stu-id="884cd-105">Applications often need toosimply add new shards toohandle data that is expected from new keys or key ranges, for a shard map that already exists.</span></span> <span data-ttu-id="884cd-106">Bijvoorbeeld, een toepassing shard door Tenant-ID moet mogelijk een nieuwe shard tooprovision voor een nieuwe tenant of gegevens shard maandelijks moet mogelijk een nieuwe shard ingericht voordat Hallo begin van elke nieuwe maand.</span><span class="sxs-lookup"><span data-stu-id="884cd-106">For example, an application sharded by Tenant ID may need tooprovision a new shard for a new tenant, or data sharded monthly may need a new shard provisioned before hello start of each new month.</span></span> 

<span data-ttu-id="884cd-107">Als nieuw bereik Hallo sleutelwaarden nog niet is onderdeel van een bestaande toewijzing, is het zeer eenvoudig tooadd Hallo nieuwe shard en koppel Hallo nieuwe sleutel of het bereik toothat shard.</span><span class="sxs-lookup"><span data-stu-id="884cd-107">If hello new range of key values is not already part of an existing mapping, it is very simple tooadd hello new shard and associate hello new key or range toothat shard.</span></span> 

### <a name="example--adding-a-shard-and-its-range-tooan-existing-shard-map"></a><span data-ttu-id="884cd-108">Voorbeeld: een shard en bijbehorende bereik tooan bestaande shard-toewijzing toe te voegen</span><span class="sxs-lookup"><span data-stu-id="884cd-108">Example:  adding a shard and its range tooan existing shard map</span></span>
<span data-ttu-id="884cd-109">In dit voorbeeld gebruikt Hallo [TryGetShard](https://msdn.microsoft.com/library/azure/dn823929.aspx) hello [CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx), [CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn807221.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeShardMap`1.CreateRangeMapping\(Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeMappingCreationInfo{`0}\)) methoden, en maakt een exemplaar van Hallo [ShardLocation](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardlocation.shardlocation.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardLocation.) klasse.</span><span class="sxs-lookup"><span data-stu-id="884cd-109">This sample uses hello [TryGetShard](https://msdn.microsoft.com/library/azure/dn823929.aspx) hello [CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx), [CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn807221.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeShardMap`1.CreateRangeMapping\(Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeMappingCreationInfo{`0}\)) methods, and creates an instance of hello [ShardLocation](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardlocation.shardlocation.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardLocation.) class.</span></span> <span data-ttu-id="884cd-110">In de steekproef Hallo hieronder een database met naam **sample_shard_2** en alle benodigde schemaobjecten daarbinnen zijn gemaakt toohold bereik [300, 400).</span><span class="sxs-lookup"><span data-stu-id="884cd-110">In hello sample below, a database named **sample_shard_2** and all necessary schema objects inside of it have been created toohold range [300, 400).</span></span>  

    // sm is a RangeShardMap object.
    // Add a new shard toohold hello range being added. 
    Shard shard2 = null; 

    if (!sm.TryGetShard(new ShardLocation(shardServer, "sample_shard_2"),out shard2)) 
    { 
        shard2 = sm.CreateShard(new ShardLocation(shardServer, "sample_shard_2"));  
    } 

    // Create hello mapping and associate it with hello new shard 
    sm.CreateRangeMapping(new RangeMappingCreationInfo<long> 
                            (new Range<long>(300, 400), shard2, MappingStatus.Online)); 


<span data-ttu-id="884cd-111">Als alternatief kunt u Powershell toocreate een nieuwe Manager van de Shard-toewijzing.</span><span class="sxs-lookup"><span data-stu-id="884cd-111">As an alternative, you can use Powershell toocreate a new Shard Map Manager.</span></span> <span data-ttu-id="884cd-112">Een voorbeeld is beschikbaar [hier](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="884cd-112">An example is available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

## <a name="tooadd-a-shard-for-an-empty-part-of-an-existing-range"></a><span data-ttu-id="884cd-113">tooadd een shard voor een leeg deel uitmaken van een bestaand bereik</span><span class="sxs-lookup"><span data-stu-id="884cd-113">tooadd a shard for an empty part of an existing range</span></span>
<span data-ttu-id="884cd-114">In sommige gevallen kan een bereik tooa shard al toegewezen en deze gedeeltelijk is gevuld met gegevens, maar u nu toekomstige gegevens toobe gerichte tooa verschillende shard.</span><span class="sxs-lookup"><span data-stu-id="884cd-114">In some circumstances, you may have already mapped a range tooa shard and partially filled it with data, but you now want upcoming data toobe directed tooa different shard.</span></span> <span data-ttu-id="884cd-115">Bijvoorbeeld, u shard per dag liggen en 50 dagen tooa shard, al is toegewezen, maar op dag 24, de gewenste tooland toekomstige gegevens in een andere shard.</span><span class="sxs-lookup"><span data-stu-id="884cd-115">For example, you shard by day range and have already allocated 50 days tooa shard, but on day 24, you want future data tooland in a different shard.</span></span> <span data-ttu-id="884cd-116">Hallo elastische database [gesplitste merge tool](sql-database-elastic-scale-overview-split-and-merge.md) kunnen deze bewerking uitvoeren, maar als verplaatsing van gegevens niet nodig (bijvoorbeeld gegevens voor Hallo reeks dagen [25, 50), dat wil zeggen, inclusief too50 dag 25 exclusieve, nog niet bestaat) u kunt uitvoeren Dit geheel met behulp van de API's voor beheer van Shard-toewijzing rechtstreeks Hallo.</span><span class="sxs-lookup"><span data-stu-id="884cd-116">hello elastic database [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md) can perform this operation, but if data movement is not necessary (for example, data for hello range of days [25, 50), i.e., day 25 inclusive too50 exclusive, does not yet exist) you can perform this entirely using hello Shard Map Management APIs directly.</span></span>

### <a name="example-splitting-a-range-and-assigning-hello-empty-portion-tooa-newly-added-shard"></a><span data-ttu-id="884cd-117">Voorbeeld: splitsen van een bereik en het toewijzen van Hallo leeg gedeelte tooa toegevoegde shard</span><span class="sxs-lookup"><span data-stu-id="884cd-117">Example: splitting a range and assigning hello empty portion tooa newly-added shard</span></span>
<span data-ttu-id="884cd-118">Een database met naam 'sample_shard_2' en alle benodigde schemaobjecten daarbinnen zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="884cd-118">A database named “sample_shard_2” and all necessary schema objects inside of it have been created.</span></span>  

    // sm is a RangeShardMap object.
    // Add a new shard toohold hello range we will move 
    Shard shard2 = null; 

    if (!sm.TryGetShard(new ShardLocation(shardServer, "sample_shard_2"),out shard2)) 
    { 

        shard2 = sm.CreateShard(new ShardLocation(shardServer, "sample_shard_2"));  
    } 

    // Split hello Range holding Key 25 

    sm.SplitMapping(sm.GetMappingForKey(25), 25); 

    // Map new range holding [25-50) toodifferent shard: 
    // first take existing mapping offline 
    sm.MarkMappingOffline(sm.GetMappingForKey(25)); 
    // now map while offline tooa different shard and take online 
    RangeMappingUpdate upd = new RangeMappingUpdate(); 
    upd.Shard = shard2; 
    sm.MarkMappingOnline(sm.UpdateMapping(sm.GetMappingForKey(25), upd)); 

<span data-ttu-id="884cd-119">**Belangrijke**: Gebruik deze methode alleen als u bepaalde die bereik voor Hallo Hallo bijgewerkt toewijzing leeg is.</span><span class="sxs-lookup"><span data-stu-id="884cd-119">**Important**:  Use this technique only if you are certain that hello range for hello updated mapping is empty.</span></span>  <span data-ttu-id="884cd-120">Hallo-methoden die hierboven niet controleren voor Hallo bereik worden verplaatst, dus is het beste tooinclude controleert in uw code.</span><span class="sxs-lookup"><span data-stu-id="884cd-120">hello methods above do not check data for hello range being moved, so it is best tooinclude checks in your code.</span></span>  <span data-ttu-id="884cd-121">Als rijen bestaan in Hallo bereik worden verplaatst, wordt de werkelijke gegevensdistributie Hallo niet overeen met Hallo bijgewerkte shard-toewijzing.</span><span class="sxs-lookup"><span data-stu-id="884cd-121">If rows exist in hello range being moved, hello actual data distribution will not match hello updated shard map.</span></span> <span data-ttu-id="884cd-122">Gebruik Hallo [gesplitste merge tool](sql-database-elastic-scale-overview-split-and-merge.md) tooperform Hallo bewerking in plaats daarvan in dergelijke gevallen.</span><span class="sxs-lookup"><span data-stu-id="884cd-122">Use hello [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md) tooperform hello operation instead in these cases.</span></span>  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

