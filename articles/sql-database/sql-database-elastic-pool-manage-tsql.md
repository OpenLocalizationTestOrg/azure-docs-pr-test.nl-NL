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
# <a name="monitor-and-manage-an-elastic-pool-with-transact-sql"></a>Bewaken en beheren van een elastische groep met Transact-SQL
Dit onderwerp leest u hoe toomanage schaalbare [elastische pools](sql-database-elastic-pool.md) met Transact-SQL.  U kunt ook maken en beheren van een Azure elastische pool Hallo [Azure-portal](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), Hallo REST-API of [C#](sql-database-elastic-pool-manage-csharp.md). U kunt ook maken en databases verplaatsen naar en van elastische pools met [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).


Gebruik Hallo [Create Database (Azure SQL Database)](https://msdn.microsoft.com/library/dn268335.aspx) en [Alter Database(Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) toocreate en de verplaatsing databases opdrachten naar en van elastische pools. Hallo elastische groep moet bestaan voordat u deze opdrachten kunt gebruiken. Deze opdrachten beïnvloeden alleen databases. Maken van nieuwe toepassingen en Hallo instellen van eigenschappen van de groep van toepassingen (zoals min en max edtu's) kunnen niet worden gewijzigd met T-SQL-opdrachten.

## <a name="create-a-pooled-database-in-an-elastic-pool"></a>Maak een gegroepeerde database in een elastische pool
Hallo CREATE DATABASE opdracht Hello SERVICE_OBJECTIVE-optie gebruiken.   

    CREATE DATABASE db1 ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3M100] ));
    -- Create a database named db1 in an elastic named S3M100.

Alle databases in een elastische groep overgenomen door de servicelaag Hallo van Hallo elastische pool (Basic, Standard, Premium). 

## <a name="move-a-database-between-elastic-pools"></a>Een database verplaatst tussen elastische pools
Gebruik de opdracht ALTER DATABASE Hallo Hello wijzigen en stel SERVICE\_SERVICEDOELSTELLING optie ELASTISCHE\_van toepassingen. Hallo naam toohello naam van de doelgroep Hallo instellen.

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [PM125] ));
    -- Move hello database named db1 tooan elastic named P1M125  

## <a name="move-a-database-into-an-elastic-pool"></a>Een database verplaatsen naar een elastische pool
Gebruik de opdracht ALTER DATABASE Hallo Hello wijzigen en stel SERVICE\_OBJECTIVE optie ELASTIC_POOL. Hallo naam toohello naam van de doelgroep Hallo instellen.

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3100] ));
    -- Move hello database named db1 tooan elastic named S3100.

## <a name="move-a-database-out-of-an-elastic-pool"></a>Een database verplaatst buiten een elastische pool
Gebruik de opdracht ALTER DATABASE Hallo en Hallo SERVICE_OBJECTIVE tooone Hallo prestatieniveaus (zoals S0 of S1) ingesteld.

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = 'S1');
    -- Changes hello database into a stand-alone database with hello service objective S1.

## <a name="list-databases-in-an-elastic-pool"></a>Lijst met databases in een elastische pool
Gebruik Hallo [sys.database\_service \_doelstellingen weergave](https://msdn.microsoft.com/library/mt712619) toolist alle databases in een elastische pool Hallo. Meld u bij toohello master databaseweergave tooquery Hallo.

    SELECT d.name, slo.*  
    FROM sys.databases d 
    JOIN sys.database_service_objectives slo  
    ON d.database_id = slo.database_id
    WHERE elastic_pool_name = 'MyElasticPool'; 

## <a name="get-resource-usage-data-for-an-elastic-pool"></a>Gegevens over brongebruik ophalen voor een elastische pool
Gebruik Hallo [sys.elastic\_groep \_resource \_weergave van statistieken](https://msdn.microsoft.com/library/mt280062.aspx) tooexamine Hallo resource gebruiksstatistieken van een elastische pool op een logische server. Meld u bij toohello master databaseweergave tooquery Hallo.

    SELECT * FROM sys.elastic_pool_resource_stats 
    WHERE elastic_pool_name = 'MyElasticPool'
    ORDER BY end_time DESC;

## <a name="get-resource-usage-for-a-pooled-database"></a>Resourcegebruik ophalen voor een gegroepeerde database
Gebruik Hallo [sys.dm\_ db\_ resource\_weergave van statistieken](https://msdn.microsoft.com/library/dn800981.aspx) of [sys.resource \_weergave van statistieken](https://msdn.microsoft.com/library/dn269979.aspx) tooexamine Hallo resource gebruiksstatistieken van een de database in een elastische pool. Dit proces is vergelijkbaar tooquerying Resourcegebruik voor één database.

## <a name="next-steps"></a>Volgende stappen
Nadat een elastische groep is gemaakt, kunt u Elastische databases in de groep Hallo beheren met elastische taken maken. Elastische taken vergemakkelijken uitgevoerd T-SQL-scripts uitvoeren op een willekeurig aantal databases in de groep Hallo. Zie voor meer informatie [elastische database taken overzicht](sql-database-elastic-jobs-overview.md). 

Zie [uitbreiden met Azure SQL Database](sql-database-elastic-scale-introduction.md): gebruik elastische database extra tooscale uit, verplaatsen van gegevens, opvragen of transacties maken.

