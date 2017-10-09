---
title: aaaGet gestart met de opslag van de wachtrij en Visual Studio verbonden services (ASP.NET Core) | Microsoft Docs
description: Hoe tooget gestart met behulp van Azure queue storage in een ASP.NET Core-project in Visual Studio
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 04977069-5b2d-4cba-84ae-9fb2f5eb1006
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 75adb7163827ab17ad89707051ff0e48dbae9c3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-queue-storage-and-visual-studio-connected-services-aspnet-core"></a><span data-ttu-id="19321-103">Aan de slag met de opslag van de wachtrij en Visual Studio verbonden services (ASP.NET Core)</span><span class="sxs-lookup"><span data-stu-id="19321-103">Get started with queue storage and Visual Studio connected services (ASP.NET Core)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="19321-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="19321-104">Overview</span></span>
<span data-ttu-id="19321-105">Dit artikel wordt beschreven hoe tooget gestart met Azure Queue storage in Visual Studio nadat u hebt gemaakt of een Azure storage-account in een ASP.NET Core-project waarnaar wordt verwezen met behulp van Visual Studio Hallo **verbonden Services toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="19321-105">This article describes how tooget started using Azure Queue storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using hello Visual Studio **Add Connected Services** dialog.</span></span> <span data-ttu-id="19321-106">Hallo **verbonden Services toevoegen** bewerking installeert Hallo juiste NuGet-pakketten tooaccess Azure-opslag in uw project en voegt Hallo-verbindingsreeks voor hello storage account tooyour project configuratiebestanden.</span><span class="sxs-lookup"><span data-stu-id="19321-106">hello **Add Connected Services** operation installs hello appropriate NuGet packages tooaccess Azure storage in your project and adds hello connection string for hello storage account tooyour project configuration files.</span></span>

<span data-ttu-id="19321-107">Azure queue storage is een service voor het opslaan van grote aantallen berichten die toegankelijk zijn vanaf een willekeurige plaats in Hallo wereld via geverifieerde aanroepen via HTTP of HTTPS.</span><span class="sxs-lookup"><span data-stu-id="19321-107">Azure queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="19321-108">Een enkel wachtrijbericht mag up too64 kilobytes (KB) groot en een wachtrij kan miljoenen berichten up toohello totale capaciteitslimiet van een opslagaccount bevatten.</span><span class="sxs-lookup"><span data-stu-id="19321-108">A single queue message can be up too64 kilobytes (KB) in size, and a queue can contain millions of messages, up toohello total capacity limit of a storage account.</span></span>

<span data-ttu-id="19321-109">tooget gestart, moet u eerst een Azure-wachtrij toocreate in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="19321-109">tooget started, you first need toocreate an Azure queue in your storage account.</span></span> <span data-ttu-id="19321-110">Leert u hoe een wachtrij in code toocreate.</span><span class="sxs-lookup"><span data-stu-id="19321-110">We'll show you how toocreate a queue in code.</span></span> <span data-ttu-id="19321-111">Ook ziet u hoe tooperform basic wachtrij-bewerkingen, zoals het toevoegen, wijzigen, lezen en verwijderen van Wachtrijberichten.</span><span class="sxs-lookup"><span data-stu-id="19321-111">We'll also show you how tooperform basic queue operations, such as adding, modifying, reading, and removing queue messages.</span></span> <span data-ttu-id="19321-112">Hallo-voorbeelden zijn geschreven in C\# code en hello Azure Storage-clientbibliotheek voor .NET.</span><span class="sxs-lookup"><span data-stu-id="19321-112">hello samples are written in C\# code and use hello Azure Storage Client Library for .NET.</span></span> <span data-ttu-id="19321-113">Zie voor meer informatie over ASP.NET [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="19321-113">For more information about ASP.NET, see [ASP.NET](http://www.asp.net).</span></span>

<span data-ttu-id="19321-114">**Opmerking:** aantal Hallo API's die aanroepen tooAzure opslag in ASP.NET Core uitvoeren zijn asynchroon.</span><span class="sxs-lookup"><span data-stu-id="19321-114">**NOTE:** Some of hello APIs that perform calls tooAzure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="19321-115">Zie [asynchrone programmering met Async en Await](http://msdn.microsoft.com/library/hh191443.aspx) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="19321-115">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="19321-116">Hallo-code hieronder wordt ervan uitgegaan programming async-methoden worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="19321-116">hello code below assumes async programming methods are being used.</span></span>

* <span data-ttu-id="19321-117">Zie [aan de slag met Azure Queue storage met .NET](storage-dotnet-how-to-use-queues.md) voor meer informatie over het bewerken van programmatisch wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="19321-117">See [Get started with Azure Queue storage using .NET](storage-dotnet-how-to-use-queues.md) for more information on programmatically manipulating queues.</span></span>
* <span data-ttu-id="19321-118">Zie [documentatie Storage](https://azure.microsoft.com/documentation/services/storage/) voor algemene informatie over Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="19321-118">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="19321-119">Zie [Cloud Services-documentatie](https://azure.microsoft.com/documentation/services/cloud-services/) voor algemene informatie over Azure-cloudservices.</span><span class="sxs-lookup"><span data-stu-id="19321-119">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="19321-120">Zie [ASP.NET](http://www.asp.net) voor meer informatie over het programmeren van ASP.NET-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="19321-120">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

## <a name="access-queues-in-code"></a><span data-ttu-id="19321-121">Toegang tot wachtrijen in code</span><span class="sxs-lookup"><span data-stu-id="19321-121">Access queues in code</span></span>
<span data-ttu-id="19321-122">tooaccess wachtrijen in ASP.NET Core projecten, moet u tooinclude Hallo volgende items tooany C#-bronbestand dat Azure queue storage opent.</span><span class="sxs-lookup"><span data-stu-id="19321-122">tooaccess queues in ASP.NET Core projects, you need tooinclude hello following items tooany C# source file that accesses Azure queue storage.</span></span>

1. <span data-ttu-id="19321-123">Zorg ervoor dat de naamruimtedeclaraties Hallo Hallo bovenaan Hallo C#-bestand in deze **met** instructies.</span><span class="sxs-lookup"><span data-stu-id="19321-123">Make sure hello namespace declarations at hello top of hello C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="19321-124">Ophalen van een **CloudStorageAccount** -object met gegevens over uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="19321-124">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="19321-125">Gebruik Hallo na code tooget Hallo uw verbindingsreeks voor opslag en de accountgegevens van de opslag van Azure Hallo-serviceconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="19321-125">Use hello following code tooget hello your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. <span data-ttu-id="19321-126">Ophalen van een **CloudQueueClient** object tooreference Hallo wachtrij-objecten in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="19321-126">Get a **CloudQueueClient** object tooreference hello queue objects in your storage account.</span></span>  
   
        // Create hello CloudQueueClient object for hello storage account.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. <span data-ttu-id="19321-127">Ophalen van een **CloudQueue** tooreference een specifieke wachtrij-object.</span><span class="sxs-lookup"><span data-stu-id="19321-127">Get a **CloudQueue** object tooreference a specific queue.</span></span>
   
        // Get a reference toohello CloudQueue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

<span data-ttu-id="19321-128">**Opmerking:** alle Hallo bovenstaande code voor het Hallo-code in Hallo volgen voorbeelden gebruiken.</span><span class="sxs-lookup"><span data-stu-id="19321-128">**NOTE:** Use all of hello above code in front of hello code in hello following samples.</span></span>

### <a name="create-a-queue-in-code"></a><span data-ttu-id="19321-129">Een wachtrij in code maken</span><span class="sxs-lookup"><span data-stu-id="19321-129">Create a queue in code</span></span>
<span data-ttu-id="19321-130">toocreate hello Azure wachtrij in code, voegt u toe een aanroep te**CreateIfNotExistsAsync**.</span><span class="sxs-lookup"><span data-stu-id="19321-130">toocreate hello Azure queue in code, just add a call too**CreateIfNotExistsAsync**.</span></span>

    // Create hello CloudQueue if it does not exist.
    await messageQueue.CreateIfNotExistsAsync();

## <a name="add-a-message-tooa-queue"></a><span data-ttu-id="19321-131">Een berichtenwachtrij tooa toevoegen</span><span class="sxs-lookup"><span data-stu-id="19321-131">Add a message tooa queue</span></span>
<span data-ttu-id="19321-132">tooinsert een bericht in een bestaande wachtrij maakt u een nieuwe **CloudQueueMessage** object en vervolgens aanroep Hallo **AddMessageAsync** methode.</span><span class="sxs-lookup"><span data-stu-id="19321-132">tooinsert a message into an existing queue, create a new **CloudQueueMessage** object, then call hello **AddMessageAsync** method.</span></span>

<span data-ttu-id="19321-133">Een **CloudQueueMessage** object kan worden gemaakt vanuit een tekenreeks (in UTF-8-indeling) of een byte-matrix.</span><span class="sxs-lookup"><span data-stu-id="19321-133">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="19321-134">Hier volgt een voorbeeld waarmee het Hallo-bericht 'Hello, World' invoegt.</span><span class="sxs-lookup"><span data-stu-id="19321-134">Here is an example which inserts hello message 'Hello, World'.</span></span>

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    await messageQueue.AddMessageAsync(message);

## <a name="read-a-message-in-a-queue"></a><span data-ttu-id="19321-135">Een bericht in een wachtrij lezen</span><span class="sxs-lookup"><span data-stu-id="19321-135">Read a message in a queue</span></span>
<span data-ttu-id="19321-136">U kunt bekijken van Hallo-bericht in Hallo begin van een wachtrij zonder het te verwijderen uit de wachtrij Hallo door aanroepen Hallo **PeekMessageAsync** methode.</span><span class="sxs-lookup"><span data-stu-id="19321-136">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **PeekMessageAsync** method.</span></span>

    // Peek hello next message in hello queue. 
    CloudQueueMessage peekedMessage = await messageQueue.PeekMessageAsync();


## <a name="read-and-remove-a-message-in-a-queue"></a><span data-ttu-id="19321-137">Lezen en verwijderen van een bericht in een wachtrij</span><span class="sxs-lookup"><span data-stu-id="19321-137">Read and remove a message in a queue</span></span>
<span data-ttu-id="19321-138">Uw code kunt verwijderen (in wachtrij) een bericht van een wachtrij in twee stappen.</span><span class="sxs-lookup"><span data-stu-id="19321-138">Your code can remove (dequeue) a message from a queue in two steps.</span></span>

1. <span data-ttu-id="19321-139">Roep **GetMessageAsync** tooget Hallo volgende bericht in een wachtrij.</span><span class="sxs-lookup"><span data-stu-id="19321-139">Call **GetMessageAsync** tooget hello next message in a queue.</span></span> <span data-ttu-id="19321-140">Een bericht dat wordt geretourneerd door **GetMessageAsync** wordt onzichtbaar tooany andere codes die berichten lezen uit deze wachtrij.</span><span class="sxs-lookup"><span data-stu-id="19321-140">A message returned from **GetMessageAsync** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="19321-141">Standaard blijft het bericht onzichtbaar gedurende 30 seconden.</span><span class="sxs-lookup"><span data-stu-id="19321-141">By default, this message stays invisible for 30 seconds.</span></span>
2. <span data-ttu-id="19321-142">Hallo-bericht verwijderen uit Hallo wachtrij aanroep toofinish **DeleteMessageAsync**.</span><span class="sxs-lookup"><span data-stu-id="19321-142">toofinish removing hello message from hello queue, call **DeleteMessageAsync**.</span></span>

<span data-ttu-id="19321-143">Dit proces in twee stappen van het verwijderen van een bericht zorgt ervoor dat als uw code mislukt tooprocess een bericht vanwege problemen toohardware of software, een ander exemplaar van uw code krijgt hetzelfde bericht Hallo en probeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="19321-143">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="19321-144">Hallo volgende code aanroepen **DeleteMessageAsync** direct nadat het Hallo-bericht is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="19321-144">hello following code calls **DeleteMessageAsync** right after hello message has been processed.</span></span>

    // Get hello next message in hello queue.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();

    // Process hello message in less than 30 seconds.

    // Then delete hello message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);

## <a name="leverage-additional-options-for-dequeuing-messages"></a><span data-ttu-id="19321-145">Gebruikmaken van aanvullende opties voor berichten waarbij</span><span class="sxs-lookup"><span data-stu-id="19321-145">Leverage additional options for dequeuing messages</span></span>
<span data-ttu-id="19321-146">Er zijn twee manieren waarop u het ophalen van berichten uit een wachtrij kunt aanpassen.</span><span class="sxs-lookup"><span data-stu-id="19321-146">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="19321-147">U krijgt eerst een batch met berichten (omhoog too32).</span><span class="sxs-lookup"><span data-stu-id="19321-147">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="19321-148">Ten tweede kunt u instellen een time-out voor onzichtbaarheid langer of korter, zodat uw code meer of minder tijd toofully elk bericht niet verwerken.</span><span class="sxs-lookup"><span data-stu-id="19321-148">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="19321-149">Hallo volgende codevoorbeeld wordt de **GetMessages** methode tooget 20 berichten in één aanroep.</span><span class="sxs-lookup"><span data-stu-id="19321-149">hello following code example uses the **GetMessages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="19321-150">Vervolgens wordt elk bericht verwerkt met behulp van een **foreach**-lus.</span><span class="sxs-lookup"><span data-stu-id="19321-150">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="19321-151">Hallo onzichtbaarheid too5 minuten voor de time-out voor elk bericht wordt ook ingesteld.</span><span class="sxs-lookup"><span data-stu-id="19321-151">It also sets hello invisibility timeout too5 minutes for each message.</span></span> <span data-ttu-id="19321-152">Opmerking dat Hallo 5 minuten start voor alle op Hallo dezelfde berichten tijd, betekent dat als er 5 minuten zijn verstreken na de aanroep hello te**GetMessages**, alle berichten die niet zijn verwijderd weer worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="19321-152">Note that hello 5 minutes start for all messages at hello same time, so after 5 minutes have passed after hello call too**GetMessages**, any messages which have not been deleted become visible again.</span></span>

    // Retrieve 20 messages at a time, keeping those messages invisible for 5 minutes, 
    //   delete each message after processing.

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.
        queue.DeleteMessage(message);
    }

## <a name="get-hello-queue-length"></a><span data-ttu-id="19321-153">Hallo-wachtrijlengte ophalen</span><span class="sxs-lookup"><span data-stu-id="19321-153">Get hello queue length</span></span>
<span data-ttu-id="19321-154">U kunt een schatting maken van het aantal berichten Hallo krijgen in een wachtrij.</span><span class="sxs-lookup"><span data-stu-id="19321-154">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="19321-155">De **FetchAttributes** methode vraagt de queue-service Hallo Hallo wachtrij-kenmerken, zoals aantal Hallo-berichten ophalen.</span><span class="sxs-lookup"><span data-stu-id="19321-155">The **FetchAttributes** method asks hello queue service to retrieve hello queue attributes, including hello message count.</span></span> <span data-ttu-id="19321-156">Hallo **ApproximateMethodCount** eigenschap retourneert de laatste waarde Hallo opgehaald door de **FetchAttributes** methode zonder Hallo queue-service aanroepen.</span><span class="sxs-lookup"><span data-stu-id="19321-156">hello **ApproximateMethodCount** property returns hello last value retrieved by the **FetchAttributes** method, without calling hello queue service.</span></span>

    // Fetch hello queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve hello cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display hello number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-hello-async-await-pattern-with-common-queue-apis"></a><span data-ttu-id="19321-157">Hallo Async-Await-patroon gebruiken met de gemeenschappelijke wachtrij API 's</span><span class="sxs-lookup"><span data-stu-id="19321-157">Use hello Async-Await pattern with common queue APIs</span></span>
<span data-ttu-id="19321-158">Dit voorbeeld toont hoe toouse Hallo Async-Await-patroon met gemeenschappelijke wachtrij API's.</span><span class="sxs-lookup"><span data-stu-id="19321-158">This example shows how toouse hello Async-Await pattern with common queue APIs.</span></span> <span data-ttu-id="19321-159">Hallo voorbeeld aanroepen Hallo asynchrone versie van elk Hallo opgegeven methoden.</span><span class="sxs-lookup"><span data-stu-id="19321-159">hello sample calls hello async version of each of hello given methods.</span></span> <span data-ttu-id="19321-160">Deze kunnen worden gezien door Hallo Async na herstel van elke methode.</span><span class="sxs-lookup"><span data-stu-id="19321-160">This can be seen by hello Async post-fix of each method.</span></span> <span data-ttu-id="19321-161">Wanneer een async-methode wordt gebruikt, wordt Hallo Async-Await-patroon lokale uitvoering onderbroken totdat het Hallo-aanroep is voltooid.</span><span class="sxs-lookup"><span data-stu-id="19321-161">When an async method is used, hello Async-Await pattern suspends local execution until hello call is completed.</span></span> <span data-ttu-id="19321-162">Hierdoor kunnen de huidige thread toodo Hallo andere taken die knelpunten in de prestaties worden voorkomen en verbetert de algehele respons van uw toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="19321-162">This behavior allows hello current thread toodo other work which helps avoid performance bottlenecks and improves hello overall responsiveness of your application.</span></span> <span data-ttu-id="19321-163">Zie voor meer informatie over het gebruik van hello Async-Await-patroon in .NET, [Async en Await (C# en Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span><span class="sxs-lookup"><span data-stu-id="19321-163">For more details on using hello Async-Await pattern in .NET, see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

    // Create a message tooadd toohello queue.
    CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

    // Async enqueue hello message.
    await messageQueue.AddMessageAsync(cloudQueueMessage);
    Console.WriteLine("Message added");

    // Async dequeue hello message.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();
    Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

    // Async delete hello message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);
    Console.WriteLine("Deleted message");
## <a name="delete-a-queue"></a><span data-ttu-id="19321-164">Een wachtrij verwijderen</span><span class="sxs-lookup"><span data-stu-id="19321-164">Delete a queue</span></span>
<span data-ttu-id="19321-165">toodelete een wachtrij en alle Hallo-berichten die dit, neemt u contact de **verwijderen** methode op Hallo wachtrij-object.</span><span class="sxs-lookup"><span data-stu-id="19321-165">toodelete a queue and all hello messages contained in it, call the **Delete** method on hello queue object.</span></span>

    // Delete hello queue.
    messageQueue.Delete();


## <a name="next-steps"></a><span data-ttu-id="19321-166">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="19321-166">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

