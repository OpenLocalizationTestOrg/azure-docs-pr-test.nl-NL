---
title: 'T-SQL: Een elastische pool in Azure SQL Database beheren | Microsoft Docs'
description: Gebruik de T-SQL-toomanage een elastische pool in Azure SQL Database.
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
ms.openlocfilehash: 666f131b2c88849a1a9ea83381bbc27548e93599
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-an-elastic-pool-with-transact-sql"></a><span data-ttu-id="36e80-103">Bewaken en beheren van een elastische groep met Transact-SQL</span><span class="sxs-lookup"><span data-stu-id="36e80-103">Monitor and manage an elastic pool with Transact-SQL</span></span>
<span data-ttu-id="36e80-104">Dit onderwerp leest u hoe toomanage schaalbare [elastische pools](sql-database-elastic-pool.md) met Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="36e80-104">This topic shows you how toomanage scalable [elastic pools](sql-database-elastic-pool.md) with Transact-SQL.</span></span>  <span data-ttu-id="36e80-105">U kunt ook maken en beheren van een Azure elastische pool Hallo [Azure-portal](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), Hallo REST-API of [C#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="36e80-105">You can also create and manage an Azure elastic pool hello [Azure portal](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), hello REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="36e80-106">U kunt ook maken en databases verplaatsen naar en van elastische pools met [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span><span class="sxs-lookup"><span data-stu-id="36e80-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>


<span data-ttu-id="36e80-107">Gebruik Hallo [Create Database (Azure SQL Database)](https://msdn.microsoft.com/library/dn268335.aspx) en [Alter Database(Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) toocreate en de verplaatsing databases opdrachten naar en van elastische pools.</span><span class="sxs-lookup"><span data-stu-id="36e80-107">Use hello [Create Database (Azure SQL Database)](https://msdn.microsoft.com/library/dn268335.aspx) and [Alter Database(Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) commands toocreate and move databases into and out of elastic pools.</span></span> <span data-ttu-id="36e80-108">Hallo elastische groep moet bestaan voordat u deze opdrachten kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="36e80-108">hello elastic pool must exist before you can use these commands.</span></span> <span data-ttu-id="36e80-109">Deze opdrachten beïnvloeden alleen databases.</span><span class="sxs-lookup"><span data-stu-id="36e80-109">These commands affect only databases.</span></span> <span data-ttu-id="36e80-110">Maken van nieuwe toepassingen en Hallo instellen van eigenschappen van de groep van toepassingen (zoals min en max edtu's) kunnen niet worden gewijzigd met T-SQL-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="36e80-110">Creation of new pools and hello setting of pool properties (such as min and max eDTUs) cannot be changed with T-SQL commands.</span></span>

## <a name="create-a-pooled-database-in-an-elastic-pool"></a><span data-ttu-id="36e80-111">Maak een gegroepeerde database in een elastische pool</span><span class="sxs-lookup"><span data-stu-id="36e80-111">Create a pooled database in an elastic pool</span></span>
<span data-ttu-id="36e80-112">Hallo CREATE DATABASE opdracht Hello SERVICE_OBJECTIVE-optie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="36e80-112">Use hello CREATE DATABASE command with hello SERVICE_OBJECTIVE option.</span></span>   

    CREATE DATABASE db1 ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3M100] ));
    -- Create a database named db1 in an elastic named S3M100.

<span data-ttu-id="36e80-113">Alle databases in een elastische groep overgenomen door de servicelaag Hallo van Hallo elastische pool (Basic, Standard, Premium).</span><span class="sxs-lookup"><span data-stu-id="36e80-113">All databases in an elastic pool inherit hello service tier of hello elastic pool (Basic, Standard, Premium).</span></span> 

## <a name="move-a-database-between-elastic-pools"></a><span data-ttu-id="36e80-114">Een database verplaatst tussen elastische pools</span><span class="sxs-lookup"><span data-stu-id="36e80-114">Move a database between elastic pools</span></span>
<span data-ttu-id="36e80-115">Gebruik de opdracht ALTER DATABASE Hallo Hello wijzigen en stel SERVICE\_SERVICEDOELSTELLING optie ELASTISCHE\_van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="36e80-115">Use hello ALTER DATABASE command with hello MODIFY and set SERVICE\_OBJECTIVE option as ELASTIC\_POOL.</span></span> <span data-ttu-id="36e80-116">Hallo naam toohello naam van de doelgroep Hallo instellen.</span><span class="sxs-lookup"><span data-stu-id="36e80-116">Set hello name toohello name of hello target pool.</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [PM125] ));
    -- Move hello database named db1 tooan elastic named P1M125  

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="36e80-117">Een database verplaatsen naar een elastische pool</span><span class="sxs-lookup"><span data-stu-id="36e80-117">Move a database into an elastic pool</span></span>
<span data-ttu-id="36e80-118">Gebruik de opdracht ALTER DATABASE Hallo Hello wijzigen en stel SERVICE\_OBJECTIVE optie ELASTIC_POOL.</span><span class="sxs-lookup"><span data-stu-id="36e80-118">Use hello ALTER DATABASE command with hello MODIFY and set SERVICE\_OBJECTIVE option as ELASTIC_POOL.</span></span> <span data-ttu-id="36e80-119">Hallo naam toohello naam van de doelgroep Hallo instellen.</span><span class="sxs-lookup"><span data-stu-id="36e80-119">Set hello name toohello name of hello target pool.</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3100] ));
    -- Move hello database named db1 tooan elastic named S3100.

## <a name="move-a-database-out-of-an-elastic-pool"></a><span data-ttu-id="36e80-120">Een database verplaatst buiten een elastische pool</span><span class="sxs-lookup"><span data-stu-id="36e80-120">Move a database out of an elastic pool</span></span>
<span data-ttu-id="36e80-121">Gebruik de opdracht ALTER DATABASE Hallo en Hallo SERVICE_OBJECTIVE tooone Hallo prestatieniveaus (zoals S0 of S1) ingesteld.</span><span class="sxs-lookup"><span data-stu-id="36e80-121">Use hello ALTER DATABASE command and set hello SERVICE_OBJECTIVE tooone of hello performance levels (such as S0 or S1).</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = 'S1');
    -- Changes hello database into a stand-alone database with hello service objective S1.

## <a name="list-databases-in-an-elastic-pool"></a><span data-ttu-id="36e80-122">Lijst met databases in een elastische pool</span><span class="sxs-lookup"><span data-stu-id="36e80-122">List databases in an elastic pool</span></span>
<span data-ttu-id="36e80-123">Gebruik Hallo [sys.database\_service \_doelstellingen weergave](https://msdn.microsoft.com/library/mt712619) toolist alle databases in een elastische pool Hallo.</span><span class="sxs-lookup"><span data-stu-id="36e80-123">Use hello [sys.database\_service \_objectives view](https://msdn.microsoft.com/library/mt712619) toolist all hello databases in an elastic pool.</span></span> <span data-ttu-id="36e80-124">Meld u bij toohello master databaseweergave tooquery Hallo.</span><span class="sxs-lookup"><span data-stu-id="36e80-124">Log in toohello master database tooquery hello view.</span></span>

    SELECT d.name, slo.*  
    FROM sys.databases d 
    JOIN sys.database_service_objectives slo  
    ON d.database_id = slo.database_id
    WHERE elastic_pool_name = 'MyElasticPool'; 

## <a name="get-resource-usage-data-for-an-elastic-pool"></a><span data-ttu-id="36e80-125">Gegevens over brongebruik ophalen voor een elastische pool</span><span class="sxs-lookup"><span data-stu-id="36e80-125">Get resource usage data for an elastic pool</span></span>
<span data-ttu-id="36e80-126">Gebruik Hallo [sys.elastic\_groep \_resource \_weergave van statistieken](https://msdn.microsoft.com/library/mt280062.aspx) tooexamine Hallo resource gebruiksstatistieken van een elastische pool op een logische server.</span><span class="sxs-lookup"><span data-stu-id="36e80-126">Use hello [sys.elastic\_pool \_resource \_stats view](https://msdn.microsoft.com/library/mt280062.aspx) tooexamine hello resource usage statistics of an elastic pool on a logical server.</span></span> <span data-ttu-id="36e80-127">Meld u bij toohello master databaseweergave tooquery Hallo.</span><span class="sxs-lookup"><span data-stu-id="36e80-127">Log in toohello master database tooquery hello view.</span></span>

    SELECT * FROM sys.elastic_pool_resource_stats 
    WHERE elastic_pool_name = 'MyElasticPool'
    ORDER BY end_time DESC;

## <a name="get-resource-usage-for-a-pooled-database"></a><span data-ttu-id="36e80-128">Resourcegebruik ophalen voor een gegroepeerde database</span><span class="sxs-lookup"><span data-stu-id="36e80-128">Get resource usage for a pooled database</span></span>
<span data-ttu-id="36e80-129">Gebruik Hallo [sys.dm\_ db\_ resource\_weergave van statistieken](https://msdn.microsoft.com/library/dn800981.aspx) of [sys.resource \_weergave van statistieken](https://msdn.microsoft.com/library/dn269979.aspx) tooexamine Hallo resource gebruiksstatistieken van een de database in een elastische pool.</span><span class="sxs-lookup"><span data-stu-id="36e80-129">Use hello [sys.dm\_ db\_ resource\_stats view](https://msdn.microsoft.com/library/dn800981.aspx) or [sys.resource \_stats view](https://msdn.microsoft.com/library/dn269979.aspx) tooexamine hello resource usage statistics of a database in an elastic pool.</span></span> <span data-ttu-id="36e80-130">Dit proces is vergelijkbaar tooquerying Resourcegebruik voor één database.</span><span class="sxs-lookup"><span data-stu-id="36e80-130">This process is similar tooquerying resource usage for a single database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="36e80-131">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="36e80-131">Next steps</span></span>
<span data-ttu-id="36e80-132">Nadat een elastische groep is gemaakt, kunt u Elastische databases in de groep Hallo beheren met elastische taken maken.</span><span class="sxs-lookup"><span data-stu-id="36e80-132">After creating an elastic pool, you can manage elastic databases in hello pool by creating elastic jobs.</span></span> <span data-ttu-id="36e80-133">Elastische taken vergemakkelijken uitgevoerd T-SQL-scripts uitvoeren op een willekeurig aantal databases in de groep Hallo.</span><span class="sxs-lookup"><span data-stu-id="36e80-133">Elastic jobs facilitate running T-SQL scripts against any number of databases in hello pool.</span></span> <span data-ttu-id="36e80-134">Zie voor meer informatie [elastische database taken overzicht](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="36e80-134">For more information, see [Elastic database jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

<span data-ttu-id="36e80-135">Zie [uitbreiden met Azure SQL Database](sql-database-elastic-scale-introduction.md): gebruik elastische database extra tooscale uit, verplaatsen van gegevens, opvragen of transacties maken.</span><span class="sxs-lookup"><span data-stu-id="36e80-135">See [Scaling out with Azure SQL Database](sql-database-elastic-scale-introduction.md): use elastic database tools tooscale out, move data, query, or create transactions.</span></span>

