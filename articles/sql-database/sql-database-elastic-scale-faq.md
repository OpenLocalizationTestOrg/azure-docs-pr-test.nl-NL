---
title: aaaAzure SQL elastische Scale Veelgestelde vragen | Microsoft Docs
description: Veelgestelde vragen over Azure SQL Database elastisch schalen.
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: e60dde9c-bb7b-4f2f-b52c-bdb506d49fcb
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 8c77902e8ce9cbbc5e081cd9d2c911d4c8dc9e5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-database-tools-faq"></a>Hulpprogramma's voor elastische database Veelgestelde vragen
#### <a name="if-i-have-a-single-tenant-per-shard-and-no-sharding-key-how-do-i-populate-hello-sharding-key-for-hello-schema-info"></a>Als ik een één-tenant per shard en geen sharding-sleutel hebt, hoe ik vullen Hallo sharding-sleutel voor schema-informatie Hallo?
Hallo schema info-object is alleen gebruikte toosplit samenvoegen scenario's. Als een toepassing inherent single-tenant is, hoeven niet Hallo gesplitste Merge tool en dus er is geen noodzaak toopopulate Hallo schema info object.

#### <a name="ive-provisioned-a-database-and-i-already-have-a-shard-map-manager-how-do-i-register-this-new-database-as-a-shard"></a>Een database hebt ingericht en ik heb al een Manager Shard-kaart, hoe kan ik deze nieuwe database registreren als een shard?
Zie  **[een shard tooan toepassing met behulp van Hallo-clientbibliotheek voor elastische database toe te voegen](sql-database-elastic-scale-add-a-shard.md)**. 

#### <a name="how-much-do-elastic-database-tools-cost"></a>Wat elastische database extra kosten?
Met behulp van de clientbibliotheek voor elastische database Hallo worden eventuele kosten. Kosten doorlopen alleen voor hello Azure SQL-databases die u gebruikt voor shards en Hallo Shard kaart Manager, evenals Hallo web/worker functies die u inricht voor Hallo gesplitste Merge tool.

#### <a name="why-are-my-credentials-not-working-when-i-add-a-shard-from-a-different-server"></a>Waarom wordt mijn referenties niet werkt wanneer ik een shard uit een andere server toevoegen?
Gebruik geen referenties in de vorm van Hallo ' gebruikers-ID =username@servername', in plaats daarvan gewoon gebruiken ' gebruikers-ID = gebruikersnaam '.  Zorg ook dat 'gebruikersnaam' hello aanmelding de juiste machtigingen heeft op Hallo shard.

#### <a name="do-i-need-toocreate-a-shard-map-manager-and-populate-shards-every-time-i-start-my-applications"></a>Ik moet een Manager Shard-toewijzing toocreate en shards vullen telkens wanneer ik mijn toepassingen starten?
Niet-maken van de Shard-toewijzing Manager Hallo Hallo (bijvoorbeeld  **[ShardMapManagerFactory.CreateSqlShardMapManager](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx)**) is een eenmalige bewerking.  Uw toepassing hello aanroep moet gebruiken  **[ShardMapManagerFactory.TryGetSqlShardMapManager()](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx)**  tijdens het opstarten van een toepassing.  Er mag slechts één aanroep per toepassingsdomein.

#### <a name="i-have-questions-about-using-elastic-database-tools-how-do-i-get-them-answered"></a>Ik heb vragen over het gebruik van hulpprogramma's voor elastische database, hoe krijg ik ze beantwoord?
Neem contact op Hallo toous [-forum Azure SQL Database](https://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted).

#### <a name="when-i-get-a-database-connection-using-a-sharding-key-i-can-still-query-data-for-other-sharding-keys-on-hello-same-shard--is-this-by-design"></a>Bij het ophalen van een databaseverbinding met een sharding-sleutel, ik kan nog steeds gegevens opvragen voor andere sharding-codes op Hallo dezelfde shard.  Dit is standaard?
Hallo Elastic Scale API's bieden u een verbinding toohello juiste database voor uw sharding-sleutel, maar bieden geen sharding sleutel filteren.  Voeg **waar** componenten tooyour query toorestrict Hallo bereik toohello sharding-sleutel hebt opgegeven indien nodig.

#### <a name="can-i-use-a-different-azure-database-edition-for-each-shard-in-my-shard-set"></a>Kan ik een andere editie van Azure-Database gebruiken voor elke shard in mijn shard-set?
Ja, een shard is een individuele database en één shard kan dus een Premium-editie terwijl een andere een Standard-editie. Bovendien kunt Hallo-editie van een shard omhoog of omlaag schalen meerdere keren tijdens het Hallo-levensduur van Hallo shard.

#### <a name="does-hello-split-merge-tool-provision-or-delete-a-database-during-a-split-or-merge-operation"></a>Gesplitste Merge tool inrichten hello (of verwijderen) een database tijdens een bewerking splitsen of samenvoegen?
Nee. Voor **splitsen** bewerkingen, Hallo doeldatabase moet bestaan met het bijbehorende schema Hallo en Hello Shard kaart Manager zijn geregistreerd.  Voor **samenvoegen** bewerkingen, moet u Hallo shard uit Hallo shard-toewijzing manager verwijderen en vervolgens Hallo-database te verwijderen.

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

