---
title: aaaQuery shard Azure SQL-databases | Microsoft Docs
description: Query's uitvoeren via shards Hallo-clientbibliotheek voor elastische database gebruiken.
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
editor: 
ms.assetid: a4379c15-f213-4026-ab6f-a450ee9d5758
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2016
ms.author: torsteng
ms.openlocfilehash: a1f0763935a6807b74aa9dec477714e8d117417d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="multi-shard-querying"></a>Meerdere shard opvragen
## <a name="overview"></a>Overzicht
Hello [hulpmiddelen voor elastische databases](sql-database-elastic-scale-introduction.md), u kunt shard databaseoplossingen maken. **Uitvoeren van query's met meerdere shard** wordt gebruikt voor taken zoals verzameling/rapportage gegevens waarvoor het uitvoeren van een query die zich uitstrekt over meerdere shards. (Dit te contrast[gegevensafhankelijke routering](sql-database-elastic-scale-data-dependent-routing.md), die al het werk wordt uitgevoerd op een enkele shard.) 

1. Ophalen van een [ **RangeShardMap** ](https://msdn.microsoft.com/library/azure/dn807318.aspx) of [ **ListShardMap** ](https://msdn.microsoft.com/library/azure/dn807370.aspx) met Hallo [ **TryGetRangeShardMap** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), Hallo [ **TryGetListShardMap**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), of Hallo [ **GetShardMap** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) methode. Zie [ **samenstellen van een ShardMapManager** ](sql-database-elastic-scale-shard-map-management.md#constructing-a-shardmapmanager) en [ **ophalen van een RangeShardMap of ListShardMap**](sql-database-elastic-scale-shard-map-management.md#get-a-rangeshardmap-or-listshardmap).
2. Maak een  **[MultiShardConnection](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardconnection.aspx)**  object.
3. Maak een  **[MultiShardCommand](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.aspx)**. 
4. Set Hallo  **[eigenschap CommandText](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.commandtext.aspx#P:Microsoft.Azure.SqlDatabase.ElasticScale.Query.MultiShardCommand.CommandText)**  tooa T-SQL-opdracht.
5. Hallo-opdracht uitvoeren door de aanroepende Hallo  **[ExecuteReader methode](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.executereader.aspx)**.
6. Met behulp van Hallo Hallo-resultaten weergeven  **[MultiShardDataReader klasse](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multisharddatareader.aspx)**. 

## <a name="example"></a>Voorbeeld
Hallo volgende code laat zien Hallo gebruik van meerdere shard uitvoeren van query's met behulp van een bepaalde **ShardMap** met de naam *myShardMap*. 

    using (MultiShardConnection conn = new MultiShardConnection( 
                                        myShardMap.GetShards(), 
                                        myShardConnectionString) 
          ) 
    { 
    using (MultiShardCommand cmd = conn.CreateCommand())
           { 
            cmd.CommandText = "SELECT c1, c2, c3 FROM ShardedTable"; 
            cmd.CommandType = CommandType.Text; 
            cmd.ExecutionOptions = MultiShardExecutionOptions.IncludeShardNameColumn; 
            cmd.ExecutionPolicy = MultiShardExecutionPolicy.PartialResults; 

            using (MultiShardDataReader sdr = cmd.ExecuteReader()) 
                { 
                    while (sdr.Read())
                        { 
                            var c1Field = sdr.GetString(0); 
                            var c2Field = sdr.GetFieldValue<int>(1); 
                            var c3Field = sdr.GetFieldValue<Int64>(2);
                        } 
                 } 
           } 
    } 


Een belangrijk verschil is Hallo constructie van meerdere shard-verbindingen. Waar **SqlConnection** is van invloed op een individuele database hello **MultiShardConnection** duurt een ***verzameling shards*** als invoer. Vul Hallo verzameling shards uit een shard-toewijzing. Hallo-query wordt vervolgens uitgevoerd op Hallo-verzameling van shards met **UNION ALL** semantiek tooassemble één algemene resultaat. Hallo-naam van Hallo shard waar Hallo rij is afkomstig uit kunt eventueel de toegevoegd toohello uitvoer met behulp van Hallo **ExecutionOptions** eigenschap op de opdracht. 

Houd er rekening mee Hallo aanroep te**myShardMap.GetShards()**. Deze methode haalt alle shards uit Hallo shard-toewijzing en biedt een eenvoudige manier toorun een query voor alle relevante databases. Hallo verzameling shards voor een query meerdere shard kan verfijnd verder door het uitvoeren van een LINQ opvragen over Hallo verzamelen die wordt geretourneerd door Hallo te**myShardMap.GetShards()**. In combinatie met Hallo gedeeltelijke resultaten beleid is de huidige capaciteit Hallo in meerdere shard opvragen ontworpen toowork voor tientallen up toohundreds met shards.

Een beperking voor het uitvoeren van query's met meerdere shard is momenteel Hallo gebrek aan validatie voor shards en shardlets die worden opgevraagd. Tijdens het gegevensafhankelijke routering, bevestigt dat een bepaalde shard deel van Hallo shard-toewijzing op moment van query's op Hallo uitmaakt, Voer meerdere shard-query's niet deze controle uit. Dit kan leiden toomulti shard-query uitvoeren op databases die zijn verwijderd uit Hallo shard-toewijzing.

## <a name="multi-shard-queries-and-split-merge-operations"></a>Meerdere shard-query's en gesplitste samenvoegbewerkingen
Meerdere shard-query's controleren niet of shardlets op Hallo van de query database lopende gesplitste merge-bewerkingen deelnemen. (Zie [vergroten/verkleinen met Hallo elastische Database split-samenvoegen hulpprogramma](sql-database-elastic-scale-overview-split-and-merge.md).) Dit kan leiden tooinconsistencies waar rijen van dezelfde shardlet weergeven voor meerdere databases in Hallo Hallo dezelfde meerdere shard-query. Houd rekening met deze beperkingen en overweeg een verwerkingsstop voor lopende gesplitste samenvoegen bewerkingen en wijzigingen toohello shard kaart tijdens het uitvoeren van query's met meerdere shard.

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

## <a name="see-also"></a>Zie ook
**[System.Data.SqlClient](http://msdn.microsoft.com/library/System.Data.SqlClient.aspx)**  klassen en methoden.

Beheren met behulp van Hallo shards [clientbibliotheek voor elastische Database](sql-database-elastic-database-client-library.md). Bevat een naamruimte aangeroepen [Microsoft.Azure.SqlDatabase.ElasticScale.Query](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.aspx) die Hallo mogelijkheid tooquery biedt meerdere shards met een enkele query en het resultaat. Biedt een query uitvoert abstractie via een verzameling met shards. Het bevat ook alternatieve uitvoeringsbeleidsregels, met name gedeeltelijke resultaten, toodeal met fouten tijdens het opvragen via veel shards.  

