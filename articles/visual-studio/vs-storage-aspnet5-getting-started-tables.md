---
title: aaaHow tooget gestart met de tabelopslag en Visual Studio verbonden services (ASP.NET Core) | Microsoft Docs
description: Hoe tooget gestart met Azure Table storage in een ASP.NET Core-project in Visual Studio nadat tooa storage-account met Visual Studio verbinding services verbonden
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: c3c451d1-71ff-4222-a348-c41c98a02b85
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: e3eb3f3e65456108dd3cde7e3e470f98ba456e35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-started-with-azure-table-storage-and-visual-studio-connected-services"></a><span data-ttu-id="1c2d0-103">Hoe tooget de slag met Azure Table storage en Visual Studio verbonden services</span><span class="sxs-lookup"><span data-stu-id="1c2d0-103">How tooget started with Azure Table storage and Visual Studio connected services</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="1c2d0-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="1c2d0-104">Overview</span></span>
<span data-ttu-id="1c2d0-105">Dit artikel wordt beschreven hoe gestart met behulp van Azure Table storage in Visual Studio nadat u hebt gemaakt of een Azure storage-account in een ASP.NET Core-project waarnaar wordt verwezen met behulp van Visual Studio Hallo **verbonden Services toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1c2d0-105">This article describes how get started using Azure Table storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using hello Visual Studio **Add Connected Services** dialog.</span></span>

<span data-ttu-id="1c2d0-106">Hello Azure Table storage-service kunt u toostore grote hoeveelheden gestructureerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="1c2d0-106">hello Azure Table storage service enables you toostore large amounts of structured data.</span></span> <span data-ttu-id="1c2d0-107">Hallo-service is een NoSQL-gegevensarchief die geverifieerde aanroepen vanuit binnen en buiten hello Azure-cloud accepteert.</span><span class="sxs-lookup"><span data-stu-id="1c2d0-107">hello service is a NoSQL data store that accepts authenticated calls from inside and outside hello Azure cloud.</span></span> <span data-ttu-id="1c2d0-108">Azure-tabellen zijn ideaal voor het opslaan van gestructureerde, niet-relationele gegevens.</span><span class="sxs-lookup"><span data-stu-id="1c2d0-108">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="1c2d0-109">Hallo **verbonden Services toevoegen** bewerking installeert Hallo juiste NuGet-pakketten tooaccess Azure-opslag in uw project en voegt Hallo-verbindingsreeks voor hello storage account tooyour project configuratiebestanden.</span><span class="sxs-lookup"><span data-stu-id="1c2d0-109">hello **Add Connected Services** operation installs hello appropriate NuGet packages tooaccess Azure storage in your project and adds hello connection string for hello storage account tooyour project configuration files.</span></span>

<span data-ttu-id="1c2d0-110">Zie voor meer algemene informatie over het gebruik van Azure Table storage [aan de slag met Azure Table storage met .NET](../storage/storage-dotnet-how-to-use-tables.md).</span><span class="sxs-lookup"><span data-stu-id="1c2d0-110">For more general information about using Azure Table storage, see [Get started with Azure Table storage using .NET](../storage/storage-dotnet-how-to-use-tables.md).</span></span>

<span data-ttu-id="1c2d0-111">tooget gestart, moet u eerst toocreate een tabel in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="1c2d0-111">tooget started, you first need toocreate a table in your storage account.</span></span> <span data-ttu-id="1c2d0-112">We laten zien u hoe een Azure toocreate tabel in de code.</span><span class="sxs-lookup"><span data-stu-id="1c2d0-112">We'll show you how toocreate an Azure table in code.</span></span> <span data-ttu-id="1c2d0-113">Ook ziet u hoe de basistabel tooperform en entiteit bewerkingen, zoals het toevoegen, wijzigen, lezen en lezen tabel entiteiten.</span><span class="sxs-lookup"><span data-stu-id="1c2d0-113">We'll also show you how tooperform basic table and entity operations, such as adding, modifying, reading and reading table entities.</span></span> <span data-ttu-id="1c2d0-114">Hallo-voorbeelden zijn geschreven in C\# code en hello Azure Storage-clientbibliotheek voor .NET.</span><span class="sxs-lookup"><span data-stu-id="1c2d0-114">hello samples are written in C\# code and use hello Azure Storage Client Library for .NET.</span></span>

<span data-ttu-id="1c2d0-115">**Opmerking** -aantal Hallo API's die het uitvoeren van aanroepen uit tooAzure opslag in ASP.NET Core zijn asynchroon.</span><span class="sxs-lookup"><span data-stu-id="1c2d0-115">**NOTE** - Some of hello APIs that perform calls out tooAzure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="1c2d0-116">Zie [asynchrone programmering met Async en Await](http://msdn.microsoft.com/library/hh191443.aspx) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="1c2d0-116">See [Asynchronous Programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="1c2d0-117">Hallo-code hieronder wordt ervan uitgegaan programming Async-methoden worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1c2d0-117">hello code below assumes Async programming methods are being used.</span></span>

## <a name="access-tables-in-code"></a><span data-ttu-id="1c2d0-118">Toegang tot tabellen in code</span><span class="sxs-lookup"><span data-stu-id="1c2d0-118">Access tables in code</span></span>
<span data-ttu-id="1c2d0-119">tooaccess tabellen in ASP.NET Core projecten, moet u tooinclude Hallo items tooany C#-bronbestanden die toegang hebben tot Azure-tabelopslag te volgen.</span><span class="sxs-lookup"><span data-stu-id="1c2d0-119">tooaccess tables in ASP.NET Core projects, you need tooinclude hello following items tooany C# source files that access Azure table storage.</span></span>

1. <span data-ttu-id="1c2d0-120">Zorg ervoor dat de naamruimtedeclaraties Hallo Hallo bovenaan Hallo C#-bestand in deze **met** instructies.</span><span class="sxs-lookup"><span data-stu-id="1c2d0-120">Make sure hello namespace declarations at hello top of hello C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="1c2d0-121">Ophalen van een **CloudStorageAccount** -object met gegevens over uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="1c2d0-121">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="1c2d0-122">Gebruik Hallo na code tooget Hallo uw verbindingsreeks voor opslag en de accountgegevens van de opslag van Azure Hallo-serviceconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="1c2d0-122">Use hello following code tooget hello your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
            CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
   
    <span data-ttu-id="1c2d0-123">**Opmerking** -alle Hallo bovenstaande code voor het Hallo-code in Hallo volgen voorbeelden gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1c2d0-123">**NOTE** - Use all of hello above code in front of hello code in hello following samples.</span></span>
3. <span data-ttu-id="1c2d0-124">Ophalen van een **CloudTableClient** object tooreference Hallo table-objecten in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="1c2d0-124">Get a **CloudTableClient** object tooreference hello table objects in your storage account.</span></span>  
   
        // Create hello table client.
        CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. <span data-ttu-id="1c2d0-125">Ophalen van een **CloudTable** verwijst naar object tooreference een specifieke tabel en entiteiten.</span><span class="sxs-lookup"><span data-stu-id="1c2d0-125">Get a **CloudTable** reference object tooreference a specific table and entities.</span></span>
   
        // Get a reference tooa table named "peopleTable"
        CloudTable table = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a><span data-ttu-id="1c2d0-126">Een tabel in code maken</span><span class="sxs-lookup"><span data-stu-id="1c2d0-126">Create a table in code</span></span>
<span data-ttu-id="1c2d0-127">toocreate hello Azure-tabel, voegt u toe een aanroep te**CreateIfNotExistsAsync()**.</span><span class="sxs-lookup"><span data-stu-id="1c2d0-127">toocreate hello Azure table, just add a call too**CreateIfNotExistsAsync()**.</span></span>

    // Create hello CloudTable if it does not exist
    await table.CreateIfNotExistsAsync();

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="1c2d0-128">Een entiteit tooa tabel toevoegen</span><span class="sxs-lookup"><span data-stu-id="1c2d0-128">Add an entity tooa table</span></span>
<span data-ttu-id="1c2d0-129">een entiteit tooa tabel maken van een klasse die tooadd definieert Hallo eigenschappen van uw entiteit.</span><span class="sxs-lookup"><span data-stu-id="1c2d0-129">tooadd an entity tooa table you create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="1c2d0-130">Hallo volgende code definieert een entiteitsklasse aangeroepen **CustomerEntity** dat wordt gebruikt de voornaam van de klant als de rijsleutel Hallo- en achternaam als partitiesleutel Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="1c2d0-130">hello following code defines an entity class called **CustomerEntity** that uses hello customer's first name as hello row key and last name as hello partition key.</span></span>

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

<span data-ttu-id="1c2d0-131">Tabelbewerkingen met betrekking tot entiteiten klaar bent met Hallo **CloudTable** object u eerder in 'Toegang tot tabellen in de code' gemaakt</span><span class="sxs-lookup"><span data-stu-id="1c2d0-131">Table operations involving entities are done using hello **CloudTable** object you created earlier in "Access tables in code."</span></span> <span data-ttu-id="1c2d0-132">Hallo **TableOperation** object vertegenwoordigt Hallo bewerking toobe gedaan.</span><span class="sxs-lookup"><span data-stu-id="1c2d0-132">hello **TableOperation** object represents hello operation toobe done.</span></span> <span data-ttu-id="1c2d0-133">Hallo van de volgende code voorbeeld ziet u hoe toocreate een **CloudTable** object en een **CustomerEntity** object.</span><span class="sxs-lookup"><span data-stu-id="1c2d0-133">hello following code example shows how toocreate a **CloudTable** object and a **CustomerEntity** object.</span></span> <span data-ttu-id="1c2d0-134">tooprepare hello bewerking, een **TableOperation** tooinsert hello klantentiteit in Hallo-tabel is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1c2d0-134">tooprepare hello operation, a **TableOperation** is created tooinsert hello customer entity into hello table.</span></span> <span data-ttu-id="1c2d0-135">Ten slotte wordt Hallo-bewerking uitgevoerd door het aanroepen van CloudTable.ExecuteAsync.</span><span class="sxs-lookup"><span data-stu-id="1c2d0-135">Finally, hello operation is executed by calling CloudTable.ExecuteAsync.</span></span>

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create hello TableOperation that inserts hello customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute hello insert operation.
    await peopleTable.ExecuteAsync(insertOperation);

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="1c2d0-136">Een batch entiteiten invoegen</span><span class="sxs-lookup"><span data-stu-id="1c2d0-136">Insert a batch of entities</span></span>
<span data-ttu-id="1c2d0-137">U kunt meerdere entiteiten invoegen in een tabel in een enkel schrijfbewerking.</span><span class="sxs-lookup"><span data-stu-id="1c2d0-137">You can insert multiple entities into a table in a single write operation.</span></span> <span data-ttu-id="1c2d0-138">Hallo volgende codevoorbeeld maakt twee entiteitsobjecten ('Jeff Smith' en 'Ben Smith'), voegt deze tooa **TableBatchOperation** -object op met de Hallo **invoegen** methode en Hallo-bewerking wordt gestart door het aanroepen van CloudTable.ExecuteBatchAsync.</span><span class="sxs-lookup"><span data-stu-id="1c2d0-138">hello following code example creates two entity objects ("Jeff Smith" and "Ben Smith"), adds them tooa **TableBatchOperation** object using hello **Insert** method, and then starts hello operation by calling CloudTable.ExecuteBatchAsync.</span></span>

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
    await peopleTable.ExecuteBatchAsync(batchOperation);

## <a name="get-all-of-hello-entities-in-a-partition"></a><span data-ttu-id="1c2d0-139">Alle Hallo entiteiten in een partitie ophalen</span><span class="sxs-lookup"><span data-stu-id="1c2d0-139">Get all of hello entities in a partition</span></span>
<span data-ttu-id="1c2d0-140">een tabel voor alle entiteiten in een partitie, gebruik Hallo tooquery een **TableQuery** object.</span><span class="sxs-lookup"><span data-stu-id="1c2d0-140">tooquery a table for all of hello entities in a partition, use a **TableQuery** object.</span></span> <span data-ttu-id="1c2d0-141">Hallo geeft volgende codevoorbeeld een filter voor entiteiten waarbij 'Smith' hello partitiesleutel is.</span><span class="sxs-lookup"><span data-stu-id="1c2d0-141">hello following code example specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="1c2d0-142">Dit voorbeeld wordt Hallo velden van elke entiteit in Hallo query resultaten toohello-console.</span><span class="sxs-lookup"><span data-stu-id="1c2d0-142">This example prints hello fields of each entity in hello query results toohello console.</span></span>

    // Construct hello query operation for all customer entities where PartitionKey="Smith".
    TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>().Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

    // Print hello fields for each customer.
    TableContinuationToken token = null;
    do
    {
        TableQuerySegment<CustomerEntity> resultSegment = await peopleTable.ExecuteQuerySegmentedAsync(query, token);
        token = resultSegment.ContinuationToken;

        foreach (CustomerEntity entity in resultSegment.Results)
        {
            Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
            entity.Email, entity.PhoneNumber);
        }
    } while (token != null);

## <a name="get-a-single-entity"></a><span data-ttu-id="1c2d0-143">Één entiteit ophalen</span><span class="sxs-lookup"><span data-stu-id="1c2d0-143">Get a single entity</span></span>
<span data-ttu-id="1c2d0-144">U kunt een query tooget één specifieke entiteit schrijven.</span><span class="sxs-lookup"><span data-stu-id="1c2d0-144">You can write a query tooget a single, specific entity.</span></span> <span data-ttu-id="1c2d0-145">Hallo volgende code wordt een **TableOperation** object toospecify 'Ben Smith' met de naam van de klant.</span><span class="sxs-lookup"><span data-stu-id="1c2d0-145">hello following code uses a **TableOperation** object toospecify a customer named 'Ben Smith'.</span></span> <span data-ttu-id="1c2d0-146">Deze methode retourneert één entiteit in plaats van een verzameling en Hallo geretourneerd waarde in **TableResult.Result** is een **CustomerEntity** object.</span><span class="sxs-lookup"><span data-stu-id="1c2d0-146">This method returns just one entity, rather than a collection, and hello returned value in **TableResult.Result** is a **CustomerEntity** object.</span></span> <span data-ttu-id="1c2d0-147">Het opgeven van de partitie-als rijsleutels in een query is Hallo snelste manier tooretrieve één entiteit van Hallo **tabel** service.</span><span class="sxs-lookup"><span data-stu-id="1c2d0-147">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello **Table** service.</span></span>

    // Create a retrieve operation that takes a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute hello retrieve operation.
    TableResult retrievedResult = await peopleTable.ExecuteAsync(retrieveOperation);

    // Print hello phone number of hello result.
    if (retrievedResult.Result != null)
       Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
    else
       Console.WriteLine("hello phone number could not be retrieved.");

## <a name="delete-an-entity"></a><span data-ttu-id="1c2d0-148">Een entiteit verwijderen</span><span class="sxs-lookup"><span data-stu-id="1c2d0-148">Delete an entity</span></span>
<span data-ttu-id="1c2d0-149">Nadat u deze hebt gevonden, kunt u een entiteit verwijderen.</span><span class="sxs-lookup"><span data-stu-id="1c2d0-149">You can delete an entity after you find it.</span></span> <span data-ttu-id="1c2d0-150">Hallo volgende code gezocht naar een klantentiteit met de naam 'Ben Smith' en als het wordt gevonden, wordt de snelkoppeling verwijderd.</span><span class="sxs-lookup"><span data-stu-id="1c2d0-150">hello following code looks for a customer entity named "Ben Smith" and if it finds it, it deletes it.</span></span>

    // Create a retrieve operation that expects a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute hello operation.
    TableResult retrievedResult = peopleTable.Execute(retrieveOperation);

    // Assign hello result tooa CustomerEntity object.
    CustomerEntity deleteEntity = (CustomerEntity)retrievedResult.Result;

    // Create hello Delete TableOperation and then execute it.
    if (deleteEntity != null)
    {
       TableOperation deleteOperation = TableOperation.Delete(deleteEntity);

       // Execute hello operation.
       await peopleTable.ExecuteAsync(deleteOperation);

       Console.WriteLine("Entity deleted.");
    }

    else
       Console.WriteLine("Couldn't delete hello entity.");

## <a name="next-steps"></a><span data-ttu-id="1c2d0-151">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1c2d0-151">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-tables-next-steps](../../includes/vs-storage-dotnet-tables-next-steps.md)]

