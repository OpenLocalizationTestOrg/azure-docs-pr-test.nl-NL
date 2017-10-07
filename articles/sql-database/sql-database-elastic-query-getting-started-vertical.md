---
title: aaaGet gestart met meerdere databases query's (verticale partities) | Microsoft Docs
description: hoe toouse elastische databasequery met databases verticaal gepartitioneerd
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: e5b44b10-c432-4f96-b20e-08615ff4d5dd
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: torsteng
ms.openlocfilehash: 9e6183268e8bf87e3ac28f502711fcc05a7a3f52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-cross-database-queries-vertical-partitioning-preview"></a>Aan de slag met meerdere databases query's (verticale partities) (preview)
Elastische database kunt (preview) voor Azure SQL Database u query toorun T-SQL-query's die meerdere databases met behulp van één verbindingspunt omvatten. Dit onderwerp geldt te[verticaal gepartitioneerd databases](sql-database-elastic-query-vertical-partitioning.md).  

Wanneer voltooid, wordt u: meer informatie over hoe tooconfigure en het gebruik van een Azure SQL Database-tooperform query's die bestaan meerdere verwante databases. 

Zie voor meer informatie over Hallo elastische database query functie [overzicht van Azure SQL Database elastische database query](sql-database-elastic-query-overview.md). 

## <a name="prerequisites"></a>Vereisten

U moet beschikken over een externe gegevensbron ALTER machtiging. Deze machtiging is opgenomen in de machtiging ALTER DATABASE Hallo. EEN externe gegevensbron ALTER machtigingen zijn vereist toorefer toohello onderliggende gegevensbron.

## <a name="create-hello-sample-databases"></a>Hallo voorbeelddatabases maken
toostart met moeten we twee databases toocreate: **klanten** en **Orders**, zich in dezelfde of een andere logische servers Hallo.   

Uitvoeren van query's volgen op Hallo Hallo **Orders** database toocreate hello **OrderInformation** tabel en invoer Hallo voorbeeldgegevens. 

    CREATE TABLE [dbo].[OrderInformation]( 
        [OrderID] [int] NOT NULL, 
        [CustomerID] [int] NOT NULL 
        ) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (123, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (149, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (857, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (321, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (564, 8) 

Nu uitvoeren na de query op Hallo **klanten** database toocreate hello **CustomerInformation** tabel en invoer Hallo voorbeeldgegevens. 

    CREATE TABLE [dbo].[CustomerInformation]( 
        [CustomerID] [int] NOT NULL, 
        [CustomerName] [varchar](50) NULL, 
        [Company] [varchar](50) NULL 
        CONSTRAINT [CustID] PRIMARY KEY CLUSTERED ([CustomerID] ASC) 
    ) 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (1, 'Jack', 'ABC') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (2, 'Steve', 'XYZ') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (3, 'Lylla', 'MNO') 

## <a name="create-database-objects"></a>Database-objecten maken
### <a name="database-scoped-master-key-and-credentials"></a>Database-scoped hoofdsleutel en referenties
1. Open SQL Server Management Studio of SQL Server Data Tools in Visual Studio.
2. Verbinding maken met toohello orderdatabase en Voer Hallo volgende T-SQL-opdrachten:
   
        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>'; 
        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred 
        WITH IDENTITY = '<username>', 
        SECRET = '<password>';  
   
    Hallo 'gebruikersnaam' en 'password' moet Hallo gebruikersnaam en wachtwoord toologin in Hallo klanten database gebruikt.
    Verificatie met behulp van Azure Active Directory met elastische query's is momenteel niet ondersteund.

### <a name="external-data-sources"></a>Externe gegevensbronnen
een externe gegevensbron toocreate Hallo volgende opdracht uit op Hallo orderdatabase uitvoeren: 

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH 
        (TYPE = RDBMS, 
        LOCATION = '<server_name>.database.windows.net', 
        DATABASE_NAME = 'Customers', 
        CREDENTIAL = ElasticDBQueryCred, 
    ) ;

### <a name="external-tables"></a>Externe tabellen
Een externe tabel maken op Hallo Orders-database die overeenkomt met de Hallo definitie van Hallo CustomerInformation tabel:

    CREATE EXTERNAL TABLE [dbo].[CustomerInformation] 
    ( [CustomerID] [int] NOT NULL, 
      [CustomerName] [varchar](50) NOT NULL, 
      [Company] [varchar](50) NOT NULL) 
    WITH 
    ( DATA_SOURCE = MyElasticDBQueryDataSrc) 

## <a name="execute-a-sample-elastic-database-t-sql-query"></a>Een voorbeeld elastische database T-SQL-query uitvoeren
Als u de externe gegevensbron en uw externe tabellen kunt u nu gebruiken T-SQL-tooquery uw externe tabellen hebt gedefinieerd. Voer deze query uit op Hallo orderdatabase: 

    SELECT OrderInformation.CustomerID, OrderInformation.OrderId, CustomerInformation.CustomerName, CustomerInformation.Company 
    FROM OrderInformation 
    INNER JOIN CustomerInformation 
    ON CustomerInformation.CustomerID = OrderInformation.CustomerID 

## <a name="cost"></a>Kosten
Op dit moment is Hallo elastische database query functie opgenomen in Hallo kosten van uw Azure SQL Database.  

Zie voor informatie over prijzen [prijzen SQL Database](https://azure.microsoft.com/pricing/details/sql-database). 

## <a name="next-steps"></a>Volgende stappen

* Zie voor een overzicht van elastische query [elastische query overzicht](sql-database-elastic-query-overview.md).
* Zie voor de syntaxis en voorbeelden query's voor verticaal gepartitioneerde gegevens [gegevens opvragen verticaal gepartitioneerd)](sql-database-elastic-query-vertical-partitioning.md)
* Zie voor een zelfstudie horizontaal partitioneren (sharding) [aan de slag met elastische query voor horizontale partitioneren (sharding)](sql-database-elastic-query-getting-started.md).
* Zie voor de syntaxis en voorbeelden query's voor horizontaal gepartitioneerde gegevens [gegevens opvragen horizontaal gepartitioneerd)](sql-database-elastic-query-horizontal-partitioning.md)
* Zie [sp\_uitvoeren \_externe](https://msdn.microsoft.com/library/mt703714) voor een opgeslagen procedure die een Transact-SQL-instructie op een enkele externe Azure SQL Database of een set van databases die fungeren als shards in een horizontale partitieschema wordt uitgevoerd.