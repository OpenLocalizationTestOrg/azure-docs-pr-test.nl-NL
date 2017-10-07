---
title: aaaGet de slag met Azure Table storage met .NET | Microsoft Docs
description: Gestructureerde gegevens opslaan in Hallo cloud met Azure Table storage, een NoSQL-gegevensarchief.
services: cosmos-db
documentationcenter: .net
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: fe46d883-7bed-49dd-980e-5c71df36adb3
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 04/10/2017
ms.author: mimig
ms.openlocfilehash: a3e9a4c6f6fd5e724535b86a3f99cd4c161de6de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-table-storage-using-net"></a>Aan de slag met Azure Table Storage met .NET
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

Azure Table storage is een service waarmee gestructureerde NoSQL-gegevens in de cloud hello, bieden een sleutelkenmerk opslaan met een schemaloos ontwerp worden opgeslagen. Omdat Table storage schemaloos is, is het eenvoudig tooadapt uw gegevens als Hallo van uw toepassing veranderen behoeften. Toegang tooTable opslaggegevens is snel en kostenefficiënt voor verschillende soorten toepassingen en is meestal lager goedkoper dan traditionele SQL voor vergelijkbare gegevensvolumes.

U kunt Table storage toostore flexibele gegevenssets zoals gebruikersgegevens voor webtoepassingen, adresboeken, apparaatgegevens of andere typen metagegevens die uw service nodig. U kunt een willekeurig aantal entiteiten opslaan in een tabel en een opslagaccount kan een onbeperkt aantal tabellen up toohello capaciteitslimiet van Hallo opslagaccount bevatten.

### <a name="about-this-tutorial"></a>Over deze zelfstudie
Deze zelfstudie leert u hoe toouse hello [Azure Storage-clientbibliotheek voor .NET](https://www.nuget.org/packages/WindowsAzure.Storage/) in enkele algemene scenario's voor Azure Table-opslag. Deze scenario's worden geïllustreerd met C#-voorbeelden voor het maken en verwijderen van een tabel en het invoegen, bijwerken, verwijderen en opvragen van tabelgegevens.

## <a name="prerequisites"></a>Vereisten

U moet Hallo volgende toocomplete in deze zelfstudie is:

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Azure Storage-clientbibliotheek voor .NET](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [Azure Configuration Manager voor .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* [Azure Storage-account](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a>Meer voorbeelden
Zie [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/) (Aan de slag met Azure Table Storage in .NET) voor meer voorbeelden van het gebruik van Table Storage. Hallo-voorbeeldtoepassing downloaden en uitvoeren, of blader Hallo-code op GitHub.

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a>Using-instructies toevoegen
Voeg de volgende Hallo **met** richtlijnen toohello bovenaan Hallo `Program.cs` bestand:

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Table; // Namespace for Table storage types
```

### <a name="parse-hello-connection-string"></a>Hallo-verbindingsreeks parseren
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-table-service-client"></a>Hallo tabelserviceclient maken
Hallo [CloudTableClient] [ dotnet_CloudTableClient] klasse kunt u tooretrieve tabellen en entiteiten die zijn opgeslagen in de Table storage. Hier volgt een eenrichtingssessie toocreate hello tabelserviceclient:

```csharp
// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```

U bent nu klaar toowrite-code die gegevens leest uit en schrijft tooTable opslag van gegevens.

## <a name="create-a-table"></a>Een tabel maken
Dit voorbeeld ziet u hoe toocreate een tabel als deze niet al bestaat:

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Retrieve a reference toohello table.
CloudTable table = tableClient.GetTableReference("people");

// Create hello table if it doesn't exist.
table.CreateIfNotExists();
```

## <a name="add-an-entity-tooa-table"></a>Een entiteit tooa tabel toevoegen
Entiteiten tooC #-objecten worden toegewezen met behulp van een aangepaste klasse die is afgeleid van [TableEntity][dotnet_TableEntity]. tooadd een entiteit tooa tabel, maak een klasse die eigenschappen Hallo van uw entiteit definieert. Hallo definieert volgende code een entiteitsklasse die de voornaam van de klant Hallo als Hallo rijsleutel en achternaam als partitiesleutel Hallo gebruikt. Samen een entiteit partitie en rijsleutel worden geïdentificeerd in Hallo tabel. Entiteiten met dezelfde partitiesleutel kan sneller worden opgevraagd dan entiteiten met verschillende Hallo partitie-sleutels, maar met verschillende partitiesleutels kunt grotere schaalbaarheid van parallelle bewerkingen. Entiteiten toobe opgeslagen in tabellen moet met een ondersteund type, bijvoorbeeld worden afgeleid van Hallo [TableEntity] [ dotnet_TableEntity] klasse. Entiteitseigenschappen gewenst toostore in een tabel moeten worden openbare eigenschappen van het type Hallo en ondersteunen ophalen en instellen van waarden. Ook *moet* uw entiteitstype een parameterloze constructor bevatten.

```csharp
public class CustomerEntity : TableEntity
{
    public CustomerEntity(string lastName, string firstName)
    {
        this.PartitionKey = lastName;
        this.RowKey = firstName;
    }

    public CustomerEntity() { }

    public string Email { get; set; }

    public string PhoneNumber { get; set; }
}
```

Tabelbewerkingen die betrekking hebben op entiteiten worden uitgevoerd via Hallo [CloudTable] [ dotnet_CloudTable] -object dat u eerder hebt gemaakt in het gedeelte voor Hallo 'Een tabel maken'. Hallo wordt bewerking toobe uitgevoerd vertegenwoordigd door een [TableOperation] [ dotnet_TableOperation] object. Hallo volgende codevoorbeeld toont Hallo maken van Hallo [CloudTable] [ dotnet_CloudTable] object en vervolgens een **CustomerEntity** object. tooprepare hello bewerking, een [TableOperation] [ dotnet_TableOperation] object tooinsert hello klantentiteit in Hallo-tabel is gemaakt. Ten slotte Hallo-bewerking wordt uitgevoerd door het aanroepen van [CloudTable][dotnet_CloudTable].[ Uitvoeren van][dotnet_CloudTable_Execute].

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create hello TableOperation object that inserts hello customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute hello insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a>Een batch entiteiten invoegen
U kunt in één schrijfbewerking een batch entiteiten invoegen in een tabel. Enkele aanvullende opmerkingen over batchbewerkingen:

* U kunt updates, verwijderingen en invoegingen uitvoeren in Hallo dezelfde batchbewerking single.
* Een batchbewerking kan up too100 entiteiten bevatten.
* Alle entiteiten in een batchbewerking moeten Hallo hebben dezelfde partitiesleutel.
* Het is mogelijk tooperform een query als batchbewerking uit, moet dit Hallo enige bewerking in Hallo batch.

Hallo volgende codevoorbeeld maakt twee entiteitsobjecten en voegt u elk te[TableBatchOperation] [ dotnet_TableBatchOperation] met behulp van Hallo [invoegen] [ dotnet_TableBatchOperation_Insert] methode. Vervolgens [CloudTable][dotnet_CloudTable].[ ExecuteBatch] [ dotnet_CloudTable_ExecuteBatch] tooexecute Hallo-bewerking wordt aangeroepen.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create hello batch operation.
TableBatchOperation batchOperation = new TableBatchOperation();

// Create a customer entity and add it toohello table.
CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
customer1.Email = "Jeff@contoso.com";
customer1.PhoneNumber = "425-555-0104";

// Create another customer entity and add it toohello table.
CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
customer2.Email = "Ben@contoso.com";
customer2.PhoneNumber = "425-555-0102";

// Add both customer entities toohello batch insert operation.
batchOperation.Insert(customer1);
batchOperation.Insert(customer2);

// Execute hello batch operation.
table.ExecuteBatch(batchOperation);
```

## <a name="retrieve-all-entities-in-a-partition"></a>Alle entiteiten in een partitie ophalen
een tabel voor alle entiteiten in een partitie, gebruik tooquery een [TableQuery] [ dotnet_TableQuery] object. Hallo geeft volgende codevoorbeeld een filter voor entiteiten waarbij 'Smith' hello partitiesleutel is. Dit voorbeeld wordt Hallo velden van elke entiteit in Hallo query resultaten toohello-console.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Construct hello query operation for all customer entities where PartitionKey="Smith".
TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>().Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

// Print hello fields for each customer.
foreach (CustomerEntity entity in table.ExecuteQuery(query))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

## <a name="retrieve-a-range-of-entities-in-a-partition"></a>Een bereik van entiteiten in een partitie ophalen
Als u niet tooquery alle entiteiten in een partitie wilt, kunt u een bereik opgeven door een combinatie van Hallo partitie sleutel filter met een rijsleutelfilter. Hallo volgende codevoorbeeld maakt gebruik van twee filters tooget alle entiteiten in de partitie 'Smith' waar Hallo rijsleutel (voornaam) begint met een letter voordat 'E' in hello alfabet en wordt vervolgens Hallo queryresultaten.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create hello table query.
TableQuery<CustomerEntity> rangeQuery = new TableQuery<CustomerEntity>().Where(
    TableQuery.CombineFilters(
        TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"),
        TableOperators.And,
        TableQuery.GenerateFilterCondition("RowKey", QueryComparisons.LessThan, "E")));

// Loop through hello results, displaying information about hello entity.
foreach (CustomerEntity entity in table.ExecuteQuery(rangeQuery))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

## <a name="retrieve-a-single-entity"></a>Eén entiteit ophalen
U kunt een query tooretrieve één specifieke entiteit schrijven. Hallo volgende code gebruikt [TableOperation] [ dotnet_TableOperation] toospecify Hallo klant 'Ben Smith'. Deze methode retourneert één entiteit in plaats van een verzameling en Hallo geretourneerd waarde in [TableResult][dotnet_TableResult].[ Resultaat] [ dotnet_TableResult_Result] is een **CustomerEntity** object. Het opgeven van de partitie-als rijsleutels in een query is Hallo snelste manier tooretrieve uit de tabelservice Hallo één entiteit.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Print hello phone number of hello result.
if (retrievedResult.Result != null)
{
    Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
}
else
{
    Console.WriteLine("hello phone number could not be retrieved.");
}
```

## <a name="replace-an-entity"></a>Een entiteit vervangen
tooupdate een entiteit ophalen uit de tabelservice hello, Hallo entiteitsobject wijzigen en vervolgens weer toohello tabelservice Hallo wijzigingen opslaan. Hallo wijzigt volgende code het telefoonnummer van een bestaande klant. In plaats van [Insert][dotnet_TableOperation_Insert] aan te roepen, gebruikt deze code [Replace][dotnet_TableOperation_Replace]. [Vervang] [ dotnet_TableOperation_Replace] oorzaken Hallo entiteit toobe volledig vervangen op Hallo van server, tenzij het Hallo-entiteit op Hallo-server is gewijzigd sinds het is opgehaald, in welk geval Hallo-bewerking mislukt. Hiermee wordt de toepassing per ongeluk een wijziging overschrijft aangebracht tussen Hallo ophalen en bijwerken door een ander onderdeel van uw toepassing tooprevent. Hallo correcte verwerking van deze fout is tooretrieve Hallo entiteit opnieuw, breng uw wijzigingen (indien nog geldig) en voert u een andere [vervangen] [ dotnet_TableOperation_Replace] bewerking. Hallo volgende sectie wordt uitgelegd hoe u toooverride dit gedrag.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Assign hello result tooa CustomerEntity object.
CustomerEntity updateEntity = (CustomerEntity)retrievedResult.Result;

if (updateEntity != null)
{
    // Change hello phone number.
    updateEntity.PhoneNumber = "425-555-0105";

    // Create hello Replace TableOperation.
    TableOperation updateOperation = TableOperation.Replace(updateEntity);

    // Execute hello operation.
    table.Execute(updateOperation);

    Console.WriteLine("Entity updated.");
}
else
{
    Console.WriteLine("Entity could not be retrieved.");
}
```

## <a name="insert-or-replace-an-entity"></a>Een entiteit invoegen of vervangen
[Vervang] [ dotnet_TableOperation_Replace] bewerkingen mislukken als Hallo entiteit is gewijzigd sinds het ophalen van Hallo-server. Bovendien moet u ophalen Hallo entiteit van de server Hallo eerst om Hallo [vervangen] [ dotnet_TableOperation_Replace] bewerking toobe geslaagd. Soms echter weet u niet of het Hallo entiteit op Hallo-server bestaat en Hallo van de huidige waarden die erin niet relevant zijn. Met uw update worden deze allemaal overschreven. tooaccomplish, gebruikt u een [InsertOrReplace] [ dotnet_TableOperation_InsertOrReplace] bewerking. Deze bewerking wordt Hallo entiteit ingevoegd als deze niet bestaat of vervangen als het geval is, ongeacht wanneer de laatste update Hallo is uitgevoerd.

In de Hallo volgende codevoorbeeld, wordt een klantentiteit voor 'Fred Jones' gemaakt en ingevoegd in Hallo 'gebruikers' tabel. Vervolgens gebruiken we Hallo [InsertOrReplace] [ dotnet_TableOperation_InsertOrReplace] bewerking toosave een entity met Hallo dezelfde partitiesleutel (Jones) en rij sleutel (Fred) toohello server, ditmaal met een andere waarde voor Hallo telefoonnummer de eigenschap. Omdat we [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] hebben gebruikt, worden alle bijbehorende eigenschapswaarden vervangen. Echter, als een entiteit 'Fred Jones' al in tabel hello bestaat hadn't, deze zou zijn ingevoegd.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a customer entity.
CustomerEntity customer3 = new CustomerEntity("Jones", "Fred");
customer3.Email = "Fred@contoso.com";
customer3.PhoneNumber = "425-555-0106";

// Create hello TableOperation object that inserts hello customer entity.
TableOperation insertOperation = TableOperation.Insert(customer3);

// Execute hello operation.
table.Execute(insertOperation);

// Create another customer entity with hello same partition key and row key.
// We've already created a 'Fred Jones' entity and saved it toothe
// 'people' table, but here we're specifying a different value for the
// PhoneNumber property.
CustomerEntity customer4 = new CustomerEntity("Jones", "Fred");
customer4.Email = "Fred@contoso.com";
customer4.PhoneNumber = "425-555-0107";

// Create hello InsertOrReplace TableOperation.
TableOperation insertOrReplaceOperation = TableOperation.InsertOrReplace(customer4);

// Execute hello operation. Because a 'Fred Jones' entity already exists in the
// 'people' table, its property values will be overwritten by those in this
// CustomerEntity. If 'Fred Jones' didn't already exist, hello entity would be
// added toohello table.
table.Execute(insertOrReplaceOperation);
```

## <a name="query-a-subset-of-entity-properties"></a>Een query uitvoeren op een subset van entiteitseigenschappen
Een tabelquery haalt u slechts enkele eigenschappen van een entiteit in plaats van alle Hallo entiteitseigenschappen. Deze methode, projectie genoemd, verbruikt minder bandbreedte en kan de queryprestaties verbeteren, vooral bij grote entiteiten. Hallo-query in de volgende code Hallo retourneert alleen Hallo e-mailadressen van entiteiten in Hallo tabel. Dit wordt gedaan via een [DynamicTableEntity][dotnet_DynamicTableEntity]- en een [EntityResolver][dotnet_EntityResolver]-query. U kunt meer informatie over projectie in Hallo [blogbericht introductie tot Upsert en Query projectie blogbericht][blog_post_upsert]. Projectie wordt niet ondersteund door de opslagemulator hello, zodat deze code wordt alleen uitgevoerd als u een account in de tabelservice Hallo.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Define hello query, and select only hello Email property.
TableQuery<DynamicTableEntity> projectionQuery = new TableQuery<DynamicTableEntity>().Select(new string[] { "Email" });

// Define an entity resolver toowork with hello entity after retrieval.
EntityResolver<string> resolver = (pk, rk, ts, props, etag) => props.ContainsKey("Email") ? props["Email"].StringValue : null;

foreach (string projectedEmail in table.ExecuteQuery(projectionQuery, resolver, null, null))
{
    Console.WriteLine(projectedEmail);
}
```

## <a name="delete-an-entity"></a>Een entiteit verwijderen
U kunt een entiteit gemakkelijk verwijderen nadat u deze hebt opgehaald met behulp van Hallo hetzelfde patroon weergegeven voor het bijwerken van een entiteit. Hallo na de code opgehaald en wordt een klantentiteit verwijderd.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that expects a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Assign hello result tooa CustomerEntity.
CustomerEntity deleteEntity = (CustomerEntity)retrievedResult.Result;

// Create hello Delete TableOperation.
if (deleteEntity != null)
{
    TableOperation deleteOperation = TableOperation.Delete(deleteEntity);

    // Execute hello operation.
    table.Execute(deleteOperation);

    Console.WriteLine("Entity deleted.");
}
else
{
    Console.WriteLine("Could not retrieve hello entity.");
}
```

## <a name="delete-a-table"></a>Een tabel verwijderen
Ten slotte verwijdert Hallo volgende codevoorbeeld een tabel uit een opslagaccount. Een tabel die is verwijderd is niet beschikbaar toobe opnieuw worden gemaakt voor een bepaalde tijd na Hallo verwijderen.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Delete hello table it if exists.
table.DeleteIfExists();
```

## <a name="retrieve-entities-in-pages-asynchronously"></a>Entiteiten asynchroon ophalen op pagina's
Als u een groot aantal entiteiten leest en entiteiten tooprocess/weergeven gewenste terwijl ze worden opgehaald in plaats van wachten tot ze alle tooreturn, kunt u entiteiten ophalen met behulp van een gesegmenteerde query. Dit voorbeeld toont hoe tooreturn resultaten op pagina's met behulp van Hallo Async-Await-patroon, zodat de uitvoering niet wordt geblokkeerd terwijl u wacht voor een groot aantal resultaten tooreturn. Zie voor meer informatie over het gebruik van hello Async-Await-patroon in .NET, [asynchrone programmering met Async en Await (C# en Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx).

```csharp
// Initialize a default TableQuery tooretrieve all hello entities in hello table.
TableQuery<CustomerEntity> tableQuery = new TableQuery<CustomerEntity>();

// Initialize hello continuation token toonull toostart from hello beginning of hello table.
TableContinuationToken continuationToken = null;

do
{
    // Retrieve a segment (up too1,000 entities).
    TableQuerySegment<CustomerEntity> tableQueryResult =
        await table.ExecuteQuerySegmentedAsync(tableQuery, continuationToken);

    // Assign hello new continuation token tootell hello service where to
    // continue on hello next iteration (or null if it has reached hello end).
    continuationToken = tableQueryResult.ContinuationToken;

    // Print hello number of rows retrieved.
    Console.WriteLine("Rows retrieved {0}", tableQueryResult.Results.Count);

// Loop until a null continuation token is received, indicating hello end of hello table.
} while(continuationToken != null);
```

## <a name="next-steps"></a>Volgende stappen
Nu u Hallo basisprincipes van Table storage hebt geleerd, volgt u deze koppelingen toolearn over complexere opslagtaken:

* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is een gratis, zelfstandige app van Microsoft waarmee u toowork visueel met Azure Storage-gegevens op Windows-, Mac OS- en Linux.
* Zie [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/) (Aan de slag met Azure Table Storage in .NET) voor meer voorbeelden van Table Storage.
* Hallo tabel-service-naslagdocumentatie voor volledige informatie over beschikbare API's bekijken:
* [Naslaginformatie over de Storage-clientbibliotheek voor .NET](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
* [Naslaginformatie over de REST-API](http://msdn.microsoft.com/library/azure/dd179355)
* Meer informatie over hoe u toosimplify Hallo code schrijft toowork met Azure Storage met behulp van Hallo [Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)
* Bekijk meer functie handleidingen toolearn over aanvullende mogelijkheden voor het opslaan van gegevens in Azure.
* [Aan de slag met Azure Blob storage met .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) toostore ongestructureerde gegevens.
* [Verbinding maken met tooSQL Database met behulp van .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md) toostore relationele gegevens.

[Download and install hello Azure SDK for .NET]: /develop/net/
[Creating an Azure Project in Visual Studio]: http://msdn.microsoft.com/library/azure/ee405487.aspx

[blog_post_upsert]: http://blogs.msdn.com/b/windowsazurestorage/archive/2011/09/15/windows-azure-tables-introducing-upsert-and-query-projection.aspx

[dotnet_api_ref]: https://msdn.microsoft.com/library/azure/mt347887.aspx
[dotnet_CloudTableClient]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.cloudtableclient.aspx
[dotnet_CloudTable]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.cloudtable.aspx
[dotnet_CloudTable_Execute]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.cloudtable.execute.aspx
[dotnet_CloudTable_ExecuteBatch]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.cloudtable.executebatch.aspx
[dotnet_DynamicTableEntity]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.dynamictableentity.aspx
[dotnet_EntityResolver]: https://msdn.microsoft.com/library/jj733144.aspx
[dotnet_TableBatchOperation]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tablebatchoperation.aspx
[dotnet_TableBatchOperation_Insert]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tablebatchoperation.insert.aspx
[dotnet_TableEntity]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableentity.aspx
[dotnet_TableOperation]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableoperation.aspx
[dotnet_TableOperation_Insert]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableoperation.insert.aspx
[dotnet_TableOperation_InsertOrReplace]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableoperation.insertorreplace.aspx
[dotnet_TableOperation_Replace]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableoperation.replace.aspx
[dotnet_TableQuery]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tablequery.aspx
[dotnet_TableResult]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableresult.aspx
[dotnet_TableResult_Result]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableresult.result.aspx
