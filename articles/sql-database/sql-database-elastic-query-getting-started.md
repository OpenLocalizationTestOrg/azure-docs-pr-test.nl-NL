---
title: aaaReport voor cloud uitgebreide databases (horizontale partitionering) | Microsoft Docs
description: hoe toouse cross database databasequery 's
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: c81ef5e3-41e9-4fd2-8631-868f2e168147
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: mlandzic
ms.openlocfilehash: e34f398f8d408cffd91a70fc2cfbda73daec3550
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="report-across-scaled-out-cloud-databases-preview"></a>Rapport over cloud uitgebreide databases (preview)
U kunt rapporten maken uit meerdere Azure SQL-databases vanuit een enkele verbinding punt met een [elastische query](sql-database-elastic-query-overview.md). Hallo-databases worden horizontaal gepartitioneerd (ook wel bekend als 'shard').

Als u een bestaande database hebt, raadpleegt u [migreren bestaande databases tooscaled-out-databases](sql-database-elastic-convert-to-use-elastic-tools.md).

toounderstand hello SQL-objecten die nodig zijn tooquery, Zie [Query over horizontaal gepartitioneerde databases](sql-database-elastic-query-horizontal-partitioning.md).

## <a name="prerequisites"></a>Vereisten
Downloaden en uitvoeren van Hallo [aan de slag met elastische Database extra voorbeeld](sql-database-elastic-scale-get-started.md).

## <a name="create-a-shard-map-manager-using-hello-sample-app"></a>Een shard-toewijzing manager met Hallo voorbeeld-app maken
Hier maakt u een shard-toewijzing manager samen met enkele shards, gevolgd door het invoegen van gegevens in Hallo shards. Als u per ongeluk tooalready shards setup met gedeelde gegevens zich bevinden, kunt u Hallo stappen overslaan en de volgende sectie toohello verplaatsen.

1. Bouwen en uitvoeren van Hallo **aan de slag met hulpprogramma's voor elastische Database** voorbeeldtoepassing. Hallo stappen tot stap 7 in de sectie Hallo [Hallo voorbeeld-app downloaden en uitvoeren](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app). Aan het einde van de Hallo van stap 7 ziet u Hallo na de opdrachtprompt:

    ![opdrachtprompt][1]
2. In het opdrachtvenster hello, typ '1' en druk op **Enter**. Dit maakt Hallo shard-toewijzing manager en voegt u twee shards toohello-server. Vervolgens typt u "3" en druk op **Enter**; Hallo actie vier keer herhalen. Dit invoegen voorbeeld gegevensrijen in uw shards.
3. Hallo [Azure-portal](https://portal.azure.com) moet drie nieuwe databases worden weergegeven in de server:

   ![Visual Studio-bevestiging][2]

   Cross-databasequery's worden op dit moment ondersteund via Hallo elastische Database clientbibliotheken. Gebruik bijvoorbeeld optie 4 in Hallo-opdrachtvenster. Hallo-resultaten van een query meerdere shard zijn altijd een **UNION ALL** van Hallo resultaten van alle shards.

   In de volgende sectie hello maken we een voorbeeld database eindpunt die ondersteuning biedt voor uitgebreide query Hallo gegevens over shards.

## <a name="create-an-elastic-query-database"></a>Een voor elastische querydatabase maken
1. Open Hallo [Azure-portal](https://portal.azure.com) en zich aanmelden.
2. Maak een nieuwe Azure SQL-database in Hallo dezelfde server als de shard-instellingen. Naam Hallo database 'ElasticDBQuery'.

    ![Azure-portal en de prijscategorie][3]

    > [!NOTE]
    > u kunt een bestaande database gebruiken. Als u doet dit, niet moet een Hallo shards dat u tooexecute wilt uw query's op. Deze database wordt gebruikt voor het maken van Hallo van metagegevensobjecten voor een elastische database-query.
    >

## <a name="create-database-objects"></a>Database-objecten maken
### <a name="database-scoped-master-key-and-credentials"></a>Database-scoped hoofdsleutel en referenties
Dit zijn de gebruikte tooconnect toohello shard kaart manager en Hallo shards:

1. Open SQL Server Management Studio of SQL Server Data Tools in Visual Studio.
2. Verbinding maken met database tooElasticDBQuery en Hallo volgende T-SQL-opdrachten uitvoeren:

        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred
        WITH IDENTITY = '<username>',
        SECRET = '<password>';

    'gebruikersnaam' en 'password' moet worden Hallo dezelfde als de aanmeldingsgegevens die zijn gebruikt in stap 6 van [Hallo voorbeeld-app downloaden en uitvoeren](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app) in [aan de slag met hulpprogramma's voor elastische database](sql-database-elastic-scale-get-started.md).

### <a name="external-data-sources"></a>Externe gegevensbronnen
een externe gegevensbron toocreate Hallo volgende opdracht uit op Hallo ElasticDBQuery database uitvoeren:

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH
      (TYPE = SHARD_MAP_MANAGER,
      LOCATION = '<server_name>.database.windows.net',
      DATABASE_NAME = 'ElasticScaleStarterKit_ShardMapManagerDb',
      CREDENTIAL = ElasticDBQueryCred,
       SHARD_MAP_NAME = 'CustomerIDShardMap'
    ) ;

 'CustomerIDShardMap' hello naam is van Hallo shard-kaart, als u hebt gemaakt Hallo shard-toewijzing en shard-toewijzing manager tools-voorbeeld gebruikt Hallo elastische database. Als u uw aangepaste instellingen voor dit voorbeeld gebruikt, klikt u vervolgens moet het echter Hallo shard-toewijzingsnaam die u hebt gekozen in uw toepassing.

### <a name="external-tables"></a>Externe tabellen
Een externe tabel die overeenkomt met Hallo klantentabel op Hallo shards door het uitvoeren van de volgende opdracht uit op ElasticDBQuery database Hallo maken:

    CREATE EXTERNAL TABLE [dbo].[Customers]
    ( [CustomerId] [int] NOT NULL,
      [Name] [nvarchar](256) NOT NULL,
      [RegionId] [int] NOT NULL)
    WITH
    ( DATA_SOURCE = MyElasticDBQueryDataSrc,
      DISTRIBUTION = SHARDED([CustomerId])
    ) ;

## <a name="execute-a-sample-elastic-database-t-sql-query"></a>Een voorbeeld elastische database T-SQL-query uitvoeren
U kunt nu volledige T-SQL gebruiken via uw externe tabellen, nadat u uw externe gegevensbron en uw externe tabellen hebt gedefinieerd.

Voer deze query uit op Hallo ElasticDBQuery database:

    select count(CustomerId) from [dbo].[Customers]

U zult die query Hallo cumuleert de resultaten van alle Hallo shards en geeft Hallo volgende uitvoer:

![Uitvoerdetails][4]

## <a name="import-elastic-database-query-results-tooexcel"></a>Elastische database query resultaten tooExcel importeren
 U kunt Hallo resultaten uit van een query tooan Excel-bestand importeren.

1. Start Excel 2013.
2. Navigeer toohello **gegevens** lint.
3. Klik op **van andere bronnen** en klik op **van SQL Server**.

   ![Excel importeren uit andere bronnen][5]
4. In Hallo **Wizard Gegevensverbinding** Typ Hallo server servernaam en aanmeldingsreferenties. Klik op **Volgende**.
5. In het dialoogvenster Hallo **Selecteer Hallo-database met Hallo gegevens die u wilt**, selecteer Hallo **ElasticDBQuery** database.
6. Selecteer Hallo **klanten** tabel in de lijstweergave Hallo en klikt u op **volgende**. Klik vervolgens op **voltooien**.
7. In Hallo **importgegevens** formulier onder **Selecteer hoe u tooview deze gegevens in uw werkmap**, selecteer **tabel** en klik op **OK**.

Alle rijen uit Hallo **klanten** tabel, opgeslagen in verschillende shards vullen Hallo Excel-werkblad.

Nu kunt u krachtige gegevensfuncties visualisatie van Excel. U kunt Hallo verbindingsreeks gebruiken met de naam van uw server, databasenaam en referenties tooconnect uw BI en gegevens integratie extra toohello elastische query uitvoeren op database. Zorg ervoor dat SQL Server wordt ondersteund als een gegevensbron voor het hulpprogramma. U kunt toohello elastische query uitvoeren op database en de externe tabellen net als elke andere SQL Server-database en SQL Server-tabellen die u wilt verbinding maken toowith uw hulpprogramma verwijzen.

### <a name="cost"></a>Kosten
Er zijn geen extra kosten voor het gebruik van Hallo elastische databasequery functie.

Zie voor informatie over prijzen [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/).

## <a name="next-steps"></a>Volgende stappen

* Zie voor een overzicht van elastische query [elastische query overzicht](sql-database-elastic-query-overview.md).
* Zie voor een verticale partitie zelfstudie [aan de slag met cross-databasequery (verticale partities)](sql-database-elastic-query-getting-started-vertical.md).
* Zie voor de syntaxis en voorbeelden query's voor verticaal gepartitioneerde gegevens [gegevens opvragen verticaal gepartitioneerd)](sql-database-elastic-query-vertical-partitioning.md)
* Zie voor de syntaxis en voorbeelden query's voor horizontaal gepartitioneerde gegevens [gegevens opvragen horizontaal gepartitioneerd)](sql-database-elastic-query-horizontal-partitioning.md)
* Zie [sp\_uitvoeren \_externe](https://msdn.microsoft.com/library/mt703714) voor een opgeslagen procedure die een Transact-SQL-instructie op een enkele externe Azure SQL Database of een set van databases die fungeren als shards in een horizontale partitieschema wordt uitgevoerd.


<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
