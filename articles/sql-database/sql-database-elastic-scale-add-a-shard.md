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
# <a name="adding-a-shard-using-elastic-database-tools"></a>Toevoegen van een shard met hulpprogramma's van elastische Database
## <a name="tooadd-a-shard-for-a-new-range-or-key"></a>tooadd een shard voor een nieuw bereik of de sleutel
Toepassingen vaak moet toosimply nieuwe shards toohandle gegevens toevoegen die wordt verwacht van de nieuwe sleutels of sleutelbereiken, voor een shard-toewijzing die al bestaat. Bijvoorbeeld, een toepassing shard door Tenant-ID moet mogelijk een nieuwe shard tooprovision voor een nieuwe tenant of gegevens shard maandelijks moet mogelijk een nieuwe shard ingericht voordat Hallo begin van elke nieuwe maand. 

Als nieuw bereik Hallo sleutelwaarden nog niet is onderdeel van een bestaande toewijzing, is het zeer eenvoudig tooadd Hallo nieuwe shard en koppel Hallo nieuwe sleutel of het bereik toothat shard. 

### <a name="example--adding-a-shard-and-its-range-tooan-existing-shard-map"></a>Voorbeeld: een shard en bijbehorende bereik tooan bestaande shard-toewijzing toe te voegen
In dit voorbeeld gebruikt Hallo [TryGetShard](https://msdn.microsoft.com/library/azure/dn823929.aspx) hello [CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx), [CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn807221.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeShardMap`1.CreateRangeMapping\(Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeMappingCreationInfo{`0}\)) methoden, en maakt een exemplaar van Hallo [ShardLocation](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardlocation.shardlocation.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardLocation.) klasse. In de steekproef Hallo hieronder een database met naam **sample_shard_2** en alle benodigde schemaobjecten daarbinnen zijn gemaakt toohold bereik [300, 400).  

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


Als alternatief kunt u Powershell toocreate een nieuwe Manager van de Shard-toewijzing. Een voorbeeld is beschikbaar [hier](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).

## <a name="tooadd-a-shard-for-an-empty-part-of-an-existing-range"></a>tooadd een shard voor een leeg deel uitmaken van een bestaand bereik
In sommige gevallen kan een bereik tooa shard al toegewezen en deze gedeeltelijk is gevuld met gegevens, maar u nu toekomstige gegevens toobe gerichte tooa verschillende shard. Bijvoorbeeld, u shard per dag liggen en 50 dagen tooa shard, al is toegewezen, maar op dag 24, de gewenste tooland toekomstige gegevens in een andere shard. Hallo elastische database [gesplitste merge tool](sql-database-elastic-scale-overview-split-and-merge.md) kunnen deze bewerking uitvoeren, maar als verplaatsing van gegevens niet nodig (bijvoorbeeld gegevens voor Hallo reeks dagen [25, 50), dat wil zeggen, inclusief too50 dag 25 exclusieve, nog niet bestaat) u kunt uitvoeren Dit geheel met behulp van de API's voor beheer van Shard-toewijzing rechtstreeks Hallo.

### <a name="example-splitting-a-range-and-assigning-hello-empty-portion-tooa-newly-added-shard"></a>Voorbeeld: splitsen van een bereik en het toewijzen van Hallo leeg gedeelte tooa toegevoegde shard
Een database met naam 'sample_shard_2' en alle benodigde schemaobjecten daarbinnen zijn gemaakt.  

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

**Belangrijke**: Gebruik deze methode alleen als u bepaalde die bereik voor Hallo Hallo bijgewerkt toewijzing leeg is.  Hallo-methoden die hierboven niet controleren voor Hallo bereik worden verplaatst, dus is het beste tooinclude controleert in uw code.  Als rijen bestaan in Hallo bereik worden verplaatst, wordt de werkelijke gegevensdistributie Hallo niet overeen met Hallo bijgewerkte shard-toewijzing. Gebruik Hallo [gesplitste merge tool](sql-database-elastic-scale-overview-split-and-merge.md) tooperform Hallo bewerking in plaats daarvan in dergelijke gevallen.  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

