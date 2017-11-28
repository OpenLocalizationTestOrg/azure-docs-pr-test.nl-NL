---
title: 'T-SQL: Een elastische pool in Azure SQL Database beheren | Microsoft Docs'
description: T-SQL gebruiken voor het beheren van een Azure SQL Database elastische pool.
services: sql-database
documentationcenter: 
author: srinia
manager: jhubbard
editor: 
ms.assetid: 4e288e17-bc3e-4255-9fbe-0a2ac0dbd7dd
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 05/27/2016
ms.author: srinia
ms.openlocfilehash: c6b64e4a7fd91283a37a792b294965064d653003
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-and-manage-an-elastic-pool-with-transact-sql"></a><span data-ttu-id="7408c-103">Bewaken en beheren van een elastische groep met Transact-SQL</span><span class="sxs-lookup"><span data-stu-id="7408c-103">Monitor and manage an elastic pool with Transact-SQL</span></span>
<span data-ttu-id="7408c-104">In dit onderwerp wordt beschreven hoe u voor het beheren van schaalbare [elastische pools](sql-database-elastic-pool.md) met Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="7408c-104">This topic shows you how to manage scalable [elastic pools](sql-database-elastic-pool.md) with Transact-SQL.</span></span>  <span data-ttu-id="7408c-105">U kunt ook maken en een elastische pool in Azure beheren de [Azure-portal](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), de REST-API of [C#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="7408c-105">You can also create and manage an Azure elastic pool the [Azure portal](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), the REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="7408c-106">U kunt ook maken en databases verplaatsen naar en van elastische pools met [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span><span class="sxs-lookup"><span data-stu-id="7408c-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>


<span data-ttu-id="7408c-107">Gebruik de [Create Database (Azure SQL Database)](https://msdn.microsoft.com/library/dn268335.aspx) en [Database(Azure SQL Database) Alter](https://msdn.microsoft.com/library/mt574871.aspx) opdrachten voor het maken en databases verplaatsen naar en van elastische pools.</span><span class="sxs-lookup"><span data-stu-id="7408c-107">Use the [Create Database (Azure SQL Database)](https://msdn.microsoft.com/library/dn268335.aspx) and [Alter Database(Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) commands to create and move databases into and out of elastic pools.</span></span> <span data-ttu-id="7408c-108">De elastische groep moet bestaan voordat u deze opdrachten kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7408c-108">The elastic pool must exist before you can use these commands.</span></span> <span data-ttu-id="7408c-109">Deze opdrachten beïnvloeden alleen databases.</span><span class="sxs-lookup"><span data-stu-id="7408c-109">These commands affect only databases.</span></span> <span data-ttu-id="7408c-110">Maken van nieuwe groepen en het instellen van eigenschappen van de groep van toepassingen (zoals min en max edtu's) kunnen niet worden gewijzigd met T-SQL-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="7408c-110">Creation of new pools and the setting of pool properties (such as min and max eDTUs) cannot be changed with T-SQL commands.</span></span>

## <a name="create-a-pooled-database-in-an-elastic-pool"></a><span data-ttu-id="7408c-111">Maak een gegroepeerde database in een elastische pool</span><span class="sxs-lookup"><span data-stu-id="7408c-111">Create a pooled database in an elastic pool</span></span>
<span data-ttu-id="7408c-112">Gebruik de opdracht CREATE DATABASE met de optie SERVICE_OBJECTIVE.</span><span class="sxs-lookup"><span data-stu-id="7408c-112">Use the CREATE DATABASE command with the SERVICE_OBJECTIVE option.</span></span>   

    CREATE DATABASE db1 ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3M100] ));
    -- Create a database named db1 in an elastic named S3M100.

<span data-ttu-id="7408c-113">Alle databases in een elastische groep overgenomen door de servicelaag van de elastische pool (Basic, Standard, Premium).</span><span class="sxs-lookup"><span data-stu-id="7408c-113">All databases in an elastic pool inherit the service tier of the elastic pool (Basic, Standard, Premium).</span></span> 

## <a name="move-a-database-between-elastic-pools"></a><span data-ttu-id="7408c-114">Een database verplaatst tussen elastische pools</span><span class="sxs-lookup"><span data-stu-id="7408c-114">Move a database between elastic pools</span></span>
<span data-ttu-id="7408c-115">Gebruik de opdracht ALTER DATABASE met de wijzigen en stel SERVICE\_SERVICEDOELSTELLING optie ELASTISCHE\_van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="7408c-115">Use the ALTER DATABASE command with the MODIFY and set SERVICE\_OBJECTIVE option as ELASTIC\_POOL.</span></span> <span data-ttu-id="7408c-116">De naam instellen op de naam van de doelgroep.</span><span class="sxs-lookup"><span data-stu-id="7408c-116">Set the name to the name of the target pool.</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [PM125] ));
    -- Move the database named db1 to an elastic named P1M125  

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="7408c-117">Een database verplaatsen naar een elastische pool</span><span class="sxs-lookup"><span data-stu-id="7408c-117">Move a database into an elastic pool</span></span>
<span data-ttu-id="7408c-118">Gebruik de opdracht ALTER DATABASE met de wijzigen en stel SERVICE\_OBJECTIVE optie ELASTIC_POOL.</span><span class="sxs-lookup"><span data-stu-id="7408c-118">Use the ALTER DATABASE command with the MODIFY and set SERVICE\_OBJECTIVE option as ELASTIC_POOL.</span></span> <span data-ttu-id="7408c-119">De naam instellen op de naam van de doelgroep.</span><span class="sxs-lookup"><span data-stu-id="7408c-119">Set the name to the name of the target pool.</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3100] ));
    -- Move the database named db1 to an elastic named S3100.

## <a name="move-a-database-out-of-an-elastic-pool"></a><span data-ttu-id="7408c-120">Een database verplaatst buiten een elastische pool</span><span class="sxs-lookup"><span data-stu-id="7408c-120">Move a database out of an elastic pool</span></span>
<span data-ttu-id="7408c-121">Gebruik de opdracht ALTER DATABASE en SERVICE_OBJECTIVE ingesteld op een van de prestaties (zoals S0 of S1).</span><span class="sxs-lookup"><span data-stu-id="7408c-121">Use the ALTER DATABASE command and set the SERVICE_OBJECTIVE to one of the performance levels (such as S0 or S1).</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = 'S1');
    -- Changes the database into a stand-alone database with the service objective S1.

## <a name="list-databases-in-an-elastic-pool"></a><span data-ttu-id="7408c-122">Lijst met databases in een elastische pool</span><span class="sxs-lookup"><span data-stu-id="7408c-122">List databases in an elastic pool</span></span>
<span data-ttu-id="7408c-123">Gebruik de [sys.database\_service \_doelstellingen weergave](https://msdn.microsoft.com/library/mt712619) voor een lijst met alle databases in een elastische pool.</span><span class="sxs-lookup"><span data-stu-id="7408c-123">Use the [sys.database\_service \_objectives view](https://msdn.microsoft.com/library/mt712619) to list all the databases in an elastic pool.</span></span> <span data-ttu-id="7408c-124">Meld u aan bij de master database query uitvoeren op de weergave.</span><span class="sxs-lookup"><span data-stu-id="7408c-124">Log in to the master database to query the view.</span></span>

    SELECT d.name, slo.*  
    FROM sys.databases d 
    JOIN sys.database_service_objectives slo  
    ON d.database_id = slo.database_id
    WHERE elastic_pool_name = 'MyElasticPool'; 

## <a name="get-resource-usage-data-for-an-elastic-pool"></a><span data-ttu-id="7408c-125">Gegevens over brongebruik ophalen voor een elastische pool</span><span class="sxs-lookup"><span data-stu-id="7408c-125">Get resource usage data for an elastic pool</span></span>
<span data-ttu-id="7408c-126">Gebruik de [sys.elastic\_groep \_resource \_weergave van statistieken](https://msdn.microsoft.com/library/mt280062.aspx) onderzoeken gebruiksstatistieken voor de bron van een elastische pool op een logische server.</span><span class="sxs-lookup"><span data-stu-id="7408c-126">Use the [sys.elastic\_pool \_resource \_stats view](https://msdn.microsoft.com/library/mt280062.aspx) to examine the resource usage statistics of an elastic pool on a logical server.</span></span> <span data-ttu-id="7408c-127">Meld u aan bij de master database query uitvoeren op de weergave.</span><span class="sxs-lookup"><span data-stu-id="7408c-127">Log in to the master database to query the view.</span></span>

    SELECT * FROM sys.elastic_pool_resource_stats 
    WHERE elastic_pool_name = 'MyElasticPool'
    ORDER BY end_time DESC;

## <a name="get-resource-usage-for-a-pooled-database"></a><span data-ttu-id="7408c-128">Resourcegebruik ophalen voor een gegroepeerde database</span><span class="sxs-lookup"><span data-stu-id="7408c-128">Get resource usage for a pooled database</span></span>
<span data-ttu-id="7408c-129">Gebruik de [sys.dm\_ db\_ resource\_weergave van statistieken](https://msdn.microsoft.com/library/dn800981.aspx) of [sys.resource \_weergave van statistieken](https://msdn.microsoft.com/library/dn269979.aspx) onderzoeken gebruiksstatistieken voor de bron van een database in een elastische pool.</span><span class="sxs-lookup"><span data-stu-id="7408c-129">Use the [sys.dm\_ db\_ resource\_stats view](https://msdn.microsoft.com/library/dn800981.aspx) or [sys.resource \_stats view](https://msdn.microsoft.com/library/dn269979.aspx) to examine the resource usage statistics of a database in an elastic pool.</span></span> <span data-ttu-id="7408c-130">Dit proces is vergelijkbaar met het Resourcegebruik voor één database opvragen.</span><span class="sxs-lookup"><span data-stu-id="7408c-130">This process is similar to querying resource usage for a single database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7408c-131">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7408c-131">Next steps</span></span>
<span data-ttu-id="7408c-132">Nadat een elastische groep is gemaakt, kunt u Elastische databases in de pool beheren met elastische taken maken.</span><span class="sxs-lookup"><span data-stu-id="7408c-132">After creating an elastic pool, you can manage elastic databases in the pool by creating elastic jobs.</span></span> <span data-ttu-id="7408c-133">Elastische taken vergemakkelijken actieve T-SQL-scripts uitvoeren op een willekeurig aantal databases in de pool.</span><span class="sxs-lookup"><span data-stu-id="7408c-133">Elastic jobs facilitate running T-SQL scripts against any number of databases in the pool.</span></span> <span data-ttu-id="7408c-134">Zie voor meer informatie [elastische database taken overzicht](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7408c-134">For more information, see [Elastic database jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

<span data-ttu-id="7408c-135">Zie [uitbreiden met Azure SQL Database](sql-database-elastic-scale-introduction.md): gebruik elastische database-hulpmiddelen om uitschalen, het verplaatsen van gegevens, opvragen of transacties maken.</span><span class="sxs-lookup"><span data-stu-id="7408c-135">See [Scaling out with Azure SQL Database](sql-database-elastic-scale-introduction.md): use elastic database tools to scale out, move data, query, or create transactions.</span></span>

