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
# <a name="how-tooimport-data-into-azure-cosmos-db-for-hello-documentdb-api"></a>Hoe Hallo tooimport gegevens naar Azure Cosmos DB voor DocumentDB API?

Deze zelfstudie bevat instructies over het gebruik van Azure DB die Cosmos Hallo: hulpprogramma voor gegevensmigratie voor DocumentDB-API, die u gegevens uit diverse bronnen importeren kunt, met inbegrip van JSON-bestanden, CSV-bestanden, SQL, MongoDB, Azure Table storage, Amazon DynamoDB en Azure Cosmos DB DocumentDB API-verzamelingen in verzamelingen voor gebruiken met Azure Cosmos DB en Hallo DocumentDB-API. hulpprogramma voor gegevensmigratie Hallo kan ook worden gebruikt bij het migreren van een verzameling van één partitie verzameling tooa meerdere partitie voor Hallo DocumentDB-API.

hulpprogramma voor gegevensmigratie Hallo werkt alleen wanneer het importeren van gegevens naar Azure Cosmos DB voor gebruik met Hallo DocumentDB-API. Het importeren van gegevens voor gebruik met Hallo tabel API of Graph API wordt niet ondersteund op dit moment. 

tooimport gegevens voor gebruik met Hallo MongoDB-API, Zie [Azure Cosmos DB: hoe toomigrate-gegevens voor de MongoDB-API Hallo?](mongodb-migrate.md).

Deze zelfstudie behandelt Hallo taken te volgen:

> [!div class="checklist"]
> * Hallo-hulpprogramma voor gegevensmigratie installeren
> * Het importeren van gegevens uit verschillende gegevensbronnen
> * Exporteren van Azure DB die Cosmos tooJSON

## <a id="Prerequisites"></a>Vereisten
Zorg ervoor dat er Hallo volgende zijn geïnstalleerd voordat Hallo-instructies in dit artikel:

* [Microsoft .NET Framework 4,51](https://www.microsoft.com/download/developer-tools.aspx) of hoger.

## <a id="Overviewl"></a>Overzicht van het hulpprogramma voor gegevensmigratie Hallo
Hallo-hulpprogramma voor gegevensmigratie is een open-source-oplossing die gegevens tooAzure Cosmos DB uit diverse bronnen importeert, met inbegrip van:

* JSON-bestanden
* MongoDB
* SQL Server
* CSV-bestanden
* Azure Table Storage
* Amazon DynamoDB
* HBase
* Azure DB Cosmos-verzamelingen

Tijdens het Hallo-import-hulpprogramma omvat een grafische gebruikersinterface (dtui.exe), kan het ook aangestuurd vanaf de opdrachtregel hello (dt.exe). Er is in feite een opdracht optie toooutput Hallo die zijn gekoppeld na het instellen van een import via Hallo gebruikersinterface. In tabelvorm brongegevens (bijvoorbeeld SQL Server- of CSV-bestanden) kan worden getransformeerd zodat hiërarchische relaties (subdocumenten) kunnen worden gemaakt tijdens het importeren. Houd lezen toolearn meer informatie over opties voor gegevensbron voorbeeld opdrachtregels tooimport van elke bron, doel-opties en weer te geven resultaten importeren.

## <a id="Install"></a>Hallo-hulpprogramma voor gegevensmigratie installeren
broncode van Hallo migratie hulpprogramma is beschikbaar op GitHub in [deze opslagplaats](https://github.com/azure/azure-documentdb-datamigrationtool) en een gecompileerde versie is beschikbaar vanuit [Microsoft Download Center](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d). U kunt compileren Hallo oplossing of gewoon downloaden en extraheren Hallo gecompileerde versie tooa directory van uw keuze. Voer vervolgens een:

* **Dtui.exe**: versie van de grafische interface van Hallo-hulpprogramma
* **DT.exe**: opdrachtregelprogramma versie van Hallo-hulpprogramma

## <a name="import-data"></a>Gegevens importeren

Zodra u Hallo-hulpprogramma hebt geïnstalleerd, is het tijd tooimport uw gegevens. Welk type gegevens wilt u toch tooimport?

* [JSON-bestanden](#JSON)
* [MongoDB](#MongoDB)
* [MongoDB exportbestanden](#MongoDBExport)
* [SQL Server](#SQL)
* [CSV-bestanden](#CSV)
* [Azure Table storage](#AzureTableSource)
* [Amazon DynamoDB](#DynamoDBSource)
* [BLOB](#BlobImport)
* [Azure DB Cosmos-verzamelingen](#DocumentDBSource)
* [HBase](#HBaseSource)
* [Azure DB Cosmos bulkimport](#DocumentDBBulkImport)
* [Azure DB Cosmos sequentiële record importeren](#DocumentDSeqTarget)


## <a id="JSON"></a>tooimport JSON-bestanden
Hallo JSON-bestand bron importfunctie optie kunt u tooimport een of meer JSON-bestanden voor één document of JSON-bestanden dat elk een matrix met JSON-documenten bevatten. Als u mappen met JSON-bestanden tooimport toevoegt, hebt u de mogelijkheid Hallo van recursief zoeken naar bestanden in submappen.

![Schermopname van JSON-bestand bronopties - hulpprogramma's voor migratie](./media/import-data/jsonsource.png)

Hier volgen enkele opdrachtregel voorbeelden tooimport JSON-bestanden:

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

## <a id="MongoDB"></a>tooimport van MongoDB

> [!IMPORTANT]
> Als u Azure DB die Cosmos-account met ondersteuning voor MongoDB tooan importeert, volgt u deze [instructies](mongodb-migrate.md).
> 
> 

Hallo MongoDB bron importfunctie optie kunt u tooimport uit een afzonderlijke MongoDB-verzameling en filter optioneel documenten met behulp van een query en/of Hallo documentstructuur wijzigen met behulp van een projectie.  

![Schermopname van MongoDB-opties voor gegevensbron](./media/import-data/mongodbsource.png)

Hallo-verbindingsreeks is in de Hallo standaard MongoDB-indeling:

    mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database>

> [!NOTE]
> Gebruik Hallo controleren opdracht tooensure die Hallo MongoDB-exemplaar is opgegeven in tekenreeksveld Hallo-verbinding kan worden benaderd.
> 
> 

Voer de naam Hallo van Hallo-verzameling van waaruit de gegevens worden geïmporteerd. U kunt eventueel opgeven of een bestand voor een query opgeven (bijvoorbeeld {pop: {$gt: 5000}}) en/of een projectie (bijvoorbeeld {loc:0}) tooboth filter en vorm Hallo gegevens toobe geïmporteerd.

Hier volgen enkele tooimport opdrachtregel voorbeelden van MongoDB:

    #Import all documents from a MongoDB collection
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZips /t.IdField:_id /t.CollectionThroughput:2500

    #Import documents from a MongoDB collection which match hello query and exclude hello loc field
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /s.Query:{pop:{$gt:50000}} /s.Projection:{loc:0} /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZipsTransform /t.IdField:_id/t.CollectionThroughput:2500

## <a id="MongoDBExport"></a>tooimport MongoDB exportbestanden

> [!IMPORTANT]
> Als u Azure DB die Cosmos-account met ondersteuning voor MongoDB tooan importeert, volgt u deze [instructies](mongodb-migrate.md).
> 
> 

Hallo importfunctie optie voor de gegevensbron van MongoDB export JSON-bestand kunt u tooimport een of meer JSON-bestanden die zijn geproduceerd met Hallo mongoexport hulpprogramma.  

![Schermopname van MongoDB-exportopties bron](./media/import-data/mongodbexportsource.png)

Als u mappen met MongoDB export JSON-bestanden voor het importeren van toevoegt, hebt u de mogelijkheid Hallo van recursief zoeken naar bestanden in submappen.

Hier volgt een opdrachtregel voorbeeld tooimport van MongoDB export JSON-bestanden:

    dt.exe /s:MongoDBExport /s.Files:D:\mongoemployees.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:employees /t.IdField:_id /t.Dates:Epoch /t.CollectionThroughput:2500

## <a id="SQL"></a>tooimport van SQL Server
Hallo SQL bron importfunctie optie kunt u tooimport uit een afzonderlijke SQL Server-database en filter optioneel Hallo records toobe geïmporteerd met behulp van een query. Bovendien kunt u de documentstructuur Hallo wijzigen door op te geven van een geneste scheidingsteken (meer informatie over die later).  

![Schermafbeelding van de SQL - opties voor hulpprogramma's voor migratie](./media/import-data/sqlexportsource.png)

Hallo-indeling van de verbindingsreeks Hallo is Hallo standaard SQL indeling voor een verbindingsreeks.

> [!NOTE]
> Gebruik Hallo controleren opdracht tooensure die SQL Server-exemplaar is opgegeven in Hallo verbinding tekenreeksveld Hallo toegankelijk zijn.
> 
> 

Hallo nesten scheidingsteken eigenschap wordt gebruikte toocreate hiërarchische relaties (onderliggende documenten) tijdens het importeren. Houd rekening met Hallo SQL-query te volgen:

*CAST (BusinessEntityID AS varchar) als de Id, naam, adrestype als [Address.AddressType], AddressLine1 als [Address.AddressLine1], plaats als [Address.Location.City], StateProvinceName als [Address.Location.StateProvinceName], postcode als [selecteren Address.PostalCode] CountryRegionName als [Address.CountryRegionName] uit Sales.vStoreWithAddresses waar adrestype = 'Hoofdkantoor'*

Die resulteert hello (gedeeltelijke) resultaten te volgen:

![Schermafbeelding van de SQL-queryresultaten](./media/import-data/sqlqueryresults.png)

Houd er rekening mee Hallo aliassen zoals Address.AddressType en Address.Location.StateProvinceName. Door op te geven van een geneste scheidingsteken van '.', Hallo import-hulpprogramma maakt adres en Address.Location subdocumenten tijdens Hallo importeren. Hier volgt een voorbeeld van een resulterende document in Azure Cosmos DB:

*{'id': '956', 'Name': 'Fijner verkoop en Service', 'Adres': {'Adrestype': 'Hoofdkantoor', 'AddressLine1': '#500 75 O'Connor straat', 'Locatie': {'Stad': 'Canada Ottawa', 'StateProvinceName': "Ontario"}, 'Postcode': 'K4B 1S2', 'CountryRegionName': ' Canada'}}*

Hier volgen enkele tooimport opdrachtregel voorbeelden van SQL Server:

    #Import records from SQL which match a query
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, * from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Stores /t.IdField:Id /t.CollectionThroughput:2500

    #Import records from sql which match a query and create hierarchical relationships
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /s.NestingSeparator:. /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:StoresSub /t.IdField:Id /t.CollectionThroughput:2500

## <a id="CSV"></a>tooimport CSV-bestanden en converteren CSV tooJSON
Hallo CSV-bestand bron importfunctie optie kunt u tooimport een of meer CSV-bestanden. Als u mappen met CSV-bestanden voor het importeren van toevoegt, hebt u de mogelijkheid Hallo van recursief zoeken naar bestanden in submappen.

![Schermopname van CSV - opties voor CSV tooJSON](media/import-data/csvsource.png)

SQL-bron vergelijkbare toohello, Hallo scheidingsteken eigenschap nesten mogelijk gebruikte toocreate hiërarchische relaties (onderliggende documenten) tijdens het importeren. Houd rekening met Hallo veldnamenrij CSV en gegevensrijen te volgen:

![Schermopname van CSV-voorbeeld registreert - CSV tooJSON](./media/import-data/csvsample.png)

Houd er rekening mee Hallo aliassen zoals DomainInfo.Domain_Name en RedirectInfo.Redirecting. Door op te geven van een geneste scheidingsteken van '.', Hallo import-hulpprogramma DomainInfo maakt en RedirectInfo subdocumenten tijdens Hallo importeren. Hier volgt een voorbeeld van een resulterende document in Azure Cosmos DB:

*{{"DomainInfo": {'Domeinnaam': 'ACUS.GOV', 'Domain_Name_Address': 'http://www. ACUS.GOV"}, 'Federale instantie': 'Beheerdersrechten Conferentie van Hallo Verenigde Staten',"RedirectInfo": {'Omleiden': '0', 'Redirect_Destination': '"}, 'id': '9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d'}*

hulpprogramma voor het importeren van Hallo probeert tooinfer type-informatie voor zonder aanhalingstekens waarden in CSV-bestanden (tussen aanhalingstekens waarden worden altijd behandeld als tekenreeksen).  Typen in Hallo volgorde worden aangeduid: getal, datum/tijd, Booleaanse waarde.  

Er zijn twee andere dingen toonote over CSV-import:

1. Standaard zonder aanhalingstekens waarden zijn altijd bijgesneden voor tabs en spaties, terwijl tussen aanhalingstekens waarden behouden als blijven-is. Dit gedrag kan worden onderdrukt met Hallo die Trim aanhalingstekens waarden checkbox of Hallo /s.TrimQuoted opdrachtregeloptie.
2. Standaard wordt een zonder aanhalingstekens null worden beschouwd als een null-waarde. Dit gedrag kan worden genegeerd (dat wil zeggen een zonder aanhalingstekens null behandelen als een tekenreeks 'null') Hello zonder aanhalingstekens NULL als tekenreeks checkbox of Hallo /s.NoUnquotedNulls opdrachtregeloptie behandelen.

Hier volgt een voorbeeld van de opdrachtregel voor CSV-import:

    dt.exe /s:CsvFile /s.Files:.\Employees.csv /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Employees /t.IdField:EntityID /t.CollectionThroughput:2500

## <a id="AzureTableSource"></a>tooimport uit Azure Table storage
Hallo bron Azure Table-importprogramma opslagoptie kunt u tooimport uit een afzonderlijke tabel voor Azure Table storage en filter optioneel Hallo tabel entiteiten toobe geïmporteerd. Houd er rekening mee dat u Hallo gegevensmigratie hulpprogramma tooimport Azure Table storage-gegevens naar Azure Cosmos DB kan niet voor gebruik met Hallo tabel-API gebruiken. Alleen importeren tooAzure Cosmos DB voor gebruik met DocumentDB API hello wordt ondersteund op dit moment.

![Schermopname van Azure Table storage bronopties](./media/import-data/azuretablesource.png)

Hallo-indeling van Hallo verbindingsreeks voor Azure Table-opslag is:

    DefaultEndpointsProtocol=<protocol>;AccountName=<Account Name>;AccountKey=<Account Key>;

> [!NOTE]
> Gebruik Hallo controleren opdracht tooensure die hello Azure Table storage-exemplaar is opgegeven in tekenreeksveld Hallo-verbinding kan worden benaderd.
> 
> 

Voer de naam Hallo van hello Azure tabel waaruit gegevens worden geïmporteerd. U kunt eventueel opgeven een [filter](https://msdn.microsoft.com/library/azure/ff683669.aspx).

Hello Azure Table storage bronoptie importfunctie heeft Hallo extra opties te volgen:

1. Interne velden bevatten
   1. All - omvatten alle interne velden (PartitionKey, RowKey en tijdstempel)
   2. Geen - uitsluiten alle interne velden
   3. RowKey - Hallo RowKey veld alleen opnemen
2. Kolommen selecteren
   1. Azure Table storage filters bieden geen ondersteuning voor projecties. Als u tooonly importeren specifieke Azure Table-entiteitseigenschappen wilt, ze toohello kolommen selecteren lijst toevoegen. Alle andere entiteitseigenschappen wordt genegeerd.

Hier volgt een opdrachtregel voorbeeld tooimport uit Azure Table storage:

    dt.exe /s:AzureTable /s.ConnectionString:"DefaultEndpointsProtocol=https;AccountName=<Account Name>;AccountKey=<Account Key>" /s.Table:metrics /s.InternalFields:All /s.Filter:"PartitionKey eq 'Partition1' and RowKey gt '00001'" /s.Projection:ObjectCount;ObjectSize  /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:metrics /t.CollectionThroughput:2500

## <a id="DynamoDBSource"></a>tooimport van Amazon DynamoDB
Hallo Amazon DynamoDB bron importfunctie optie kunt u tooimport uit de tabel van een afzonderlijke Amazon DynamoDB en filter optioneel Hallo entiteiten toobe geïmporteerd. Verschillende sjablonen zijn bedoeld om het instellen van een import zo eenvoudig mogelijk is.

![Schermopname van Amazon DynamoDB bronopties - hulpprogramma's voor migratie](./media/import-data/dynamodbsource1.png)

![Schermopname van Amazon DynamoDB bronopties - hulpprogramma's voor migratie](./media/import-data/dynamodbsource2.png)

Hallo-indeling van Hallo Amazon DynamoDB verbindingsreeks is:

    ServiceURL=<Service Address>;AccessKey=<Access Key>;SecretKey=<Secret Key>;

> [!NOTE]
> Gebruik Hallo controleren opdracht tooensure die Hallo DynamoDB Amazon-exemplaar is opgegeven in tekenreeksveld Hallo-verbinding kan worden benaderd.
> 
> 

Hier volgt een opdrachtregel voorbeeld tooimport van Amazon DynamoDB:

    dt.exe /s:DynamoDB /s.ConnectionString:ServiceURL=https://dynamodb.us-east-1.amazonaws.com;AccessKey=<accessKey>;SecretKey=<secretKey> /s.Request:"{   """TableName""": """ProductCatalog""" }" /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<Azure Cosmos DB Endpoint>;AccountKey=<Azure Cosmos DB Key>;Database=<Azure Cosmos DB Database>;" /t.Collection:catalogCollection /t.CollectionThroughput:2500

## <a id="BlobImport"></a>tooimport bestanden uit Azure Blob-opslag
Hallo JSON-bestand, MongoDB-exportbestand en CSV-bestand bron importfunctie opties kunnen u tooimport een of meer bestanden uit Azure Blob-opslag. Nadat u een URL van de Blob-container en de Accountsleutel, moet u gewoon een reguliere expressie tooselect Hallo bestand(en) tooimport bieden.

![Schermopname van Blob-bestand bronopties](./media/import-data/blobsource.png)

Ga als volgt vanaf de opdrachtregel tooimport JSON voorbeeldbestanden uit Azure Blob-opslag:

    dt.exe /s:JsonFile /s.Files:"blobs://<account key>@account.blob.core.windows.net:443/importcontainer/.*" /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:doctest

## <a id="DocumentDBSource"></a>tooimport uit een verzameling Azure Cosmos DB DocumentDB-API
Hello Azure Cosmos DB bron importfunctie optie kunt u tooimport gegevens uit een of meer Azure Cosmos DB verzamelingen en filter optioneel documenten met behulp van een query.  

![Opties voor schermopname van Azure Cosmos DB-gegevensbron](./media/import-data/documentdbsource.png)

Hallo-indeling van hello Azure Cosmos DB-verbindingsreeks is:

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

Hallo verbindingsreeks voor Azure DB die Cosmos-account kan worden opgehaald uit de blade van de sleutels Hallo van hello Azure-portal, zoals beschreven in [hoe toomanage een account voor Azure Cosmos DB](manage-account.md), maar de naam van de Hallo van Hallo-database toohello toobe toegevoegd moet de verbindingsreeks in Hallo volgende indeling:

    Database=<CosmosDB Database>;

> [!NOTE]
> Gebruik Hallo controleren opdracht tooensure die hello Azure DB die Cosmos-exemplaar is opgegeven in tekenreeksveld Hallo-verbinding kan worden benaderd.
> 
> 

tooimport van één Azure Cosmos DB verzameling Hallo naam invoeren van Hallo-verzameling van waaruit de gegevens worden geïmporteerd. tooimport van meerdere Azure Cosmos DB verzamelingen bieden een reguliere expressie toomatch een of meer verzamelingsnamen (bijvoorbeeld collection01 | collection02 | collection03). U kan eventueel opgeeft, of een bestand voor een query tooboth filter opgeven en vorm Hallo gegevens toobe geïmporteerd.

> [!NOTE]
> Aangezien Hallo verzameling veld reguliere expressies, accepteert als u wilt importeren uit één verzameling waarvan de naam tekens van de reguliere expressie bevat, moeten vervolgens die tekens worden voorafgegaan dienovereenkomstig.
> 
> 

Hello Azure Cosmos DB importfunctie bronoptie heeft Hallo volgende geavanceerde opties:

1. Interne velden bevatten: Geeft aan of tooinclude Azure Cosmos DB document Systeemeigenschappen in Hallo exporteren (bijvoorbeeld _rid, _ts).
2. Aantal nieuwe pogingen bij fouten: Hiermee geeft u het aantal keren tooretry verbinding tooAzure Cosmos DB in geval van een tijdelijke fouten (bijvoorbeeld connectiviteit onderbreking op het netwerk) Hallo Hallo.
3. Interval voor opnieuw proberen: Geeft aan hoe lang toowait tussen opnieuw uit te voeren Hallo verbinding tooAzure Cosmos DB in geval van een tijdelijke fouten (bijvoorbeeld connectiviteit onderbreking op het netwerk).
4. Verbindingsmodus: Hiermee geeft u Hallo verbinding modus toouse met Azure Cosmos DB. Hallo beschikbare opties zijn DirectTcp, DirectHttps en Gateway. Hallo rechtstreekse verbinding modi zijn sneller, terwijl Hallo gateway modus meer firewall beschrijvende aangezien hierbij alleen poort 443.

![Schermopname van Azure Cosmos DB bron geavanceerde opties](./media/import-data/documentdbsourceoptions.png)

> [!TIP]
> Hallo hulpprogramma standaardwaarden tooconnection modus DirectTcp voor importeren. Als u de firewall-problemen ondervindt, overschakelen tooconnection modus Gateway, omdat hiervoor alleen poort 443.
> 
> 

Hier volgen enkele tooimport opdrachtregel voorbeelden van Azure DB die Cosmos:

    #Migrate data from one Azure Cosmos DB collection tooanother Azure Cosmos DB collections
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:TEColl /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:TESessions /t.CollectionThroughput:2500

    #Migrate data from multiple Azure Cosmos DB collections tooa single Azure Cosmos DB collection
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:comp1|comp2|comp3|comp4 /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:singleCollection /t.CollectionThroughput:2500

    #Export an Azure Cosmos DB collection tooa JSON file
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:StoresSub /t:JsonFile /t.File:StoresExport.json /t.Overwrite /t.CollectionThroughput:2500

> [!TIP]
> Hello Azure Cosmos DB Data Import-hulpprogramma ondersteunt ook het importeren van gegevens van Hallo [Azure Cosmos DB Emulator](local-emulator.md). Bij het importeren van een lokale emulator, Hallo eindpunt instellen te`https://localhost:<port>`. 
> 
> 

## <a id="HBaseSource"></a>tooimport van HBase
Hallo HBase bron importfunctie optie kunt u tooimport gegevens uit een HBase-tabel en eventueel Hallo gegevens te filteren. Verschillende sjablonen zijn bedoeld om het instellen van een import zo eenvoudig mogelijk is.

![Schermopname van HBase-opties voor gegevensbron](./media/import-data/hbasesource1.png)

![Schermopname van HBase-opties voor gegevensbron](./media/import-data/hbasesource2.png)

Hallo-indeling van Hallo HBase Stargate verbindingsreeks is:

    ServiceURL=<server-address>;Username=<username>;Password=<password>

> [!NOTE]
> Gebruik Hallo controleren opdracht tooensure die Hallo HBase-exemplaar is opgegeven in tekenreeksveld Hallo-verbinding kan worden benaderd.
> 
> 

Hier volgt een opdrachtregel voorbeeld tooimport van HBase:

    dt.exe /s:HBase /s.ConnectionString:ServiceURL=<server-address>;Username=<username>;Password=<password> /s.Table:Contacts /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:hbaseimport

## <a id="DocumentDBBulkTarget"></a>tooimport toohello DocumentDB-API (bulkimport)
Importfunctie van Hello Azure Cosmos DB bulksgewijs kunt u tooimport vanaf elke Hallo beschikbare opties voor gegevensbron met behulp van een Azure Cosmos DB opgeslagen procedure voor efficiëntie. Hallo-hulpprogramma ondersteunt één gepartitioneerd Azure Cosmos DB verzameling tooone importeren, evenals shard importeren, waarbij de gegevens in meerdere één gepartitioneerd Azure Cosmos DB verzamelingen zijn gepartitioneerd. Zie voor meer informatie over het partitioneren van gegevens, [partitionering en schalen in Azure Cosmos DB](partition-data.md). Hallo-hulpprogramma wordt maken, uitvoeren en vervolgens Hallo opgeslagen procedure verwijderen uit de verzameling(en) van Hallo doel.  

![Schermopname van Azure Cosmos DB bulksgewijs opties](./media/import-data/documentdbbulk.png)

Hallo-indeling van hello Azure Cosmos DB-verbindingsreeks is:

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

Hallo verbindingsreeks voor Azure DB die Cosmos-account kan worden opgehaald uit de blade van de sleutels Hallo van hello Azure-portal, zoals beschreven in [hoe toomanage een account voor Azure Cosmos DB](manage-account.md), maar de naam van de Hallo van Hallo-database toohello toobe toegevoegd moet de verbindingsreeks in Hallo volgende indeling:

    Database=<CosmosDB Database>;

> [!NOTE]
> Gebruik Hallo controleren opdracht tooensure die hello Azure DB die Cosmos-exemplaar is opgegeven in tekenreeksveld Hallo-verbinding kan worden benaderd.
> 
> 

tooimport tooa één verzameling, Voer Hallo-naam van Hallo verzameling toowhich gegevens worden geïmporteerd en klik op de knop toevoegen Hallo. tooimport toomultiple verzamelingen, de verzamelingsnaam van elke afzonderlijk Voer of gebruik Hallo syntaxis toospecify na meerdere verzamelingen: *collection_prefix*[begin index - end-index]. Houd rekening met Hallo volgende bij het opgeven van meerdere verzamelingen via de hiervoor genoemde Hallo-syntaxis:

1. Alleen geheel getal bereik bestandsnaampatronen worden ondersteund. Bijvoorbeeld, geven verzameling [0-3] produceert Hallo verzamelingen te volgen: collection0, collection1, collection2, collection3.
2. U kunt een verkorte syntaxis gebruiken: verzameling [3] wordt vermeld in stap 1 verzamelingen dezelfde set verzenden.
3. Meer dan een vervanging kan worden opgegeven. Bijvoorbeeld, verzameling [0-1] [0-9] genereert 20 verzamelingsnamen met toonaangevende nullen (collection01,... 02... 03).

Eenmaal hello verzameling namen zijn opgegeven, kiest u de gewenste doorvoer Hallo van Hallo verzameling(en) (400 RUs too10, 000 RUs). Kies een hogere doorvoer voor de beste prestaties importeren. Zie voor meer informatie over prestatieniveaus [prestatieniveaus in Azure Cosmos DB](performance-levels.md).

> [!NOTE]
> Hallo prestatie doorvoer-instelling is alleen van toepassing toocollection maken. Als Hallo collectie al bestaat opgegeven, wordt de doorvoer niet gewijzigd.
> 
> 

Bij het importeren van verzamelingen toomultiple ondersteunt Hallo import-hulpprogramma hash op basis van sharding. Geef in dit scenario Hallo documenteigenschap gewenst toouse als partitiesleutel Hallo (als partitiesleutel leeg is, documenten zijn shard willekeurig in Hallo doel verzamelingen).

U kunt eventueel opgeven welk veld in de bron voor het importeren van Hallo als hello Azure Cosmos DB document-id-eigenschap moet worden gebruikt tijdens het importeren van hello (Let erop dat als documenten geen deze eigenschap bevatten, klikt u vervolgens Hallo import-hulpprogramma een GUID als de waarde van de eigenschap id Hallo genereert).

Er zijn tijdens het importeren van een aantal geavanceerde opties beschikbaar. Tijdens het Hallo-hulpprogramma omvat eerst een standaard bulkimport opgeslagen procedure (BulkInsert.js), kunt u eventueel toospecify uw eigen importprocedure opgeslagen:

 ![Schermopname van Azure Cosmos DB bulksgewijs invoegen sproc optie](./media/import-data/bulkinsertsp.png)

Bij het importeren van datum-typen (bijvoorbeeld van SQL Server of MongoDB), kunt u kunt daarnaast voor kiezen tussen de drie opties voor importeren:

 ![Schermopname van Azure Cosmos DB datum tijdopties importeren](./media/import-data/datetimeoptions.png)

* Tekenreeks: Behouden als een string-waarde
* Epoche: Behouden als een getalwaarde epoche
* Beide: Zowel tekenreeks als numerieke waarden epoche bewaard. Deze optie maakt u een subdocument, bijvoorbeeld: "date_joined": {'' waarde '': ' 2013-10-21T21:17:25.2410000Z ', ' epoche ': 1382390245}

Hello Azure Cosmos DB bulksgewijs importfunctie heeft Hallo volgende als u meer geavanceerde opties:

1. Batchgrootte: Hallo hulpprogramma standaardwaarden tooa batchgrootte van 50.  Als Hallo documenten toobe geïmporteerd groot zijn, kunt u overwegen Hallo batchgrootte te verlagen. Als u daarentegen als Hallo documenten toobe geïmporteerd klein zijn, kunt u Hallo batchgrootte verhogen.
2. Maximum aantal Script-grootte (bytes): Hallo hulpprogramma standaardinstellingen tooa script maximale grootte van 512KB
3. Schakel automatische van generatie-Id: Als elke document toobe geïmporteerd een id-veld bevat, deze optie kunt betere prestaties. Een unieke id-veld ontbreekt documenten worden niet geïmporteerd.
4. Update bestaande documenten: Hallo hulpprogramma standaardwaarden toonot bestaande documenten vervangen door een ID-conflicten. Deze optie kunt bestaande documenten met overeenkomende id overschrijven. Deze functie is handig voor geplande gegevens migraties die bijwerken van bestaande documenten.
5. Aantal nieuwe pogingen bij fouten: Hiermee geeft u het aantal keren tooretry verbinding tooAzure Cosmos DB in geval van een tijdelijke fouten (bijvoorbeeld connectiviteit onderbreking op het netwerk) Hallo Hallo.
6. Interval voor opnieuw proberen: Geeft aan hoe lang toowait tussen opnieuw uit te voeren Hallo verbinding tooAzure Cosmos DB in geval van een tijdelijke fouten (bijvoorbeeld connectiviteit onderbreking op het netwerk).
7. Verbindingsmodus: Hiermee geeft u Hallo verbinding modus toouse met Azure Cosmos DB. Hallo beschikbare opties zijn DirectTcp, DirectHttps en Gateway. Hallo rechtstreekse verbinding modi zijn sneller, terwijl Hallo gateway modus meer firewall beschrijvende aangezien hierbij alleen poort 443.

![Schermopname van Azure Cosmos DB bulkimport geavanceerde opties](./media/import-data/docdbbulkoptions.png)

> [!TIP]
> Hallo hulpprogramma standaardwaarden tooconnection modus DirectTcp voor importeren. Als u de firewall-problemen ondervindt, overschakelen tooconnection modus Gateway, omdat hiervoor alleen poort 443.
> 
> 

## <a id="DocumentDBSeqTarget"></a>tooimport toohello DocumentDB-API (sequentiële Record importeren)
Importfunctie van Hello Azure Cosmos DB sequentiële record kunt u tooimport van Hallo beschikbare bron opties op basis van door een andere record. U kunt deze optie selecteren als u de bestaande verzameling tooan heeft het quotum van opgeslagen procedures bereikt importeert. Hallo hulpprogramma ondersteunt importeren tooa enkel Azure DB die Cosmos-verzameling (één partitie en meerdere partitie), evenals shard importeren, waarbij de gegevens in Azure Cosmos DB meerdere verzamelingen voor één partitie en/of meerdere partitie zijn gepartitioneerd. Zie voor meer informatie over het partitioneren van gegevens, [partitionering en schalen in Azure Cosmos DB](partition-data.md).

![Schermopname van Azure Cosmos DB-opties voor opeenvolgende record importeren](./media/import-data/documentdbsequential.png)

Hallo-indeling van hello Azure Cosmos DB-verbindingsreeks is:

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

Hallo verbindingsreeks voor Azure DB die Cosmos-account kan worden opgehaald uit de blade van de sleutels Hallo van hello Azure-portal, zoals beschreven in [hoe toomanage een account voor Azure Cosmos DB](manage-account.md), maar de naam van de Hallo van Hallo-database toohello toobe toegevoegd moet de verbindingsreeks in Hallo volgende indeling:

    Database=<Azure Cosmos DB Database>;

> [!NOTE]
> Gebruik Hallo controleren opdracht tooensure die hello Azure DB die Cosmos-exemplaar is opgegeven in tekenreeksveld Hallo-verbinding kan worden benaderd.
> 
> 

tooimport tooa één verzameling, Voer Hallo-naam van Hallo verzameling toowhich gegevens worden geïmporteerd en klik op de knop toevoegen Hallo. tooimport toomultiple verzamelingen, de verzamelingsnaam van elke afzonderlijk Voer of gebruik Hallo syntaxis toospecify na meerdere verzamelingen: *collection_prefix*[begin index - end-index]. Houd rekening met Hallo volgende bij het opgeven van meerdere verzamelingen via de hiervoor genoemde Hallo-syntaxis:

1. Alleen geheel getal bereik bestandsnaampatronen worden ondersteund. Bijvoorbeeld, geven verzameling [0-3] produceert Hallo verzamelingen te volgen: collection0, collection1, collection2, collection3.
2. U kunt een verkorte syntaxis gebruiken: verzameling [3] wordt vermeld in stap 1 verzamelingen dezelfde set verzenden.
3. Meer dan een vervanging kan worden opgegeven. Bijvoorbeeld, verzameling [0-1] [0-9] genereert 20 verzamelingsnamen met toonaangevende nullen (collection01,... 02... 03).

Eenmaal hello verzameling namen zijn opgegeven, kiest u de gewenste doorvoer Hallo van Hallo verzameling(en) (400 RUs too250, 000 RUs). Kies een hogere doorvoer voor de beste prestaties importeren. Zie voor meer informatie over prestatieniveaus [prestatieniveaus in Azure Cosmos DB](performance-levels.md). Een toocollections met doorvoer importeren > 10.000 RUs een partitiesleutel is vereist. Als u op meer dan 250.000 RUs toohave kiest, moet u toofile een aanvraag in de portal toohave Hallo verhoogd van uw account.

> [!NOTE]
> Hallo doorvoer instelling is alleen van toepassing toocollection maken. Als Hallo collectie al bestaat opgegeven, wordt de doorvoer niet gewijzigd.
> 
> 

Bij het importeren van verzamelingen toomultiple ondersteunt Hallo import-hulpprogramma hash op basis van sharding. Geef in dit scenario Hallo documenteigenschap gewenst toouse als partitiesleutel Hallo (als partitiesleutel leeg is, documenten zijn shard willekeurig in Hallo doel verzamelingen).

U kunt eventueel opgeven welk veld in de bron voor het importeren van Hallo als hello Azure Cosmos DB document-id-eigenschap moet worden gebruikt tijdens het importeren van hello (Let erop dat als documenten geen deze eigenschap bevatten, klikt u vervolgens Hallo import-hulpprogramma een GUID als de waarde van de eigenschap id Hallo genereert).

Er zijn tijdens het importeren van een aantal geavanceerde opties beschikbaar. Eerst bij het importeren van datum-typen (bijvoorbeeld van SQL Server of MongoDB), kunt u tussen de drie opties voor importeren:

 ![Schermopname van Azure Cosmos DB datum tijdopties importeren](./media/import-data/datetimeoptions.png)

* Tekenreeks: Behouden als een string-waarde
* Epoche: Behouden als een getalwaarde epoche
* Beide: Zowel tekenreeks als numerieke waarden epoche bewaard. Deze optie maakt u een subdocument, bijvoorbeeld: "date_joined": {'' waarde '': ' 2013-10-21T21:17:25.2410000Z ', ' epoche ': 1382390245}

Hello Azure DB Cosmos - sequentiële record importfunctie heeft Hallo volgende als u meer geavanceerde opties:

1. Aantal parallelle aanvragen: Hallo hulpprogramma standaardinstellingen too2 parallelle aanvragen. Als Hallo documenten toobe geïmporteerd klein zijn, kunt u overwegen Hallo aantal parallelle aanvragen verhogen. Houd er rekening mee dat als dit nummer te veel wordt gegenereerd, Hallo importeren beperking ondervinden.
2. Schakel automatische van generatie-Id: Als elke document toobe geïmporteerd een id-veld bevat, deze optie kunt betere prestaties. Een unieke id-veld ontbreekt documenten worden niet geïmporteerd.
3. Update bestaande documenten: Hallo hulpprogramma standaardwaarden toonot bestaande documenten vervangen door een ID-conflicten. Deze optie kunt bestaande documenten met overeenkomende id overschrijven. Deze functie is handig voor geplande gegevens migraties die bijwerken van bestaande documenten.
4. Aantal nieuwe pogingen bij fouten: Hiermee geeft u het aantal keren tooretry verbinding tooAzure Cosmos DB in geval van een tijdelijke fouten (bijvoorbeeld connectiviteit onderbreking op het netwerk) Hallo Hallo.
5. Interval voor opnieuw proberen: Geeft aan hoe lang toowait tussen opnieuw uit te voeren Hallo verbinding tooAzure Cosmos DB in geval van een tijdelijke fouten (bijvoorbeeld connectiviteit onderbreking op het netwerk).
6. Verbindingsmodus: Hiermee geeft u Hallo verbinding modus toouse met Azure Cosmos DB. Hallo beschikbare opties zijn DirectTcp, DirectHttps en Gateway. Hallo rechtstreekse verbinding modi zijn sneller, terwijl Hallo gateway modus meer firewall beschrijvende aangezien hierbij alleen poort 443.

![Schermopname van Azure Cosmos DB sequentiële record importeren geavanceerde opties](./media/import-data/documentdbsequentialoptions.png)

> [!TIP]
> Hallo hulpprogramma standaardwaarden tooconnection modus DirectTcp voor importeren. Als u de firewall-problemen ondervindt, overschakelen tooconnection modus Gateway, omdat hiervoor alleen poort 443.
> 
> 

## <a id="IndexingPolicy"></a>Een indexeringsbeleid opgeven bij het maken van Azure DB die Cosmos-verzamelingen
Als u hulpprogramma toocreate verzamelingen Hallo migratie tijdens het importeren toestaat, kunt u Hallo indexeringsbeleid van Hallo verzamelingen. Navigeer in Hallo geavanceerde opties sectie van hello Azure Cosmos DB bulkimport en Azure Cosmos DB sequentiële record opties, toohello beleid Indexing-sectie.

![Schermopname van Azure Cosmos DB indexeren beleid geavanceerde opties](./media/import-data/indexingpolicy1.png)

Hallo indexeren beleid geavanceerde optie gebruikt, kunt u selecteren een bestand met beleidsregel van indexering, handmatig een indexeringsbeleid invoeren, of uit een reeks standaardsjablonen (door de rechtermuisknop te klikken in Hallo beleid textbox indexeren).

Beleidssjablonen Hallo Hallo hulpprogramma biedt zijn:

* De standaardinstelling. Dit beleid wordt aanbevolen wanneer u het uitvoeren van de gelijkheid query uitgevoerd naar tekenreeksen en ORDER BY, bereik en gelijkheid query's gebruiken voor getallen. Dit beleid heeft een lagere opslagoverhead voor indexering dan bereik.
* Het bereik. Dit beleid wordt aanbevolen u ORDER BY, bereik en gelijkheid query's op de cijfers en tekenreeksen. Dit beleid heeft een hogere opslagoverhead voor indexering dan standaard of hash-bewerking.

![Schermopname van Azure Cosmos DB indexeren beleid geavanceerde opties](./media/import-data/indexingpolicy2.png)

> [!NOTE]
> Als u een indexeringsbeleid niet opgeeft, wordt het standaardbeleid Hallo worden toegepast. Zie voor meer informatie over indexering beleid [Azure Cosmos DB indexeren beleid](indexing-policies.md).
> 
> 

## <a name="export-toojson-file"></a>TooJSON-bestand exporteren
Exportfunctie van Hello Azure Cosmos DB JSON kunt u tooexport van Hallo beschikbare bron opties tooa JSON-bestand met een matrix met JSON-documenten. Hallo-hulpprogramma wordt afgehandeld Hallo exporteren voor u of u kunt kiezen tooview Hallo resulterende migratie opdracht en voert u de opdracht Hallo zelf. Hallo resulterende JSON-bestand kan worden opgeslagen, lokaal of in Azure Blob-opslag.

![Schermopname van Azure Cosmos DB JSON-optie voor het exporteren van lokaal bestand](./media/import-data/jsontarget.png)

![Schermopname van Azure Cosmos DB JSON Azure Blob storage exportoptie](./media/import-data/jsontarget2.png)

U kunt eventueel tooprettify Hallo resulterende JSON die wordt vergroot Hallo Hallo resulterende document terwijl meer leesbaar waardoor Hallo inhoud.

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

## <a name="advanced-configuration"></a>Geavanceerde configuratie
Geef Hallo-locatie van Hallo log-bestand toowhich eventuele fouten die zijn geschreven gewenst in Hallo geavanceerde configuratie. Hallo volgens de regels van toepassing toothis pagina:

1. Als een bestandsnaam niet opgegeven is, wordt op Hallo resultatenpagina alle fouten geretourneerd.
2. Als een bestandsnaam is opgegeven zonder een map, wordt klikt u vervolgens Hallo-bestand gemaakt (of overschreven) in de huidige omgeving map Hallo.
3. Als u selecteert een bestaand bestand en vervolgens Hallo-bestand wordt overschreven, er is geen optie toevoegen.

Kies of alle toolog, kritiek, of er geen foutberichten. Ten slotte kunt u bepalen hoe vaak Hallo voor scherm overdracht bericht wordt bijgewerkt met de voortgang ervan.

    ![Screenshot of Advanced configuration screen](./media/import-data/AdvancedConfiguration.png)

## <a name="confirm-import-settings-and-view-command-line"></a>Bevestig de instellingen importeren en weergeven vanaf de opdrachtregel
1. Na het opgeven van informatie van gegevensbron, doelinformatie en geavanceerde configuratie, bekijk Hallo migratie samenvatting en, desgewenst weergeven/kopiëren Hallo resulterende migratie-opdracht (kopiëren Hallo-opdracht is nuttig tooautomate importbewerkingen):
   
    ![Schermopname van het scherm Samenvatting](./media/import-data/summary.png)
   
    ![Schermopname van het scherm Samenvatting](./media/import-data/summarycommand.png)
2. Wanneer u tevreden met de bron en doel-opties bent, klikt u op **importeren**. Hallo verstreken tijd, overgedragen aantal en foutgegevens (als u een bestandsnaam in de geavanceerde configuratie Hallo niet opgeven) wordt bijgewerkt Hallo importeren bezig is. Als u klaar is, kunt u Hallo resultaten (bijvoorbeeld toodeal met alle mislukte importeren) exporteren.
   
    ![Schermopname van Azure Cosmos DB JSON exportoptie](./media/import-data/viewresults.png)
3. U mogelijk ook een nieuwe import starten te behouden de bestaande instellingen hello (bijvoorbeeld verbinding tekenreeks informatie, de bron en doel keuze, etc.) of opnieuw instellen van alle waarden.
   
    ![Schermopname van Azure Cosmos DB JSON exportoptie](./media/import-data/newimport.png)

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt u Hallo volgende gedaan:

> [!div class="checklist"]
> * Hallo-hulpprogramma voor gegevensmigratie geïnstalleerd
> * Geïmporteerde gegevens uit verschillende gegevensbronnen
> * Geëxporteerd vanuit Azure Cosmos DB tooJSON

U kunt nu de volgende zelfstudie toohello gaan en meer informatie hoe tooquery-gegevens met behulp van Azure Cosmos DB. 

> [!div class="nextstepaction"]
>[Hoe tooquery gegevens?](../cosmos-db/tutorial-query-documentdb.md)
