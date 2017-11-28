---
title: Migreren van bestaande databases voor scale-out | Microsoft Docs
description: Shard databases voor het gebruik van hulpprogramma's voor elastische database door het maken van een shard-toewijzing manager converteren
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
ms.openlocfilehash: 099f40d00753b7c86ba726a818f17d440a125221
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-existing-databases-to-scale-out"></a><span data-ttu-id="c866f-103">Bestaande databases migreren voor uitschaling</span><span class="sxs-lookup"><span data-stu-id="c866f-103">Migrate existing databases to scale-out</span></span>
<span data-ttu-id="c866f-104">Uw bestaande uitgebreid shard databases met hulpprogramma's van Azure SQL Database database eenvoudig te beheren (zoals de [clientbibliotheek voor elastische Database](sql-database-elastic-database-client-library.md)).</span><span class="sxs-lookup"><span data-stu-id="c866f-104">Easily manage your existing scaled-out sharded databases using Azure SQL Database database tools (such as the [Elastic Database client library](sql-database-elastic-database-client-library.md)).</span></span> <span data-ttu-id="c866f-105">U moet eerst een bestaande set van databases moeten worden gebruikt converteren de [shard kaart manager](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="c866f-105">You must first convert an existing set of databases to use the [shard map manager](sql-database-elastic-scale-shard-map-management.md).</span></span> 

## <a name="overview"></a><span data-ttu-id="c866f-106">Overzicht</span><span class="sxs-lookup"><span data-stu-id="c866f-106">Overview</span></span>
<span data-ttu-id="c866f-107">Voor het migreren van een bestaande database in de shard:</span><span class="sxs-lookup"><span data-stu-id="c866f-107">To migrate an existing sharded database:</span></span> 

1. <span data-ttu-id="c866f-108">Bereid de [shard-toewijzing manager-database](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="c866f-108">Prepare the [shard map manager database](sql-database-elastic-scale-shard-map-management.md).</span></span>
2. <span data-ttu-id="c866f-109">Maak de shard-toewijzing.</span><span class="sxs-lookup"><span data-stu-id="c866f-109">Create the shard map.</span></span>
3. <span data-ttu-id="c866f-110">Bereid de afzonderlijke shards.</span><span class="sxs-lookup"><span data-stu-id="c866f-110">Prepare the individual shards.</span></span>  
4. <span data-ttu-id="c866f-111">Toewijzingen toevoegen aan de shard-toewijzing.</span><span class="sxs-lookup"><span data-stu-id="c866f-111">Add mappings to the shard map.</span></span>

<span data-ttu-id="c866f-112">Deze technieken kunnen worden geïmplementeerd met behulp van de [clientbibliotheek voor .NET Framework](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/), of de PowerShell-scripts gevonden op [Azure SQL DB - elastische Database extra scripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="c866f-112">These techniques can be implemented using either the [.NET Framework client library](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/), or the PowerShell scripts found at [Azure SQL DB - Elastic Database tools scripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span> <span data-ttu-id="c866f-113">De voorbeelden die hier worden de PowerShell-scripts gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c866f-113">The examples here use the PowerShell scripts.</span></span>

<span data-ttu-id="c866f-114">Zie voor meer informatie over de ShardMapManager [Shard kaart management](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="c866f-114">For more information about the ShardMapManager, see [Shard map management](sql-database-elastic-scale-shard-map-management.md).</span></span> <span data-ttu-id="c866f-115">Zie voor een overzicht van de hulpprogramma's van elastische database [elastische Database functies overzicht](sql-database-elastic-scale-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c866f-115">For an overview of the elastic database tools, see [Elastic Database features overview](sql-database-elastic-scale-introduction.md).</span></span>

## <a name="prepare-the-shard-map-manager-database"></a><span data-ttu-id="c866f-116">Voorbereiden van de manager-database van de shard-kaart</span><span class="sxs-lookup"><span data-stu-id="c866f-116">Prepare the shard map manager database</span></span>
<span data-ttu-id="c866f-117">De shard-toewijzing manager is een speciale database die de gegevens voor het beheren van uitgebreide databases bevat.</span><span class="sxs-lookup"><span data-stu-id="c866f-117">The shard map manager is a special database that contains the data to manage scaled-out databases.</span></span> <span data-ttu-id="c866f-118">U kunt een bestaande database gebruiken of een nieuwe database maken.</span><span class="sxs-lookup"><span data-stu-id="c866f-118">You can use an existing database, or create a new database.</span></span> <span data-ttu-id="c866f-119">Houd er rekening mee dat een database die fungeert als de manager van shard-toewijzing niet dezelfde database als een shard moet worden.</span><span class="sxs-lookup"><span data-stu-id="c866f-119">Note that a database acting as shard map manager should not be the same database as a shard.</span></span> <span data-ttu-id="c866f-120">Houd er ook rekening mee dat het PowerShell-script niet de database voor u maken.</span><span class="sxs-lookup"><span data-stu-id="c866f-120">Also note that the PowerShell script does not create the database for you.</span></span> 

## <a name="step-1-create-a-shard-map-manager"></a><span data-ttu-id="c866f-121">Stap 1: Maak een shard kaart manager</span><span class="sxs-lookup"><span data-stu-id="c866f-121">Step 1: create a shard map manager</span></span>
    # Create a shard map manager. 
    New-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 
    #<server_name> and <smm_db_name> are the server name and database name 
    # for the new or existing database that should be used for storing 
    # tenant-database mapping information.

### <a name="to-retrieve-the-shard-map-manager"></a><span data-ttu-id="c866f-122">Voor het ophalen van de manager shard-kaart</span><span class="sxs-lookup"><span data-stu-id="c866f-122">To retrieve the shard map manager</span></span>
<span data-ttu-id="c866f-123">Na het maken, kunt u de shard-toewijzing manager met deze cmdlet ophalen.</span><span class="sxs-lookup"><span data-stu-id="c866f-123">After creation, you can retrieve the shard map manager with this cmdlet.</span></span> <span data-ttu-id="c866f-124">Deze stap is nodig voor elke keer dat u wilt gebruiken, het ShardMapManager-object.</span><span class="sxs-lookup"><span data-stu-id="c866f-124">This step is needed every time you need to use the ShardMapManager object.</span></span>

    # Try to get a reference to the Shard Map Manager  
    $ShardMapManager = Get-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 


## <a name="step-2-create-the-shard-map"></a><span data-ttu-id="c866f-125">Stap 2: Maak de shard-kaart</span><span class="sxs-lookup"><span data-stu-id="c866f-125">Step 2: create the shard map</span></span>
<span data-ttu-id="c866f-126">U moet het type van shard-toewijzing te maken.</span><span class="sxs-lookup"><span data-stu-id="c866f-126">You must select the type of shard map to create.</span></span> <span data-ttu-id="c866f-127">De keuze is afhankelijk van de database-architectuur:</span><span class="sxs-lookup"><span data-stu-id="c866f-127">The choice depends on the database architecture:</span></span> 

1. <span data-ttu-id="c866f-128">Één tenant per database (voor termen, Zie de [verklarende woordenlijst](sql-database-elastic-scale-glossary.md).)</span><span class="sxs-lookup"><span data-stu-id="c866f-128">Single tenant per database (For terms, see the [glossary](sql-database-elastic-scale-glossary.md).)</span></span> 
2. <span data-ttu-id="c866f-129">Meerdere tenants per database (twee typen):</span><span class="sxs-lookup"><span data-stu-id="c866f-129">Multiple tenants per database (two types):</span></span>
   1. <span data-ttu-id="c866f-130">Toewijzing van de lijst</span><span class="sxs-lookup"><span data-stu-id="c866f-130">List mapping</span></span>
   2. <span data-ttu-id="c866f-131">Bereik toewijzing</span><span class="sxs-lookup"><span data-stu-id="c866f-131">Range mapping</span></span>

<span data-ttu-id="c866f-132">Voor een model voor één tenant, maakt u een **lijst toewijzing** shard-toewijzing.</span><span class="sxs-lookup"><span data-stu-id="c866f-132">For a single-tenant model, create a **list mapping** shard map.</span></span> <span data-ttu-id="c866f-133">Het model voor één tenant wijst één database per tenant.</span><span class="sxs-lookup"><span data-stu-id="c866f-133">The single-tenant model assigns one database per tenant.</span></span> <span data-ttu-id="c866f-134">Dit is een doeltreffend model voor SaaS-ontwikkelaars aangezien vereenvoudigt het beheer.</span><span class="sxs-lookup"><span data-stu-id="c866f-134">This is an effective model for SaaS developers as it simplifies management.</span></span>

![Toewijzing van de lijst][1]

<span data-ttu-id="c866f-136">Het model multitenant verschillende tenants toegewezen aan een individuele database (en u kunt groepen van tenants verdelen over meerdere databases).</span><span class="sxs-lookup"><span data-stu-id="c866f-136">The multi-tenant model assigns several tenants to a single database (and you can distribute groups of tenants across multiple databases).</span></span> <span data-ttu-id="c866f-137">Dit model gebruiken wanneer u verwacht dat elke tenant kleine hoeveelheden gegevens nodig hebben.</span><span class="sxs-lookup"><span data-stu-id="c866f-137">Use this model when you expect each tenant to have small data needs.</span></span> <span data-ttu-id="c866f-138">In dit model we een scala aan tenants toewijzen aan een database met **bereik toewijzing**.</span><span class="sxs-lookup"><span data-stu-id="c866f-138">In this model, we assign a range of tenants to a database using **range mapping**.</span></span> 

![Bereik toewijzing][2]

<span data-ttu-id="c866f-140">Of u kunt implementeren met een multitenant database model met een *lijst toewijzing* meerdere tenants toewijzen aan een individuele database.</span><span class="sxs-lookup"><span data-stu-id="c866f-140">Or you can implement a multi-tenant database model using a *list mapping* to assign multiple tenants to a single database.</span></span> <span data-ttu-id="c866f-141">Bijvoorbeeld, DB1 wordt gebruikt voor het opslaan van informatie over de tenant-id 1 en 5 en DB2 slaat gegevens voor de tenant 7- en 10.</span><span class="sxs-lookup"><span data-stu-id="c866f-141">For example, DB1 is used to store information about tenant id 1 and 5, and DB2 stores data for tenant 7 and tenant 10.</span></span> 

![Muliple tenants in één DB][3] 

<span data-ttu-id="c866f-143">**Op basis van uw keuze, kies een van de volgende opties:**</span><span class="sxs-lookup"><span data-stu-id="c866f-143">**Based on your choice, choose one of these options:**</span></span>

### <a name="option-1-create-a-shard-map-for-a-list-mapping"></a><span data-ttu-id="c866f-144">Optie 1: een shard-toewijzing voor de toewijzing van een lijst maken</span><span class="sxs-lookup"><span data-stu-id="c866f-144">Option 1: create a shard map for a list mapping</span></span>
<span data-ttu-id="c866f-145">Maakt een shard-toewijzing met behulp van het object ShardMapManager.</span><span class="sxs-lookup"><span data-stu-id="c866f-145">Create a shard map using the ShardMapManager object.</span></span> 

    # $ShardMapManager is the shard map manager object. 
    $ShardMap = New-ListShardMap -KeyType $([int]) 
    -ListShardMapName 'ListShardMap' 
    -ShardMapManager $ShardMapManager 


### <a name="option-2-create-a-shard-map-for-a-range-mapping"></a><span data-ttu-id="c866f-146">Optie 2: Maak een shard-toewijzing voor de toewijzing van een bereik</span><span class="sxs-lookup"><span data-stu-id="c866f-146">Option 2: create a shard map for a range mapping</span></span>
<span data-ttu-id="c866f-147">Houd er rekening mee dat voor het gebruik van deze toewijzing patroon, tenant-id waarden moet worden continu bereiken en het is acceptabel om onderbreking in de bereiken door gewoon het bereik wordt overgeslagen bij het maken van de databases.</span><span class="sxs-lookup"><span data-stu-id="c866f-147">Note that to utilize this mapping pattern, tenant id values needs to be continuous ranges, and it is acceptable to have gap in the ranges by simply skipping the range when creating the databases.</span></span>

    # $ShardMapManager is the shard map manager object 
    # 'RangeShardMap' is the unique identifier for the range shard map.  
    $ShardMap = New-RangeShardMap 
    -KeyType $([int]) 
    -RangeShardMapName 'RangeShardMap' 
    -ShardMapManager $ShardMapManager 

### <a name="option-3-list-mappings-on-a-single-database"></a><span data-ttu-id="c866f-148">Optie 3: De toewijzingen van de lijst op een individuele database</span><span class="sxs-lookup"><span data-stu-id="c866f-148">Option 3: List mappings on a single database</span></span>
<span data-ttu-id="c866f-149">Instellen van dit patroon vereist ook het maken van een kaart lijst zoals u in stap 2, optie 1.</span><span class="sxs-lookup"><span data-stu-id="c866f-149">Setting up this pattern also requires creation of a list map as shown in step 2, option 1.</span></span>

## <a name="step-3-prepare-individual-shards"></a><span data-ttu-id="c866f-150">Stap 3: Afzonderlijke shards voorbereiden</span><span class="sxs-lookup"><span data-stu-id="c866f-150">Step 3: Prepare individual shards</span></span>
<span data-ttu-id="c866f-151">Elke shard (database) toevoegen aan de shard-toewijzing manager.</span><span class="sxs-lookup"><span data-stu-id="c866f-151">Add each shard (database) to the shard map manager.</span></span> <span data-ttu-id="c866f-152">Hiermee wordt de afzonderlijke databases voorbereid voor het opslaan van informatie over de Identiteitstoewijzing.</span><span class="sxs-lookup"><span data-stu-id="c866f-152">This prepares the individual databases for storing mapping information.</span></span> <span data-ttu-id="c866f-153">Deze methode niet uitvoeren op elke shard.</span><span class="sxs-lookup"><span data-stu-id="c866f-153">Execute this method on each shard.</span></span>

    Add-Shard 
    -ShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>'
    # The $ShardMap is the shard map created in step 2.


## <a name="step-4-add-mappings"></a><span data-ttu-id="c866f-154">Stap 4: Toewijzingen toevoegen</span><span class="sxs-lookup"><span data-stu-id="c866f-154">Step 4: Add mappings</span></span>
<span data-ttu-id="c866f-155">Toewijzingen toe te voegen, is afhankelijk van het soort shard-toewijzing die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c866f-155">The addition of mappings depends on the kind of shard map you created.</span></span> <span data-ttu-id="c866f-156">Als u een lijst kaart hebt gemaakt, kunt u de toewijzingen van de lijst toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c866f-156">If you created a list map, you add list mappings.</span></span> <span data-ttu-id="c866f-157">Als u een bereik kaart hebt gemaakt, voegt u bereik toewijzingen.</span><span class="sxs-lookup"><span data-stu-id="c866f-157">If you created a range map, you add range mappings.</span></span>

### <a name="option-1-map-the-data-for-a-list-mapping"></a><span data-ttu-id="c866f-158">Optie 1: de gegevens voor een lijst toewijzing toewijzen</span><span class="sxs-lookup"><span data-stu-id="c866f-158">Option 1: map the data for a list mapping</span></span>
<span data-ttu-id="c866f-159">De gegevens moeten worden toegewezen door de toewijzing van een lijst toe te voegen voor elke tenant.</span><span class="sxs-lookup"><span data-stu-id="c866f-159">Map the data by adding a list mapping for each tenant.</span></span>  

    # Create the mappings and associate it with the new shards 
    Add-ListMapping 
    -KeyType $([int]) 
    -ListPoint '<tenant_id>' 
    -ListShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 

### <a name="option-2-map-the-data-for-a-range-mapping"></a><span data-ttu-id="c866f-160">Optie 2: de gegevens voor de toewijzing van een bereik toewijzen</span><span class="sxs-lookup"><span data-stu-id="c866f-160">Option 2: map the data for a range mapping</span></span>
<span data-ttu-id="c866f-161">Voeg de bereik-toewijzingen voor de tenant-id bereik met alle - database koppelingen:</span><span class="sxs-lookup"><span data-stu-id="c866f-161">Add the range mappings for all the tenant id range - database associations:</span></span>

    # Create the mappings and associate it with the new shards 
    Add-RangeMapping 
    -KeyType $([int]) 
    -RangeHigh '5' 
    -RangeLow '1' 
    -RangeShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 


### <a name="step-4-option-3-map-the-data-for-multiple-tenants-on-a-single-database"></a><span data-ttu-id="c866f-162">Stap 4-optie 3: de gegevens voor meerdere tenants op een individuele database toewijzen</span><span class="sxs-lookup"><span data-stu-id="c866f-162">Step 4 option 3: map the data for multiple tenants on a single database</span></span>
<span data-ttu-id="c866f-163">Voer voor elke tenant de Add-ListMapping (optie 1, hierboven).</span><span class="sxs-lookup"><span data-stu-id="c866f-163">For each tenant, run the Add-ListMapping (option 1, above).</span></span> 

## <a name="checking-the-mappings"></a><span data-ttu-id="c866f-164">De toewijzingen controleren</span><span class="sxs-lookup"><span data-stu-id="c866f-164">Checking the mappings</span></span>
<span data-ttu-id="c866f-165">Informatie over de bestaande shards en de bijbehorende toewijzingen kan worden opgevraagd met volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="c866f-165">Information about the existing shards and the mappings associated with them can be queried using following commands:</span></span>  

    # List the shards and mappings 
    Get-Shards -ShardMap $ShardMap 
    Get-Mappings -ShardMap $ShardMap 

## <a name="summary"></a><span data-ttu-id="c866f-166">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="c866f-166">Summary</span></span>
<span data-ttu-id="c866f-167">Nadat u de installatie hebt voltooid, kunt u beginnen met het gebruik van de clientbibliotheek voor elastische Database.</span><span class="sxs-lookup"><span data-stu-id="c866f-167">Once you have completed the setup, you can begin to use the Elastic Database client library.</span></span> <span data-ttu-id="c866f-168">U kunt ook [gegevensafhankelijke routering](sql-database-elastic-scale-data-dependent-routing.md) en [query meerdere shard](sql-database-elastic-scale-multishard-querying.md).</span><span class="sxs-lookup"><span data-stu-id="c866f-168">You can also use [data dependent routing](sql-database-elastic-scale-data-dependent-routing.md) and [multi-shard query](sql-database-elastic-scale-multishard-querying.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c866f-169">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c866f-169">Next steps</span></span>
<span data-ttu-id="c866f-170">Ophalen van de PowerShell-scripts uit [Azure SQL DB elastische Database tools sripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="c866f-170">Get the PowerShell scripts from [Azure SQL DB-Elastic Database tools sripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

<span data-ttu-id="c866f-171">De hulpprogramma's zijn ook op GitHub: [/elastische-db-hulpprogramma's van Azure](https://github.com/Azure/elastic-db-tools).</span><span class="sxs-lookup"><span data-stu-id="c866f-171">The tools are also on GitHub: [Azure/elastic-db-tools](https://github.com/Azure/elastic-db-tools).</span></span>

<span data-ttu-id="c866f-172">Het samenvoegen van gesplitste-hulpprogramma gebruiken om gegevens te verplaatsen naar of van een multi-tenant model naar een model voor één tenant.</span><span class="sxs-lookup"><span data-stu-id="c866f-172">Use the split-merge tool to move data to or from a multi-tenant model to a single tenant model.</span></span> <span data-ttu-id="c866f-173">Zie [gesplitste merge tool](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c866f-173">See [Split merge tool](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c866f-174">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="c866f-174">Additional resources</span></span>
<span data-ttu-id="c866f-175">Zie voor informatie over algemene gegevensarchitectuurpatronen van multitenant software as a service (SaaS)-databasetoepassingen, [Ontwerppatronen voor multitenant SaaS-toepassingen met Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md).</span><span class="sxs-lookup"><span data-stu-id="c866f-175">For information on common data architecture patterns of multi-tenant software-as-a-service (SaaS) database applications, see [Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md).</span></span>

## <a name="questions-and-feature-requests"></a><span data-ttu-id="c866f-176">Vragen en Functieaanvragen</span><span class="sxs-lookup"><span data-stu-id="c866f-176">Questions and Feature Requests</span></span>
<span data-ttu-id="c866f-177">Voor vragen kunt contact met ons op de [SQL Database-forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) en voor functieaanvragen, deze toe te voegen aan de [forum met feedback van SQL-Database](https://feedback.azure.com/forums/217321-sql-database/).</span><span class="sxs-lookup"><span data-stu-id="c866f-177">For questions, please reach out to us on the [SQL Database forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) and for feature requests, please add them to the [SQL Database feedback forum](https://feedback.azure.com/forums/217321-sql-database/).</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-convert-to-use-elastic-tools/listmapping.png
[2]: ./media/sql-database-elastic-convert-to-use-elastic-tools/rangemapping.png
[3]: ./media/sql-database-elastic-convert-to-use-elastic-tools/multipleonsingledb.png

