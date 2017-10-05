---
title: Geo-replicatie configureren voor Azure SQL Database met Transact-SQL | Microsoft Docs
description: Geo-replicatie configureren voor Azure SQL Database Transact-SQL met
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: d94d89a6-3234-46c5-8279-5eb8daad10ac
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/14/2017
ms.author: carlrab
ms.openlocfilehash: e5011c1c67e051616d53621b72e46ba894ca3c02
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-with-transact-sql"></a>Actieve geo-replicatie configureren voor Azure SQL Database met Transact-SQL

In dit artikel leest u hoe het configureren van actieve geo-replicatie voor een Azure SQL Database met Transact-SQL.

Zie voor het initiëren van failover met Transact-SQL [initiëren van een geplande of niet-geplande failover voor Azure SQL Database met Transact-SQL](sql-database-geo-replication-failover-transact-sql.md).

> [!NOTE]
> Wanneer u actieve geo-replicatie (leesbare secundaire replica's) voor herstel na noodgevallen gebruikt moet u een failover-groep voor alle databases in een toepassing waarmee automatisch en transparant failover configureren. Deze functie is in preview. Zie voor meer informatie [automatische failover groepen en geo-replicatie](sql-database-geo-replication-overview.md).
> 
> 

Actieve geo-replicatie configureren met behulp van Transact-SQL, moet u het volgende:

* Een Azure-abonnement
* Een logische Azure SQL Database-server <MyLocalServer> en een SQL-database <MyDB> -de primaire database die u wilt repliceren
* Een of meer logische Azure SQL Database-servers < MySecondaryServer(n) > - de logische servers die de servers van partners waarin u secundaire databases maakt
* Een aanmelding die op de primaire DBManager
* Hebt u db_ownership van de lokale database dat u geo-replicatie gaat
* DBManager worden op de partner (s) waarvoor u geo-replicatie wilt configureren
* De nieuwste versie van SQL Server Management Studio (SSMS)

> [!IMPORTANT]
> Het wordt aanbevolen om altijd de nieuwste versie van Management Studio te gebruiken, zodat uw versie gesynchroniseerd blijft met updates voor Microsoft Azure en SQL Database. [SQL Server Management Studio bijwerken](https://msdn.microsoft.com/library/mt238290.aspx).
> 
> 

## <a name="add-secondary-database"></a>Secundaire database toevoegen
U kunt de **ALTER DATABASE** instructie voor het maken van een secundaire geo-replicatie-database op een partnerserver. U deze instructie niet uitvoeren op de database master van de server met de database worden gerepliceerd. De database geogerepliceerde (de ' primaire database') heeft dezelfde naam als de database wordt gerepliceerd en, standaard, hebben hetzelfde serviceniveau als de primaire database. De secundaire database kunnen worden gelezen of niet-leesbare en kan een individuele database of in een elastische pool. Zie voor meer informatie [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) en [Servicelagen](sql-database-service-tiers.md).
Nadat de secundaire database is gemaakt en wordt gemaakt, begint gegevens asynchroon van de primaire database te repliceren. De volgende stappen wordt beschreven hoe u geo-replicatie configureren met behulp van Management Studio. Stappen voor het maken van niet-leesbare en leesbare secundaire databases, als een individuele database of in een elastische pool zijn opgegeven.

> [!NOTE]
> Als een database op de opgegeven partner-server met dezelfde naam als de primaire database bestaat, de opdracht mislukt.
> 

### <a name="add-readable-secondary-single-database"></a>Leesbare secundaire database (één database) toevoegen
Gebruik de volgende stappen voor het maken van een leesbare secundaire database als een individuele database.

1. In de Management Studio verbinding met uw logische Azure SQL Database-server.
2. Open de map Databases, vouw de **systeemdatabases** map, klik met de rechtermuisknop op **master**, en klik vervolgens op **nieuwe Query**.
3. Gebruik de volgende **ALTER DATABASE** instructie naar een lokale database in een geo-replicatie primair met een leesbare secundaire database op een secundaire server maken.
   
        ALTER DATABASE <MyDB>
           ADD SECONDARY ON SERVER <MySecondaryServer2> WITH (ALLOW_CONNECTIONS = ALL);
4. Klik op **Uitvoeren** om de query uit te voeren.

### <a name="add-readable-secondary-elastic-pool"></a>Leesbare secundaire database (elastische pool) toevoegen
Gebruik de volgende stappen voor het maken van een leesbare secundaire database in een elastische pool.

1. In de Management Studio verbinding met uw logische Azure SQL Database-server.
2. Open de map Databases, vouw de **systeemdatabases** map, klik met de rechtermuisknop op **master**, en klik vervolgens op **nieuwe Query**.
3. Gebruik de volgende **ALTER DATABASE** instructie naar een lokale database in een geo-replicatie primair met een leesbare secundaire database op een secundaire server in een elastische pool maken.
   
        ALTER DATABASE <MyDB>
           ADD SECONDARY ON SERVER <MySecondaryServer4> WITH (ALLOW_CONNECTIONS = ALL
           , SERVICE_OBJECTIVE = ELASTIC_POOL (name = MyElasticPool2));
4. Klik op **Uitvoeren** om de query uit te voeren.

## <a name="remove-secondary-database"></a>Secundaire database verwijderen
U kunt de **ALTER DATABASE** instructie de replicatiesamenwerking tussen een secundaire database en de primaire permanent is beëindigd. Deze instructie is uitgevoerd voor de database master waarop de primaire database zich bevindt. Na de relatie wordt beëindigd wordt de secundaire database een normale lezen / schrijven-database. De opdracht is geslaagd, maar de secundaire alleen-lezen worden nadat de verbinding is hersteld als de verbinding met de secundaire database verbroken is. Zie voor meer informatie [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) en [Servicelagen](sql-database-service-tiers.md).

Gebruik de volgende stappen secundaire geo-replicatie verwijderen uit een associatie geo-replicatie.

1. In de Management Studio verbinding met uw logische Azure SQL Database-server.
2. Open de map Databases, vouw de **systeemdatabases** map, klik met de rechtermuisknop op **master**, en klik vervolgens op **nieuwe Query**.
3. Gebruik de volgende **ALTER DATABASE** instructie voor het verwijderen van een secundaire geo-replicatie.
   
        ALTER DATABASE <MyDB>
           REMOVE SECONDARY ON SERVER <MySecondaryServer1>;
4. Klik op **Uitvoeren** om de query uit te voeren.

## <a name="monitor-active-geo-replication-configuration-and-health"></a>Controleren van actieve geo-replicatie de configuratie en status

Monitoringtaken zijn bewaking van de configuratie van de geo-replicatie en de bewaking van de status van replicatie van gegevens.  U kunt de **sys.dm_geo_replication_links** dynamische Beheerweergave in de database master om informatie te retourneren over alle afgesloten replicatiekoppelingen voor elke database op de logische Azure SQL Database-server. Deze weergave bevat een rij voor elk van de replicatiekoppeling tussen de primaire en secundaire databases. U kunt de **sys.dm_replication_link_status** dynamische Beheerweergave te retourneren van een rij voor elke Azure SQL Database die momenteel bezig een replicatiekoppeling voor replicatie. Dit omvat zowel primaire als secundaire databases. Als meer dan één continue replicatie in een koppeling voor een bepaalde primaire database bestaat, wordt in deze tabel een rij bevat voor elk van de relaties. De weergave wordt gemaakt in alle databases, met inbegrip van de logische-master. Uitvoeren van query's in deze weergave in de logische master retourneert echter een lege set. U kunt de **sys.dm_operation_status bevat** dynamische Beheerweergave weer te geven van de status voor alle databasequery bewerkingen, inclusief de status van de replicatiekoppelingen. Zie voor meer informatie [sys.geo_replication_links (Azure SQL Database)](https://msdn.microsoft.com/library/mt575501.aspx), [sys.dm_geo_replication_link_status (Azure SQL Database)](https://msdn.microsoft.com/library/mt575504.aspx), en [sys.dm_operation_status bevat (Azure SQL Database)](https://msdn.microsoft.com/library/dn270022.aspx).

Gebruik de volgende stappen voor het bewaken van de verbinding van een actieve geo-replicatie.

1. In de Management Studio verbinding met uw logische Azure SQL Database-server.
2. Open de map Databases, vouw de **systeemdatabases** map, klik met de rechtermuisknop op **master**, en klik vervolgens op **nieuwe Query**.
3. Gebruik de volgende instructie wilt weergeven van alle databases met geo-replicatiekoppelingen.
   
        SELECT database_id, start_date, modify_date, partner_server, partner_database, replication_state_desc, role, secondary_allow_connections_desc FROM sys.geo_replication_links;
4. Klik op **Uitvoeren** om de query uit te voeren.
5. Open de map Databases, vouw de **systeemdatabases** map, klik met de rechtermuisknop op **mijndb**, en klik vervolgens op **nieuwe Query**.
6. Gebruik de volgende instructie voor het weergeven van de replicatie lag en de laatste replicatie van mijn secundaire databases van mijndb tijd.
   
        SELECT link_guid, partner_server, last_replication, replication_lag_sec FROM sys.dm_geo_replication_link_status
7. Klik op **Uitvoeren** om de query uit te voeren.
8. Gebruik de volgende instructie om de meest recente geo-replicatie-bewerkingen die zijn gekoppeld aan database mijndb weer te geven.
   
        SELECT * FROM sys.dm_operation_status where major_resource_id = 'MyDB'
        ORDER BY start_time DESC
9. Klik op **Uitvoeren** om de query uit te voeren.

## <a name="next-steps"></a>Volgende stappen
* Zie voor meer informatie over failover-groepen en actieve geo-replicatie - [failover-groepen](sql-database-geo-replication-overview.md)
* Zie voor een overzicht van zakelijke continuïteit en scenario's [Business continuity-overzicht](sql-database-business-continuity.md)

