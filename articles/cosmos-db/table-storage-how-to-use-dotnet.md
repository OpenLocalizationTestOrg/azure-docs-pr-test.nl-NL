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
# <a name="get-started-with-azure-table-storage-using-net"></a><span data-ttu-id="9ed0d-103">Aan de slag met Azure Table Storage met .NET</span><span class="sxs-lookup"><span data-stu-id="9ed0d-103">Get started with Azure Table storage using .NET</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

<span data-ttu-id="9ed0d-104">Azure Table storage is een service waarmee gestructureerde NoSQL-gegevens in de cloud hello, bieden een sleutelkenmerk opslaan met een schemaloos ontwerp worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-104">Azure Table storage is a service that stores structured NoSQL data in hello cloud, providing a key/attribute store with a schemaless design.</span></span> <span data-ttu-id="9ed0d-105">Omdat Table storage schemaloos is, is het eenvoudig tooadapt uw gegevens als Hallo van uw toepassing veranderen behoeften.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-105">Because Table storage is schemaless, it's easy tooadapt your data as hello needs of your application evolve.</span></span> <span data-ttu-id="9ed0d-106">Toegang tooTable opslaggegevens is snel en kostenefficiënt voor verschillende soorten toepassingen en is meestal lager goedkoper dan traditionele SQL voor vergelijkbare gegevensvolumes.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-106">Access tooTable storage data is fast and cost-effective for many types of applications, and is typically lower in cost than traditional SQL for similar volumes of data.</span></span>

<span data-ttu-id="9ed0d-107">U kunt Table storage toostore flexibele gegevenssets zoals gebruikersgegevens voor webtoepassingen, adresboeken, apparaatgegevens of andere typen metagegevens die uw service nodig.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-107">You can use Table storage toostore flexible datasets like user data for web applications, address books, device information, or other types of metadata your service requires.</span></span> <span data-ttu-id="9ed0d-108">U kunt een willekeurig aantal entiteiten opslaan in een tabel en een opslagaccount kan een onbeperkt aantal tabellen up toohello capaciteitslimiet van Hallo opslagaccount bevatten.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-108">You can store any number of entities in a table, and a storage account may contain any number of tables, up toohello capacity limit of hello storage account.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="9ed0d-109">Over deze zelfstudie</span><span class="sxs-lookup"><span data-stu-id="9ed0d-109">About this tutorial</span></span>
<span data-ttu-id="9ed0d-110">Deze zelfstudie leert u hoe toouse hello [Azure Storage-clientbibliotheek voor .NET](https://www.nuget.org/packages/WindowsAzure.Storage/) in enkele algemene scenario's voor Azure Table-opslag.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-110">This tutorial shows you how toouse hello [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/) in some common Azure Table storage scenarios.</span></span> <span data-ttu-id="9ed0d-111">Deze scenario's worden geïllustreerd met C#-voorbeelden voor het maken en verwijderen van een tabel en het invoegen, bijwerken, verwijderen en opvragen van tabelgegevens.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-111">These scenarios are presented using C# examples for creating and deleting a table, and inserting, updating, deleting, and querying table data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9ed0d-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="9ed0d-112">Prerequisites</span></span>

<span data-ttu-id="9ed0d-113">U moet Hallo volgende toocomplete in deze zelfstudie is:</span><span class="sxs-lookup"><span data-stu-id="9ed0d-113">You need hello following toocomplete this tutorial successfully:</span></span>

* [<span data-ttu-id="9ed0d-114">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9ed0d-114">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="9ed0d-115">Azure Storage-clientbibliotheek voor .NET</span><span class="sxs-lookup"><span data-stu-id="9ed0d-115">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="9ed0d-116">Azure Configuration Manager voor .NET</span><span class="sxs-lookup"><span data-stu-id="9ed0d-116">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* [<span data-ttu-id="9ed0d-117">Azure Storage-account</span><span class="sxs-lookup"><span data-stu-id="9ed0d-117">Azure storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a><span data-ttu-id="9ed0d-118">Meer voorbeelden</span><span class="sxs-lookup"><span data-stu-id="9ed0d-118">More samples</span></span>
<span data-ttu-id="9ed0d-119">Zie [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/) (Aan de slag met Azure Table Storage in .NET) voor meer voorbeelden van het gebruik van Table Storage.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-119">For additional examples using Table storage, see [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/).</span></span> <span data-ttu-id="9ed0d-120">Hallo-voorbeeldtoepassing downloaden en uitvoeren, of blader Hallo-code op GitHub.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-120">You can download hello sample application and run it, or browse hello code on GitHub.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="9ed0d-121">Using-instructies toevoegen</span><span class="sxs-lookup"><span data-stu-id="9ed0d-121">Add using directives</span></span>
<span data-ttu-id="9ed0d-122">Voeg de volgende Hallo **met** richtlijnen toohello bovenaan Hallo `Program.cs` bestand:</span><span class="sxs-lookup"><span data-stu-id="9ed0d-122">Add hello following **using** directives toohello top of hello `Program.cs` file:</span></span>

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Table; // Namespace for Table storage types
```

### <a name="parse-hello-connection-string"></a><span data-ttu-id="9ed0d-123">Hallo-verbindingsreeks parseren</span><span class="sxs-lookup"><span data-stu-id="9ed0d-123">Parse hello connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-table-service-client"></a><span data-ttu-id="9ed0d-124">Hallo tabelserviceclient maken</span><span class="sxs-lookup"><span data-stu-id="9ed0d-124">Create hello Table service client</span></span>
<span data-ttu-id="9ed0d-125">Hallo [CloudTableClient] [ dotnet_CloudTableClient] klasse kunt u tooretrieve tabellen en entiteiten die zijn opgeslagen in de Table storage.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-125">hello [CloudTableClient][dotnet_CloudTableClient] class enables you tooretrieve tables and entities stored in Table storage.</span></span> <span data-ttu-id="9ed0d-126">Hier volgt een eenrichtingssessie toocreate hello tabelserviceclient:</span><span class="sxs-lookup"><span data-stu-id="9ed0d-126">Here's one way toocreate hello Table service client:</span></span>

```csharp
// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```

<span data-ttu-id="9ed0d-127">U bent nu klaar toowrite-code die gegevens leest uit en schrijft tooTable opslag van gegevens.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-127">Now you are ready toowrite code that reads data from and writes data tooTable storage.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="9ed0d-128">Een tabel maken</span><span class="sxs-lookup"><span data-stu-id="9ed0d-128">Create a table</span></span>
<span data-ttu-id="9ed0d-129">Dit voorbeeld ziet u hoe toocreate een tabel als deze niet al bestaat:</span><span class="sxs-lookup"><span data-stu-id="9ed0d-129">This example shows how toocreate a table if it does not already exist:</span></span>

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

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="9ed0d-130">Een entiteit tooa tabel toevoegen</span><span class="sxs-lookup"><span data-stu-id="9ed0d-130">Add an entity tooa table</span></span>
<span data-ttu-id="9ed0d-131">Entiteiten tooC #-objecten worden toegewezen met behulp van een aangepaste klasse die is afgeleid van [TableEntity][dotnet_TableEntity].</span><span class="sxs-lookup"><span data-stu-id="9ed0d-131">Entities map tooC# objects by using a custom class derived from [TableEntity][dotnet_TableEntity].</span></span> <span data-ttu-id="9ed0d-132">tooadd een entiteit tooa tabel, maak een klasse die eigenschappen Hallo van uw entiteit definieert.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-132">tooadd an entity tooa table, create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="9ed0d-133">Hallo definieert volgende code een entiteitsklasse die de voornaam van de klant Hallo als Hallo rijsleutel en achternaam als partitiesleutel Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-133">hello following code defines an entity class that uses hello customer's first name as hello row key and last name as hello partition key.</span></span> <span data-ttu-id="9ed0d-134">Samen een entiteit partitie en rijsleutel worden geïdentificeerd in Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-134">Together, an entity's partition and row key uniquely identify it in hello table.</span></span> <span data-ttu-id="9ed0d-135">Entiteiten met dezelfde partitiesleutel kan sneller worden opgevraagd dan entiteiten met verschillende Hallo partitie-sleutels, maar met verschillende partitiesleutels kunt grotere schaalbaarheid van parallelle bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-135">Entities with hello same partition key can be queried faster than entities with different partition keys, but using diverse partition keys allows for greater scalability of parallel operations.</span></span> <span data-ttu-id="9ed0d-136">Entiteiten toobe opgeslagen in tabellen moet met een ondersteund type, bijvoorbeeld worden afgeleid van Hallo [TableEntity] [ dotnet_TableEntity] klasse.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-136">Entities toobe stored in tables must be of a supported type, for example derived from hello [TableEntity][dotnet_TableEntity] class.</span></span> <span data-ttu-id="9ed0d-137">Entiteitseigenschappen gewenst toostore in een tabel moeten worden openbare eigenschappen van het type Hallo en ondersteunen ophalen en instellen van waarden.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-137">Entity properties you'd like toostore in a table must be public properties of hello type, and support both getting and setting of values.</span></span> <span data-ttu-id="9ed0d-138">Ook *moet* uw entiteitstype een parameterloze constructor bevatten.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-138">Also, your entity type *must* expose a parameter-less constructor.</span></span>

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

<span data-ttu-id="9ed0d-139">Tabelbewerkingen die betrekking hebben op entiteiten worden uitgevoerd via Hallo [CloudTable] [ dotnet_CloudTable] -object dat u eerder hebt gemaakt in het gedeelte voor Hallo 'Een tabel maken'.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-139">Table operations that involve entities are performed via hello [CloudTable][dotnet_CloudTable] object that you created earlier in hello "Create a table" section.</span></span> <span data-ttu-id="9ed0d-140">Hallo wordt bewerking toobe uitgevoerd vertegenwoordigd door een [TableOperation] [ dotnet_TableOperation] object.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-140">hello operation toobe performed is represented by a [TableOperation][dotnet_TableOperation] object.</span></span> <span data-ttu-id="9ed0d-141">Hallo volgende codevoorbeeld toont Hallo maken van Hallo [CloudTable] [ dotnet_CloudTable] object en vervolgens een **CustomerEntity** object.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-141">hello following code example shows hello creation of hello [CloudTable][dotnet_CloudTable] object and then a **CustomerEntity** object.</span></span> <span data-ttu-id="9ed0d-142">tooprepare hello bewerking, een [TableOperation] [ dotnet_TableOperation] object tooinsert hello klantentiteit in Hallo-tabel is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-142">tooprepare hello operation, a [TableOperation][dotnet_TableOperation] object is created tooinsert hello customer entity into hello table.</span></span> <span data-ttu-id="9ed0d-143">Ten slotte Hallo-bewerking wordt uitgevoerd door het aanroepen van [CloudTable][dotnet_CloudTable].[ Uitvoeren van][dotnet_CloudTable_Execute].</span><span class="sxs-lookup"><span data-stu-id="9ed0d-143">Finally, hello operation is executed by calling [CloudTable][dotnet_CloudTable].[Execute][dotnet_CloudTable_Execute].</span></span>

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

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="9ed0d-144">Een batch entiteiten invoegen</span><span class="sxs-lookup"><span data-stu-id="9ed0d-144">Insert a batch of entities</span></span>
<span data-ttu-id="9ed0d-145">U kunt in één schrijfbewerking een batch entiteiten invoegen in een tabel.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-145">You can insert a batch of entities into a table in one write operation.</span></span> <span data-ttu-id="9ed0d-146">Enkele aanvullende opmerkingen over batchbewerkingen:</span><span class="sxs-lookup"><span data-stu-id="9ed0d-146">Some other notes on batch operations:</span></span>

* <span data-ttu-id="9ed0d-147">U kunt updates, verwijderingen en invoegingen uitvoeren in Hallo dezelfde batchbewerking single.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-147">You can perform updates, deletes, and inserts in hello same single batch operation.</span></span>
* <span data-ttu-id="9ed0d-148">Een batchbewerking kan up too100 entiteiten bevatten.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-148">A single batch operation can include up too100 entities.</span></span>
* <span data-ttu-id="9ed0d-149">Alle entiteiten in een batchbewerking moeten Hallo hebben dezelfde partitiesleutel.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-149">All entities in a single batch operation must have hello same partition key.</span></span>
* <span data-ttu-id="9ed0d-150">Het is mogelijk tooperform een query als batchbewerking uit, moet dit Hallo enige bewerking in Hallo batch.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-150">While it is possible tooperform a query as a batch operation, it must be hello only operation in hello batch.</span></span>

<span data-ttu-id="9ed0d-151">Hallo volgende codevoorbeeld maakt twee entiteitsobjecten en voegt u elk te[TableBatchOperation] [ dotnet_TableBatchOperation] met behulp van Hallo [invoegen] [ dotnet_TableBatchOperation_Insert] methode.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-151">hello following code example creates two entity objects and adds each too[TableBatchOperation][dotnet_TableBatchOperation] by using hello [Insert][dotnet_TableBatchOperation_Insert] method.</span></span> <span data-ttu-id="9ed0d-152">Vervolgens [CloudTable][dotnet_CloudTable].[ ExecuteBatch] [ dotnet_CloudTable_ExecuteBatch] tooexecute Hallo-bewerking wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-152">Then, [CloudTable][dotnet_CloudTable].[ExecuteBatch][dotnet_CloudTable_ExecuteBatch] is called tooexecute hello operation.</span></span>

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

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="9ed0d-153">Alle entiteiten in een partitie ophalen</span><span class="sxs-lookup"><span data-stu-id="9ed0d-153">Retrieve all entities in a partition</span></span>
<span data-ttu-id="9ed0d-154">een tabel voor alle entiteiten in een partitie, gebruik tooquery een [TableQuery] [ dotnet_TableQuery] object.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-154">tooquery a table for all entities in a partition, use a [TableQuery][dotnet_TableQuery] object.</span></span> <span data-ttu-id="9ed0d-155">Hallo geeft volgende codevoorbeeld een filter voor entiteiten waarbij 'Smith' hello partitiesleutel is.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-155">hello following code example specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="9ed0d-156">Dit voorbeeld wordt Hallo velden van elke entiteit in Hallo query resultaten toohello-console.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-156">This example prints hello fields of each entity in hello query results toohello console.</span></span>

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

## <a name="retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="9ed0d-157">Een bereik van entiteiten in een partitie ophalen</span><span class="sxs-lookup"><span data-stu-id="9ed0d-157">Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="9ed0d-158">Als u niet tooquery alle entiteiten in een partitie wilt, kunt u een bereik opgeven door een combinatie van Hallo partitie sleutel filter met een rijsleutelfilter.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-158">If you don't want tooquery all entities in a partition, you can specify a range by combining hello partition key filter with a row key filter.</span></span> <span data-ttu-id="9ed0d-159">Hallo volgende codevoorbeeld maakt gebruik van twee filters tooget alle entiteiten in de partitie 'Smith' waar Hallo rijsleutel (voornaam) begint met een letter voordat 'E' in hello alfabet en wordt vervolgens Hallo queryresultaten.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-159">hello following code example uses two filters tooget all entities in partition 'Smith' where hello row key (first name) starts with a letter before 'E' in hello alphabet, then prints hello query results.</span></span>

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

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="9ed0d-160">Eén entiteit ophalen</span><span class="sxs-lookup"><span data-stu-id="9ed0d-160">Retrieve a single entity</span></span>
<span data-ttu-id="9ed0d-161">U kunt een query tooretrieve één specifieke entiteit schrijven.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-161">You can write a query tooretrieve a single, specific entity.</span></span> <span data-ttu-id="9ed0d-162">Hallo volgende code gebruikt [TableOperation] [ dotnet_TableOperation] toospecify Hallo klant 'Ben Smith'.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-162">hello following code uses [TableOperation][dotnet_TableOperation] toospecify hello customer 'Ben Smith'.</span></span> <span data-ttu-id="9ed0d-163">Deze methode retourneert één entiteit in plaats van een verzameling en Hallo geretourneerd waarde in [TableResult][dotnet_TableResult].[ Resultaat] [ dotnet_TableResult_Result] is een **CustomerEntity** object.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-163">This method returns just one entity rather than a collection, and hello returned value in [TableResult][dotnet_TableResult].[Result][dotnet_TableResult_Result] is a **CustomerEntity** object.</span></span> <span data-ttu-id="9ed0d-164">Het opgeven van de partitie-als rijsleutels in een query is Hallo snelste manier tooretrieve uit de tabelservice Hallo één entiteit.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-164">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello Table service.</span></span>

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

## <a name="replace-an-entity"></a><span data-ttu-id="9ed0d-165">Een entiteit vervangen</span><span class="sxs-lookup"><span data-stu-id="9ed0d-165">Replace an entity</span></span>
<span data-ttu-id="9ed0d-166">tooupdate een entiteit ophalen uit de tabelservice hello, Hallo entiteitsobject wijzigen en vervolgens weer toohello tabelservice Hallo wijzigingen opslaan.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-166">tooupdate an entity, retrieve it from hello Table service, modify hello entity object, and then save hello changes back toohello Table service.</span></span> <span data-ttu-id="9ed0d-167">Hallo wijzigt volgende code het telefoonnummer van een bestaande klant.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-167">hello following code changes an existing customer's phone number.</span></span> <span data-ttu-id="9ed0d-168">In plaats van [Insert][dotnet_TableOperation_Insert] aan te roepen, gebruikt deze code [Replace][dotnet_TableOperation_Replace].</span><span class="sxs-lookup"><span data-stu-id="9ed0d-168">Instead of calling [Insert][dotnet_TableOperation_Insert], this code uses [Replace][dotnet_TableOperation_Replace].</span></span> <span data-ttu-id="9ed0d-169">[Vervang] [ dotnet_TableOperation_Replace] oorzaken Hallo entiteit toobe volledig vervangen op Hallo van server, tenzij het Hallo-entiteit op Hallo-server is gewijzigd sinds het is opgehaald, in welk geval Hallo-bewerking mislukt.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-169">[Replace][dotnet_TableOperation_Replace] causes hello entity toobe fully replaced on hello server, unless hello entity on hello server has changed since it was retrieved, in which case hello operation will fail.</span></span> <span data-ttu-id="9ed0d-170">Hiermee wordt de toepassing per ongeluk een wijziging overschrijft aangebracht tussen Hallo ophalen en bijwerken door een ander onderdeel van uw toepassing tooprevent.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-170">This failure is tooprevent your application from inadvertently overwriting a change made between hello retrieval and update by another component of your application.</span></span> <span data-ttu-id="9ed0d-171">Hallo correcte verwerking van deze fout is tooretrieve Hallo entiteit opnieuw, breng uw wijzigingen (indien nog geldig) en voert u een andere [vervangen] [ dotnet_TableOperation_Replace] bewerking.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-171">hello proper handling of this failure is tooretrieve hello entity again, make your changes (if still valid), and then perform another [Replace][dotnet_TableOperation_Replace] operation.</span></span> <span data-ttu-id="9ed0d-172">Hallo volgende sectie wordt uitgelegd hoe u toooverride dit gedrag.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-172">hello next section will show you how toooverride this behavior.</span></span>

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

## <a name="insert-or-replace-an-entity"></a><span data-ttu-id="9ed0d-173">Een entiteit invoegen of vervangen</span><span class="sxs-lookup"><span data-stu-id="9ed0d-173">Insert-or-replace an entity</span></span>
<span data-ttu-id="9ed0d-174">[Vervang] [ dotnet_TableOperation_Replace] bewerkingen mislukken als Hallo entiteit is gewijzigd sinds het ophalen van Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-174">[Replace][dotnet_TableOperation_Replace] operations will fail if hello entity has been changed since it was retrieved from hello server.</span></span> <span data-ttu-id="9ed0d-175">Bovendien moet u ophalen Hallo entiteit van de server Hallo eerst om Hallo [vervangen] [ dotnet_TableOperation_Replace] bewerking toobe geslaagd.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-175">Furthermore, you must retrieve hello entity from hello server first in order for hello [Replace][dotnet_TableOperation_Replace] operation toobe successful.</span></span> <span data-ttu-id="9ed0d-176">Soms echter weet u niet of het Hallo entiteit op Hallo-server bestaat en Hallo van de huidige waarden die erin niet relevant zijn.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-176">Sometimes, however, you don't know if hello entity exists on hello server and hello current values stored in it are irrelevant.</span></span> <span data-ttu-id="9ed0d-177">Met uw update worden deze allemaal overschreven.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-177">Your update should overwrite them all.</span></span> <span data-ttu-id="9ed0d-178">tooaccomplish, gebruikt u een [InsertOrReplace] [ dotnet_TableOperation_InsertOrReplace] bewerking.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-178">tooaccomplish this, you would use an [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] operation.</span></span> <span data-ttu-id="9ed0d-179">Deze bewerking wordt Hallo entiteit ingevoegd als deze niet bestaat of vervangen als het geval is, ongeacht wanneer de laatste update Hallo is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-179">This operation inserts hello entity if it doesn't exist, or replaces it if it does, regardless of when hello last update was made.</span></span>

<span data-ttu-id="9ed0d-180">In de Hallo volgende codevoorbeeld, wordt een klantentiteit voor 'Fred Jones' gemaakt en ingevoegd in Hallo 'gebruikers' tabel.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-180">In hello following code example, a customer entity for 'Fred Jones' is created and inserted into hello 'people' table.</span></span> <span data-ttu-id="9ed0d-181">Vervolgens gebruiken we Hallo [InsertOrReplace] [ dotnet_TableOperation_InsertOrReplace] bewerking toosave een entity met Hallo dezelfde partitiesleutel (Jones) en rij sleutel (Fred) toohello server, ditmaal met een andere waarde voor Hallo telefoonnummer de eigenschap.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-181">Next, we use hello [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] operation toosave an entity with hello same partition key (Jones) and row key (Fred) toohello server, this time with a different value for hello PhoneNumber property.</span></span> <span data-ttu-id="9ed0d-182">Omdat we [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] hebben gebruikt, worden alle bijbehorende eigenschapswaarden vervangen.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-182">Because we use [InsertOrReplace][dotnet_TableOperation_InsertOrReplace], all of its property values are replaced.</span></span> <span data-ttu-id="9ed0d-183">Echter, als een entiteit 'Fred Jones' al in tabel hello bestaat hadn't, deze zou zijn ingevoegd.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-183">However, if a 'Fred Jones' entity hadn't already existed in hello table, it would have been inserted.</span></span>

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

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="9ed0d-184">Een query uitvoeren op een subset van entiteitseigenschappen</span><span class="sxs-lookup"><span data-stu-id="9ed0d-184">Query a subset of entity properties</span></span>
<span data-ttu-id="9ed0d-185">Een tabelquery haalt u slechts enkele eigenschappen van een entiteit in plaats van alle Hallo entiteitseigenschappen.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-185">A table query can retrieve just a few properties from an entity instead of all hello entity properties.</span></span> <span data-ttu-id="9ed0d-186">Deze methode, projectie genoemd, verbruikt minder bandbreedte en kan de queryprestaties verbeteren, vooral bij grote entiteiten.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-186">This technique, called projection, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="9ed0d-187">Hallo-query in de volgende code Hallo retourneert alleen Hallo e-mailadressen van entiteiten in Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-187">hello query in hello following code returns only hello email addresses of entities in hello table.</span></span> <span data-ttu-id="9ed0d-188">Dit wordt gedaan via een [DynamicTableEntity][dotnet_DynamicTableEntity]- en een [EntityResolver][dotnet_EntityResolver]-query.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-188">This is done by using a query of [DynamicTableEntity][dotnet_DynamicTableEntity] and also [EntityResolver][dotnet_EntityResolver].</span></span> <span data-ttu-id="9ed0d-189">U kunt meer informatie over projectie in Hallo [blogbericht introductie tot Upsert en Query projectie blogbericht][blog_post_upsert].</span><span class="sxs-lookup"><span data-stu-id="9ed0d-189">You can learn more about projection in hello [Introducing Upsert and Query Projection blog post][blog_post_upsert].</span></span> <span data-ttu-id="9ed0d-190">Projectie wordt niet ondersteund door de opslagemulator hello, zodat deze code wordt alleen uitgevoerd als u een account in de tabelservice Hallo.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-190">Projection is not supported by hello storage emulator, so this code runs only when you're using an account in hello Table service.</span></span>

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

## <a name="delete-an-entity"></a><span data-ttu-id="9ed0d-191">Een entiteit verwijderen</span><span class="sxs-lookup"><span data-stu-id="9ed0d-191">Delete an entity</span></span>
<span data-ttu-id="9ed0d-192">U kunt een entiteit gemakkelijk verwijderen nadat u deze hebt opgehaald met behulp van Hallo hetzelfde patroon weergegeven voor het bijwerken van een entiteit.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-192">You can easily delete an entity after you have retrieved it by using hello same pattern shown for updating an entity.</span></span> <span data-ttu-id="9ed0d-193">Hallo na de code opgehaald en wordt een klantentiteit verwijderd.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-193">hello following code retrieves and deletes a customer entity.</span></span>

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

## <a name="delete-a-table"></a><span data-ttu-id="9ed0d-194">Een tabel verwijderen</span><span class="sxs-lookup"><span data-stu-id="9ed0d-194">Delete a table</span></span>
<span data-ttu-id="9ed0d-195">Ten slotte verwijdert Hallo volgende codevoorbeeld een tabel uit een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-195">Finally, hello following code example deletes a table from a storage account.</span></span> <span data-ttu-id="9ed0d-196">Een tabel die is verwijderd is niet beschikbaar toobe opnieuw worden gemaakt voor een bepaalde tijd na Hallo verwijderen.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-196">A table that has been deleted will be unavailable toobe re-created for a period of time following hello deletion.</span></span>

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

## <a name="retrieve-entities-in-pages-asynchronously"></a><span data-ttu-id="9ed0d-197">Entiteiten asynchroon ophalen op pagina's</span><span class="sxs-lookup"><span data-stu-id="9ed0d-197">Retrieve entities in pages asynchronously</span></span>
<span data-ttu-id="9ed0d-198">Als u een groot aantal entiteiten leest en entiteiten tooprocess/weergeven gewenste terwijl ze worden opgehaald in plaats van wachten tot ze alle tooreturn, kunt u entiteiten ophalen met behulp van een gesegmenteerde query.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-198">If you are reading a large number of entities, and you want tooprocess/display entities as they are retrieved rather than waiting for them all tooreturn, you can retrieve entities by using a segmented query.</span></span> <span data-ttu-id="9ed0d-199">Dit voorbeeld toont hoe tooreturn resultaten op pagina's met behulp van Hallo Async-Await-patroon, zodat de uitvoering niet wordt geblokkeerd terwijl u wacht voor een groot aantal resultaten tooreturn.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-199">This example shows how tooreturn results in pages by using hello Async-Await pattern so that execution is not blocked while you're waiting for a large set of results tooreturn.</span></span> <span data-ttu-id="9ed0d-200">Zie voor meer informatie over het gebruik van hello Async-Await-patroon in .NET, [asynchrone programmering met Async en Await (C# en Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx).</span><span class="sxs-lookup"><span data-stu-id="9ed0d-200">For more details on using hello Async-Await pattern in .NET, see [Asynchronous programming with Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx).</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="9ed0d-201">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9ed0d-201">Next steps</span></span>
<span data-ttu-id="9ed0d-202">Nu u Hallo basisprincipes van Table storage hebt geleerd, volgt u deze koppelingen toolearn over complexere opslagtaken:</span><span class="sxs-lookup"><span data-stu-id="9ed0d-202">Now that you've learned hello basics of Table storage, follow these links toolearn about more complex storage tasks:</span></span>

* <span data-ttu-id="9ed0d-203">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is een gratis, zelfstandige app van Microsoft waarmee u toowork visueel met Azure Storage-gegevens op Windows-, Mac OS- en Linux.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-203">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="9ed0d-204">Zie [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/) (Aan de slag met Azure Table Storage in .NET) voor meer voorbeelden van Table Storage.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-204">See more Table storage samples in [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)</span></span>
* <span data-ttu-id="9ed0d-205">Hallo tabel-service-naslagdocumentatie voor volledige informatie over beschikbare API's bekijken:</span><span class="sxs-lookup"><span data-stu-id="9ed0d-205">View hello Table service reference documentation for complete details about available APIs:</span></span>
* [<span data-ttu-id="9ed0d-206">Naslaginformatie over de Storage-clientbibliotheek voor .NET</span><span class="sxs-lookup"><span data-stu-id="9ed0d-206">Storage Client Library for .NET reference</span></span>](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
* [<span data-ttu-id="9ed0d-207">Naslaginformatie over de REST-API</span><span class="sxs-lookup"><span data-stu-id="9ed0d-207">REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="9ed0d-208">Meer informatie over hoe u toosimplify Hallo code schrijft toowork met Azure Storage met behulp van Hallo [Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="9ed0d-208">Learn how toosimplify hello code you write toowork with Azure Storage by using hello [Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)</span></span>
* <span data-ttu-id="9ed0d-209">Bekijk meer functie handleidingen toolearn over aanvullende mogelijkheden voor het opslaan van gegevens in Azure.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-209">View more feature guides toolearn about additional options for storing data in Azure.</span></span>
* <span data-ttu-id="9ed0d-210">[Aan de slag met Azure Blob storage met .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) toostore ongestructureerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-210">[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) toostore unstructured data.</span></span>
* <span data-ttu-id="9ed0d-211">[Verbinding maken met tooSQL Database met behulp van .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md) toostore relationele gegevens.</span><span class="sxs-lookup"><span data-stu-id="9ed0d-211">[Connect tooSQL Database by using .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md) toostore relational data.</span></span>

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
