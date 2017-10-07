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
# <a name="reporting-across-scaled-out-cloud-databases-preview"></a><span data-ttu-id="5e276-103">Rapportage over cloud uitgebreide databases (preview)</span><span class="sxs-lookup"><span data-stu-id="5e276-103">Reporting across scaled-out cloud databases (preview)</span></span>
![Vragen over shards][1]

<span data-ttu-id="5e276-105">Shard databases rijen verdelen over een uitgebreid uit gegevens die laag.</span><span class="sxs-lookup"><span data-stu-id="5e276-105">Sharded databases distribute rows across a scaled out data tier.</span></span> <span data-ttu-id="5e276-106">Hallo-schema is vrijwel identiek voor alle deelnemende databases, ook wel bekend als horizontaal partitioneren.</span><span class="sxs-lookup"><span data-stu-id="5e276-106">hello schema is identical on all participating databases, also known as horizontal partitioning.</span></span> <span data-ttu-id="5e276-107">Een elastische query gebruiken, kunt u rapporten die alle databases in een shard-database omvatten maken.</span><span class="sxs-lookup"><span data-stu-id="5e276-107">Using an elastic query, you can create reports that span all databases in a sharded database.</span></span>

<span data-ttu-id="5e276-108">Zie voor een snel starten [rapportage over cloud uitgebreide databases](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="5e276-108">For a quick start, see [Reporting across scaled-out cloud databases](sql-database-elastic-query-getting-started.md).</span></span>

<span data-ttu-id="5e276-109">Zie voor niet-shard databases [Query via cloud-databases met verschillende schema's](sql-database-elastic-query-vertical-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="5e276-109">For non-sharded databases, see [Query across cloud databases with different schemas](sql-database-elastic-query-vertical-partitioning.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="5e276-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="5e276-110">Prerequisites</span></span>
* <span data-ttu-id="5e276-111">Maakt een shard-toewijzing met Hallo-clientbibliotheek voor elastische database.</span><span class="sxs-lookup"><span data-stu-id="5e276-111">Create a shard map using hello elastic database client library.</span></span> <span data-ttu-id="5e276-112">Zie [Shard kaart management](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="5e276-112">see [Shard map management](sql-database-elastic-scale-shard-map-management.md).</span></span> <span data-ttu-id="5e276-113">Of gebruik Hallo voorbeeld-app in [aan de slag met hulpprogramma's voor elastische database](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="5e276-113">Or use hello sample app in [Get started with elastic database tools](sql-database-elastic-scale-get-started.md).</span></span>
* <span data-ttu-id="5e276-114">U kunt ook [migreren bestaande databases tooscaled-out-databases](sql-database-elastic-convert-to-use-elastic-tools.md).</span><span class="sxs-lookup"><span data-stu-id="5e276-114">Alternatively, see [Migrate existing databases tooscaled-out databases](sql-database-elastic-convert-to-use-elastic-tools.md).</span></span>
* <span data-ttu-id="5e276-115">Hallo-gebruiker, moet ze beschikken over een externe gegevensbron ALTER machtiging.</span><span class="sxs-lookup"><span data-stu-id="5e276-115">hello user must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="5e276-116">Deze machtiging is opgenomen in de machtiging ALTER DATABASE Hallo.</span><span class="sxs-lookup"><span data-stu-id="5e276-116">This permission is included with hello ALTER DATABASE permission.</span></span>
* <span data-ttu-id="5e276-117">EEN externe gegevensbron ALTER machtigingen zijn vereist toorefer toohello onderliggende gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="5e276-117">ALTER ANY EXTERNAL DATA SOURCE permissions are needed toorefer toohello underlying data source.</span></span>

## <a name="overview"></a><span data-ttu-id="5e276-118">Overzicht</span><span class="sxs-lookup"><span data-stu-id="5e276-118">Overview</span></span>
<span data-ttu-id="5e276-119">Deze instructies maken Hallo metagegevens weergave van de gedeelde gegevenslaag in Hallo elastische query uitvoeren op database.</span><span class="sxs-lookup"><span data-stu-id="5e276-119">These statements create hello metadata representation of your sharded data tier in hello elastic query database.</span></span> 

1. [<span data-ttu-id="5e276-120">CREATE MASTER KEY</span><span class="sxs-lookup"><span data-stu-id="5e276-120">CREATE MASTER KEY</span></span>](https://msdn.microsoft.com/library/ms174382.aspx)
2. [<span data-ttu-id="5e276-121">MAKEN VAN DATABASE-SCOPED REFERENTIE</span><span class="sxs-lookup"><span data-stu-id="5e276-121">CREATE DATABASE SCOPED CREDENTIAL</span></span>](https://msdn.microsoft.com/library/mt270260.aspx)
3. [<span data-ttu-id="5e276-122">EXTERNE GEGEVENSBRON MAKEN</span><span class="sxs-lookup"><span data-stu-id="5e276-122">CREATE EXTERNAL DATA SOURCE</span></span>](https://msdn.microsoft.com/library/dn935022.aspx)
4. [<span data-ttu-id="5e276-123">CREATE EXTERNAL TABLE</span><span class="sxs-lookup"><span data-stu-id="5e276-123">CREATE EXTERNAL TABLE</span></span>](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="11-create-database-scoped-master-key-and-credentials"></a><span data-ttu-id="5e276-124">1.1 bereik databasehoofdsleutel en referenties maken</span><span class="sxs-lookup"><span data-stu-id="5e276-124">1.1 Create database scoped master key and credentials</span></span>
<span data-ttu-id="5e276-125">Hallo-referentie wordt gebruikt door Hallo elastische query tooconnect tooyour externe databases.</span><span class="sxs-lookup"><span data-stu-id="5e276-125">hello credential is used by hello elastic query tooconnect tooyour remote databases.</span></span>  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> <span data-ttu-id="5e276-126">Zorg ervoor dat Hallo *'\<gebruikersnaam\>'* omvat geen *'@servername'* achtervoegsel.</span><span class="sxs-lookup"><span data-stu-id="5e276-126">Make sure that hello *"\<username\>"* does not include any *"@servername"* suffix.</span></span> 
> 
> 

## <a name="12-create-external-data-sources"></a><span data-ttu-id="5e276-127">1.2 externe gegevensbronnen maken</span><span class="sxs-lookup"><span data-stu-id="5e276-127">1.2 Create external data sources</span></span>
<span data-ttu-id="5e276-128">Syntaxis:</span><span class="sxs-lookup"><span data-stu-id="5e276-128">Syntax:</span></span>

    <External_Data_Source> ::=    
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH                                              
            (TYPE = SHARD_MAP_MANAGER,
                       LOCATION = '<fully_qualified_server_name>',
            DATABASE_NAME = ‘<shardmap_database_name>',
            CREDENTIAL = <credential_name>, 
            SHARD_MAP_NAME = ‘<shardmapname>’ 
                   ) [;] 

### <a name="example"></a><span data-ttu-id="5e276-129">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="5e276-129">Example</span></span>
    CREATE EXTERNAL DATA SOURCE MyExtSrc 
    WITH 
    ( 
        TYPE=SHARD_MAP_MANAGER,
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ShardMapDatabase', 
        CREDENTIAL= SMMUser, 
        SHARD_MAP_NAME='ShardMap' 
    );

<span data-ttu-id="5e276-130">Hallo-lijst met huidige externe gegevensbronnen ophalen:</span><span class="sxs-lookup"><span data-stu-id="5e276-130">Retrieve hello list of current external data sources:</span></span> 

    select * from sys.external_data_sources; 

<span data-ttu-id="5e276-131">de externe gegevensbron Hallo verwijst naar de shard-kaart.</span><span class="sxs-lookup"><span data-stu-id="5e276-131">hello external data source references your shard map.</span></span> <span data-ttu-id="5e276-132">Een elastische query gebruikt vervolgens de externe gegevensbron Hallo en onderliggende shard kaart tooenumerate Hallo databases die deel uitmaken van de gegevenslaag Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="5e276-132">An elastic query then uses hello external data source and hello underlying shard map tooenumerate hello databases that participate in hello data tier.</span></span> <span data-ttu-id="5e276-133">Hallo dezelfde referenties zijn gebruikte tooread hello shard-toewijzing en tooaccess gegevens op Hallo shards tijdens de verwerking van een elastische query Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="5e276-133">hello same credentials are used tooread hello shard map and tooaccess hello data on hello shards during hello processing of an elastic query.</span></span> 

## <a name="13-create-external-tables"></a><span data-ttu-id="5e276-134">1.3 externe tabellen maken</span><span class="sxs-lookup"><span data-stu-id="5e276-134">1.3 Create external tables</span></span>
<span data-ttu-id="5e276-135">Syntaxis:</span><span class="sxs-lookup"><span data-stu-id="5e276-135">Syntax:</span></span>  

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name  
        ( { <column_definition> } [ ,...n ])     
        { WITH ( <sharded_external_table_options> ) }
    ) [;]  

    <sharded_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>,       
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 
      DISTRIBUTION = SHARDED(<sharding_column_name>) | REPLICATED |ROUND_ROBIN

<span data-ttu-id="5e276-136">**Voorbeeld**</span><span class="sxs-lookup"><span data-stu-id="5e276-136">**Example**</span></span>

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

<span data-ttu-id="5e276-137">Hallo-lijst met externe tabellen ophalen van de huidige database Hallo:</span><span class="sxs-lookup"><span data-stu-id="5e276-137">Retrieve hello list of external tables from hello current database:</span></span> 

    SELECT * from sys.external_tables; 

<span data-ttu-id="5e276-138">externe tabellen toodrop:</span><span class="sxs-lookup"><span data-stu-id="5e276-138">toodrop external tables:</span></span>

    DROP EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name[;]

### <a name="remarks"></a><span data-ttu-id="5e276-139">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="5e276-139">Remarks</span></span>
<span data-ttu-id="5e276-140">Hallo gegevens\_bron component Hallo externe gegevensbron (een shard-kaart) die wordt gebruikt voor de externe tabel Hallo definieert.</span><span class="sxs-lookup"><span data-stu-id="5e276-140">hello DATA\_SOURCE clause defines hello external data source (a shard map) that is used for hello external table.</span></span>  

<span data-ttu-id="5e276-141">Hallo SCHEMA\_naam en het OBJECT\_naam componenten Hallo externe tabel tooa met tabeldefinitie in een ander schema toewijzen.</span><span class="sxs-lookup"><span data-stu-id="5e276-141">hello SCHEMA\_NAME and OBJECT\_NAME clauses map hello external table definition tooa table in a different schema.</span></span> <span data-ttu-id="5e276-142">Als u dit weglaat, Hallo-schema van Hallo extern object wordt aangenomen dat toobe 'dbo' en de naam ervan wordt uitgegaan van toobe identieke toohello externe tabelnaam wordt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="5e276-142">If omitted, hello schema of hello remote object is assumed toobe “dbo” and its name is assumed toobe identical toohello external table name being defined.</span></span> <span data-ttu-id="5e276-143">Dit is handig als Hallo-naam van de externe tabel is al in gebruik in Hallo-database waar u toocreate Hallo externe tabel.</span><span class="sxs-lookup"><span data-stu-id="5e276-143">This is useful if hello name of your remote table is already taken in hello database where you want toocreate hello external table.</span></span> <span data-ttu-id="5e276-144">Bijvoorbeeld, u wilt dat een externe tabel tooget een samengevoegde weergave van catalogusweergaven toodefine of DMV's voor uw gegevens geschaalde uit laag.</span><span class="sxs-lookup"><span data-stu-id="5e276-144">For  example, you want toodefine an external table tooget an aggregate view of catalog views or DMVs on your scaled out data tier.</span></span> <span data-ttu-id="5e276-145">Aangezien lokaal catalogusweergaven en DMV's bestaat, kunt u hun namen voor de definitie van de externe tabel Hallo niet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5e276-145">Since catalog views and DMVs already exist locally, you cannot use their names for hello external table definition.</span></span> <span data-ttu-id="5e276-146">In plaats daarvan gebruik een andere naam en Hallo catalogusweergave gebruiken of de naam van de DMV in Hallo SCHEMA Hallo\_naam en/of OBJECT\_naam componenten.</span><span class="sxs-lookup"><span data-stu-id="5e276-146">Instead, use a different name and use hello catalog view’s or hello DMV’s name in hello SCHEMA\_NAME and/or OBJECT\_NAME clauses.</span></span> <span data-ttu-id="5e276-147">(Zie onderstaand voorbeeld voor Hallo.)</span><span class="sxs-lookup"><span data-stu-id="5e276-147">(See hello example below.)</span></span> 

<span data-ttu-id="5e276-148">Hallo distributie-component bevat Hallo gegevensdistributie gebruikt voor deze tabel.</span><span class="sxs-lookup"><span data-stu-id="5e276-148">hello DISTRIBUTION clause specifies hello data distribution used for this table.</span></span> <span data-ttu-id="5e276-149">Hallo-queryprocessor Hallo informatie in Hallo distributie component toobuild Hallo meest efficiënt queryplannen wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5e276-149">hello query processor utilizes hello information provided in hello DISTRIBUTION clause toobuild hello most efficient query plans.</span></span>  

1. <span data-ttu-id="5e276-150">**SHARD** betekent dat gegevens horizontaal over Hallo databases is gepartitioneerd.</span><span class="sxs-lookup"><span data-stu-id="5e276-150">**SHARDED** means data is horizontally partitioned across hello databases.</span></span> <span data-ttu-id="5e276-151">Hallo partitiesleutel voor Hallo gegevensdistributie Hallo is **< sharding_column_name >** parameter.</span><span class="sxs-lookup"><span data-stu-id="5e276-151">hello partitioning key for hello data distribution is hello **<sharding_column_name>** parameter.</span></span>
2. <span data-ttu-id="5e276-152">**GEREPLICEERD** betekent dat identieke kopieën van Hallo tabel aanwezig op elke database zijn.</span><span class="sxs-lookup"><span data-stu-id="5e276-152">**REPLICATED** means that identical copies of hello table are present on each database.</span></span> <span data-ttu-id="5e276-153">Het is uw verantwoordelijkheid tooensure Hallo replica's zijn identiek voor Hallo-databases.</span><span class="sxs-lookup"><span data-stu-id="5e276-153">It is your responsibility tooensure that hello replicas are identical across hello databases.</span></span>
3. <span data-ttu-id="5e276-154">**RONDE\_ROBIN** betekent die tabel Hallo horizontaal is gepartitioneerd met behulp van een distributiemethode van afhankelijk zijn van toepassing.</span><span class="sxs-lookup"><span data-stu-id="5e276-154">**ROUND\_ROBIN** means that hello table is horizontally partitioned using an application-dependent distribution method.</span></span> 

<span data-ttu-id="5e276-155">**Gegevens servicetier verwijzing**: Hallo externe tabel DDL verwijst tooan externe gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="5e276-155">**Data tier reference**: hello external table DDL refers tooan external data source.</span></span> <span data-ttu-id="5e276-156">de externe gegevensbron Hallo geeft een shard-toewijzing die externe tabel Hallo Hallo informatie nodig toolocate alle Hallo-databases in de gegevenslaag biedt.</span><span class="sxs-lookup"><span data-stu-id="5e276-156">hello external data source specifies a shard map which provides hello external table with hello information necessary toolocate all hello databases in your data tier.</span></span> 

### <a name="security-considerations"></a><span data-ttu-id="5e276-157">Beveiligingsoverwegingen</span><span class="sxs-lookup"><span data-stu-id="5e276-157">Security considerations</span></span>
<span data-ttu-id="5e276-158">Gebruikers met toegang toohello externe tabel toegang automatisch toohello onderliggende externe tabellen onder Hallo referentie gegeven in de definitie van Hallo de externe gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="5e276-158">Users with access toohello external table automatically gain access toohello underlying remote tables under hello credential given in hello external data source definition.</span></span> <span data-ttu-id="5e276-159">Vermijd ongewenste verhoging van bevoegdheden via Hallo referentie van de externe gegevensbron Hallo.</span><span class="sxs-lookup"><span data-stu-id="5e276-159">Avoid undesired elevation of privileges through hello credential of hello external data source.</span></span> <span data-ttu-id="5e276-160">Gebruik GRANT of REVOKE voor een externe tabel net alsof het een gewone tabellen.</span><span class="sxs-lookup"><span data-stu-id="5e276-160">Use GRANT or REVOKE for an external table just as though it were a regular table.</span></span>  

<span data-ttu-id="5e276-161">Nadat u uw externe gegevensbron en uw externe tabellen hebt gedefinieerd, kunt u nu volledige T-SQL gebruiken via uw externe tabellen.</span><span class="sxs-lookup"><span data-stu-id="5e276-161">Once you have defined your external data source and your external tables, you can now use full T-SQL over your external tables.</span></span>

## <a name="example-querying-horizontal-partitioned-databases"></a><span data-ttu-id="5e276-162">Voorbeeld: uitvoeren van query's horizontale gepartitioneerde databases</span><span class="sxs-lookup"><span data-stu-id="5e276-162">Example: querying horizontal partitioned databases</span></span>
<span data-ttu-id="5e276-163">Hallo volgende query voert een koppeling drie richtingen tussen datawarehouses, orders en regels en maakt gebruik van verschillende statistische functies en een selectieve filter.</span><span class="sxs-lookup"><span data-stu-id="5e276-163">hello following query performs a three-way join between warehouses, orders and order lines and uses several aggregates and a selective filter.</span></span> <span data-ttu-id="5e276-164">Er wordt vanuit gegaan (1) de horizontale partitionering (sharding) en (2) worden in datawarehouses, orders en regels shard Hallo datawarehouse-id-kolom zijn en die Hallo elastische query kunt plaatsen Hallo joins op Hallo shards en Hallo dure deel van Hallo-query op Hallo verwerken shards parallel.</span><span class="sxs-lookup"><span data-stu-id="5e276-164">It assumes (1) horizontal partitioning (sharding) and (2) that warehouses, orders and order lines are sharded by hello warehouse id column, and that hello elastic query can co-locate hello joins on hello shards and process hello expensive part of hello query on hello shards in parallel.</span></span> 

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

## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a><span data-ttu-id="5e276-165">Opgeslagen procedure voor uitvoering op afstand T-SQL: sp\_execute_remote</span><span class="sxs-lookup"><span data-stu-id="5e276-165">Stored procedure for remote T-SQL execution: sp\_execute_remote</span></span>
<span data-ttu-id="5e276-166">Elastische query bevat ook een opgeslagen procedure die rechtstreekse toegang toohello shards biedt.</span><span class="sxs-lookup"><span data-stu-id="5e276-166">Elastic query also introduces a stored procedure that provides direct access toohello shards.</span></span> <span data-ttu-id="5e276-167">Hallo opgeslagen procedure is aangeroepen [sp\_uitvoeren \_externe](https://msdn.microsoft.com/library/mt703714) en kan extern opgeslagen procedures gebruikt tooexecute of T-SQL-code op Hallo externe databases.</span><span class="sxs-lookup"><span data-stu-id="5e276-167">hello stored procedure is called [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) and can be used tooexecute remote stored procedures or T-SQL code on hello remote databases.</span></span> <span data-ttu-id="5e276-168">Het duurt Hallo volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="5e276-168">It takes hello following parameters:</span></span> 

* <span data-ttu-id="5e276-169">Naam van de gegevensbron (nvarchar): Hallo-naam van de externe gegevensbron Hallo van het type RDBMS.</span><span class="sxs-lookup"><span data-stu-id="5e276-169">Data source name (nvarchar): hello name of hello external data source of type RDBMS.</span></span> 
* <span data-ttu-id="5e276-170">Query (nvarchar): Hallo T-SQL-query toobe uitgevoerd op elke shard.</span><span class="sxs-lookup"><span data-stu-id="5e276-170">Query (nvarchar): hello T-SQL query toobe executed on each shard.</span></span> 
* <span data-ttu-id="5e276-171">Parameterdeclaratie (nvarchar) - optioneel: de tekenreeks met gegevens typedefinities voor Hallo-parameters die worden gebruikt in de queryparameter hello (zoals sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="5e276-171">Parameter declaration (nvarchar) - optional: String with data type definitions for hello parameters used in hello Query parameter (like sp_executesql).</span></span> 
* <span data-ttu-id="5e276-172">Waarde parameterlijst - optioneel: door komma's gescheiden lijst met parameterwaarden (zoals sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="5e276-172">Parameter value list - optional: Comma-separated list of parameter values (like sp_executesql).</span></span>

<span data-ttu-id="5e276-173">Hallo sp\_uitvoeren\_maakt gebruik van externe Hallo externe gegevensbron opgegeven in Hallo aanroep parameters tooexecute Hallo gegeven T-SQL-instructie op Hallo externe databases.</span><span class="sxs-lookup"><span data-stu-id="5e276-173">hello sp\_execute\_remote uses hello external data source provided in hello invocation parameters tooexecute hello given T-SQL statement on hello remote databases.</span></span> <span data-ttu-id="5e276-174">Hallo-referentie van Hallo externe gegevens tooconnect toohello shardmap manager brondatabase en de externe databases Hallo wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5e276-174">It uses hello credential of hello external data source tooconnect toohello shardmap manager database and hello remote databases.</span></span>  

<span data-ttu-id="5e276-175">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="5e276-175">Example:</span></span> 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 

## <a name="connectivity-for-tools"></a><span data-ttu-id="5e276-176">Connectiviteit voor hulpprogramma 's</span><span class="sxs-lookup"><span data-stu-id="5e276-176">Connectivity for tools</span></span>
<span data-ttu-id="5e276-177">Reguliere tekenreeksen tooconnect van de SQL Server-verbinding gebruiken uw toepassing, uw database BI en gegevens integratie extra toohello met de definities van de externe tabel.</span><span class="sxs-lookup"><span data-stu-id="5e276-177">Use regular SQL Server connection strings tooconnect your application, your BI and data integration tools toohello database with your external table definitions.</span></span> <span data-ttu-id="5e276-178">Zorg ervoor dat SQL Server wordt ondersteund als een gegevensbron voor het hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="5e276-178">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="5e276-179">Vervolgens verwijzen naar Hallo elastische query uitvoeren op database zoals een ander SQL Server-database verbonden toohello hulpprogramma en externe tabellen vanuit uw hulpprogramma of toepassing gebruiken alsof ze lokaal tabellen.</span><span class="sxs-lookup"><span data-stu-id="5e276-179">Then reference hello elastic query database like any other SQL Server database connected toohello tool, and use external tables from your tool or application as if they were local tables.</span></span> 

## <a name="best-practices"></a><span data-ttu-id="5e276-180">Aanbevolen procedures</span><span class="sxs-lookup"><span data-stu-id="5e276-180">Best practices</span></span>
* <span data-ttu-id="5e276-181">Zorg ervoor dat die database Hallo elastische query eindpunt access toohello shardmap-database en alle shards via SQL DB firewalls Hallo heeft gekregen.</span><span class="sxs-lookup"><span data-stu-id="5e276-181">Ensure that hello elastic query endpoint database has been given access toohello shardmap database and all shards through hello SQL DB firewalls.</span></span>  
* <span data-ttu-id="5e276-182">Valideren of Hallo gegevensdistributie gedefinieerd door de externe tabel Hallo af te dwingen.</span><span class="sxs-lookup"><span data-stu-id="5e276-182">Validate or enforce hello data distribution defined by hello external table.</span></span> <span data-ttu-id="5e276-183">Als uw werkelijke gegevensdistributie van het Hallo-distributiepunt opgegeven in de tabeldefinitie van de verschilt, kan uw query's kunnen onverwachte resultaten opleveren.</span><span class="sxs-lookup"><span data-stu-id="5e276-183">If your actual data distribution is different from hello distribution specified in your table definition, your queries may yield unexpected results.</span></span> 
* <span data-ttu-id="5e276-184">Elastische query momenteel geen uit shard elimineren wanneer predicaten Hallo sharding sleutel zou toe te staan toosafely uitsluiten bepaalde shards van verwerken.</span><span class="sxs-lookup"><span data-stu-id="5e276-184">Elastic query currently does not perform shard elimination when predicates over hello sharding key would allow it toosafely exclude certain shards from processing.</span></span>
* <span data-ttu-id="5e276-185">Elastische query werkt het beste voor query's waar de meeste Hallo berekening op Hallo shards kan worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5e276-185">Elastic query works best for queries where most of hello computation can be done on hello shards.</span></span> <span data-ttu-id="5e276-186">U doorgaans ophalen Hallo beste queryprestaties selectief filter predicaten die kan worden geëvalueerd op Hallo shards of joins via Hallo sleutels die kunnen worden uitgevoerd op een manier uitgelijnd op alle shards.</span><span class="sxs-lookup"><span data-stu-id="5e276-186">You typically get hello best query performance with selective filter predicates that can be evaluated on hello shards or joins over hello partitioning keys that can be performed in a partition-aligned way on all shards.</span></span> <span data-ttu-id="5e276-187">Andere querypatronen mogelijk grote hoeveelheden gegevens van Hallo shards toohello hoofdknooppunt tooload en slecht mag uitvoeren</span><span class="sxs-lookup"><span data-stu-id="5e276-187">Other query patterns may need tooload large amounts of data from hello shards toohello head node and may perform poorly</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e276-188">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5e276-188">Next steps</span></span>

* <span data-ttu-id="5e276-189">Zie voor een overzicht van elastische query [elastische query overzicht](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5e276-189">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="5e276-190">Zie voor een verticale partitie zelfstudie [aan de slag met cross-databasequery (verticale partities)](sql-database-elastic-query-getting-started-vertical.md).</span><span class="sxs-lookup"><span data-stu-id="5e276-190">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="5e276-191">Zie voor de syntaxis en voorbeelden query's voor verticaal gepartitioneerde gegevens [gegevens opvragen verticaal gepartitioneerd)](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="5e276-191">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="5e276-192">Zie voor een zelfstudie horizontaal partitioneren (sharding) [aan de slag met elastische query voor horizontale partitioneren (sharding)](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="5e276-192">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="5e276-193">Zie [sp\_uitvoeren \_externe](https://msdn.microsoft.com/library/mt703714) voor een opgeslagen procedure die een Transact-SQL-instructie op een enkele externe Azure SQL Database of een set van databases die fungeren als shards in een horizontale partitieschema wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5e276-193">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-horizontal-partitioning/horizontalpartitioning.png
<!--anchors-->
