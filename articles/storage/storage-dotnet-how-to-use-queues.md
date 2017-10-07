---
title: aaaGet de slag met Azure Queue storage met .NET | Microsoft Docs
description: Azure Queues biedt betrouwbare, asynchrone uitwisseling van berichten tussen toepassingsonderdelen. Cloud messaging Hiermee uw toepassing onderdelen tooscale onafhankelijk.
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: c0f82537-a613-4f01-b2ed-fc82e5eea2a7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/27/2017
ms.author: robinsh
ms.openlocfilehash: 36bbb40189a301cddbc2ded92d0623fa5e093eb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-queue-storage-using-net"></a>Aan de slag met Azure Queue Storage met .NET
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

## <a name="overview"></a>Overzicht
Azure Queue Storage biedt uitwisseling van berichten tussen toepassingsonderdelen in de cloud. Bij het ontwerpen van schaalbare toepassingen worden toepassingsonderdelen vaak ontkoppeld, zodat ze onafhankelijk van elkaar kunnen worden geschaald. Queue storage biedt asynchrone messaging voor communicatie tussen toepassingsonderdelen, of ze worden uitgevoerd in Hallo cloud, op Hallo bureaublad, op een on-premises server of op een mobiel apparaat. Queue Storage biedt daarnaast ondersteuning voor het beheren van asynchrone taken en het samenstellen van proceswerkstromen.

### <a name="about-this-tutorial"></a>Over deze zelfstudie
Deze zelfstudie laat zien hoe toowrite .NET code van enkele algemene scenario's met Azure Queue storage. Scenario's die aan bod komen, zijn onder meer het maken en verwijderen van wachtrijen en het toevoegen, lezen en verwijderen van wachtrijberichten.

**Geschatte tijd toocomplete:** 45 minuten

**Vereisten:**

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Azure Storage-clientbibliotheek voor .NET](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [Azure Configuration Manager voor .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* Een [Azure Storage-account](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a>Using-instructies toevoegen
Voeg de volgende Hallo `using` richtlijnen toohello bovenaan Hallo `Program.cs` bestand:

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Queue; // Namespace for Queue storage types
```

### <a name="parse-hello-connection-string"></a>Hallo-verbindingsreeks parseren
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-queue-service-client"></a>Hallo Queue-serviceclient maken
Hallo **CloudQueueClient** klasse kunt u tooretrieve wachtrijen opgeslagen in Queue storage. Hier volgt een eenrichtingssessie toocreate Hallo-client-service:

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
```
    
U bent nu klaar toowrite-code die gegevens leest uit en schrijft tooQueue gegevensopslag.

## <a name="create-a-queue"></a>Een wachtrij maken
Dit voorbeeld ziet u hoe toocreate een wachtrij als deze niet al bestaat:

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa container.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create hello queue if it doesn't already exist
queue.CreateIfNotExists();
```

## <a name="insert-a-message-into-a-queue"></a>Een bericht in een wachtrij invoegen
een bericht in een bestaande wachtrij tooinsert eerst maakt u een nieuwe **CloudQueueMessage**. Daarna roept Hallo **AddMessage** methode. Een **CloudQueueMessage** kan worden gemaakt vanuit een tekenreeks (in UTF-8-indeling) of een **byte**matrix. Hier volgt de code die een wachtrij maakt (als deze niet bestaat) en voegt het Hallo-bericht 'Hello, World':

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create hello queue if it doesn't already exist.
queue.CreateIfNotExists();

// Create a message and add it toohello queue.
CloudQueueMessage message = new CloudQueueMessage("Hello, World");
queue.AddMessage(message);
```

## <a name="peek-at-hello-next-message"></a>Bekijken van volgende Hallo-bericht
U kunt bekijken van Hallo-bericht in Hallo begin van een wachtrij zonder het te verwijderen uit de wachtrij Hallo door aanroepen Hallo **PeekMessage** methode.

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Peek at hello next message
CloudQueueMessage peekedMessage = queue.PeekMessage();

// Display message.
Console.WriteLine(peekedMessage.AsString);
```

## <a name="change-hello-contents-of-a-queued-message"></a>Hallo-inhoud van een bericht in de wachtrij wijzigen
U kunt Hallo inhoud van een bericht in-place in Hallo wachtrij wijzigen. Als het bericht een werktaak vertegenwoordigt, kunt u deze functie tooupdate de status van de werktaak hello gebruiken. Hallo na code Hallo-bericht van wachtrij bijgewerkt met nieuwe inhoud en sets Hallo zichtbaarheid time-out tooextend 60 seconden. Hallo-status van de werkitems die zijn gekoppeld aan het Hallo-bericht opgeslagen, en geeft Hallo-client een andere minuut toocontinue werkt op het Hallo-bericht. U kunt deze techniek tootrack meerdere stappen bestaande werkstromen op Wachtrijberichten, zonder toostart via van Hallo begin als een verwerkingsstap vanwege problemen met toohardware of software. Doorgaans houdt u ook een aantal voor nieuwe pogingen en als hello bericht opnieuw wordt geprobeerd meer dan  *n*  tijdstippen, verwijdert u het. Dit biedt bescherming tegen berichten die een toepassingsfout activeren telkens wanneer ze worden verwerkt.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get hello message from hello queue and update hello message contents.
CloudQueueMessage message = queue.GetMessage();
message.SetMessageContent("Updated contents.");
queue.UpdateMessage(message,
    TimeSpan.FromSeconds(60.0),  // Make it invisible for another 60 seconds.
    MessageUpdateFields.Content | MessageUpdateFields.Visibility);
```

## <a name="de-queue-hello-next-message"></a>Het volgende Hallo-bericht uit de wachtrij
Met uw code wordt een bericht in twee stappen uit de wachtrij verwijderd. Als u aanroept **GetMessage**, krijgt u het volgende Hallo-bericht in een wachtrij. Een bericht dat wordt geretourneerd door **GetMessage** wordt onzichtbaar tooany andere codes die berichten lezen uit deze wachtrij. Standaard blijft het bericht onzichtbaar gedurende 30 seconden. toofinish verwijderen Hallo-bericht uit de wachtrij hello, moet u ook aanroepen **DeleteMessage**. Dit proces in twee stappen van het verwijderen van een bericht zorgt ervoor dat als uw code mislukt tooprocess een bericht vanwege problemen toohardware of software, een ander exemplaar van uw code krijgt hetzelfde bericht Hallo en probeer het opnieuw. Uw code haalt **DeleteMessage** direct nadat het Hallo-bericht is verwerkt.

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get hello next message
CloudQueueMessage retrievedMessage = queue.GetMessage();

//Process hello message in less than 30 seconds, and then delete hello message
queue.DeleteMessage(retrievedMessage);
```

## <a name="use-async-await-pattern-with-common-queue-storage-apis"></a>Het Async-Await-patroon gebruiken met algemene Queue Storage-API's
Dit voorbeeld toont hoe toouse Hallo Async-Await patroon met algemene Queue storage API's. Hallo voorbeeld roept Hallo asynchrone versie van elk Hallo opgegeven methoden, zoals aangegeven door Hallo *asynchrone* achtervoegsel van elke methode. Wanneer een async-methode wordt gebruikt, Hallo async-await patroon lokale uitvoering wordt onderbroken totdat het Hallo-aanroep is voltooid. Hierdoor kunnen de huidige thread toodo Hallo andere taken die knelpunten in de prestaties worden voorkomen en verbetert de algehele respons van uw toepassing hello. Zie voor meer informatie over het gebruik van Hallo Async-Await-patroon in .NET [Async en Await (C# en Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)

```csharp
// Create hello queue if it doesn't already exist
if(await queue.CreateIfNotExistsAsync())
{
    Console.WriteLine("Queue '{0}' Created", queue.Name);
}
else
{
    Console.WriteLine("Queue '{0}' Exists", queue.Name);
}

// Create a message tooput in hello queue
CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

// Async enqueue hello message
await queue.AddMessageAsync(cloudQueueMessage);
Console.WriteLine("Message added");

// Async dequeue hello message
CloudQueueMessage retrievedMessage = await queue.GetMessageAsync();
Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

// Async delete hello message
await queue.DeleteMessageAsync(retrievedMessage);
Console.WriteLine("Deleted message");
```
    
## <a name="leverage-additional-options-for-de-queuing-messages"></a>Gebruikmaken van aanvullende opties voor het verwijderen van berichten uit de wachtrij
Er zijn twee manieren waarop u het ophalen van berichten uit een wachtrij kunt aanpassen.
U krijgt eerst een batch met berichten (omhoog too32). Ten tweede kunt u instellen een time-out voor onzichtbaarheid langer of korter, zodat uw code meer of minder tijd toofully elk bericht niet verwerken. Hallo volgende codevoorbeeld wordt de **GetMessages** methode tooget 20 berichten in één aanroep. Vervolgens wordt elk bericht verwerkt met behulp van een **foreach**-lus. Hallo onzichtbaarheid toofive minuten voor de time-out voor elk bericht wordt ook ingesteld. Houd er rekening mee dat Hallo 5 minuten voor alle berichten op Hallo dezelfde time begint, betekent dat als er 5 minuten zijn verstreken sinds de aanroep hello te**GetMessages**, alle berichten die niet zijn verwijderd weer zichtbaar worden.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

foreach (CloudQueueMessage message in queue.GetMessages(20, TimeSpan.FromMinutes(5)))
{
    // Process all messages in less than 5 minutes, deleting each message after processing.
    queue.DeleteMessage(message);
}
```

## <a name="get-hello-queue-length"></a>Hallo-wachtrijlengte ophalen
U kunt een schatting maken van het aantal berichten Hallo krijgen in een wachtrij. De **FetchAttributes** methode vraagt de Queue-service Hallo Hallo wachtrij-kenmerken, zoals aantal Hallo-berichten ophalen. Hallo **ApproximateMessageCount** eigenschap retourneert de laatste waarde Hallo opgehaald door de **FetchAttributes** methode zonder Hallo Queue-service aanroepen.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Fetch hello queue attributes.
queue.FetchAttributes();

// Retrieve hello cached approximate message count.
int? cachedMessageCount = queue.ApproximateMessageCount;

// Display number of messages.
Console.WriteLine("Number of messages in queue: " + cachedMessageCount);
```

## <a name="delete-a-queue"></a>Een wachtrij verwijderen
toodelete een wachtrij en alle Hallo-berichten die dit, neemt u contact de **verwijderen** methode op Hallo wachtrij-object.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Delete hello queue.
queue.Delete();
```
    

## <a name="next-steps"></a>Volgende stappen
Nu u Hallo basisprincipes van Queue storage hebt geleerd, volgt u deze koppelingen toolearn over complexere opslagtaken.

* Weergave Hallo wachtrij-naslagdocumentatie voor meer informatie over beschikbare API's:
  * [Naslaginformatie over de Storage-clientbibliotheek voor .NET](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
  * [Naslaginformatie over de REST-API](http://msdn.microsoft.com/library/azure/dd179355)
* Meer informatie over hoe u toosimplify Hallo code schrijft toowork met Azure Storage met behulp van Hallo [Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md).
* Bekijk meer functie handleidingen toolearn over aanvullende mogelijkheden voor het opslaan van gegevens in Azure.
  * [Aan de slag met Azure Table storage met .NET](storage-dotnet-how-to-use-tables.md) toostore gestructureerde gegevens.
  * [Aan de slag met Azure Blob storage met .NET](storage-dotnet-how-to-use-blobs.md) toostore ongestructureerde gegevens.
  * [Verbinding maken met tooSQL Database met behulp van .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md) toostore relationele gegevens.

[Download and install hello Azure SDK for .NET]: /develop/net/
[.NET client library reference]: http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409
[Creating a Azure Project in Visual Studio]: http://msdn.microsoft.com/library/azure/ee405487.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[OData]: http://nuget.org/packages/Microsoft.Data.OData/5.0.2
[Edm]: http://nuget.org/packages/Microsoft.Data.Edm/5.0.2
[Spatial]: http://nuget.org/packages/System.Spatial/5.0.2
