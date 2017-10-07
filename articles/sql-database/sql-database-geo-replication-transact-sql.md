---
title: aaaConfigure geo-replicatie voor Azure SQL Database met Transact-SQL | Microsoft Docs
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
ms.openlocfilehash: 295b6b12f257dfb15131d5ee28fbe65c6476352d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-with-transact-sql"></a>Actieve geo-replicatie configureren voor Azure SQL Database met Transact-SQL

Dit artikel ziet u hoe tooconfigure actieve geo-replicatie voor een Azure SQL Database met Transact-SQL.

tooinitiate failover met Transact-SQL, Zie [initiëren van een geplande of niet-geplande failover voor Azure SQL Database met Transact-SQL](sql-database-geo-replication-failover-transact-sql.md).

> [!NOTE]
> Wanneer u actieve geo-replicatie (leesbare secundaire replica's) voor herstel na noodgevallen gebruikt moet u een failover-groep voor alle databases in een toepassing tooenable automatisch en transparant failover configureren. Deze functie is in preview. Zie voor meer informatie [automatische failover groepen en geo-replicatie](sql-database-geo-replication-overview.md).
> 
> 

tooconfigure actieve geo-replicatie met Transact-SQL, moet u de volgende Hallo:

* Een Azure-abonnement
* Een logische Azure SQL Database-server <MyLocalServer> en een SQL-database <MyDB> -Hallo primaire database die u tooreplicate wilt
* Een of meer logische Azure SQL Database-servers < MySecondaryServer(n) > - Hallo logische servers die worden servers van partners Hallo waarin u secundaire databases maakt
* Een aanmelding die DBManager op Hallo primaire
* Hebt u db_ownership van Hallo lokale database dat u geo-replicatie gaat
* DBManager worden op Hallo partner (s) toowhich configureert u geo-replicatie
* Hallo nieuwste versie van SQL Server Management Studio (SSMS)

> [!IMPORTANT]
> Het verdient aanbeveling dat u altijd hello gebruiken meest recente versie van Management Studio tooremain gesynchroniseerd met updates tooMicrosoft Azure en SQL-Database. [SQL Server Management Studio bijwerken](https://msdn.microsoft.com/library/mt238290.aspx).
> 
> 

## <a name="add-secondary-database"></a>Secundaire database toevoegen
U kunt Hallo **ALTER DATABASE** instructie toocreate een geo-replicatie secundaire database op een partnerserver. U deze instructie niet uitvoeren op Hallo hoofddatabase van Hallo server met Hallo database toobe is gerepliceerd. Hallo geogerepliceerde database ('primaire database' hello) heeft dezelfde naam als Hallo-database wordt gerepliceerd en wordt standaard Hallo hebt Hallo hetzelfde niveau als de primaire database Hallo-service. Hallo secundaire database kunnen worden gelezen of niet-leesbare en kan een individuele database of in een elastische pool. Zie voor meer informatie [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) en [Servicelagen](sql-database-service-tiers.md).
Nadat Hallo secundaire database is gemaakt en wordt gemaakt, begint gegevens van de primaire database Hallo asynchroon te repliceren. Hallo stappen hieronder wordt beschreven hoe tooconfigure geo-replicatie met Management Studio. Als een individuele database of in een elastische pool zijn stappen toocreate niet-leesbare en leesbare secundaire replica's, beschikbaar.

> [!NOTE]
> Als een database bestaat op Hallo opgegeven partner-server met dezelfde naam als de primaire Hallo Hallo mislukt Hallo-opdracht van de database.
> 

### <a name="add-readable-secondary-single-database"></a>Leesbare secundaire database (één database) toevoegen
Volgende stappen toocreate een leesbare secundaire database als een individuele database Hallo gebruiken.

1. In Management Studio verbinding met de logische tooyour Azure SQL Database-server.
2. Open de map Hallo-Databases, vouw Hallo **systeemdatabases** map, klik met de rechtermuisknop op **master**, en klik vervolgens op **nieuwe Query**.
3. Gebruik de volgende Hallo **ALTER DATABASE** instructie toomake een lokale database in een primaire geo-replicatie met een leesbare secundaire database op een secundaire server.
   
        ALTER DATABASE <MyDB>
           ADD SECONDARY ON SERVER <MySecondaryServer2> WITH (ALLOW_CONNECTIONS = ALL);
4. Klik op **Execute** toorun Hallo query.

### <a name="add-readable-secondary-elastic-pool"></a>Leesbare secundaire database (elastische pool) toevoegen
Gebruik Hallo stappen toocreate een leesbare secundaire database in een elastische pool te volgen.

1. In Management Studio verbinding met de logische tooyour Azure SQL Database-server.
2. Open de map Hallo-Databases, vouw Hallo **systeemdatabases** map, klik met de rechtermuisknop op **master**, en klik vervolgens op **nieuwe Query**.
3. Gebruik de volgende Hallo **ALTER DATABASE** instructie toomake een lokale database in een primaire geo-replicatie met een leesbare secundaire database op een secundaire server in een elastische pool.
   
        ALTER DATABASE <MyDB>
           ADD SECONDARY ON SERVER <MySecondaryServer4> WITH (ALLOW_CONNECTIONS = ALL
           , SERVICE_OBJECTIVE = ELASTIC_POOL (name = MyElasticPool2));
4. Klik op **Execute** toorun Hallo query.

## <a name="remove-secondary-database"></a>Secundaire database verwijderen
U kunt Hallo **ALTER DATABASE** instructie toopermanently Hallo replicatiesamenwerking tussen een secundaire database en de primaire beëindigen. Deze instructie is uitgevoerd voor de hoofddatabase Hallo op welke Hallo primaire database zich bevindt. Hallo secundaire database wordt na beëindiging van de relatie Hallo, een normale lezen / schrijven-database. Als Hallo connectiviteit toosecondary database verbroken is Hallo-opdracht is uitgevoerd maar Hallo secundaire worden alleen-lezen nadat de verbinding is hersteld. Zie voor meer informatie [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) en [Servicelagen](sql-database-service-tiers.md).

Volgende stappen tooremove geo-replicatie secundaire uit een associatie geo-replicatie hello gebruiken.

1. In Management Studio verbinding met de logische tooyour Azure SQL Database-server.
2. Open de map Hallo-Databases, vouw Hallo **systeemdatabases** map, klik met de rechtermuisknop op **master**, en klik vervolgens op **nieuwe Query**.
3. Gebruik de volgende Hallo **ALTER DATABASE** instructie tooremove geo-replicatie secundaire.
   
        ALTER DATABASE <MyDB>
           REMOVE SECONDARY ON SERVER <MySecondaryServer1>;
4. Klik op **Execute** toorun Hallo query.

## <a name="monitor-active-geo-replication-configuration-and-health"></a>Controleren van actieve geo-replicatie de configuratie en status

Bewaking taken omvatten het controleren van Hallo geo-replicatie configuratie en bewaking van de status van replicatie van gegevens.  U kunt Hallo **sys.dm_geo_replication_links** dynamische Beheerweergave in Hallo hoofddatabase tooreturn informatie over alle afgesloten replicatiekoppelingen voor elke database op logische hello Azure SQL Database-server. Deze weergave bevat een rij voor elk van de replicatiekoppeling Hallo tussen de primaire en secundaire databases. U kunt Hallo **sys.dm_replication_link_status** dynamische Beheerweergave weergeven tooreturn een rij voor elke Azure SQL Database die momenteel bezig een replicatiekoppeling voor replicatie. Dit omvat zowel primaire als secundaire databases. Als meer dan één continue replicatie in een koppeling voor een bepaalde primaire database bestaat, wordt in deze tabel een rij bevat voor elk Hallo relaties. Hallo weergave wordt gemaakt in alle databases, met inbegrip van Hallo logische master. Uitvoeren van query's in deze weergave in de logische master Hallo retourneert echter een lege set. U kunt Hallo **sys.dm_operation_status bevat** dynamische Beheerweergave tooshow Hallo status bekijken voor alle bewerkingen, inclusief Hallo status van replicatiekoppelingen Hallo databasequery. Zie voor meer informatie [sys.geo_replication_links (Azure SQL Database)](https://msdn.microsoft.com/library/mt575501.aspx), [sys.dm_geo_replication_link_status (Azure SQL Database)](https://msdn.microsoft.com/library/mt575504.aspx), en [sys.dm_operation_status bevat (Azure SQL Database)](https://msdn.microsoft.com/library/dn270022.aspx).

Hallo te volgen stappen toomonitor een actieve geo-replicatie samen gebruiken.

1. In Management Studio verbinding met de logische tooyour Azure SQL Database-server.
2. Open de map Hallo-Databases, vouw Hallo **systeemdatabases** map, klik met de rechtermuisknop op **master**, en klik vervolgens op **nieuwe Query**.
3. Hallo instructie tooshow na alle databases met geo-replicatiekoppelingen gebruiken.
   
        SELECT database_id, start_date, modify_date, partner_server, partner_database, replication_state_desc, role, secondary_allow_connections_desc FROM sys.geo_replication_links;
4. Klik op **Execute** toorun Hallo query.
5. Open de map Hallo-Databases, vouw Hallo **systeemdatabases** map, klik met de rechtermuisknop op **mijndb**, en klik vervolgens op **nieuwe Query**.
6. Gebruik Hallo instructie tooshow Hallo replicatie na vertraagde en laatste tijdstip van de replicatie van mijn secundaire databases van mijndb.
   
        SELECT link_guid, partner_server, last_replication, replication_lag_sec FROM sys.dm_geo_replication_link_status
7. Klik op **Execute** toorun Hallo query.
8. Gebruik hello instructie tooshow Hallo meest recente geo-replicatie bewerkingen die zijn gekoppeld met database mijndb te volgen.
   
        SELECT * FROM sys.dm_operation_status where major_resource_id = 'MyDB'
        ORDER BY start_time DESC
9. Klik op **Execute** toorun Hallo query.

## <a name="next-steps"></a>Volgende stappen
* toolearn meer informatie over failover-groepen en actieve geo-replicatie, Zie - [failover-groepen](sql-database-geo-replication-overview.md)
* Zie voor een overzicht van zakelijke continuïteit en scenario's [Business continuity-overzicht](sql-database-business-continuity.md)

