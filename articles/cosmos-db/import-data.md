---
title: hulpprogramma voor migratie van aaaDatabase voor Azure Cosmos DB | Microsoft Docs
description: Meer informatie over hoe toouse Hallo bron Azure Cosmos DB gegevens migration tools tooimport gegevens tooAzure Cosmos-DB uit diverse bronnen, met inbegrip van MongoDB, SQL Server, Table storage, Amazon DynamoDB, CSV en JSON-bestanden worden geopend. CSV tooJSON conversie.
keywords: CSV toojson, hulpprogramma's voor migratie, converteren csv toojson
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
ms.openlocfilehash: 997648a31602d854db75bb6ce4e2ecff36fc1069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimport-data-into-azure-cosmos-db-for-hello-documentdb-api"></a><span data-ttu-id="44878-105">Hoe Hallo tooimport gegevens naar Azure Cosmos DB voor DocumentDB API?</span><span class="sxs-lookup"><span data-stu-id="44878-105">How tooimport data into Azure Cosmos DB for hello DocumentDB API?</span></span>

<span data-ttu-id="44878-106">Deze zelfstudie bevat instructies over het gebruik van Azure DB die Cosmos Hallo: hulpprogramma voor gegevensmigratie voor DocumentDB-API, die u gegevens uit diverse bronnen importeren kunt, met inbegrip van JSON-bestanden, CSV-bestanden, SQL, MongoDB, Azure Table storage, Amazon DynamoDB en Azure Cosmos DB DocumentDB API-verzamelingen in verzamelingen voor gebruiken met Azure Cosmos DB en Hallo DocumentDB-API.</span><span class="sxs-lookup"><span data-stu-id="44878-106">This tutorial provides instructions on using hello Azure Cosmos DB: DocumentDB API Data Migration tool, which can import data from various sources, including JSON files, CSV files, SQL, MongoDB, Azure Table storage, Amazon DynamoDB and Azure Cosmos DB DocumentDB API collections into collections for use with Azure Cosmos DB and hello DocumentDB API.</span></span> <span data-ttu-id="44878-107">hulpprogramma voor gegevensmigratie Hallo kan ook worden gebruikt bij het migreren van een verzameling van één partitie verzameling tooa meerdere partitie voor Hallo DocumentDB-API.</span><span class="sxs-lookup"><span data-stu-id="44878-107">hello Data Migration tool can also be used when migrating from a single partition collection tooa multi-partition collection for hello DocumentDB API.</span></span>

<span data-ttu-id="44878-108">hulpprogramma voor gegevensmigratie Hallo werkt alleen wanneer het importeren van gegevens naar Azure Cosmos DB voor gebruik met Hallo DocumentDB-API.</span><span class="sxs-lookup"><span data-stu-id="44878-108">hello Data Migration tool only works when importing data into Azure Cosmos DB for use with hello DocumentDB API.</span></span> <span data-ttu-id="44878-109">Het importeren van gegevens voor gebruik met Hallo tabel API of Graph API wordt niet ondersteund op dit moment.</span><span class="sxs-lookup"><span data-stu-id="44878-109">Importing data for use with hello Table API or Graph API is not supported at this time.</span></span> 

<span data-ttu-id="44878-110">tooimport gegevens voor gebruik met Hallo MongoDB-API, Zie [Azure Cosmos DB: hoe toomigrate-gegevens voor de MongoDB-API Hallo?](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="44878-110">tooimport data for use with hello MongoDB API, see [Azure Cosmos DB: How toomigrate data for hello MongoDB API?](mongodb-migrate.md).</span></span>

<span data-ttu-id="44878-111">Deze zelfstudie behandelt Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="44878-111">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="44878-112">Hallo-hulpprogramma voor gegevensmigratie installeren</span><span class="sxs-lookup"><span data-stu-id="44878-112">Installing hello Data Migration tool</span></span>
> * <span data-ttu-id="44878-113">Het importeren van gegevens uit verschillende gegevensbronnen</span><span class="sxs-lookup"><span data-stu-id="44878-113">Importing data from different data sources</span></span>
> * <span data-ttu-id="44878-114">Exporteren van Azure DB die Cosmos tooJSON</span><span class="sxs-lookup"><span data-stu-id="44878-114">Exporting from Azure Cosmos DB tooJSON</span></span>

## <span data-ttu-id="44878-115"><a id="Prerequisites"></a>Vereisten</span><span class="sxs-lookup"><span data-stu-id="44878-115"><a id="Prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="44878-116">Zorg ervoor dat er Hallo volgende zijn geïnstalleerd voordat Hallo-instructies in dit artikel:</span><span class="sxs-lookup"><span data-stu-id="44878-116">Before following hello instructions in this article, ensure that you have hello following installed:</span></span>

* <span data-ttu-id="44878-117">[Microsoft .NET Framework 4,51](https://www.microsoft.com/download/developer-tools.aspx) of hoger.</span><span class="sxs-lookup"><span data-stu-id="44878-117">[Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) or higher.</span></span>

## <span data-ttu-id="44878-118"><a id="Overviewl"></a>Overzicht van het hulpprogramma voor gegevensmigratie Hallo</span><span class="sxs-lookup"><span data-stu-id="44878-118"><a id="Overviewl"></a>Overview of hello Data Migration tool</span></span>
<span data-ttu-id="44878-119">Hallo-hulpprogramma voor gegevensmigratie is een open-source-oplossing die gegevens tooAzure Cosmos DB uit diverse bronnen importeert, met inbegrip van:</span><span class="sxs-lookup"><span data-stu-id="44878-119">hello Data Migration tool is an open source solution that imports data tooAzure Cosmos DB from a variety of sources, including:</span></span>

* <span data-ttu-id="44878-120">JSON-bestanden</span><span class="sxs-lookup"><span data-stu-id="44878-120">JSON files</span></span>
* <span data-ttu-id="44878-121">MongoDB</span><span class="sxs-lookup"><span data-stu-id="44878-121">MongoDB</span></span>
* <span data-ttu-id="44878-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="44878-122">SQL Server</span></span>
* <span data-ttu-id="44878-123">CSV-bestanden</span><span class="sxs-lookup"><span data-stu-id="44878-123">CSV files</span></span>
* <span data-ttu-id="44878-124">Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="44878-124">Azure Table storage</span></span>
* <span data-ttu-id="44878-125">Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="44878-125">Amazon DynamoDB</span></span>
* <span data-ttu-id="44878-126">HBase</span><span class="sxs-lookup"><span data-stu-id="44878-126">HBase</span></span>
* <span data-ttu-id="44878-127">Azure DB Cosmos-verzamelingen</span><span class="sxs-lookup"><span data-stu-id="44878-127">Azure Cosmos DB collections</span></span>

<span data-ttu-id="44878-128">Tijdens het Hallo-import-hulpprogramma omvat een grafische gebruikersinterface (dtui.exe), kan het ook aangestuurd vanaf de opdrachtregel hello (dt.exe).</span><span class="sxs-lookup"><span data-stu-id="44878-128">While hello import tool includes a graphical user interface (dtui.exe), it can also be driven from hello command line (dt.exe).</span></span> <span data-ttu-id="44878-129">Er is in feite een opdracht optie toooutput Hallo die zijn gekoppeld na het instellen van een import via Hallo gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="44878-129">In fact, there is an option toooutput hello associated command after setting up an import through hello UI.</span></span> <span data-ttu-id="44878-130">In tabelvorm brongegevens (bijvoorbeeld SQL Server- of CSV-bestanden) kan worden getransformeerd zodat hiërarchische relaties (subdocumenten) kunnen worden gemaakt tijdens het importeren.</span><span class="sxs-lookup"><span data-stu-id="44878-130">Tabular source data (e.g. SQL Server or CSV files) can be transformed such that hierarchical relationships (subdocuments) can be created during import.</span></span> <span data-ttu-id="44878-131">Houd lezen toolearn meer informatie over opties voor gegevensbron voorbeeld opdrachtregels tooimport van elke bron, doel-opties en weer te geven resultaten importeren.</span><span class="sxs-lookup"><span data-stu-id="44878-131">Keep reading toolearn more about source options, sample command lines tooimport from each source, target options, and viewing import results.</span></span>

## <span data-ttu-id="44878-132"><a id="Install"></a>Hallo-hulpprogramma voor gegevensmigratie installeren</span><span class="sxs-lookup"><span data-stu-id="44878-132"><a id="Install"></a>Install hello Data Migration tool</span></span>
<span data-ttu-id="44878-133">broncode van Hallo migratie hulpprogramma is beschikbaar op GitHub in [deze opslagplaats](https://github.com/azure/azure-documentdb-datamigrationtool) en een gecompileerde versie is beschikbaar vanuit [Microsoft Download Center](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d).</span><span class="sxs-lookup"><span data-stu-id="44878-133">hello migration tool source code is available on GitHub in [this repository](https://github.com/azure/azure-documentdb-datamigrationtool) and a compiled version is available from [Microsoft Download Center](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d).</span></span> <span data-ttu-id="44878-134">U kunt compileren Hallo oplossing of gewoon downloaden en extraheren Hallo gecompileerde versie tooa directory van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="44878-134">You may either compile hello solution or simply download and extract hello compiled version tooa directory of your choice.</span></span> <span data-ttu-id="44878-135">Voer vervolgens een:</span><span class="sxs-lookup"><span data-stu-id="44878-135">Then run either:</span></span>

* <span data-ttu-id="44878-136">**Dtui.exe**: versie van de grafische interface van Hallo-hulpprogramma</span><span class="sxs-lookup"><span data-stu-id="44878-136">**Dtui.exe**: Graphical interface version of hello tool</span></span>
* <span data-ttu-id="44878-137">**DT.exe**: opdrachtregelprogramma versie van Hallo-hulpprogramma</span><span class="sxs-lookup"><span data-stu-id="44878-137">**Dt.exe**: Command-line version of hello tool</span></span>

## <a name="import-data"></a><span data-ttu-id="44878-138">Gegevens importeren</span><span class="sxs-lookup"><span data-stu-id="44878-138">Import data</span></span>

<span data-ttu-id="44878-139">Zodra u Hallo-hulpprogramma hebt geïnstalleerd, is het tijd tooimport uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="44878-139">Once you've installed hello tool, it's time tooimport your data.</span></span> <span data-ttu-id="44878-140">Welk type gegevens wilt u toch tooimport?</span><span class="sxs-lookup"><span data-stu-id="44878-140">What kind of data do you want tooimport?</span></span>

* [<span data-ttu-id="44878-141">JSON-bestanden</span><span class="sxs-lookup"><span data-stu-id="44878-141">JSON files</span></span>](#JSON)
* [<span data-ttu-id="44878-142">MongoDB</span><span class="sxs-lookup"><span data-stu-id="44878-142">MongoDB</span></span>](#MongoDB)
* [<span data-ttu-id="44878-143">MongoDB exportbestanden</span><span class="sxs-lookup"><span data-stu-id="44878-143">MongoDB Export files</span></span>](#MongoDBExport)
* [<span data-ttu-id="44878-144">SQL Server</span><span class="sxs-lookup"><span data-stu-id="44878-144">SQL Server</span></span>](#SQL)
* [<span data-ttu-id="44878-145">CSV-bestanden</span><span class="sxs-lookup"><span data-stu-id="44878-145">CSV files</span></span>](#CSV)
* [<span data-ttu-id="44878-146">Azure Table storage</span><span class="sxs-lookup"><span data-stu-id="44878-146">Azure Table storage</span></span>](#AzureTableSource)
* [<span data-ttu-id="44878-147">Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="44878-147">Amazon DynamoDB</span></span>](#DynamoDBSource)
* [<span data-ttu-id="44878-148">BLOB</span><span class="sxs-lookup"><span data-stu-id="44878-148">Blob</span></span>](#BlobImport)
* [<span data-ttu-id="44878-149">Azure DB Cosmos-verzamelingen</span><span class="sxs-lookup"><span data-stu-id="44878-149">Azure Cosmos DB collections</span></span>](#DocumentDBSource)
* [<span data-ttu-id="44878-150">HBase</span><span class="sxs-lookup"><span data-stu-id="44878-150">HBase</span></span>](#HBaseSource)
* [<span data-ttu-id="44878-151">Azure DB Cosmos bulkimport</span><span class="sxs-lookup"><span data-stu-id="44878-151">Azure Cosmos DB bulk import</span></span>](#DocumentDBBulkImport)
* [<span data-ttu-id="44878-152">Azure DB Cosmos sequentiële record importeren</span><span class="sxs-lookup"><span data-stu-id="44878-152">Azure Cosmos DB sequential record import</span></span>](#DocumentDSeqTarget)


## <span data-ttu-id="44878-153"><a id="JSON"></a>tooimport JSON-bestanden</span><span class="sxs-lookup"><span data-stu-id="44878-153"><a id="JSON"></a>tooimport JSON files</span></span>
<span data-ttu-id="44878-154">Hallo JSON-bestand bron importfunctie optie kunt u tooimport een of meer JSON-bestanden voor één document of JSON-bestanden dat elk een matrix met JSON-documenten bevatten.</span><span class="sxs-lookup"><span data-stu-id="44878-154">hello JSON file source importer option allows you tooimport one or more single document JSON files or JSON files that each contain an array of JSON documents.</span></span> <span data-ttu-id="44878-155">Als u mappen met JSON-bestanden tooimport toevoegt, hebt u de mogelijkheid Hallo van recursief zoeken naar bestanden in submappen.</span><span class="sxs-lookup"><span data-stu-id="44878-155">When adding folders that contain JSON files tooimport, you have hello option of recursively searching for files in subfolders.</span></span>

![Schermopname van JSON-bestand bronopties - hulpprogramma's voor migratie](./media/import-data/jsonsource.png)

<span data-ttu-id="44878-157">Hier volgen enkele opdrachtregel voorbeelden tooimport JSON-bestanden:</span><span class="sxs-lookup"><span data-stu-id="44878-157">Here are some command line samples tooimport JSON files:</span></span>

    #Import a single JSON file
    dt.exe /s:JsonFile /s.Files:.\Sessions.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory of JSON files
    dt.exe /s:JsonFile /s.Files:C:\TESessions\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory (including sub-directories) of JSON files
    dt.exe /s:JsonFile /s.Files:C:\LastFMMusic\**\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Music /t.CollectionThroughput:2500

    #Import a directory (single), directory (recursive), and individual JSON files
    dt.exe /s:JsonFile /s.Files:C:\Tweets\*.*;C:\LargeDocs\**\*.*;C:\TESessions\Session48172.json;C:\TESessions\Session48173.json;C:\TESessions\Session48174.json;C:\TESessions\Session48175.json;C:\TESessions\Session48177.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:subs /t.CollectionThroughput:2500

    #Import a single JSON file and partition hello data across 4 collections
    dt.exe /s:JsonFile /s.Files:D:\\CompanyData\\Companies.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:comp[1-4] /t.PartitionKey:name /t.CollectionThroughput:2500

## <span data-ttu-id="44878-158"><a id="MongoDB"></a>tooimport van MongoDB</span><span class="sxs-lookup"><span data-stu-id="44878-158"><a id="MongoDB"></a>tooimport from MongoDB</span></span>

> [!IMPORTANT]
> <span data-ttu-id="44878-159">Als u Azure DB die Cosmos-account met ondersteuning voor MongoDB tooan importeert, volgt u deze [instructies](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="44878-159">If you are importing tooan Azure Cosmos DB account with Support for MongoDB, follow these [instructions](mongodb-migrate.md).</span></span>
> 
> 

<span data-ttu-id="44878-160">Hallo MongoDB bron importfunctie optie kunt u tooimport uit een afzonderlijke MongoDB-verzameling en filter optioneel documenten met behulp van een query en/of Hallo documentstructuur wijzigen met behulp van een projectie.</span><span class="sxs-lookup"><span data-stu-id="44878-160">hello MongoDB source importer option allows you tooimport from an individual MongoDB collection and optionally filter documents using a query and/or modify hello document structure by using a projection.</span></span>  

![Schermopname van MongoDB-opties voor gegevensbron](./media/import-data/mongodbsource.png)

<span data-ttu-id="44878-162">Hallo-verbindingsreeks is in de Hallo standaard MongoDB-indeling:</span><span class="sxs-lookup"><span data-stu-id="44878-162">hello connection string is in hello standard MongoDB format:</span></span>

    mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database>

> [!NOTE]
> <span data-ttu-id="44878-163">Gebruik Hallo controleren opdracht tooensure die Hallo MongoDB-exemplaar is opgegeven in tekenreeksveld Hallo-verbinding kan worden benaderd.</span><span class="sxs-lookup"><span data-stu-id="44878-163">Use hello Verify command tooensure that hello MongoDB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="44878-164">Voer de naam Hallo van Hallo-verzameling van waaruit de gegevens worden geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="44878-164">Enter hello name of hello collection from which data will be imported.</span></span> <span data-ttu-id="44878-165">U kunt eventueel opgeven of een bestand voor een query opgeven (bijvoorbeeld {pop: {$gt: 5000}}) en/of een projectie (bijvoorbeeld {loc:0}) tooboth filter en vorm Hallo gegevens toobe geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="44878-165">You may optionally specify or provide a file for a query (e.g. {pop: {$gt:5000}} ) and/or projection (e.g. {loc:0} ) tooboth filter and shape hello data toobe imported.</span></span>

<span data-ttu-id="44878-166">Hier volgen enkele tooimport opdrachtregel voorbeelden van MongoDB:</span><span class="sxs-lookup"><span data-stu-id="44878-166">Here are some command line samples tooimport from MongoDB:</span></span>

    #Import all documents from a MongoDB collection
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZips /t.IdField:_id /t.CollectionThroughput:2500

    #Import documents from a MongoDB collection which match hello query and exclude hello loc field
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /s.Query:{pop:{$gt:50000}} /s.Projection:{loc:0} /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZipsTransform /t.IdField:_id/t.CollectionThroughput:2500

## <span data-ttu-id="44878-167"><a id="MongoDBExport"></a>tooimport MongoDB exportbestanden</span><span class="sxs-lookup"><span data-stu-id="44878-167"><a id="MongoDBExport"></a>tooimport MongoDB export files</span></span>

> [!IMPORTANT]
> <span data-ttu-id="44878-168">Als u Azure DB die Cosmos-account met ondersteuning voor MongoDB tooan importeert, volgt u deze [instructies](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="44878-168">If you are importing tooan Azure Cosmos DB account with support for MongoDB, follow these [instructions](mongodb-migrate.md).</span></span>
> 
> 

<span data-ttu-id="44878-169">Hallo importfunctie optie voor de gegevensbron van MongoDB export JSON-bestand kunt u tooimport een of meer JSON-bestanden die zijn geproduceerd met Hallo mongoexport hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="44878-169">hello MongoDB export JSON file source importer option allows you tooimport one or more JSON files produced from hello mongoexport utility.</span></span>  

![Schermopname van MongoDB-exportopties bron](./media/import-data/mongodbexportsource.png)

<span data-ttu-id="44878-171">Als u mappen met MongoDB export JSON-bestanden voor het importeren van toevoegt, hebt u de mogelijkheid Hallo van recursief zoeken naar bestanden in submappen.</span><span class="sxs-lookup"><span data-stu-id="44878-171">When adding folders that contain MongoDB export JSON files for import, you have hello option of recursively searching for files in subfolders.</span></span>

<span data-ttu-id="44878-172">Hier volgt een opdrachtregel voorbeeld tooimport van MongoDB export JSON-bestanden:</span><span class="sxs-lookup"><span data-stu-id="44878-172">Here is a command line sample tooimport from MongoDB export JSON files:</span></span>

    dt.exe /s:MongoDBExport /s.Files:D:\mongoemployees.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:employees /t.IdField:_id /t.Dates:Epoch /t.CollectionThroughput:2500

## <span data-ttu-id="44878-173"><a id="SQL"></a>tooimport van SQL Server</span><span class="sxs-lookup"><span data-stu-id="44878-173"><a id="SQL"></a>tooimport from SQL Server</span></span>
<span data-ttu-id="44878-174">Hallo SQL bron importfunctie optie kunt u tooimport uit een afzonderlijke SQL Server-database en filter optioneel Hallo records toobe geïmporteerd met behulp van een query.</span><span class="sxs-lookup"><span data-stu-id="44878-174">hello SQL source importer option allows you tooimport from an individual SQL Server database and optionally filter hello records toobe imported using a query.</span></span> <span data-ttu-id="44878-175">Bovendien kunt u de documentstructuur Hallo wijzigen door op te geven van een geneste scheidingsteken (meer informatie over die later).</span><span class="sxs-lookup"><span data-stu-id="44878-175">In addition, you can modify hello document structure by specifying a nesting separator (more on that in a moment).</span></span>  

![Schermafbeelding van de SQL - opties voor hulpprogramma's voor migratie](./media/import-data/sqlexportsource.png)

<span data-ttu-id="44878-177">Hallo-indeling van de verbindingsreeks Hallo is Hallo standaard SQL indeling voor een verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="44878-177">hello format of hello connection string is hello standard SQL connection string format.</span></span>

> [!NOTE]
> <span data-ttu-id="44878-178">Gebruik Hallo controleren opdracht tooensure die SQL Server-exemplaar is opgegeven in Hallo verbinding tekenreeksveld Hallo toegankelijk zijn.</span><span class="sxs-lookup"><span data-stu-id="44878-178">Use hello Verify command tooensure that hello SQL Server instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="44878-179">Hallo nesten scheidingsteken eigenschap wordt gebruikte toocreate hiërarchische relaties (onderliggende documenten) tijdens het importeren.</span><span class="sxs-lookup"><span data-stu-id="44878-179">hello nesting separator property is used toocreate hierarchical relationships (sub-documents) during import.</span></span> <span data-ttu-id="44878-180">Houd rekening met Hallo SQL-query te volgen:</span><span class="sxs-lookup"><span data-stu-id="44878-180">Consider hello following SQL query:</span></span>

<span data-ttu-id="44878-181">*CAST (BusinessEntityID AS varchar) als de Id, naam, adrestype als [Address.AddressType], AddressLine1 als [Address.AddressLine1], plaats als [Address.Location.City], StateProvinceName als [Address.Location.StateProvinceName], postcode als [selecteren Address.PostalCode] CountryRegionName als [Address.CountryRegionName] uit Sales.vStoreWithAddresses waar adrestype = 'Hoofdkantoor'*</span><span class="sxs-lookup"><span data-stu-id="44878-181">*select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'*</span></span>

<span data-ttu-id="44878-182">Die resulteert hello (gedeeltelijke) resultaten te volgen:</span><span class="sxs-lookup"><span data-stu-id="44878-182">Which returns hello following (partial) results:</span></span>

![Schermafbeelding van de SQL-queryresultaten](./media/import-data/sqlqueryresults.png)

<span data-ttu-id="44878-184">Houd er rekening mee Hallo aliassen zoals Address.AddressType en Address.Location.StateProvinceName.</span><span class="sxs-lookup"><span data-stu-id="44878-184">Note hello aliases such as Address.AddressType and Address.Location.StateProvinceName.</span></span> <span data-ttu-id="44878-185">Door op te geven van een geneste scheidingsteken van '.', Hallo import-hulpprogramma maakt adres en Address.Location subdocumenten tijdens Hallo importeren.</span><span class="sxs-lookup"><span data-stu-id="44878-185">By specifying a nesting separator of ‘.’, hello import tool creates Address and Address.Location subdocuments during hello import.</span></span> <span data-ttu-id="44878-186">Hier volgt een voorbeeld van een resulterende document in Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="44878-186">Here is an example of a resulting document in Azure Cosmos DB:</span></span>

<span data-ttu-id="44878-187">*{'id': '956', 'Name': 'Fijner verkoop en Service', 'Adres': {'Adrestype': 'Hoofdkantoor', 'AddressLine1': '#500 75 O'Connor straat', 'Locatie': {'Stad': 'Canada Ottawa', 'StateProvinceName': "Ontario"}, 'Postcode': 'K4B 1S2', 'CountryRegionName': ' Canada'}}*</span><span class="sxs-lookup"><span data-stu-id="44878-187">*{ "id": "956", "Name": "Finer Sales and Service", "Address": { "AddressType": "Main Office", "AddressLine1": "#500-75 O'Connor Street", "Location": { "City": "Ottawa", "StateProvinceName": "Ontario" }, "PostalCode": "K4B 1S2", "CountryRegionName": "Canada" } }*</span></span>

<span data-ttu-id="44878-188">Hier volgen enkele tooimport opdrachtregel voorbeelden van SQL Server:</span><span class="sxs-lookup"><span data-stu-id="44878-188">Here are some command line samples tooimport from SQL Server:</span></span>

    #Import records from SQL which match a query
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, * from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Stores /t.IdField:Id /t.CollectionThroughput:2500

    #Import records from sql which match a query and create hierarchical relationships
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /s.NestingSeparator:. /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:StoresSub /t.IdField:Id /t.CollectionThroughput:2500

## <span data-ttu-id="44878-189"><a id="CSV"></a>tooimport CSV-bestanden en converteren CSV tooJSON</span><span class="sxs-lookup"><span data-stu-id="44878-189"><a id="CSV"></a>tooimport CSV files and convert CSV tooJSON</span></span>
<span data-ttu-id="44878-190">Hallo CSV-bestand bron importfunctie optie kunt u tooimport een of meer CSV-bestanden.</span><span class="sxs-lookup"><span data-stu-id="44878-190">hello CSV file source importer option enables you tooimport one or more CSV files.</span></span> <span data-ttu-id="44878-191">Als u mappen met CSV-bestanden voor het importeren van toevoegt, hebt u de mogelijkheid Hallo van recursief zoeken naar bestanden in submappen.</span><span class="sxs-lookup"><span data-stu-id="44878-191">When adding folders that contain CSV files for import, you have hello option of recursively searching for files in subfolders.</span></span>

![Schermopname van CSV - opties voor CSV tooJSON](media/import-data/csvsource.png)

<span data-ttu-id="44878-193">SQL-bron vergelijkbare toohello, Hallo scheidingsteken eigenschap nesten mogelijk gebruikte toocreate hiërarchische relaties (onderliggende documenten) tijdens het importeren.</span><span class="sxs-lookup"><span data-stu-id="44878-193">Similar toohello SQL source, hello nesting separator property may be used toocreate hierarchical relationships (sub-documents) during import.</span></span> <span data-ttu-id="44878-194">Houd rekening met Hallo veldnamenrij CSV en gegevensrijen te volgen:</span><span class="sxs-lookup"><span data-stu-id="44878-194">Consider hello following CSV header row and data rows:</span></span>

![Schermopname van CSV-voorbeeld registreert - CSV tooJSON](./media/import-data/csvsample.png)

<span data-ttu-id="44878-196">Houd er rekening mee Hallo aliassen zoals DomainInfo.Domain_Name en RedirectInfo.Redirecting.</span><span class="sxs-lookup"><span data-stu-id="44878-196">Note hello aliases such as DomainInfo.Domain_Name and RedirectInfo.Redirecting.</span></span> <span data-ttu-id="44878-197">Door op te geven van een geneste scheidingsteken van '.', Hallo import-hulpprogramma DomainInfo maakt en RedirectInfo subdocumenten tijdens Hallo importeren.</span><span class="sxs-lookup"><span data-stu-id="44878-197">By specifying a nesting separator of ‘.’, hello import tool will create DomainInfo and RedirectInfo subdocuments during hello import.</span></span> <span data-ttu-id="44878-198">Hier volgt een voorbeeld van een resulterende document in Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="44878-198">Here is an example of a resulting document in Azure Cosmos DB:</span></span>

<span data-ttu-id="44878-199">*{{"DomainInfo": {'Domeinnaam': 'ACUS.GOV', 'Domain_Name_Address': 'http://www. ACUS.GOV"}, 'Federale instantie': 'Beheerdersrechten Conferentie van Hallo Verenigde Staten',"RedirectInfo": {'Omleiden': '0', 'Redirect_Destination': '"}, 'id': '9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d'}*</span><span class="sxs-lookup"><span data-stu-id="44878-199">*{ "DomainInfo": { "Domain_Name": "ACUS.GOV", "Domain_Name_Address": "http://www.ACUS.GOV" }, "Federal Agency": "Administrative Conference of hello United States", "RedirectInfo": { "Redirecting": "0", "Redirect_Destination": "" }, "id": "9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d" }*</span></span>

<span data-ttu-id="44878-200">hulpprogramma voor het importeren van Hallo probeert tooinfer type-informatie voor zonder aanhalingstekens waarden in CSV-bestanden (tussen aanhalingstekens waarden worden altijd behandeld als tekenreeksen).</span><span class="sxs-lookup"><span data-stu-id="44878-200">hello import tool will attempt tooinfer type information for unquoted values in CSV files (quoted values are always treated as strings).</span></span>  <span data-ttu-id="44878-201">Typen in Hallo volgorde worden aangeduid: getal, datum/tijd, Booleaanse waarde.</span><span class="sxs-lookup"><span data-stu-id="44878-201">Types are identified in hello following order: number, datetime, boolean.</span></span>  

<span data-ttu-id="44878-202">Er zijn twee andere dingen toonote over CSV-import:</span><span class="sxs-lookup"><span data-stu-id="44878-202">There are two other things toonote about CSV import:</span></span>

1. <span data-ttu-id="44878-203">Standaard zonder aanhalingstekens waarden zijn altijd bijgesneden voor tabs en spaties, terwijl tussen aanhalingstekens waarden behouden als blijven-is.</span><span class="sxs-lookup"><span data-stu-id="44878-203">By default, unquoted values are always trimmed for tabs and spaces, while quoted values are preserved as-is.</span></span> <span data-ttu-id="44878-204">Dit gedrag kan worden onderdrukt met Hallo die Trim aanhalingstekens waarden checkbox of Hallo /s.TrimQuoted opdrachtregeloptie.</span><span class="sxs-lookup"><span data-stu-id="44878-204">This behavior can be overridden with hello Trim quoted values checkbox or hello /s.TrimQuoted command line option.</span></span>
2. <span data-ttu-id="44878-205">Standaard wordt een zonder aanhalingstekens null worden beschouwd als een null-waarde.</span><span class="sxs-lookup"><span data-stu-id="44878-205">By default, an unquoted null is treated as a null value.</span></span> <span data-ttu-id="44878-206">Dit gedrag kan worden genegeerd (dat wil zeggen een zonder aanhalingstekens null behandelen als een tekenreeks 'null') Hello zonder aanhalingstekens NULL als tekenreeks checkbox of Hallo /s.NoUnquotedNulls opdrachtregeloptie behandelen.</span><span class="sxs-lookup"><span data-stu-id="44878-206">This behavior can be overridden (i.e. treat an unquoted null as a “null” string) with hello Treat unquoted NULL as string checkbox or hello /s.NoUnquotedNulls command line option.</span></span>

<span data-ttu-id="44878-207">Hier volgt een voorbeeld van de opdrachtregel voor CSV-import:</span><span class="sxs-lookup"><span data-stu-id="44878-207">Here is a command line sample for CSV import:</span></span>

    dt.exe /s:CsvFile /s.Files:.\Employees.csv /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Employees /t.IdField:EntityID /t.CollectionThroughput:2500

## <span data-ttu-id="44878-208"><a id="AzureTableSource"></a>tooimport uit Azure Table storage</span><span class="sxs-lookup"><span data-stu-id="44878-208"><a id="AzureTableSource"></a>tooimport from Azure Table storage</span></span>
<span data-ttu-id="44878-209">Hallo bron Azure Table-importprogramma opslagoptie kunt u tooimport uit een afzonderlijke tabel voor Azure Table storage en filter optioneel Hallo tabel entiteiten toobe geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="44878-209">hello Azure Table storage source importer option allows you tooimport from an individual Azure Table storage table and optionally filter hello table entities toobe imported.</span></span> <span data-ttu-id="44878-210">Houd er rekening mee dat u Hallo gegevensmigratie hulpprogramma tooimport Azure Table storage-gegevens naar Azure Cosmos DB kan niet voor gebruik met Hallo tabel-API gebruiken.</span><span class="sxs-lookup"><span data-stu-id="44878-210">Note that you cannot use hello Data Migration tool tooimport Azure Table storage data into Azure Cosmos DB for use with hello Table API.</span></span> <span data-ttu-id="44878-211">Alleen importeren tooAzure Cosmos DB voor gebruik met DocumentDB API hello wordt ondersteund op dit moment.</span><span class="sxs-lookup"><span data-stu-id="44878-211">Only importing tooAzure Cosmos DB for use with hello DocumentDB API is supported at this time.</span></span>

![Schermopname van Azure Table storage bronopties](./media/import-data/azuretablesource.png)

<span data-ttu-id="44878-213">Hallo-indeling van Hallo verbindingsreeks voor Azure Table-opslag is:</span><span class="sxs-lookup"><span data-stu-id="44878-213">hello format of hello Azure Table storage connection string is:</span></span>

    DefaultEndpointsProtocol=<protocol>;AccountName=<Account Name>;AccountKey=<Account Key>;

> [!NOTE]
> <span data-ttu-id="44878-214">Gebruik Hallo controleren opdracht tooensure die hello Azure Table storage-exemplaar is opgegeven in tekenreeksveld Hallo-verbinding kan worden benaderd.</span><span class="sxs-lookup"><span data-stu-id="44878-214">Use hello Verify command tooensure that hello Azure Table storage instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="44878-215">Voer de naam Hallo van hello Azure tabel waaruit gegevens worden geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="44878-215">Enter hello name of hello Azure table from which data will be imported.</span></span> <span data-ttu-id="44878-216">U kunt eventueel opgeven een [filter](https://msdn.microsoft.com/library/azure/ff683669.aspx).</span><span class="sxs-lookup"><span data-stu-id="44878-216">You may optionally specify a [filter](https://msdn.microsoft.com/library/azure/ff683669.aspx).</span></span>

<span data-ttu-id="44878-217">Hello Azure Table storage bronoptie importfunctie heeft Hallo extra opties te volgen:</span><span class="sxs-lookup"><span data-stu-id="44878-217">hello Azure Table storage source importer option has hello following additional options:</span></span>

1. <span data-ttu-id="44878-218">Interne velden bevatten</span><span class="sxs-lookup"><span data-stu-id="44878-218">Include Internal Fields</span></span>
   1. <span data-ttu-id="44878-219">All - omvatten alle interne velden (PartitionKey, RowKey en tijdstempel)</span><span class="sxs-lookup"><span data-stu-id="44878-219">All - Include all internal fields (PartitionKey, RowKey, and Timestamp)</span></span>
   2. <span data-ttu-id="44878-220">Geen - uitsluiten alle interne velden</span><span class="sxs-lookup"><span data-stu-id="44878-220">None - Exclude all internal fields</span></span>
   3. <span data-ttu-id="44878-221">RowKey - Hallo RowKey veld alleen opnemen</span><span class="sxs-lookup"><span data-stu-id="44878-221">RowKey - Only include hello RowKey field</span></span>
2. <span data-ttu-id="44878-222">Kolommen selecteren</span><span class="sxs-lookup"><span data-stu-id="44878-222">Select Columns</span></span>
   1. <span data-ttu-id="44878-223">Azure Table storage filters bieden geen ondersteuning voor projecties.</span><span class="sxs-lookup"><span data-stu-id="44878-223">Azure Table storage filters do not support projections.</span></span> <span data-ttu-id="44878-224">Als u tooonly importeren specifieke Azure Table-entiteitseigenschappen wilt, ze toohello kolommen selecteren lijst toevoegen.</span><span class="sxs-lookup"><span data-stu-id="44878-224">If you want tooonly import specific Azure Table entity properties, add them toohello Select Columns list.</span></span> <span data-ttu-id="44878-225">Alle andere entiteitseigenschappen wordt genegeerd.</span><span class="sxs-lookup"><span data-stu-id="44878-225">All other entity properties will be ignored.</span></span>

<span data-ttu-id="44878-226">Hier volgt een opdrachtregel voorbeeld tooimport uit Azure Table storage:</span><span class="sxs-lookup"><span data-stu-id="44878-226">Here is a command line sample tooimport from Azure Table storage:</span></span>

    dt.exe /s:AzureTable /s.ConnectionString:"DefaultEndpointsProtocol=https;AccountName=<Account Name>;AccountKey=<Account Key>" /s.Table:metrics /s.InternalFields:All /s.Filter:"PartitionKey eq 'Partition1' and RowKey gt '00001'" /s.Projection:ObjectCount;ObjectSize  /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:metrics /t.CollectionThroughput:2500

## <span data-ttu-id="44878-227"><a id="DynamoDBSource"></a>tooimport van Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="44878-227"><a id="DynamoDBSource"></a>tooimport from Amazon DynamoDB</span></span>
<span data-ttu-id="44878-228">Hallo Amazon DynamoDB bron importfunctie optie kunt u tooimport uit de tabel van een afzonderlijke Amazon DynamoDB en filter optioneel Hallo entiteiten toobe geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="44878-228">hello Amazon DynamoDB source importer option allows you tooimport from an individual Amazon DynamoDB table and optionally filter hello entities toobe imported.</span></span> <span data-ttu-id="44878-229">Verschillende sjablonen zijn bedoeld om het instellen van een import zo eenvoudig mogelijk is.</span><span class="sxs-lookup"><span data-stu-id="44878-229">Several templates are provided so that setting up an import is as easy as possible.</span></span>

![Schermopname van Amazon DynamoDB bronopties - hulpprogramma's voor migratie](./media/import-data/dynamodbsource1.png)

![Schermopname van Amazon DynamoDB bronopties - hulpprogramma's voor migratie](./media/import-data/dynamodbsource2.png)

<span data-ttu-id="44878-232">Hallo-indeling van Hallo Amazon DynamoDB verbindingsreeks is:</span><span class="sxs-lookup"><span data-stu-id="44878-232">hello format of hello Amazon DynamoDB connection string is:</span></span>

    ServiceURL=<Service Address>;AccessKey=<Access Key>;SecretKey=<Secret Key>;

> [!NOTE]
> <span data-ttu-id="44878-233">Gebruik Hallo controleren opdracht tooensure die Hallo DynamoDB Amazon-exemplaar is opgegeven in tekenreeksveld Hallo-verbinding kan worden benaderd.</span><span class="sxs-lookup"><span data-stu-id="44878-233">Use hello Verify command tooensure that hello Amazon DynamoDB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="44878-234">Hier volgt een opdrachtregel voorbeeld tooimport van Amazon DynamoDB:</span><span class="sxs-lookup"><span data-stu-id="44878-234">Here is a command line sample tooimport from Amazon DynamoDB:</span></span>

    dt.exe /s:DynamoDB /s.ConnectionString:ServiceURL=https://dynamodb.us-east-1.amazonaws.com;AccessKey=<accessKey>;SecretKey=<secretKey> /s.Request:"{   """TableName""": """ProductCatalog""" }" /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<Azure Cosmos DB Endpoint>;AccountKey=<Azure Cosmos DB Key>;Database=<Azure Cosmos DB Database>;" /t.Collection:catalogCollection /t.CollectionThroughput:2500

## <span data-ttu-id="44878-235"><a id="BlobImport"></a>tooimport bestanden uit Azure Blob-opslag</span><span class="sxs-lookup"><span data-stu-id="44878-235"><a id="BlobImport"></a>tooimport files from Azure Blob storage</span></span>
<span data-ttu-id="44878-236">Hallo JSON-bestand, MongoDB-exportbestand en CSV-bestand bron importfunctie opties kunnen u tooimport een of meer bestanden uit Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="44878-236">hello JSON file, MongoDB export file, and CSV file source importer options allow you tooimport one or more files from Azure Blob storage.</span></span> <span data-ttu-id="44878-237">Nadat u een URL van de Blob-container en de Accountsleutel, moet u gewoon een reguliere expressie tooselect Hallo bestand(en) tooimport bieden.</span><span class="sxs-lookup"><span data-stu-id="44878-237">After specifying a Blob container URL and Account Key, simply provide a regular expression tooselect hello file(s) tooimport.</span></span>

![Schermopname van Blob-bestand bronopties](./media/import-data/blobsource.png)

<span data-ttu-id="44878-239">Ga als volgt vanaf de opdrachtregel tooimport JSON voorbeeldbestanden uit Azure Blob-opslag:</span><span class="sxs-lookup"><span data-stu-id="44878-239">Here is command line sample tooimport JSON files from Azure Blob storage:</span></span>

    dt.exe /s:JsonFile /s.Files:"blobs://<account key>@account.blob.core.windows.net:443/importcontainer/.*" /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:doctest

## <span data-ttu-id="44878-240"><a id="DocumentDBSource"></a>tooimport uit een verzameling Azure Cosmos DB DocumentDB-API</span><span class="sxs-lookup"><span data-stu-id="44878-240"><a id="DocumentDBSource"></a>tooimport from an Azure Cosmos DB DocumentDB API collection</span></span>
<span data-ttu-id="44878-241">Hello Azure Cosmos DB bron importfunctie optie kunt u tooimport gegevens uit een of meer Azure Cosmos DB verzamelingen en filter optioneel documenten met behulp van een query.</span><span class="sxs-lookup"><span data-stu-id="44878-241">hello Azure Cosmos DB source importer option allows you tooimport data from one or more Azure Cosmos DB collections and optionally filter documents using a query.</span></span>  

![Opties voor schermopname van Azure Cosmos DB-gegevensbron](./media/import-data/documentdbsource.png)

<span data-ttu-id="44878-243">Hallo-indeling van hello Azure Cosmos DB-verbindingsreeks is:</span><span class="sxs-lookup"><span data-stu-id="44878-243">hello format of hello Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="44878-244">Hallo verbindingsreeks voor Azure DB die Cosmos-account kan worden opgehaald uit de blade van de sleutels Hallo van hello Azure-portal, zoals beschreven in [hoe toomanage een account voor Azure Cosmos DB](manage-account.md), maar de naam van de Hallo van Hallo-database toohello toobe toegevoegd moet de verbindingsreeks in Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="44878-244">hello Azure Cosmos DB account connection string can be retrieved from hello Keys blade of hello Azure portal, as described in [How toomanage an Azure Cosmos DB account](manage-account.md), however hello name of hello database needs toobe appended toohello connection string in hello following format:</span></span>

    Database=<CosmosDB Database>;

> [!NOTE]
> <span data-ttu-id="44878-245">Gebruik Hallo controleren opdracht tooensure die hello Azure DB die Cosmos-exemplaar is opgegeven in tekenreeksveld Hallo-verbinding kan worden benaderd.</span><span class="sxs-lookup"><span data-stu-id="44878-245">Use hello Verify command tooensure that hello Azure Cosmos DB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="44878-246">tooimport van één Azure Cosmos DB verzameling Hallo naam invoeren van Hallo-verzameling van waaruit de gegevens worden geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="44878-246">tooimport from a single Azure Cosmos DB collection, enter hello name of hello collection from which data will be imported.</span></span> <span data-ttu-id="44878-247">tooimport van meerdere Azure Cosmos DB verzamelingen bieden een reguliere expressie toomatch een of meer verzamelingsnamen (bijvoorbeeld collection01 | collection02 | collection03).</span><span class="sxs-lookup"><span data-stu-id="44878-247">tooimport from multiple Azure Cosmos DB collections, provide a regular expression toomatch one or more collection names (e.g. collection01 | collection02 | collection03).</span></span> <span data-ttu-id="44878-248">U kan eventueel opgeeft, of een bestand voor een query tooboth filter opgeven en vorm Hallo gegevens toobe geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="44878-248">You may optionally specify, or provide a file for, a query tooboth filter and shape hello data toobe imported.</span></span>

> [!NOTE]
> <span data-ttu-id="44878-249">Aangezien Hallo verzameling veld reguliere expressies, accepteert als u wilt importeren uit één verzameling waarvan de naam tekens van de reguliere expressie bevat, moeten vervolgens die tekens worden voorafgegaan dienovereenkomstig.</span><span class="sxs-lookup"><span data-stu-id="44878-249">Since hello collection field accepts regular expressions, if you are importing from a single collection whose name contains regular expression characters, then those characters must be escaped accordingly.</span></span>
> 
> 

<span data-ttu-id="44878-250">Hello Azure Cosmos DB importfunctie bronoptie heeft Hallo volgende geavanceerde opties:</span><span class="sxs-lookup"><span data-stu-id="44878-250">hello Azure Cosmos DB source importer option has hello following advanced options:</span></span>

1. <span data-ttu-id="44878-251">Interne velden bevatten: Geeft aan of tooinclude Azure Cosmos DB document Systeemeigenschappen in Hallo exporteren (bijvoorbeeld _rid, _ts).</span><span class="sxs-lookup"><span data-stu-id="44878-251">Include Internal Fields: Specifies whether or not tooinclude Azure Cosmos DB document system properties in hello export (e.g. _rid, _ts).</span></span>
2. <span data-ttu-id="44878-252">Aantal nieuwe pogingen bij fouten: Hiermee geeft u het aantal keren tooretry verbinding tooAzure Cosmos DB in geval van een tijdelijke fouten (bijvoorbeeld connectiviteit onderbreking op het netwerk) Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="44878-252">Number of Retries on Failure: Specifies hello number of times tooretry hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
3. <span data-ttu-id="44878-253">Interval voor opnieuw proberen: Geeft aan hoe lang toowait tussen opnieuw uit te voeren Hallo verbinding tooAzure Cosmos DB in geval van een tijdelijke fouten (bijvoorbeeld connectiviteit onderbreking op het netwerk).</span><span class="sxs-lookup"><span data-stu-id="44878-253">Retry Interval: Specifies how long toowait between retrying hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
4. <span data-ttu-id="44878-254">Verbindingsmodus: Hiermee geeft u Hallo verbinding modus toouse met Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="44878-254">Connection Mode: Specifies hello connection mode toouse with Azure Cosmos DB.</span></span> <span data-ttu-id="44878-255">Hallo beschikbare opties zijn DirectTcp, DirectHttps en Gateway.</span><span class="sxs-lookup"><span data-stu-id="44878-255">hello available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="44878-256">Hallo rechtstreekse verbinding modi zijn sneller, terwijl Hallo gateway modus meer firewall beschrijvende aangezien hierbij alleen poort 443.</span><span class="sxs-lookup"><span data-stu-id="44878-256">hello direct connection modes are faster, while hello gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Schermopname van Azure Cosmos DB bron geavanceerde opties](./media/import-data/documentdbsourceoptions.png)

> [!TIP]
> <span data-ttu-id="44878-258">Hallo hulpprogramma standaardwaarden tooconnection modus DirectTcp voor importeren.</span><span class="sxs-lookup"><span data-stu-id="44878-258">hello import tool defaults tooconnection mode DirectTcp.</span></span> <span data-ttu-id="44878-259">Als u de firewall-problemen ondervindt, overschakelen tooconnection modus Gateway, omdat hiervoor alleen poort 443.</span><span class="sxs-lookup"><span data-stu-id="44878-259">If you experience firewall issues, switch tooconnection mode Gateway, as it only requires port 443.</span></span>
> 
> 

<span data-ttu-id="44878-260">Hier volgen enkele tooimport opdrachtregel voorbeelden van Azure DB die Cosmos:</span><span class="sxs-lookup"><span data-stu-id="44878-260">Here are some command line samples tooimport from Azure Cosmos DB:</span></span>

    #Migrate data from one Azure Cosmos DB collection tooanother Azure Cosmos DB collections
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:TEColl /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:TESessions /t.CollectionThroughput:2500

    #Migrate data from multiple Azure Cosmos DB collections tooa single Azure Cosmos DB collection
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:comp1|comp2|comp3|comp4 /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:singleCollection /t.CollectionThroughput:2500

    #Export an Azure Cosmos DB collection tooa JSON file
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:StoresSub /t:JsonFile /t.File:StoresExport.json /t.Overwrite /t.CollectionThroughput:2500

> [!TIP]
> <span data-ttu-id="44878-261">Hello Azure Cosmos DB Data Import-hulpprogramma ondersteunt ook het importeren van gegevens van Hallo [Azure Cosmos DB Emulator](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="44878-261">hello Azure Cosmos DB Data Import Tool also supports import of data from hello [Azure Cosmos DB Emulator](local-emulator.md).</span></span> <span data-ttu-id="44878-262">Bij het importeren van een lokale emulator, Hallo eindpunt instellen te`https://localhost:<port>`.</span><span class="sxs-lookup"><span data-stu-id="44878-262">When importing data from a local emulator, set hello endpoint too`https://localhost:<port>`.</span></span> 
> 
> 

## <span data-ttu-id="44878-263"><a id="HBaseSource"></a>tooimport van HBase</span><span class="sxs-lookup"><span data-stu-id="44878-263"><a id="HBaseSource"></a>tooimport from HBase</span></span>
<span data-ttu-id="44878-264">Hallo HBase bron importfunctie optie kunt u tooimport gegevens uit een HBase-tabel en eventueel Hallo gegevens te filteren.</span><span class="sxs-lookup"><span data-stu-id="44878-264">hello HBase source importer option allows you tooimport data from an HBase table and optionally filter hello data.</span></span> <span data-ttu-id="44878-265">Verschillende sjablonen zijn bedoeld om het instellen van een import zo eenvoudig mogelijk is.</span><span class="sxs-lookup"><span data-stu-id="44878-265">Several templates are provided so that setting up an import is as easy as possible.</span></span>

![Schermopname van HBase-opties voor gegevensbron](./media/import-data/hbasesource1.png)

![Schermopname van HBase-opties voor gegevensbron](./media/import-data/hbasesource2.png)

<span data-ttu-id="44878-268">Hallo-indeling van Hallo HBase Stargate verbindingsreeks is:</span><span class="sxs-lookup"><span data-stu-id="44878-268">hello format of hello HBase Stargate connection string is:</span></span>

    ServiceURL=<server-address>;Username=<username>;Password=<password>

> [!NOTE]
> <span data-ttu-id="44878-269">Gebruik Hallo controleren opdracht tooensure die Hallo HBase-exemplaar is opgegeven in tekenreeksveld Hallo-verbinding kan worden benaderd.</span><span class="sxs-lookup"><span data-stu-id="44878-269">Use hello Verify command tooensure that hello HBase instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="44878-270">Hier volgt een opdrachtregel voorbeeld tooimport van HBase:</span><span class="sxs-lookup"><span data-stu-id="44878-270">Here is a command line sample tooimport from HBase:</span></span>

    dt.exe /s:HBase /s.ConnectionString:ServiceURL=<server-address>;Username=<username>;Password=<password> /s.Table:Contacts /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:hbaseimport

## <span data-ttu-id="44878-271"><a id="DocumentDBBulkTarget"></a>tooimport toohello DocumentDB-API (bulkimport)</span><span class="sxs-lookup"><span data-stu-id="44878-271"><a id="DocumentDBBulkTarget"></a>tooimport toohello DocumentDB API (Bulk Import)</span></span>
<span data-ttu-id="44878-272">Importfunctie van Hello Azure Cosmos DB bulksgewijs kunt u tooimport vanaf elke Hallo beschikbare opties voor gegevensbron met behulp van een Azure Cosmos DB opgeslagen procedure voor efficiëntie.</span><span class="sxs-lookup"><span data-stu-id="44878-272">hello Azure Cosmos DB Bulk importer allows you tooimport from any of hello available source options, using an Azure Cosmos DB stored procedure for efficiency.</span></span> <span data-ttu-id="44878-273">Hallo-hulpprogramma ondersteunt één gepartitioneerd Azure Cosmos DB verzameling tooone importeren, evenals shard importeren, waarbij de gegevens in meerdere één gepartitioneerd Azure Cosmos DB verzamelingen zijn gepartitioneerd.</span><span class="sxs-lookup"><span data-stu-id="44878-273">hello tool supports import tooone single-partitioned Azure Cosmos DB collection, as well as sharded import whereby data is partitioned across multiple single-partitioned Azure Cosmos DB collections.</span></span> <span data-ttu-id="44878-274">Zie voor meer informatie over het partitioneren van gegevens, [partitionering en schalen in Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="44878-274">For more information about partitioning data, see [Partitioning and scaling in Azure Cosmos DB](partition-data.md).</span></span> <span data-ttu-id="44878-275">Hallo-hulpprogramma wordt maken, uitvoeren en vervolgens Hallo opgeslagen procedure verwijderen uit de verzameling(en) van Hallo doel.</span><span class="sxs-lookup"><span data-stu-id="44878-275">hello tool will create, execute, and then delete hello stored procedure from hello target collection(s).</span></span>  

![Schermopname van Azure Cosmos DB bulksgewijs opties](./media/import-data/documentdbbulk.png)

<span data-ttu-id="44878-277">Hallo-indeling van hello Azure Cosmos DB-verbindingsreeks is:</span><span class="sxs-lookup"><span data-stu-id="44878-277">hello format of hello Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="44878-278">Hallo verbindingsreeks voor Azure DB die Cosmos-account kan worden opgehaald uit de blade van de sleutels Hallo van hello Azure-portal, zoals beschreven in [hoe toomanage een account voor Azure Cosmos DB](manage-account.md), maar de naam van de Hallo van Hallo-database toohello toobe toegevoegd moet de verbindingsreeks in Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="44878-278">hello Azure Cosmos DB account connection string can be retrieved from hello Keys blade of hello Azure portal, as described in [How toomanage an Azure Cosmos DB account](manage-account.md), however hello name of hello database needs toobe appended toohello connection string in hello following format:</span></span>

    Database=<CosmosDB Database>;

> [!NOTE]
> <span data-ttu-id="44878-279">Gebruik Hallo controleren opdracht tooensure die hello Azure DB die Cosmos-exemplaar is opgegeven in tekenreeksveld Hallo-verbinding kan worden benaderd.</span><span class="sxs-lookup"><span data-stu-id="44878-279">Use hello Verify command tooensure that hello Azure Cosmos DB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="44878-280">tooimport tooa één verzameling, Voer Hallo-naam van Hallo verzameling toowhich gegevens worden geïmporteerd en klik op de knop toevoegen Hallo.</span><span class="sxs-lookup"><span data-stu-id="44878-280">tooimport tooa single collection, enter hello name of hello collection toowhich data will be imported and click hello Add button.</span></span> <span data-ttu-id="44878-281">tooimport toomultiple verzamelingen, de verzamelingsnaam van elke afzonderlijk Voer of gebruik Hallo syntaxis toospecify na meerdere verzamelingen: *collection_prefix*[begin index - end-index].</span><span class="sxs-lookup"><span data-stu-id="44878-281">tooimport toomultiple collections, either enter each collection name individually or use hello following syntax toospecify multiple collections: *collection_prefix*[start index - end index].</span></span> <span data-ttu-id="44878-282">Houd rekening met Hallo volgende bij het opgeven van meerdere verzamelingen via de hiervoor genoemde Hallo-syntaxis:</span><span class="sxs-lookup"><span data-stu-id="44878-282">When specifying multiple collections via hello aforementioned syntax, keep hello following in mind:</span></span>

1. <span data-ttu-id="44878-283">Alleen geheel getal bereik bestandsnaampatronen worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="44878-283">Only integer range name patterns are supported.</span></span> <span data-ttu-id="44878-284">Bijvoorbeeld, geven verzameling [0-3] produceert Hallo verzamelingen te volgen: collection0, collection1, collection2, collection3.</span><span class="sxs-lookup"><span data-stu-id="44878-284">For example, specifying collection[0-3] will produce hello following collections: collection0, collection1, collection2, collection3.</span></span>
2. <span data-ttu-id="44878-285">U kunt een verkorte syntaxis gebruiken: verzameling [3] wordt vermeld in stap 1 verzamelingen dezelfde set verzenden.</span><span class="sxs-lookup"><span data-stu-id="44878-285">You can use an abbreviated syntax: collection[3] will emit same set of collections mentioned in step 1.</span></span>
3. <span data-ttu-id="44878-286">Meer dan een vervanging kan worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="44878-286">More than one substitution can be provided.</span></span> <span data-ttu-id="44878-287">Bijvoorbeeld, verzameling [0-1] [0-9] genereert 20 verzamelingsnamen met toonaangevende nullen (collection01,... 02... 03).</span><span class="sxs-lookup"><span data-stu-id="44878-287">For example, collection[0-1] [0-9] will generate 20 collection names with leading zeros (collection01, ..02, ..03).</span></span>

<span data-ttu-id="44878-288">Eenmaal hello verzameling namen zijn opgegeven, kiest u de gewenste doorvoer Hallo van Hallo verzameling(en) (400 RUs too10, 000 RUs).</span><span class="sxs-lookup"><span data-stu-id="44878-288">Once hello collection name(s) have been specified, choose hello desired throughput of hello collection(s) (400 RUs too10,000 RUs).</span></span> <span data-ttu-id="44878-289">Kies een hogere doorvoer voor de beste prestaties importeren.</span><span class="sxs-lookup"><span data-stu-id="44878-289">For best import performance, choose a higher throughput.</span></span> <span data-ttu-id="44878-290">Zie voor meer informatie over prestatieniveaus [prestatieniveaus in Azure Cosmos DB](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="44878-290">For more information about performance levels, see [Performance levels in Azure Cosmos DB](performance-levels.md).</span></span>

> [!NOTE]
> <span data-ttu-id="44878-291">Hallo prestatie doorvoer-instelling is alleen van toepassing toocollection maken.</span><span class="sxs-lookup"><span data-stu-id="44878-291">hello performance throughput setting only applies toocollection creation.</span></span> <span data-ttu-id="44878-292">Als Hallo collectie al bestaat opgegeven, wordt de doorvoer niet gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="44878-292">If hello specified collection already exists, its throughput will not be modified.</span></span>
> 
> 

<span data-ttu-id="44878-293">Bij het importeren van verzamelingen toomultiple ondersteunt Hallo import-hulpprogramma hash op basis van sharding.</span><span class="sxs-lookup"><span data-stu-id="44878-293">When importing toomultiple collections, hello import tool supports hash based sharding.</span></span> <span data-ttu-id="44878-294">Geef in dit scenario Hallo documenteigenschap gewenst toouse als partitiesleutel Hallo (als partitiesleutel leeg is, documenten zijn shard willekeurig in Hallo doel verzamelingen).</span><span class="sxs-lookup"><span data-stu-id="44878-294">In this scenario, specify hello document property you wish toouse as hello Partition Key (if Partition Key is left blank, documents will be sharded randomly across hello target collections).</span></span>

<span data-ttu-id="44878-295">U kunt eventueel opgeven welk veld in de bron voor het importeren van Hallo als hello Azure Cosmos DB document-id-eigenschap moet worden gebruikt tijdens het importeren van hello (Let erop dat als documenten geen deze eigenschap bevatten, klikt u vervolgens Hallo import-hulpprogramma een GUID als de waarde van de eigenschap id Hallo genereert).</span><span class="sxs-lookup"><span data-stu-id="44878-295">You may optionally specify which field in hello import source should be used as hello Azure Cosmos DB document id property during hello import (note that if documents do not contain this property, then hello import tool will generate a GUID as hello id property value).</span></span>

<span data-ttu-id="44878-296">Er zijn tijdens het importeren van een aantal geavanceerde opties beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="44878-296">There are a number of advanced options available during import.</span></span> <span data-ttu-id="44878-297">Tijdens het Hallo-hulpprogramma omvat eerst een standaard bulkimport opgeslagen procedure (BulkInsert.js), kunt u eventueel toospecify uw eigen importprocedure opgeslagen:</span><span class="sxs-lookup"><span data-stu-id="44878-297">First, while hello tool includes a default bulk import stored procedure (BulkInsert.js), you may choose toospecify your own import stored procedure:</span></span>

 ![Schermopname van Azure Cosmos DB bulksgewijs invoegen sproc optie](./media/import-data/bulkinsertsp.png)

<span data-ttu-id="44878-299">Bij het importeren van datum-typen (bijvoorbeeld van SQL Server of MongoDB), kunt u kunt daarnaast voor kiezen tussen de drie opties voor importeren:</span><span class="sxs-lookup"><span data-stu-id="44878-299">Additionally, when importing date types (e.g. from SQL Server or MongoDB), you can choose between three import options:</span></span>

 ![Schermopname van Azure Cosmos DB datum tijdopties importeren](./media/import-data/datetimeoptions.png)

* <span data-ttu-id="44878-301">Tekenreeks: Behouden als een string-waarde</span><span class="sxs-lookup"><span data-stu-id="44878-301">String: Persist as a string value</span></span>
* <span data-ttu-id="44878-302">Epoche: Behouden als een getalwaarde epoche</span><span class="sxs-lookup"><span data-stu-id="44878-302">Epoch: Persist as an Epoch number value</span></span>
* <span data-ttu-id="44878-303">Beide: Zowel tekenreeks als numerieke waarden epoche bewaard.</span><span class="sxs-lookup"><span data-stu-id="44878-303">Both: Persist both string and Epoch number values.</span></span> <span data-ttu-id="44878-304">Deze optie maakt u een subdocument, bijvoorbeeld: "date_joined": {'' waarde '': ' 2013-10-21T21:17:25.2410000Z ', ' epoche ': 1382390245}</span><span class="sxs-lookup"><span data-stu-id="44878-304">This option will create a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span></span>

<span data-ttu-id="44878-305">Hello Azure Cosmos DB bulksgewijs importfunctie heeft Hallo volgende als u meer geavanceerde opties:</span><span class="sxs-lookup"><span data-stu-id="44878-305">hello Azure Cosmos DB Bulk importer has hello following additional advanced options:</span></span>

1. <span data-ttu-id="44878-306">Batchgrootte: Hallo hulpprogramma standaardwaarden tooa batchgrootte van 50.</span><span class="sxs-lookup"><span data-stu-id="44878-306">Batch Size: hello tool defaults tooa batch size of 50.</span></span>  <span data-ttu-id="44878-307">Als Hallo documenten toobe geïmporteerd groot zijn, kunt u overwegen Hallo batchgrootte te verlagen.</span><span class="sxs-lookup"><span data-stu-id="44878-307">If hello documents toobe imported are large, consider lowering hello batch size.</span></span> <span data-ttu-id="44878-308">Als u daarentegen als Hallo documenten toobe geïmporteerd klein zijn, kunt u Hallo batchgrootte verhogen.</span><span class="sxs-lookup"><span data-stu-id="44878-308">Conversely, if hello documents toobe imported are small, consider raising hello batch size.</span></span>
2. <span data-ttu-id="44878-309">Maximum aantal Script-grootte (bytes): Hallo hulpprogramma standaardinstellingen tooa script maximale grootte van 512KB</span><span class="sxs-lookup"><span data-stu-id="44878-309">Max Script Size (bytes): hello tool defaults tooa max script size of 512KB</span></span>
3. <span data-ttu-id="44878-310">Schakel automatische van generatie-Id: Als elke document toobe geïmporteerd een id-veld bevat, deze optie kunt betere prestaties.</span><span class="sxs-lookup"><span data-stu-id="44878-310">Disable Automatic Id Generation: If every document toobe imported contains an id field, then selecting this option can increase performance.</span></span> <span data-ttu-id="44878-311">Een unieke id-veld ontbreekt documenten worden niet geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="44878-311">Documents missing a unique id field will not be imported.</span></span>
4. <span data-ttu-id="44878-312">Update bestaande documenten: Hallo hulpprogramma standaardwaarden toonot bestaande documenten vervangen door een ID-conflicten.</span><span class="sxs-lookup"><span data-stu-id="44878-312">Update Existing Documents: hello tool defaults toonot replacing existing documents with id conflicts.</span></span> <span data-ttu-id="44878-313">Deze optie kunt bestaande documenten met overeenkomende id overschrijven.</span><span class="sxs-lookup"><span data-stu-id="44878-313">Selecting this option will allow overwriting existing documents with matching ids.</span></span> <span data-ttu-id="44878-314">Deze functie is handig voor geplande gegevens migraties die bijwerken van bestaande documenten.</span><span class="sxs-lookup"><span data-stu-id="44878-314">This feature is useful for scheduled data migrations that update existing documents.</span></span>
5. <span data-ttu-id="44878-315">Aantal nieuwe pogingen bij fouten: Hiermee geeft u het aantal keren tooretry verbinding tooAzure Cosmos DB in geval van een tijdelijke fouten (bijvoorbeeld connectiviteit onderbreking op het netwerk) Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="44878-315">Number of Retries on Failure: Specifies hello number of times tooretry hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
6. <span data-ttu-id="44878-316">Interval voor opnieuw proberen: Geeft aan hoe lang toowait tussen opnieuw uit te voeren Hallo verbinding tooAzure Cosmos DB in geval van een tijdelijke fouten (bijvoorbeeld connectiviteit onderbreking op het netwerk).</span><span class="sxs-lookup"><span data-stu-id="44878-316">Retry Interval: Specifies how long toowait between retrying hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
7. <span data-ttu-id="44878-317">Verbindingsmodus: Hiermee geeft u Hallo verbinding modus toouse met Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="44878-317">Connection Mode: Specifies hello connection mode toouse with Azure Cosmos DB.</span></span> <span data-ttu-id="44878-318">Hallo beschikbare opties zijn DirectTcp, DirectHttps en Gateway.</span><span class="sxs-lookup"><span data-stu-id="44878-318">hello available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="44878-319">Hallo rechtstreekse verbinding modi zijn sneller, terwijl Hallo gateway modus meer firewall beschrijvende aangezien hierbij alleen poort 443.</span><span class="sxs-lookup"><span data-stu-id="44878-319">hello direct connection modes are faster, while hello gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Schermopname van Azure Cosmos DB bulkimport geavanceerde opties](./media/import-data/docdbbulkoptions.png)

> [!TIP]
> <span data-ttu-id="44878-321">Hallo hulpprogramma standaardwaarden tooconnection modus DirectTcp voor importeren.</span><span class="sxs-lookup"><span data-stu-id="44878-321">hello import tool defaults tooconnection mode DirectTcp.</span></span> <span data-ttu-id="44878-322">Als u de firewall-problemen ondervindt, overschakelen tooconnection modus Gateway, omdat hiervoor alleen poort 443.</span><span class="sxs-lookup"><span data-stu-id="44878-322">If you experience firewall issues, switch tooconnection mode Gateway, as it only requires port 443.</span></span>
> 
> 

## <span data-ttu-id="44878-323"><a id="DocumentDBSeqTarget"></a>tooimport toohello DocumentDB-API (sequentiële Record importeren)</span><span class="sxs-lookup"><span data-stu-id="44878-323"><a id="DocumentDBSeqTarget"></a>tooimport toohello DocumentDB API (Sequential Record Import)</span></span>
<span data-ttu-id="44878-324">Importfunctie van Hello Azure Cosmos DB sequentiële record kunt u tooimport van Hallo beschikbare bron opties op basis van door een andere record.</span><span class="sxs-lookup"><span data-stu-id="44878-324">hello Azure Cosmos DB sequential record importer allows you tooimport from any of hello available source options on a record by record basis.</span></span> <span data-ttu-id="44878-325">U kunt deze optie selecteren als u de bestaande verzameling tooan heeft het quotum van opgeslagen procedures bereikt importeert.</span><span class="sxs-lookup"><span data-stu-id="44878-325">You might choose this option if you’re importing tooan existing collection that has reached its quota of stored procedures.</span></span> <span data-ttu-id="44878-326">Hallo hulpprogramma ondersteunt importeren tooa enkel Azure DB die Cosmos-verzameling (één partitie en meerdere partitie), evenals shard importeren, waarbij de gegevens in Azure Cosmos DB meerdere verzamelingen voor één partitie en/of meerdere partitie zijn gepartitioneerd.</span><span class="sxs-lookup"><span data-stu-id="44878-326">hello tool supports import tooa single (both single-partition and multi-partition) Azure Cosmos DB collection, as well as sharded import whereby data is partitioned across multiple single-partition and/or multi-partition Azure Cosmos DB collections.</span></span> <span data-ttu-id="44878-327">Zie voor meer informatie over het partitioneren van gegevens, [partitionering en schalen in Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="44878-327">For more information about partitioning data, see [Partitioning and scaling in Azure Cosmos DB](partition-data.md).</span></span>

![Schermopname van Azure Cosmos DB-opties voor opeenvolgende record importeren](./media/import-data/documentdbsequential.png)

<span data-ttu-id="44878-329">Hallo-indeling van hello Azure Cosmos DB-verbindingsreeks is:</span><span class="sxs-lookup"><span data-stu-id="44878-329">hello format of hello Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="44878-330">Hallo verbindingsreeks voor Azure DB die Cosmos-account kan worden opgehaald uit de blade van de sleutels Hallo van hello Azure-portal, zoals beschreven in [hoe toomanage een account voor Azure Cosmos DB](manage-account.md), maar de naam van de Hallo van Hallo-database toohello toobe toegevoegd moet de verbindingsreeks in Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="44878-330">hello Azure Cosmos DB account connection string can be retrieved from hello Keys blade of hello Azure portal, as described in [How toomanage an Azure Cosmos DB account](manage-account.md), however hello name of hello database needs toobe appended toohello connection string in hello following format:</span></span>

    Database=<Azure Cosmos DB Database>;

> [!NOTE]
> <span data-ttu-id="44878-331">Gebruik Hallo controleren opdracht tooensure die hello Azure DB die Cosmos-exemplaar is opgegeven in tekenreeksveld Hallo-verbinding kan worden benaderd.</span><span class="sxs-lookup"><span data-stu-id="44878-331">Use hello Verify command tooensure that hello Azure Cosmos DB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="44878-332">tooimport tooa één verzameling, Voer Hallo-naam van Hallo verzameling toowhich gegevens worden geïmporteerd en klik op de knop toevoegen Hallo.</span><span class="sxs-lookup"><span data-stu-id="44878-332">tooimport tooa single collection, enter hello name of hello collection toowhich data will be imported and click hello Add button.</span></span> <span data-ttu-id="44878-333">tooimport toomultiple verzamelingen, de verzamelingsnaam van elke afzonderlijk Voer of gebruik Hallo syntaxis toospecify na meerdere verzamelingen: *collection_prefix*[begin index - end-index].</span><span class="sxs-lookup"><span data-stu-id="44878-333">tooimport toomultiple collections, either enter each collection name individually or use hello following syntax toospecify multiple collections: *collection_prefix*[start index - end index].</span></span> <span data-ttu-id="44878-334">Houd rekening met Hallo volgende bij het opgeven van meerdere verzamelingen via de hiervoor genoemde Hallo-syntaxis:</span><span class="sxs-lookup"><span data-stu-id="44878-334">When specifying multiple collections via hello aforementioned syntax, keep hello following in mind:</span></span>

1. <span data-ttu-id="44878-335">Alleen geheel getal bereik bestandsnaampatronen worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="44878-335">Only integer range name patterns are supported.</span></span> <span data-ttu-id="44878-336">Bijvoorbeeld, geven verzameling [0-3] produceert Hallo verzamelingen te volgen: collection0, collection1, collection2, collection3.</span><span class="sxs-lookup"><span data-stu-id="44878-336">For example, specifying collection[0-3] will produce hello following collections: collection0, collection1, collection2, collection3.</span></span>
2. <span data-ttu-id="44878-337">U kunt een verkorte syntaxis gebruiken: verzameling [3] wordt vermeld in stap 1 verzamelingen dezelfde set verzenden.</span><span class="sxs-lookup"><span data-stu-id="44878-337">You can use an abbreviated syntax: collection[3] will emit same set of collections mentioned in step 1.</span></span>
3. <span data-ttu-id="44878-338">Meer dan een vervanging kan worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="44878-338">More than one substitution can be provided.</span></span> <span data-ttu-id="44878-339">Bijvoorbeeld, verzameling [0-1] [0-9] genereert 20 verzamelingsnamen met toonaangevende nullen (collection01,... 02... 03).</span><span class="sxs-lookup"><span data-stu-id="44878-339">For example, collection[0-1] [0-9] will generate 20 collection names with leading zeros (collection01, ..02, ..03).</span></span>

<span data-ttu-id="44878-340">Eenmaal hello verzameling namen zijn opgegeven, kiest u de gewenste doorvoer Hallo van Hallo verzameling(en) (400 RUs too250, 000 RUs).</span><span class="sxs-lookup"><span data-stu-id="44878-340">Once hello collection name(s) have been specified, choose hello desired throughput of hello collection(s) (400 RUs too250,000 RUs).</span></span> <span data-ttu-id="44878-341">Kies een hogere doorvoer voor de beste prestaties importeren.</span><span class="sxs-lookup"><span data-stu-id="44878-341">For best import performance, choose a higher throughput.</span></span> <span data-ttu-id="44878-342">Zie voor meer informatie over prestatieniveaus [prestatieniveaus in Azure Cosmos DB](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="44878-342">For more information about performance levels, see [Performance levels in Azure Cosmos DB](performance-levels.md).</span></span> <span data-ttu-id="44878-343">Een toocollections met doorvoer importeren > 10.000 RUs een partitiesleutel is vereist.</span><span class="sxs-lookup"><span data-stu-id="44878-343">Any import toocollections with throughput >10,000 RUs will require a partition key.</span></span> <span data-ttu-id="44878-344">Als u op meer dan 250.000 RUs toohave kiest, moet u toofile een aanvraag in de portal toohave Hallo verhoogd van uw account.</span><span class="sxs-lookup"><span data-stu-id="44878-344">If you choose toohave more than 250,000 RUs, you will need toofile a request in hello portal toohave your account increased.</span></span>

> [!NOTE]
> <span data-ttu-id="44878-345">Hallo doorvoer instelling is alleen van toepassing toocollection maken.</span><span class="sxs-lookup"><span data-stu-id="44878-345">hello throughput setting only applies toocollection creation.</span></span> <span data-ttu-id="44878-346">Als Hallo collectie al bestaat opgegeven, wordt de doorvoer niet gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="44878-346">If hello specified collection already exists, its throughput will not be modified.</span></span>
> 
> 

<span data-ttu-id="44878-347">Bij het importeren van verzamelingen toomultiple ondersteunt Hallo import-hulpprogramma hash op basis van sharding.</span><span class="sxs-lookup"><span data-stu-id="44878-347">When importing toomultiple collections, hello import tool supports hash based sharding.</span></span> <span data-ttu-id="44878-348">Geef in dit scenario Hallo documenteigenschap gewenst toouse als partitiesleutel Hallo (als partitiesleutel leeg is, documenten zijn shard willekeurig in Hallo doel verzamelingen).</span><span class="sxs-lookup"><span data-stu-id="44878-348">In this scenario, specify hello document property you wish toouse as hello Partition Key (if Partition Key is left blank, documents will be sharded randomly across hello target collections).</span></span>

<span data-ttu-id="44878-349">U kunt eventueel opgeven welk veld in de bron voor het importeren van Hallo als hello Azure Cosmos DB document-id-eigenschap moet worden gebruikt tijdens het importeren van hello (Let erop dat als documenten geen deze eigenschap bevatten, klikt u vervolgens Hallo import-hulpprogramma een GUID als de waarde van de eigenschap id Hallo genereert).</span><span class="sxs-lookup"><span data-stu-id="44878-349">You may optionally specify which field in hello import source should be used as hello Azure Cosmos DB document id property during hello import (note that if documents do not contain this property, then hello import tool will generate a GUID as hello id property value).</span></span>

<span data-ttu-id="44878-350">Er zijn tijdens het importeren van een aantal geavanceerde opties beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="44878-350">There are a number of advanced options available during import.</span></span> <span data-ttu-id="44878-351">Eerst bij het importeren van datum-typen (bijvoorbeeld van SQL Server of MongoDB), kunt u tussen de drie opties voor importeren:</span><span class="sxs-lookup"><span data-stu-id="44878-351">First, when importing date types (e.g. from SQL Server or MongoDB), you can choose between three import options:</span></span>

 ![Schermopname van Azure Cosmos DB datum tijdopties importeren](./media/import-data/datetimeoptions.png)

* <span data-ttu-id="44878-353">Tekenreeks: Behouden als een string-waarde</span><span class="sxs-lookup"><span data-stu-id="44878-353">String: Persist as a string value</span></span>
* <span data-ttu-id="44878-354">Epoche: Behouden als een getalwaarde epoche</span><span class="sxs-lookup"><span data-stu-id="44878-354">Epoch: Persist as an Epoch number value</span></span>
* <span data-ttu-id="44878-355">Beide: Zowel tekenreeks als numerieke waarden epoche bewaard.</span><span class="sxs-lookup"><span data-stu-id="44878-355">Both: Persist both string and Epoch number values.</span></span> <span data-ttu-id="44878-356">Deze optie maakt u een subdocument, bijvoorbeeld: "date_joined": {'' waarde '': ' 2013-10-21T21:17:25.2410000Z ', ' epoche ': 1382390245}</span><span class="sxs-lookup"><span data-stu-id="44878-356">This option will create a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span></span>

<span data-ttu-id="44878-357">Hello Azure DB Cosmos - sequentiële record importfunctie heeft Hallo volgende als u meer geavanceerde opties:</span><span class="sxs-lookup"><span data-stu-id="44878-357">hello Azure Cosmos DB - Sequential record importer has hello following additional advanced options:</span></span>

1. <span data-ttu-id="44878-358">Aantal parallelle aanvragen: Hallo hulpprogramma standaardinstellingen too2 parallelle aanvragen.</span><span class="sxs-lookup"><span data-stu-id="44878-358">Number of Parallel Requests: hello tool defaults too2 parallel requests.</span></span> <span data-ttu-id="44878-359">Als Hallo documenten toobe geïmporteerd klein zijn, kunt u overwegen Hallo aantal parallelle aanvragen verhogen.</span><span class="sxs-lookup"><span data-stu-id="44878-359">If hello documents toobe imported are small, consider raising hello number of parallel requests.</span></span> <span data-ttu-id="44878-360">Houd er rekening mee dat als dit nummer te veel wordt gegenereerd, Hallo importeren beperking ondervinden.</span><span class="sxs-lookup"><span data-stu-id="44878-360">Note that if this number is raised too much, hello import may experience throttling.</span></span>
2. <span data-ttu-id="44878-361">Schakel automatische van generatie-Id: Als elke document toobe geïmporteerd een id-veld bevat, deze optie kunt betere prestaties.</span><span class="sxs-lookup"><span data-stu-id="44878-361">Disable Automatic Id Generation: If every document toobe imported contains an id field, then selecting this option can increase performance.</span></span> <span data-ttu-id="44878-362">Een unieke id-veld ontbreekt documenten worden niet geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="44878-362">Documents missing a unique id field will not be imported.</span></span>
3. <span data-ttu-id="44878-363">Update bestaande documenten: Hallo hulpprogramma standaardwaarden toonot bestaande documenten vervangen door een ID-conflicten.</span><span class="sxs-lookup"><span data-stu-id="44878-363">Update Existing Documents: hello tool defaults toonot replacing existing documents with id conflicts.</span></span> <span data-ttu-id="44878-364">Deze optie kunt bestaande documenten met overeenkomende id overschrijven.</span><span class="sxs-lookup"><span data-stu-id="44878-364">Selecting this option will allow overwriting existing documents with matching ids.</span></span> <span data-ttu-id="44878-365">Deze functie is handig voor geplande gegevens migraties die bijwerken van bestaande documenten.</span><span class="sxs-lookup"><span data-stu-id="44878-365">This feature is useful for scheduled data migrations that update existing documents.</span></span>
4. <span data-ttu-id="44878-366">Aantal nieuwe pogingen bij fouten: Hiermee geeft u het aantal keren tooretry verbinding tooAzure Cosmos DB in geval van een tijdelijke fouten (bijvoorbeeld connectiviteit onderbreking op het netwerk) Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="44878-366">Number of Retries on Failure: Specifies hello number of times tooretry hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
5. <span data-ttu-id="44878-367">Interval voor opnieuw proberen: Geeft aan hoe lang toowait tussen opnieuw uit te voeren Hallo verbinding tooAzure Cosmos DB in geval van een tijdelijke fouten (bijvoorbeeld connectiviteit onderbreking op het netwerk).</span><span class="sxs-lookup"><span data-stu-id="44878-367">Retry Interval: Specifies how long toowait between retrying hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
6. <span data-ttu-id="44878-368">Verbindingsmodus: Hiermee geeft u Hallo verbinding modus toouse met Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="44878-368">Connection Mode: Specifies hello connection mode toouse with Azure Cosmos DB.</span></span> <span data-ttu-id="44878-369">Hallo beschikbare opties zijn DirectTcp, DirectHttps en Gateway.</span><span class="sxs-lookup"><span data-stu-id="44878-369">hello available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="44878-370">Hallo rechtstreekse verbinding modi zijn sneller, terwijl Hallo gateway modus meer firewall beschrijvende aangezien hierbij alleen poort 443.</span><span class="sxs-lookup"><span data-stu-id="44878-370">hello direct connection modes are faster, while hello gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Schermopname van Azure Cosmos DB sequentiële record importeren geavanceerde opties](./media/import-data/documentdbsequentialoptions.png)

> [!TIP]
> <span data-ttu-id="44878-372">Hallo hulpprogramma standaardwaarden tooconnection modus DirectTcp voor importeren.</span><span class="sxs-lookup"><span data-stu-id="44878-372">hello import tool defaults tooconnection mode DirectTcp.</span></span> <span data-ttu-id="44878-373">Als u de firewall-problemen ondervindt, overschakelen tooconnection modus Gateway, omdat hiervoor alleen poort 443.</span><span class="sxs-lookup"><span data-stu-id="44878-373">If you experience firewall issues, switch tooconnection mode Gateway, as it only requires port 443.</span></span>
> 
> 

## <span data-ttu-id="44878-374"><a id="IndexingPolicy"></a>Een indexeringsbeleid opgeven bij het maken van Azure DB die Cosmos-verzamelingen</span><span class="sxs-lookup"><span data-stu-id="44878-374"><a id="IndexingPolicy"></a>Specify an indexing policy when creating Azure Cosmos DB collections</span></span>
<span data-ttu-id="44878-375">Als u hulpprogramma toocreate verzamelingen Hallo migratie tijdens het importeren toestaat, kunt u Hallo indexeringsbeleid van Hallo verzamelingen.</span><span class="sxs-lookup"><span data-stu-id="44878-375">When you allow hello migration tool toocreate collections during import, you can specify hello indexing policy of hello collections.</span></span> <span data-ttu-id="44878-376">Navigeer in Hallo geavanceerde opties sectie van hello Azure Cosmos DB bulkimport en Azure Cosmos DB sequentiële record opties, toohello beleid Indexing-sectie.</span><span class="sxs-lookup"><span data-stu-id="44878-376">In hello advanced options section of hello Azure Cosmos DB Bulk import and Azure Cosmos DB Sequential record options, navigate toohello Indexing Policy section.</span></span>

![Schermopname van Azure Cosmos DB indexeren beleid geavanceerde opties](./media/import-data/indexingpolicy1.png)

<span data-ttu-id="44878-378">Hallo indexeren beleid geavanceerde optie gebruikt, kunt u selecteren een bestand met beleidsregel van indexering, handmatig een indexeringsbeleid invoeren, of uit een reeks standaardsjablonen (door de rechtermuisknop te klikken in Hallo beleid textbox indexeren).</span><span class="sxs-lookup"><span data-stu-id="44878-378">Using hello Indexing Policy advanced option, you can select an indexing policy file, manually enter an indexing policy, or select from a set of default templates (by right clicking in hello indexing policy textbox).</span></span>

<span data-ttu-id="44878-379">Beleidssjablonen Hallo Hallo hulpprogramma biedt zijn:</span><span class="sxs-lookup"><span data-stu-id="44878-379">hello policy templates hello tool provides are:</span></span>

* <span data-ttu-id="44878-380">De standaardinstelling.</span><span class="sxs-lookup"><span data-stu-id="44878-380">Default.</span></span> <span data-ttu-id="44878-381">Dit beleid wordt aanbevolen wanneer u het uitvoeren van de gelijkheid query uitgevoerd naar tekenreeksen en ORDER BY, bereik en gelijkheid query's gebruiken voor getallen.</span><span class="sxs-lookup"><span data-stu-id="44878-381">This policy is best when you’re performing equality queries against strings and using ORDER BY, range, and equality queries for numbers.</span></span> <span data-ttu-id="44878-382">Dit beleid heeft een lagere opslagoverhead voor indexering dan bereik.</span><span class="sxs-lookup"><span data-stu-id="44878-382">This policy has a lower index storage overhead than Range.</span></span>
* <span data-ttu-id="44878-383">Het bereik.</span><span class="sxs-lookup"><span data-stu-id="44878-383">Range.</span></span> <span data-ttu-id="44878-384">Dit beleid wordt aanbevolen u ORDER BY, bereik en gelijkheid query's op de cijfers en tekenreeksen.</span><span class="sxs-lookup"><span data-stu-id="44878-384">This policy is best you’re using ORDER BY, range and equality queries on both numbers and strings.</span></span> <span data-ttu-id="44878-385">Dit beleid heeft een hogere opslagoverhead voor indexering dan standaard of hash-bewerking.</span><span class="sxs-lookup"><span data-stu-id="44878-385">This policy has a higher index storage overhead than Default or Hash.</span></span>

![Schermopname van Azure Cosmos DB indexeren beleid geavanceerde opties](./media/import-data/indexingpolicy2.png)

> [!NOTE]
> <span data-ttu-id="44878-387">Als u een indexeringsbeleid niet opgeeft, wordt het standaardbeleid Hallo worden toegepast.</span><span class="sxs-lookup"><span data-stu-id="44878-387">If you do not specify an indexing policy, then hello default policy will be applied.</span></span> <span data-ttu-id="44878-388">Zie voor meer informatie over indexering beleid [Azure Cosmos DB indexeren beleid](indexing-policies.md).</span><span class="sxs-lookup"><span data-stu-id="44878-388">For more information about indexing policies, see [Azure Cosmos DB indexing policies](indexing-policies.md).</span></span>
> 
> 

## <a name="export-toojson-file"></a><span data-ttu-id="44878-389">TooJSON-bestand exporteren</span><span class="sxs-lookup"><span data-stu-id="44878-389">Export tooJSON file</span></span>
<span data-ttu-id="44878-390">Exportfunctie van Hello Azure Cosmos DB JSON kunt u tooexport van Hallo beschikbare bron opties tooa JSON-bestand met een matrix met JSON-documenten.</span><span class="sxs-lookup"><span data-stu-id="44878-390">hello Azure Cosmos DB JSON exporter allows you tooexport any of hello available source options tooa JSON file that contains an array of JSON documents.</span></span> <span data-ttu-id="44878-391">Hallo-hulpprogramma wordt afgehandeld Hallo exporteren voor u of u kunt kiezen tooview Hallo resulterende migratie opdracht en voert u de opdracht Hallo zelf.</span><span class="sxs-lookup"><span data-stu-id="44878-391">hello tool will handle hello export for you, or you can choose tooview hello resulting migration command and run hello command yourself.</span></span> <span data-ttu-id="44878-392">Hallo resulterende JSON-bestand kan worden opgeslagen, lokaal of in Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="44878-392">hello resulting JSON file may be stored locally or in Azure Blob storage.</span></span>

![Schermopname van Azure Cosmos DB JSON-optie voor het exporteren van lokaal bestand](./media/import-data/jsontarget.png)

![Schermopname van Azure Cosmos DB JSON Azure Blob storage exportoptie](./media/import-data/jsontarget2.png)

<span data-ttu-id="44878-395">U kunt eventueel tooprettify Hallo resulterende JSON die wordt vergroot Hallo Hallo resulterende document terwijl meer leesbaar waardoor Hallo inhoud.</span><span class="sxs-lookup"><span data-stu-id="44878-395">You may optionally choose tooprettify hello resulting JSON, which will increase hello size of hello resulting document while making hello contents more human readable.</span></span>

    Standard JSON export
    [{"id":"Sample","Title":"About Paris","Language":{"Name":"English"},"Author":{"Name":"Don","Location":{"City":"Paris","Country":"France"}},"Content":"Don's document in Azure Cosmos DB is a valid JSON document as defined by hello JSON spec.","PageViews":10000,"Topics":[{"Title":"History of Paris"},{"Title":"Places toosee in Paris"}]}]

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
    "Content": "Don's document in Azure Cosmos DB is a valid JSON document as defined by hello JSON spec.",
    "PageViews": 10000,
    "Topics": [
      {
        "Title": "History of Paris"
      },
      {
        "Title": "Places toosee in Paris"
      }
    ]
    }]

## <a name="advanced-configuration"></a><span data-ttu-id="44878-396">Geavanceerde configuratie</span><span class="sxs-lookup"><span data-stu-id="44878-396">Advanced configuration</span></span>
<span data-ttu-id="44878-397">Geef Hallo-locatie van Hallo log-bestand toowhich eventuele fouten die zijn geschreven gewenst in Hallo geavanceerde configuratie.</span><span class="sxs-lookup"><span data-stu-id="44878-397">In hello Advanced configuration screen, specify hello location of hello log file toowhich you would like any errors written.</span></span> <span data-ttu-id="44878-398">Hallo volgens de regels van toepassing toothis pagina:</span><span class="sxs-lookup"><span data-stu-id="44878-398">hello following rules apply toothis page:</span></span>

1. <span data-ttu-id="44878-399">Als een bestandsnaam niet opgegeven is, wordt op Hallo resultatenpagina alle fouten geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="44878-399">If a file name is not provided, then all errors will be returned on hello Results page.</span></span>
2. <span data-ttu-id="44878-400">Als een bestandsnaam is opgegeven zonder een map, wordt klikt u vervolgens Hallo-bestand gemaakt (of overschreven) in de huidige omgeving map Hallo.</span><span class="sxs-lookup"><span data-stu-id="44878-400">If a file name is provided without a directory, then hello file will be created (or overwritten) in hello current environment directory.</span></span>
3. <span data-ttu-id="44878-401">Als u selecteert een bestaand bestand en vervolgens Hallo-bestand wordt overschreven, er is geen optie toevoegen.</span><span class="sxs-lookup"><span data-stu-id="44878-401">If you select an existing file, then hello file will be overwritten, there is no append option.</span></span>

<span data-ttu-id="44878-402">Kies of alle toolog, kritiek, of er geen foutberichten.</span><span class="sxs-lookup"><span data-stu-id="44878-402">Then, choose whether toolog all, critical, or no error messages.</span></span> <span data-ttu-id="44878-403">Ten slotte kunt u bepalen hoe vaak Hallo voor scherm overdracht bericht wordt bijgewerkt met de voortgang ervan.</span><span class="sxs-lookup"><span data-stu-id="44878-403">Finally, decide how frequently hello on screen transfer message will be updated with its progress.</span></span>

    ![Screenshot of Advanced configuration screen](./media/import-data/AdvancedConfiguration.png)

## <a name="confirm-import-settings-and-view-command-line"></a><span data-ttu-id="44878-404">Bevestig de instellingen importeren en weergeven vanaf de opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="44878-404">Confirm import settings and view command line</span></span>
1. <span data-ttu-id="44878-405">Na het opgeven van informatie van gegevensbron, doelinformatie en geavanceerde configuratie, bekijk Hallo migratie samenvatting en, desgewenst weergeven/kopiëren Hallo resulterende migratie-opdracht (kopiëren Hallo-opdracht is nuttig tooautomate importbewerkingen):</span><span class="sxs-lookup"><span data-stu-id="44878-405">After specifying source information, target information, and advanced configuration, review hello migration summary and, optionally, view/copy hello resulting migration command (copying hello command is useful tooautomate import operations):</span></span>
   
    ![Schermopname van het scherm Samenvatting](./media/import-data/summary.png)
   
    ![Schermopname van het scherm Samenvatting](./media/import-data/summarycommand.png)
2. <span data-ttu-id="44878-408">Wanneer u tevreden met de bron en doel-opties bent, klikt u op **importeren**.</span><span class="sxs-lookup"><span data-stu-id="44878-408">Once you’re satisfied with your source and target options, click **Import**.</span></span> <span data-ttu-id="44878-409">Hallo verstreken tijd, overgedragen aantal en foutgegevens (als u een bestandsnaam in de geavanceerde configuratie Hallo niet opgeven) wordt bijgewerkt Hallo importeren bezig is.</span><span class="sxs-lookup"><span data-stu-id="44878-409">hello elapsed time, transferred count, and failure information (if you didn't provide a file name in hello Advanced configuration) will update as hello import is in process.</span></span> <span data-ttu-id="44878-410">Als u klaar is, kunt u Hallo resultaten (bijvoorbeeld toodeal met alle mislukte importeren) exporteren.</span><span class="sxs-lookup"><span data-stu-id="44878-410">Once complete, you can export hello results (e.g. toodeal with any import failures).</span></span>
   
    ![Schermopname van Azure Cosmos DB JSON exportoptie](./media/import-data/viewresults.png)
3. <span data-ttu-id="44878-412">U mogelijk ook een nieuwe import starten te behouden de bestaande instellingen hello (bijvoorbeeld verbinding tekenreeks informatie, de bron en doel keuze, etc.) of opnieuw instellen van alle waarden.</span><span class="sxs-lookup"><span data-stu-id="44878-412">You may also start a new import, either keeping hello existing settings (e.g. connection string information, source and target choice, etc.) or resetting all values.</span></span>
   
    ![Schermopname van Azure Cosmos DB JSON exportoptie](./media/import-data/newimport.png)

## <a name="next-steps"></a><span data-ttu-id="44878-414">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="44878-414">Next steps</span></span>

<span data-ttu-id="44878-415">In deze zelfstudie hebt u Hallo volgende gedaan:</span><span class="sxs-lookup"><span data-stu-id="44878-415">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="44878-416">Hallo-hulpprogramma voor gegevensmigratie geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="44878-416">Installed hello Data Migration tool</span></span>
> * <span data-ttu-id="44878-417">Geïmporteerde gegevens uit verschillende gegevensbronnen</span><span class="sxs-lookup"><span data-stu-id="44878-417">Imported data from different data sources</span></span>
> * <span data-ttu-id="44878-418">Geëxporteerd vanuit Azure Cosmos DB tooJSON</span><span class="sxs-lookup"><span data-stu-id="44878-418">Exported from Azure Cosmos DB tooJSON</span></span>

<span data-ttu-id="44878-419">U kunt nu de volgende zelfstudie toohello gaan en meer informatie hoe tooquery-gegevens met behulp van Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="44878-419">You can now proceed toohello next tutorial and learn how tooquery data using Azure Cosmos DB.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="44878-420">Hoe tooquery gegevens?</span><span class="sxs-lookup"><span data-stu-id="44878-420">How tooquery data?</span></span>](../cosmos-db/tutorial-query-documentdb.md)
