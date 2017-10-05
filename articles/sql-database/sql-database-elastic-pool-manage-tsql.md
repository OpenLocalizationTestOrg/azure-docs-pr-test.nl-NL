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
# <a name="monitor-and-manage-an-elastic-pool-with-transact-sql"></a>Bewaken en beheren van een elastische groep met Transact-SQL
In dit onderwerp wordt beschreven hoe u voor het beheren van schaalbare [elastische pools](sql-database-elastic-pool.md) met Transact-SQL.  U kunt ook maken en een elastische pool in Azure beheren de [Azure-portal](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), de REST-API of [C#](sql-database-elastic-pool-manage-csharp.md). U kunt ook maken en databases verplaatsen naar en van elastische pools met [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).


Gebruik de [Create Database (Azure SQL Database)](https://msdn.microsoft.com/library/dn268335.aspx) en [Database(Azure SQL Database) Alter](https://msdn.microsoft.com/library/mt574871.aspx) opdrachten voor het maken en databases verplaatsen naar en van elastische pools. De elastische groep moet bestaan voordat u deze opdrachten kunt gebruiken. Deze opdrachten beïnvloeden alleen databases. Maken van nieuwe groepen en het instellen van eigenschappen van de groep van toepassingen (zoals min en max edtu's) kunnen niet worden gewijzigd met T-SQL-opdrachten.

## <a name="create-a-pooled-database-in-an-elastic-pool"></a>Maak een gegroepeerde database in een elastische pool
Gebruik de opdracht CREATE DATABASE met de optie SERVICE_OBJECTIVE.   

    CREATE DATABASE db1 ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3M100] ));
    -- Create a database named db1 in an elastic named S3M100.

Alle databases in een elastische groep overgenomen door de servicelaag van de elastische pool (Basic, Standard, Premium). 

## <a name="move-a-database-between-elastic-pools"></a>Een database verplaatst tussen elastische pools
Gebruik de opdracht ALTER DATABASE met de wijzigen en stel SERVICE\_SERVICEDOELSTELLING optie ELASTISCHE\_van toepassingen. De naam instellen op de naam van de doelgroep.

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [PM125] ));
    -- Move the database named db1 to an elastic named P1M125  

## <a name="move-a-database-into-an-elastic-pool"></a>Een database verplaatsen naar een elastische pool
Gebruik de opdracht ALTER DATABASE met de wijzigen en stel SERVICE\_OBJECTIVE optie ELASTIC_POOL. De naam instellen op de naam van de doelgroep.

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3100] ));
    -- Move the database named db1 to an elastic named S3100.

## <a name="move-a-database-out-of-an-elastic-pool"></a>Een database verplaatst buiten een elastische pool
Gebruik de opdracht ALTER DATABASE en SERVICE_OBJECTIVE ingesteld op een van de prestaties (zoals S0 of S1).

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = 'S1');
    -- Changes the database into a stand-alone database with the service objective S1.

## <a name="list-databases-in-an-elastic-pool"></a>Lijst met databases in een elastische pool
Gebruik de [sys.database\_service \_doelstellingen weergave](https://msdn.microsoft.com/library/mt712619) voor een lijst met alle databases in een elastische pool. Meld u aan bij de master database query uitvoeren op de weergave.

    SELECT d.name, slo.*  
    FROM sys.databases d 
    JOIN sys.database_service_objectives slo  
    ON d.database_id = slo.database_id
    WHERE elastic_pool_name = 'MyElasticPool'; 

## <a name="get-resource-usage-data-for-an-elastic-pool"></a>Gegevens over brongebruik ophalen voor een elastische pool
Gebruik de [sys.elastic\_groep \_resource \_weergave van statistieken](https://msdn.microsoft.com/library/mt280062.aspx) onderzoeken gebruiksstatistieken voor de bron van een elastische pool op een logische server. Meld u aan bij de master database query uitvoeren op de weergave.

    SELECT * FROM sys.elastic_pool_resource_stats 
    WHERE elastic_pool_name = 'MyElasticPool'
    ORDER BY end_time DESC;

## <a name="get-resource-usage-for-a-pooled-database"></a>Resourcegebruik ophalen voor een gegroepeerde database
Gebruik de [sys.dm\_ db\_ resource\_weergave van statistieken](https://msdn.microsoft.com/library/dn800981.aspx) of [sys.resource \_weergave van statistieken](https://msdn.microsoft.com/library/dn269979.aspx) onderzoeken gebruiksstatistieken voor de bron van een database in een elastische pool. Dit proces is vergelijkbaar met het Resourcegebruik voor één database opvragen.

## <a name="next-steps"></a>Volgende stappen
Nadat een elastische groep is gemaakt, kunt u Elastische databases in de pool beheren met elastische taken maken. Elastische taken vergemakkelijken actieve T-SQL-scripts uitvoeren op een willekeurig aantal databases in de pool. Zie voor meer informatie [elastische database taken overzicht](sql-database-elastic-jobs-overview.md). 

Zie [uitbreiden met Azure SQL Database](sql-database-elastic-scale-introduction.md): gebruik elastische database-hulpmiddelen om uitschalen, het verplaatsen van gegevens, opvragen of transacties maken.

