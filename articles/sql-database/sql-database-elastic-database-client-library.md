---
title: aaaBuilding schaalbare cloud databases | Microsoft Docs
description: Schaalbare apps van .NET-database met Hallo-clientbibliotheek voor elastische database maken
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
ms.openlocfilehash: ca34eff2078c0700dee1bc587f264bbfca979eb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="building-scalable-cloud-databases"></a>Schaalbare clouddatabases bouwen
Databases uitbreiden kan gemakkelijk worden gedaan met behulp van schaalbare hulpprogramma's en functies voor Azure SQL Database. In het bijzonder, kunt u Hallo **clientbibliotheek voor elastische Database** toocreate en uitgebreide databases beheren. Deze functie kunt u eenvoudig shard toepassingen ontwikkelen met honderden, of zelfs duizenden — van Azure SQL-databases. [Elastische taken](sql-database-elastic-jobs-powershell.md) gebruikte toohelp eenvoudig beheer van deze databases vervolgens kunnen worden.

tooinstall hello bibliotheek, gaat u te[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/). 

## <a name="documentation"></a>Documentatie
1. [Aan de slag met tools voor Elastic Database](sql-database-elastic-scale-get-started.md)
2. [Functies voor elastische Database](sql-database-elastic-scale-introduction.md)
3. [Shard-toewijzingsbeheer](sql-database-elastic-scale-shard-map-management.md)
4. [Migreren van bestaande databases tooscale-out](sql-database-elastic-convert-to-use-elastic-tools.md)
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
Uitbreiden van toepassingen via *sharding* uitdagingen voor zowel Hallo ontwikkelaar als Hallo beheerder geeft. Hallo-clientbibliotheek vereenvoudigt u beheertaken Hallo dankzij de hulpprogramma's waarmee u zowel ontwikkelaars en beheerders uitgebreide databases beheren. In een typisch voorbeeld zijn er veel databases, bekend als 'shards,' toomanage. Klanten zich bevindt dezelfde database Hallo en er is één database per klant (een schema voor één tenant). Hallo-clientbibliotheek omvat de volgende functies:

- **Beheer van shard-toewijzing**: een speciale aangeroepen Hallo 'shard-toewijzing manager'-database wordt gemaakt. Beheer van shard-toewijzing is Hallo mogelijkheid voor een toepassing toomanage metagegevens over de shards. Ontwikkelaars kunnen deze functionaliteit tooregister databases gebruiken als shards, beschrijven toewijzingen van afzonderlijke sharding-sleutels of sleutelbereiken toothose databases en onderhouden van deze metagegevens als Hallo getal en samenstelling van databases zich verder ontwikkelen tooreflect capaciteit wijzigingen. Zonder clientbibliotheek Hallo elastische database moet u toospend veel tijd Hallo management code te schrijven bij het implementeren van sharding. Zie voor meer informatie [Shard kaart management](sql-database-elastic-scale-shard-map-management.md).

- **Gegevensafhankelijke routering**: Stel dat een aanvraag afkomstig is in de toepassing hello. Op basis van Hallo sharding-sleutelwaarde van Hallo aanvraag, moet Hallo toepassing toodetermine Hallo juiste database op basis van Hallo sleutelwaarde. Vervolgens wordt een toohello database tooprocess Hallo verbindingsaanvraag geopend. Gegevensafhankelijke routering biedt Hallo mogelijkheid tooopen verbindingen met een enkele eenvoudige aanroep in Hallo shard-toewijzing van de toepassing hello. Gegevensafhankelijke routering is een ander aspect van infrastructuur-code die nu wordt gedekt door functionaliteit in Hallo-clientbibliotheek voor elastische database. Zie voor meer informatie [gegevensafhankelijke routering](sql-database-elastic-scale-data-dependent-routing.md).
- **Meerdere shard-query's (MSQ)**: uitvoeren van query's met meerdere shard werkt bij een aanvraag verschillende (of alle) shards omvat. Een query meerdere shard Hallo voert dezelfde T-SQL-code op alle shards of een set met shards. Hallo-resultaten van deelnemende shards Hallo worden samengevoegd in een algemene resultatenset met UNION ALL semantiek. Hallo functionaliteit, zoals beschikbaar via het Hallo-clientbibliotheek handelt vele taken, waaronder: Verbindingsbeheer, threadbeheer, verwerking van de fout en tussenliggende resultaten verwerken. MSQ kunt opvragen van toohundreds met shards. Zie voor meer informatie [opvragen van meerdere shard](sql-database-elastic-scale-multishard-querying.md).

In het algemeen kunnen klanten die gebruikmaken van hulpprogramma's voor elastische database tooget volledige T-SQL-functionaliteit verwachten bij het indienen van shard-local-bewerkingen in tegenstelling tot toocross-shard-bewerkingen die hun eigen semantiek hebben.

## <a name="next-steps"></a>Volgende stappen
Probeer Hallo [voorbeeldapp](sql-database-elastic-scale-get-started.md) die Hallo clientfuncties laat zien. 

tooinstall hello bibliotheek, gaat u te[clientbibliotheek voor elastische Database](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).

Zie voor instructies over het gebruik van Hallo gesplitste merge tool Hallo [gesplitste merge tool overzicht](sql-database-elastic-scale-overview-split-and-merge.md).

[Clientbibliotheek voor elastische database is nu open brongegevens!](https://azure.microsoft.com/blog/elastic-database-client-library-is-now-open-sourced/)

Gebruik [elastische query's](sql-database-elastic-query-overview.md).

Hallo bibliotheek is beschikbaar als open-sourcesoftware op [GitHub](https://github.com/Azure/elastic-db-tools). 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->
[1]:./media/sql-database-elastic-database-client-library/glossary.png

