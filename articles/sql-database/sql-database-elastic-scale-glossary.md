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
# <a name="elastic-database-tools-glossary"></a>Elastische Database extra verklarende woordenlijst
Hallo volgende termen gedefinieerd voor Hallo [hulpmiddelen voor elastische databases](sql-database-elastic-scale-introduction.md), een functie van Azure SQL Database. Hallo hulpprogramma's zijn gebruikte toomanage [shard toegewezen](sql-database-elastic-scale-shard-map-management.md), en bevatten Hallo [clientbibliotheek](sql-database-elastic-database-client-library.md), Hallo [gesplitste merge tool](sql-database-elastic-scale-overview-split-and-merge.md), [elastische pools](sql-database-elastic-pool.md), en [query's](sql-database-elastic-query-overview.md). 

Deze termen worden gebruikt [toevoegen van een shard met hulpprogramma's van elastische Database](sql-database-elastic-scale-add-a-shard.md) en [hello RecoveryManager klasse toofix shard kaart problemen met](sql-database-elastic-database-recovery-manager.md).

![Elastische Scale voorwaarden][1]

**Database**: een Azure SQL-database. 

**Gegevensafhankelijke routering**: Hallo functionaliteit waarmee een toepassing tooconnect tooa shard krijgt een specifieke sharding-sleutel. Zie [gegevensafhankelijke routering](sql-database-elastic-scale-data-dependent-routing.md). Te vergelijken**[Query meerdere Shard](sql-database-elastic-scale-multishard-querying.md)**.

**Globale shard-toewijzing**: Hallo toewijzing tussen sharding-sleutels en hun respectieve shards binnen een **shard set**. Hallo globale shard-toewijzing wordt opgeslagen in Hallo **shard kaart manager**. Te vergelijken**lokale shard-toewijzing**.

**Lijst shard-toewijzing**: een shard-toewijzing in welke sharding sleutels afzonderlijk zijn toegewezen. Te vergelijken**bereik Shard-toewijzing**.   

**Lokale shard-toewijzing**: opgeslagen op een shard, Hallo lokale shard-toewijzing toewijzingen voor Hallo shardlets die zich op Hallo shard bevinden bevat.

**Meerdere shard query**: mogelijkheid tooissue een query op meerdere shards Hallo; resultatensets worden geretourneerd met UNION ALL semantiek (ook wel bekend als ' fan-out query'). Te vergelijken**gegevensafhankelijke routering**.

**Multitenant** en **één tenant**: dit betekent dat een single-tenant-database en een multitenant-database:

![Één en multitenant-databases](./media/sql-database-elastic-scale-glossary/multi-single-simple.png)

Hier volgt een weergave van **shard** één en multitenant-databases. 

![Één en multitenant-databases](./media/sql-database-elastic-scale-glossary/shards-single-multi.png)

**Bereik shard-toewijzing**: een shard-toewijzing in welke Hallo shard-strategie voor distributie is gebaseerd op meerdere bereiken met opeenvolgende waarden. 

**Verwijzen naar tabellen**: tabellen die zijn niet shard maar zijn gerepliceerd in shards. Zip-codes kunnen bijvoorbeeld worden opgeslagen in een tabel. 

**Shard**: een Azure SQL-database waarin gegevens uit een gegevensset shard wordt opgeslagen. 

**Elasticiteit shard**: Hallo mogelijkheid tooperform beide **horizontaal schalen** en **verticaal schalen**.

**Shard tabellen**: tabellen die zijn shard, dat wil zeggen, waarvan de gegevens is verdeeld over de shards op basis van hun sharding-sleutelwaarden. 

**Sharding sleutel**: een waarde in de kolom die bepaalt hoe de gegevens is verdeeld over shards. Hallo waardetype kan bestaan uit een van de volgende Hallo: **int**, **bigint**, **varbinary**, of **uniqueidentifier**. 

**Shard set**: Hallo verzameling shards die toegewezen toohello zijn dezelfde shard-toewijzing in Hallo shard-toewijzing beheer.  

**Shardlet**: alle Hallo gegevens die zijn gekoppeld aan een enkele waarde van een sharding-sleutel op een shard. Een shardlet is Hallo kleinste eenheid van de verplaatsing van gegevens mogelijk wanneer herdistribueren shard tabellen. 

**Shard-toewijzing**: Hallo verzameling toewijzingen tussen sharding-sleutels en hun respectieve shards.

**Beheer van shard-toewijzing**: een store, management-object en gegevens die Hallo shard toewijzing(en), shard-locaties en toewijzingen voor een of meer sets van shard bevat.

![Toewijzingen][2]

## <a name="verbs"></a>Termen
**Horizontaal schalen**: Hallo act van schaling uit (of in) een verzameling van shards door toe te voegen of te verwijderen van shards tooa shard-kaart, zoals hieronder wordt weergegeven.

![Horizontale en verticale schalen][3]

**Samenvoegen**: Hallo handeling shardlets verplaatsen van twee shards tooone shard en Hallo shard-toewijzing dienovereenkomstig bijgewerkt.

**Shardlet verplaatsen**: Hallo act van een andere shard van één shardlet tooa verplaatsen. 

**Shard**: Hallo act van het partitioneren van horizontaal identiek gestructureerde gegevens over meerdere databases op basis van een sharding-sleutel.

**Gesplitste**: Hallo act van verschillende shardlets verplaatsen van één shard tooanother (meestal nieuwe) shard. Een sharding-sleutel wordt geleverd door de gebruiker Hallo huidige Hallo punt splitsen.

**Verticale schaal**: Hallo act van schaal omhoog (of omlaag) Hallo prestatieniveau van een afzonderlijke shard. Bijvoorbeeld, een shard wordt gewijzigd van standaard tooPremium (die resulteert in meer bronnen). 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-glossary/glossary.png
[2]: ./media/sql-database-elastic-scale-glossary/mappings.png
[3]: ./media/sql-database-elastic-scale-glossary/h_versus_vert.png

