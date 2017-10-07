---
title: aaaQuery via cloud-databases met verschillende schema | Microsoft Docs
description: hoe tooset om meerdere databases query's via verticale partities
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: 84c261f2-9edc-42f4-988c-cf2f251f5eff
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 1134e2e608128b7a9cac47ff35a22a11e6e5bc14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="query-across-cloud-databases-with-different-schemas-preview"></a>Query voor cloud-databases met verschillende schema's (preview)
![Query tussen tabellen in verschillende databases][1]

Databases verticaal gepartitioneerd Gebruik verschillende sets van tabellen op verschillende databases. Dat betekent dat Hallo-schema verschilt van andere databases. Alle tabellen voor inventarisatie zijn bijvoorbeeld op de ene database terwijl alle accounting-gerelateerde tabellen op een tweede database zijn. 

## <a name="prerequisites"></a>Vereisten
* Hallo-gebruiker, moet ze beschikken over een externe gegevensbron ALTER machtiging. Deze machtiging is opgenomen in de machtiging ALTER DATABASE Hallo.
* EEN externe gegevensbron ALTER machtigingen zijn vereist toorefer toohello onderliggende gegevensbron.

## <a name="overview"></a>Overzicht

> [!NOTE]
> In tegenstelling tot met horizontale partitioneren, afhankelijk deze DDL-componenten niet van het definiëren van een gegevenslaag met een shard-toewijzing via Hallo-clientbibliotheek voor elastische database.
>

1. [CREATE MASTER KEY](https://msdn.microsoft.com/library/ms174382.aspx)
2. [MAKEN VAN DATABASE-SCOPED REFERENTIE](https://msdn.microsoft.com/library/mt270260.aspx)
3. [EXTERNE GEGEVENSBRON MAKEN](https://msdn.microsoft.com/library/dn935022.aspx)
4. [CREATE EXTERNAL TABLE](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="create-database-scoped-master-key-and-credentials"></a>Bereik databasehoofdsleutel en referenties maken
Hallo-referentie wordt gebruikt door Hallo elastische query tooconnect tooyour externe databases.  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> Zorg ervoor dat Hallo `<username>` omvat geen **'@servername'** achtervoegsel. 
>

## <a name="create-external-data-sources"></a>Externe gegevensbronnen maken
Syntaxis:

    <External_Data_Source> ::=
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH 
               (TYPE = RDBMS,
                LOCATION = ’<fully_qualified_server_name>’,
                DATABASE_NAME = ‘<remote_database_name>’,  
                CREDENTIAL = <credential_name> 
                ) [;] 

> [!IMPORTANT]
> Hallo typeparameter te moet worden ingesteld**RDBMS**. 
>

### <a name="example"></a>Voorbeeld
Hallo illustreert volgende voorbeeld Hallo gebruik van Hallo instructie CREATE voor externe gegevensbronnen. 

    CREATE EXTERNAL DATA SOURCE RemoteReferenceData 
    WITH 
    ( 
        TYPE=RDBMS, 
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ReferenceData', 
        CREDENTIAL= SqlUser 
    ); 

tooretrieve hello lijst met huidige externe gegevensbronnen: 

    select * from sys.external_data_sources; 

### <a name="external-tables"></a>Externe tabellen
Syntaxis:

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name . ] table_name  
    ( { <column_definition> } [ ,...n ])     
    { WITH ( <rdbms_external_table_options> ) } 
    )[;] 

    <rdbms_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>, 
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 

### <a name="example"></a>Voorbeeld
    CREATE EXTERNAL TABLE [dbo].[customer]( 
        [c_id] int NOT NULL, 
        [c_firstname] nvarchar(256) NULL, 
        [c_lastname] nvarchar(256) NOT NULL, 
        [street] nvarchar(256) NOT NULL, 
        [city] nvarchar(256) NOT NULL, 
        [state] nvarchar(20) NULL, 
        [country] nvarchar(50) NOT NULL, 
    ) 
    WITH 
    ( 
           DATA_SOURCE = RemoteReferenceData 
    ); 

Hallo volgende voorbeeld ziet u hoe tooretrieve lijst met externe tabellen uit de huidige database Hallo Hallo: 

    select * from sys.external_tables; 

### <a name="remarks"></a>Opmerkingen
Elastische query breidt Hallo bestaande externe tabel syntaxis toodefine externe tabellen die gebruikmaken van externe gegevensbronnen van het type RDBMS. De definitie van een externe tabel voor de verticale partities heeft betrekking op Hallo volgende aspecten: 

* **Schema**: Hallo externe tabel DDL definieert een schema dat uw query's kunnen gebruiken. Hallo-schema is opgegeven in de definitie van de externe tabel moet toomatch Hallo schema van Hallo tabellen in de externe database Hallo waar Hallo werkelijke gegevens worden opgeslagen. 
* **Verwijzing naar de externe database**: Hallo externe tabel DDL verwijst tooan externe gegevensbron. de externe gegevensbron Hallo bevat logische Hallo-servernaam en databasenaam op van de externe database Hallo waar Hallo feitelijke tabelgegevens worden opgeslagen. 

Met een externe gegevensbron, zoals wordt beschreven in de vorige sectie hello, is Hallo syntaxis toocreate externe tabellen als volgt: 

Hallo DATA_SOURCE component definieert Hallo externe gegevensbron (dat wil zeggen Hallo externe database in geval van een verticale partities) die wordt gebruikt voor de externe tabel Hallo.  

Hallo SCHEMA_NAME en OBJECT_NAME kunnen bieden respectievelijk Hallo mogelijkheid toomap Hallo externe tabel tooa met tabeldefinitie in een ander schema op de externe database Hallo of tooa-tabel met een andere naam. Dit is handig als u toodefine een externe tabel tooa catalogusweergave of DMV op de externe database- of een andere situatie waarin de naam van de externe tabel Hallo is al in gebruik lokaal.  

Hallo verwijderd volgende DDL-instructie de definitie van een bestaande externe tabel van de lokale catalogus Hallo. Dit heeft geen gevolgen voor de externe database Hallo. 

    DROP EXTERNAL TABLE [ [ schema_name ] . | schema_name. ] table_name[;]  

**Machtigingen voor de externe tabel CREATE/DROP**: een externe gegevensbron ALTER machtigingen nodig voor de externe tabel-DDL die tevens benodigde toorefer toohello onderliggende gegevensbron.  

## <a name="security-considerations"></a>Beveiligingsoverwegingen
Gebruikers met toegang toohello externe tabel toegang automatisch toohello onderliggende externe tabellen onder Hallo referentie gegeven in de definitie van Hallo de externe gegevensbron. U moet zorgvuldig toegang toohello externe tabel in de volgorde tooavoid ongewenste verhoging van bevoegdheden via Hallo referentie van de externe gegevensbron Hallo beheren. Reguliere SQL-machtigingen kunnen worden gebruikt tooGRANT of in te trekken toegang tooan externe tabel net alsof het een gewone tabellen.  

## <a name="example-querying-vertically-partitioned-databases"></a>Voorbeeld: verticaal opvragen gepartitioneerd databases
Hallo volgende query wordt uitgevoerd een join drie richtingen tussen Hallo twee lokale tabellen voor orders en regels en de externe tabel Hallo voor klanten. Dit is een voorbeeld van Hallo verwijzing gegevens gebruiksvoorbeeld voor elastische query: 

    SELECT      
     c_id as customer,
     c_lastname as customer_name,
     count(*) as cnt_orderline, 
     max(ol_quantity) as max_quantity,
     avg(ol_amount) as avg_amount,
     min(ol_delivery_d) as min_deliv_date
    FROM customer 
    JOIN orders 
    ON c_id = o_c_id
    JOIN  order_line 
    ON o_id = ol_o_id and o_c_id = ol_c_id
    WHERE c_id = 100


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
Kunt u reguliere SQL Server-verbinding tekenreeksen tooconnect uw BI en gegevens integratie extra toodatabases op Hallo SQL DB-server waarvoor elastische query ingeschakeld en externe tabellen die zijn gedefinieerd. Zorg ervoor dat SQL Server wordt ondersteund als een gegevensbron voor het hulpprogramma. Raadpleeg toohello elastische query uitvoeren op database en de externe tabellen net als elke andere SQL Server-database dat u verbinding toowith uw hulpprogramma maken wilt. 

## <a name="best-practices"></a>Aanbevolen procedures
* Zorg ervoor dat die database Hallo elastische query eindpunt heeft gegeven voor toegang toohello externe database toegang inschakelen voor Azure-Services in de firewall-configuratie van SQL-database. Zorg er ook voor dat Hallo-referentie opgegeven Hallo externe gegevens brondefinitie is zich bij de externe database Hallo aanmelden kan en Hallo machtigingen tooaccess Hallo externe tabel is.  
* Elastische query werkt het beste voor query's waar de meeste Hallo berekening kan worden uitgevoerd op Hallo externe databases. U doorgaans ophalen Hallo beste queryprestaties selectief filter predicaten die kan worden geëvalueerd op Hallo externe databases of samenvoegingen die volledig kunnen worden uitgevoerd op de externe database Hallo. Andere querypatronen mogelijk grote hoeveelheden gegevens van de externe database Hallo tooload en slecht mag uitvoeren. 

## <a name="next-steps"></a>Volgende stappen

* Zie voor een overzicht van elastische query [elastische query overzicht](sql-database-elastic-query-overview.md).
* Zie voor een verticale partitie zelfstudie [aan de slag met cross-databasequery (verticale partities)](sql-database-elastic-query-getting-started-vertical.md).
* Zie voor een zelfstudie horizontaal partitioneren (sharding) [aan de slag met elastische query voor horizontale partitioneren (sharding)](sql-database-elastic-query-getting-started.md).
* Zie voor de syntaxis en voorbeelden query's voor horizontaal gepartitioneerde gegevens [gegevens opvragen horizontaal gepartitioneerd)](sql-database-elastic-query-horizontal-partitioning.md)
* Zie [sp\_uitvoeren \_externe](https://msdn.microsoft.com/library/mt703714) voor een opgeslagen procedure die een Transact-SQL-instructie op een enkele externe Azure SQL Database of een set van databases die fungeren als shards in een horizontale partitieschema wordt uitgevoerd.


<!--Image references-->
[1]: ./media/sql-database-elastic-query-vertical-partitioning/verticalpartitioning.png


<!--anchors-->
