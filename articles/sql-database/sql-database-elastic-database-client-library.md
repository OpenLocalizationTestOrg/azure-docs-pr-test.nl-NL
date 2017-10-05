---
title: Schaalbare cloud databases bouwen | Microsoft Docs
description: Schaalbare apps van .NET-database met de clientbibliotheek voor elastische database maken
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 1f11c52d-13c1-4994-b9b1-5b1ae2f9255f
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: ddove
ms.openlocfilehash: 0128b333f04847ab646dcb0759fcef5f7e86ffd9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="building-scalable-cloud-databases"></a>Schaalbare clouddatabases bouwen
Databases uitbreiden kan gemakkelijk worden gedaan met behulp van schaalbare hulpprogramma's en functies voor Azure SQL Database. U kunt in het bijzonder de **clientbibliotheek voor elastische Database** maken en beheren van uitgebreide databases. Deze functie kunt u eenvoudig shard toepassingen ontwikkelen met honderden, of zelfs duizenden — van Azure SQL-databases. [Elastische taken](sql-database-elastic-jobs-powershell.md) kan vervolgens worden gebruikt voor het beheer te vereenvoudigen voor deze databases.

Als u wilt installeren in de bibliotheek, gaat u naar [Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/). 

## <a name="documentation"></a>Documentatie
1. [Aan de slag met tools voor Elastic Database](sql-database-elastic-scale-get-started.md)
2. [Functies voor elastische Database](sql-database-elastic-scale-introduction.md)
3. [Shard-toewijzingsbeheer](sql-database-elastic-scale-shard-map-management.md)
4. [Bestaande databases migreren voor uitschaling](sql-database-elastic-convert-to-use-elastic-tools.md)
5. [Gegevensafhankelijke routering](sql-database-elastic-scale-data-dependent-routing.md)
6. [Meerdere shard-query 's](sql-database-elastic-scale-multishard-querying.md)
7. [Toevoegen van een shard met hulpprogramma's van elastische Database](sql-database-elastic-scale-add-a-shard.md)
8. [Multitenant-toepassingen met elastische database-hulpprogramma's en beveiliging](sql-database-elastic-tools-multi-tenant-row-level-security.md)
9. [Upgrade van client-bibliotheek-apps](sql-database-elastic-scale-upgrade-client-library.md) 
10. [Overzicht van de elastische query 's](sql-database-elastic-query-overview.md)
11. [Woordenlijst voor hulpprogramma's voor Elastic Database](sql-database-elastic-scale-glossary.md)
12. [Elastische Database-clientbibliotheek met Entity Framework](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md)
13. [Clientbibliotheek voor elastische database met Dapper](sql-database-elastic-scale-working-with-dapper.md)
14. [Gesplitste merge tool](sql-database-elastic-scale-overview-split-and-merge.md)
15. [Prestatiemeteritems voor shard-toewijzingsbeheer](sql-database-elastic-database-client-library.md) 
16. [Veelgestelde vragen over de hulpprogramma's voor elastische database](sql-database-elastic-scale-faq.md)

## <a name="client-capabilities"></a>Client-mogelijkheden
Uitbreiden van toepassingen via *sharding* geeft uitdagingen voor zowel de ontwikkelaar als de beheerder. De clientbibliotheek vereenvoudigt de beheertaken dankzij de hulpprogramma's waarmee u zowel ontwikkelaars en beheerders uitgebreide databases beheren. In een typisch voorbeeld zijn er veel databases, bekend als 'shards', om te beheren. Klanten in dezelfde database zich bevindt en er is één database per klant (een schema voor één tenant). De clientbibliotheek omvat de volgende functies:

- **Beheer van shard-toewijzing**: een bijzondere database met de naam van de 'shard kaart manager' is gemaakt. Beheer van shard-toewijzing is de mogelijkheid voor een toepassing voor het beheren van metagegevens over de shards. Ontwikkelaars kunnen deze functionaliteit gebruiken databases registreren als shards, beschrijven toewijzingen van afzonderlijke sharding-sleutels of sleutelbereiken voor deze databases en onderhouden van deze metagegevens als het getal en samenstelling van databases die zijn ontwikkeld naar aanleiding van wijzigingen van de capaciteit. U moet besteden veel tijd de management code te schrijven bij het implementeren van sharding zonder de clientbibliotheek elastische database. Zie voor meer informatie [Shard kaart management](sql-database-elastic-scale-shard-map-management.md).

- **Gegevensafhankelijke routering**: Stel dat een aanvraag afkomstig is in de toepassing. Op basis van de sharding-sleutelwaarde van de aanvraag, moet de toepassing om te bepalen van de juiste database op basis van de waarde van de sleutel. Het opent vervolgens een verbinding met de database om de aanvraag te verwerken. Gegevensafhankelijke routering biedt de mogelijkheid voor het openen van verbindingen met een enkele eenvoudige aanroep in de shard-toewijzing van de toepassing. Gegevensafhankelijke routering is een ander aspect van infrastructuur-code die nu wordt gedekt door functies van de clientbibliotheek voor elastische database. Zie voor meer informatie [gegevensafhankelijke routering](sql-database-elastic-scale-data-dependent-routing.md).
- **Meerdere shard-query's (MSQ)**: uitvoeren van query's met meerdere shard werkt bij een aanvraag verschillende (of alle) shards omvat. De dezelfde T-SQL-code een meerdere shard-query uitgevoerd op alle shards of een set met shards. De resultaten van de deelnemende shards worden samengevoegd in een algemene resultatenset met UNION ALL semantiek. De functionaliteit, zoals beschikbaar gesteld via de clientbibliotheek handelt vele taken, waaronder: Verbindingsbeheer, threadbeheer, verwerking van de fout en tussenliggende resultaten verwerken. MSQ kunt honderden shards opvragen. Zie voor meer informatie [opvragen van meerdere shard](sql-database-elastic-scale-multishard-querying.md).

In het algemeen kunnen klanten die gebruikmaken van hulpprogramma's voor elastische database verwachten volledige functionaliteit van T-SQL ophalen bij het indienen van shard-local-bewerkingen in plaats van cross-shard-bewerkingen die hun eigen heeft.

## <a name="next-steps"></a>Volgende stappen
Probeer de [voorbeeldapp](sql-database-elastic-scale-get-started.md) die laat zien van de clientfuncties. 

Als u wilt installeren in de bibliotheek, gaat u naar [clientbibliotheek voor elastische Database](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).

Zie voor instructies over het hulpprogramma voor het splitsen samenvoegen, de [gesplitste merge tool overzicht](sql-database-elastic-scale-overview-split-and-merge.md).

[Clientbibliotheek voor elastische database is nu open brongegevens!](https://azure.microsoft.com/blog/elastic-database-client-library-is-now-open-sourced/)

Gebruik [elastische query's](sql-database-elastic-query-overview.md).

De bibliotheek is beschikbaar als open-sourcesoftware op [GitHub](https://github.com/Azure/elastic-db-tools). 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->
[1]:./media/sql-database-elastic-database-client-library/glossary.png

