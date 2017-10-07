---
title: aaaAzure limieten voor SQL Database | Microsoft Docs
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
ms.openlocfilehash: 3e7be4fdc74e802d37274690531caaf138bcedb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-resource-limits"></a>Limieten voor Azure SQL Database
## <a name="overview"></a>Overzicht
Azure SQL Database beheert Hallo resources beschikbaar tooa database met behulp van twee verschillende mechanismen: **Resources Governance** en **afdwinging van limieten**. Dit onderwerp wordt uitgelegd dat deze twee hoofdgebieden voor bronbeheer.

## <a name="resource-governance"></a>Resource governance
Een van de Hallo ontwerpdoelstellingen van Servicelagen Basic, Standard, Premium en Premium RS Hallo is voor Azure SQL Database toobehave alsof Hallo-database wordt uitgevoerd op een eigen machine, geïsoleerd van andere databases. Resource governance emuleert dit gedrag. Hallo geaggregeerd Resourcegebruik bereikt Hallo maximaal beschikbare CPU, geheugen, i/o-logboek en gegevens i/o-resources toegewezen toohello database resource governance wachtrijen query's in uitvoering als toohello in de wachtrij query's als ze vrijmaken bronnen toewijzen.

Als op een toegewezen machine, gebruik van alle beschikbare resources resulteert in een langer uitvoering van query's dat momenteel wordt uitgevoerd, hetgeen kan leiden tot opdracht time-outs op Hallo-client. Toepassingen met agressieve Pogingslogica en toepassingen die voor het uitvoeren van query's op Hallo-database met een hoge frequentie kunnen foutberichten ondervindt bij het tooexecute nieuwe query's als Hallo-limiet van gelijktijdige aanvragen is bereikt.

### <a name="recommendations"></a>Aanbevelingen:
Hallo brongebruik en Hallo gemiddelde reactietijden van query's bewaken wanneer bijna Hallo maximaal gebruik van een database. Wanneer zich voordoen tijdens een hogere query latenties in het algemeen hebt u drie opties:

1. Verminder het aantal inkomende aanvragen toohello database tooprevent time-outs en Hallo stapel up aanvragen Hallo.
2. Een hogere prestaties niveau toohello database toewijzen.
3. Query's tooreduce Hallo Resourcegebruik van elke query optimaliseren. Zie voor meer informatie Hallo Query afstemmen/Hinting-sectie in hello Azure SQL Database-prestaties richtlijnen artikel.

## <a name="enforcement-of-limits"></a>Afdwinging van grenzen
Bronnen dan CPU, geheugen, i/o-logboek en i/o-gegevens worden afgedwongen door de nieuwe aanvragen geweigerd wanneer limieten zijn bereikt. Wanneer een database bereikt maximumgrootte Hallo geconfigureerd, voegt en updates die verhogen gegevensgrootte mislukken terwijl selecteert en verwijderingen blijven toowork. Clients ontvangen een [foutbericht](sql-database-develop-error-messages.md) afhankelijk van het Hallo-limiet die is bereikt.

Hallo aantal verbindingen tooa SQL-database en Hallo aantal gelijktijdige aanvragen die kunnen worden verwerkt, zijn bijvoorbeeld beperkt. SQL-Database kunt het aantal verbindingen toohello database toobe Hallo groter dan Hallo aantal gelijktijdige aanvragen toosupport Groepsgewijze verbinding nodig. Tijdens het Hallo aantal verbindingen die beschikbaar zijn kan eenvoudig worden beheerd door de toepassing hello, wordt het aantal parallelle aanvragen Hallo vaak is keren moeilijker tooestimate en toocontrol. Met name tijdens piekbelastingen wanneer Hallo toepassing ofwel te veel aanvragen verzendt of Hallo database de limieten bereikt en opstapelen werkthreads vanwege toolonger actieve query's is gestart, fouten kunnen worden aangetroffen.

## <a name="service-tiers-and-performance-levels"></a>Servicelagen en prestatieniveaus
Er zijn Servicelagen en prestatieniveaus van één database- en elastische pools.

### <a name="single-databases"></a>Individuele databases
Voor een individuele database worden Hallo grenzen van een database gedefinieerd door Hallo database prijscategorie en prestatieniveau serviceniveau. Hallo volgende tabel beschrijft de kenmerken Hallo van Basic, Standard, Premium en RS Premium-databases op verschillende prestatieniveaus.

[!INCLUDE [SQL DB service tiers table](../../includes/sql-database-service-tiers-table.md)]

> [!IMPORTANT]
> Klanten die gebruikmaken van P11 en P15 prestatieniveaus kunnen van too4 TB van opgenomen opslag zonder extra kosten gebruiken. Deze optie 4 TB is momenteel beschikbaar is in de volgende regio's Hallo: ons East2, VS-West, Gov ons Virginia, West-Europa, Duitsland centraal, Zuid-Oost-Azië, Japan-Oost, Australië-Oost, Canada centraal en Canada-Oost.
>

### <a name="elastic-pools"></a>Pools voor Elastic Database
[Elastische pools](sql-database-elastic-pool.md) resources delen met andere databases in Hallo-groep. Hallo volgende tabel beschrijft de kenmerken Hallo van Basic, Standard, Premium en RS Premium elastische pools.

[!INCLUDE [SQL DB service tiers table for elastic databases](../../includes/sql-database-service-tiers-table-elastic-pools.md)]

Zie voor een uitgebreide definitie van elke bron die is opgenomen in de vorige tabellen Hallo Hallo beschrijvingen in [Service tier mogelijkheden en beperkingen van](sql-database-performance-guidance.md#service-tier-capabilities-and-limits). Zie voor een overzicht van Servicelagen [Azure SQL Database servicecategorieën en prestatieniveaus](sql-database-service-tiers.md).

## <a name="other-sql-database-limits"></a>De limieten van andere SQL-Database
| Onderwerp | Limiet | Beschrijving |
| --- | --- | --- |
| Databases met automatische export per abonnement |10 |Automatische export kunt u een aangepaste planning toocreate voor de back-up van uw SQL-databases. Voorbeeld van deze functie Hallo eindigt op 1 maart 2017.  |
| Databases per server |Up too5000 |Up too5000 zijn per server databases toegestaan. |
| Dtu's per server |45000 |45000 dtu's zijn toegestaan per server voor het inrichten van zelfstandige databases en elastische pools. Hallo totaal aantal zelfstandige-databases en pools toegestaan per server wordt beperkt alleen door het aantal dtu's server Hallo.  

> [!IMPORTANT]
> Azure SQL Database geautomatiseerde exporteren bevindt zich nu in preview en wordt buiten gebruik worden gesteld op 1 maart 2017. Vanaf 1 December 2016, langer u niet kunnen tooconfigure automatische export op elke SQL-database. Uw bestaande automatische exporttaken blijven toowork tot 1 maart 2017. Na 1e December 2016, kunt u [lange bewaartermijn van de back-](sql-database-long-term-retention.md) of [Azure Automation](../automation/automation-intro.md) tooarchive SQL-databases regelmatig met behulp van PowerShell regelmatig volgens planning tooa van uw keuze. Voor een voorbeeld van een script, kunt u downloaden Hallo [voorbeeldscript vanuit GitHub](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-automation-automated-export).
>


## <a name="resources"></a>Resources
[Azure-abonnement en Servicelimieten, quota's en beperkingen](../azure-subscription-service-limits.md)

[Azure SQL Database servicecategorieën en prestatieniveaus](sql-database-service-tiers.md)

[Foutberichten voor client-programma's van SQL-database](sql-database-develop-error-messages.md)
