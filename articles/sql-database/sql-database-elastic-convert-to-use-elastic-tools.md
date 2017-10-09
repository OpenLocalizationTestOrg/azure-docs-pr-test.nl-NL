---
title: aaaMigrate bestaande databases tooscale-out | Microsoft Docs
description: Converteren van hulpprogramma's shard databases toouse elastische database door het maken van een manager shard-kaart
services: sql-database
documentationcenter: 
author: ddove
manager: jhubbard
editor: 
ms.assetid: 8c851d8e-8fd5-4327-89c1-9178b20ddd69
ms.service: sql-database
ms.custom: scale out apps
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: fa2c9e3699f30667cf547d1faadf4504609199be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-existing-databases-tooscale-out"></a><span data-ttu-id="9928e-103">Migreren van bestaande databases tooscale-out</span><span class="sxs-lookup"><span data-stu-id="9928e-103">Migrate existing databases tooscale-out</span></span>
<span data-ttu-id="9928e-104">Uw bestaande uitgebreid shard databases met hulpprogramma's van Azure SQL Database database eenvoudig te beheren (zoals Hallo [clientbibliotheek voor elastische Database](sql-database-elastic-database-client-library.md)).</span><span class="sxs-lookup"><span data-stu-id="9928e-104">Easily manage your existing scaled-out sharded databases using Azure SQL Database database tools (such as hello [Elastic Database client library](sql-database-elastic-database-client-library.md)).</span></span> <span data-ttu-id="9928e-105">U moet eerst een bestaande set van databases toouse Hallo converteren [shard kaart manager](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="9928e-105">You must first convert an existing set of databases toouse hello [shard map manager](sql-database-elastic-scale-shard-map-management.md).</span></span> 

## <a name="overview"></a><span data-ttu-id="9928e-106">Overzicht</span><span class="sxs-lookup"><span data-stu-id="9928e-106">Overview</span></span>
<span data-ttu-id="9928e-107">een bestaande database in de shard toomigrate:</span><span class="sxs-lookup"><span data-stu-id="9928e-107">toomigrate an existing sharded database:</span></span> 

1. <span data-ttu-id="9928e-108">Hallo voorbereiden [shard-toewijzing manager-database](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="9928e-108">Prepare hello [shard map manager database](sql-database-elastic-scale-shard-map-management.md).</span></span>
2. <span data-ttu-id="9928e-109">Hallo shard-toewijzing worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9928e-109">Create hello shard map.</span></span>
3. <span data-ttu-id="9928e-110">Bereid Hallo afzonderlijke shards.</span><span class="sxs-lookup"><span data-stu-id="9928e-110">Prepare hello individual shards.</span></span>  
4. <span data-ttu-id="9928e-111">Toewijzingen toohello shard-toewijzing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="9928e-111">Add mappings toohello shard map.</span></span>

<span data-ttu-id="9928e-112">Deze technieken kunnen worden geïmplementeerd met de Hallo [clientbibliotheek voor .NET Framework](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/), of de PowerShell-scripts Hallo gevonden op [Azure SQL DB - elastische Database extra scripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="9928e-112">These techniques can be implemented using either hello [.NET Framework client library](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/), or hello PowerShell scripts found at [Azure SQL DB - Elastic Database tools scripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span> <span data-ttu-id="9928e-113">Hier voorbeelden Hallo Hallo PowerShell-scripts gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9928e-113">hello examples here use hello PowerShell scripts.</span></span>

<span data-ttu-id="9928e-114">Zie voor meer informatie over Hallo ShardMapManager [Shard kaart management](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="9928e-114">For more information about hello ShardMapManager, see [Shard map management](sql-database-elastic-scale-shard-map-management.md).</span></span> <span data-ttu-id="9928e-115">Zie voor een overzicht van Hallo elastische database-hulpprogramma's [elastische Database functies overzicht](sql-database-elastic-scale-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9928e-115">For an overview of hello elastic database tools, see [Elastic Database features overview](sql-database-elastic-scale-introduction.md).</span></span>

## <a name="prepare-hello-shard-map-manager-database"></a><span data-ttu-id="9928e-116">Hallo shard kaart manager-database voorbereiden</span><span class="sxs-lookup"><span data-stu-id="9928e-116">Prepare hello shard map manager database</span></span>
<span data-ttu-id="9928e-117">Hallo shard-toewijzing manager is een speciale database die Hallo gegevens toomanage uitgebreide databases bevat.</span><span class="sxs-lookup"><span data-stu-id="9928e-117">hello shard map manager is a special database that contains hello data toomanage scaled-out databases.</span></span> <span data-ttu-id="9928e-118">U kunt een bestaande database gebruiken of een nieuwe database maken.</span><span class="sxs-lookup"><span data-stu-id="9928e-118">You can use an existing database, or create a new database.</span></span> <span data-ttu-id="9928e-119">Houd er rekening mee dat een database, fungeert als shard kaart manager mag geen Hallo dezelfde database als een shard.</span><span class="sxs-lookup"><span data-stu-id="9928e-119">Note that a database acting as shard map manager should not be hello same database as a shard.</span></span> <span data-ttu-id="9928e-120">Houd er ook rekening mee dat Hallo PowerShell-script niet Hallo-database voor u maken.</span><span class="sxs-lookup"><span data-stu-id="9928e-120">Also note that hello PowerShell script does not create hello database for you.</span></span> 

## <a name="step-1-create-a-shard-map-manager"></a><span data-ttu-id="9928e-121">Stap 1: Maak een shard kaart manager</span><span class="sxs-lookup"><span data-stu-id="9928e-121">Step 1: create a shard map manager</span></span>
    # Create a shard map manager. 
    New-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 
    #<server_name> and <smm_db_name> are hello server name and database name 
    # for hello new or existing database that should be used for storing 
    # tenant-database mapping information.

### <a name="tooretrieve-hello-shard-map-manager"></a><span data-ttu-id="9928e-122">manager tooretrieve hello shard-kaart</span><span class="sxs-lookup"><span data-stu-id="9928e-122">tooretrieve hello shard map manager</span></span>
<span data-ttu-id="9928e-123">Na het maken, kunt u Hallo shard-toewijzing manager met deze cmdlet ophalen.</span><span class="sxs-lookup"><span data-stu-id="9928e-123">After creation, you can retrieve hello shard map manager with this cmdlet.</span></span> <span data-ttu-id="9928e-124">Deze stap is nodig voor elke keer dat u moet toouse hello ShardMapManager object.</span><span class="sxs-lookup"><span data-stu-id="9928e-124">This step is needed every time you need toouse hello ShardMapManager object.</span></span>

    # Try tooget a reference toohello Shard Map Manager  
    $ShardMapManager = Get-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 


## <a name="step-2-create-hello-shard-map"></a><span data-ttu-id="9928e-125">Stap 2: Maak Hallo shard-kaart</span><span class="sxs-lookup"><span data-stu-id="9928e-125">Step 2: create hello shard map</span></span>
<span data-ttu-id="9928e-126">U kunt shard-toewijzing toocreate Hallo type moet selecteren.</span><span class="sxs-lookup"><span data-stu-id="9928e-126">You must select hello type of shard map toocreate.</span></span> <span data-ttu-id="9928e-127">Hallo keuze is afhankelijk van Hallo database-architectuur:</span><span class="sxs-lookup"><span data-stu-id="9928e-127">hello choice depends on hello database architecture:</span></span> 

1. <span data-ttu-id="9928e-128">Één tenant per database (voor termen, Zie Hallo [verklarende woordenlijst](sql-database-elastic-scale-glossary.md).)</span><span class="sxs-lookup"><span data-stu-id="9928e-128">Single tenant per database (For terms, see hello [glossary](sql-database-elastic-scale-glossary.md).)</span></span> 
2. <span data-ttu-id="9928e-129">Meerdere tenants per database (twee typen):</span><span class="sxs-lookup"><span data-stu-id="9928e-129">Multiple tenants per database (two types):</span></span>
   1. <span data-ttu-id="9928e-130">Toewijzing van de lijst</span><span class="sxs-lookup"><span data-stu-id="9928e-130">List mapping</span></span>
   2. <span data-ttu-id="9928e-131">Bereik toewijzing</span><span class="sxs-lookup"><span data-stu-id="9928e-131">Range mapping</span></span>

<span data-ttu-id="9928e-132">Voor een model voor één tenant, maakt u een **lijst toewijzing** shard-toewijzing.</span><span class="sxs-lookup"><span data-stu-id="9928e-132">For a single-tenant model, create a **list mapping** shard map.</span></span> <span data-ttu-id="9928e-133">Hallo één tenant model wijst één database per tenant.</span><span class="sxs-lookup"><span data-stu-id="9928e-133">hello single-tenant model assigns one database per tenant.</span></span> <span data-ttu-id="9928e-134">Dit is een doeltreffend model voor SaaS-ontwikkelaars aangezien vereenvoudigt het beheer.</span><span class="sxs-lookup"><span data-stu-id="9928e-134">This is an effective model for SaaS developers as it simplifies management.</span></span>

![Toewijzing van de lijst][1]

<span data-ttu-id="9928e-136">Hallo multitenant model wijst verschillende tenants tooa één database (en u kunt groepen van tenants verdelen over meerdere databases).</span><span class="sxs-lookup"><span data-stu-id="9928e-136">hello multi-tenant model assigns several tenants tooa single database (and you can distribute groups of tenants across multiple databases).</span></span> <span data-ttu-id="9928e-137">Dit model gebruiken wanneer u verwacht dat elke tenant toohave kleine hoeveelheden gegevens nodig heeft.</span><span class="sxs-lookup"><span data-stu-id="9928e-137">Use this model when you expect each tenant toohave small data needs.</span></span> <span data-ttu-id="9928e-138">In dit model we een bereik van het gebruik van tenants tooa database toewijzen **bereik toewijzing**.</span><span class="sxs-lookup"><span data-stu-id="9928e-138">In this model, we assign a range of tenants tooa database using **range mapping**.</span></span> 

![Bereik toewijzing][2]

<span data-ttu-id="9928e-140">Of u kunt implementeren met een multitenant database model met een *lijst toewijzing* tooassign meerdere tenants tooa één database.</span><span class="sxs-lookup"><span data-stu-id="9928e-140">Or you can implement a multi-tenant database model using a *list mapping* tooassign multiple tenants tooa single database.</span></span> <span data-ttu-id="9928e-141">Bijvoorbeeld, DB1 is gebruikte toostore informatie over de tenant-id 1 en 5 en DB2 slaat gegevens voor de tenant 7- en 10.</span><span class="sxs-lookup"><span data-stu-id="9928e-141">For example, DB1 is used toostore information about tenant id 1 and 5, and DB2 stores data for tenant 7 and tenant 10.</span></span> 

![Muliple tenants in één DB][3] 

<span data-ttu-id="9928e-143">**Op basis van uw keuze, kies een van de volgende opties:**</span><span class="sxs-lookup"><span data-stu-id="9928e-143">**Based on your choice, choose one of these options:**</span></span>

### <a name="option-1-create-a-shard-map-for-a-list-mapping"></a><span data-ttu-id="9928e-144">Optie 1: een shard-toewijzing voor de toewijzing van een lijst maken</span><span class="sxs-lookup"><span data-stu-id="9928e-144">Option 1: create a shard map for a list mapping</span></span>
<span data-ttu-id="9928e-145">Maakt een shard-toewijzing Hallo ShardMapManager object gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9928e-145">Create a shard map using hello ShardMapManager object.</span></span> 

    # $ShardMapManager is hello shard map manager object. 
    $ShardMap = New-ListShardMap -KeyType $([int]) 
    -ListShardMapName 'ListShardMap' 
    -ShardMapManager $ShardMapManager 


### <a name="option-2-create-a-shard-map-for-a-range-mapping"></a><span data-ttu-id="9928e-146">Optie 2: Maak een shard-toewijzing voor de toewijzing van een bereik</span><span class="sxs-lookup"><span data-stu-id="9928e-146">Option 2: create a shard map for a range mapping</span></span>
<span data-ttu-id="9928e-147">Houd er rekening mee dat tooutilize dit patroon van een toewijzing, tenant-id-waarden moet toobe continue bereiken en acceptabele toohave gat in Hallo bereiken door gewoon Hallo bereik wordt overgeslagen bij het maken van databases Hallo is.</span><span class="sxs-lookup"><span data-stu-id="9928e-147">Note that tooutilize this mapping pattern, tenant id values needs toobe continuous ranges, and it is acceptable toohave gap in hello ranges by simply skipping hello range when creating hello databases.</span></span>

    # $ShardMapManager is hello shard map manager object 
    # 'RangeShardMap' is hello unique identifier for hello range shard map.  
    $ShardMap = New-RangeShardMap 
    -KeyType $([int]) 
    -RangeShardMapName 'RangeShardMap' 
    -ShardMapManager $ShardMapManager 

### <a name="option-3-list-mappings-on-a-single-database"></a><span data-ttu-id="9928e-148">Optie 3: De toewijzingen van de lijst op een individuele database</span><span class="sxs-lookup"><span data-stu-id="9928e-148">Option 3: List mappings on a single database</span></span>
<span data-ttu-id="9928e-149">Instellen van dit patroon vereist ook het maken van een kaart lijst zoals u in stap 2, optie 1.</span><span class="sxs-lookup"><span data-stu-id="9928e-149">Setting up this pattern also requires creation of a list map as shown in step 2, option 1.</span></span>

## <a name="step-3-prepare-individual-shards"></a><span data-ttu-id="9928e-150">Stap 3: Afzonderlijke shards voorbereiden</span><span class="sxs-lookup"><span data-stu-id="9928e-150">Step 3: Prepare individual shards</span></span>
<span data-ttu-id="9928e-151">Voeg elke manager shard (database) toohello shard-toewijzing toe.</span><span class="sxs-lookup"><span data-stu-id="9928e-151">Add each shard (database) toohello shard map manager.</span></span> <span data-ttu-id="9928e-152">Hallo afzonderlijke databases nu voorbereid voor het opslaan van informatie over de Identiteitstoewijzing.</span><span class="sxs-lookup"><span data-stu-id="9928e-152">This prepares hello individual databases for storing mapping information.</span></span> <span data-ttu-id="9928e-153">Deze methode niet uitvoeren op elke shard.</span><span class="sxs-lookup"><span data-stu-id="9928e-153">Execute this method on each shard.</span></span>

    Add-Shard 
    -ShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>'
    # hello $ShardMap is hello shard map created in step 2.


## <a name="step-4-add-mappings"></a><span data-ttu-id="9928e-154">Stap 4: Toewijzingen toevoegen</span><span class="sxs-lookup"><span data-stu-id="9928e-154">Step 4: Add mappings</span></span>
<span data-ttu-id="9928e-155">Hallo toewijzingen toe te voegen, is afhankelijk van Hallo soort shard-toewijzing die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9928e-155">hello addition of mappings depends on hello kind of shard map you created.</span></span> <span data-ttu-id="9928e-156">Als u een lijst kaart hebt gemaakt, kunt u de toewijzingen van de lijst toevoegen.</span><span class="sxs-lookup"><span data-stu-id="9928e-156">If you created a list map, you add list mappings.</span></span> <span data-ttu-id="9928e-157">Als u een bereik kaart hebt gemaakt, voegt u bereik toewijzingen.</span><span class="sxs-lookup"><span data-stu-id="9928e-157">If you created a range map, you add range mappings.</span></span>

### <a name="option-1-map-hello-data-for-a-list-mapping"></a><span data-ttu-id="9928e-158">Optie 1: Hallo-gegevens voor een lijst toewijzing toewijzen</span><span class="sxs-lookup"><span data-stu-id="9928e-158">Option 1: map hello data for a list mapping</span></span>
<span data-ttu-id="9928e-159">Hallo gegevens moeten worden toegewezen door de toewijzing van een lijst toe te voegen voor elke tenant.</span><span class="sxs-lookup"><span data-stu-id="9928e-159">Map hello data by adding a list mapping for each tenant.</span></span>  

    # Create hello mappings and associate it with hello new shards 
    Add-ListMapping 
    -KeyType $([int]) 
    -ListPoint '<tenant_id>' 
    -ListShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 

### <a name="option-2-map-hello-data-for-a-range-mapping"></a><span data-ttu-id="9928e-160">Optie 2: Hallo-gegevens voor de toewijzing van een bereik toewijzen</span><span class="sxs-lookup"><span data-stu-id="9928e-160">Option 2: map hello data for a range mapping</span></span>
<span data-ttu-id="9928e-161">Hallo bereik toewijzingen voor alle Hallo tenant bereik-id - database koppelingen toevoegen:</span><span class="sxs-lookup"><span data-stu-id="9928e-161">Add hello range mappings for all hello tenant id range - database associations:</span></span>

    # Create hello mappings and associate it with hello new shards 
    Add-RangeMapping 
    -KeyType $([int]) 
    -RangeHigh '5' 
    -RangeLow '1' 
    -RangeShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 


### <a name="step-4-option-3-map-hello-data-for-multiple-tenants-on-a-single-database"></a><span data-ttu-id="9928e-162">Stap 4-optie 3: Hallo gegevens moeten worden toegewezen voor meerdere tenants op een individuele database</span><span class="sxs-lookup"><span data-stu-id="9928e-162">Step 4 option 3: map hello data for multiple tenants on a single database</span></span>
<span data-ttu-id="9928e-163">Voer voor elke tenant Hallo toevoegen ListMapping (optie 1, hierboven).</span><span class="sxs-lookup"><span data-stu-id="9928e-163">For each tenant, run hello Add-ListMapping (option 1, above).</span></span> 

## <a name="checking-hello-mappings"></a><span data-ttu-id="9928e-164">Hallo toewijzingen controleren</span><span class="sxs-lookup"><span data-stu-id="9928e-164">Checking hello mappings</span></span>
<span data-ttu-id="9928e-165">Informatie over Hallo bestaande shards en Hallo-toewijzingen die zijn gekoppeld aan deze kan worden opgevraagd met volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="9928e-165">Information about hello existing shards and hello mappings associated with them can be queried using following commands:</span></span>  

    # List hello shards and mappings 
    Get-Shards -ShardMap $ShardMap 
    Get-Mappings -ShardMap $ShardMap 

## <a name="summary"></a><span data-ttu-id="9928e-166">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="9928e-166">Summary</span></span>
<span data-ttu-id="9928e-167">Nadat u Hallo-installatie hebt voltooid, kunt u beginnen toouse Hallo elastische Database-clientbibliotheek.</span><span class="sxs-lookup"><span data-stu-id="9928e-167">Once you have completed hello setup, you can begin toouse hello Elastic Database client library.</span></span> <span data-ttu-id="9928e-168">U kunt ook [gegevensafhankelijke routering](sql-database-elastic-scale-data-dependent-routing.md) en [query meerdere shard](sql-database-elastic-scale-multishard-querying.md).</span><span class="sxs-lookup"><span data-stu-id="9928e-168">You can also use [data dependent routing](sql-database-elastic-scale-data-dependent-routing.md) and [multi-shard query](sql-database-elastic-scale-multishard-querying.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9928e-169">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9928e-169">Next steps</span></span>
<span data-ttu-id="9928e-170">Ophalen van de PowerShell-scripts Hallo van [Azure SQL DB elastische Database tools sripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="9928e-170">Get hello PowerShell scripts from [Azure SQL DB-Elastic Database tools sripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

<span data-ttu-id="9928e-171">Hallo-hulpprogramma's zijn ook op GitHub: [/elastische-db-hulpprogramma's van Azure](https://github.com/Azure/elastic-db-tools).</span><span class="sxs-lookup"><span data-stu-id="9928e-171">hello tools are also on GitHub: [Azure/elastic-db-tools](https://github.com/Azure/elastic-db-tools).</span></span>

<span data-ttu-id="9928e-172">Hallo gesplitste merge tool toomove gegevens tooor van een multi-tenant model tooa één tenant-model gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9928e-172">Use hello split-merge tool toomove data tooor from a multi-tenant model tooa single tenant model.</span></span> <span data-ttu-id="9928e-173">Zie [gesplitste merge tool](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9928e-173">See [Split merge tool](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9928e-174">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="9928e-174">Additional resources</span></span>
<span data-ttu-id="9928e-175">Zie voor informatie over algemene gegevensarchitectuurpatronen van multitenant software as a service (SaaS)-databasetoepassingen, [Ontwerppatronen voor multitenant SaaS-toepassingen met Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md).</span><span class="sxs-lookup"><span data-stu-id="9928e-175">For information on common data architecture patterns of multi-tenant software-as-a-service (SaaS) database applications, see [Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md).</span></span>

## <a name="questions-and-feature-requests"></a><span data-ttu-id="9928e-176">Vragen en Functieaanvragen</span><span class="sxs-lookup"><span data-stu-id="9928e-176">Questions and Feature Requests</span></span>
<span data-ttu-id="9928e-177">Voor vragen kunt contact toous op Hallo [SQL Database-forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) en voor functieaanvragen, deze toe te voegen toohello [forum met feedback van SQL-Database](https://feedback.azure.com/forums/217321-sql-database/).</span><span class="sxs-lookup"><span data-stu-id="9928e-177">For questions, please reach out toous on hello [SQL Database forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) and for feature requests, please add them toohello [SQL Database feedback forum](https://feedback.azure.com/forums/217321-sql-database/).</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-convert-to-use-elastic-tools/listmapping.png
[2]: ./media/sql-database-elastic-convert-to-use-elastic-tools/rangemapping.png
[3]: ./media/sql-database-elastic-convert-to-use-elastic-tools/multipleonsingledb.png

