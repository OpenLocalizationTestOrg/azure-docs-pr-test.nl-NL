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
# <a name="query-across-cloud-databases-with-different-schemas-preview"></a><span data-ttu-id="ed57d-103">Query voor cloud-databases met verschillende schema's (preview)</span><span class="sxs-lookup"><span data-stu-id="ed57d-103">Query across cloud databases with different schemas (preview)</span></span>
![Query tussen tabellen in verschillende databases][1]

<span data-ttu-id="ed57d-105">Databases verticaal gepartitioneerd Gebruik verschillende sets van tabellen op verschillende databases.</span><span class="sxs-lookup"><span data-stu-id="ed57d-105">Vertically-partitioned databases use different sets of tables on different databases.</span></span> <span data-ttu-id="ed57d-106">Dat betekent dat Hallo-schema verschilt van andere databases.</span><span class="sxs-lookup"><span data-stu-id="ed57d-106">That means that hello schema is different on different databases.</span></span> <span data-ttu-id="ed57d-107">Alle tabellen voor inventarisatie zijn bijvoorbeeld op de ene database terwijl alle accounting-gerelateerde tabellen op een tweede database zijn.</span><span class="sxs-lookup"><span data-stu-id="ed57d-107">For instance, all tables for inventory are on one database while all accounting-related tables are on a second database.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ed57d-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ed57d-108">Prerequisites</span></span>
* <span data-ttu-id="ed57d-109">Hallo-gebruiker, moet ze beschikken over een externe gegevensbron ALTER machtiging.</span><span class="sxs-lookup"><span data-stu-id="ed57d-109">hello user must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="ed57d-110">Deze machtiging is opgenomen in de machtiging ALTER DATABASE Hallo.</span><span class="sxs-lookup"><span data-stu-id="ed57d-110">This permission is included with hello ALTER DATABASE permission.</span></span>
* <span data-ttu-id="ed57d-111">EEN externe gegevensbron ALTER machtigingen zijn vereist toorefer toohello onderliggende gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="ed57d-111">ALTER ANY EXTERNAL DATA SOURCE permissions are needed toorefer toohello underlying data source.</span></span>

## <a name="overview"></a><span data-ttu-id="ed57d-112">Overzicht</span><span class="sxs-lookup"><span data-stu-id="ed57d-112">Overview</span></span>

> [!NOTE]
> <span data-ttu-id="ed57d-113">In tegenstelling tot met horizontale partitioneren, afhankelijk deze DDL-componenten niet van het definiëren van een gegevenslaag met een shard-toewijzing via Hallo-clientbibliotheek voor elastische database.</span><span class="sxs-lookup"><span data-stu-id="ed57d-113">Unlike with horizontal partitioning, these DDL statements do not depend on defining a data tier with a shard map through hello elastic database client library.</span></span>
>

1. [<span data-ttu-id="ed57d-114">CREATE MASTER KEY</span><span class="sxs-lookup"><span data-stu-id="ed57d-114">CREATE MASTER KEY</span></span>](https://msdn.microsoft.com/library/ms174382.aspx)
2. [<span data-ttu-id="ed57d-115">MAKEN VAN DATABASE-SCOPED REFERENTIE</span><span class="sxs-lookup"><span data-stu-id="ed57d-115">CREATE DATABASE SCOPED CREDENTIAL</span></span>](https://msdn.microsoft.com/library/mt270260.aspx)
3. [<span data-ttu-id="ed57d-116">EXTERNE GEGEVENSBRON MAKEN</span><span class="sxs-lookup"><span data-stu-id="ed57d-116">CREATE EXTERNAL DATA SOURCE</span></span>](https://msdn.microsoft.com/library/dn935022.aspx)
4. [<span data-ttu-id="ed57d-117">CREATE EXTERNAL TABLE</span><span class="sxs-lookup"><span data-stu-id="ed57d-117">CREATE EXTERNAL TABLE</span></span>](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="create-database-scoped-master-key-and-credentials"></a><span data-ttu-id="ed57d-118">Bereik databasehoofdsleutel en referenties maken</span><span class="sxs-lookup"><span data-stu-id="ed57d-118">Create database scoped master key and credentials</span></span>
<span data-ttu-id="ed57d-119">Hallo-referentie wordt gebruikt door Hallo elastische query tooconnect tooyour externe databases.</span><span class="sxs-lookup"><span data-stu-id="ed57d-119">hello credential is used by hello elastic query tooconnect tooyour remote databases.</span></span>  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> <span data-ttu-id="ed57d-120">Zorg ervoor dat Hallo `<username>` omvat geen **'@servername'** achtervoegsel.</span><span class="sxs-lookup"><span data-stu-id="ed57d-120">Ensure that hello `<username>` does not include any **"@servername"** suffix.</span></span> 
>

## <a name="create-external-data-sources"></a><span data-ttu-id="ed57d-121">Externe gegevensbronnen maken</span><span class="sxs-lookup"><span data-stu-id="ed57d-121">Create external data sources</span></span>
<span data-ttu-id="ed57d-122">Syntaxis:</span><span class="sxs-lookup"><span data-stu-id="ed57d-122">Syntax:</span></span>

    <External_Data_Source> ::=
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH 
               (TYPE = RDBMS,
                LOCATION = ’<fully_qualified_server_name>’,
                DATABASE_NAME = ‘<remote_database_name>’,  
                CREDENTIAL = <credential_name> 
                ) [;] 

> [!IMPORTANT]
> <span data-ttu-id="ed57d-123">Hallo typeparameter te moet worden ingesteld**RDBMS**.</span><span class="sxs-lookup"><span data-stu-id="ed57d-123">hello TYPE parameter must be set too**RDBMS**.</span></span> 
>

### <a name="example"></a><span data-ttu-id="ed57d-124">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="ed57d-124">Example</span></span>
<span data-ttu-id="ed57d-125">Hallo illustreert volgende voorbeeld Hallo gebruik van Hallo instructie CREATE voor externe gegevensbronnen.</span><span class="sxs-lookup"><span data-stu-id="ed57d-125">hello following example illustrates hello use of hello CREATE statement for external data sources.</span></span> 

    CREATE EXTERNAL DATA SOURCE RemoteReferenceData 
    WITH 
    ( 
        TYPE=RDBMS, 
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ReferenceData', 
        CREDENTIAL= SqlUser 
    ); 

<span data-ttu-id="ed57d-126">tooretrieve hello lijst met huidige externe gegevensbronnen:</span><span class="sxs-lookup"><span data-stu-id="ed57d-126">tooretrieve hello list of current external data sources:</span></span> 

    select * from sys.external_data_sources; 

### <a name="external-tables"></a><span data-ttu-id="ed57d-127">Externe tabellen</span><span class="sxs-lookup"><span data-stu-id="ed57d-127">External Tables</span></span>
<span data-ttu-id="ed57d-128">Syntaxis:</span><span class="sxs-lookup"><span data-stu-id="ed57d-128">Syntax:</span></span>

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name . ] table_name  
    ( { <column_definition> } [ ,...n ])     
    { WITH ( <rdbms_external_table_options> ) } 
    )[;] 

    <rdbms_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>, 
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 

### <a name="example"></a><span data-ttu-id="ed57d-129">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="ed57d-129">Example</span></span>
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

<span data-ttu-id="ed57d-130">Hallo volgende voorbeeld ziet u hoe tooretrieve lijst met externe tabellen uit de huidige database Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="ed57d-130">hello following example shows how tooretrieve hello list of external tables from hello current database:</span></span> 

    select * from sys.external_tables; 

### <a name="remarks"></a><span data-ttu-id="ed57d-131">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="ed57d-131">Remarks</span></span>
<span data-ttu-id="ed57d-132">Elastische query breidt Hallo bestaande externe tabel syntaxis toodefine externe tabellen die gebruikmaken van externe gegevensbronnen van het type RDBMS.</span><span class="sxs-lookup"><span data-stu-id="ed57d-132">Elastic query extends hello existing external table syntax toodefine external tables that use external data sources of type RDBMS.</span></span> <span data-ttu-id="ed57d-133">De definitie van een externe tabel voor de verticale partities heeft betrekking op Hallo volgende aspecten:</span><span class="sxs-lookup"><span data-stu-id="ed57d-133">An external table definition for vertical partitioning covers hello following aspects:</span></span> 

* <span data-ttu-id="ed57d-134">**Schema**: Hallo externe tabel DDL definieert een schema dat uw query's kunnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ed57d-134">**Schema**: hello external table DDL defines a schema that your queries can use.</span></span> <span data-ttu-id="ed57d-135">Hallo-schema is opgegeven in de definitie van de externe tabel moet toomatch Hallo schema van Hallo tabellen in de externe database Hallo waar Hallo werkelijke gegevens worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="ed57d-135">hello schema provided in your external table definition needs toomatch hello schema of hello tables in hello remote database where hello actual data is stored.</span></span> 
* <span data-ttu-id="ed57d-136">**Verwijzing naar de externe database**: Hallo externe tabel DDL verwijst tooan externe gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="ed57d-136">**Remote database reference**: hello external table DDL refers tooan external data source.</span></span> <span data-ttu-id="ed57d-137">de externe gegevensbron Hallo bevat logische Hallo-servernaam en databasenaam op van de externe database Hallo waar Hallo feitelijke tabelgegevens worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="ed57d-137">hello external data source specifies hello logical server name and database name of hello remote database where hello actual table data is stored.</span></span> 

<span data-ttu-id="ed57d-138">Met een externe gegevensbron, zoals wordt beschreven in de vorige sectie hello, is Hallo syntaxis toocreate externe tabellen als volgt:</span><span class="sxs-lookup"><span data-stu-id="ed57d-138">Using an external data source as outlined in hello previous section, hello syntax toocreate external tables is as follows:</span></span> 

<span data-ttu-id="ed57d-139">Hallo DATA_SOURCE component definieert Hallo externe gegevensbron (dat wil zeggen Hallo externe database in geval van een verticale partities) die wordt gebruikt voor de externe tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="ed57d-139">hello DATA_SOURCE clause defines hello external data source (i.e. hello remote database in case of vertical partitioning) that is used for hello external table.</span></span>  

<span data-ttu-id="ed57d-140">Hallo SCHEMA_NAME en OBJECT_NAME kunnen bieden respectievelijk Hallo mogelijkheid toomap Hallo externe tabel tooa met tabeldefinitie in een ander schema op de externe database Hallo of tooa-tabel met een andere naam.</span><span class="sxs-lookup"><span data-stu-id="ed57d-140">hello SCHEMA_NAME and OBJECT_NAME clauses provide hello ability toomap hello external table definition tooa table in a different schema on hello remote database, or tooa table with a different name, respectively.</span></span> <span data-ttu-id="ed57d-141">Dit is handig als u toodefine een externe tabel tooa catalogusweergave of DMV op de externe database- of een andere situatie waarin de naam van de externe tabel Hallo is al in gebruik lokaal.</span><span class="sxs-lookup"><span data-stu-id="ed57d-141">This is useful if you want toodefine an external table tooa catalog view or DMV on your remote database - or any other situation where hello remote table name is already taken locally.</span></span>  

<span data-ttu-id="ed57d-142">Hallo verwijderd volgende DDL-instructie de definitie van een bestaande externe tabel van de lokale catalogus Hallo.</span><span class="sxs-lookup"><span data-stu-id="ed57d-142">hello following DDL statement drops an existing external table definition from hello local catalog.</span></span> <span data-ttu-id="ed57d-143">Dit heeft geen gevolgen voor de externe database Hallo.</span><span class="sxs-lookup"><span data-stu-id="ed57d-143">It does not impact hello remote database.</span></span> 

    DROP EXTERNAL TABLE [ [ schema_name ] . | schema_name. ] table_name[;]  

<span data-ttu-id="ed57d-144">**Machtigingen voor de externe tabel CREATE/DROP**: een externe gegevensbron ALTER machtigingen nodig voor de externe tabel-DDL die tevens benodigde toorefer toohello onderliggende gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="ed57d-144">**Permissions for CREATE/DROP EXTERNAL TABLE**: ALTER ANY EXTERNAL DATA SOURCE permissions are needed for external table DDL which is also needed toorefer toohello underlying data source.</span></span>  

## <a name="security-considerations"></a><span data-ttu-id="ed57d-145">Beveiligingsoverwegingen</span><span class="sxs-lookup"><span data-stu-id="ed57d-145">Security considerations</span></span>
<span data-ttu-id="ed57d-146">Gebruikers met toegang toohello externe tabel toegang automatisch toohello onderliggende externe tabellen onder Hallo referentie gegeven in de definitie van Hallo de externe gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="ed57d-146">Users with access toohello external table automatically gain access toohello underlying remote tables under hello credential given in hello external data source definition.</span></span> <span data-ttu-id="ed57d-147">U moet zorgvuldig toegang toohello externe tabel in de volgorde tooavoid ongewenste verhoging van bevoegdheden via Hallo referentie van de externe gegevensbron Hallo beheren.</span><span class="sxs-lookup"><span data-stu-id="ed57d-147">You should carefully manage access toohello external table in order tooavoid undesired elevation of privileges through hello credential of hello external data source.</span></span> <span data-ttu-id="ed57d-148">Reguliere SQL-machtigingen kunnen worden gebruikt tooGRANT of in te trekken toegang tooan externe tabel net alsof het een gewone tabellen.</span><span class="sxs-lookup"><span data-stu-id="ed57d-148">Regular SQL permissions can be used tooGRANT or REVOKE access tooan external table just as though it were a regular table.</span></span>  

## <a name="example-querying-vertically-partitioned-databases"></a><span data-ttu-id="ed57d-149">Voorbeeld: verticaal opvragen gepartitioneerd databases</span><span class="sxs-lookup"><span data-stu-id="ed57d-149">Example: querying vertically partitioned databases</span></span>
<span data-ttu-id="ed57d-150">Hallo volgende query wordt uitgevoerd een join drie richtingen tussen Hallo twee lokale tabellen voor orders en regels en de externe tabel Hallo voor klanten.</span><span class="sxs-lookup"><span data-stu-id="ed57d-150">hello following query performs a three-way join between hello two local tables for orders and order lines and hello remote table for customers.</span></span> <span data-ttu-id="ed57d-151">Dit is een voorbeeld van Hallo verwijzing gegevens gebruiksvoorbeeld voor elastische query:</span><span class="sxs-lookup"><span data-stu-id="ed57d-151">This is an example of hello reference data use case for elastic query:</span></span> 

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


## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a><span data-ttu-id="ed57d-152">Opgeslagen procedure voor uitvoering op afstand T-SQL: sp\_execute_remote</span><span class="sxs-lookup"><span data-stu-id="ed57d-152">Stored procedure for remote T-SQL execution: sp\_execute_remote</span></span>
<span data-ttu-id="ed57d-153">Elastische query bevat ook een opgeslagen procedure die rechtstreekse toegang toohello shards biedt.</span><span class="sxs-lookup"><span data-stu-id="ed57d-153">Elastic query also introduces a stored procedure that provides direct access toohello shards.</span></span> <span data-ttu-id="ed57d-154">Hallo opgeslagen procedure is aangeroepen [sp\_uitvoeren \_externe](https://msdn.microsoft.com/library/mt703714) en kan extern opgeslagen procedures gebruikt tooexecute of T-SQL-code op Hallo externe databases.</span><span class="sxs-lookup"><span data-stu-id="ed57d-154">hello stored procedure is called [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) and can be used tooexecute remote stored procedures or T-SQL code on hello remote databases.</span></span> <span data-ttu-id="ed57d-155">Het duurt Hallo volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="ed57d-155">It takes hello following parameters:</span></span> 

* <span data-ttu-id="ed57d-156">Naam van de gegevensbron (nvarchar): Hallo-naam van de externe gegevensbron Hallo van het type RDBMS.</span><span class="sxs-lookup"><span data-stu-id="ed57d-156">Data source name (nvarchar): hello name of hello external data source of type RDBMS.</span></span> 
* <span data-ttu-id="ed57d-157">Query (nvarchar): Hallo T-SQL-query toobe uitgevoerd op elke shard.</span><span class="sxs-lookup"><span data-stu-id="ed57d-157">Query (nvarchar): hello T-SQL query toobe executed on each shard.</span></span> 
* <span data-ttu-id="ed57d-158">Parameterdeclaratie (nvarchar) - optioneel: de tekenreeks met gegevens typedefinities voor Hallo-parameters die worden gebruikt in de queryparameter hello (zoals sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="ed57d-158">Parameter declaration (nvarchar) - optional: String with data type definitions for hello parameters used in hello Query parameter (like sp_executesql).</span></span> 
* <span data-ttu-id="ed57d-159">Waarde parameterlijst - optioneel: door komma's gescheiden lijst met parameterwaarden (zoals sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="ed57d-159">Parameter value list - optional: Comma-separated list of parameter values (like sp_executesql).</span></span>

<span data-ttu-id="ed57d-160">Hallo sp\_uitvoeren\_maakt gebruik van externe Hallo externe gegevensbron opgegeven in Hallo aanroep parameters tooexecute Hallo gegeven T-SQL-instructie op Hallo externe databases.</span><span class="sxs-lookup"><span data-stu-id="ed57d-160">hello sp\_execute\_remote uses hello external data source provided in hello invocation parameters tooexecute hello given T-SQL statement on hello remote databases.</span></span> <span data-ttu-id="ed57d-161">Hallo-referentie van Hallo externe gegevens tooconnect toohello shardmap manager brondatabase en de externe databases Hallo wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ed57d-161">It uses hello credential of hello external data source tooconnect toohello shardmap manager database and hello remote databases.</span></span>  

<span data-ttu-id="ed57d-162">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="ed57d-162">Example:</span></span> 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 



## <a name="connectivity-for-tools"></a><span data-ttu-id="ed57d-163">Connectiviteit voor hulpprogramma 's</span><span class="sxs-lookup"><span data-stu-id="ed57d-163">Connectivity for tools</span></span>
<span data-ttu-id="ed57d-164">Kunt u reguliere SQL Server-verbinding tekenreeksen tooconnect uw BI en gegevens integratie extra toodatabases op Hallo SQL DB-server waarvoor elastische query ingeschakeld en externe tabellen die zijn gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="ed57d-164">You can use regular SQL Server connection strings tooconnect your BI and data integration tools toodatabases on hello SQL DB server that has elastic query enabled and external tables defined.</span></span> <span data-ttu-id="ed57d-165">Zorg ervoor dat SQL Server wordt ondersteund als een gegevensbron voor het hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="ed57d-165">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="ed57d-166">Raadpleeg toohello elastische query uitvoeren op database en de externe tabellen net als elke andere SQL Server-database dat u verbinding toowith uw hulpprogramma maken wilt.</span><span class="sxs-lookup"><span data-stu-id="ed57d-166">Then refer toohello elastic query database and its external tables just like any other SQL Server database that you would connect toowith your tool.</span></span> 

## <a name="best-practices"></a><span data-ttu-id="ed57d-167">Aanbevolen procedures</span><span class="sxs-lookup"><span data-stu-id="ed57d-167">Best practices</span></span>
* <span data-ttu-id="ed57d-168">Zorg ervoor dat die database Hallo elastische query eindpunt heeft gegeven voor toegang toohello externe database toegang inschakelen voor Azure-Services in de firewall-configuratie van SQL-database.</span><span class="sxs-lookup"><span data-stu-id="ed57d-168">Ensure that hello elastic query endpoint database has been given access toohello remote database by enabling access for Azure Services in its SQL DB firewall configuration.</span></span> <span data-ttu-id="ed57d-169">Zorg er ook voor dat Hallo-referentie opgegeven Hallo externe gegevens brondefinitie is zich bij de externe database Hallo aanmelden kan en Hallo machtigingen tooaccess Hallo externe tabel is.</span><span class="sxs-lookup"><span data-stu-id="ed57d-169">Also ensure that hello credential provided in hello external data source definition can successfully log into hello remote database and has hello permissions tooaccess hello remote table.</span></span>  
* <span data-ttu-id="ed57d-170">Elastische query werkt het beste voor query's waar de meeste Hallo berekening kan worden uitgevoerd op Hallo externe databases.</span><span class="sxs-lookup"><span data-stu-id="ed57d-170">Elastic query works best for queries where most of hello computation can be done on hello remote databases.</span></span> <span data-ttu-id="ed57d-171">U doorgaans ophalen Hallo beste queryprestaties selectief filter predicaten die kan worden geëvalueerd op Hallo externe databases of samenvoegingen die volledig kunnen worden uitgevoerd op de externe database Hallo.</span><span class="sxs-lookup"><span data-stu-id="ed57d-171">You typically get hello best query performance with selective filter predicates that can be evaluated on hello remote databases or joins that can be performed completely on hello remote database.</span></span> <span data-ttu-id="ed57d-172">Andere querypatronen mogelijk grote hoeveelheden gegevens van de externe database Hallo tooload en slecht mag uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="ed57d-172">Other query patterns may need tooload large amounts of data from hello remote database and may perform poorly.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ed57d-173">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ed57d-173">Next steps</span></span>

* <span data-ttu-id="ed57d-174">Zie voor een overzicht van elastische query [elastische query overzicht](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ed57d-174">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="ed57d-175">Zie voor een verticale partitie zelfstudie [aan de slag met cross-databasequery (verticale partities)](sql-database-elastic-query-getting-started-vertical.md).</span><span class="sxs-lookup"><span data-stu-id="ed57d-175">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="ed57d-176">Zie voor een zelfstudie horizontaal partitioneren (sharding) [aan de slag met elastische query voor horizontale partitioneren (sharding)](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="ed57d-176">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="ed57d-177">Zie voor de syntaxis en voorbeelden query's voor horizontaal gepartitioneerde gegevens [gegevens opvragen horizontaal gepartitioneerd)](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="ed57d-177">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="ed57d-178">Zie [sp\_uitvoeren \_externe](https://msdn.microsoft.com/library/mt703714) voor een opgeslagen procedure die een Transact-SQL-instructie op een enkele externe Azure SQL Database of een set van databases die fungeren als shards in een horizontale partitieschema wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ed57d-178">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-vertical-partitioning/verticalpartitioning.png


<!--anchors-->
