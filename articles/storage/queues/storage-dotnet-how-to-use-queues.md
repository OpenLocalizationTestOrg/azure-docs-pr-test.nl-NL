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
ms.openlocfilehash: 0cf6a71392b2fe859c7c9a9898c1ec84bcab4b19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-queue-storage-using-net"></a><span data-ttu-id="88fec-104">Aan de slag met Azure Queue Storage met .NET</span><span class="sxs-lookup"><span data-stu-id="88fec-104">Get started with Azure Queue storage using .NET</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

## <a name="overview"></a><span data-ttu-id="88fec-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="88fec-105">Overview</span></span>
<span data-ttu-id="88fec-106">Azure Queue Storage biedt uitwisseling van berichten tussen toepassingsonderdelen in de cloud.</span><span class="sxs-lookup"><span data-stu-id="88fec-106">Azure Queue storage provides cloud messaging between application components.</span></span> <span data-ttu-id="88fec-107">Bij het ontwerpen van schaalbare toepassingen worden toepassingsonderdelen vaak ontkoppeld, zodat ze onafhankelijk van elkaar kunnen worden geschaald.</span><span class="sxs-lookup"><span data-stu-id="88fec-107">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span></span> <span data-ttu-id="88fec-108">Queue storage biedt asynchrone messaging voor communicatie tussen toepassingsonderdelen, of ze worden uitgevoerd in Hallo cloud, op Hallo bureaublad, op een on-premises server of op een mobiel apparaat.</span><span class="sxs-lookup"><span data-stu-id="88fec-108">Queue storage delivers asynchronous messaging for communication between application components, whether they are running in hello cloud, on hello desktop, on an on-premises server, or on a mobile device.</span></span> <span data-ttu-id="88fec-109">Queue Storage biedt daarnaast ondersteuning voor het beheren van asynchrone taken en het samenstellen van proceswerkstromen.</span><span class="sxs-lookup"><span data-stu-id="88fec-109">Queue storage also supports managing asynchronous tasks and building process work flows.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="88fec-110">Over deze zelfstudie</span><span class="sxs-lookup"><span data-stu-id="88fec-110">About this tutorial</span></span>
<span data-ttu-id="88fec-111">Deze zelfstudie laat zien hoe toowrite .NET code van enkele algemene scenario's met Azure Queue storage.</span><span class="sxs-lookup"><span data-stu-id="88fec-111">This tutorial shows how toowrite .NET code for some common scenarios using Azure Queue storage.</span></span> <span data-ttu-id="88fec-112">Scenario's die aan bod komen, zijn onder meer het maken en verwijderen van wachtrijen en het toevoegen, lezen en verwijderen van wachtrijberichten.</span><span class="sxs-lookup"><span data-stu-id="88fec-112">Scenarios covered include creating and deleting queues and adding, reading, and deleting queue messages.</span></span>

<span data-ttu-id="88fec-113">**Geschatte tijd toocomplete:** 45 minuten</span><span class="sxs-lookup"><span data-stu-id="88fec-113">**Estimated time toocomplete:** 45 minutes</span></span>

<span data-ttu-id="88fec-114">**Vereisten:**</span><span class="sxs-lookup"><span data-stu-id="88fec-114">**Prerequisities:**</span></span>

* [<span data-ttu-id="88fec-115">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="88fec-115">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="88fec-116">Azure Storage-clientbibliotheek voor .NET</span><span class="sxs-lookup"><span data-stu-id="88fec-116">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="88fec-117">Azure Configuration Manager voor .NET</span><span class="sxs-lookup"><span data-stu-id="88fec-117">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* <span data-ttu-id="88fec-118">Een [Azure Storage-account](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="88fec-118">An [Azure storage account](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json#create-a-storage-account)</span></span>

[!INCLUDE [storage-dotnet-client-library-version-include](../../../includes/storage-dotnet-client-library-version-include.md)]

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="88fec-119">Using-instructies toevoegen</span><span class="sxs-lookup"><span data-stu-id="88fec-119">Add using directives</span></span>
<span data-ttu-id="88fec-120">Voeg de volgende Hallo `using` richtlijnen toohello bovenaan Hallo `Program.cs` bestand:</span><span class="sxs-lookup"><span data-stu-id="88fec-120">Add hello following `using` directives toohello top of hello `Program.cs` file:</span></span>

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Queue; // Namespace for Queue storage types
```

### <a name="parse-hello-connection-string"></a><span data-ttu-id="88fec-121">Hallo-verbindingsreeks parseren</span><span class="sxs-lookup"><span data-stu-id="88fec-121">Parse hello connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-queue-service-client"></a><span data-ttu-id="88fec-122">Hallo Queue-serviceclient maken</span><span class="sxs-lookup"><span data-stu-id="88fec-122">Create hello Queue service client</span></span>
<span data-ttu-id="88fec-123">Hallo **CloudQueueClient** klasse kunt u tooretrieve wachtrijen opgeslagen in Queue storage.</span><span class="sxs-lookup"><span data-stu-id="88fec-123">hello **CloudQueueClient** class enables you tooretrieve queues stored in Queue storage.</span></span> <span data-ttu-id="88fec-124">Hier volgt een eenrichtingssessie toocreate Hallo-client-service:</span><span class="sxs-lookup"><span data-stu-id="88fec-124">Here's one way toocreate hello service client:</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
```
    
<span data-ttu-id="88fec-125">U bent nu klaar toowrite-code die gegevens leest uit en schrijft tooQueue gegevensopslag.</span><span class="sxs-lookup"><span data-stu-id="88fec-125">Now you are ready toowrite code that reads data from and writes data tooQueue storage.</span></span>

## <a name="create-a-queue"></a><span data-ttu-id="88fec-126">Een wachtrij maken</span><span class="sxs-lookup"><span data-stu-id="88fec-126">Create a queue</span></span>
<span data-ttu-id="88fec-127">Dit voorbeeld ziet u hoe toocreate een wachtrij als deze niet al bestaat:</span><span class="sxs-lookup"><span data-stu-id="88fec-127">This example shows how toocreate a queue if it does not already exist:</span></span>

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

## <a name="insert-a-message-into-a-queue"></a><span data-ttu-id="88fec-128">Een bericht in een wachtrij invoegen</span><span class="sxs-lookup"><span data-stu-id="88fec-128">Insert a message into a queue</span></span>
<span data-ttu-id="88fec-129">een bericht in een bestaande wachtrij tooinsert eerst maakt u een nieuwe **CloudQueueMessage**.</span><span class="sxs-lookup"><span data-stu-id="88fec-129">tooinsert a message into an existing queue, first create a new **CloudQueueMessage**.</span></span> <span data-ttu-id="88fec-130">Daarna roept Hallo **AddMessage** methode.</span><span class="sxs-lookup"><span data-stu-id="88fec-130">Next, call hello **AddMessage** method.</span></span> <span data-ttu-id="88fec-131">Een **CloudQueueMessage** kan worden gemaakt vanuit een tekenreeks (in UTF-8-indeling) of een **byte**matrix.</span><span class="sxs-lookup"><span data-stu-id="88fec-131">A **CloudQueueMessage** can be created from either a string (in UTF-8 format) or a **byte** array.</span></span> <span data-ttu-id="88fec-132">Hier volgt de code die een wachtrij maakt (als deze niet bestaat) en voegt het Hallo-bericht 'Hello, World':</span><span class="sxs-lookup"><span data-stu-id="88fec-132">Here is code which creates a queue (if it doesn't exist) and inserts hello message 'Hello, World':</span></span>

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

## <a name="peek-at-hello-next-message"></a><span data-ttu-id="88fec-133">Bekijken van volgende Hallo-bericht</span><span class="sxs-lookup"><span data-stu-id="88fec-133">Peek at hello next message</span></span>
<span data-ttu-id="88fec-134">U kunt bekijken van Hallo-bericht in Hallo begin van een wachtrij zonder het te verwijderen uit de wachtrij Hallo door aanroepen Hallo **PeekMessage** methode.</span><span class="sxs-lookup"><span data-stu-id="88fec-134">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **PeekMessage** method.</span></span>

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

## <a name="change-hello-contents-of-a-queued-message"></a><span data-ttu-id="88fec-135">Hallo-inhoud van een bericht in de wachtrij wijzigen</span><span class="sxs-lookup"><span data-stu-id="88fec-135">Change hello contents of a queued message</span></span>
<span data-ttu-id="88fec-136">U kunt Hallo inhoud van een bericht in-place in Hallo wachtrij wijzigen.</span><span class="sxs-lookup"><span data-stu-id="88fec-136">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="88fec-137">Als het bericht een werktaak vertegenwoordigt, kunt u deze functie tooupdate de status van de werktaak hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="88fec-137">If the message represents a work task, you could use this feature tooupdate the status of hello work task.</span></span> <span data-ttu-id="88fec-138">Hallo na code Hallo-bericht van wachtrij bijgewerkt met nieuwe inhoud en sets Hallo zichtbaarheid time-out tooextend 60 seconden.</span><span class="sxs-lookup"><span data-stu-id="88fec-138">hello following code updates hello queue message with new contents, and sets hello visibility timeout tooextend another 60 seconds.</span></span> <span data-ttu-id="88fec-139">Hallo-status van de werkitems die zijn gekoppeld aan het Hallo-bericht opgeslagen, en geeft Hallo-client een andere minuut toocontinue werkt op het Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="88fec-139">This saves hello state of work associated with hello message, and gives hello client another minute toocontinue working on hello message.</span></span> <span data-ttu-id="88fec-140">U kunt deze techniek tootrack meerdere stappen bestaande werkstromen op Wachtrijberichten, zonder toostart via van Hallo begin als een verwerkingsstap vanwege problemen met toohardware of software.</span><span class="sxs-lookup"><span data-stu-id="88fec-140">You could use this technique tootrack multi-step workflows on queue messages, without having toostart over from hello beginning if a processing step fails due toohardware or software failure.</span></span> <span data-ttu-id="88fec-141">Doorgaans houdt u ook een aantal voor nieuwe pogingen en als hello bericht opnieuw wordt geprobeerd meer dan  *n*  tijdstippen, verwijdert u het.</span><span class="sxs-lookup"><span data-stu-id="88fec-141">Typically, you would keep a retry count as well, and if hello message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="88fec-142">Dit biedt bescherming tegen berichten die een toepassingsfout activeren telkens wanneer ze worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="88fec-142">This protects against a message that triggers an application error each time it is processed.</span></span>

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

## <a name="de-queue-hello-next-message"></a><span data-ttu-id="88fec-143">Het volgende Hallo-bericht uit de wachtrij</span><span class="sxs-lookup"><span data-stu-id="88fec-143">De-queue hello next message</span></span>
<span data-ttu-id="88fec-144">Met uw code wordt een bericht in twee stappen uit de wachtrij verwijderd.</span><span class="sxs-lookup"><span data-stu-id="88fec-144">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="88fec-145">Als u aanroept **GetMessage**, krijgt u het volgende Hallo-bericht in een wachtrij.</span><span class="sxs-lookup"><span data-stu-id="88fec-145">When you call **GetMessage**, you get hello next message in a queue.</span></span> <span data-ttu-id="88fec-146">Een bericht dat wordt geretourneerd door **GetMessage** wordt onzichtbaar tooany andere codes die berichten lezen uit deze wachtrij.</span><span class="sxs-lookup"><span data-stu-id="88fec-146">A message returned from **GetMessage** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="88fec-147">Standaard blijft het bericht onzichtbaar gedurende 30 seconden.</span><span class="sxs-lookup"><span data-stu-id="88fec-147">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="88fec-148">toofinish verwijderen Hallo-bericht uit de wachtrij hello, moet u ook aanroepen **DeleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="88fec-148">toofinish removing hello message from hello queue, you must also call **DeleteMessage**.</span></span> <span data-ttu-id="88fec-149">Dit proces in twee stappen van het verwijderen van een bericht zorgt ervoor dat als uw code mislukt tooprocess een bericht vanwege problemen toohardware of software, een ander exemplaar van uw code krijgt hetzelfde bericht Hallo en probeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="88fec-149">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="88fec-150">Uw code haalt **DeleteMessage** direct nadat het Hallo-bericht is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="88fec-150">Your code calls **DeleteMessage** right after hello message has been processed.</span></span>

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

## <a name="use-async-await-pattern-with-common-queue-storage-apis"></a><span data-ttu-id="88fec-151">Het Async-Await-patroon gebruiken met algemene Queue Storage-API's</span><span class="sxs-lookup"><span data-stu-id="88fec-151">Use Async-Await pattern with common Queue storage APIs</span></span>
<span data-ttu-id="88fec-152">Dit voorbeeld toont hoe toouse Hallo Async-Await patroon met algemene Queue storage API's.</span><span class="sxs-lookup"><span data-stu-id="88fec-152">This example shows how toouse hello Async-Await pattern with common Queue storage APIs.</span></span> <span data-ttu-id="88fec-153">Hallo voorbeeld roept Hallo asynchrone versie van elk Hallo opgegeven methoden, zoals aangegeven door Hallo *asynchrone* achtervoegsel van elke methode.</span><span class="sxs-lookup"><span data-stu-id="88fec-153">hello sample calls hello asynchronous version of each of hello given methods, as indicated by hello *Async* suffix of each method.</span></span> <span data-ttu-id="88fec-154">Wanneer een async-methode wordt gebruikt, Hallo async-await patroon lokale uitvoering wordt onderbroken totdat het Hallo-aanroep is voltooid.</span><span class="sxs-lookup"><span data-stu-id="88fec-154">When an async method is used, hello async-await pattern suspends local execution until hello call completes.</span></span> <span data-ttu-id="88fec-155">Hierdoor kunnen de huidige thread toodo Hallo andere taken die knelpunten in de prestaties worden voorkomen en verbetert de algehele respons van uw toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="88fec-155">This behavior allows hello current thread toodo other work, which helps avoid performance bottlenecks and improves hello overall responsiveness of your application.</span></span> <span data-ttu-id="88fec-156">Zie voor meer informatie over het gebruik van Hallo Async-Await-patroon in .NET [Async en Await (C# en Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span><span class="sxs-lookup"><span data-stu-id="88fec-156">For more details on using hello Async-Await pattern in .NET see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

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
    
## <a name="leverage-additional-options-for-de-queuing-messages"></a><span data-ttu-id="88fec-157">Gebruikmaken van aanvullende opties voor het verwijderen van berichten uit de wachtrij</span><span class="sxs-lookup"><span data-stu-id="88fec-157">Leverage additional options for de-queuing messages</span></span>
<span data-ttu-id="88fec-158">Er zijn twee manieren waarop u het ophalen van berichten uit een wachtrij kunt aanpassen.</span><span class="sxs-lookup"><span data-stu-id="88fec-158">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="88fec-159">U krijgt eerst een batch met berichten (omhoog too32).</span><span class="sxs-lookup"><span data-stu-id="88fec-159">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="88fec-160">Ten tweede kunt u instellen een time-out voor onzichtbaarheid langer of korter, zodat uw code meer of minder tijd toofully elk bericht niet verwerken.</span><span class="sxs-lookup"><span data-stu-id="88fec-160">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="88fec-161">Hallo volgende codevoorbeeld wordt de **GetMessages** methode tooget 20 berichten in één aanroep.</span><span class="sxs-lookup"><span data-stu-id="88fec-161">hello following code example uses the **GetMessages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="88fec-162">Vervolgens wordt elk bericht verwerkt met behulp van een **foreach**-lus.</span><span class="sxs-lookup"><span data-stu-id="88fec-162">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="88fec-163">Hallo onzichtbaarheid toofive minuten voor de time-out voor elk bericht wordt ook ingesteld.</span><span class="sxs-lookup"><span data-stu-id="88fec-163">It also sets hello invisibility timeout toofive minutes for each message.</span></span> <span data-ttu-id="88fec-164">Houd er rekening mee dat Hallo 5 minuten voor alle berichten op Hallo dezelfde time begint, betekent dat als er 5 minuten zijn verstreken sinds de aanroep hello te**GetMessages**, alle berichten die niet zijn verwijderd weer zichtbaar worden.</span><span class="sxs-lookup"><span data-stu-id="88fec-164">Note that hello 5 minutes starts for all messages at hello same time, so after 5 minutes have passed since hello call too**GetMessages**, any messages which have not been deleted will become visible again.</span></span>

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

## <a name="get-hello-queue-length"></a><span data-ttu-id="88fec-165">Hallo-wachtrijlengte ophalen</span><span class="sxs-lookup"><span data-stu-id="88fec-165">Get hello queue length</span></span>
<span data-ttu-id="88fec-166">U kunt een schatting maken van het aantal berichten Hallo krijgen in een wachtrij.</span><span class="sxs-lookup"><span data-stu-id="88fec-166">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="88fec-167">De **FetchAttributes** methode vraagt de Queue-service Hallo Hallo wachtrij-kenmerken, zoals aantal Hallo-berichten ophalen.</span><span class="sxs-lookup"><span data-stu-id="88fec-167">The **FetchAttributes** method asks hello Queue service to retrieve hello queue attributes, including hello message count.</span></span> <span data-ttu-id="88fec-168">Hallo **ApproximateMessageCount** eigenschap retourneert de laatste waarde Hallo opgehaald door de **FetchAttributes** methode zonder Hallo Queue-service aanroepen.</span><span class="sxs-lookup"><span data-stu-id="88fec-168">hello **ApproximateMessageCount** property returns hello last value retrieved by the **FetchAttributes** method, without calling hello Queue service.</span></span>

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

## <a name="delete-a-queue"></a><span data-ttu-id="88fec-169">Een wachtrij verwijderen</span><span class="sxs-lookup"><span data-stu-id="88fec-169">Delete a queue</span></span>
<span data-ttu-id="88fec-170">toodelete een wachtrij en alle Hallo-berichten die dit, neemt u contact de **verwijderen** methode op Hallo wachtrij-object.</span><span class="sxs-lookup"><span data-stu-id="88fec-170">toodelete a queue and all hello messages contained in it, call the **Delete** method on hello queue object.</span></span>

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
    

## <a name="next-steps"></a><span data-ttu-id="88fec-171">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="88fec-171">Next steps</span></span>
<span data-ttu-id="88fec-172">Nu u Hallo basisprincipes van Queue storage hebt geleerd, volgt u deze koppelingen toolearn over complexere opslagtaken.</span><span class="sxs-lookup"><span data-stu-id="88fec-172">Now that you've learned hello basics of Queue storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="88fec-173">Weergave Hallo wachtrij-naslagdocumentatie voor meer informatie over beschikbare API's:</span><span class="sxs-lookup"><span data-stu-id="88fec-173">View hello Queue service reference documentation for complete details about available APIs:</span></span>
  * [<span data-ttu-id="88fec-174">Naslaginformatie over de Storage-clientbibliotheek voor .NET</span><span class="sxs-lookup"><span data-stu-id="88fec-174">Storage Client Library for .NET reference</span></span>](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
  * [<span data-ttu-id="88fec-175">Naslaginformatie over de REST-API</span><span class="sxs-lookup"><span data-stu-id="88fec-175">REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="88fec-176">Meer informatie over hoe u toosimplify Hallo code schrijft toowork met Azure Storage met behulp van Hallo [Azure WebJobs SDK](../../app-service-web/websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="88fec-176">Learn how toosimplify hello code you write toowork with Azure Storage by using hello [Azure WebJobs SDK](../../app-service-web/websites-dotnet-webjobs-sdk.md).</span></span>
* <span data-ttu-id="88fec-177">Bekijk meer functie handleidingen toolearn over aanvullende mogelijkheden voor het opslaan van gegevens in Azure.</span><span class="sxs-lookup"><span data-stu-id="88fec-177">View more feature guides toolearn about additional options for storing data in Azure.</span></span>
  * <span data-ttu-id="88fec-178">[Aan de slag met Azure Table storage met .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md) toostore gestructureerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="88fec-178">[Get started with Azure Table storage using .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md) toostore structured data.</span></span>
  * <span data-ttu-id="88fec-179">[Aan de slag met Azure Blob storage met .NET](../blobs/storage-dotnet-how-to-use-blobs.md) toostore ongestructureerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="88fec-179">[Get started with Azure Blob storage using .NET](../blobs/storage-dotnet-how-to-use-blobs.md) toostore unstructured data.</span></span>
  * <span data-ttu-id="88fec-180">[Verbinding maken met tooSQL Database met behulp van .NET (C#)](../../sql-database/sql-database-connect-query-dotnet-core.md) toostore relationele gegevens.</span><span class="sxs-lookup"><span data-stu-id="88fec-180">[Connect tooSQL Database by using .NET (C#)](../../sql-database/sql-database-connect-query-dotnet-core.md) toostore relational data.</span></span>

[Download and install hello Azure SDK for .NET]: /develop/net/
[.NET client library reference]: http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409
[Creating a Azure Project in Visual Studio]: http://msdn.microsoft.com/library/azure/ee405487.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[OData]: http://nuget.org/packages/Microsoft.Data.OData/5.0.2
[Edm]: http://nuget.org/packages/Microsoft.Data.Edm/5.0.2
[Spatial]: http://nuget.org/packages/System.Spatial/5.0.2
