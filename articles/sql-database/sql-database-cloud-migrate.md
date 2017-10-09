---
title: aaaSQL Server-database migratie tooAzure SQL-Database | Microsoft Docs
description: Meer informatie over hoe SQL Server-database migratie tooAzure SQL-Database in de cloud Hallo. Database migratie extra tootest compatibiliteit met eerdere toodatabase migratie gebruiken.
keywords: databasemigratie, sql server-databasemigratie, hulpprogramma's voor databasemigratie, database migreren, sql-database migreren
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 9cf09000-87fc-4589-8543-a89175151bc2
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sqldb-migrate
ms.date: 02/08/2017
ms.author: carlrab
ms.openlocfilehash: 3a5e879404dd2da1dd5254a6134e3ee1517648db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sql-server-database-migration-toosql-database-in-hello-cloud"></a>SQL Server-database migratie tooSQL Database in de cloud Hallo
In dit artikel leert u Hallo twee methoden voor het migreren van een SQL Server 2005 of hoger database tooAzure SQL-Database. Hallo eerste methode is eenvoudiger, maar sommige vereist mogelijk aanzienlijke downtime tijdens de migratie Hallo. de tweede methode Hallo is complexere, maar elimineert aanzienlijk uitvaltijd tijdens de migratie Hallo.

In beide gevallen moet u tooensure die brondatabase Hallo is compatibel met Azure SQL Database met Hallo [gegevens migratie-assistent (DMA)](https://www.microsoft.com/download/details.aspx?id=53595). SQL Database V12 nadert [functie pariteit](sql-database-features.md) met SQL Server dan problemen gerelateerde tooserver-niveau en tussen meerdere databases bewerkingen. Databases en toepassingen die afhankelijk van zijn [gedeeltelijk ondersteund of niet-ondersteunde functies](sql-database-transact-sql-information.md) moeten sommige [herstructureren toofix deze compatibiliteitsproblemen](sql-database-cloud-migrate.md#resolving-database-migration-compatibility-issues) voordat Hallo SQL Server-database kan worden gemigreerd.

> [!NOTE]
> toomigrate een SQL Server-database, met inbegrip van Microsoft Access, Sybase, MySQL Oracle en DB2 tooAzure SQL-Database, Zie [SQL Server Migration Assistant](https://blogs.msdn.microsoft.com/datamigration/2016/12/22/released-sql-server-migration-assistant-ssma-v7-2/).
> 

## <a name="method-1-migration-with-downtime-during-hello-migration"></a>Methode 1: Migratie uitvaltijd tijdens de migratie Hallo

 Gebruik deze methode als u zich enige uitvaltijd kunt permitteren of als u met het oog op een latere migratie een testmigratie van een productiedatabase uitvoert. Zie voor een zelfstudie [migreren van een SQL Server-database](sql-database-migrate-your-sql-server-database.md).

Hallo bevat volgende lijst algemene werkstroom voor de migratie van een SQL Server-database met deze methode Hallo.

  ![Diagram van VSSSDT-migratie](./media/sql-database-cloud-migrate/azure-sql-migration-sql-db.png)

1. Hallo-database voor compatibiliteit met behulp van de meest recente versie van Hallo beoordelen [gegevens migratie-assistent (DMA)](https://www.microsoft.com/download/details.aspx?id=53595).
2. Bereid alle benodigde fixes voor als Transact-SQL-scripts.
3. Maak een transactioneel consistent kopie van de brondatabase hello wordt gemigreerd - en zorg ervoor dat er geen verdere wijzigingen worden aangebracht toohello brondatabase (of kunt u deze wijzigingen handmatig toepassen nadat Hallo migratie is voltooid). Er zijn veel manieren tooquiesce een database, van het uitschakelen van de client verbinding toocreating een [databasemomentopname](https://msdn.microsoft.com/library/ms175876.aspx).
4. Implementeer Hallo Transact-SQL-scripts tooapply Hallo oplossingen toohello database kopiëren.
5. [Exporteren](sql-database-export.md) Hallo tooa voor database-exemplaar. Bacpac-bestand op een lokale schijf.
6. [Importeren](sql-database-import.md) Hallo. Hulpprogramma's, Bacpac-bestand als een nieuwe Azure SQL database met behulp van een enkele BACPAC importeren met SQLPackage.exe wordt Hallo aanbevolen hulpprogramma voor de beste prestaties.

### <a name="optimizing-data-transfer-performance-during-migration"></a>De prestaties van de gegevensoverdracht tijdens de migratie optimaliseren 

Hallo volgende lijst bevat aanbevelingen voor de beste prestaties tijdens het importeren van Hallo.

* Kies Hallo hoogste serviceniveau en prestaties servicetier dat uw budget toomaximize Hallo overdracht prestaties toestaat. U kunt omlaag schalen nadat de migratie Hallo toosave geld is voltooid. 
* Minimaliseren Hallo afstand tussen uw. Bacpac-bestand en Hallo bestemming Datacenter.
* Schakel automatische statistieken tijdens de migratie uit.
* Partitioneer tabellen en indexen.
* Verwijder geïndexeerde weergaven en maak ze opnieuw nadat de migratie is voltooid.
* Zelden querygegevens historische tooanother database verwijderen en deze historische gegevens tooa afzonderlijke Azure SQL database worden gemigreerd. U kunt dan [elastische query's](sql-database-elastic-query-overview.md) uitvoeren om eventueel benodigde historische gegevens op te vragen.

### <a name="optimize-performance-after-hello-migration-completes"></a>Optimaliseren nadat Hallo migratie is voltooid

[Statistieken bijwerken](https://msdn.microsoft.com/library/ms187348.aspx) met volledige scan na Hallo migratie is voltooid.

## <a name="method-2-use-transactional-replication"></a>Methode 2: Transactionele replicatie gebruiken

Wanneer u geen tooremove uw SQL Server-database van de productie enkele tijdens het Hallo-migratie is, kunt u transactionele replicatie van SQL Server gebruiken als uw migratieoplossing. toouse deze methode Hallo brondatabase moet voldoen aan Hallo [vereisten voor transactionele replicatie](https://msdn.microsoft.com/library/mt589530.aspx) en niet compatibel met Azure SQL Database. Zie voor meer informatie over SQL-replicatie met AlwaysOn [replicatie configureren voor AlwaysOn-beschikbaarheidsgroepen (SQL Server)](/sql/database-engine/availability-groups/windows/configure-replication-for-always-on-availability-groups-sql-server).

toouse deze oplossing u uw Azure SQL Database configureren als een abonnee toohello SQL Server-exemplaar dat u wenst dat toomigrate. Hallo distributor voor transactionele replicatie worden gegevens gesynchroniseerd van Hallo database toobe gesynchroniseerd (Hallo uitgever) bij doorgaan met de nieuwe transacties plaatsvinden. 

Transactionele replicatie weergegeven alle wijzigingen tooyour gegevens of schema in uw Azure SQL Database. Wanneer u eenmaal Hallo synchronisatie voltooid is en u klaar toomigrate bent, Hallo verbindingsreeks van uw toepassingen toopoint wijzigen ze tooyour Azure SQL Database. Nadat transactionele replicatie leeghalen wijzigingen links op de brondatabase en alle toepassingen die uw serviceverbindingspunt tooAzure DB, kunt u transactionele replicatie verwijderen. Uw Azure SQL Database is nu uw productiesysteem.

 ![SeedCloudTR-diagram](./media/sql-database-cloud-migrate/SeedCloudTR.png)

> [!TIP]
> U kunt ook transactionele replicatie toomigrate een subset van de brondatabase. Hallo-publicatie replicatie van tooAzure SQL-Database kan worden beperkt tooa subset van Hallo-tabellen in Hallo-database wordt gerepliceerd. U kunt voor elke tabel wordt gerepliceerd, Hallo gegevens tooa subset van Hallo rijen en/of een subset kolommen Hallo beperken.
>

### <a name="migration-toosql-database-using-transaction-replication-workflow"></a>Migratie tooSQL Database met de werkstroom van de replicatie van de transactie

> [!IMPORTANT]
> Gebruik Hallo meest recente versie van SQL Server Management Studio tooremain gesynchroniseerd met updates tooMicrosoft Azure en SQL-Database. In oudere versies van SQL Server Management Studio kunt u SQL Database niet instellen als abonnee. [SQL Server Management Studio bijwerken](https://msdn.microsoft.com/library/mt238290.aspx).
> 

1. Distributie instellen
   -  [SQL Server Management Studio (SSMS) gebruiken](https://msdn.microsoft.com/library/ms151192.aspx#Anchor_1)
   -  [Transact-SQL gebruiken](https://msdn.microsoft.com/library/ms151192.aspx#Anchor_2)
2. Publicatie maken
   -  [SQL Server Management Studio (SSMS) gebruiken](https://msdn.microsoft.com/library/ms151160.aspx#Anchor_1)
   -  [Transact-SQL gebruiken](https://msdn.microsoft.com/library/ms151160.aspx#Anchor_2)
3. Abonnement maken
   -  [SQL Server Management Studio (SSMS) gebruiken](https://msdn.microsoft.com/library/ms152566.aspx#Anchor_0)
   -  [Transact-SQL gebruiken](https://msdn.microsoft.com/library/ms152566.aspx#Anchor_1)

### <a name="some-tips-and-differences-for-migrating-toosql-database"></a>Enkele tips en verschillen voor het migreren van tooSQL Database

1. Gebruik een lokale distributeur. 
   - Dit zorgt ervoor dat invloed op de prestaties op Hallo-server. 
   - Als prestatieresultaat Hallo onacceptabel is, kunt u een andere server maar complexiteit in beheer- en wordt toegevoegd.
2. Bij het selecteren van een map met momentopnamen, zorg ervoor dat Hallo map die u selecteert is groot genoeg toohold een BCP van elke tabel wilt tooreplicate. 
3. Momentopname maken van vergrendelingen Hallo gekoppelde tabellen totdat deze is voltooid, zodat uw momentopname op de juiste wijze plannen. 
4. In Azure SQL Database worden alleen push-abonnementen ondersteund. U kunt alleen abonnees uit de brondatabase Hallo toevoegen.

## <a name="resolving-database-migration-compatibility-issues"></a>Compatibiliteitsproblemen met databasemigratie oplossen
Er zijn tal van compatibiliteitsproblemen die u tegenkomen kunt, afhankelijk van beide op Hallo-versie van SQL Server in Hallo bron database en Hallo complexiteit van het Hallo-database die u wilt migreren. Oudere versies van SQL Server hebben vaker te maken met compatibiliteitsproblemen. Hallo na bronnen gebruiken, Daarnaast tooa gericht zoekopdrachten op Internet met uw zoekmachine van opties:

* [SQL Server-databasefuncties die niet worden ondersteund in Azure SQL Database](sql-database-transact-sql-information.md)
* [Database Engine-functionaliteit in SQL Server 2016 stopgezet](https://msdn.microsoft.com/library/ms144262%28v=sql.130%29)
* [Database Engine-functionaliteit in SQL Server 2014 stopgezet](https://msdn.microsoft.com/library/ms144262%28v=sql.120%29)
* [Database Engine-functionaliteit in SQL Server 2012 stopgezet](https://msdn.microsoft.com/library/ms144262%28v=sql.110%29)
* [Database Engine-functionaliteit in SQL Server 2008 R2 stopgezet](https://msdn.microsoft.com/library/ms144262%28v=sql.105%29)
* [Database Engine-functionaliteit in SQL Server 2005 stopgezet](https://msdn.microsoft.com/library/ms144262%28v=sql.90%29)

Bovendien toosearching Hallo van Internet en met behulp van deze resources gebruiken Hallo [MSDN SQL Server-communityforums](https://social.msdn.microsoft.com/Forums/sqlserver/home?category=sqlserver) of [StackOverflow](http://stackoverflow.com/).

## <a name="next-steps"></a>Volgende stappen
* Hallo-script te gebruiken op Hallo Azure SQL EMEA Engineers blog[tempdb-gebruik tijdens de migratie controleren](https://blogs.msdn.microsoft.com/azuresqlemea/2016/12/28/lesson-learned-10-monitoring-tempdb-usage/).
* Hallo-script te gebruiken op Hallo Azure SQL EMEA Engineers blog[ruimte voor transactielogboeken Hallo van uw database bewaken tijdens migratie is](https://blogs.msdn.microsoft.com/azuresqlemea/2016/10/31/lesson-learned-7-monitoring-the-transaction-log-space-of-my-database/0).
* Voor een SQL Server Customer Advisory Team blog over het migreren met behulp van Bacpac-bestanden, Zie [migreren van SQL Server-tooAzure SQL-Database Bacpac-bestanden met](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).
* Zie voor meer informatie over het werken met de UTC-tijd na de migratie [wijzigen Hallo standaardtijdzone voor uw lokale tijdzone](https://blogs.msdn.microsoft.com/azuresqlemea/2016/07/27/lesson-learned-4-modifying-the-default-time-zone-for-your-local-time-zone/).
* Zie voor meer informatie over het wijzigen van de standaardtaal Hallo van een database na de migratie [hoe toochange standaardtaal van Azure SQL Database Hallo](https://blogs.msdn.microsoft.com/azuresqlemea/2017/01/13/lesson-learned-16-how-to-change-the-default-language-of-azure-sql-database/).


