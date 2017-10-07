---
title: aaaReporting voor cloud uitgebreide databases | Microsoft Docs
description: hoe tooset up elastische query's over horizontale partities
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: f86eccb8-6323-4ba7-8559-8a7c039049f3
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: mlandzic
ms.openlocfilehash: 78986c2040bf308195bf7c77e64d4f37273fcf36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-across-scaled-out-cloud-databases-preview"></a>Rapportage over cloud uitgebreide databases (preview)
![Vragen over shards][1]

Shard databases rijen verdelen over een uitgebreid uit gegevens die laag. Hallo-schema is vrijwel identiek voor alle deelnemende databases, ook wel bekend als horizontaal partitioneren. Een elastische query gebruiken, kunt u rapporten die alle databases in een shard-database omvatten maken.

Zie voor een snel starten [rapportage over cloud uitgebreide databases](sql-database-elastic-query-getting-started.md).

Zie voor niet-shard databases [Query via cloud-databases met verschillende schema's](sql-database-elastic-query-vertical-partitioning.md). 

## <a name="prerequisites"></a>Vereisten
* Maakt een shard-toewijzing met Hallo-clientbibliotheek voor elastische database. Zie [Shard kaart management](sql-database-elastic-scale-shard-map-management.md). Of gebruik Hallo voorbeeld-app in [aan de slag met hulpprogramma's voor elastische database](sql-database-elastic-scale-get-started.md).
* U kunt ook [migreren bestaande databases tooscaled-out-databases](sql-database-elastic-convert-to-use-elastic-tools.md).
* Hallo-gebruiker, moet ze beschikken over een externe gegevensbron ALTER machtiging. Deze machtiging is opgenomen in de machtiging ALTER DATABASE Hallo.
* EEN externe gegevensbron ALTER machtigingen zijn vereist toorefer toohello onderliggende gegevensbron.

## <a name="overview"></a>Overzicht
Deze instructies maken Hallo metagegevens weergave van de gedeelde gegevenslaag in Hallo elastische query uitvoeren op database. 

1. [CREATE MASTER KEY](https://msdn.microsoft.com/library/ms174382.aspx)
2. [MAKEN VAN DATABASE-SCOPED REFERENTIE](https://msdn.microsoft.com/library/mt270260.aspx)
3. [EXTERNE GEGEVENSBRON MAKEN](https://msdn.microsoft.com/library/dn935022.aspx)
4. [CREATE EXTERNAL TABLE](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="11-create-database-scoped-master-key-and-credentials"></a>1.1 bereik databasehoofdsleutel en referenties maken
Hallo-referentie wordt gebruikt door Hallo elastische query tooconnect tooyour externe databases.  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> Zorg ervoor dat Hallo *'\<gebruikersnaam\>'* omvat geen *'@servername'* achtervoegsel. 
> 
> 

## <a name="12-create-external-data-sources"></a>1.2 externe gegevensbronnen maken
Syntaxis:

    <External_Data_Source> ::=    
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH                                              
            (TYPE = SHARD_MAP_MANAGER,
                       LOCATION = '<fully_qualified_server_name>',
            DATABASE_NAME = ‘<shardmap_database_name>',
            CREDENTIAL = <credential_name>, 
            SHARD_MAP_NAME = ‘<shardmapname>’ 
                   ) [;] 

### <a name="example"></a>Voorbeeld
    CREATE EXTERNAL DATA SOURCE MyExtSrc 
    WITH 
    ( 
        TYPE=SHARD_MAP_MANAGER,
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ShardMapDatabase', 
        CREDENTIAL= SMMUser, 
        SHARD_MAP_NAME='ShardMap' 
    );

Hallo-lijst met huidige externe gegevensbronnen ophalen: 

    select * from sys.external_data_sources; 

de externe gegevensbron Hallo verwijst naar de shard-kaart. Een elastische query gebruikt vervolgens de externe gegevensbron Hallo en onderliggende shard kaart tooenumerate Hallo databases die deel uitmaken van de gegevenslaag Hallo Hallo. Hallo dezelfde referenties zijn gebruikte tooread hello shard-toewijzing en tooaccess gegevens op Hallo shards tijdens de verwerking van een elastische query Hallo Hallo. 

## <a name="13-create-external-tables"></a>1.3 externe tabellen maken
Syntaxis:  

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name  
        ( { <column_definition> } [ ,...n ])     
        { WITH ( <sharded_external_table_options> ) }
    ) [;]  

    <sharded_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>,       
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 
      DISTRIBUTION = SHARDED(<sharding_column_name>) | REPLICATED |ROUND_ROBIN

**Voorbeeld**

    CREATE EXTERNAL TABLE [dbo].[order_line]( 
         [ol_o_id] int NOT NULL, 
         [ol_d_id] tinyint NOT NULL,
         [ol_w_id] int NOT NULL, 
         [ol_number] tinyint NOT NULL, 
         [ol_i_id] int NOT NULL, 
         [ol_delivery_d] datetime NOT NULL, 
         [ol_amount] smallmoney NOT NULL, 
         [ol_supply_w_id] int NOT NULL, 
         [ol_quantity] smallint NOT NULL, 
         [ol_dist_info] char(24) NOT NULL 
    ) 

    WITH 
    ( 
        DATA_SOURCE = MyExtSrc, 
         SCHEMA_NAME = 'orders', 
         OBJECT_NAME = 'order_details', 
        DISTRIBUTION=SHARDED(ol_w_id)
    ); 

Hallo-lijst met externe tabellen ophalen van de huidige database Hallo: 

    SELECT * from sys.external_tables; 

externe tabellen toodrop:

    DROP EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name[;]

### <a name="remarks"></a>Opmerkingen
Hallo gegevens\_bron component Hallo externe gegevensbron (een shard-kaart) die wordt gebruikt voor de externe tabel Hallo definieert.  

Hallo SCHEMA\_naam en het OBJECT\_naam componenten Hallo externe tabel tooa met tabeldefinitie in een ander schema toewijzen. Als u dit weglaat, Hallo-schema van Hallo extern object wordt aangenomen dat toobe 'dbo' en de naam ervan wordt uitgegaan van toobe identieke toohello externe tabelnaam wordt gedefinieerd. Dit is handig als Hallo-naam van de externe tabel is al in gebruik in Hallo-database waar u toocreate Hallo externe tabel. Bijvoorbeeld, u wilt dat een externe tabel tooget een samengevoegde weergave van catalogusweergaven toodefine of DMV's voor uw gegevens geschaalde uit laag. Aangezien lokaal catalogusweergaven en DMV's bestaat, kunt u hun namen voor de definitie van de externe tabel Hallo niet gebruiken. In plaats daarvan gebruik een andere naam en Hallo catalogusweergave gebruiken of de naam van de DMV in Hallo SCHEMA Hallo\_naam en/of OBJECT\_naam componenten. (Zie onderstaand voorbeeld voor Hallo.) 

Hallo distributie-component bevat Hallo gegevensdistributie gebruikt voor deze tabel. Hallo-queryprocessor Hallo informatie in Hallo distributie component toobuild Hallo meest efficiënt queryplannen wordt gebruikt.  

1. **SHARD** betekent dat gegevens horizontaal over Hallo databases is gepartitioneerd. Hallo partitiesleutel voor Hallo gegevensdistributie Hallo is **< sharding_column_name >** parameter.
2. **GEREPLICEERD** betekent dat identieke kopieën van Hallo tabel aanwezig op elke database zijn. Het is uw verantwoordelijkheid tooensure Hallo replica's zijn identiek voor Hallo-databases.
3. **RONDE\_ROBIN** betekent die tabel Hallo horizontaal is gepartitioneerd met behulp van een distributiemethode van afhankelijk zijn van toepassing. 

**Gegevens servicetier verwijzing**: Hallo externe tabel DDL verwijst tooan externe gegevensbron. de externe gegevensbron Hallo geeft een shard-toewijzing die externe tabel Hallo Hallo informatie nodig toolocate alle Hallo-databases in de gegevenslaag biedt. 

### <a name="security-considerations"></a>Beveiligingsoverwegingen
Gebruikers met toegang toohello externe tabel toegang automatisch toohello onderliggende externe tabellen onder Hallo referentie gegeven in de definitie van Hallo de externe gegevensbron. Vermijd ongewenste verhoging van bevoegdheden via Hallo referentie van de externe gegevensbron Hallo. Gebruik GRANT of REVOKE voor een externe tabel net alsof het een gewone tabellen.  

Nadat u uw externe gegevensbron en uw externe tabellen hebt gedefinieerd, kunt u nu volledige T-SQL gebruiken via uw externe tabellen.

## <a name="example-querying-horizontal-partitioned-databases"></a>Voorbeeld: uitvoeren van query's horizontale gepartitioneerde databases
Hallo volgende query voert een koppeling drie richtingen tussen datawarehouses, orders en regels en maakt gebruik van verschillende statistische functies en een selectieve filter. Er wordt vanuit gegaan (1) de horizontale partitionering (sharding) en (2) worden in datawarehouses, orders en regels shard Hallo datawarehouse-id-kolom zijn en die Hallo elastische query kunt plaatsen Hallo joins op Hallo shards en Hallo dure deel van Hallo-query op Hallo verwerken shards parallel. 

    select  
         w_id as warehouse,
         o_c_id as customer,
         count(*) as cnt_orderline,
         max(ol_quantity) as max_quantity,
         avg(ol_amount) as avg_amount, 
         min(ol_delivery_d) as min_deliv_date
    from warehouse 
    join orders 
    on w_id = o_w_id
    join order_line 
    on o_id = ol_o_id and o_w_id = ol_w_id 
    where w_id > 100 and w_id < 200 
    group by w_id, o_c_id 

## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a>Opgeslagen procedure voor uitvoering op afstand T-SQL: sp\_execute_remote
Elastische query bevat ook een opgeslagen procedure die rechtstreekse toegang toohello shards biedt. Hallo opgeslagen procedure is aangeroepen [sp\_uitvoeren \_externe](https://msdn.microsoft.com/library/mt703714) en kan extern opgeslagen procedures gebruikt tooexecute of T-SQL-code op Hallo externe databases. Het duurt Hallo volgende parameters: 

* Naam van de gegevensbron (nvarchar): Hallo-naam van de externe gegevensbron Hallo van het type RDBMS. 
* Query (nvarchar): Hallo T-SQL-query toobe uitgevoerd op elke shard. 
* Parameterdeclaratie (nvarchar) - optioneel: de tekenreeks met gegevens typedefinities voor Hallo-parameters die worden gebruikt in de queryparameter hello (zoals sp_executesql). 
* Waarde parameterlijst - optioneel: door komma's gescheiden lijst met parameterwaarden (zoals sp_executesql).

Hallo sp\_uitvoeren\_maakt gebruik van externe Hallo externe gegevensbron opgegeven in Hallo aanroep parameters tooexecute Hallo gegeven T-SQL-instructie op Hallo externe databases. Hallo-referentie van Hallo externe gegevens tooconnect toohello shardmap manager brondatabase en de externe databases Hallo wordt gebruikt.  

Voorbeeld: 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 

## <a name="connectivity-for-tools"></a>Connectiviteit voor hulpprogramma 's
Reguliere tekenreeksen tooconnect van de SQL Server-verbinding gebruiken uw toepassing, uw database BI en gegevens integratie extra toohello met de definities van de externe tabel. Zorg ervoor dat SQL Server wordt ondersteund als een gegevensbron voor het hulpprogramma. Vervolgens verwijzen naar Hallo elastische query uitvoeren op database zoals een ander SQL Server-database verbonden toohello hulpprogramma en externe tabellen vanuit uw hulpprogramma of toepassing gebruiken alsof ze lokaal tabellen. 

## <a name="best-practices"></a>Aanbevolen procedures
* Zorg ervoor dat die database Hallo elastische query eindpunt access toohello shardmap-database en alle shards via SQL DB firewalls Hallo heeft gekregen.  
* Valideren of Hallo gegevensdistributie gedefinieerd door de externe tabel Hallo af te dwingen. Als uw werkelijke gegevensdistributie van het Hallo-distributiepunt opgegeven in de tabeldefinitie van de verschilt, kan uw query's kunnen onverwachte resultaten opleveren. 
* Elastische query momenteel geen uit shard elimineren wanneer predicaten Hallo sharding sleutel zou toe te staan toosafely uitsluiten bepaalde shards van verwerken.
* Elastische query werkt het beste voor query's waar de meeste Hallo berekening op Hallo shards kan worden uitgevoerd. U doorgaans ophalen Hallo beste queryprestaties selectief filter predicaten die kan worden geëvalueerd op Hallo shards of joins via Hallo sleutels die kunnen worden uitgevoerd op een manier uitgelijnd op alle shards. Andere querypatronen mogelijk grote hoeveelheden gegevens van Hallo shards toohello hoofdknooppunt tooload en slecht mag uitvoeren

## <a name="next-steps"></a>Volgende stappen

* Zie voor een overzicht van elastische query [elastische query overzicht](sql-database-elastic-query-overview.md).
* Zie voor een verticale partitie zelfstudie [aan de slag met cross-databasequery (verticale partities)](sql-database-elastic-query-getting-started-vertical.md).
* Zie voor de syntaxis en voorbeelden query's voor verticaal gepartitioneerde gegevens [gegevens opvragen verticaal gepartitioneerd)](sql-database-elastic-query-vertical-partitioning.md)
* Zie voor een zelfstudie horizontaal partitioneren (sharding) [aan de slag met elastische query voor horizontale partitioneren (sharding)](sql-database-elastic-query-getting-started.md).
* Zie [sp\_uitvoeren \_externe](https://msdn.microsoft.com/library/mt703714) voor een opgeslagen procedure die een Transact-SQL-instructie op een enkele externe Azure SQL Database of een set van databases die fungeren als shards in een horizontale partitieschema wordt uitgevoerd.


<!--Image references-->
[1]: ./media/sql-database-elastic-query-horizontal-partitioning/horizontalpartitioning.png
<!--anchors-->
