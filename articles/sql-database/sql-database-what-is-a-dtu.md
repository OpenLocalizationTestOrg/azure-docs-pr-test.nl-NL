---
title: 'SQL Database: wat is een DTU? | Microsoft Docs'
description: Inzicht in wat een Azure SQL Database-transactie-eenheid is.
keywords: databaseopties, prestaties van de database
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: CarlRabeler
ms.assetid: 89e3e9ce-2eeb-4949-b40f-6fc3bf520538
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: NA
ms.date: 04/13/2017
ms.author: carlrab
ms.openlocfilehash: ba1fe580b32826259edaf6c8dc124faaf5b3d234
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="explaining-database-transaction-units-dtus-and-elastic-database-transaction-units-edtus"></a>Over DTU's (Database Transaction Units) en eDTU's (elastische Database Transaction Units)
Dit artikel wordt uitgelegd's (Database Transaction Units) en elastische Database Transaction Units (edtu's) en wat er gebeurt als u raakt Hallo maximum aantal dtu's of edtu's.  

## <a name="what-are-database-transaction-units-dtus"></a>Wat zijn DTU's (Database Transaction Units)?
Voor één Azure SQL database op een specifiek prestatieniveau binnen een [servicelaag](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels), Microsoft garandeert een bepaalde mate van resources voor die database (onafhankelijk van een andere database in Azure-cloud Hallo) en het geven van een voorspelbare niveau van de prestaties. Deze hoeveelheid resources wordt berekend als een aantal Database Transaction Units of dtu's en is een gecombineerde meting van CPU, geheugen, i/o (gegevens en transactie logboekregistratie i/o). Hallo-verhouding onder deze resources oorspronkelijk is bepaald door een [benchmark-OLTP-werkbelasting](sql-database-benchmark-overview.md) ontworpen toobe typische van echte OLTP-werkbelastingen. Wanneer uw werkbelasting Hallo bedrag van elk van deze resources overschrijdt, wordt uw doorvoer is beperkte - resulterende in tragere prestaties en time-outs. Hallo-bronnen worden gebruikt door de werkbelasting van uw hebben geen invloed op Hallo resources beschikbaar tooother SQL-databases in hello Azure-cloud en Hallo resource die wordt gebruikt door andere werkbelastingen hebben geen invloed op Hallo resources beschikbaar tooyour SQL-database.

![selectiekader](./media/sql-database-what-is-a-dtu/bounding-box.png)

Dtu's zijn handig voor understanding Hallo relatieve hoeveelheid resources tussen Azure SQL-Databases op verschillende prestatieniveaus en Servicelagen. Bijvoorbeeld gelijk Hallo dtu's verdubbeld doordat Hallo prestatieniveau van een database toodoubling Hallo set beschikbaar toothat resourcedatabase. Zo biedt een Premium P11-database met 1750 DTU's 350 keer meer DTU aan rekenvermogen dan een Basic-database met 5 DTU's.  

toogain dieper inzicht in hello (DTU) resourceverbruik van uw werkbelasting, gebruik [Azure SQL Database Query Performance Insight](sql-database-query-performance.md) naar:

- Hallo top-query's op het aantal CPU/duur/uitvoering die mogelijk kan worden afgestemd voor verbeterde prestaties identificeren. Bijvoorbeeld, een i/o-intensieve query kan profiteren van Hallo gebruik van [in het geheugen optimalisatietechnieken](sql-database-in-memory.md) toomake beter gebruik van het beschikbare geheugen op een bepaalde prijscategorie en prestatieniveau serviceniveau Hallo.
- Inzoomen op Hallo details van een query, geven de tekst en de geschiedenis van bronnen beter worden benut.
- Access-prestaties afstemmen van de aanbevelingen die acties uitgevoerd door weergeven [SQL Database Advisor](sql-database-advisor.md).

U kunt [Servicelagen wijzigen](sql-database-service-tiers.md) op elk gewenst moment met minimale downtime tooyour toepassing (gemiddeld over het algemeen binnen vier seconden). Voor veel bedrijven en apps kunnen toocreate databases wordt en bellen prestaties omhoog of omlaag op aanvraag al voldoende, vooral als de gebruikspatronen redelijk voorspelbaar zijn. Maar als er onvoorspelbare gebruikspatronen, het, kunt u harde toomanage kosten en uw bedrijfsmodel. In dit scenario gebruikt u een elastische pool met een bepaald aantal edtu's die worden gedeeld door meerdere database in Hallo-pool.

![Inleiding tooSQL Database: één database dtu's per laag en niveau](./media/sql-database-what-is-a-dtu/single_db_dtus.png)

## <a name="what-are-elastic-database-transaction-units-edtus"></a>Wat zijn eDTU's (elastische Database Transaction Units)?
In plaats daarvan dan bieden een specifieke set resources (dtu's) tooa SQL-Database die altijd beschikbaar ongeacht of die niet nodig zijn, u kunt plaatsen databases in een [elastische pool](sql-database-elastic-pool.md) op een SQL-Database-server die een verzameling resources deelt onder deze database. Hallo gedeelde bronnen in een elastische pool gemeten door elastische Database Transaction Units of edtu's. Elastische pools bieden een eenvoudige, rendabele oplossing toomanage Hallo prestatiedoelstellingen voor meerdere databases met breed uiteenlopende en onvoorspelbare gebruikspatronen. U kunt in een elastische pool garanderen dat geen één database maakt gebruik van alle resources Hallo in Hallo van toepassingen en ook dat de minimale hoeveelheid resources is altijd beschikbaar tooa database in een elastische pool. Zie [elastische pools](sql-database-elastic-pool.md) voor meer informatie.

![Inleiding tooSQL Database: edtu's per laag en niveau](./media/sql-database-what-is-a-dtu/sqldb_elastic_pools.png)

Een pool krijgt een bepaald aantal eDTU's voor een vaste prijs. In de elastische pool hello krijgen afzonderlijke databases Hallo flexibiliteit tooauto-scale binnen de grenzen van Hallo geconfigureerd. Een database kan meer edtu's toomeet vraag gebruiken terwijl databases onder lichte lading minder toohello punt verbruikt dat databases onder geen load geen edtu's gebruiken onder een zware belasting. Door het inrichten van resources voor de hele pool Hallo plaats per database beheertaken zijn vereenvoudigd en u hebt een voorspelbare budget voor Hallo van toepassingen.

Aanvullende edtu's kunnen tooan bestaande toepassingen zonder uitvaltijd voor de database en geen invloed hebben op Hallo-databases in Hallo groep worden toegevoegd. En als de extra eDTU's niet meer nodig zijn, kunnen ze op elk moment uit een bestaande pool worden verwijderd. U kunt toevoegen of afgetrokken databases toohello groep of limiet Hallo hoeveelheid edtu's dat een database onder een zware belasting tooreserve edtu's kunt gebruiken voor andere databases. Als een database is zoals verwacht onder-gebruik van bronnen die u kunt verlaten Hallo van toepassingen en configureren als een individuele database met voorspelbare hoeveelheid resources die zijn vereist.

## <a name="how-can-i-determine-hello-number-of-dtus-needed-by-my-workload"></a>Hoe kan ik het aantal dtu's dat nodig is voor mijn werkbelasting Hallo zien?
Als u toomigrate een bestaande on-premises of virtuele machine werkbelasting tooAzure SQL-Database van SQL Server zoeken wilt, kunt u Hallo [DTU Calculator](http://dtucalculator.azurewebsites.net/) tooapproximate Hallo aantal dtu's dat nodig is. Voor de werkbelasting van een bestaande Azure SQL Database, kunt u [SQL Database Query Performance Insight](sql-database-query-performance.md) toounderstand uw database resource verbruik (dtu's) tooget dieper inzicht in hoe toooptimize uw workload. U kunt ook Hallo [sys.dm_db_ resource_stats](https://msdn.microsoft.com/library/dn800981.aspx) DMV tooget Hallo verbruik resourcegegevens voor Hallo laatste één uur. U kunt ook Hallo catalogusweergave [sys.resource_stats](http://msdn.microsoft.com/library/dn269979.aspx) kan ook worden opgevraagde tooget Hallo dezelfde gegevens voor de afgelopen veertien dagen Hallo Hoewel op een lagere betrouwbaarheid van vijf minuten gemiddelden.

## <a name="how-do-i-know-if-i-could-benefit-from-an-elastic-pool-of-resources"></a>Hoe weet ik of een elastische pool met resources voor mij voordeliger is?
Pools zijn geschikt voor een groot aantal databases met specifieke gebruikspatronen. Voor een bepaalde database wordt dit patroon gekenmerkt door een laag gemiddeld gebruik met relatief incidentele gebruikspieken. SQL-Database wordt automatisch evalueert Hallo historische brongebruik van de databases op een bestaande SQL-databaseserver en raadt Hallo geschikte groep configuratie in hello Azure-portal. Zie [Wanneer moet een elastische pool worden gebruikt?](sql-database-elastic-pool.md) voor meer informatie.

## <a name="what-happens-when-i-hit-my-maximum-dtus"></a>Wat gebeurt er wanneer ik het maximumaantal DTU's heb bereikt
Prestaties zijn kalibreren en geregeld tooprovide Hallo nodig resources toorun uw werkbelasting van de database van toohello max limieten toegestaan voor uw geselecteerde service laag/prestatieniveau. Als uw werkbelasting wordt roept Hallo grenzen in een van de CPU/gegevens i/o/logboek-i/o-limieten, u tooreceive Hallo bronnen op de maximaal toegestane niveau Hallo doorgaan, maar u waarschijnlijk toosee verhoogd latenties zijn voor uw query's. Deze limieten resulteren niet in fouten, maar in plaats daarvan een vertraging van de werkbelasting hello, tenzij Hallo vertraging zo ernstig wordt dat query's timing start uit. Als u de limiet hebt bereikt van het maximaal toegestane aantal gelijktijdige sessies/gebruikersaanvragen (werkthreads), treden expliciete fouten op. Zie [Azure SQL Database resource limits](sql-database-resource-limits.md) (Resourcelimieten voor Azure SQL Database) voor informatie over andere resources dan CPU, geheugen, gegevens-I/O en transactielogboek-I/O.

## <a name="next-steps"></a>Volgende stappen
* Zie [servicelaag](sql-database-service-tiers.md) voor informatie over het Hallo dtu's en beschikbaar voor individuele databases en elastische groepen met edtu's.
* Zie [Azure SQL Database resource limits](sql-database-resource-limits.md) (Resourcelimieten voor Azure SQL Database) voor informatie over andere resources dan CPU, geheugen, gegevens-I/O en transactielogboek-I/O.
* Zie [SQL Database Query Performance Insight](sql-database-query-performance.md) toounderstand uw verbruik (dtu's).
* Zie [overzicht van de SQL-Database benchmarks](sql-database-benchmark-overview.md) toounderstand Hallo methodologie achter Hallo OLTP-benchmark werkbelasting toodetermine hello DTU overlopen gebruikt.
