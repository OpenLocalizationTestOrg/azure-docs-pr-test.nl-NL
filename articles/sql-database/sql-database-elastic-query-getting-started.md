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
# <a name="report-across-scaled-out-cloud-databases-preview"></a><span data-ttu-id="c6b17-103">Rapport over cloud uitgebreide databases (preview)</span><span class="sxs-lookup"><span data-stu-id="c6b17-103">Report across scaled-out cloud databases (preview)</span></span>
<span data-ttu-id="c6b17-104">U kunt rapporten maken uit meerdere Azure SQL-databases vanuit een enkele verbinding punt met een [elastische query](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c6b17-104">You can create reports from multiple Azure SQL databases from a single connection point using an [elastic query](sql-database-elastic-query-overview.md).</span></span> <span data-ttu-id="c6b17-105">Hallo-databases worden horizontaal gepartitioneerd (ook wel bekend als 'shard').</span><span class="sxs-lookup"><span data-stu-id="c6b17-105">hello databases must be horizontally partitioned (also known as "sharded").</span></span>

<span data-ttu-id="c6b17-106">Als u een bestaande database hebt, raadpleegt u [migreren bestaande databases tooscaled-out-databases](sql-database-elastic-convert-to-use-elastic-tools.md).</span><span class="sxs-lookup"><span data-stu-id="c6b17-106">If you have an existing database, see [Migrating existing databases tooscaled-out databases](sql-database-elastic-convert-to-use-elastic-tools.md).</span></span>

<span data-ttu-id="c6b17-107">toounderstand hello SQL-objecten die nodig zijn tooquery, Zie [Query over horizontaal gepartitioneerde databases](sql-database-elastic-query-horizontal-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="c6b17-107">toounderstand hello SQL objects needed tooquery, see [Query across horizontally partitioned databases](sql-database-elastic-query-horizontal-partitioning.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c6b17-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c6b17-108">Prerequisites</span></span>
<span data-ttu-id="c6b17-109">Downloaden en uitvoeren van Hallo [aan de slag met elastische Database extra voorbeeld](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c6b17-109">Download and run hello [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="create-a-shard-map-manager-using-hello-sample-app"></a><span data-ttu-id="c6b17-110">Een shard-toewijzing manager met Hallo voorbeeld-app maken</span><span class="sxs-lookup"><span data-stu-id="c6b17-110">Create a shard map manager using hello sample app</span></span>
<span data-ttu-id="c6b17-111">Hier maakt u een shard-toewijzing manager samen met enkele shards, gevolgd door het invoegen van gegevens in Hallo shards.</span><span class="sxs-lookup"><span data-stu-id="c6b17-111">Here you will create a shard map manager along with several shards, followed by insertion of data into hello shards.</span></span> <span data-ttu-id="c6b17-112">Als u per ongeluk tooalready shards setup met gedeelde gegevens zich bevinden, kunt u Hallo stappen overslaan en de volgende sectie toohello verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="c6b17-112">If you happen tooalready have shards setup with sharded data in them, you can skip hello following steps and move toohello next section.</span></span>

1. <span data-ttu-id="c6b17-113">Bouwen en uitvoeren van Hallo **aan de slag met hulpprogramma's voor elastische Database** voorbeeldtoepassing.</span><span class="sxs-lookup"><span data-stu-id="c6b17-113">Build and run hello **Getting started with Elastic Database tools** sample application.</span></span> <span data-ttu-id="c6b17-114">Hallo stappen tot stap 7 in de sectie Hallo [Hallo voorbeeld-app downloaden en uitvoeren](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span><span class="sxs-lookup"><span data-stu-id="c6b17-114">Follow hello steps until step 7 in hello section [Download and run hello sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span></span> <span data-ttu-id="c6b17-115">Aan het einde van de Hallo van stap 7 ziet u Hallo na de opdrachtprompt:</span><span class="sxs-lookup"><span data-stu-id="c6b17-115">At hello end of Step 7, you will see hello following command prompt:</span></span>

    ![opdrachtprompt][1]
2. <span data-ttu-id="c6b17-117">In het opdrachtvenster hello, typ '1' en druk op **Enter**.</span><span class="sxs-lookup"><span data-stu-id="c6b17-117">In hello command window, type "1" and press **Enter**.</span></span> <span data-ttu-id="c6b17-118">Dit maakt Hallo shard-toewijzing manager en voegt u twee shards toohello-server.</span><span class="sxs-lookup"><span data-stu-id="c6b17-118">This creates hello shard map manager, and adds two shards toohello server.</span></span> <span data-ttu-id="c6b17-119">Vervolgens typt u "3" en druk op **Enter**; Hallo actie vier keer herhalen.</span><span class="sxs-lookup"><span data-stu-id="c6b17-119">Then type "3" and press **Enter**; repeat hello action four times.</span></span> <span data-ttu-id="c6b17-120">Dit invoegen voorbeeld gegevensrijen in uw shards.</span><span class="sxs-lookup"><span data-stu-id="c6b17-120">This inserts sample data rows in your shards.</span></span>
3. <span data-ttu-id="c6b17-121">Hallo [Azure-portal](https://portal.azure.com) moet drie nieuwe databases worden weergegeven in de server:</span><span class="sxs-lookup"><span data-stu-id="c6b17-121">hello [Azure portal](https://portal.azure.com) should show three new databases in your server:</span></span>

   ![Visual Studio-bevestiging][2]

   <span data-ttu-id="c6b17-123">Cross-databasequery's worden op dit moment ondersteund via Hallo elastische Database clientbibliotheken.</span><span class="sxs-lookup"><span data-stu-id="c6b17-123">At this point, cross-database queries are supported through hello Elastic Database client libraries.</span></span> <span data-ttu-id="c6b17-124">Gebruik bijvoorbeeld optie 4 in Hallo-opdrachtvenster.</span><span class="sxs-lookup"><span data-stu-id="c6b17-124">For example, use option 4 in hello command window.</span></span> <span data-ttu-id="c6b17-125">Hallo-resultaten van een query meerdere shard zijn altijd een **UNION ALL** van Hallo resultaten van alle shards.</span><span class="sxs-lookup"><span data-stu-id="c6b17-125">hello results from a multi-shard query are always a **UNION ALL** of hello results from all shards.</span></span>

   <span data-ttu-id="c6b17-126">In de volgende sectie hello maken we een voorbeeld database eindpunt die ondersteuning biedt voor uitgebreide query Hallo gegevens over shards.</span><span class="sxs-lookup"><span data-stu-id="c6b17-126">In hello next section, we create a sample database endpoint that supports richer querying of hello data across shards.</span></span>

## <a name="create-an-elastic-query-database"></a><span data-ttu-id="c6b17-127">Een voor elastische querydatabase maken</span><span class="sxs-lookup"><span data-stu-id="c6b17-127">Create an elastic query database</span></span>
1. <span data-ttu-id="c6b17-128">Open Hallo [Azure-portal](https://portal.azure.com) en zich aanmelden.</span><span class="sxs-lookup"><span data-stu-id="c6b17-128">Open hello [Azure portal](https://portal.azure.com) and log in.</span></span>
2. <span data-ttu-id="c6b17-129">Maak een nieuwe Azure SQL-database in Hallo dezelfde server als de shard-instellingen.</span><span class="sxs-lookup"><span data-stu-id="c6b17-129">Create a new Azure SQL database in hello same server as your shard setup.</span></span> <span data-ttu-id="c6b17-130">Naam Hallo database 'ElasticDBQuery'.</span><span class="sxs-lookup"><span data-stu-id="c6b17-130">Name hello database "ElasticDBQuery."</span></span>

    ![Azure-portal en de prijscategorie][3]

    > [!NOTE]
    > <span data-ttu-id="c6b17-132">u kunt een bestaande database gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c6b17-132">you can use an existing database.</span></span> <span data-ttu-id="c6b17-133">Als u doet dit, niet moet een Hallo shards dat u tooexecute wilt uw query's op.</span><span class="sxs-lookup"><span data-stu-id="c6b17-133">If you can do so, it must not be one of hello shards that you would like tooexecute your queries on.</span></span> <span data-ttu-id="c6b17-134">Deze database wordt gebruikt voor het maken van Hallo van metagegevensobjecten voor een elastische database-query.</span><span class="sxs-lookup"><span data-stu-id="c6b17-134">This database will be used for creating hello metadata objects for an elastic database query.</span></span>
    >

## <a name="create-database-objects"></a><span data-ttu-id="c6b17-135">Database-objecten maken</span><span class="sxs-lookup"><span data-stu-id="c6b17-135">Create database objects</span></span>
### <a name="database-scoped-master-key-and-credentials"></a><span data-ttu-id="c6b17-136">Database-scoped hoofdsleutel en referenties</span><span class="sxs-lookup"><span data-stu-id="c6b17-136">Database-scoped master key and credentials</span></span>
<span data-ttu-id="c6b17-137">Dit zijn de gebruikte tooconnect toohello shard kaart manager en Hallo shards:</span><span class="sxs-lookup"><span data-stu-id="c6b17-137">These are used tooconnect toohello shard map manager and hello shards:</span></span>

1. <span data-ttu-id="c6b17-138">Open SQL Server Management Studio of SQL Server Data Tools in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c6b17-138">Open SQL Server Management Studio or SQL Server Data Tools in Visual Studio.</span></span>
2. <span data-ttu-id="c6b17-139">Verbinding maken met database tooElasticDBQuery en Hallo volgende T-SQL-opdrachten uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="c6b17-139">Connect tooElasticDBQuery database and execute hello following T-SQL commands:</span></span>

        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred
        WITH IDENTITY = '<username>',
        SECRET = '<password>';

    <span data-ttu-id="c6b17-140">'gebruikersnaam' en 'password' moet worden Hallo dezelfde als de aanmeldingsgegevens die zijn gebruikt in stap 6 van [Hallo voorbeeld-app downloaden en uitvoeren](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app) in [aan de slag met hulpprogramma's voor elastische database](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c6b17-140">"username" and "password" should be hello same as login information used in step 6 of [Download and run hello sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app) in [Getting started with elastic database tools](sql-database-elastic-scale-get-started.md).</span></span>

### <a name="external-data-sources"></a><span data-ttu-id="c6b17-141">Externe gegevensbronnen</span><span class="sxs-lookup"><span data-stu-id="c6b17-141">External data sources</span></span>
<span data-ttu-id="c6b17-142">een externe gegevensbron toocreate Hallo volgende opdracht uit op Hallo ElasticDBQuery database uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="c6b17-142">toocreate an external data source, execute hello following command on hello ElasticDBQuery database:</span></span>

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH
      (TYPE = SHARD_MAP_MANAGER,
      LOCATION = '<server_name>.database.windows.net',
      DATABASE_NAME = 'ElasticScaleStarterKit_ShardMapManagerDb',
      CREDENTIAL = ElasticDBQueryCred,
       SHARD_MAP_NAME = 'CustomerIDShardMap'
    ) ;

 <span data-ttu-id="c6b17-143">'CustomerIDShardMap' hello naam is van Hallo shard-kaart, als u hebt gemaakt Hallo shard-toewijzing en shard-toewijzing manager tools-voorbeeld gebruikt Hallo elastische database.</span><span class="sxs-lookup"><span data-stu-id="c6b17-143">"CustomerIDShardMap" is hello name of hello shard map, if you created hello shard map and shard map manager using hello elastic database tools sample.</span></span> <span data-ttu-id="c6b17-144">Als u uw aangepaste instellingen voor dit voorbeeld gebruikt, klikt u vervolgens moet het echter Hallo shard-toewijzingsnaam die u hebt gekozen in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="c6b17-144">However, if you used your custom setup for this sample, then it should be hello shard map name you chose in your application.</span></span>

### <a name="external-tables"></a><span data-ttu-id="c6b17-145">Externe tabellen</span><span class="sxs-lookup"><span data-stu-id="c6b17-145">External tables</span></span>
<span data-ttu-id="c6b17-146">Een externe tabel die overeenkomt met Hallo klantentabel op Hallo shards door het uitvoeren van de volgende opdracht uit op ElasticDBQuery database Hallo maken:</span><span class="sxs-lookup"><span data-stu-id="c6b17-146">Create an external table that matches hello Customers table on hello shards by executing hello following command on ElasticDBQuery database:</span></span>

    CREATE EXTERNAL TABLE [dbo].[Customers]
    ( [CustomerId] [int] NOT NULL,
      [Name] [nvarchar](256) NOT NULL,
      [RegionId] [int] NOT NULL)
    WITH
    ( DATA_SOURCE = MyElasticDBQueryDataSrc,
      DISTRIBUTION = SHARDED([CustomerId])
    ) ;

## <a name="execute-a-sample-elastic-database-t-sql-query"></a><span data-ttu-id="c6b17-147">Een voorbeeld elastische database T-SQL-query uitvoeren</span><span class="sxs-lookup"><span data-stu-id="c6b17-147">Execute a sample elastic database T-SQL query</span></span>
<span data-ttu-id="c6b17-148">U kunt nu volledige T-SQL gebruiken via uw externe tabellen, nadat u uw externe gegevensbron en uw externe tabellen hebt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="c6b17-148">Once you have defined your external data source and your external tables you can now use full T-SQL over your external tables.</span></span>

<span data-ttu-id="c6b17-149">Voer deze query uit op Hallo ElasticDBQuery database:</span><span class="sxs-lookup"><span data-stu-id="c6b17-149">Execute this query on hello ElasticDBQuery database:</span></span>

    select count(CustomerId) from [dbo].[Customers]

<span data-ttu-id="c6b17-150">U zult die query Hallo cumuleert de resultaten van alle Hallo shards en geeft Hallo volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="c6b17-150">You will notice that hello query aggregates results from all hello shards and gives hello following output:</span></span>

![Uitvoerdetails][4]

## <a name="import-elastic-database-query-results-tooexcel"></a><span data-ttu-id="c6b17-152">Elastische database query resultaten tooExcel importeren</span><span class="sxs-lookup"><span data-stu-id="c6b17-152">Import elastic database query results tooExcel</span></span>
 <span data-ttu-id="c6b17-153">U kunt Hallo resultaten uit van een query tooan Excel-bestand importeren.</span><span class="sxs-lookup"><span data-stu-id="c6b17-153">You can import hello results from of a query tooan Excel file.</span></span>

1. <span data-ttu-id="c6b17-154">Start Excel 2013.</span><span class="sxs-lookup"><span data-stu-id="c6b17-154">Launch Excel 2013.</span></span>
2. <span data-ttu-id="c6b17-155">Navigeer toohello **gegevens** lint.</span><span class="sxs-lookup"><span data-stu-id="c6b17-155">Navigate toohello **Data** ribbon.</span></span>
3. <span data-ttu-id="c6b17-156">Klik op **van andere bronnen** en klik op **van SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="c6b17-156">Click **From Other Sources** and click **From SQL Server**.</span></span>

   ![Excel importeren uit andere bronnen][5]
4. <span data-ttu-id="c6b17-158">In Hallo **Wizard Gegevensverbinding** Typ Hallo server servernaam en aanmeldingsreferenties.</span><span class="sxs-lookup"><span data-stu-id="c6b17-158">In hello **Data Connection Wizard** type hello server name and login credentials.</span></span> <span data-ttu-id="c6b17-159">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="c6b17-159">Then click **Next**.</span></span>
5. <span data-ttu-id="c6b17-160">In het dialoogvenster Hallo **Selecteer Hallo-database met Hallo gegevens die u wilt**, selecteer Hallo **ElasticDBQuery** database.</span><span class="sxs-lookup"><span data-stu-id="c6b17-160">In hello dialog box **Select hello database that contains hello data you want**, select hello **ElasticDBQuery** database.</span></span>
6. <span data-ttu-id="c6b17-161">Selecteer Hallo **klanten** tabel in de lijstweergave Hallo en klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="c6b17-161">Select hello **Customers** table in hello list view and click **Next**.</span></span> <span data-ttu-id="c6b17-162">Klik vervolgens op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="c6b17-162">Then click **Finish**.</span></span>
7. <span data-ttu-id="c6b17-163">In Hallo **importgegevens** formulier onder **Selecteer hoe u tooview deze gegevens in uw werkmap**, selecteer **tabel** en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="c6b17-163">In hello **Import Data** form, under **Select how you want tooview this data in your workbook**, select **Table** and click **OK**.</span></span>

<span data-ttu-id="c6b17-164">Alle rijen uit Hallo **klanten** tabel, opgeslagen in verschillende shards vullen Hallo Excel-werkblad.</span><span class="sxs-lookup"><span data-stu-id="c6b17-164">All hello rows from **Customers** table, stored in different shards populate hello Excel sheet.</span></span>

<span data-ttu-id="c6b17-165">Nu kunt u krachtige gegevensfuncties visualisatie van Excel.</span><span class="sxs-lookup"><span data-stu-id="c6b17-165">You can now use Excel’s powerful data visualization functions.</span></span> <span data-ttu-id="c6b17-166">U kunt Hallo verbindingsreeks gebruiken met de naam van uw server, databasenaam en referenties tooconnect uw BI en gegevens integratie extra toohello elastische query uitvoeren op database.</span><span class="sxs-lookup"><span data-stu-id="c6b17-166">You can use hello connection string with your server name, database name and credentials tooconnect your BI and data integration tools toohello elastic query database.</span></span> <span data-ttu-id="c6b17-167">Zorg ervoor dat SQL Server wordt ondersteund als een gegevensbron voor het hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="c6b17-167">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="c6b17-168">U kunt toohello elastische query uitvoeren op database en de externe tabellen net als elke andere SQL Server-database en SQL Server-tabellen die u wilt verbinding maken toowith uw hulpprogramma verwijzen.</span><span class="sxs-lookup"><span data-stu-id="c6b17-168">You can refer toohello elastic query database and external tables just like any other SQL Server database and SQL Server tables that you would connect toowith your tool.</span></span>

### <a name="cost"></a><span data-ttu-id="c6b17-169">Kosten</span><span class="sxs-lookup"><span data-stu-id="c6b17-169">Cost</span></span>
<span data-ttu-id="c6b17-170">Er zijn geen extra kosten voor het gebruik van Hallo elastische databasequery functie.</span><span class="sxs-lookup"><span data-stu-id="c6b17-170">There is no additional charge for using hello Elastic Database Query feature.</span></span>

<span data-ttu-id="c6b17-171">Zie voor informatie over prijzen [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="c6b17-171">For pricing information see [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6b17-172">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c6b17-172">Next steps</span></span>

* <span data-ttu-id="c6b17-173">Zie voor een overzicht van elastische query [elastische query overzicht](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c6b17-173">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="c6b17-174">Zie voor een verticale partitie zelfstudie [aan de slag met cross-databasequery (verticale partities)](sql-database-elastic-query-getting-started-vertical.md).</span><span class="sxs-lookup"><span data-stu-id="c6b17-174">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="c6b17-175">Zie voor de syntaxis en voorbeelden query's voor verticaal gepartitioneerde gegevens [gegevens opvragen verticaal gepartitioneerd)](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="c6b17-175">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="c6b17-176">Zie voor de syntaxis en voorbeelden query's voor horizontaal gepartitioneerde gegevens [gegevens opvragen horizontaal gepartitioneerd)](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="c6b17-176">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="c6b17-177">Zie [sp\_uitvoeren \_externe](https://msdn.microsoft.com/library/mt703714) voor een opgeslagen procedure die een Transact-SQL-instructie op een enkele externe Azure SQL Database of een set van databases die fungeren als shards in een horizontale partitieschema wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c6b17-177">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
