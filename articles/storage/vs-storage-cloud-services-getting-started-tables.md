---
title: aaaGet gestart met de tabelopslag en Visual Studio verbonden services (cloudservices) | Microsoft Docs
description: Hoe tooget gestart met Azure Table storage in een cloud service-project in Visual Studio nadat tooa storage-account met Visual Studio verbinding services verbonden
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: a3a11ed8-ba7f-4193-912b-e555f5b72184
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: efb16953e05764cb162cbdae4d0eab57f781682d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-table-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="8fa04-103">Aan de slag met Azure-tabelopslag en Visual Studio verbonden services (cloud services-projecten)</span><span class="sxs-lookup"><span data-stu-id="8fa04-103">Getting started with Azure table storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="8fa04-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="8fa04-104">Overview</span></span>
<span data-ttu-id="8fa04-105">Dit artikel wordt beschreven hoe tooget gestart met behulp van Azure-tabelopslag in Visual Studio nadat u hebt gemaakt of een Azure storage-account in een cloud services-project waarnaar wordt verwezen met behulp van Visual Studio Hallo **verbonden Services toevoegen** dialoogvenster .</span><span class="sxs-lookup"><span data-stu-id="8fa04-105">This article describes how tooget started using Azure table storage in Visual Studio after you have created or referenced an Azure storage account in a cloud services project by using hello Visual Studio **Add Connected Services** dialog.</span></span> <span data-ttu-id="8fa04-106">Hallo **verbonden Services toevoegen** bewerking installeert Hallo juiste NuGet-pakketten tooaccess Azure-opslag in uw project en voegt Hallo-verbindingsreeks voor hello storage account tooyour project configuratiebestanden.</span><span class="sxs-lookup"><span data-stu-id="8fa04-106">hello **Add Connected Services** operation installs hello appropriate NuGet packages tooaccess Azure storage in your project and adds hello connection string for hello storage account tooyour project configuration files.</span></span>

<span data-ttu-id="8fa04-107">Hello Azure Table storage-service kunt u toostore grote hoeveelheden gestructureerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="8fa04-107">hello Azure Table storage service enables you toostore large amounts of structured data.</span></span> <span data-ttu-id="8fa04-108">Hallo-service is een NoSQL-gegevensarchief die geverifieerde aanroepen vanuit binnen en buiten hello Azure-cloud accepteert.</span><span class="sxs-lookup"><span data-stu-id="8fa04-108">hello service is a NoSQL datastore that accepts authenticated calls from inside and outside hello Azure cloud.</span></span> <span data-ttu-id="8fa04-109">Azure-tabellen zijn ideaal voor het opslaan van gestructureerde, niet-relationele gegevens.</span><span class="sxs-lookup"><span data-stu-id="8fa04-109">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="8fa04-110">tooget gestart, moet u eerst toocreate een tabel in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="8fa04-110">tooget started, you first need toocreate a table in your storage account.</span></span> <span data-ttu-id="8fa04-111">Leert u hoe een Azure toocreate tabel in de code en ook hoe tooperform basistabel en entiteit bewerkingen, zoals het toevoegen, wijzigen, lezen en lezen van tabel entiteiten.</span><span class="sxs-lookup"><span data-stu-id="8fa04-111">We'll show you how toocreate an Azure table in code, and also how tooperform basic table and entity operations, such as adding, modifying, reading and reading table entities.</span></span> <span data-ttu-id="8fa04-112">Hallo-voorbeelden zijn geschreven in C\# code en gebruik Hallo [Microsoft Azure Storage-clientbibliotheek voor .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="8fa04-112">hello samples are written in C\# code and use hello [Microsoft Azure Storage client library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="8fa04-113">**Opmerking:** aantal Hallo API's die voor het uitvoeren van aanroepen uit tooAzure opslag zijn asynchroon.</span><span class="sxs-lookup"><span data-stu-id="8fa04-113">**NOTE:** Some of hello APIs that perform calls out tooAzure storage are asynchronous.</span></span> <span data-ttu-id="8fa04-114">Zie [asynchrone programmering met Async en Await](http://msdn.microsoft.com/library/hh191443.aspx) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="8fa04-114">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="8fa04-115">Hallo-code hieronder wordt ervan uitgegaan programming async-methoden worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8fa04-115">hello code below assumes async programming methods are being used.</span></span>

* <span data-ttu-id="8fa04-116">Zie [aan de slag met Azure Table storage met .NET](storage-dotnet-how-to-use-tables.md) voor meer informatie over het bewerken van programmatisch tabellen.</span><span class="sxs-lookup"><span data-stu-id="8fa04-116">See [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md) for more information on programmatically manipulating tables.</span></span>
* <span data-ttu-id="8fa04-117">Zie [documentatie Storage](https://azure.microsoft.com/documentation/services/storage/) voor algemene informatie over Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="8fa04-117">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="8fa04-118">Zie [Cloud Services-documentatie](https://azure.microsoft.com/documentation/services/cloud-services/) voor algemene informatie over Azure-cloudservices.</span><span class="sxs-lookup"><span data-stu-id="8fa04-118">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="8fa04-119">Zie [ASP.NET](http://www.asp.net) voor meer informatie over het programmeren van ASP.NET-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="8fa04-119">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

## <a name="access-tables-in-code"></a><span data-ttu-id="8fa04-120">Toegang tot tabellen in code</span><span class="sxs-lookup"><span data-stu-id="8fa04-120">Access tables in code</span></span>
<span data-ttu-id="8fa04-121">tooaccess tabellen in cloudserviceprojecten, moet u tooinclude Hallo items tooany C#-bronbestanden die toegang hebben tot Azure-tabelopslag te volgen.</span><span class="sxs-lookup"><span data-stu-id="8fa04-121">tooaccess tables in cloud service projects, you need tooinclude hello following items tooany C# source files that access Azure table storage.</span></span>

1. <span data-ttu-id="8fa04-122">Zorg ervoor dat de naamruimtedeclaraties Hallo Hallo bovenaan Hallo C#-bestand in deze **met** instructies.</span><span class="sxs-lookup"><span data-stu-id="8fa04-122">Make sure hello namespace declarations at hello top of hello C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="8fa04-123">Ophalen van een **CloudStorageAccount** -object met gegevens over uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="8fa04-123">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="8fa04-124">Hallo volgende code tooget Hallo opslag tekenreeks en storage-account verbindingsgegevens uit hello Azure-service-configuratie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8fa04-124">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage account name>
         _AzureStorageConnectionString"));
   > [!NOTE]
   > <span data-ttu-id="8fa04-125">Alle Hallo bovenstaande code voor het Hallo-code in Hallo volgen voorbeelden gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8fa04-125">Use all of hello above code in front of hello code in hello following samples.</span></span>
   > 
   > 
3. <span data-ttu-id="8fa04-126">Ophalen van een **CloudTableClient** object tooreference Hallo table-objecten in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="8fa04-126">Get a **CloudTableClient** object tooreference hello table objects in your storage account.</span></span>
   
         // Create hello table client.
         CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. <span data-ttu-id="8fa04-127">Ophalen van een **CloudTable** verwijst naar object tooreference een specifieke tabel en entiteiten.</span><span class="sxs-lookup"><span data-stu-id="8fa04-127">Get a **CloudTable** reference object tooreference a specific table and entities.</span></span>
   
        // Get a reference tooa table named "peopleTable".
        CloudTable peopleTable = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a><span data-ttu-id="8fa04-128">Een tabel in code maken</span><span class="sxs-lookup"><span data-stu-id="8fa04-128">Create a table in code</span></span>
<span data-ttu-id="8fa04-129">toocreate hello Azure-tabel, voegt u toe een aanroep te**CreateIfNotExistsAsync** toohello nadat u een **CloudTable** zoals beschreven in de sectie van de 'Toegang tot tabellen in de code' Hallo-object.</span><span class="sxs-lookup"><span data-stu-id="8fa04-129">toocreate hello Azure table, just add a call too**CreateIfNotExistsAsync** toohello after you get a **CloudTable** object as described in hello "Access tables in code" section.</span></span>

    // Create hello CloudTable if it does not exist.
    await peopleTable.CreateIfNotExistsAsync();

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="8fa04-130">Een entiteit tooa tabel toevoegen</span><span class="sxs-lookup"><span data-stu-id="8fa04-130">Add an entity tooa table</span></span>
<span data-ttu-id="8fa04-131">tooadd een entiteit tooa tabel, maak een klasse die eigenschappen Hallo van uw entiteit definieert.</span><span class="sxs-lookup"><span data-stu-id="8fa04-131">tooadd an entity tooa table, create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="8fa04-132">Hallo volgende code definieert een entiteitsklasse aangeroepen **CustomerEntity** dat wordt gebruikt de voornaam van de klant als de rijsleutel Hallo- en achternaam als partitiesleutel Hallo HALLO hallo.</span><span class="sxs-lookup"><span data-stu-id="8fa04-132">hello following code defines an entity class called **CustomerEntity** that uses hello customer's first name as hello row key and hello last name as hello partition key.</span></span>

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

<span data-ttu-id="8fa04-133">Tabelbewerkingen met betrekking tot entiteiten klaar bent met Hallo **CloudTable** -object dat u eerder in 'Toegang tot tabellen in de code' gemaakt</span><span class="sxs-lookup"><span data-stu-id="8fa04-133">Table operations involving entities are done using hello **CloudTable** object that you created earlier in "Access tables in code."</span></span> <span data-ttu-id="8fa04-134">Hallo **TableOperation** object vertegenwoordigt Hallo bewerking toobe gedaan.</span><span class="sxs-lookup"><span data-stu-id="8fa04-134">hello **TableOperation** object represents hello operation toobe done.</span></span> <span data-ttu-id="8fa04-135">Hallo van de volgende code voorbeeld ziet u hoe toocreate een **CloudTable** object en een **CustomerEntity** object.</span><span class="sxs-lookup"><span data-stu-id="8fa04-135">hello following code example shows how toocreate a **CloudTable** object and a **CustomerEntity** object.</span></span> <span data-ttu-id="8fa04-136">tooprepare hello bewerking, een **TableOperation** tooinsert hello klantentiteit in Hallo-tabel is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8fa04-136">tooprepare hello operation, a **TableOperation** is created tooinsert hello customer entity into hello table.</span></span> <span data-ttu-id="8fa04-137">Ten slotte Hallo-bewerking wordt uitgevoerd door het aanroepen van **CloudTable.ExecuteAsync**.</span><span class="sxs-lookup"><span data-stu-id="8fa04-137">Finally, hello operation is executed by calling **CloudTable.ExecuteAsync**.</span></span>

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create hello TableOperation that inserts hello customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute hello insert operation.
    await peopleTable.ExecuteAsync(insertOperation);


## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="8fa04-138">Een batch entiteiten invoegen</span><span class="sxs-lookup"><span data-stu-id="8fa04-138">Insert a batch of entities</span></span>
<span data-ttu-id="8fa04-139">U kunt meerdere entiteiten invoegen in een tabel in een enkel schrijfbewerking.</span><span class="sxs-lookup"><span data-stu-id="8fa04-139">You can insert multiple entities into a table in a single write operation.</span></span> <span data-ttu-id="8fa04-140">Hallo volgende codevoorbeeld maakt twee entiteitsobjecten ('Jeff Smith' en 'Ben Smith'), voegt deze tooa **TableBatchOperation** object met Hallo methode invoegen en vervolgens wordt gestart opnieuw door het aanroepen van Hallo  **CloudTable.ExecuteBatchAsync**.</span><span class="sxs-lookup"><span data-stu-id="8fa04-140">hello following code example creates two entity objects ("Jeff Smith" and "Ben Smith"), adds them tooa **TableBatchOperation** object using hello Insert method, and then starts hello operation by calling **CloudTable.ExecuteBatchAsync**.</span></span>

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

## <a name="get-all-of-hello-entities-in-a-partition"></a><span data-ttu-id="8fa04-141">Alle Hallo entiteiten in een partitie ophalen</span><span class="sxs-lookup"><span data-stu-id="8fa04-141">Get all of hello entities in a partition</span></span>
<span data-ttu-id="8fa04-142">een tabel voor alle entiteiten in een partitie, gebruik Hallo tooquery een **TableQuery** object.</span><span class="sxs-lookup"><span data-stu-id="8fa04-142">tooquery a table for all of hello entities in a partition, use a **TableQuery** object.</span></span> <span data-ttu-id="8fa04-143">Hallo geeft volgende codevoorbeeld een filter voor entiteiten waarbij 'Smith' hello partitiesleutel is.</span><span class="sxs-lookup"><span data-stu-id="8fa04-143">hello following code example specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="8fa04-144">Dit voorbeeld wordt Hallo velden van elke entiteit in Hallo query resultaten toohello-console.</span><span class="sxs-lookup"><span data-stu-id="8fa04-144">This example prints hello fields of each entity in hello query results toohello console.</span></span>

    // Construct hello query operation for all customer entities where PartitionKey="Smith".
    TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

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

    return View();


## <a name="get-a-single-entity"></a><span data-ttu-id="8fa04-145">Één entiteit ophalen</span><span class="sxs-lookup"><span data-stu-id="8fa04-145">Get a single entity</span></span>
<span data-ttu-id="8fa04-146">U kunt een query tooget één specifieke entiteit schrijven.</span><span class="sxs-lookup"><span data-stu-id="8fa04-146">You can write a query tooget a single, specific entity.</span></span> <span data-ttu-id="8fa04-147">Hallo volgende code wordt een **TableOperation** object toospecify 'Ben Smith' met de naam van de klant.</span><span class="sxs-lookup"><span data-stu-id="8fa04-147">hello following code uses a **TableOperation** object toospecify a customer named 'Ben Smith'.</span></span> <span data-ttu-id="8fa04-148">Deze methode retourneert één entiteit in plaats van een verzameling en Hallo geretourneerd waarde in **TableResult.Result** is een **CustomerEntity** object.</span><span class="sxs-lookup"><span data-stu-id="8fa04-148">This method returns just one entity, rather than a collection, and hello returned value in **TableResult.Result** is a **CustomerEntity** object.</span></span> <span data-ttu-id="8fa04-149">Het opgeven van de partitie-als rijsleutels in een query is Hallo snelste manier tooretrieve één entiteit van Hallo **tabel** service.</span><span class="sxs-lookup"><span data-stu-id="8fa04-149">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello **Table** service.</span></span>

    // Create a retrieve operation that takes a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute hello retrieve operation.
    TableResult retrievedResult = await peopleTable.ExecuteAsync(retrieveOperation);

    // Print hello phone number of hello result.
    if (retrievedResult.Result != null)
       Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
    else
       Console.WriteLine("hello phone number could not be retrieved.");

## <a name="delete-an-entity"></a><span data-ttu-id="8fa04-150">Een entiteit verwijderen</span><span class="sxs-lookup"><span data-stu-id="8fa04-150">Delete an entity</span></span>
<span data-ttu-id="8fa04-151">Nadat u deze hebt gevonden, kunt u een entiteit verwijderen.</span><span class="sxs-lookup"><span data-stu-id="8fa04-151">You can delete an entity after you find it.</span></span> <span data-ttu-id="8fa04-152">Hallo volgende code gezocht naar een klantentiteit met de naam 'Ben Smith', en als het wordt gevonden, wordt de snelkoppeling verwijderd.</span><span class="sxs-lookup"><span data-stu-id="8fa04-152">hello following code looks for a customer entity named "Ben Smith", and if it finds it, it deletes it.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="8fa04-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8fa04-153">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-tables-next-steps](../../includes/vs-storage-dotnet-tables-next-steps.md)]

