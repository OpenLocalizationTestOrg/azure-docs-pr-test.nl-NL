---
title: Hulpprogramma voor migratie van database voor Azure Cosmos DB | Microsoft Docs
description: Informatie over het gebruik van de open-source Azure Cosmos DB hulpprogramma's voor gegevensmigratie voor het importeren van gegevens naar Azure Cosmos DB uit diverse bronnen, met inbegrip van MongoDB, SQL Server, Table storage, Amazon DynamoDB, CSV en JSON-bestanden. CSV naar JSON converteren.
keywords: CSV in json, 's voor migratie van databases, csv niet converteren naar json
services: cosmos-db
author: andrewhoh
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: d173581d-782a-445c-98d9-5e3c49b00e25
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: anhoh
ms.custom: mvc
ms.openlocfilehash: 23a4a82dbdb611f4da90562af936fca28da9b24d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-import-data-into-azure-cosmos-db-for-the-documentdb-api"></a><span data-ttu-id="48d0b-105">Het importeren van gegevens in Azure Cosmos DB voor de API DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="48d0b-105">How to import data into Azure Cosmos DB for the DocumentDB API?</span></span>

<span data-ttu-id="48d0b-106">Deze zelfstudie bevat instructies over het gebruik van de Cosmos Azure DB: hulpprogramma voor gegevensmigratie voor DocumentDB-API, die u gegevens uit diverse bronnen importeren kunt, met inbegrip van JSON-bestanden, CSV-bestanden, SQL, MongoDB, Azure Table storage, Amazon DynamoDB en Azure Cosmos DB DocumentDB-API verzamelingen in verzamelingen voor gebruik met Azure Cosmos DB en de DocumentDB-API.</span><span class="sxs-lookup"><span data-stu-id="48d0b-106">This tutorial provides instructions on using the Azure Cosmos DB: DocumentDB API Data Migration tool, which can import data from various sources, including JSON files, CSV files, SQL, MongoDB, Azure Table storage, Amazon DynamoDB and Azure Cosmos DB DocumentDB API collections into collections for use with Azure Cosmos DB and the DocumentDB API.</span></span> <span data-ttu-id="48d0b-107">Het hulpprogramma voor migratie van gegevens kan ook worden gebruikt bij het migreren van een verzameling van één partitie in een verzameling met meerdere partitie voor de DocumentDB-API.</span><span class="sxs-lookup"><span data-stu-id="48d0b-107">The Data Migration tool can also be used when migrating from a single partition collection to a multi-partition collection for the DocumentDB API.</span></span>

<span data-ttu-id="48d0b-108">Het hulpprogramma voor gegevensmigratie werkt alleen wanneer het importeren van gegevens naar Azure Cosmos DB voor gebruik met de DocumentDB-API.</span><span class="sxs-lookup"><span data-stu-id="48d0b-108">The Data Migration tool only works when importing data into Azure Cosmos DB for use with the DocumentDB API.</span></span> <span data-ttu-id="48d0b-109">Het importeren van gegevens voor gebruik met de API van de tabel of Graph API wordt niet ondersteund op dit moment.</span><span class="sxs-lookup"><span data-stu-id="48d0b-109">Importing data for use with the Table API or Graph API is not supported at this time.</span></span> 

<span data-ttu-id="48d0b-110">Om gegevens te importeren voor gebruik met de MongoDB-API, Zie [Azure Cosmos DB: het migreren van gegevens voor de MongoDB-API?](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="48d0b-110">To import data for use with the MongoDB API, see [Azure Cosmos DB: How to migrate data for the MongoDB API?](mongodb-migrate.md).</span></span>

<span data-ttu-id="48d0b-111">Deze zelfstudie bevat de volgende taken:</span><span class="sxs-lookup"><span data-stu-id="48d0b-111">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="48d0b-112">Het hulpprogramma voor gegevensmigratie installeren</span><span class="sxs-lookup"><span data-stu-id="48d0b-112">Installing the Data Migration tool</span></span>
> * <span data-ttu-id="48d0b-113">Het importeren van gegevens uit verschillende gegevensbronnen</span><span class="sxs-lookup"><span data-stu-id="48d0b-113">Importing data from different data sources</span></span>
> * <span data-ttu-id="48d0b-114">Exporteren van Azure Cosmos DB naar JSON</span><span class="sxs-lookup"><span data-stu-id="48d0b-114">Exporting from Azure Cosmos DB to JSON</span></span>

## <span data-ttu-id="48d0b-115"><a id="Prerequisites"></a>Vereisten</span><span class="sxs-lookup"><span data-stu-id="48d0b-115"><a id="Prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="48d0b-116">Voordat u de instructies in dit artikel uitvoert, zorg ervoor dat u het volgende zijn geïnstalleerd hebt:</span><span class="sxs-lookup"><span data-stu-id="48d0b-116">Before following the instructions in this article, ensure that you have the following installed:</span></span>

* <span data-ttu-id="48d0b-117">[Microsoft .NET Framework 4,51](https://www.microsoft.com/download/developer-tools.aspx) of hoger.</span><span class="sxs-lookup"><span data-stu-id="48d0b-117">[Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) or higher.</span></span>

## <span data-ttu-id="48d0b-118"><a id="Overviewl"></a>Overzicht van het hulpprogramma voor migratie van gegevens</span><span class="sxs-lookup"><span data-stu-id="48d0b-118"><a id="Overviewl"></a>Overview of the Data Migration tool</span></span>
<span data-ttu-id="48d0b-119">Het hulpprogramma voor migratie van gegevens is een open-source-oplossing waarmee gegevens worden geïmporteerd met Azure Cosmos DB uit diverse bronnen, met inbegrip van:</span><span class="sxs-lookup"><span data-stu-id="48d0b-119">The Data Migration tool is an open source solution that imports data to Azure Cosmos DB from a variety of sources, including:</span></span>

* <span data-ttu-id="48d0b-120">JSON-bestanden</span><span class="sxs-lookup"><span data-stu-id="48d0b-120">JSON files</span></span>
* <span data-ttu-id="48d0b-121">MongoDB</span><span class="sxs-lookup"><span data-stu-id="48d0b-121">MongoDB</span></span>
* <span data-ttu-id="48d0b-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="48d0b-122">SQL Server</span></span>
* <span data-ttu-id="48d0b-123">CSV-bestanden</span><span class="sxs-lookup"><span data-stu-id="48d0b-123">CSV files</span></span>
* <span data-ttu-id="48d0b-124">Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="48d0b-124">Azure Table storage</span></span>
* <span data-ttu-id="48d0b-125">Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="48d0b-125">Amazon DynamoDB</span></span>
* <span data-ttu-id="48d0b-126">HBase</span><span class="sxs-lookup"><span data-stu-id="48d0b-126">HBase</span></span>
* <span data-ttu-id="48d0b-127">Azure DB Cosmos-verzamelingen</span><span class="sxs-lookup"><span data-stu-id="48d0b-127">Azure Cosmos DB collections</span></span>

<span data-ttu-id="48d0b-128">Terwijl het hulpprogramma voor importeren, bevat een grafische gebruikersinterface (dtui.exe), kan het ook aangestuurd vanaf de opdrachtregel (dt.exe).</span><span class="sxs-lookup"><span data-stu-id="48d0b-128">While the import tool includes a graphical user interface (dtui.exe), it can also be driven from the command line (dt.exe).</span></span> <span data-ttu-id="48d0b-129">Er is in feite een optie voor uitvoer van de bijbehorende opdracht na het instellen van een import via de gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="48d0b-129">In fact, there is an option to output the associated command after setting up an import through the UI.</span></span> <span data-ttu-id="48d0b-130">In tabelvorm brongegevens (bijvoorbeeld SQL Server- of CSV-bestanden) kan worden getransformeerd zodat hiërarchische relaties (subdocumenten) kunnen worden gemaakt tijdens het importeren.</span><span class="sxs-lookup"><span data-stu-id="48d0b-130">Tabular source data (e.g. SQL Server or CSV files) can be transformed such that hierarchical relationships (subdocuments) can be created during import.</span></span> <span data-ttu-id="48d0b-131">Houd lezen voor meer informatie over opties voor gegevensbron steekproef van opdrachtregels voor het importeren uit elke bron, doel-opties en importeren van de weer te geven resultaten.</span><span class="sxs-lookup"><span data-stu-id="48d0b-131">Keep reading to learn more about source options, sample command lines to import from each source, target options, and viewing import results.</span></span>

## <span data-ttu-id="48d0b-132"><a id="Install"></a>Het hulpprogramma voor gegevensmigratie installeren</span><span class="sxs-lookup"><span data-stu-id="48d0b-132"><a id="Install"></a>Install the Data Migration tool</span></span>
<span data-ttu-id="48d0b-133">De broncode van de migratie-hulpprogramma is beschikbaar op GitHub in [deze opslagplaats](https://github.com/azure/azure-documentdb-datamigrationtool) en een gecompileerde versie is beschikbaar vanuit [Microsoft Download Center](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d).</span><span class="sxs-lookup"><span data-stu-id="48d0b-133">The migration tool source code is available on GitHub in [this repository](https://github.com/azure/azure-documentdb-datamigrationtool) and a compiled version is available from [Microsoft Download Center](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d).</span></span> <span data-ttu-id="48d0b-134">U kunt compileren van de oplossing of gewoon downloaden en uitpakken van de gecompileerde versie naar een map van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="48d0b-134">You may either compile the solution or simply download and extract the compiled version to a directory of your choice.</span></span> <span data-ttu-id="48d0b-135">Voer vervolgens een:</span><span class="sxs-lookup"><span data-stu-id="48d0b-135">Then run either:</span></span>

* <span data-ttu-id="48d0b-136">**Dtui.exe**: versie van de grafische interface van het hulpprogramma</span><span class="sxs-lookup"><span data-stu-id="48d0b-136">**Dtui.exe**: Graphical interface version of the tool</span></span>
* <span data-ttu-id="48d0b-137">**DT.exe**: opdrachtregelprogramma versie van het hulpprogramma</span><span class="sxs-lookup"><span data-stu-id="48d0b-137">**Dt.exe**: Command-line version of the tool</span></span>

## <a name="import-data"></a><span data-ttu-id="48d0b-138">Gegevens importeren</span><span class="sxs-lookup"><span data-stu-id="48d0b-138">Import data</span></span>

<span data-ttu-id="48d0b-139">Nadat u het hulpprogramma hebt geïnstalleerd, is het tijd om uw gegevens te importeren.</span><span class="sxs-lookup"><span data-stu-id="48d0b-139">Once you've installed the tool, it's time to import your data.</span></span> <span data-ttu-id="48d0b-140">Welk type gegevens wilt u gebruiken om te importeren?</span><span class="sxs-lookup"><span data-stu-id="48d0b-140">What kind of data do you want to import?</span></span>

* [<span data-ttu-id="48d0b-141">JSON-bestanden</span><span class="sxs-lookup"><span data-stu-id="48d0b-141">JSON files</span></span>](#JSON)
* [<span data-ttu-id="48d0b-142">MongoDB</span><span class="sxs-lookup"><span data-stu-id="48d0b-142">MongoDB</span></span>](#MongoDB)
* [<span data-ttu-id="48d0b-143">MongoDB exportbestanden</span><span class="sxs-lookup"><span data-stu-id="48d0b-143">MongoDB Export files</span></span>](#MongoDBExport)
* [<span data-ttu-id="48d0b-144">SQL Server</span><span class="sxs-lookup"><span data-stu-id="48d0b-144">SQL Server</span></span>](#SQL)
* [<span data-ttu-id="48d0b-145">CSV-bestanden</span><span class="sxs-lookup"><span data-stu-id="48d0b-145">CSV files</span></span>](#CSV)
* [<span data-ttu-id="48d0b-146">Azure Table storage</span><span class="sxs-lookup"><span data-stu-id="48d0b-146">Azure Table storage</span></span>](#AzureTableSource)
* [<span data-ttu-id="48d0b-147">Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="48d0b-147">Amazon DynamoDB</span></span>](#DynamoDBSource)
* [<span data-ttu-id="48d0b-148">BLOB</span><span class="sxs-lookup"><span data-stu-id="48d0b-148">Blob</span></span>](#BlobImport)
* [<span data-ttu-id="48d0b-149">Azure DB Cosmos-verzamelingen</span><span class="sxs-lookup"><span data-stu-id="48d0b-149">Azure Cosmos DB collections</span></span>](#DocumentDBSource)
* [<span data-ttu-id="48d0b-150">HBase</span><span class="sxs-lookup"><span data-stu-id="48d0b-150">HBase</span></span>](#HBaseSource)
* [<span data-ttu-id="48d0b-151">Azure DB Cosmos bulkimport</span><span class="sxs-lookup"><span data-stu-id="48d0b-151">Azure Cosmos DB bulk import</span></span>](#DocumentDBBulkImport)
* [<span data-ttu-id="48d0b-152">Azure DB Cosmos sequentiële record importeren</span><span class="sxs-lookup"><span data-stu-id="48d0b-152">Azure Cosmos DB sequential record import</span></span>](#DocumentDSeqTarget)


## <span data-ttu-id="48d0b-153"><a id="JSON"></a>JSON-bestanden importeren</span><span class="sxs-lookup"><span data-stu-id="48d0b-153"><a id="JSON"></a>To import JSON files</span></span>
<span data-ttu-id="48d0b-154">De optie voor de gegevensbron importfunctie van JSON-bestand kunt u wilt importeren een of meer JSON-bestanden voor één document of JSON-bestanden dat elk een matrix met JSON-documenten bevatten.</span><span class="sxs-lookup"><span data-stu-id="48d0b-154">The JSON file source importer option allows you to import one or more single document JSON files or JSON files that each contain an array of JSON documents.</span></span> <span data-ttu-id="48d0b-155">Bij het toevoegen van mappen met JSON-bestanden te importeren, hebt u de mogelijkheid van recursief zoeken naar bestanden in submappen.</span><span class="sxs-lookup"><span data-stu-id="48d0b-155">When adding folders that contain JSON files to import, you have the option of recursively searching for files in subfolders.</span></span>

![Schermopname van JSON-bestand bronopties - hulpprogramma's voor migratie](./media/import-data/jsonsource.png)

<span data-ttu-id="48d0b-157">Hier volgen enkele voorbeelden vanaf de opdrachtregel voor het importeren van JSON-bestanden:</span><span class="sxs-lookup"><span data-stu-id="48d0b-157">Here are some command line samples to import JSON files:</span></span>

    #Import a single JSON file
    dt.exe /s:JsonFile /s.Files:.\Sessions.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory of JSON files
    dt.exe /s:JsonFile /s.Files:C:\TESessions\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory (including sub-directories) of JSON files
    dt.exe /s:JsonFile /s.Files:C:\LastFMMusic\**\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Music /t.CollectionThroughput:2500

    #Import a directory (single), directory (recursive), and individual JSON files
    dt.exe /s:JsonFile /s.Files:C:\Tweets\*.*;C:\LargeDocs\**\*.*;C:\TESessions\Session48172.json;C:\TESessions\Session48173.json;C:\TESessions\Session48174.json;C:\TESessions\Session48175.json;C:\TESessions\Session48177.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:subs /t.CollectionThroughput:2500

    #Import a single JSON file and partition the data across 4 collections
    dt.exe /s:JsonFile /s.Files:D:\\CompanyData\\Companies.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:comp[1-4] /t.PartitionKey:name /t.CollectionThroughput:2500

## <span data-ttu-id="48d0b-158"><a id="MongoDB"></a>Importeren van MongoDB</span><span class="sxs-lookup"><span data-stu-id="48d0b-158"><a id="MongoDB"></a>To import from MongoDB</span></span>

> [!IMPORTANT]
> <span data-ttu-id="48d0b-159">Als u naar een Cosmos-DB Azure-account met ondersteuning voor MongoDB importeren wilt, volgt u deze [instructies](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="48d0b-159">If you are importing to an Azure Cosmos DB account with Support for MongoDB, follow these [instructions](mongodb-migrate.md).</span></span>
> 
> 

<span data-ttu-id="48d0b-160">De optie voor MongoDB importfunctie kunt u importeren uit een afzonderlijke MongoDB-verzameling en eventueel documenten met behulp van een query filteren en/of de documentstructuur wijzigen met behulp van een projectie.</span><span class="sxs-lookup"><span data-stu-id="48d0b-160">The MongoDB source importer option allows you to import from an individual MongoDB collection and optionally filter documents using a query and/or modify the document structure by using a projection.</span></span>  

![Schermopname van MongoDB-opties voor gegevensbron](./media/import-data/mongodbsource.png)

<span data-ttu-id="48d0b-162">De verbindingsreeks heeft de standaard MongoDB-indeling:</span><span class="sxs-lookup"><span data-stu-id="48d0b-162">The connection string is in the standard MongoDB format:</span></span>

    mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database>

> [!NOTE]
> <span data-ttu-id="48d0b-163">Gebruik de opdracht controleren om ervoor te zorgen dat het MongoDB-exemplaar dat is opgegeven in het veld connection string kan worden geopend.</span><span class="sxs-lookup"><span data-stu-id="48d0b-163">Use the Verify command to ensure that the MongoDB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="48d0b-164">Voer de naam van de verzameling van waaruit de gegevens worden geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="48d0b-164">Enter the name of the collection from which data will be imported.</span></span> <span data-ttu-id="48d0b-165">U kunt eventueel opgeven of een bestand voor een query opgeven (bijvoorbeeld {pop: {$gt: 5000}}) en/of een projectie (bijvoorbeeld {loc:0}) voor zowel filteren en vorm van de gegevens moeten worden geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="48d0b-165">You may optionally specify or provide a file for a query (e.g. {pop: {$gt:5000}} ) and/or projection (e.g. {loc:0} ) to both filter and shape the data to be imported.</span></span>

<span data-ttu-id="48d0b-166">Hier volgen enkele voorbeelden vanaf de opdrachtregel om te importeren uit MongoDB:</span><span class="sxs-lookup"><span data-stu-id="48d0b-166">Here are some command line samples to import from MongoDB:</span></span>

    #Import all documents from a MongoDB collection
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZips /t.IdField:_id /t.CollectionThroughput:2500

    #Import documents from a MongoDB collection which match the query and exclude the loc field
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /s.Query:{pop:{$gt:50000}} /s.Projection:{loc:0} /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZipsTransform /t.IdField:_id/t.CollectionThroughput:2500

## <span data-ttu-id="48d0b-167"><a id="MongoDBExport"></a>Voor het importeren van de exportbestanden MongoDB</span><span class="sxs-lookup"><span data-stu-id="48d0b-167"><a id="MongoDBExport"></a>To import MongoDB export files</span></span>

> [!IMPORTANT]
> <span data-ttu-id="48d0b-168">Als u naar een Cosmos-DB Azure-account met ondersteuning voor MongoDB importeren wilt, volgt u deze [instructies](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="48d0b-168">If you are importing to an Azure Cosmos DB account with support for MongoDB, follow these [instructions](mongodb-migrate.md).</span></span>
> 
> 

<span data-ttu-id="48d0b-169">De MongoDB JSON-bestand bron importfunctie exportoptie kunt u voor het importeren van een of meer JSON-bestanden van het hulpprogramma mongoexport geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="48d0b-169">The MongoDB export JSON file source importer option allows you to import one or more JSON files produced from the mongoexport utility.</span></span>  

![Schermopname van MongoDB-exportopties bron](./media/import-data/mongodbexportsource.png)

<span data-ttu-id="48d0b-171">Als u mappen met MongoDB export JSON-bestanden voor het importeren van toevoegt, hebt u de mogelijkheid van recursief zoeken naar bestanden in submappen.</span><span class="sxs-lookup"><span data-stu-id="48d0b-171">When adding folders that contain MongoDB export JSON files for import, you have the option of recursively searching for files in subfolders.</span></span>

<span data-ttu-id="48d0b-172">Hier volgt een voorbeeld van de opdrachtregel om te importeren uit JSON-bestanden van MongoDB-export:</span><span class="sxs-lookup"><span data-stu-id="48d0b-172">Here is a command line sample to import from MongoDB export JSON files:</span></span>

    dt.exe /s:MongoDBExport /s.Files:D:\mongoemployees.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:employees /t.IdField:_id /t.Dates:Epoch /t.CollectionThroughput:2500

## <span data-ttu-id="48d0b-173"><a id="SQL"></a>Om te importeren uit SQL Server</span><span class="sxs-lookup"><span data-stu-id="48d0b-173"><a id="SQL"></a>To import from SQL Server</span></span>
<span data-ttu-id="48d0b-174">De SQL-bron importfunctie optie kunt u om te importeren uit een afzonderlijke SQL Server-database en optioneel de records moeten worden geïmporteerd met behulp van een query filteren.</span><span class="sxs-lookup"><span data-stu-id="48d0b-174">The SQL source importer option allows you to import from an individual SQL Server database and optionally filter the records to be imported using a query.</span></span> <span data-ttu-id="48d0b-175">U kunt bovendien de documentstructuur wijzigen door op te geven van een geneste scheidingsteken (meer informatie over die later).</span><span class="sxs-lookup"><span data-stu-id="48d0b-175">In addition, you can modify the document structure by specifying a nesting separator (more on that in a moment).</span></span>  

![Schermafbeelding van de SQL - opties voor hulpprogramma's voor migratie](./media/import-data/sqlexportsource.png)

<span data-ttu-id="48d0b-177">De indeling van de verbindingsreeks is standaard SQL indeling van de verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="48d0b-177">The format of the connection string is the standard SQL connection string format.</span></span>

> [!NOTE]
> <span data-ttu-id="48d0b-178">Gebruik de opdracht controleren om ervoor te zorgen dat de SQL Server-exemplaar dat is opgegeven in het veld connection string kan worden geopend.</span><span class="sxs-lookup"><span data-stu-id="48d0b-178">Use the Verify command to ensure that the SQL Server instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="48d0b-179">De geneste scheidingsteken-eigenschap gebruikt voor het maken van hiërarchische relaties (onderliggende documenten) tijdens het importeren.</span><span class="sxs-lookup"><span data-stu-id="48d0b-179">The nesting separator property is used to create hierarchical relationships (sub-documents) during import.</span></span> <span data-ttu-id="48d0b-180">Houd rekening met de volgende SQL-query:</span><span class="sxs-lookup"><span data-stu-id="48d0b-180">Consider the following SQL query:</span></span>

<span data-ttu-id="48d0b-181">*CAST (BusinessEntityID AS varchar) als de Id, naam, adrestype als [Address.AddressType], AddressLine1 als [Address.AddressLine1], plaats als [Address.Location.City], StateProvinceName als [Address.Location.StateProvinceName], postcode als [selecteren Address.PostalCode] CountryRegionName als [Address.CountryRegionName] uit Sales.vStoreWithAddresses waar adrestype = 'Hoofdkantoor'*</span><span class="sxs-lookup"><span data-stu-id="48d0b-181">*select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'*</span></span>

<span data-ttu-id="48d0b-182">Dit retourneert de volgende resultaten voor (gedeeltelijk):</span><span class="sxs-lookup"><span data-stu-id="48d0b-182">Which returns the following (partial) results:</span></span>

![Schermafbeelding van de SQL-queryresultaten](./media/import-data/sqlqueryresults.png)

<span data-ttu-id="48d0b-184">Noteer de aliassen zoals Address.AddressType en Address.Location.StateProvinceName.</span><span class="sxs-lookup"><span data-stu-id="48d0b-184">Note the aliases such as Address.AddressType and Address.Location.StateProvinceName.</span></span> <span data-ttu-id="48d0b-185">Door op te geven van een geneste scheidingsteken van '.', het hulpprogramma voor importeren adres en Address.Location subdocumenten maakt tijdens het importeren.</span><span class="sxs-lookup"><span data-stu-id="48d0b-185">By specifying a nesting separator of ‘.’, the import tool creates Address and Address.Location subdocuments during the import.</span></span> <span data-ttu-id="48d0b-186">Hier volgt een voorbeeld van een resulterende document in Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="48d0b-186">Here is an example of a resulting document in Azure Cosmos DB:</span></span>

<span data-ttu-id="48d0b-187">*{'id': '956', 'Name': 'Fijner verkoop en Service', 'Adres': {'Adrestype': 'Hoofdkantoor', 'AddressLine1': '#500 75 O'Connor straat', 'Locatie': {'Stad': 'Canada Ottawa', 'StateProvinceName': "Ontario"}, 'Postcode': 'K4B 1S2', 'CountryRegionName': ' Canada'}}*</span><span class="sxs-lookup"><span data-stu-id="48d0b-187">*{ "id": "956", "Name": "Finer Sales and Service", "Address": { "AddressType": "Main Office", "AddressLine1": "#500-75 O'Connor Street", "Location": { "City": "Ottawa", "StateProvinceName": "Ontario" }, "PostalCode": "K4B 1S2", "CountryRegionName": "Canada" } }*</span></span>

<span data-ttu-id="48d0b-188">Hier volgen enkele voorbeelden vanaf de opdrachtregel om te importeren uit SQL Server:</span><span class="sxs-lookup"><span data-stu-id="48d0b-188">Here are some command line samples to import from SQL Server:</span></span>

    #Import records from SQL which match a query
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, * from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Stores /t.IdField:Id /t.CollectionThroughput:2500

    #Import records from sql which match a query and create hierarchical relationships
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /s.NestingSeparator:. /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:StoresSub /t.IdField:Id /t.CollectionThroughput:2500

## <span data-ttu-id="48d0b-189"><a id="CSV"></a>CSV-bestanden importeren en CSV niet converteren naar JSON</span><span class="sxs-lookup"><span data-stu-id="48d0b-189"><a id="CSV"></a>To import CSV files and convert CSV to JSON</span></span>
<span data-ttu-id="48d0b-190">De optie voor de gegevensbron importfunctie van CSV-bestand kunt u een of meer CSV-bestanden te importeren.</span><span class="sxs-lookup"><span data-stu-id="48d0b-190">The CSV file source importer option enables you to import one or more CSV files.</span></span> <span data-ttu-id="48d0b-191">Bij het toevoegen van mappen met CSV-bestanden voor importeren, hebt u de mogelijkheid van recursief zoeken naar bestanden in submappen.</span><span class="sxs-lookup"><span data-stu-id="48d0b-191">When adding folders that contain CSV files for import, you have the option of recursively searching for files in subfolders.</span></span>

![Schermopname van CSV - opties voor CSV in JSON](media/import-data/csvsource.png)

<span data-ttu-id="48d0b-193">Vergelijkbaar met de SQL-bron, het aantal geneste scheidingsteken-eigenschap kan hiërarchische relaties (onderliggende documenten) maken tijdens het importeren worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="48d0b-193">Similar to the SQL source, the nesting separator property may be used to create hierarchical relationships (sub-documents) during import.</span></span> <span data-ttu-id="48d0b-194">Houd rekening met de volgende header voor de CSV-rij en gegevensrijen:</span><span class="sxs-lookup"><span data-stu-id="48d0b-194">Consider the following CSV header row and data rows:</span></span>

![Schermopname van CSV-voorbeeld registreert - CSV in JSON](./media/import-data/csvsample.png)

<span data-ttu-id="48d0b-196">Noteer de aliassen zoals DomainInfo.Domain_Name en RedirectInfo.Redirecting.</span><span class="sxs-lookup"><span data-stu-id="48d0b-196">Note the aliases such as DomainInfo.Domain_Name and RedirectInfo.Redirecting.</span></span> <span data-ttu-id="48d0b-197">Door op te geven van een geneste scheidingsteken van '.', maakt het hulpprogramma voor importeren DomainInfo en RedirectInfo subdocumenten tijdens het importeren.</span><span class="sxs-lookup"><span data-stu-id="48d0b-197">By specifying a nesting separator of ‘.’, the import tool will create DomainInfo and RedirectInfo subdocuments during the import.</span></span> <span data-ttu-id="48d0b-198">Hier volgt een voorbeeld van een resulterende document in Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="48d0b-198">Here is an example of a resulting document in Azure Cosmos DB:</span></span>

<span data-ttu-id="48d0b-199">*{"DomainInfo": {'Domeinnaam': 'ACUS.GOV', 'Domain_Name_Address': 'http://www.ACUS.GOV'}, 'Federale instantie': ' beheerdersrechten Conferentie van de Verenigde Staten ', 'RedirectInfo': {'Omleiden': '0', 'Redirect_Destination': ' "}, 'id': '9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d'}*</span><span class="sxs-lookup"><span data-stu-id="48d0b-199">*{ "DomainInfo": { "Domain_Name": "ACUS.GOV", "Domain_Name_Address": "http://www.ACUS.GOV" }, "Federal Agency": "Administrative Conference of the United States", "RedirectInfo": { "Redirecting": "0", "Redirect_Destination": "" }, "id": "9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d" }*</span></span>

<span data-ttu-id="48d0b-200">Het hulpprogramma voor importeren probeert te afleiden typegegevens zonder aanhalingstekens waarden in CSV-bestanden (tussen aanhalingstekens waarden worden altijd behandeld als tekenreeksen).</span><span class="sxs-lookup"><span data-stu-id="48d0b-200">The import tool will attempt to infer type information for unquoted values in CSV files (quoted values are always treated as strings).</span></span>  <span data-ttu-id="48d0b-201">Typen worden geïdentificeerd in de volgende volgorde: getal, datum/tijd, Booleaanse waarde.</span><span class="sxs-lookup"><span data-stu-id="48d0b-201">Types are identified in the following order: number, datetime, boolean.</span></span>  

<span data-ttu-id="48d0b-202">Er zijn twee dingen te weten over de CSV-import:</span><span class="sxs-lookup"><span data-stu-id="48d0b-202">There are two other things to note about CSV import:</span></span>

1. <span data-ttu-id="48d0b-203">Standaard zonder aanhalingstekens waarden zijn altijd bijgesneden voor tabs en spaties, terwijl tussen aanhalingstekens waarden behouden als blijven-is.</span><span class="sxs-lookup"><span data-stu-id="48d0b-203">By default, unquoted values are always trimmed for tabs and spaces, while quoted values are preserved as-is.</span></span> <span data-ttu-id="48d0b-204">Dit gedrag kan worden genegeerd met het selectievakje Trim tussen aanhalingstekens waarden of de opdrachtregeloptie /s.TrimQuoted.</span><span class="sxs-lookup"><span data-stu-id="48d0b-204">This behavior can be overridden with the Trim quoted values checkbox or the /s.TrimQuoted command line option.</span></span>
2. <span data-ttu-id="48d0b-205">Standaard wordt een zonder aanhalingstekens null worden beschouwd als een null-waarde.</span><span class="sxs-lookup"><span data-stu-id="48d0b-205">By default, an unquoted null is treated as a null value.</span></span> <span data-ttu-id="48d0b-206">Dit gedrag kan worden genegeerd (dat wil zeggen een zonder aanhalingstekens null behandelen als een tekenreeks 'null') met het behandelen zonder aanhalingstekens NULL als tekenreeks selectievakje of de opdrachtregeloptie /s.NoUnquotedNulls.</span><span class="sxs-lookup"><span data-stu-id="48d0b-206">This behavior can be overridden (i.e. treat an unquoted null as a “null” string) with the Treat unquoted NULL as string checkbox or the /s.NoUnquotedNulls command line option.</span></span>

<span data-ttu-id="48d0b-207">Hier volgt een voorbeeld van de opdrachtregel voor CSV-import:</span><span class="sxs-lookup"><span data-stu-id="48d0b-207">Here is a command line sample for CSV import:</span></span>

    dt.exe /s:CsvFile /s.Files:.\Employees.csv /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Employees /t.IdField:EntityID /t.CollectionThroughput:2500

## <span data-ttu-id="48d0b-208"><a id="AzureTableSource"></a>Om te importeren uit Azure Table storage</span><span class="sxs-lookup"><span data-stu-id="48d0b-208"><a id="AzureTableSource"></a>To import from Azure Table storage</span></span>
<span data-ttu-id="48d0b-209">De optie voor de gegevensbron importfunctie van Azure Table storage kunt u om te importeren uit een afzonderlijke tabel voor Azure Table storage en filter optioneel de tabelentiteiten worden geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="48d0b-209">The Azure Table storage source importer option allows you to import from an individual Azure Table storage table and optionally filter the table entities to be imported.</span></span> <span data-ttu-id="48d0b-210">Houd er rekening mee dat u het hulpprogramma voor migratie van gegevens niet gebruiken voor Azure Table storage-gegevens importeren in Azure Cosmos DB voor gebruik met de tabel-API.</span><span class="sxs-lookup"><span data-stu-id="48d0b-210">Note that you cannot use the Data Migration tool to import Azure Table storage data into Azure Cosmos DB for use with the Table API.</span></span> <span data-ttu-id="48d0b-211">Op dit moment wordt alleen importeren in Azure Cosmos DB voor gebruik met de DocumentDB-API ondersteund.</span><span class="sxs-lookup"><span data-stu-id="48d0b-211">Only importing to Azure Cosmos DB for use with the DocumentDB API is supported at this time.</span></span>

![Schermopname van Azure Table storage bronopties](./media/import-data/azuretablesource.png)

<span data-ttu-id="48d0b-213">De indeling van de verbindingsreeks voor Azure Table storage is:</span><span class="sxs-lookup"><span data-stu-id="48d0b-213">The format of the Azure Table storage connection string is:</span></span>

    DefaultEndpointsProtocol=<protocol>;AccountName=<Account Name>;AccountKey=<Account Key>;

> [!NOTE]
> <span data-ttu-id="48d0b-214">Gebruik de opdracht controleren om ervoor te zorgen dat het opgegeven in het veld connection string Azure Table storage-exemplaar kan worden geopend.</span><span class="sxs-lookup"><span data-stu-id="48d0b-214">Use the Verify command to ensure that the Azure Table storage instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="48d0b-215">Voer de naam van de Azure-tabel waaruit gegevens worden geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="48d0b-215">Enter the name of the Azure table from which data will be imported.</span></span> <span data-ttu-id="48d0b-216">U kunt eventueel opgeven een [filter](https://msdn.microsoft.com/library/azure/ff683669.aspx).</span><span class="sxs-lookup"><span data-stu-id="48d0b-216">You may optionally specify a [filter](https://msdn.microsoft.com/library/azure/ff683669.aspx).</span></span>

<span data-ttu-id="48d0b-217">De optie Azure Table storage importfunctie heeft de volgende aanvullende opties:</span><span class="sxs-lookup"><span data-stu-id="48d0b-217">The Azure Table storage source importer option has the following additional options:</span></span>

1. <span data-ttu-id="48d0b-218">Interne velden bevatten</span><span class="sxs-lookup"><span data-stu-id="48d0b-218">Include Internal Fields</span></span>
   1. <span data-ttu-id="48d0b-219">All - omvatten alle interne velden (PartitionKey, RowKey en tijdstempel)</span><span class="sxs-lookup"><span data-stu-id="48d0b-219">All - Include all internal fields (PartitionKey, RowKey, and Timestamp)</span></span>
   2. <span data-ttu-id="48d0b-220">Geen - uitsluiten alle interne velden</span><span class="sxs-lookup"><span data-stu-id="48d0b-220">None - Exclude all internal fields</span></span>
   3. <span data-ttu-id="48d0b-221">RowKey - alleen bestaan uit het veld RowKey</span><span class="sxs-lookup"><span data-stu-id="48d0b-221">RowKey - Only include the RowKey field</span></span>
2. <span data-ttu-id="48d0b-222">Kolommen selecteren</span><span class="sxs-lookup"><span data-stu-id="48d0b-222">Select Columns</span></span>
   1. <span data-ttu-id="48d0b-223">Azure Table storage filters bieden geen ondersteuning voor projecties.</span><span class="sxs-lookup"><span data-stu-id="48d0b-223">Azure Table storage filters do not support projections.</span></span> <span data-ttu-id="48d0b-224">Als u importeren alleen specifieke Azure Table-entiteitseigenschappen wilt, deze toevoegen aan de lijst met kolommen selecteren.</span><span class="sxs-lookup"><span data-stu-id="48d0b-224">If you want to only import specific Azure Table entity properties, add them to the Select Columns list.</span></span> <span data-ttu-id="48d0b-225">Alle andere entiteitseigenschappen wordt genegeerd.</span><span class="sxs-lookup"><span data-stu-id="48d0b-225">All other entity properties will be ignored.</span></span>

<span data-ttu-id="48d0b-226">Hier volgt een voorbeeld van de opdrachtregel om te importeren uit Azure Table storage:</span><span class="sxs-lookup"><span data-stu-id="48d0b-226">Here is a command line sample to import from Azure Table storage:</span></span>

    dt.exe /s:AzureTable /s.ConnectionString:"DefaultEndpointsProtocol=https;AccountName=<Account Name>;AccountKey=<Account Key>" /s.Table:metrics /s.InternalFields:All /s.Filter:"PartitionKey eq 'Partition1' and RowKey gt '00001'" /s.Projection:ObjectCount;ObjectSize  /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:metrics /t.CollectionThroughput:2500

## <span data-ttu-id="48d0b-227"><a id="DynamoDBSource"></a>Om te importeren uit Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="48d0b-227"><a id="DynamoDBSource"></a>To import from Amazon DynamoDB</span></span>
<span data-ttu-id="48d0b-228">De Amazon DynamoDB bron importfunctie optie kunt u om te importeren uit een tabel met afzonderlijke Amazon DynamoDB en filter optioneel de entiteiten worden geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="48d0b-228">The Amazon DynamoDB source importer option allows you to import from an individual Amazon DynamoDB table and optionally filter the entities to be imported.</span></span> <span data-ttu-id="48d0b-229">Verschillende sjablonen zijn bedoeld om het instellen van een import zo eenvoudig mogelijk is.</span><span class="sxs-lookup"><span data-stu-id="48d0b-229">Several templates are provided so that setting up an import is as easy as possible.</span></span>

![Schermopname van Amazon DynamoDB bronopties - hulpprogramma's voor migratie](./media/import-data/dynamodbsource1.png)

![Schermopname van Amazon DynamoDB bronopties - hulpprogramma's voor migratie](./media/import-data/dynamodbsource2.png)

<span data-ttu-id="48d0b-232">De indeling van de verbindingsreeks Amazon DynamoDB is:</span><span class="sxs-lookup"><span data-stu-id="48d0b-232">The format of the Amazon DynamoDB connection string is:</span></span>

    ServiceURL=<Service Address>;AccessKey=<Access Key>;SecretKey=<Secret Key>;

> [!NOTE]
> <span data-ttu-id="48d0b-233">Gebruik de opdracht controleren om ervoor te zorgen dat het opgegeven in het veld connection string Amazon DynamoDB exemplaar kan worden geopend.</span><span class="sxs-lookup"><span data-stu-id="48d0b-233">Use the Verify command to ensure that the Amazon DynamoDB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="48d0b-234">Hier volgt een voorbeeld van de opdrachtregel om te importeren uit Amazon DynamoDB:</span><span class="sxs-lookup"><span data-stu-id="48d0b-234">Here is a command line sample to import from Amazon DynamoDB:</span></span>

    dt.exe /s:DynamoDB /s.ConnectionString:ServiceURL=https://dynamodb.us-east-1.amazonaws.com;AccessKey=<accessKey>;SecretKey=<secretKey> /s.Request:"{   """TableName""": """ProductCatalog""" }" /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<Azure Cosmos DB Endpoint>;AccountKey=<Azure Cosmos DB Key>;Database=<Azure Cosmos DB Database>;" /t.Collection:catalogCollection /t.CollectionThroughput:2500

## <span data-ttu-id="48d0b-235"><a id="BlobImport"></a>Om bestanden te importeren uit Azure Blob-opslag</span><span class="sxs-lookup"><span data-stu-id="48d0b-235"><a id="BlobImport"></a>To import files from Azure Blob storage</span></span>
<span data-ttu-id="48d0b-236">De JSON-bestand, MongoDB-exportbestand en CSV-bestand bron importfunctie opties kunnen u een of meer bestanden importeren uit Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="48d0b-236">The JSON file, MongoDB export file, and CSV file source importer options allow you to import one or more files from Azure Blob storage.</span></span> <span data-ttu-id="48d0b-237">Nadat u een URL van de Blob-container en de Accountsleutel, bieden u gewoon een reguliere expressie om te selecteren van de bestanden te importeren.</span><span class="sxs-lookup"><span data-stu-id="48d0b-237">After specifying a Blob container URL and Account Key, simply provide a regular expression to select the file(s) to import.</span></span>

![Schermopname van Blob-bestand bronopties](./media/import-data/blobsource.png)

<span data-ttu-id="48d0b-239">Hier volgt een voorbeeld van een opdrachtregel JSON-bestanden importeren uit Azure Blob-opslag:</span><span class="sxs-lookup"><span data-stu-id="48d0b-239">Here is command line sample to import JSON files from Azure Blob storage:</span></span>

    dt.exe /s:JsonFile /s.Files:"blobs://<account key>@account.blob.core.windows.net:443/importcontainer/.*" /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:doctest

## <span data-ttu-id="48d0b-240"><a id="DocumentDBSource"></a>Om te importeren uit een verzameling Azure Cosmos DB DocumentDB-API</span><span class="sxs-lookup"><span data-stu-id="48d0b-240"><a id="DocumentDBSource"></a>To import from an Azure Cosmos DB DocumentDB API collection</span></span>
<span data-ttu-id="48d0b-241">De optie Azure Cosmos DB importfunctie kunt u gegevens importeren uit een of meer Azure Cosmos DB verzamelingen en filter optioneel documenten met behulp van een query.</span><span class="sxs-lookup"><span data-stu-id="48d0b-241">The Azure Cosmos DB source importer option allows you to import data from one or more Azure Cosmos DB collections and optionally filter documents using a query.</span></span>  

![Opties voor schermopname van Azure Cosmos DB-gegevensbron](./media/import-data/documentdbsource.png)

<span data-ttu-id="48d0b-243">De indeling van de Azure DB die Cosmos-verbindingsreeks is:</span><span class="sxs-lookup"><span data-stu-id="48d0b-243">The format of the Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="48d0b-244">De verbindingsreeks voor Azure DB die Cosmos-account kan worden opgehaald uit de blade sleutels van de Azure-portal, zoals beschreven in [het beheren van een account voor Azure Cosmos DB](manage-account.md), maar de naam van de database moet worden toegevoegd aan de verbinding de tekenreeks in de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="48d0b-244">The Azure Cosmos DB account connection string can be retrieved from the Keys blade of the Azure portal, as described in [How to manage an Azure Cosmos DB account](manage-account.md), however the name of the database needs to be appended to the connection string in the following format:</span></span>

    Database=<CosmosDB Database>;

> [!NOTE]
> <span data-ttu-id="48d0b-245">Gebruik de opdracht controleren om ervoor te zorgen dat het Azure DB die Cosmos-exemplaar dat is opgegeven in het veld connection string kan worden geopend.</span><span class="sxs-lookup"><span data-stu-id="48d0b-245">Use the Verify command to ensure that the Azure Cosmos DB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="48d0b-246">Als u wilt importeren uit een verzameling met één Azure Cosmos DB, voer de naam van de verzameling van waaruit de gegevens worden geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="48d0b-246">To import from a single Azure Cosmos DB collection, enter the name of the collection from which data will be imported.</span></span> <span data-ttu-id="48d0b-247">Om te importeren uit meerdere Azure Cosmos DB verzamelingen, bieden een reguliere expressie zodat deze overeenkomt met een of meer verzamelingsnamen (bijvoorbeeld collection01 | collection02 | collection03).</span><span class="sxs-lookup"><span data-stu-id="48d0b-247">To import from multiple Azure Cosmos DB collections, provide a regular expression to match one or more collection names (e.g. collection01 | collection02 | collection03).</span></span> <span data-ttu-id="48d0b-248">U kunt eventueel, of geef een bestand voor een query op filter en de vorm van de gegevens moeten worden geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="48d0b-248">You may optionally specify, or provide a file for, a query to both filter and shape the data to be imported.</span></span>

> [!NOTE]
> <span data-ttu-id="48d0b-249">Omdat het veld voor de verzameling reguliere expressies, accepteert als u wilt importeren uit één verzameling waarvan de naam tekens van de reguliere expressie bevat, moeten vervolgens die tekens worden voorafgegaan dienovereenkomstig.</span><span class="sxs-lookup"><span data-stu-id="48d0b-249">Since the collection field accepts regular expressions, if you are importing from a single collection whose name contains regular expression characters, then those characters must be escaped accordingly.</span></span>
> 
> 

<span data-ttu-id="48d0b-250">De optie Azure Cosmos DB importfunctie heeft de volgende geavanceerde opties:</span><span class="sxs-lookup"><span data-stu-id="48d0b-250">The Azure Cosmos DB source importer option has the following advanced options:</span></span>

1. <span data-ttu-id="48d0b-251">Interne velden bevatten: Hiermee geeft u wel of niet Azure Cosmos DB document Systeemeigenschappen opnemen in de uitvoer (bijvoorbeeld _rid, _ts).</span><span class="sxs-lookup"><span data-stu-id="48d0b-251">Include Internal Fields: Specifies whether or not to include Azure Cosmos DB document system properties in the export (e.g. _rid, _ts).</span></span>
2. <span data-ttu-id="48d0b-252">Aantal nieuwe pogingen bij fouten: Hiermee geeft u het aantal keren opnieuw de verbinding met Azure Cosmos DB in geval van een tijdelijke fouten (bijvoorbeeld connectiviteit onderbreking op het netwerk).</span><span class="sxs-lookup"><span data-stu-id="48d0b-252">Number of Retries on Failure: Specifies the number of times to retry the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
3. <span data-ttu-id="48d0b-253">Interval voor opnieuw proberen: Geeft aan hoe lang moet worden gewacht tussen opnieuw verbinding met Azure Cosmos-database in geval van een tijdelijke fouten (bijvoorbeeld connectiviteit onderbreking op het netwerk).</span><span class="sxs-lookup"><span data-stu-id="48d0b-253">Retry Interval: Specifies how long to wait between retrying the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
4. <span data-ttu-id="48d0b-254">Verbindingsmodus: Hiermee geeft u de verbindingsmodus gebruiken met Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="48d0b-254">Connection Mode: Specifies the connection mode to use with Azure Cosmos DB.</span></span> <span data-ttu-id="48d0b-255">De beschikbare opties zijn DirectTcp, DirectHttps en Gateway.</span><span class="sxs-lookup"><span data-stu-id="48d0b-255">The available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="48d0b-256">De modi rechtstreekse verbinding zijn sneller, terwijl de gateway-modus meer firewall beschrijvende is aangezien hierbij alleen poort 443.</span><span class="sxs-lookup"><span data-stu-id="48d0b-256">The direct connection modes are faster, while the gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Schermopname van Azure Cosmos DB bron geavanceerde opties](./media/import-data/documentdbsourceoptions.png)

> [!TIP]
> <span data-ttu-id="48d0b-258">Het hulpprogramma voor importeren standaard verbindingsmodus DirectTcp.</span><span class="sxs-lookup"><span data-stu-id="48d0b-258">The import tool defaults to connection mode DirectTcp.</span></span> <span data-ttu-id="48d0b-259">Als u de firewall-problemen ondervindt, overschakelen naar verbindingsmodus Gateway, omdat hiervoor alleen poort 443.</span><span class="sxs-lookup"><span data-stu-id="48d0b-259">If you experience firewall issues, switch to connection mode Gateway, as it only requires port 443.</span></span>
> 
> 

<span data-ttu-id="48d0b-260">Hier volgen enkele voorbeelden vanaf de opdrachtregel om te importeren uit Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="48d0b-260">Here are some command line samples to import from Azure Cosmos DB:</span></span>

    #Migrate data from one Azure Cosmos DB collection to another Azure Cosmos DB collections
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:TEColl /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:TESessions /t.CollectionThroughput:2500

    #Migrate data from multiple Azure Cosmos DB collections to a single Azure Cosmos DB collection
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:comp1|comp2|comp3|comp4 /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:singleCollection /t.CollectionThroughput:2500

    #Export an Azure Cosmos DB collection to a JSON file
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:StoresSub /t:JsonFile /t.File:StoresExport.json /t.Overwrite /t.CollectionThroughput:2500

> [!TIP]
> <span data-ttu-id="48d0b-261">Het Azure Cosmos DB Data Import-hulpprogramma ondersteunt ook het importeren van gegevens uit de [Azure Cosmos DB Emulator](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="48d0b-261">The Azure Cosmos DB Data Import Tool also supports import of data from the [Azure Cosmos DB Emulator](local-emulator.md).</span></span> <span data-ttu-id="48d0b-262">Bij het importeren van een lokale emulator, het eindpunt instellen op `https://localhost:<port>`.</span><span class="sxs-lookup"><span data-stu-id="48d0b-262">When importing data from a local emulator, set the endpoint to `https://localhost:<port>`.</span></span> 
> 
> 

## <span data-ttu-id="48d0b-263"><a id="HBaseSource"></a>Importeren van HBase</span><span class="sxs-lookup"><span data-stu-id="48d0b-263"><a id="HBaseSource"></a>To import from HBase</span></span>
<span data-ttu-id="48d0b-264">De optie voor HBase importfunctie kunt u gegevens importeren uit een HBase-tabel en optioneel filter de gegevens.</span><span class="sxs-lookup"><span data-stu-id="48d0b-264">The HBase source importer option allows you to import data from an HBase table and optionally filter the data.</span></span> <span data-ttu-id="48d0b-265">Verschillende sjablonen zijn bedoeld om het instellen van een import zo eenvoudig mogelijk is.</span><span class="sxs-lookup"><span data-stu-id="48d0b-265">Several templates are provided so that setting up an import is as easy as possible.</span></span>

![Schermopname van HBase-opties voor gegevensbron](./media/import-data/hbasesource1.png)

![Schermopname van HBase-opties voor gegevensbron](./media/import-data/hbasesource2.png)

<span data-ttu-id="48d0b-268">De indeling van de verbindingsreeks HBase Stargate is:</span><span class="sxs-lookup"><span data-stu-id="48d0b-268">The format of the HBase Stargate connection string is:</span></span>

    ServiceURL=<server-address>;Username=<username>;Password=<password>

> [!NOTE]
> <span data-ttu-id="48d0b-269">Gebruik de opdracht controleren om ervoor te zorgen dat het HBase-exemplaar dat is opgegeven in het veld connection string kan worden geopend.</span><span class="sxs-lookup"><span data-stu-id="48d0b-269">Use the Verify command to ensure that the HBase instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="48d0b-270">Hier volgt een voorbeeld van de opdrachtregel om te importeren uit HBase:</span><span class="sxs-lookup"><span data-stu-id="48d0b-270">Here is a command line sample to import from HBase:</span></span>

    dt.exe /s:HBase /s.ConnectionString:ServiceURL=<server-address>;Username=<username>;Password=<password> /s.Table:Contacts /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:hbaseimport

## <span data-ttu-id="48d0b-271"><a id="DocumentDBBulkTarget"></a>Om te importeren naar de DocumentDB-API (bulksgewijs importeren)</span><span class="sxs-lookup"><span data-stu-id="48d0b-271"><a id="DocumentDBBulkTarget"></a>To import to the DocumentDB API (Bulk Import)</span></span>
<span data-ttu-id="48d0b-272">De importfunctie Azure Cosmos DB bulksgewijs kunt u om te importeren uit een van de bronopties die beschikbaar, met behulp van een Azure Cosmos DB opgeslagen procedure voor efficiëntie.</span><span class="sxs-lookup"><span data-stu-id="48d0b-272">The Azure Cosmos DB Bulk importer allows you to import from any of the available source options, using an Azure Cosmos DB stored procedure for efficiency.</span></span> <span data-ttu-id="48d0b-273">Het hulpprogramma ondersteunt importeren naar één enkel gepartitioneerd Azure Cosmos DB verzameling, evenals shard importeren, waarbij de gegevens in meerdere één gepartitioneerd Azure Cosmos DB verzamelingen zijn gepartitioneerd.</span><span class="sxs-lookup"><span data-stu-id="48d0b-273">The tool supports import to one single-partitioned Azure Cosmos DB collection, as well as sharded import whereby data is partitioned across multiple single-partitioned Azure Cosmos DB collections.</span></span> <span data-ttu-id="48d0b-274">Zie voor meer informatie over het partitioneren van gegevens, [partitionering en schalen in Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="48d0b-274">For more information about partitioning data, see [Partitioning and scaling in Azure Cosmos DB](partition-data.md).</span></span> <span data-ttu-id="48d0b-275">Het hulpprogramma wordt maken, uitvoeren en verwijder de opgeslagen procedure uit de verzameling(en) doel.</span><span class="sxs-lookup"><span data-stu-id="48d0b-275">The tool will create, execute, and then delete the stored procedure from the target collection(s).</span></span>  

![Schermopname van Azure Cosmos DB bulksgewijs opties](./media/import-data/documentdbbulk.png)

<span data-ttu-id="48d0b-277">De indeling van de Azure DB die Cosmos-verbindingsreeks is:</span><span class="sxs-lookup"><span data-stu-id="48d0b-277">The format of the Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="48d0b-278">De verbindingsreeks voor Azure DB die Cosmos-account kan worden opgehaald uit de blade sleutels van de Azure-portal, zoals beschreven in [het beheren van een account voor Azure Cosmos DB](manage-account.md), maar de naam van de database moet worden toegevoegd aan de verbinding de tekenreeks in de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="48d0b-278">The Azure Cosmos DB account connection string can be retrieved from the Keys blade of the Azure portal, as described in [How to manage an Azure Cosmos DB account](manage-account.md), however the name of the database needs to be appended to the connection string in the following format:</span></span>

    Database=<CosmosDB Database>;

> [!NOTE]
> <span data-ttu-id="48d0b-279">Gebruik de opdracht controleren om ervoor te zorgen dat het Azure DB die Cosmos-exemplaar dat is opgegeven in het veld connection string kan worden geopend.</span><span class="sxs-lookup"><span data-stu-id="48d0b-279">Use the Verify command to ensure that the Azure Cosmos DB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="48d0b-280">Als u wilt importeren naar één verzameling, voer de naam van de verzameling waarop gegevens worden geïmporteerd en klik op de knop toevoegen.</span><span class="sxs-lookup"><span data-stu-id="48d0b-280">To import to a single collection, enter the name of the collection to which data will be imported and click the Add button.</span></span> <span data-ttu-id="48d0b-281">Als u wilt importeren tot meerdere verzamelingen, voer de verzamelingsnaam van elke afzonderlijk of gebruik de volgende syntaxis om op te geven van meerdere verzamelingen: *collection_prefix*[begin index - end-index].</span><span class="sxs-lookup"><span data-stu-id="48d0b-281">To import to multiple collections, either enter each collection name individually or use the following syntax to specify multiple collections: *collection_prefix*[start index - end index].</span></span> <span data-ttu-id="48d0b-282">Houd rekening met het volgende bij het opgeven van meerdere verzamelingen via de hiervoor genoemde syntaxis:</span><span class="sxs-lookup"><span data-stu-id="48d0b-282">When specifying multiple collections via the aforementioned syntax, keep the following in mind:</span></span>

1. <span data-ttu-id="48d0b-283">Alleen geheel getal bereik bestandsnaampatronen worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="48d0b-283">Only integer range name patterns are supported.</span></span> <span data-ttu-id="48d0b-284">Bijvoorbeeld, geven verzameling [0-3] wordt produceren van de volgende verzamelingen: collection0, collection1, collection2, collection3.</span><span class="sxs-lookup"><span data-stu-id="48d0b-284">For example, specifying collection[0-3] will produce the following collections: collection0, collection1, collection2, collection3.</span></span>
2. <span data-ttu-id="48d0b-285">U kunt een verkorte syntaxis gebruiken: verzameling [3] wordt vermeld in stap 1 verzamelingen dezelfde set verzenden.</span><span class="sxs-lookup"><span data-stu-id="48d0b-285">You can use an abbreviated syntax: collection[3] will emit same set of collections mentioned in step 1.</span></span>
3. <span data-ttu-id="48d0b-286">Meer dan een vervanging kan worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="48d0b-286">More than one substitution can be provided.</span></span> <span data-ttu-id="48d0b-287">Bijvoorbeeld, verzameling [0-1] [0-9] genereert 20 verzamelingsnamen met toonaangevende nullen (collection01,... 02... 03).</span><span class="sxs-lookup"><span data-stu-id="48d0b-287">For example, collection[0-1] [0-9] will generate 20 collection names with leading zeros (collection01, ..02, ..03).</span></span>

<span data-ttu-id="48d0b-288">Wanneer de verzameling namen zijn opgegeven, kiest u de gewenste doorvoer van de verzameling(en) (400 RUs naar 10.000 RUs).</span><span class="sxs-lookup"><span data-stu-id="48d0b-288">Once the collection name(s) have been specified, choose the desired throughput of the collection(s) (400 RUs to 10,000 RUs).</span></span> <span data-ttu-id="48d0b-289">Kies een hogere doorvoer voor de beste prestaties importeren.</span><span class="sxs-lookup"><span data-stu-id="48d0b-289">For best import performance, choose a higher throughput.</span></span> <span data-ttu-id="48d0b-290">Zie voor meer informatie over prestatieniveaus [prestatieniveaus in Azure Cosmos DB](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="48d0b-290">For more information about performance levels, see [Performance levels in Azure Cosmos DB](performance-levels.md).</span></span>

> [!NOTE]
> <span data-ttu-id="48d0b-291">De instelling van de doorvoer prestaties is alleen van toepassing op het maken van de verzameling.</span><span class="sxs-lookup"><span data-stu-id="48d0b-291">The performance throughput setting only applies to collection creation.</span></span> <span data-ttu-id="48d0b-292">Als de opgegeven verzameling al bestaat, wordt de doorvoer niet gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="48d0b-292">If the specified collection already exists, its throughput will not be modified.</span></span>
> 
> 

<span data-ttu-id="48d0b-293">Bij het importeren van meerdere verzamelingen, wordt in de import-hulpprogramma ondersteunt hash sharding gebaseerd.</span><span class="sxs-lookup"><span data-stu-id="48d0b-293">When importing to multiple collections, the import tool supports hash based sharding.</span></span> <span data-ttu-id="48d0b-294">Geef in dit scenario wordt de documenteigenschap dat u wilt gebruiken als de partitiesleutel (als partitiesleutel leeg is, documenten zijn shard willekeurig in de doel-verzamelingen).</span><span class="sxs-lookup"><span data-stu-id="48d0b-294">In this scenario, specify the document property you wish to use as the Partition Key (if Partition Key is left blank, documents will be sharded randomly across the target collections).</span></span>

<span data-ttu-id="48d0b-295">U kunt eventueel opgeven welk veld in de bron voor het importeren moet worden gebruikt als de eigenschap id van Azure DB die Cosmos-document tijdens het importeren (Let erop dat als documenten geen deze eigenschap bevatten, wordt het hulpprogramma voor importeren wordt gegenereerd zodra een GUID als de waarde van de id-eigenschap).</span><span class="sxs-lookup"><span data-stu-id="48d0b-295">You may optionally specify which field in the import source should be used as the Azure Cosmos DB document id property during the import (note that if documents do not contain this property, then the import tool will generate a GUID as the id property value).</span></span>

<span data-ttu-id="48d0b-296">Er zijn tijdens het importeren van een aantal geavanceerde opties beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="48d0b-296">There are a number of advanced options available during import.</span></span> <span data-ttu-id="48d0b-297">Terwijl het hulpprogramma omvat eerst een standaard bulkimport opgeslagen procedure (BulkInsert.js), kunt u uw eigen importeren opgeslagen procedure opgeven:</span><span class="sxs-lookup"><span data-stu-id="48d0b-297">First, while the tool includes a default bulk import stored procedure (BulkInsert.js), you may choose to specify your own import stored procedure:</span></span>

 ![Schermopname van Azure Cosmos DB bulksgewijs invoegen sproc optie](./media/import-data/bulkinsertsp.png)

<span data-ttu-id="48d0b-299">Bij het importeren van datum-typen (bijvoorbeeld van SQL Server of MongoDB), kunt u kunt daarnaast voor kiezen tussen de drie opties voor importeren:</span><span class="sxs-lookup"><span data-stu-id="48d0b-299">Additionally, when importing date types (e.g. from SQL Server or MongoDB), you can choose between three import options:</span></span>

 ![Schermopname van Azure Cosmos DB datum tijdopties importeren](./media/import-data/datetimeoptions.png)

* <span data-ttu-id="48d0b-301">Tekenreeks: Behouden als een string-waarde</span><span class="sxs-lookup"><span data-stu-id="48d0b-301">String: Persist as a string value</span></span>
* <span data-ttu-id="48d0b-302">Epoche: Behouden als een getalwaarde epoche</span><span class="sxs-lookup"><span data-stu-id="48d0b-302">Epoch: Persist as an Epoch number value</span></span>
* <span data-ttu-id="48d0b-303">Beide: Zowel tekenreeks als numerieke waarden epoche bewaard.</span><span class="sxs-lookup"><span data-stu-id="48d0b-303">Both: Persist both string and Epoch number values.</span></span> <span data-ttu-id="48d0b-304">Deze optie maakt u een subdocument, bijvoorbeeld: "date_joined": {'' waarde '': ' 2013-10-21T21:17:25.2410000Z ', ' epoche ': 1382390245}</span><span class="sxs-lookup"><span data-stu-id="48d0b-304">This option will create a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span></span>

<span data-ttu-id="48d0b-305">De Azure Cosmos DB Bulk-importprogramma heeft de volgende aanvullende geavanceerde opties:</span><span class="sxs-lookup"><span data-stu-id="48d0b-305">The Azure Cosmos DB Bulk importer has the following additional advanced options:</span></span>

1. <span data-ttu-id="48d0b-306">Batchgrootte: Het hulpprogramma wordt standaard ingesteld op een batchgrootte van 50.</span><span class="sxs-lookup"><span data-stu-id="48d0b-306">Batch Size: The tool defaults to a batch size of 50.</span></span>  <span data-ttu-id="48d0b-307">Als de documenten die moeten worden geïmporteerd groot zijn, kunt u overwegen de batchgrootte te verlagen.</span><span class="sxs-lookup"><span data-stu-id="48d0b-307">If the documents to be imported are large, consider lowering the batch size.</span></span> <span data-ttu-id="48d0b-308">Als u daarentegen als de documenten die moeten worden geïmporteerd klein zijn, kunt u de batchgrootte verhogen.</span><span class="sxs-lookup"><span data-stu-id="48d0b-308">Conversely, if the documents to be imported are small, consider raising the batch size.</span></span>
2. <span data-ttu-id="48d0b-309">Maximum aantal Script-grootte (bytes): het hulpprogramma wordt standaard ingesteld op een script maximale grootte van 512KB</span><span class="sxs-lookup"><span data-stu-id="48d0b-309">Max Script Size (bytes): The tool defaults to a max script size of 512KB</span></span>
3. <span data-ttu-id="48d0b-310">Schakel automatische van generatie-Id: Als elk document dat moet worden geïmporteerd, een id-veld bevat, deze optie kan de prestaties verbeteren.</span><span class="sxs-lookup"><span data-stu-id="48d0b-310">Disable Automatic Id Generation: If every document to be imported contains an id field, then selecting this option can increase performance.</span></span> <span data-ttu-id="48d0b-311">Een unieke id-veld ontbreekt documenten worden niet geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="48d0b-311">Documents missing a unique id field will not be imported.</span></span>
4. <span data-ttu-id="48d0b-312">Update bestaande documenten: Het hulpprogramma wordt standaard ingesteld op niet vervangen door een bestaand document-id's.</span><span class="sxs-lookup"><span data-stu-id="48d0b-312">Update Existing Documents: The tool defaults to not replacing existing documents with id conflicts.</span></span> <span data-ttu-id="48d0b-313">Deze optie kunt bestaande documenten met overeenkomende id overschrijven.</span><span class="sxs-lookup"><span data-stu-id="48d0b-313">Selecting this option will allow overwriting existing documents with matching ids.</span></span> <span data-ttu-id="48d0b-314">Deze functie is handig voor geplande gegevens migraties die bijwerken van bestaande documenten.</span><span class="sxs-lookup"><span data-stu-id="48d0b-314">This feature is useful for scheduled data migrations that update existing documents.</span></span>
5. <span data-ttu-id="48d0b-315">Aantal nieuwe pogingen bij fouten: Hiermee geeft u het aantal keren opnieuw de verbinding met Azure Cosmos DB in geval van een tijdelijke fouten (bijvoorbeeld connectiviteit onderbreking op het netwerk).</span><span class="sxs-lookup"><span data-stu-id="48d0b-315">Number of Retries on Failure: Specifies the number of times to retry the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
6. <span data-ttu-id="48d0b-316">Interval voor opnieuw proberen: Geeft aan hoe lang moet worden gewacht tussen opnieuw verbinding met Azure Cosmos-database in geval van een tijdelijke fouten (bijvoorbeeld connectiviteit onderbreking op het netwerk).</span><span class="sxs-lookup"><span data-stu-id="48d0b-316">Retry Interval: Specifies how long to wait between retrying the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
7. <span data-ttu-id="48d0b-317">Verbindingsmodus: Hiermee geeft u de verbindingsmodus gebruiken met Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="48d0b-317">Connection Mode: Specifies the connection mode to use with Azure Cosmos DB.</span></span> <span data-ttu-id="48d0b-318">De beschikbare opties zijn DirectTcp, DirectHttps en Gateway.</span><span class="sxs-lookup"><span data-stu-id="48d0b-318">The available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="48d0b-319">De modi rechtstreekse verbinding zijn sneller, terwijl de gateway-modus meer firewall beschrijvende is aangezien hierbij alleen poort 443.</span><span class="sxs-lookup"><span data-stu-id="48d0b-319">The direct connection modes are faster, while the gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Schermopname van Azure Cosmos DB bulkimport geavanceerde opties](./media/import-data/docdbbulkoptions.png)

> [!TIP]
> <span data-ttu-id="48d0b-321">Het hulpprogramma voor importeren standaard verbindingsmodus DirectTcp.</span><span class="sxs-lookup"><span data-stu-id="48d0b-321">The import tool defaults to connection mode DirectTcp.</span></span> <span data-ttu-id="48d0b-322">Als u de firewall-problemen ondervindt, overschakelen naar verbindingsmodus Gateway, omdat hiervoor alleen poort 443.</span><span class="sxs-lookup"><span data-stu-id="48d0b-322">If you experience firewall issues, switch to connection mode Gateway, as it only requires port 443.</span></span>
> 
> 

## <span data-ttu-id="48d0b-323"><a id="DocumentDBSeqTarget"></a>Om te importeren naar de DocumentDB-API (sequentiële Record importeren)</span><span class="sxs-lookup"><span data-stu-id="48d0b-323"><a id="DocumentDBSeqTarget"></a>To import to the DocumentDB API (Sequential Record Import)</span></span>
<span data-ttu-id="48d0b-324">De importfunctie van Azure DB die Cosmos sequentiële record kunt u om te importeren uit een van de beschikbare opties op basis van door een andere record.</span><span class="sxs-lookup"><span data-stu-id="48d0b-324">The Azure Cosmos DB sequential record importer allows you to import from any of the available source options on a record by record basis.</span></span> <span data-ttu-id="48d0b-325">U kunt deze optie selecteren als u wilt importeren naar een bestaande collectie heeft het quotum van opgeslagen procedures bereikt.</span><span class="sxs-lookup"><span data-stu-id="48d0b-325">You might choose this option if you’re importing to an existing collection that has reached its quota of stored procedures.</span></span> <span data-ttu-id="48d0b-326">Het hulpprogramma ondersteunt importeren naar een verzameling van de Azure Cosmos DB één (één partitie en meerdere partitie), evenals shard importeren, waarbij de gegevens in Azure Cosmos DB meerdere verzamelingen voor één partitie en/of meerdere partitie zijn gepartitioneerd.</span><span class="sxs-lookup"><span data-stu-id="48d0b-326">The tool supports import to a single (both single-partition and multi-partition) Azure Cosmos DB collection, as well as sharded import whereby data is partitioned across multiple single-partition and/or multi-partition Azure Cosmos DB collections.</span></span> <span data-ttu-id="48d0b-327">Zie voor meer informatie over het partitioneren van gegevens, [partitionering en schalen in Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="48d0b-327">For more information about partitioning data, see [Partitioning and scaling in Azure Cosmos DB](partition-data.md).</span></span>

![Schermopname van Azure Cosmos DB-opties voor opeenvolgende record importeren](./media/import-data/documentdbsequential.png)

<span data-ttu-id="48d0b-329">De indeling van de Azure DB die Cosmos-verbindingsreeks is:</span><span class="sxs-lookup"><span data-stu-id="48d0b-329">The format of the Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="48d0b-330">De verbindingsreeks voor Azure DB die Cosmos-account kan worden opgehaald uit de blade sleutels van de Azure-portal, zoals beschreven in [het beheren van een account voor Azure Cosmos DB](manage-account.md), maar de naam van de database moet worden toegevoegd aan de verbinding de tekenreeks in de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="48d0b-330">The Azure Cosmos DB account connection string can be retrieved from the Keys blade of the Azure portal, as described in [How to manage an Azure Cosmos DB account](manage-account.md), however the name of the database needs to be appended to the connection string in the following format:</span></span>

    Database=<Azure Cosmos DB Database>;

> [!NOTE]
> <span data-ttu-id="48d0b-331">Gebruik de opdracht controleren om ervoor te zorgen dat het Azure DB die Cosmos-exemplaar dat is opgegeven in het veld connection string kan worden geopend.</span><span class="sxs-lookup"><span data-stu-id="48d0b-331">Use the Verify command to ensure that the Azure Cosmos DB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="48d0b-332">Als u wilt importeren naar één verzameling, voer de naam van de verzameling waarop gegevens worden geïmporteerd en klik op de knop toevoegen.</span><span class="sxs-lookup"><span data-stu-id="48d0b-332">To import to a single collection, enter the name of the collection to which data will be imported and click the Add button.</span></span> <span data-ttu-id="48d0b-333">Als u wilt importeren tot meerdere verzamelingen, voer de verzamelingsnaam van elke afzonderlijk of gebruik de volgende syntaxis om op te geven van meerdere verzamelingen: *collection_prefix*[begin index - end-index].</span><span class="sxs-lookup"><span data-stu-id="48d0b-333">To import to multiple collections, either enter each collection name individually or use the following syntax to specify multiple collections: *collection_prefix*[start index - end index].</span></span> <span data-ttu-id="48d0b-334">Houd rekening met het volgende bij het opgeven van meerdere verzamelingen via de hiervoor genoemde syntaxis:</span><span class="sxs-lookup"><span data-stu-id="48d0b-334">When specifying multiple collections via the aforementioned syntax, keep the following in mind:</span></span>

1. <span data-ttu-id="48d0b-335">Alleen geheel getal bereik bestandsnaampatronen worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="48d0b-335">Only integer range name patterns are supported.</span></span> <span data-ttu-id="48d0b-336">Bijvoorbeeld, geven verzameling [0-3] wordt produceren van de volgende verzamelingen: collection0, collection1, collection2, collection3.</span><span class="sxs-lookup"><span data-stu-id="48d0b-336">For example, specifying collection[0-3] will produce the following collections: collection0, collection1, collection2, collection3.</span></span>
2. <span data-ttu-id="48d0b-337">U kunt een verkorte syntaxis gebruiken: verzameling [3] wordt vermeld in stap 1 verzamelingen dezelfde set verzenden.</span><span class="sxs-lookup"><span data-stu-id="48d0b-337">You can use an abbreviated syntax: collection[3] will emit same set of collections mentioned in step 1.</span></span>
3. <span data-ttu-id="48d0b-338">Meer dan een vervanging kan worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="48d0b-338">More than one substitution can be provided.</span></span> <span data-ttu-id="48d0b-339">Bijvoorbeeld, verzameling [0-1] [0-9] genereert 20 verzamelingsnamen met toonaangevende nullen (collection01,... 02... 03).</span><span class="sxs-lookup"><span data-stu-id="48d0b-339">For example, collection[0-1] [0-9] will generate 20 collection names with leading zeros (collection01, ..02, ..03).</span></span>

<span data-ttu-id="48d0b-340">Wanneer de verzameling namen zijn opgegeven, kiest u de gewenste doorvoer van de verzameling(en) (400 RUs naar 250.000 RUs).</span><span class="sxs-lookup"><span data-stu-id="48d0b-340">Once the collection name(s) have been specified, choose the desired throughput of the collection(s) (400 RUs to 250,000 RUs).</span></span> <span data-ttu-id="48d0b-341">Kies een hogere doorvoer voor de beste prestaties importeren.</span><span class="sxs-lookup"><span data-stu-id="48d0b-341">For best import performance, choose a higher throughput.</span></span> <span data-ttu-id="48d0b-342">Zie voor meer informatie over prestatieniveaus [prestatieniveaus in Azure Cosmos DB](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="48d0b-342">For more information about performance levels, see [Performance levels in Azure Cosmos DB](performance-levels.md).</span></span> <span data-ttu-id="48d0b-343">Invoer voor verzamelingen met doorvoer > 10.000 RUs een partitiesleutel is vereist.</span><span class="sxs-lookup"><span data-stu-id="48d0b-343">Any import to collections with throughput >10,000 RUs will require a partition key.</span></span> <span data-ttu-id="48d0b-344">Als u ervoor kiest om meer dan 250.000 RUs, moet u naar het bestand van een aanvraag in de portal voor uw account wordt verhoogd.</span><span class="sxs-lookup"><span data-stu-id="48d0b-344">If you choose to have more than 250,000 RUs, you will need to file a request in the portal to have your account increased.</span></span>

> [!NOTE]
> <span data-ttu-id="48d0b-345">De doorvoer-instelling is alleen van toepassing op het maken van de verzameling.</span><span class="sxs-lookup"><span data-stu-id="48d0b-345">The throughput setting only applies to collection creation.</span></span> <span data-ttu-id="48d0b-346">Als de opgegeven verzameling al bestaat, wordt de doorvoer niet gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="48d0b-346">If the specified collection already exists, its throughput will not be modified.</span></span>
> 
> 

<span data-ttu-id="48d0b-347">Bij het importeren van meerdere verzamelingen, wordt in de import-hulpprogramma ondersteunt hash sharding gebaseerd.</span><span class="sxs-lookup"><span data-stu-id="48d0b-347">When importing to multiple collections, the import tool supports hash based sharding.</span></span> <span data-ttu-id="48d0b-348">Geef in dit scenario wordt de documenteigenschap dat u wilt gebruiken als de partitiesleutel (als partitiesleutel leeg is, documenten zijn shard willekeurig in de doel-verzamelingen).</span><span class="sxs-lookup"><span data-stu-id="48d0b-348">In this scenario, specify the document property you wish to use as the Partition Key (if Partition Key is left blank, documents will be sharded randomly across the target collections).</span></span>

<span data-ttu-id="48d0b-349">U kunt eventueel opgeven welk veld in de bron voor het importeren moet worden gebruikt als de eigenschap id van Azure DB die Cosmos-document tijdens het importeren (Let erop dat als documenten geen deze eigenschap bevatten, wordt het hulpprogramma voor importeren wordt gegenereerd zodra een GUID als de waarde van de id-eigenschap).</span><span class="sxs-lookup"><span data-stu-id="48d0b-349">You may optionally specify which field in the import source should be used as the Azure Cosmos DB document id property during the import (note that if documents do not contain this property, then the import tool will generate a GUID as the id property value).</span></span>

<span data-ttu-id="48d0b-350">Er zijn tijdens het importeren van een aantal geavanceerde opties beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="48d0b-350">There are a number of advanced options available during import.</span></span> <span data-ttu-id="48d0b-351">Eerst bij het importeren van datum-typen (bijvoorbeeld van SQL Server of MongoDB), kunt u tussen de drie opties voor importeren:</span><span class="sxs-lookup"><span data-stu-id="48d0b-351">First, when importing date types (e.g. from SQL Server or MongoDB), you can choose between three import options:</span></span>

 ![Schermopname van Azure Cosmos DB datum tijdopties importeren](./media/import-data/datetimeoptions.png)

* <span data-ttu-id="48d0b-353">Tekenreeks: Behouden als een string-waarde</span><span class="sxs-lookup"><span data-stu-id="48d0b-353">String: Persist as a string value</span></span>
* <span data-ttu-id="48d0b-354">Epoche: Behouden als een getalwaarde epoche</span><span class="sxs-lookup"><span data-stu-id="48d0b-354">Epoch: Persist as an Epoch number value</span></span>
* <span data-ttu-id="48d0b-355">Beide: Zowel tekenreeks als numerieke waarden epoche bewaard.</span><span class="sxs-lookup"><span data-stu-id="48d0b-355">Both: Persist both string and Epoch number values.</span></span> <span data-ttu-id="48d0b-356">Deze optie maakt u een subdocument, bijvoorbeeld: "date_joined": {'' waarde '': ' 2013-10-21T21:17:25.2410000Z ', ' epoche ': 1382390245}</span><span class="sxs-lookup"><span data-stu-id="48d0b-356">This option will create a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span></span>

<span data-ttu-id="48d0b-357">De Azure Cosmos DB - sequentiële record importfunctie heeft de volgende aanvullende geavanceerde opties:</span><span class="sxs-lookup"><span data-stu-id="48d0b-357">The Azure Cosmos DB - Sequential record importer has the following additional advanced options:</span></span>

1. <span data-ttu-id="48d0b-358">Aantal parallelle aanvragen: het hulpprogramma wordt standaard ingesteld op 2 parallelle aanvragen.</span><span class="sxs-lookup"><span data-stu-id="48d0b-358">Number of Parallel Requests: The tool defaults to 2 parallel requests.</span></span> <span data-ttu-id="48d0b-359">Als de documenten die moeten worden geïmporteerd klein zijn, kunt u overwegen het verhogen van het aantal parallelle aanvragen.</span><span class="sxs-lookup"><span data-stu-id="48d0b-359">If the documents to be imported are small, consider raising the number of parallel requests.</span></span> <span data-ttu-id="48d0b-360">Houd er rekening mee dat als dit nummer te veel wordt gegenereerd, de import beperking ondervinden.</span><span class="sxs-lookup"><span data-stu-id="48d0b-360">Note that if this number is raised too much, the import may experience throttling.</span></span>
2. <span data-ttu-id="48d0b-361">Schakel automatische van generatie-Id: Als elk document dat moet worden geïmporteerd, een id-veld bevat, deze optie kan de prestaties verbeteren.</span><span class="sxs-lookup"><span data-stu-id="48d0b-361">Disable Automatic Id Generation: If every document to be imported contains an id field, then selecting this option can increase performance.</span></span> <span data-ttu-id="48d0b-362">Een unieke id-veld ontbreekt documenten worden niet geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="48d0b-362">Documents missing a unique id field will not be imported.</span></span>
3. <span data-ttu-id="48d0b-363">Update bestaande documenten: Het hulpprogramma wordt standaard ingesteld op niet vervangen door een bestaand document-id's.</span><span class="sxs-lookup"><span data-stu-id="48d0b-363">Update Existing Documents: The tool defaults to not replacing existing documents with id conflicts.</span></span> <span data-ttu-id="48d0b-364">Deze optie kunt bestaande documenten met overeenkomende id overschrijven.</span><span class="sxs-lookup"><span data-stu-id="48d0b-364">Selecting this option will allow overwriting existing documents with matching ids.</span></span> <span data-ttu-id="48d0b-365">Deze functie is handig voor geplande gegevens migraties die bijwerken van bestaande documenten.</span><span class="sxs-lookup"><span data-stu-id="48d0b-365">This feature is useful for scheduled data migrations that update existing documents.</span></span>
4. <span data-ttu-id="48d0b-366">Aantal nieuwe pogingen bij fouten: Hiermee geeft u het aantal keren opnieuw de verbinding met Azure Cosmos DB in geval van een tijdelijke fouten (bijvoorbeeld connectiviteit onderbreking op het netwerk).</span><span class="sxs-lookup"><span data-stu-id="48d0b-366">Number of Retries on Failure: Specifies the number of times to retry the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
5. <span data-ttu-id="48d0b-367">Interval voor opnieuw proberen: Geeft aan hoe lang moet worden gewacht tussen opnieuw verbinding met Azure Cosmos-database in geval van een tijdelijke fouten (bijvoorbeeld connectiviteit onderbreking op het netwerk).</span><span class="sxs-lookup"><span data-stu-id="48d0b-367">Retry Interval: Specifies how long to wait between retrying the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
6. <span data-ttu-id="48d0b-368">Verbindingsmodus: Hiermee geeft u de verbindingsmodus gebruiken met Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="48d0b-368">Connection Mode: Specifies the connection mode to use with Azure Cosmos DB.</span></span> <span data-ttu-id="48d0b-369">De beschikbare opties zijn DirectTcp, DirectHttps en Gateway.</span><span class="sxs-lookup"><span data-stu-id="48d0b-369">The available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="48d0b-370">De modi rechtstreekse verbinding zijn sneller, terwijl de gateway-modus meer firewall beschrijvende is aangezien hierbij alleen poort 443.</span><span class="sxs-lookup"><span data-stu-id="48d0b-370">The direct connection modes are faster, while the gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Schermopname van Azure Cosmos DB sequentiële record importeren geavanceerde opties](./media/import-data/documentdbsequentialoptions.png)

> [!TIP]
> <span data-ttu-id="48d0b-372">Het hulpprogramma voor importeren standaard verbindingsmodus DirectTcp.</span><span class="sxs-lookup"><span data-stu-id="48d0b-372">The import tool defaults to connection mode DirectTcp.</span></span> <span data-ttu-id="48d0b-373">Als u de firewall-problemen ondervindt, overschakelen naar verbindingsmodus Gateway, omdat hiervoor alleen poort 443.</span><span class="sxs-lookup"><span data-stu-id="48d0b-373">If you experience firewall issues, switch to connection mode Gateway, as it only requires port 443.</span></span>
> 
> 

## <span data-ttu-id="48d0b-374"><a id="IndexingPolicy"></a>Een indexeringsbeleid opgeven bij het maken van Azure DB die Cosmos-verzamelingen</span><span class="sxs-lookup"><span data-stu-id="48d0b-374"><a id="IndexingPolicy"></a>Specify an indexing policy when creating Azure Cosmos DB collections</span></span>
<span data-ttu-id="48d0b-375">Als u om verzamelingen te maken tijdens het importeren van het hulpprogramma voor migratie toestaat, kunt u het indexeringsbeleid van de verzamelingen.</span><span class="sxs-lookup"><span data-stu-id="48d0b-375">When you allow the migration tool to create collections during import, you can specify the indexing policy of the collections.</span></span> <span data-ttu-id="48d0b-376">In de sectie Geavanceerde opties van de Azure Cosmos DB bulkimport en Azure Cosmos DB sequentiële record opties, navigeer naar de sectie beleid voor indexering.</span><span class="sxs-lookup"><span data-stu-id="48d0b-376">In the advanced options section of the Azure Cosmos DB Bulk import and Azure Cosmos DB Sequential record options, navigate to the Indexing Policy section.</span></span>

![Schermopname van Azure Cosmos DB indexeren beleid geavanceerde opties](./media/import-data/indexingpolicy1.png)

<span data-ttu-id="48d0b-378">Het indexeren beleid geavanceerde optie gebruikt, kunt u selecteren een bestand met beleidsregel van indexering, handmatig een indexeringsbeleid invoeren, of uit een reeks standaardsjablonen (met de rechtermuisknop te klikken in het tekstvak voor indexering beleid).</span><span class="sxs-lookup"><span data-stu-id="48d0b-378">Using the Indexing Policy advanced option, you can select an indexing policy file, manually enter an indexing policy, or select from a set of default templates (by right clicking in the indexing policy textbox).</span></span>

<span data-ttu-id="48d0b-379">De beleidssjablonen van die het hulpprogramma geeft zijn:</span><span class="sxs-lookup"><span data-stu-id="48d0b-379">The policy templates the tool provides are:</span></span>

* <span data-ttu-id="48d0b-380">De standaardinstelling.</span><span class="sxs-lookup"><span data-stu-id="48d0b-380">Default.</span></span> <span data-ttu-id="48d0b-381">Dit beleid wordt aanbevolen wanneer u het uitvoeren van de gelijkheid query uitgevoerd naar tekenreeksen en ORDER BY, bereik en gelijkheid query's gebruiken voor getallen.</span><span class="sxs-lookup"><span data-stu-id="48d0b-381">This policy is best when you’re performing equality queries against strings and using ORDER BY, range, and equality queries for numbers.</span></span> <span data-ttu-id="48d0b-382">Dit beleid heeft een lagere opslagoverhead voor indexering dan bereik.</span><span class="sxs-lookup"><span data-stu-id="48d0b-382">This policy has a lower index storage overhead than Range.</span></span>
* <span data-ttu-id="48d0b-383">Het bereik.</span><span class="sxs-lookup"><span data-stu-id="48d0b-383">Range.</span></span> <span data-ttu-id="48d0b-384">Dit beleid wordt aanbevolen u ORDER BY, bereik en gelijkheid query's op de cijfers en tekenreeksen.</span><span class="sxs-lookup"><span data-stu-id="48d0b-384">This policy is best you’re using ORDER BY, range and equality queries on both numbers and strings.</span></span> <span data-ttu-id="48d0b-385">Dit beleid heeft een hogere opslagoverhead voor indexering dan standaard of hash-bewerking.</span><span class="sxs-lookup"><span data-stu-id="48d0b-385">This policy has a higher index storage overhead than Default or Hash.</span></span>

![Schermopname van Azure Cosmos DB indexeren beleid geavanceerde opties](./media/import-data/indexingpolicy2.png)

> [!NOTE]
> <span data-ttu-id="48d0b-387">Als u een indexeringsbeleid niet opgeeft, wordt het standaardbeleid worden toegepast.</span><span class="sxs-lookup"><span data-stu-id="48d0b-387">If you do not specify an indexing policy, then the default policy will be applied.</span></span> <span data-ttu-id="48d0b-388">Zie voor meer informatie over indexering beleid [Azure Cosmos DB indexeren beleid](indexing-policies.md).</span><span class="sxs-lookup"><span data-stu-id="48d0b-388">For more information about indexing policies, see [Azure Cosmos DB indexing policies](indexing-policies.md).</span></span>
> 
> 

## <a name="export-to-json-file"></a><span data-ttu-id="48d0b-389">Exporteren naar JSON-bestand</span><span class="sxs-lookup"><span data-stu-id="48d0b-389">Export to JSON file</span></span>
<span data-ttu-id="48d0b-390">De exportfunctie Azure Cosmos DB JSON kunt u een van de beschikbare opties voor exporteren naar een JSON-bestand met een matrix met JSON-documenten.</span><span class="sxs-lookup"><span data-stu-id="48d0b-390">The Azure Cosmos DB JSON exporter allows you to export any of the available source options to a JSON file that contains an array of JSON documents.</span></span> <span data-ttu-id="48d0b-391">Het hulpprogramma wordt afgehandeld tijdens de export voor u of u kunt kiezen om de resulterende migratie-opdracht weer en voer de opdracht zelf.</span><span class="sxs-lookup"><span data-stu-id="48d0b-391">The tool will handle the export for you, or you can choose to view the resulting migration command and run the command yourself.</span></span> <span data-ttu-id="48d0b-392">Het resulterende JSON-bestand kan worden opgeslagen, lokaal of in Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="48d0b-392">The resulting JSON file may be stored locally or in Azure Blob storage.</span></span>

![Schermopname van Azure Cosmos DB JSON-optie voor het exporteren van lokaal bestand](./media/import-data/jsontarget.png)

![Schermopname van Azure Cosmos DB JSON Azure Blob storage exportoptie](./media/import-data/jsontarget2.png)

<span data-ttu-id="48d0b-395">U kunt eventueel de resulterende JSON die de grootte van het resulterende document vergroot tijdens het maken van de inhoud meer prettify leesbaar.</span><span class="sxs-lookup"><span data-stu-id="48d0b-395">You may optionally choose to prettify the resulting JSON, which will increase the size of the resulting document while making the contents more human readable.</span></span>

    Standard JSON export
    [{"id":"Sample","Title":"About Paris","Language":{"Name":"English"},"Author":{"Name":"Don","Location":{"City":"Paris","Country":"France"}},"Content":"Don's document in Azure Cosmos DB is a valid JSON document as defined by the JSON spec.","PageViews":10000,"Topics":[{"Title":"History of Paris"},{"Title":"Places to see in Paris"}]}]

    Prettified JSON export
    [
     {
    "id": "Sample",
    "Title": "About Paris",
    "Language": {
      "Name": "English"
    },
    "Author": {
      "Name": "Don",
      "Location": {
        "City": "Paris",
        "Country": "France"
      }
    },
    "Content": "Don's document in Azure Cosmos DB is a valid JSON document as defined by the JSON spec.",
    "PageViews": 10000,
    "Topics": [
      {
        "Title": "History of Paris"
      },
      {
        "Title": "Places to see in Paris"
      }
    ]
    }]

## <a name="advanced-configuration"></a><span data-ttu-id="48d0b-396">Geavanceerde configuratie</span><span class="sxs-lookup"><span data-stu-id="48d0b-396">Advanced configuration</span></span>
<span data-ttu-id="48d0b-397">Geef de locatie van het logboekbestand waarnaar u eventuele fouten die zijn geschreven dat wilt in het scherm Geavanceerde configuratie.</span><span class="sxs-lookup"><span data-stu-id="48d0b-397">In the Advanced configuration screen, specify the location of the log file to which you would like any errors written.</span></span> <span data-ttu-id="48d0b-398">De volgende regels zijn van toepassing op deze pagina:</span><span class="sxs-lookup"><span data-stu-id="48d0b-398">The following rules apply to this page:</span></span>

1. <span data-ttu-id="48d0b-399">Als een bestandsnaam niet opgegeven is, wordt op de pagina met alle fouten geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="48d0b-399">If a file name is not provided, then all errors will be returned on the Results page.</span></span>
2. <span data-ttu-id="48d0b-400">Als een bestandsnaam is opgegeven zonder een map, zal klikt u vervolgens het bestand worden gemaakt (of overschreven) in de huidige map in de omgeving.</span><span class="sxs-lookup"><span data-stu-id="48d0b-400">If a file name is provided without a directory, then the file will be created (or overwritten) in the current environment directory.</span></span>
3. <span data-ttu-id="48d0b-401">Als u een bestaand bestand en vervolgens het bestand wordt overschreven, er is geen optie toevoegen.</span><span class="sxs-lookup"><span data-stu-id="48d0b-401">If you select an existing file, then the file will be overwritten, there is no append option.</span></span>

<span data-ttu-id="48d0b-402">Kies of u aan te melden, kritiek, of er geen foutberichten.</span><span class="sxs-lookup"><span data-stu-id="48d0b-402">Then, choose whether to log all, critical, or no error messages.</span></span> <span data-ttu-id="48d0b-403">Ten slotte kunt u bepalen hoe vaak het bericht voor overdracht van op scherm wordt bijgewerkt met de voortgang ervan.</span><span class="sxs-lookup"><span data-stu-id="48d0b-403">Finally, decide how frequently the on screen transfer message will be updated with its progress.</span></span>

    ![Screenshot of Advanced configuration screen](./media/import-data/AdvancedConfiguration.png)

## <a name="confirm-import-settings-and-view-command-line"></a><span data-ttu-id="48d0b-404">Bevestig de instellingen importeren en weergeven vanaf de opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="48d0b-404">Confirm import settings and view command line</span></span>
1. <span data-ttu-id="48d0b-405">Na het opgeven van informatie van gegevensbron, doelinformatie en geavanceerde configuratie controleren van de migratie samenvatting en, desgewenst weergeven/kopiëren de resulterende migratie-opdracht (kopiëren van de opdracht is nuttig voor het automatiseren van importbewerkingen):</span><span class="sxs-lookup"><span data-stu-id="48d0b-405">After specifying source information, target information, and advanced configuration, review the migration summary and, optionally, view/copy the resulting migration command (copying the command is useful to automate import operations):</span></span>
   
    ![Schermopname van het scherm Samenvatting](./media/import-data/summary.png)
   
    ![Schermopname van het scherm Samenvatting](./media/import-data/summarycommand.png)
2. <span data-ttu-id="48d0b-408">Wanneer u tevreden met de bron en doel-opties bent, klikt u op **importeren**.</span><span class="sxs-lookup"><span data-stu-id="48d0b-408">Once you’re satisfied with your source and target options, click **Import**.</span></span> <span data-ttu-id="48d0b-409">De verstreken tijd, aantal verzonden en foutgegevens (als u een bestandsnaam in de geavanceerde configuratie niet opgeven) wordt bijgewerkt, omdat het importeren in het proces.</span><span class="sxs-lookup"><span data-stu-id="48d0b-409">The elapsed time, transferred count, and failure information (if you didn't provide a file name in the Advanced configuration) will update as the import is in process.</span></span> <span data-ttu-id="48d0b-410">Als u klaar is, kunt u de resultaten exporteren (bijvoorbeeld om te gaan met eventuele fouten importeren).</span><span class="sxs-lookup"><span data-stu-id="48d0b-410">Once complete, you can export the results (e.g. to deal with any import failures).</span></span>
   
    ![Schermopname van Azure Cosmos DB JSON exportoptie](./media/import-data/viewresults.png)
3. <span data-ttu-id="48d0b-412">U kunt ook een nieuwe import starten te behouden de bestaande instellingen (bijvoorbeeld verbinding tekenreeks informatie, de bron en doel keuze, etc.) of opnieuw instellen van alle waarden.</span><span class="sxs-lookup"><span data-stu-id="48d0b-412">You may also start a new import, either keeping the existing settings (e.g. connection string information, source and target choice, etc.) or resetting all values.</span></span>
   
    ![Schermopname van Azure Cosmos DB JSON exportoptie](./media/import-data/newimport.png)

## <a name="next-steps"></a><span data-ttu-id="48d0b-414">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="48d0b-414">Next steps</span></span>

<span data-ttu-id="48d0b-415">In deze zelfstudie hebt u het volgende gedaan:</span><span class="sxs-lookup"><span data-stu-id="48d0b-415">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="48d0b-416">Het hulpprogramma voor gegevensmigratie is geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="48d0b-416">Installed the Data Migration tool</span></span>
> * <span data-ttu-id="48d0b-417">Geïmporteerde gegevens uit verschillende gegevensbronnen</span><span class="sxs-lookup"><span data-stu-id="48d0b-417">Imported data from different data sources</span></span>
> * <span data-ttu-id="48d0b-418">Uit Azure Cosmos DB geëxporteerd naar JSON</span><span class="sxs-lookup"><span data-stu-id="48d0b-418">Exported from Azure Cosmos DB to JSON</span></span>

<span data-ttu-id="48d0b-419">U kunt nu doorgaan met de volgende zelfstudie en informatie over het opvragen van gegevens met behulp van Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="48d0b-419">You can now proceed to the next tutorial and learn how to query data using Azure Cosmos DB.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="48d0b-420">Hoe kan ik een query over gegevens?</span><span class="sxs-lookup"><span data-stu-id="48d0b-420">How to query data?</span></span>](../cosmos-db/tutorial-query-documentdb.md)
