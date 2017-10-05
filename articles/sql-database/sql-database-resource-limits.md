---
title: Limieten voor Azure SQL Database | Microsoft Docs
description: Deze pagina beschrijft enkele algemene resource beperkingen voor Azure SQL Database.
services: sql-database
documentationcenter: na
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 884e519f-23bb-4b73-a718-00658629646a
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/12/2017
ms.author: carlrab
ms.openlocfilehash: e75458db79e6c15f8d5155b71f04a20fa21818ff
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-sql-database-resource-limits"></a>Limieten voor Azure SQL Database
## <a name="overview"></a>Overzicht
Azure SQL Database beheert de beschikbare bronnen voor een database met behulp van twee verschillende mechanismen: **Resources Governance** en **afdwinging van limieten**. Dit onderwerp wordt uitgelegd dat deze twee hoofdgebieden voor bronbeheer.

## <a name="resource-governance"></a>Resource governance
Een van de ontwerpdoelstellingen van de servicecategorieën Basic, Standard, Premium en Premium RS is voor Azure SQL Database zich gedraagt alsof de database wordt uitgevoerd op de eigen machine, geïsoleerd van andere databases. Resource governance emuleert dit gedrag. Het samengevoegde Resourcegebruik bereikt de maximaal beschikbare CPU, geheugen, i/o-logboek en gegevens i/o-resources toegewezen aan de database en resource governance wachtrijen query's in uitvoering als bronnen toewijzen aan de wachtrij query's, zoals ze vrij te maken.

Als op een toegewezen machine, gebruik van alle beschikbare resources resulteert in een langer uitvoering van query's dat momenteel wordt uitgevoerd, hetgeen kan leiden tot time-outs van de opdracht op de client. Toepassingen met agressieve Pogingslogica en toepassingen die voor het uitvoeren van query's op de database met een hoge frequentie kunnen foutberichten ondervindt bij het nieuwe query's uitvoeren wanneer het maximum aantal gelijktijdige aanvragen is bereikt.

### <a name="recommendations"></a>Aanbevelingen:
Het Resourcegebruik en de gemiddelde reactietijden van query's bewaken wanneer bijna de maximale capaciteit van een database. Wanneer zich voordoen tijdens een hogere query latenties in het algemeen hebt u drie opties:

1. Verminder het aantal binnenkomende aanvragen naar de database om te voorkomen dat de time-out en de stapel van aanvragen.
2. Een hoger prestatieniveau toewijzen aan de database.
3. Query's voor het beperken van het Resourcegebruik van elke query optimaliseren. Zie de sectie Query afstemmen/Hinting in de Azure SQL Database-prestaties richtlijnen artikel voor meer informatie.

## <a name="enforcement-of-limits"></a>Afdwinging van grenzen
Bronnen dan CPU, geheugen, i/o-logboek en i/o-gegevens worden afgedwongen door de nieuwe aanvragen geweigerd wanneer limieten zijn bereikt. Wanneer een database heeft de geconfigureerde limiet bereikt, mislukken INSERT en updates die gegevens vergroot, terwijl selecteert en verwijderingen blijven werken. Clients ontvangen een [foutbericht](sql-database-develop-error-messages.md) , afhankelijk van de limiet is bereikt.

Bijvoorbeeld, zijn het aantal verbindingen met een SQL-database en het aantal gelijktijdige aanvragen die kunnen worden verwerkt beperkt. SQL-Database kunt het aantal verbindingen met de database moet groter zijn dan het aantal gelijktijdige aanvragen voor de ondersteuning van groepsgewijze verbinding nodig. Terwijl het aantal verbindingen die beschikbaar zijn, kan eenvoudig worden beheerd door de toepassing, is het aantal parallelle aanvragen vaak keren moeilijker om in te schatten en om te bepalen. Met name tijdens piekbelastingen wanneer de toepassing een verzendt te veel aanvragen of de database bereikt de resource beperkt en begint opstapelen werkthreads vanwege langer actieve query's, kunnen fouten worden aangetroffen.

## <a name="service-tiers-and-performance-levels"></a>Servicelagen en prestatieniveaus
Er zijn Servicelagen en prestatieniveaus van één database- en elastische pools.

### <a name="single-databases"></a>Individuele databases
Voor één database worden de grenzen van een database gedefinieerd door de database prijscategorie en prestatieniveau serviceniveau. De volgende tabel beschrijft de kenmerken van Basic, Standard, Premium en RS Premium-databases op verschillende prestatieniveaus.

[!INCLUDE [SQL DB service tiers table](../../includes/sql-database-service-tiers-table.md)]

> [!IMPORTANT]
> Klanten die gebruikmaken van P11 en P15 prestatieniveaus kunnen maximaal 4 TB opgenomen opslag gebruiken zonder extra kosten. Deze optie 4 TB is momenteel beschikbaar in de volgende gebieden: ons East2, VS-West, Gov ons Virginia, West-Europa, Duitsland centraal, Zuid-Oost-Azië, Japan-Oost, Australië-Oost, Canada centraal en Canada-Oost.
>

### <a name="elastic-pools"></a>Pools voor Elastic Database
[Elastische pools](sql-database-elastic-pool.md) resources delen met andere databases in de pool. De volgende tabel beschrijft de kenmerken van Basic, Standard, Premium en RS Premium elastische pools.

[!INCLUDE [SQL DB service tiers table for elastic databases](../../includes/sql-database-service-tiers-table-elastic-pools.md)]

Zie de beschrijvingen in voor een uitgebreide definitie van elke bron die is opgenomen in de vorige tabellen [Service tier mogelijkheden en beperkingen van](sql-database-performance-guidance.md#service-tier-capabilities-and-limits). Zie voor een overzicht van Servicelagen [Azure SQL Database servicecategorieën en prestatieniveaus](sql-database-service-tiers.md).

## <a name="other-sql-database-limits"></a>De limieten van andere SQL-Database
| Onderwerp | Limiet | Beschrijving |
| --- | --- | --- |
| Databases met automatische export per abonnement |10 |Automatische export kunt u een aangepaste planning voor de back-up van uw SQL-databases te maken. De evaluatieversie van dit onderdeel wordt beëindigd op 1 maart 2017.  |
| Databases per server |Maximaal 5000 |Maximaal 5000 databases zijn toegestaan per server. |
| Dtu's per server |45000 |45000 dtu's zijn toegestaan per server voor het inrichten van zelfstandige databases en elastische pools. Het totale aantal zelfstandige-databases en pools toegestaan per server wordt alleen door het aantal dtu's server beperkt.  

> [!IMPORTANT]
> Azure SQL Database geautomatiseerde exporteren bevindt zich nu in preview en wordt buiten gebruik worden gesteld op 1 maart 2017. Vanaf 1 December 2016, zich u niet langer voor het configureren van automatische export op elke SQL-database. Alle uw bestaande geautomatiseerde taken blijven werken totdat 1e maart 2017 exporteren. Na 1e December 2016, kunt u [lange bewaartermijn van de back-](sql-database-long-term-retention.md) of [Azure Automation](../automation/automation-intro.md) bij de archivering van SQL-databases met PowerShell regelmatig periodiek volgens een planning van uw keuze. Voor een voorbeeld van een script, kunt u downloaden de [voorbeeldscript vanuit GitHub](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-automation-automated-export).
>


## <a name="resources"></a>Resources
[Azure-abonnement en Servicelimieten, quota's en beperkingen](../azure-subscription-service-limits.md)

[Azure SQL Database servicecategorieën en prestatieniveaus](sql-database-service-tiers.md)

[Foutberichten voor client-programma's van SQL-database](sql-database-develop-error-messages.md)
