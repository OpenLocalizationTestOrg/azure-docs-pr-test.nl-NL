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
# <a name="getting-started-with-azure-table-storage-and-visual-studio-connected-services-cloud-services-projects"></a>Aan de slag met Azure-tabelopslag en Visual Studio verbonden services (cloud services-projecten)
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a>Overzicht
Dit artikel wordt beschreven hoe tooget gestart met behulp van Azure-tabelopslag in Visual Studio nadat u hebt gemaakt of een Azure storage-account in een cloud services-project waarnaar wordt verwezen met behulp van Visual Studio Hallo **verbonden Services toevoegen** dialoogvenster . Hallo **verbonden Services toevoegen** bewerking installeert Hallo juiste NuGet-pakketten tooaccess Azure-opslag in uw project en voegt Hallo-verbindingsreeks voor hello storage account tooyour project configuratiebestanden.

Hello Azure Table storage-service kunt u toostore grote hoeveelheden gestructureerde gegevens. Hallo-service is een NoSQL-gegevensarchief die geverifieerde aanroepen vanuit binnen en buiten hello Azure-cloud accepteert. Azure-tabellen zijn ideaal voor het opslaan van gestructureerde, niet-relationele gegevens.

tooget gestart, moet u eerst toocreate een tabel in uw opslagaccount. Leert u hoe een Azure toocreate tabel in de code en ook hoe tooperform basistabel en entiteit bewerkingen, zoals het toevoegen, wijzigen, lezen en lezen van tabel entiteiten. Hallo-voorbeelden zijn geschreven in C\# code en gebruik Hallo [Microsoft Azure Storage-clientbibliotheek voor .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).

**Opmerking:** aantal Hallo API's die voor het uitvoeren van aanroepen uit tooAzure opslag zijn asynchroon. Zie [asynchrone programmering met Async en Await](http://msdn.microsoft.com/library/hh191443.aspx) voor meer informatie. Hallo-code hieronder wordt ervan uitgegaan programming async-methoden worden gebruikt.

* Zie [aan de slag met Azure Table storage met .NET](storage-dotnet-how-to-use-tables.md) voor meer informatie over het bewerken van programmatisch tabellen.
* Zie [documentatie Storage](https://azure.microsoft.com/documentation/services/storage/) voor algemene informatie over Azure Storage.
* Zie [Cloud Services-documentatie](https://azure.microsoft.com/documentation/services/cloud-services/) voor algemene informatie over Azure-cloudservices.
* Zie [ASP.NET](http://www.asp.net) voor meer informatie over het programmeren van ASP.NET-toepassingen.

## <a name="access-tables-in-code"></a>Toegang tot tabellen in code
tooaccess tabellen in cloudserviceprojecten, moet u tooinclude Hallo items tooany C#-bronbestanden die toegang hebben tot Azure-tabelopslag te volgen.

1. Zorg ervoor dat de naamruimtedeclaraties Hallo Hallo bovenaan Hallo C#-bestand in deze **met** instructies.
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. Ophalen van een **CloudStorageAccount** -object met gegevens over uw storage-account. Hallo volgende code tooget Hallo opslag tekenreeks en storage-account verbindingsgegevens uit hello Azure-service-configuratie gebruiken.
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage account name>
         _AzureStorageConnectionString"));
   > [!NOTE]
   > Alle Hallo bovenstaande code voor het Hallo-code in Hallo volgen voorbeelden gebruiken.
   > 
   > 
3. Ophalen van een **CloudTableClient** object tooreference Hallo table-objecten in uw opslagaccount.
   
         // Create hello table client.
         CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. Ophalen van een **CloudTable** verwijst naar object tooreference een specifieke tabel en entiteiten.
   
        // Get a reference tooa table named "peopleTable".
        CloudTable peopleTable = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a>Een tabel in code maken
toocreate hello Azure-tabel, voegt u toe een aanroep te**CreateIfNotExistsAsync** toohello nadat u een **CloudTable** zoals beschreven in de sectie van de 'Toegang tot tabellen in de code' Hallo-object.

    // Create hello CloudTable if it does not exist.
    await peopleTable.CreateIfNotExistsAsync();

## <a name="add-an-entity-tooa-table"></a>Een entiteit tooa tabel toevoegen
tooadd een entiteit tooa tabel, maak een klasse die eigenschappen Hallo van uw entiteit definieert. Hallo volgende code definieert een entiteitsklasse aangeroepen **CustomerEntity** dat wordt gebruikt de voornaam van de klant als de rijsleutel Hallo- en achternaam als partitiesleutel Hallo HALLO hallo.

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

Tabelbewerkingen met betrekking tot entiteiten klaar bent met Hallo **CloudTable** -object dat u eerder in 'Toegang tot tabellen in de code' gemaakt Hallo **TableOperation** object vertegenwoordigt Hallo bewerking toobe gedaan. Hallo van de volgende code voorbeeld ziet u hoe toocreate een **CloudTable** object en een **CustomerEntity** object. tooprepare hello bewerking, een **TableOperation** tooinsert hello klantentiteit in Hallo-tabel is gemaakt. Ten slotte Hallo-bewerking wordt uitgevoerd door het aanroepen van **CloudTable.ExecuteAsync**.

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create hello TableOperation that inserts hello customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute hello insert operation.
    await peopleTable.ExecuteAsync(insertOperation);


## <a name="insert-a-batch-of-entities"></a>Een batch entiteiten invoegen
U kunt meerdere entiteiten invoegen in een tabel in een enkel schrijfbewerking. Hallo volgende codevoorbeeld maakt twee entiteitsobjecten ('Jeff Smith' en 'Ben Smith'), voegt deze tooa **TableBatchOperation** object met Hallo methode invoegen en vervolgens wordt gestart opnieuw door het aanroepen van Hallo  **CloudTable.ExecuteBatchAsync**.

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

## <a name="get-all-of-hello-entities-in-a-partition"></a>Alle Hallo entiteiten in een partitie ophalen
een tabel voor alle entiteiten in een partitie, gebruik Hallo tooquery een **TableQuery** object. Hallo geeft volgende codevoorbeeld een filter voor entiteiten waarbij 'Smith' hello partitiesleutel is. Dit voorbeeld wordt Hallo velden van elke entiteit in Hallo query resultaten toohello-console.

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


## <a name="get-a-single-entity"></a>Één entiteit ophalen
U kunt een query tooget één specifieke entiteit schrijven. Hallo volgende code wordt een **TableOperation** object toospecify 'Ben Smith' met de naam van de klant. Deze methode retourneert één entiteit in plaats van een verzameling en Hallo geretourneerd waarde in **TableResult.Result** is een **CustomerEntity** object. Het opgeven van de partitie-als rijsleutels in een query is Hallo snelste manier tooretrieve één entiteit van Hallo **tabel** service.

    // Create a retrieve operation that takes a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute hello retrieve operation.
    TableResult retrievedResult = await peopleTable.ExecuteAsync(retrieveOperation);

    // Print hello phone number of hello result.
    if (retrievedResult.Result != null)
       Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
    else
       Console.WriteLine("hello phone number could not be retrieved.");

## <a name="delete-an-entity"></a>Een entiteit verwijderen
Nadat u deze hebt gevonden, kunt u een entiteit verwijderen. Hallo volgende code gezocht naar een klantentiteit met de naam 'Ben Smith', en als het wordt gevonden, wordt de snelkoppeling verwijderd.

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

## <a name="next-steps"></a>Volgende stappen
[!INCLUDE [vs-storage-dotnet-tables-next-steps](../../includes/vs-storage-dotnet-tables-next-steps.md)]

