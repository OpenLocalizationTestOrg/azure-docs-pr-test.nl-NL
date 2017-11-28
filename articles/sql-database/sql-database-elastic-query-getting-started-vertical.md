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
# <a name="get-started-with-cross-database-queries-vertical-partitioning-preview"></a><span data-ttu-id="9d07f-103">Aan de slag met meerdere databases query's (verticale partities) (preview)</span><span class="sxs-lookup"><span data-stu-id="9d07f-103">Get started with cross-database queries (vertical partitioning) (preview)</span></span>
<span data-ttu-id="9d07f-104">Elastische database kunt (preview) voor Azure SQL Database u query toorun T-SQL-query's die meerdere databases met behulp van één verbindingspunt omvatten.</span><span class="sxs-lookup"><span data-stu-id="9d07f-104">Elastic database query (preview) for Azure SQL Database allows you toorun T-SQL queries that span multiple databases using a single connection point.</span></span> <span data-ttu-id="9d07f-105">Dit onderwerp geldt te[verticaal gepartitioneerd databases](sql-database-elastic-query-vertical-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="9d07f-105">This topic applies too[vertically partitioned databases](sql-database-elastic-query-vertical-partitioning.md).</span></span>  

<span data-ttu-id="9d07f-106">Wanneer voltooid, wordt u: meer informatie over hoe tooconfigure en het gebruik van een Azure SQL Database-tooperform query's die bestaan meerdere verwante databases.</span><span class="sxs-lookup"><span data-stu-id="9d07f-106">When completed, you will: learn how tooconfigure and use an Azure SQL Database tooperform queries that span multiple related databases.</span></span> 

<span data-ttu-id="9d07f-107">Zie voor meer informatie over Hallo elastische database query functie [overzicht van Azure SQL Database elastische database query](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9d07f-107">For more information about hello elastic database query feature, please see  [Azure SQL Database elastic database query overview](sql-database-elastic-query-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="9d07f-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="9d07f-108">Prerequisites</span></span>

<span data-ttu-id="9d07f-109">U moet beschikken over een externe gegevensbron ALTER machtiging.</span><span class="sxs-lookup"><span data-stu-id="9d07f-109">You must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="9d07f-110">Deze machtiging is opgenomen in de machtiging ALTER DATABASE Hallo.</span><span class="sxs-lookup"><span data-stu-id="9d07f-110">This permission is included with hello ALTER DATABASE permission.</span></span> <span data-ttu-id="9d07f-111">EEN externe gegevensbron ALTER machtigingen zijn vereist toorefer toohello onderliggende gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="9d07f-111">ALTER ANY EXTERNAL DATA SOURCE permissions are needed toorefer toohello underlying data source.</span></span>

## <a name="create-hello-sample-databases"></a><span data-ttu-id="9d07f-112">Hallo voorbeelddatabases maken</span><span class="sxs-lookup"><span data-stu-id="9d07f-112">Create hello sample databases</span></span>
<span data-ttu-id="9d07f-113">toostart met moeten we twee databases toocreate: **klanten** en **Orders**, zich in dezelfde of een andere logische servers Hallo.</span><span class="sxs-lookup"><span data-stu-id="9d07f-113">toostart with, we need toocreate two databases, **Customers** and **Orders**, either in hello same or different logical servers.</span></span>   

<span data-ttu-id="9d07f-114">Uitvoeren van query's volgen op Hallo Hallo **Orders** database toocreate hello **OrderInformation** tabel en invoer Hallo voorbeeldgegevens.</span><span class="sxs-lookup"><span data-stu-id="9d07f-114">Execute hello following queries on hello **Orders** database toocreate hello **OrderInformation** table and input hello sample data.</span></span> 

    CREATE TABLE [dbo].[OrderInformation]( 
        [OrderID] [int] NOT NULL, 
        [CustomerID] [int] NOT NULL 
        ) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (123, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (149, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (857, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (321, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (564, 8) 

<span data-ttu-id="9d07f-115">Nu uitvoeren na de query op Hallo **klanten** database toocreate hello **CustomerInformation** tabel en invoer Hallo voorbeeldgegevens.</span><span class="sxs-lookup"><span data-stu-id="9d07f-115">Now, execute following query on hello **Customers** database toocreate hello **CustomerInformation** table and input hello sample data.</span></span> 

    CREATE TABLE [dbo].[CustomerInformation]( 
        [CustomerID] [int] NOT NULL, 
        [CustomerName] [varchar](50) NULL, 
        [Company] [varchar](50) NULL 
        CONSTRAINT [CustID] PRIMARY KEY CLUSTERED ([CustomerID] ASC) 
    ) 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (1, 'Jack', 'ABC') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (2, 'Steve', 'XYZ') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (3, 'Lylla', 'MNO') 

## <a name="create-database-objects"></a><span data-ttu-id="9d07f-116">Database-objecten maken</span><span class="sxs-lookup"><span data-stu-id="9d07f-116">Create database objects</span></span>
### <a name="database-scoped-master-key-and-credentials"></a><span data-ttu-id="9d07f-117">Database-scoped hoofdsleutel en referenties</span><span class="sxs-lookup"><span data-stu-id="9d07f-117">Database scoped master key and credentials</span></span>
1. <span data-ttu-id="9d07f-118">Open SQL Server Management Studio of SQL Server Data Tools in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9d07f-118">Open SQL Server Management Studio or SQL Server Data Tools in Visual Studio.</span></span>
2. <span data-ttu-id="9d07f-119">Verbinding maken met toohello orderdatabase en Voer Hallo volgende T-SQL-opdrachten:</span><span class="sxs-lookup"><span data-stu-id="9d07f-119">Connect toohello Orders database and execute hello following T-SQL commands:</span></span>
   
        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>'; 
        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred 
        WITH IDENTITY = '<username>', 
        SECRET = '<password>';  
   
    <span data-ttu-id="9d07f-120">Hallo 'gebruikersnaam' en 'password' moet Hallo gebruikersnaam en wachtwoord toologin in Hallo klanten database gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9d07f-120">hello "username" and "password" should be hello username and password used toologin into hello Customers database.</span></span>
    <span data-ttu-id="9d07f-121">Verificatie met behulp van Azure Active Directory met elastische query's is momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="9d07f-121">Authentication using Azure Active Directory with elastic queries is not currently supported.</span></span>

### <a name="external-data-sources"></a><span data-ttu-id="9d07f-122">Externe gegevensbronnen</span><span class="sxs-lookup"><span data-stu-id="9d07f-122">External data sources</span></span>
<span data-ttu-id="9d07f-123">een externe gegevensbron toocreate Hallo volgende opdracht uit op Hallo orderdatabase uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="9d07f-123">toocreate an external data source, execute hello following command on hello Orders database:</span></span> 

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH 
        (TYPE = RDBMS, 
        LOCATION = '<server_name>.database.windows.net', 
        DATABASE_NAME = 'Customers', 
        CREDENTIAL = ElasticDBQueryCred, 
    ) ;

### <a name="external-tables"></a><span data-ttu-id="9d07f-124">Externe tabellen</span><span class="sxs-lookup"><span data-stu-id="9d07f-124">External tables</span></span>
<span data-ttu-id="9d07f-125">Een externe tabel maken op Hallo Orders-database die overeenkomt met de Hallo definitie van Hallo CustomerInformation tabel:</span><span class="sxs-lookup"><span data-stu-id="9d07f-125">Create an external table on hello Orders database, which matches hello definition of hello CustomerInformation table:</span></span>

    CREATE EXTERNAL TABLE [dbo].[CustomerInformation] 
    ( [CustomerID] [int] NOT NULL, 
      [CustomerName] [varchar](50) NOT NULL, 
      [Company] [varchar](50) NOT NULL) 
    WITH 
    ( DATA_SOURCE = MyElasticDBQueryDataSrc) 

## <a name="execute-a-sample-elastic-database-t-sql-query"></a><span data-ttu-id="9d07f-126">Een voorbeeld elastische database T-SQL-query uitvoeren</span><span class="sxs-lookup"><span data-stu-id="9d07f-126">Execute a sample elastic database T-SQL query</span></span>
<span data-ttu-id="9d07f-127">Als u de externe gegevensbron en uw externe tabellen kunt u nu gebruiken T-SQL-tooquery uw externe tabellen hebt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="9d07f-127">Once you have defined your external data source and your external tables you can now use T-SQL tooquery your external tables.</span></span> <span data-ttu-id="9d07f-128">Voer deze query uit op Hallo orderdatabase:</span><span class="sxs-lookup"><span data-stu-id="9d07f-128">Execute this query on hello Orders database:</span></span> 

    SELECT OrderInformation.CustomerID, OrderInformation.OrderId, CustomerInformation.CustomerName, CustomerInformation.Company 
    FROM OrderInformation 
    INNER JOIN CustomerInformation 
    ON CustomerInformation.CustomerID = OrderInformation.CustomerID 

## <a name="cost"></a><span data-ttu-id="9d07f-129">Kosten</span><span class="sxs-lookup"><span data-stu-id="9d07f-129">Cost</span></span>
<span data-ttu-id="9d07f-130">Op dit moment is Hallo elastische database query functie opgenomen in Hallo kosten van uw Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="9d07f-130">Currently, hello elastic database query feature is included into hello cost of your Azure SQL Database.</span></span>  

<span data-ttu-id="9d07f-131">Zie voor informatie over prijzen [prijzen SQL Database](https://azure.microsoft.com/pricing/details/sql-database).</span><span class="sxs-lookup"><span data-stu-id="9d07f-131">For pricing information see [SQL Database Pricing](https://azure.microsoft.com/pricing/details/sql-database).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9d07f-132">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9d07f-132">Next steps</span></span>

* <span data-ttu-id="9d07f-133">Zie voor een overzicht van elastische query [elastische query overzicht](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9d07f-133">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="9d07f-134">Zie voor de syntaxis en voorbeelden query's voor verticaal gepartitioneerde gegevens [gegevens opvragen verticaal gepartitioneerd)](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="9d07f-134">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="9d07f-135">Zie voor een zelfstudie horizontaal partitioneren (sharding) [aan de slag met elastische query voor horizontale partitioneren (sharding)](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="9d07f-135">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="9d07f-136">Zie voor de syntaxis en voorbeelden query's voor horizontaal gepartitioneerde gegevens [gegevens opvragen horizontaal gepartitioneerd)](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="9d07f-136">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="9d07f-137">Zie [sp\_uitvoeren \_externe](https://msdn.microsoft.com/library/mt703714) voor een opgeslagen procedure die een Transact-SQL-instructie op een enkele externe Azure SQL Database of een set van databases die fungeren als shards in een horizontale partitieschema wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9d07f-137">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>