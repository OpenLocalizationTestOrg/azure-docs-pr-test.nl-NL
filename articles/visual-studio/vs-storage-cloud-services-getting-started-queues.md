---
title: aaaGet gestart met de opslag van de wachtrij en Visual Studio verbonden services (cloudservices) | Microsoft Docs
description: Hoe tooget gestart met Azure Queue storage in een cloud service-project in Visual Studio nadat tooa storage-account met Visual Studio verbinding services verbonden
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: da587aac-5e64-4e9a-8405-44cc1924881d
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 1e90eeb826131cadca90dcb720c931fff5fedcb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="6f923-103">Aan de slag met Azure Queue storage en Visual Studio verbonden services (cloud services-projecten)</span><span class="sxs-lookup"><span data-stu-id="6f923-103">Getting started with Azure Queue storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="6f923-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="6f923-104">Overview</span></span>
<span data-ttu-id="6f923-105">Dit artikel wordt beschreven hoe tooget gestart met Azure Queue storage in Visual Studio nadat u hebt gemaakt of een Azure storage-account in een cloud services-project waarnaar wordt verwezen met behulp van Visual Studio Hallo **verbonden Services toevoegen** dialoogvenster .</span><span class="sxs-lookup"><span data-stu-id="6f923-105">This article describes how tooget started using Azure Queue storage in Visual Studio after you have created or referenced an Azure storage account in a cloud services project by using hello  Visual Studio **Add Connected Services** dialog.</span></span>

<span data-ttu-id="6f923-106">Leert u hoe een wachtrij in code toocreate.</span><span class="sxs-lookup"><span data-stu-id="6f923-106">We'll show you how toocreate a queue in code.</span></span> <span data-ttu-id="6f923-107">Ook ziet u hoe tooperform basic wachtrij-bewerkingen, zoals het toevoegen, wijzigen, lezen en verwijderen van Wachtrijberichten.</span><span class="sxs-lookup"><span data-stu-id="6f923-107">We'll also show you how tooperform basic queue operations, such as adding, modifying, reading and removing queue messages.</span></span> <span data-ttu-id="6f923-108">Hallo-voorbeelden zijn geschreven in C#-code en gebruiken van Hallo [Microsoft Azure Storage-clientbibliotheek voor .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="6f923-108">hello samples are written in C# code and use hello [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="6f923-109">Hallo **verbonden Services toevoegen** bewerking installeert Hallo juiste NuGet-pakketten tooaccess Azure-opslag in uw project en voegt Hallo-verbindingsreeks voor hello storage account tooyour project configuratiebestanden.</span><span class="sxs-lookup"><span data-stu-id="6f923-109">hello **Add Connected Services** operation installs hello appropriate NuGet packages tooaccess Azure storage in your project and adds hello connection string for hello storage account tooyour project configuration files.</span></span>

* <span data-ttu-id="6f923-110">Zie [aan de slag met Azure Queue storage met .NET](../storage/queues/storage-dotnet-how-to-use-queues.md) voor meer informatie over het bewerken van wachtrijen in code.</span><span class="sxs-lookup"><span data-stu-id="6f923-110">See [Get started with Azure Queue storage using .NET](../storage/queues/storage-dotnet-how-to-use-queues.md) for more information on manipulating queues in code.</span></span>
* <span data-ttu-id="6f923-111">Zie [documentatie Storage](https://azure.microsoft.com/documentation/services/storage/) voor algemene informatie over Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="6f923-111">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="6f923-112">Zie [Cloud Services-documentatie](https://azure.microsoft.com/documentation/services/cloud-services/) voor algemene informatie over Azure-cloudservices.</span><span class="sxs-lookup"><span data-stu-id="6f923-112">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="6f923-113">Zie [ASP.NET](http://www.asp.net) voor meer informatie over het programmeren van ASP.NET-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="6f923-113">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

<span data-ttu-id="6f923-114">Azure Queue storage is een service voor het opslaan van grote aantallen berichten die toegankelijk zijn vanaf een willekeurige plaats in Hallo wereld via geverifieerde aanroepen via HTTP of HTTPS.</span><span class="sxs-lookup"><span data-stu-id="6f923-114">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="6f923-115">Een enkel wachtrijbericht mag up too64 KB groot en een wachtrij kan miljoenen berichten up toohello totale capaciteitslimiet van een opslagaccount bevatten.</span><span class="sxs-lookup"><span data-stu-id="6f923-115">A single queue message can be up too64 KB in size, and a queue can contain millions of messages, up toohello total capacity limit of a storage account.</span></span>

## <a name="access-queues-in-code"></a><span data-ttu-id="6f923-116">Toegang tot wachtrijen in code</span><span class="sxs-lookup"><span data-stu-id="6f923-116">Access queues in code</span></span>
<span data-ttu-id="6f923-117">tooaccess wachtrijen in Visual Studio Cloud Services-projecten, moet u tooinclude Hallo volgende items tooany C#-bronbestand die toegang hebben tot Azure Queue storage.</span><span class="sxs-lookup"><span data-stu-id="6f923-117">tooaccess queues in Visual Studio Cloud Services projects, you need tooinclude hello following items tooany C# source file that access Azure Queue storage.</span></span>

1. <span data-ttu-id="6f923-118">Zorg ervoor dat de naamruimtedeclaraties Hallo Hallo bovenaan Hallo C#-bestand in deze **met** instructies.</span><span class="sxs-lookup"><span data-stu-id="6f923-118">Make sure hello namespace declarations at hello top of hello C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
2. <span data-ttu-id="6f923-119">Ophalen van een **CloudStorageAccount** -object met gegevens over uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="6f923-119">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="6f923-120">Gebruik Hallo na code tooget Hallo uw verbindingsreeks voor opslag en de accountgegevens van de opslag van Azure Hallo-serviceconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="6f923-120">Use hello following code tooget hello your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. <span data-ttu-id="6f923-121">Ophalen van een **CloudQueueClient** object tooreference Hallo wachtrij-objecten in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="6f923-121">Get a **CloudQueueClient** object tooreference hello queue objects in your storage account.</span></span>  
   
        // Create hello queue client.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. <span data-ttu-id="6f923-122">Ophalen van een **CloudQueue** tooreference een specifieke wachtrij-object.</span><span class="sxs-lookup"><span data-stu-id="6f923-122">Get a **CloudQueue** object tooreference a specific queue.</span></span>
   
        // Get a reference tooa queue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

<span data-ttu-id="6f923-123">**Opmerking:** alle Hallo bovenstaande code voor het Hallo-code in Hallo volgen voorbeelden gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6f923-123">**NOTE:** Use all of hello above code in front of hello code in hello following samples.</span></span>

## <a name="create-a-queue-in-code"></a><span data-ttu-id="6f923-124">Een wachtrij in code maken</span><span class="sxs-lookup"><span data-stu-id="6f923-124">Create a queue in code</span></span>
<span data-ttu-id="6f923-125">toocreate hello wachtrij in code, voegt u toe een aanroep te**CreateIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="6f923-125">toocreate hello queue in code, just add a call too**CreateIfNotExists**.</span></span>

    // Create hello CloudQueue if it does not exist
    messageQueue.CreateIfNotExists();

## <a name="add-a-message-tooa-queue"></a><span data-ttu-id="6f923-126">Een berichtenwachtrij tooa toevoegen</span><span class="sxs-lookup"><span data-stu-id="6f923-126">Add a message tooa queue</span></span>
<span data-ttu-id="6f923-127">tooinsert een bericht in een bestaande wachtrij maakt u een nieuwe **CloudQueueMessage** object en vervolgens aanroep Hallo **AddMessage** methode.</span><span class="sxs-lookup"><span data-stu-id="6f923-127">tooinsert a message into an existing queue, create a new **CloudQueueMessage** object, then call hello **AddMessage** method.</span></span>

<span data-ttu-id="6f923-128">Een **CloudQueueMessage** object kan worden gemaakt vanuit een tekenreeks (in UTF-8-indeling) of een byte-matrix.</span><span class="sxs-lookup"><span data-stu-id="6f923-128">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="6f923-129">Hier volgt een voorbeeld waarmee het Hallo-bericht 'Hello, World' invoegt.</span><span class="sxs-lookup"><span data-stu-id="6f923-129">Here is an example which inserts hello message 'Hello, World'.</span></span>

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    messageQueue.AddMessage(message);

## <a name="read-a-message-in-a-queue"></a><span data-ttu-id="6f923-130">Een bericht in een wachtrij lezen</span><span class="sxs-lookup"><span data-stu-id="6f923-130">Read a message in a queue</span></span>
<span data-ttu-id="6f923-131">U kunt bekijken van Hallo-bericht in Hallo begin van een wachtrij zonder het te verwijderen uit de wachtrij Hallo door aanroepen Hallo **PeekMessage** methode.</span><span class="sxs-lookup"><span data-stu-id="6f923-131">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **PeekMessage** method.</span></span>

    // Peek at hello next message
    CloudQueueMessage peekedMessage = messageQueue.PeekMessage();

## <a name="read-and-remove-a-message-in-a-queue"></a><span data-ttu-id="6f923-132">Lezen en verwijderen van een bericht in een wachtrij</span><span class="sxs-lookup"><span data-stu-id="6f923-132">Read and remove a message in a queue</span></span>
<span data-ttu-id="6f923-133">Uw code kunt verwijderen (uit de wachtrij) een bericht van een wachtrij in twee stappen.</span><span class="sxs-lookup"><span data-stu-id="6f923-133">Your code can remove (de-queue) a message from a queue in two steps.</span></span>

1. <span data-ttu-id="6f923-134">Roep **GetMessage** tooget Hallo volgende bericht in een wachtrij.</span><span class="sxs-lookup"><span data-stu-id="6f923-134">Call **GetMessage** tooget hello next message in a queue.</span></span> <span data-ttu-id="6f923-135">Een bericht dat wordt geretourneerd door **GetMessage** wordt onzichtbaar tooany andere codes die berichten lezen uit deze wachtrij.</span><span class="sxs-lookup"><span data-stu-id="6f923-135">A message returned from **GetMessage** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="6f923-136">Standaard blijft het bericht onzichtbaar gedurende 30 seconden.</span><span class="sxs-lookup"><span data-stu-id="6f923-136">By default, this message stays invisible for 30 seconds.</span></span>
2. <span data-ttu-id="6f923-137">Hallo-bericht verwijderen uit Hallo wachtrij aanroep toofinish **DeleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="6f923-137">toofinish removing hello message from hello queue, call **DeleteMessage**.</span></span>

<span data-ttu-id="6f923-138">Dit proces in twee stappen van het verwijderen van een bericht zorgt ervoor dat als uw code mislukt tooprocess een bericht vanwege problemen toohardware of software, een ander exemplaar van uw code krijgt hetzelfde bericht Hallo en probeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="6f923-138">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="6f923-139">Hallo volgende code aanroepen **DeleteMessage** direct nadat het Hallo-bericht is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="6f923-139">hello following code calls **DeleteMessage** right after hello message has been processed.</span></span>

    // Get hello next message in hello queue.
    CloudQueueMessage retrievedMessage = messageQueue.GetMessage();

    // Process hello message in less than 30 seconds

    // Then delete hello message.
    await messageQueue.DeleteMessage(retrievedMessage);


## <a name="use-additional-options-tooprocess-and-remove-queue-messages"></a><span data-ttu-id="6f923-140">Aanvullende opties tooprocess gebruiken en verwijderen van Wachtrijberichten</span><span class="sxs-lookup"><span data-stu-id="6f923-140">Use additional options tooprocess and remove queue messages</span></span>
<span data-ttu-id="6f923-141">Er zijn twee manieren waarop u het ophalen van berichten uit een wachtrij kunt aanpassen.</span><span class="sxs-lookup"><span data-stu-id="6f923-141">There are two ways you can customize message retrieval from a queue.</span></span>

* <span data-ttu-id="6f923-142">U kunt een batch met berichten (omhoog too32) ophalen.</span><span class="sxs-lookup"><span data-stu-id="6f923-142">You can get a batch of messages (up too32).</span></span>
* <span data-ttu-id="6f923-143">U kunt een time-out langer of korter onzichtbaarheid instellen zodat uw code meer of minder tijd toofully elk bericht niet verwerken.</span><span class="sxs-lookup"><span data-stu-id="6f923-143">You can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="6f923-144">Hallo volgende codevoorbeeld wordt de **GetMessages** methode tooget 20 berichten in één aanroep.</span><span class="sxs-lookup"><span data-stu-id="6f923-144">hello following code example uses the **GetMessages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="6f923-145">Vervolgens wordt elk bericht verwerkt met behulp van een **foreach**-lus.</span><span class="sxs-lookup"><span data-stu-id="6f923-145">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="6f923-146">Hallo onzichtbaarheid toofive minuten voor de time-out voor elk bericht wordt ook ingesteld.</span><span class="sxs-lookup"><span data-stu-id="6f923-146">It also sets hello invisibility timeout toofive minutes for each message.</span></span> <span data-ttu-id="6f923-147">Houd er rekening mee dat Hallo 5 minuten voor alle berichten op Hallo dezelfde time begint, betekent dat als er 5 minuten zijn verstreken sinds de aanroep hello te**GetMessages**, alle berichten die niet zijn verwijderd weer zichtbaar worden.</span><span class="sxs-lookup"><span data-stu-id="6f923-147">Note that hello 5 minutes starts for all messages at hello same time, so after 5 minutes have passed since hello call too**GetMessages**, any messages which have not been deleted will become visible again.</span></span>

<span data-ttu-id="6f923-148">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="6f923-148">Here's an example:</span></span>

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.

        // Then delete hello message after processing
        messageQueue.DeleteMessage(message);

    }

## <a name="get-hello-queue-length"></a><span data-ttu-id="6f923-149">Hallo-wachtrijlengte ophalen</span><span class="sxs-lookup"><span data-stu-id="6f923-149">Get hello queue length</span></span>
<span data-ttu-id="6f923-150">U kunt een schatting maken van het aantal berichten Hallo krijgen in een wachtrij.</span><span class="sxs-lookup"><span data-stu-id="6f923-150">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="6f923-151">De **FetchAttributes** methode vraagt de Queue-service Hallo Hallo wachtrij-kenmerken, zoals aantal Hallo-berichten ophalen.</span><span class="sxs-lookup"><span data-stu-id="6f923-151">The **FetchAttributes** method asks hello Queue service to retrieve hello queue attributes, including hello message count.</span></span> <span data-ttu-id="6f923-152">Hallo **ApproximateMethodCount** eigenschap retourneert de laatste waarde Hallo opgehaald door de **FetchAttributes** methode zonder Hallo Queue-service aanroepen.</span><span class="sxs-lookup"><span data-stu-id="6f923-152">hello **ApproximateMethodCount** property returns hello last value retrieved by the **FetchAttributes** method, without calling hello Queue service.</span></span>

    // Fetch hello queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve hello cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-hello-async-await-pattern-with-common-azure-queue-apis"></a><span data-ttu-id="6f923-153">Hallo Async-Await-patroon gebruiken met algemene Azure Queue-API 's</span><span class="sxs-lookup"><span data-stu-id="6f923-153">Use hello Async-Await Pattern with common Azure Queue APIs</span></span>
<span data-ttu-id="6f923-154">Dit voorbeeld toont hoe toouse Hallo Async-Await patroon met algemene Azure Queue-API's.</span><span class="sxs-lookup"><span data-stu-id="6f923-154">This example shows how toouse hello Async-Await pattern with common Azure Queue APIs.</span></span> <span data-ttu-id="6f923-155">Hallo voorbeeld Hallo async-versie van elk Hallo opgegeven methoden aanroept, deze kunnen worden gezien door Hallo **asynchrone** na herstel van elke methode.</span><span class="sxs-lookup"><span data-stu-id="6f923-155">hello sample calls hello async version of each of hello given methods, this can be seen by hello **Async** post-fix of each method.</span></span> <span data-ttu-id="6f923-156">Wanneer een async-methode is gebruikte Hallo async-await patroon lokale uitvoering wordt onderbroken totdat het Hallo-aanroep is voltooid.</span><span class="sxs-lookup"><span data-stu-id="6f923-156">When an async method is used hello async-await pattern suspends local execution until hello call completes.</span></span> <span data-ttu-id="6f923-157">Hierdoor kunnen de huidige thread toodo Hallo andere taken die knelpunten in de prestaties worden voorkomen en verbetert de algehele respons van uw toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="6f923-157">This behavior allows hello current thread toodo other work which helps avoid performance bottlenecks and improves hello overall responsiveness of your application.</span></span> <span data-ttu-id="6f923-158">Zie voor meer informatie over het gebruik van Hallo Async-Await-patroon in .NET [Async en Await (C# en Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span><span class="sxs-lookup"><span data-stu-id="6f923-158">For more details on using hello Async-Await pattern in .NET see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

    // Create a message tooput in hello queue
    CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

    // Add hello message asynchronously
    await messageQueue.AddMessageAsync(cloudQueueMessage);
    Console.WriteLine("Message added");

    // Async dequeue hello message
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();
    Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

    // Delete hello message asynchronously
    await messageQueue.DeleteMessageAsync(retrievedMessage);
    Console.WriteLine("Deleted message");

## <a name="delete-a-queue"></a><span data-ttu-id="6f923-159">Een wachtrij verwijderen</span><span class="sxs-lookup"><span data-stu-id="6f923-159">Delete a queue</span></span>
<span data-ttu-id="6f923-160">een wachtrij en alle Hallo-berichten die zijn opgenomen in deze aanroep Hallo toodelete **verwijderen** methode op Hallo wachtrij-object.</span><span class="sxs-lookup"><span data-stu-id="6f923-160">toodelete a queue and all hello messages contained in it, call hello **Delete** method on hello queue object.</span></span>

    // Delete hello queue.
    messageQueue.Delete();

## <a name="next-steps"></a><span data-ttu-id="6f923-161">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6f923-161">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

