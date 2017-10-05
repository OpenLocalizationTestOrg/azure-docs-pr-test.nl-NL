---
title: Aan de slag met Azure Queue Storage met .NET | Microsoft Docs
description: Azure Queues biedt betrouwbare, asynchrone uitwisseling van berichten tussen toepassingsonderdelen. Met Cloud Messaging kunnen onderdelen van uw toepassing onafhankelijk van elkaar worden opgeschaald.
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
ms.openlocfilehash: 7f88aa9c50e669d1be7248346c7b1176bce61249
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-azure-queue-storage-using-net"></a><span data-ttu-id="21356-104">Aan de slag met Azure Queue Storage met .NET</span><span class="sxs-lookup"><span data-stu-id="21356-104">Get started with Azure Queue storage using .NET</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

## <a name="overview"></a><span data-ttu-id="21356-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="21356-105">Overview</span></span>
<span data-ttu-id="21356-106">Azure Queue Storage biedt uitwisseling van berichten tussen toepassingsonderdelen in de cloud.</span><span class="sxs-lookup"><span data-stu-id="21356-106">Azure Queue storage provides cloud messaging between application components.</span></span> <span data-ttu-id="21356-107">Bij het ontwerpen van schaalbare toepassingen worden toepassingsonderdelen vaak ontkoppeld, zodat ze onafhankelijk van elkaar kunnen worden geschaald.</span><span class="sxs-lookup"><span data-stu-id="21356-107">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span></span> <span data-ttu-id="21356-108">Queue Storage biedt asynchrone uitwisseling van berichten voor communicatie tussen toepassingsonderdelen, of deze nu worden uitgevoerd in de cloud, op een desktopcomputer, op een on-premises server of op een mobiel apparaat.</span><span class="sxs-lookup"><span data-stu-id="21356-108">Queue storage delivers asynchronous messaging for communication between application components, whether they are running in the cloud, on the desktop, on an on-premises server, or on a mobile device.</span></span> <span data-ttu-id="21356-109">Queue Storage biedt daarnaast ondersteuning voor het beheren van asynchrone taken en het samenstellen van proceswerkstromen.</span><span class="sxs-lookup"><span data-stu-id="21356-109">Queue storage also supports managing asynchronous tasks and building process work flows.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="21356-110">Over deze zelfstudie</span><span class="sxs-lookup"><span data-stu-id="21356-110">About this tutorial</span></span>
<span data-ttu-id="21356-111">Deze zelfstudie laat zien hoe u .NET-code kunt schrijven voor een aantal algemene scenario's die gebruikmaken van Azure Queue Storage.</span><span class="sxs-lookup"><span data-stu-id="21356-111">This tutorial shows how to write .NET code for some common scenarios using Azure Queue storage.</span></span> <span data-ttu-id="21356-112">Scenario's die aan bod komen, zijn onder meer het maken en verwijderen van wachtrijen en het toevoegen, lezen en verwijderen van wachtrijberichten.</span><span class="sxs-lookup"><span data-stu-id="21356-112">Scenarios covered include creating and deleting queues and adding, reading, and deleting queue messages.</span></span>

<span data-ttu-id="21356-113">**Geschatte duur:** 45 minuten</span><span class="sxs-lookup"><span data-stu-id="21356-113">**Estimated time to complete:** 45 minutes</span></span>

<span data-ttu-id="21356-114">**Vereisten:**</span><span class="sxs-lookup"><span data-stu-id="21356-114">**Prerequisities:**</span></span>

* [<span data-ttu-id="21356-115">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="21356-115">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="21356-116">Azure Storage-clientbibliotheek voor .NET</span><span class="sxs-lookup"><span data-stu-id="21356-116">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="21356-117">Azure Configuration Manager voor .NET</span><span class="sxs-lookup"><span data-stu-id="21356-117">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* <span data-ttu-id="21356-118">Een [Azure Storage-account](storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="21356-118">An [Azure storage account](storage-create-storage-account.md#create-a-storage-account)</span></span>

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="21356-119">Using-instructies toevoegen</span><span class="sxs-lookup"><span data-stu-id="21356-119">Add using directives</span></span>
<span data-ttu-id="21356-120">Voeg de volgende `Program.cs`-instructies aan het begin van het bestand `using` toe:</span><span class="sxs-lookup"><span data-stu-id="21356-120">Add the following `using` directives to the top of the `Program.cs` file:</span></span>

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Queue; // Namespace for Queue storage types
```

### <a name="parse-the-connection-string"></a><span data-ttu-id="21356-121">De verbindingsreeks parseren</span><span class="sxs-lookup"><span data-stu-id="21356-121">Parse the connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-the-queue-service-client"></a><span data-ttu-id="21356-122">De Queue-serviceclient maken</span><span class="sxs-lookup"><span data-stu-id="21356-122">Create the Queue service client</span></span>
<span data-ttu-id="21356-123">Met de **CloudQueueClient**-klasse kunt u wachtrijen ophalen die zijn opgeslagen in Queue Storage.</span><span class="sxs-lookup"><span data-stu-id="21356-123">The **CloudQueueClient** class enables you to retrieve queues stored in Queue storage.</span></span> <span data-ttu-id="21356-124">Hier volgt één manier om de serviceclient te maken:</span><span class="sxs-lookup"><span data-stu-id="21356-124">Here's one way to create the service client:</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
```
    
<span data-ttu-id="21356-125">U bent nu klaar om code te schrijven die gegevens leest uit en schrijft naar Queue Storage.</span><span class="sxs-lookup"><span data-stu-id="21356-125">Now you are ready to write code that reads data from and writes data to Queue storage.</span></span>

## <a name="create-a-queue"></a><span data-ttu-id="21356-126">Een wachtrij maken</span><span class="sxs-lookup"><span data-stu-id="21356-126">Create a queue</span></span>
<span data-ttu-id="21356-127">In dit voorbeeld ziet u hoe u een wachtrij kunt maken als deze nog niet bestaat:</span><span class="sxs-lookup"><span data-stu-id="21356-127">This example shows how to create a queue if it does not already exist:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a container.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create the queue if it doesn't already exist
queue.CreateIfNotExists();
```

## <a name="insert-a-message-into-a-queue"></a><span data-ttu-id="21356-128">Een bericht in een wachtrij invoegen</span><span class="sxs-lookup"><span data-stu-id="21356-128">Insert a message into a queue</span></span>
<span data-ttu-id="21356-129">Voor het invoegen van een bericht in een bestaande wachtrij maakt u eerst een nieuwe **CloudQueueMessage**.</span><span class="sxs-lookup"><span data-stu-id="21356-129">To insert a message into an existing queue, first create a new **CloudQueueMessage**.</span></span> <span data-ttu-id="21356-130">Daarna roept u de methode **AddMessage** aan.</span><span class="sxs-lookup"><span data-stu-id="21356-130">Next, call the **AddMessage** method.</span></span> <span data-ttu-id="21356-131">Een **CloudQueueMessage** kan worden gemaakt vanuit een tekenreeks (in UTF-8-indeling) of een **byte**matrix.</span><span class="sxs-lookup"><span data-stu-id="21356-131">A **CloudQueueMessage** can be created from either a string (in UTF-8 format) or a **byte** array.</span></span> <span data-ttu-id="21356-132">Met deze code wordt er een wachtrij gemaakt (als deze nog niet bestaat) en het bericht 'Hello, World' toegevoegd:</span><span class="sxs-lookup"><span data-stu-id="21356-132">Here is code which creates a queue (if it doesn't exist) and inserts the message 'Hello, World':</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create the queue if it doesn't already exist.
queue.CreateIfNotExists();

// Create a message and add it to the queue.
CloudQueueMessage message = new CloudQueueMessage("Hello, World");
queue.AddMessage(message);
```

## <a name="peek-at-the-next-message"></a><span data-ttu-id="21356-133">Bekijken van het volgende bericht</span><span class="sxs-lookup"><span data-stu-id="21356-133">Peek at the next message</span></span>
<span data-ttu-id="21356-134">U kunt het bericht vooraan in een wachtrij bekijken zonder het uit de wachtrij te verwijderen, door de methode **PeekMessage** aan te roepen.</span><span class="sxs-lookup"><span data-stu-id="21356-134">You can peek at the message in the front of a queue without removing it from the queue by calling the **PeekMessage** method.</span></span>

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Peek at the next message
CloudQueueMessage peekedMessage = queue.PeekMessage();

// Display message.
Console.WriteLine(peekedMessage.AsString);
```

## <a name="change-the-contents-of-a-queued-message"></a><span data-ttu-id="21356-135">De inhoud van een bericht in de wachtrij wijzigen</span><span class="sxs-lookup"><span data-stu-id="21356-135">Change the contents of a queued message</span></span>
<span data-ttu-id="21356-136">U kunt de inhoud van een bericht in de wachtrij wijzigen.</span><span class="sxs-lookup"><span data-stu-id="21356-136">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="21356-137">Als het bericht een werktaak vertegenwoordigt, kunt u deze functie gebruiken om de status van de werktaak bij te werken.</span><span class="sxs-lookup"><span data-stu-id="21356-137">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="21356-138">Met de volgende code wordt het bericht in de wachtrij bijgewerkt met nieuwe inhoud en wordt de time-out voor de zichtbaarheid met 60 seconden verlengd.</span><span class="sxs-lookup"><span data-stu-id="21356-138">The following code updates the queue message with new contents, and sets the visibility timeout to extend another 60 seconds.</span></span> <span data-ttu-id="21356-139">Hiermee wordt de status van de werkitems die aan het bericht zijn gekoppeld, opgeslagen en krijgt de client een extra minuut om aan het bericht te blijven werken.</span><span class="sxs-lookup"><span data-stu-id="21356-139">This saves the state of work associated with the message, and gives the client another minute to continue working on the message.</span></span> <span data-ttu-id="21356-140">U kunt deze techniek gebruiken om uit meerdere stappen bestaande werkstromen in berichten in de wachtrij te volgen zonder dat u helemaal opnieuw hoeft te beginnen als een verwerkingsstap vanwege een hardware- of softwarefout is mislukt.</span><span class="sxs-lookup"><span data-stu-id="21356-140">You could use this technique to track multi-step workflows on queue messages, without having to start over from the beginning if a processing step fails due to hardware or software failure.</span></span> <span data-ttu-id="21356-141">Doorgaans houdt u ook het aantal nieuwe pogingen bij en als het bericht meer dan *n* keer opnieuw is geprobeerd, verwijdert u het.</span><span class="sxs-lookup"><span data-stu-id="21356-141">Typically, you would keep a retry count as well, and if the message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="21356-142">Dit biedt bescherming tegen berichten die een toepassingsfout activeren telkens wanneer ze worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="21356-142">This protects against a message that triggers an application error each time it is processed.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get the message from the queue and update the message contents.
CloudQueueMessage message = queue.GetMessage();
message.SetMessageContent("Updated contents.");
queue.UpdateMessage(message,
    TimeSpan.FromSeconds(60.0),  // Make it invisible for another 60 seconds.
    MessageUpdateFields.Content | MessageUpdateFields.Visibility);
```

## <a name="de-queue-the-next-message"></a><span data-ttu-id="21356-143">Het volgende bericht uit de wachtrij verwijderen</span><span class="sxs-lookup"><span data-stu-id="21356-143">De-queue the next message</span></span>
<span data-ttu-id="21356-144">Met uw code wordt een bericht in twee stappen uit de wachtrij verwijderd.</span><span class="sxs-lookup"><span data-stu-id="21356-144">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="21356-145">Wanneer u **GetMessage** aanroept, wordt het volgende bericht in een wachtrij opgehaald.</span><span class="sxs-lookup"><span data-stu-id="21356-145">When you call **GetMessage**, you get the next message in a queue.</span></span> <span data-ttu-id="21356-146">Een bericht dat wordt geretourneerd door **GetMessage**, wordt onzichtbaar voor andere codes die berichten lezen uit deze wachtrij.</span><span class="sxs-lookup"><span data-stu-id="21356-146">A message returned from **GetMessage** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="21356-147">Standaard blijft het bericht onzichtbaar gedurende 30 seconden.</span><span class="sxs-lookup"><span data-stu-id="21356-147">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="21356-148">Om het bericht definitief uit de wachtrij te verwijderen, moet u ook **DeleteMessage** aanroepen.</span><span class="sxs-lookup"><span data-stu-id="21356-148">To finish removing the message from the queue, you must also call **DeleteMessage**.</span></span> <span data-ttu-id="21356-149">Dit proces in twee stappen voor het verwijderen van een bericht zorgt ervoor dat als de code er niet in slaagt een bericht te verwerken vanwege hardware- of softwareproblemen, een ander exemplaar van uw code hetzelfde bericht kan ophalen en het opnieuw kan proberen.</span><span class="sxs-lookup"><span data-stu-id="21356-149">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="21356-150">Uw code haalt **DeleteMessage** op zodra het bericht is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="21356-150">Your code calls **DeleteMessage** right after the message has been processed.</span></span>

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get the next message
CloudQueueMessage retrievedMessage = queue.GetMessage();

//Process the message in less than 30 seconds, and then delete the message
queue.DeleteMessage(retrievedMessage);
```

## <a name="use-async-await-pattern-with-common-queue-storage-apis"></a><span data-ttu-id="21356-151">Het Async-Await-patroon gebruiken met algemene Queue Storage-API's</span><span class="sxs-lookup"><span data-stu-id="21356-151">Use Async-Await pattern with common Queue storage APIs</span></span>
<span data-ttu-id="21356-152">Dit voorbeeld laat zien hoe u het Async-Await-patroon gebruikt met algemene Queue Storage-API's.</span><span class="sxs-lookup"><span data-stu-id="21356-152">This example shows how to use the Async-Await pattern with common Queue storage APIs.</span></span> <span data-ttu-id="21356-153">In het voorbeeld wordt de asynchrone versie aangeroepen van elk van de opgegeven methoden. Dit ziet u aan het achtervoegsel *Async* van elke methode.</span><span class="sxs-lookup"><span data-stu-id="21356-153">The sample calls the asynchronous version of each of the given methods, as indicated by the *Async* suffix of each method.</span></span> <span data-ttu-id="21356-154">Wanneer er een asynchrone methode wordt gebruikt, schort het Async-Await-patroon lokale uitvoering uit totdat de aanroep is voltooid.</span><span class="sxs-lookup"><span data-stu-id="21356-154">When an async method is used, the async-await pattern suspends local execution until the call completes.</span></span> <span data-ttu-id="21356-155">Dit gedrag stelt de huidige thread in staat andere bewerkingen uit te voeren, zodat knelpunten in de prestaties worden voorkomen en de algehele respons van uw toepassing verbetert.</span><span class="sxs-lookup"><span data-stu-id="21356-155">This behavior allows the current thread to do other work, which helps avoid performance bottlenecks and improves the overall responsiveness of your application.</span></span> <span data-ttu-id="21356-156">Zie [Async en Await (C# en Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx) voor meer informatie over het gebruik van het Async-Await-patroon in .NET.</span><span class="sxs-lookup"><span data-stu-id="21356-156">For more details on using the Async-Await pattern in .NET see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

```csharp
// Create the queue if it doesn't already exist
if(await queue.CreateIfNotExistsAsync())
{
    Console.WriteLine("Queue '{0}' Created", queue.Name);
}
else
{
    Console.WriteLine("Queue '{0}' Exists", queue.Name);
}

// Create a message to put in the queue
CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

// Async enqueue the message
await queue.AddMessageAsync(cloudQueueMessage);
Console.WriteLine("Message added");

// Async dequeue the message
CloudQueueMessage retrievedMessage = await queue.GetMessageAsync();
Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

// Async delete the message
await queue.DeleteMessageAsync(retrievedMessage);
Console.WriteLine("Deleted message");
```
    
## <a name="leverage-additional-options-for-de-queuing-messages"></a><span data-ttu-id="21356-157">Gebruikmaken van aanvullende opties voor het verwijderen van berichten uit de wachtrij</span><span class="sxs-lookup"><span data-stu-id="21356-157">Leverage additional options for de-queuing messages</span></span>
<span data-ttu-id="21356-158">Er zijn twee manieren waarop u het ophalen van berichten uit een wachtrij kunt aanpassen.</span><span class="sxs-lookup"><span data-stu-id="21356-158">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="21356-159">Ten eerste kunt u berichten batchgewijs (maximaal 32) ophalen.</span><span class="sxs-lookup"><span data-stu-id="21356-159">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="21356-160">Ten tweede kunt u een langere of kortere time-out voor onzichtbaarheid instellen, zodat uw code meer of minder tijd krijgt voor het volledig verwerken van elk bericht.</span><span class="sxs-lookup"><span data-stu-id="21356-160">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="21356-161">In het volgende codevoorbeeld wordt de methode **GetMessages** gebruikt om 20 berichten in één aanroep op te halen.</span><span class="sxs-lookup"><span data-stu-id="21356-161">The following code example uses the **GetMessages** method to get 20 messages in one call.</span></span> <span data-ttu-id="21356-162">Vervolgens wordt elk bericht verwerkt met behulp van een **foreach**-lus.</span><span class="sxs-lookup"><span data-stu-id="21356-162">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="21356-163">De time-out voor onzichtbaarheid wordt ingesteld op vijf minuten voor elk bericht.</span><span class="sxs-lookup"><span data-stu-id="21356-163">It also sets the invisibility timeout to five minutes for each message.</span></span> <span data-ttu-id="21356-164">Houd voor ogen dat de periode van 5 minuten voor alle berichten op hetzelfde moment start. Nadat er 5 minuten zijn verstreken sinds de aanroep van **GetMessages**, worden dus alle berichten die niet zijn verwijderd, opnieuw zichtbaar.</span><span class="sxs-lookup"><span data-stu-id="21356-164">Note that the 5 minutes starts for all messages at the same time, so after 5 minutes have passed since the call to **GetMessages**, any messages which have not been deleted will become visible again.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

foreach (CloudQueueMessage message in queue.GetMessages(20, TimeSpan.FromMinutes(5)))
{
    // Process all messages in less than 5 minutes, deleting each message after processing.
    queue.DeleteMessage(message);
}
```

## <a name="get-the-queue-length"></a><span data-ttu-id="21356-165">Lengte van de wachtrij ophalen</span><span class="sxs-lookup"><span data-stu-id="21356-165">Get the queue length</span></span>
<span data-ttu-id="21356-166">U kunt een schatting ophalen van het aantal berichten in de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="21356-166">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="21356-167">De methode **FetchAttributes** vraagt de Queue-service de wachtrij-kenmerken, zoals het aantal berichten, op te halen.</span><span class="sxs-lookup"><span data-stu-id="21356-167">The **FetchAttributes** method asks the Queue service to retrieve the queue attributes, including the message count.</span></span> <span data-ttu-id="21356-168">De eigenschap **ApproximateMessageCount** retourneert de laatste waarde die is opgehaald door de methode **FetchAttributes**, zonder de Queue-service aan te roepen.</span><span class="sxs-lookup"><span data-stu-id="21356-168">The **ApproximateMessageCount** property returns the last value retrieved by the **FetchAttributes** method, without calling the Queue service.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Fetch the queue attributes.
queue.FetchAttributes();

// Retrieve the cached approximate message count.
int? cachedMessageCount = queue.ApproximateMessageCount;

// Display number of messages.
Console.WriteLine("Number of messages in queue: " + cachedMessageCount);
```

## <a name="delete-a-queue"></a><span data-ttu-id="21356-169">Een wachtrij verwijderen</span><span class="sxs-lookup"><span data-stu-id="21356-169">Delete a queue</span></span>
<span data-ttu-id="21356-170">Als u een wachtrij en alle berichten hierin wilt verwijderen, roept u de methode **Delete** aan in het wachtrijobject.</span><span class="sxs-lookup"><span data-stu-id="21356-170">To delete a queue and all the messages contained in it, call the **Delete** method on the queue object.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Delete the queue.
queue.Delete();
```
    

## <a name="next-steps"></a><span data-ttu-id="21356-171">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="21356-171">Next steps</span></span>
<span data-ttu-id="21356-172">Nu u de basisprincipes van Queue Storage hebt geleerd, volgt u deze koppelingen voor meer informatie over complexere opslagtaken.</span><span class="sxs-lookup"><span data-stu-id="21356-172">Now that you've learned the basics of Queue storage, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="21356-173">Bekijk de naslagdocumentatie over de Queue-service voor meer informatie over beschikbare API's:</span><span class="sxs-lookup"><span data-stu-id="21356-173">View the Queue service reference documentation for complete details about available APIs:</span></span>
  * [<span data-ttu-id="21356-174">Naslaginformatie over de Storage-clientbibliotheek voor .NET</span><span class="sxs-lookup"><span data-stu-id="21356-174">Storage Client Library for .NET reference</span></span>](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
  * [<span data-ttu-id="21356-175">Naslaginformatie over REST API</span><span class="sxs-lookup"><span data-stu-id="21356-175">REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="21356-176">Leer hoe u de code die u schrijft om te werken met Azure Storage, kunt vereenvoudigen met behulp van de [Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="21356-176">Learn how to simplify the code you write to work with Azure Storage by using the [Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md).</span></span>
* <span data-ttu-id="21356-177">Bekijk meer functiehandleidingen voor informatie over aanvullende mogelijkheden voor het opslaan van gegevens in Azure.</span><span class="sxs-lookup"><span data-stu-id="21356-177">View more feature guides to learn about additional options for storing data in Azure.</span></span>
  * <span data-ttu-id="21356-178">[Aan de slag met Azure Table Storage met .NET](storage-dotnet-how-to-use-tables.md) voor het opslaan van gestructureerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="21356-178">[Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md) to store structured data.</span></span>
  * <span data-ttu-id="21356-179">[Aan de slag met Azure Blob Storage met .NET](storage-dotnet-how-to-use-blobs.md) voor het opslaan van niet-gestructureerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="21356-179">[Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) to store unstructured data.</span></span>
  * <span data-ttu-id="21356-180">[Verbinding maken met SQL Database met behulp van .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md) voor het opslaan van relationele gegevens.</span><span class="sxs-lookup"><span data-stu-id="21356-180">[Connect to SQL Database by using .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md) to store relational data.</span></span>

[Download and install the Azure SDK for .NET]: /develop/net/
[.NET client library reference]: http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409
[Creating a Azure Project in Visual Studio]: http://msdn.microsoft.com/library/azure/ee405487.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[OData]: http://nuget.org/packages/Microsoft.Data.OData/5.0.2
[Edm]: http://nuget.org/packages/Microsoft.Data.Edm/5.0.2
[Spatial]: http://nuget.org/packages/System.Spatial/5.0.2
