---
title: Aan de slag met de opslag van de wachtrij en Visual Studio verbonden services (ASP.NET Core) | Microsoft Docs
description: Hoe u aan de slag met Azure queue storage in een ASP.NET Core-project in Visual Studio
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 04977069-5b2d-4cba-84ae-9fb2f5eb1006
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 394344c0e126472b97c2e8f721c8c8d6514a17dc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-queue-storage-and-visual-studio-connected-services-aspnet-core"></a><span data-ttu-id="1301d-103">Aan de slag met de opslag van de wachtrij en Visual Studio verbonden services (ASP.NET Core)</span><span class="sxs-lookup"><span data-stu-id="1301d-103">Get started with queue storage and Visual Studio connected services (ASP.NET Core)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="1301d-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="1301d-104">Overview</span></span>
<span data-ttu-id="1301d-105">Dit artikel wordt beschreven hoe u aan de slag met Azure Queue storage in Visual Studio nadat u hebt gemaakt of een Azure storage-account in een ASP.NET Core-project waarnaar wordt verwezen door het gebruik van de Visual Studio **verbonden Services toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1301d-105">This article describes how to get started using Azure Queue storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using the Visual Studio **Add Connected Services** dialog.</span></span> <span data-ttu-id="1301d-106">De **verbonden Services toevoegen** bewerking installeert de juiste NuGet-pakketten voor toegang tot Azure-opslag in uw project en voegt u de verbindingsreeks voor de storage-account toe aan uw project configuratiebestanden.</span><span class="sxs-lookup"><span data-stu-id="1301d-106">The **Add Connected Services** operation installs the appropriate NuGet packages to access Azure storage in your project and adds the connection string for the storage account to your project configuration files.</span></span>

<span data-ttu-id="1301d-107">Azure queue storage is een service voor het opslaan van grote aantallen berichten die toegankelijk zijn vanuit overal ter wereld, via geverifieerde aanroepen via HTTP of HTTPS.</span><span class="sxs-lookup"><span data-stu-id="1301d-107">Azure queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="1301d-108">Een enkel wachtrijbericht mag maximaal 64 kB (KB) en een wachtrij kan miljoenen berichten, tot aan de totale capaciteitslimiet van een opslagaccount bevatten.</span><span class="sxs-lookup"><span data-stu-id="1301d-108">A single queue message can be up to 64 kilobytes (KB) in size, and a queue can contain millions of messages, up to the total capacity limit of a storage account.</span></span>

<span data-ttu-id="1301d-109">Om te beginnen, moet u eerst een Azure-wachtrij maken in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="1301d-109">To get started, you first need to create an Azure queue in your storage account.</span></span> <span data-ttu-id="1301d-110">Leert u hoe u een wachtrij in code maken.</span><span class="sxs-lookup"><span data-stu-id="1301d-110">We'll show you how to create a queue in code.</span></span> <span data-ttu-id="1301d-111">Ook ziet u hoe u eenvoudige wachtrij bewerkingen uitvoeren, zoals het toevoegen, wijzigen, lezen en verwijderen van Wachtrijberichten.</span><span class="sxs-lookup"><span data-stu-id="1301d-111">We'll also show you how to perform basic queue operations, such as adding, modifying, reading, and removing queue messages.</span></span> <span data-ttu-id="1301d-112">De voorbeelden zijn geschreven in C\# code en het gebruik van de Azure Storage-clientbibliotheek voor .NET.</span><span class="sxs-lookup"><span data-stu-id="1301d-112">The samples are written in C\# code and use the Azure Storage Client Library for .NET.</span></span> <span data-ttu-id="1301d-113">Zie voor meer informatie over ASP.NET [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="1301d-113">For more information about ASP.NET, see [ASP.NET](http://www.asp.net).</span></span>

<span data-ttu-id="1301d-114">**Opmerking:** enkele van de API's die het uitvoeren van aanroepen naar Azure storage in ASP.NET Core zijn asynchroon.</span><span class="sxs-lookup"><span data-stu-id="1301d-114">**NOTE:** Some of the APIs that perform calls to Azure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="1301d-115">Zie [asynchrone programmering met Async en Await](http://msdn.microsoft.com/library/hh191443.aspx) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="1301d-115">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="1301d-116">De volgende code wordt ervan uitgegaan programming async-methoden worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1301d-116">The code below assumes async programming methods are being used.</span></span>

* <span data-ttu-id="1301d-117">Zie [aan de slag met Azure Queue storage met .NET](../storage/queues/storage-dotnet-how-to-use-queues.md) voor meer informatie over het bewerken van programmatisch wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="1301d-117">See [Get started with Azure Queue storage using .NET](../storage/queues/storage-dotnet-how-to-use-queues.md) for more information on programmatically manipulating queues.</span></span>
* <span data-ttu-id="1301d-118">Zie [documentatie Storage](https://azure.microsoft.com/documentation/services/storage/) voor algemene informatie over Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="1301d-118">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="1301d-119">Zie [Cloud Services-documentatie](https://azure.microsoft.com/documentation/services/cloud-services/) voor algemene informatie over Azure-cloudservices.</span><span class="sxs-lookup"><span data-stu-id="1301d-119">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="1301d-120">Zie [ASP.NET](http://www.asp.net) voor meer informatie over het programmeren van ASP.NET-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="1301d-120">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

## <a name="access-queues-in-code"></a><span data-ttu-id="1301d-121">Toegang tot wachtrijen in code</span><span class="sxs-lookup"><span data-stu-id="1301d-121">Access queues in code</span></span>
<span data-ttu-id="1301d-122">Voor toegang tot wachtrijen in ASP.NET Core projecten, moet u de volgende items naar een C# bronbestand die toegang heeft tot Azure queue storage bevatten.</span><span class="sxs-lookup"><span data-stu-id="1301d-122">To access queues in ASP.NET Core projects, you need to include the following items to any C# source file that accesses Azure queue storage.</span></span>

1. <span data-ttu-id="1301d-123">Zorg ervoor dat de naamruimtedeclaraties boven aan het C#-bestand zijn deze **met** instructies.</span><span class="sxs-lookup"><span data-stu-id="1301d-123">Make sure the namespace declarations at the top of the C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="1301d-124">Ophalen van een **CloudStorageAccount** -object met gegevens over uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="1301d-124">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="1301d-125">De volgende code gebruiken om op te halen de uw verbindingsreeks voor opslag en opslag accountgegevens van de configuratie van Azure service.</span><span class="sxs-lookup"><span data-stu-id="1301d-125">Use the following code to get the your storage connection string and storage account information from the Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. <span data-ttu-id="1301d-126">Ophalen van een **CloudQueueClient** object om te verwijzen naar de wachtrij-objecten in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="1301d-126">Get a **CloudQueueClient** object to reference the queue objects in your storage account.</span></span>  
   
        // Create the CloudQueueClient object for the storage account.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. <span data-ttu-id="1301d-127">Ophalen van een **CloudQueue** object om te verwijzen naar een bepaalde wachtrij.</span><span class="sxs-lookup"><span data-stu-id="1301d-127">Get a **CloudQueue** object to reference a specific queue.</span></span>
   
        // Get a reference to the CloudQueue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

<span data-ttu-id="1301d-128">**Opmerking:** alle bovenstaande code voor de code in de volgende voorbeelden gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1301d-128">**NOTE:** Use all of the above code in front of the code in the following samples.</span></span>

### <a name="create-a-queue-in-code"></a><span data-ttu-id="1301d-129">Een wachtrij in code maken</span><span class="sxs-lookup"><span data-stu-id="1301d-129">Create a queue in code</span></span>
<span data-ttu-id="1301d-130">Om de Azure-wachtrij in code maken, voegt u toe een aanroep van **CreateIfNotExistsAsync**.</span><span class="sxs-lookup"><span data-stu-id="1301d-130">To create the Azure queue in code, just add a call to **CreateIfNotExistsAsync**.</span></span>

    // Create the CloudQueue if it does not exist.
    await messageQueue.CreateIfNotExistsAsync();

## <a name="add-a-message-to-a-queue"></a><span data-ttu-id="1301d-131">Een bericht toevoegen aan een wachtrij</span><span class="sxs-lookup"><span data-stu-id="1301d-131">Add a message to a queue</span></span>
<span data-ttu-id="1301d-132">Als u wilt een bericht in een bestaande wachtrij ingevoegd, maakt u een nieuwe **CloudQueueMessage** Roep vervolgens object de **AddMessageAsync** methode.</span><span class="sxs-lookup"><span data-stu-id="1301d-132">To insert a message into an existing queue, create a new **CloudQueueMessage** object, then call the **AddMessageAsync** method.</span></span>

<span data-ttu-id="1301d-133">Een **CloudQueueMessage** object kan worden gemaakt vanuit een tekenreeks (in UTF-8-indeling) of een byte-matrix.</span><span class="sxs-lookup"><span data-stu-id="1301d-133">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="1301d-134">Hier volgt een voorbeeld waarmee het bericht 'Hello, World'.</span><span class="sxs-lookup"><span data-stu-id="1301d-134">Here is an example which inserts the message 'Hello, World'.</span></span>

    // Create a message and add it to the queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    await messageQueue.AddMessageAsync(message);

## <a name="read-a-message-in-a-queue"></a><span data-ttu-id="1301d-135">Een bericht in een wachtrij lezen</span><span class="sxs-lookup"><span data-stu-id="1301d-135">Read a message in a queue</span></span>
<span data-ttu-id="1301d-136">U kunt het bericht vooraan in een wachtrij bekijken zonder het te verwijderen uit de wachtrij door het aanroepen van de **PeekMessageAsync** methode.</span><span class="sxs-lookup"><span data-stu-id="1301d-136">You can peek at the message in the front of a queue without removing it from the queue by calling the **PeekMessageAsync** method.</span></span>

    // Peek the next message in the queue. 
    CloudQueueMessage peekedMessage = await messageQueue.PeekMessageAsync();


## <a name="read-and-remove-a-message-in-a-queue"></a><span data-ttu-id="1301d-137">Lezen en verwijderen van een bericht in een wachtrij</span><span class="sxs-lookup"><span data-stu-id="1301d-137">Read and remove a message in a queue</span></span>
<span data-ttu-id="1301d-138">Uw code kunt verwijderen (in wachtrij) een bericht van een wachtrij in twee stappen.</span><span class="sxs-lookup"><span data-stu-id="1301d-138">Your code can remove (dequeue) a message from a queue in two steps.</span></span>

1. <span data-ttu-id="1301d-139">Roep **GetMessageAsync** ophalen van het volgende bericht in een wachtrij.</span><span class="sxs-lookup"><span data-stu-id="1301d-139">Call **GetMessageAsync** to get the next message in a queue.</span></span> <span data-ttu-id="1301d-140">Een bericht dat wordt geretourneerd door **GetMessageAsync** wordt onzichtbaar voor andere codes die berichten lezen uit deze wachtrij.</span><span class="sxs-lookup"><span data-stu-id="1301d-140">A message returned from **GetMessageAsync** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="1301d-141">Standaard blijft het bericht onzichtbaar gedurende 30 seconden.</span><span class="sxs-lookup"><span data-stu-id="1301d-141">By default, this message stays invisible for 30 seconds.</span></span>
2. <span data-ttu-id="1301d-142">Aanroepen voor het voltooien van het bericht uit de wachtrij verwijderen **DeleteMessageAsync**.</span><span class="sxs-lookup"><span data-stu-id="1301d-142">To finish removing the message from the queue, call **DeleteMessageAsync**.</span></span>

<span data-ttu-id="1301d-143">Dit proces in twee stappen voor het verwijderen van een bericht zorgt ervoor dat als de code er niet in slaagt een bericht te verwerken vanwege hardware- of softwareproblemen, een ander exemplaar van uw code hetzelfde bericht kan ophalen en het opnieuw kan proberen.</span><span class="sxs-lookup"><span data-stu-id="1301d-143">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="1301d-144">De volgende code aanroepen **DeleteMessageAsync** direct nadat het bericht is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="1301d-144">The following code calls **DeleteMessageAsync** right after the message has been processed.</span></span>

    // Get the next message in the queue.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();

    // Process the message in less than 30 seconds.

    // Then delete the message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);

## <a name="leverage-additional-options-for-dequeuing-messages"></a><span data-ttu-id="1301d-145">Gebruikmaken van aanvullende opties voor berichten waarbij</span><span class="sxs-lookup"><span data-stu-id="1301d-145">Leverage additional options for dequeuing messages</span></span>
<span data-ttu-id="1301d-146">Er zijn twee manieren waarop u het ophalen van berichten uit een wachtrij kunt aanpassen.</span><span class="sxs-lookup"><span data-stu-id="1301d-146">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="1301d-147">Ten eerste kunt u berichten batchgewijs (maximaal 32) ophalen.</span><span class="sxs-lookup"><span data-stu-id="1301d-147">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="1301d-148">Ten tweede kunt u een langere of kortere time-out voor onzichtbaarheid instellen, zodat uw code meer of minder tijd krijgt voor het volledig verwerken van elk bericht.</span><span class="sxs-lookup"><span data-stu-id="1301d-148">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="1301d-149">In het volgende codevoorbeeld wordt de methode **GetMessages** gebruikt om 20 berichten in één aanroep op te halen.</span><span class="sxs-lookup"><span data-stu-id="1301d-149">The following code example uses the **GetMessages** method to get 20 messages in one call.</span></span> <span data-ttu-id="1301d-150">Vervolgens wordt elk bericht verwerkt met behulp van een **foreach**-lus.</span><span class="sxs-lookup"><span data-stu-id="1301d-150">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="1301d-151">De time-out voor onzichtbaarheid wordt ingesteld op 5 minuten voor elk bericht.</span><span class="sxs-lookup"><span data-stu-id="1301d-151">It also sets the invisibility timeout to 5 minutes for each message.</span></span> <span data-ttu-id="1301d-152">Denk eraan dat de vijf minuten voor alle berichten op hetzelfde moment start doorgegeven dus na 5 minuten zijn na de aanroep **GetMessages**, alle berichten die niet zijn verwijderd weer worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="1301d-152">Note that the 5 minutes start for all messages at the same time, so after 5 minutes have passed after the call to **GetMessages**, any messages which have not been deleted become visible again.</span></span>

    // Retrieve 20 messages at a time, keeping those messages invisible for 5 minutes, 
    //   delete each message after processing.

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.
        queue.DeleteMessage(message);
    }

## <a name="get-the-queue-length"></a><span data-ttu-id="1301d-153">Lengte van de wachtrij ophalen</span><span class="sxs-lookup"><span data-stu-id="1301d-153">Get the queue length</span></span>
<span data-ttu-id="1301d-154">U kunt een schatting ophalen van het aantal berichten in de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="1301d-154">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="1301d-155">De **FetchAttributes** methode vraagt de queue-service voor het ophalen van de wachtrij-kenmerken, zoals het aantal berichten.</span><span class="sxs-lookup"><span data-stu-id="1301d-155">The **FetchAttributes** method asks the queue service to retrieve the queue attributes, including the message count.</span></span> <span data-ttu-id="1301d-156">De **ApproximateMethodCount** eigenschap retourneert de laatste waarde die is opgehaald door de **FetchAttributes** methode, zonder de queue-service aanroepen.</span><span class="sxs-lookup"><span data-stu-id="1301d-156">The **ApproximateMethodCount** property returns the last value retrieved by the **FetchAttributes** method, without calling the queue service.</span></span>

    // Fetch the queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve the cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display the number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-the-async-await-pattern-with-common-queue-apis"></a><span data-ttu-id="1301d-157">De Async-Await-patroon gebruiken met algemene queue API 's</span><span class="sxs-lookup"><span data-stu-id="1301d-157">Use the Async-Await pattern with common queue APIs</span></span>
<span data-ttu-id="1301d-158">In dit voorbeeld laat zien hoe het Async-Await-patroon gebruiken met algemene queue API's.</span><span class="sxs-lookup"><span data-stu-id="1301d-158">This example shows how to use the Async-Await pattern with common queue APIs.</span></span> <span data-ttu-id="1301d-159">Het voorbeeld roept de async-versie van elk van de opgegeven methoden.</span><span class="sxs-lookup"><span data-stu-id="1301d-159">The sample calls the async version of each of the given methods.</span></span> <span data-ttu-id="1301d-160">Deze kunnen worden gezien door de asynchrone na herstel van elke methode.</span><span class="sxs-lookup"><span data-stu-id="1301d-160">This can be seen by the Async post-fix of each method.</span></span> <span data-ttu-id="1301d-161">Wanneer een async-methode wordt gebruikt, schort het Async-Await-patroon lokale uitvoering totdat de aanroep is voltooid.</span><span class="sxs-lookup"><span data-stu-id="1301d-161">When an async method is used, the Async-Await pattern suspends local execution until the call is completed.</span></span> <span data-ttu-id="1301d-162">Dit gedrag kan de huidige thread voor andere werk die knelpunten in de prestaties worden voorkomen en verbetert de algehele respons van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="1301d-162">This behavior allows the current thread to do other work which helps avoid performance bottlenecks and improves the overall responsiveness of your application.</span></span> <span data-ttu-id="1301d-163">Zie voor meer informatie over het gebruik van het Async-Await-patroon in .NET [Async en Await (C# en Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span><span class="sxs-lookup"><span data-stu-id="1301d-163">For more details on using the Async-Await pattern in .NET, see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

    // Create a message to add to the queue.
    CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

    // Async enqueue the message.
    await messageQueue.AddMessageAsync(cloudQueueMessage);
    Console.WriteLine("Message added");

    // Async dequeue the message.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();
    Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

    // Async delete the message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);
    Console.WriteLine("Deleted message");
## <a name="delete-a-queue"></a><span data-ttu-id="1301d-164">Een wachtrij verwijderen</span><span class="sxs-lookup"><span data-stu-id="1301d-164">Delete a queue</span></span>
<span data-ttu-id="1301d-165">Als u een wachtrij en alle berichten hierin wilt verwijderen, roept u de methode **Delete** aan in het wachtrijobject.</span><span class="sxs-lookup"><span data-stu-id="1301d-165">To delete a queue and all the messages contained in it, call the **Delete** method on the queue object.</span></span>

    // Delete the queue.
    messageQueue.Delete();


## <a name="next-steps"></a><span data-ttu-id="1301d-166">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1301d-166">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

