---
title: Aan de slag met de opslag van de wachtrij en Visual Studio verbonden services (cloudservices) | Microsoft Docs
description: Hoe u aan de slag met Azure Queue storage in een cloud service-project in Visual Studio nadat u verbinding met een opslagaccount met Visual Studio hebt verbonden services
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
ms.openlocfilehash: 7a6e58a62b4cfbf99641559363dd0c860cdf8af2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="5fac6-103">Aan de slag met Azure Queue storage en Visual Studio verbonden services (cloud services-projecten)</span><span class="sxs-lookup"><span data-stu-id="5fac6-103">Getting started with Azure Queue storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="5fac6-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="5fac6-104">Overview</span></span>
<span data-ttu-id="5fac6-105">Dit artikel wordt beschreven hoe u aan de slag met Azure Queue storage in Visual Studio nadat u hebt gemaakt of een Azure storage-account in een cloud services-project waarnaar wordt verwezen door het gebruik van de Visual Studio **verbonden Services toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="5fac6-105">This article describes how to get started using Azure Queue storage in Visual Studio after you have created or referenced an Azure storage account in a cloud services project by using the  Visual Studio **Add Connected Services** dialog.</span></span>

<span data-ttu-id="5fac6-106">Leert u hoe u een wachtrij in code maken.</span><span class="sxs-lookup"><span data-stu-id="5fac6-106">We'll show you how to create a queue in code.</span></span> <span data-ttu-id="5fac6-107">Ook ziet u hoe u eenvoudige wachtrij bewerkingen uitvoeren, zoals het toevoegen, wijzigen, lezen en verwijderen van Wachtrijberichten.</span><span class="sxs-lookup"><span data-stu-id="5fac6-107">We'll also show you how to perform basic queue operations, such as adding, modifying, reading and removing queue messages.</span></span> <span data-ttu-id="5fac6-108">De voorbeelden zijn geschreven in C#-code en gebruik de [Microsoft Azure Storage-clientbibliotheek voor .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="5fac6-108">The samples are written in C# code and use the [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="5fac6-109">De **verbonden Services toevoegen** bewerking installeert de juiste NuGet-pakketten voor toegang tot Azure-opslag in uw project en voegt u de verbindingsreeks voor de storage-account toe aan uw project configuratiebestanden.</span><span class="sxs-lookup"><span data-stu-id="5fac6-109">The **Add Connected Services** operation installs the appropriate NuGet packages to access Azure storage in your project and adds the connection string for the storage account to your project configuration files.</span></span>

* <span data-ttu-id="5fac6-110">Zie [aan de slag met Azure Queue storage met .NET](../storage/queues/storage-dotnet-how-to-use-queues.md) voor meer informatie over het bewerken van wachtrijen in code.</span><span class="sxs-lookup"><span data-stu-id="5fac6-110">See [Get started with Azure Queue storage using .NET](../storage/queues/storage-dotnet-how-to-use-queues.md) for more information on manipulating queues in code.</span></span>
* <span data-ttu-id="5fac6-111">Zie [documentatie Storage](https://azure.microsoft.com/documentation/services/storage/) voor algemene informatie over Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="5fac6-111">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="5fac6-112">Zie [Cloud Services-documentatie](https://azure.microsoft.com/documentation/services/cloud-services/) voor algemene informatie over Azure-cloudservices.</span><span class="sxs-lookup"><span data-stu-id="5fac6-112">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="5fac6-113">Zie [ASP.NET](http://www.asp.net) voor meer informatie over het programmeren van ASP.NET-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="5fac6-113">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

<span data-ttu-id="5fac6-114">Azure Queue Storage is een service voor de opslag van grote aantallen berichten die via HTTP of HTTPS overal vandaan kunnen worden opgevraagd met geverifieerde aanroepen.</span><span class="sxs-lookup"><span data-stu-id="5fac6-114">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="5fac6-115">Een enkel wachtrijbericht mag maximaal 64 KB groot zijn en een wachtrij kan miljoenen berichten bevatten, tot de totale capaciteitslimiet van een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="5fac6-115">A single queue message can be up to 64 KB in size, and a queue can contain millions of messages, up to the total capacity limit of a storage account.</span></span>

## <a name="access-queues-in-code"></a><span data-ttu-id="5fac6-116">Toegang tot wachtrijen in code</span><span class="sxs-lookup"><span data-stu-id="5fac6-116">Access queues in code</span></span>
<span data-ttu-id="5fac6-117">Voor toegang tot wachtrijen in Visual Studio Cloud Services-projecten, moet u de volgende items naar een C#-bronbestand die toegang hebben tot Azure Queue storage bevatten.</span><span class="sxs-lookup"><span data-stu-id="5fac6-117">To access queues in Visual Studio Cloud Services projects, you need to include the following items to any C# source file that access Azure Queue storage.</span></span>

1. <span data-ttu-id="5fac6-118">Zorg ervoor dat de naamruimtedeclaraties boven aan het C#-bestand zijn deze **met** instructies.</span><span class="sxs-lookup"><span data-stu-id="5fac6-118">Make sure the namespace declarations at the top of the C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
2. <span data-ttu-id="5fac6-119">Ophalen van een **CloudStorageAccount** -object met gegevens over uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="5fac6-119">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="5fac6-120">De volgende code gebruiken om op te halen de uw verbindingsreeks voor opslag en opslag accountgegevens van de configuratie van Azure service.</span><span class="sxs-lookup"><span data-stu-id="5fac6-120">Use the following code to get the your storage connection string and storage account information from the Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. <span data-ttu-id="5fac6-121">Ophalen van een **CloudQueueClient** object om te verwijzen naar de wachtrij-objecten in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="5fac6-121">Get a **CloudQueueClient** object to reference the queue objects in your storage account.</span></span>  
   
        // Create the queue client.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. <span data-ttu-id="5fac6-122">Ophalen van een **CloudQueue** object om te verwijzen naar een bepaalde wachtrij.</span><span class="sxs-lookup"><span data-stu-id="5fac6-122">Get a **CloudQueue** object to reference a specific queue.</span></span>
   
        // Get a reference to a queue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

<span data-ttu-id="5fac6-123">**Opmerking:** alle bovenstaande code voor de code in de volgende voorbeelden gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5fac6-123">**NOTE:** Use all of the above code in front of the code in the following samples.</span></span>

## <a name="create-a-queue-in-code"></a><span data-ttu-id="5fac6-124">Een wachtrij in code maken</span><span class="sxs-lookup"><span data-stu-id="5fac6-124">Create a queue in code</span></span>
<span data-ttu-id="5fac6-125">Om de wachtrij in code maken, voegt u toe een aanroep van **CreateIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="5fac6-125">To create the queue in code, just add a call to **CreateIfNotExists**.</span></span>

    // Create the CloudQueue if it does not exist
    messageQueue.CreateIfNotExists();

## <a name="add-a-message-to-a-queue"></a><span data-ttu-id="5fac6-126">Een bericht toevoegen aan een wachtrij</span><span class="sxs-lookup"><span data-stu-id="5fac6-126">Add a message to a queue</span></span>
<span data-ttu-id="5fac6-127">Als u wilt een bericht in een bestaande wachtrij ingevoegd, maakt u een nieuwe **CloudQueueMessage** Roep vervolgens object de **AddMessage** methode.</span><span class="sxs-lookup"><span data-stu-id="5fac6-127">To insert a message into an existing queue, create a new **CloudQueueMessage** object, then call the **AddMessage** method.</span></span>

<span data-ttu-id="5fac6-128">Een **CloudQueueMessage** object kan worden gemaakt vanuit een tekenreeks (in UTF-8-indeling) of een byte-matrix.</span><span class="sxs-lookup"><span data-stu-id="5fac6-128">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="5fac6-129">Hier volgt een voorbeeld waarmee het bericht 'Hello, World'.</span><span class="sxs-lookup"><span data-stu-id="5fac6-129">Here is an example which inserts the message 'Hello, World'.</span></span>

    // Create a message and add it to the queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    messageQueue.AddMessage(message);

## <a name="read-a-message-in-a-queue"></a><span data-ttu-id="5fac6-130">Een bericht in een wachtrij lezen</span><span class="sxs-lookup"><span data-stu-id="5fac6-130">Read a message in a queue</span></span>
<span data-ttu-id="5fac6-131">U kunt het bericht vooraan in een wachtrij bekijken zonder het uit de wachtrij te verwijderen, door de methode **PeekMessage** aan te roepen.</span><span class="sxs-lookup"><span data-stu-id="5fac6-131">You can peek at the message in the front of a queue without removing it from the queue by calling the **PeekMessage** method.</span></span>

    // Peek at the next message
    CloudQueueMessage peekedMessage = messageQueue.PeekMessage();

## <a name="read-and-remove-a-message-in-a-queue"></a><span data-ttu-id="5fac6-132">Lezen en verwijderen van een bericht in een wachtrij</span><span class="sxs-lookup"><span data-stu-id="5fac6-132">Read and remove a message in a queue</span></span>
<span data-ttu-id="5fac6-133">Uw code kunt verwijderen (uit de wachtrij) een bericht van een wachtrij in twee stappen.</span><span class="sxs-lookup"><span data-stu-id="5fac6-133">Your code can remove (de-queue) a message from a queue in two steps.</span></span>

1. <span data-ttu-id="5fac6-134">Roep **GetMessage** ophalen van het volgende bericht in een wachtrij.</span><span class="sxs-lookup"><span data-stu-id="5fac6-134">Call **GetMessage** to get the next message in a queue.</span></span> <span data-ttu-id="5fac6-135">Een bericht dat wordt geretourneerd door **GetMessage**, wordt onzichtbaar voor andere codes die berichten lezen uit deze wachtrij.</span><span class="sxs-lookup"><span data-stu-id="5fac6-135">A message returned from **GetMessage** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="5fac6-136">Standaard blijft het bericht onzichtbaar gedurende 30 seconden.</span><span class="sxs-lookup"><span data-stu-id="5fac6-136">By default, this message stays invisible for 30 seconds.</span></span>
2. <span data-ttu-id="5fac6-137">Aanroepen voor het voltooien van het bericht uit de wachtrij verwijderen **DeleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="5fac6-137">To finish removing the message from the queue, call **DeleteMessage**.</span></span>

<span data-ttu-id="5fac6-138">Dit proces in twee stappen voor het verwijderen van een bericht zorgt ervoor dat als de code er niet in slaagt een bericht te verwerken vanwege hardware- of softwareproblemen, een ander exemplaar van uw code hetzelfde bericht kan ophalen en het opnieuw kan proberen.</span><span class="sxs-lookup"><span data-stu-id="5fac6-138">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="5fac6-139">De volgende code aanroepen **DeleteMessage** direct nadat het bericht is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="5fac6-139">The following code calls **DeleteMessage** right after the message has been processed.</span></span>

    // Get the next message in the queue.
    CloudQueueMessage retrievedMessage = messageQueue.GetMessage();

    // Process the message in less than 30 seconds

    // Then delete the message.
    await messageQueue.DeleteMessage(retrievedMessage);


## <a name="use-additional-options-to-process-and-remove-queue-messages"></a><span data-ttu-id="5fac6-140">Aanvullende opties gebruiken om te verwerken en verwijderen van Wachtrijberichten</span><span class="sxs-lookup"><span data-stu-id="5fac6-140">Use additional options to process and remove queue messages</span></span>
<span data-ttu-id="5fac6-141">Er zijn twee manieren waarop u het ophalen van berichten uit een wachtrij kunt aanpassen.</span><span class="sxs-lookup"><span data-stu-id="5fac6-141">There are two ways you can customize message retrieval from a queue.</span></span>

* <span data-ttu-id="5fac6-142">U kunt een batch met berichten (maximaal 32) ophalen.</span><span class="sxs-lookup"><span data-stu-id="5fac6-142">You can get a batch of messages (up to 32).</span></span>
* <span data-ttu-id="5fac6-143">U kunt een time-out langer of korter onzichtbaarheid instellen zodat uw code meer of minder tijd voor het volledig verwerken van elk bericht.</span><span class="sxs-lookup"><span data-stu-id="5fac6-143">You can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="5fac6-144">In het volgende codevoorbeeld wordt de methode **GetMessages** gebruikt om 20 berichten in één aanroep op te halen.</span><span class="sxs-lookup"><span data-stu-id="5fac6-144">The following code example uses the **GetMessages** method to get 20 messages in one call.</span></span> <span data-ttu-id="5fac6-145">Vervolgens wordt elk bericht verwerkt met behulp van een **foreach**-lus.</span><span class="sxs-lookup"><span data-stu-id="5fac6-145">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="5fac6-146">De time-out voor onzichtbaarheid wordt ingesteld op vijf minuten voor elk bericht.</span><span class="sxs-lookup"><span data-stu-id="5fac6-146">It also sets the invisibility timeout to five minutes for each message.</span></span> <span data-ttu-id="5fac6-147">Houd voor ogen dat de periode van 5 minuten voor alle berichten op hetzelfde moment start. Nadat er 5 minuten zijn verstreken sinds de aanroep van **GetMessages**, worden dus alle berichten die niet zijn verwijderd, opnieuw zichtbaar.</span><span class="sxs-lookup"><span data-stu-id="5fac6-147">Note that the 5 minutes starts for all messages at the same time, so after 5 minutes have passed since the call to **GetMessages**, any messages which have not been deleted will become visible again.</span></span>

<span data-ttu-id="5fac6-148">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="5fac6-148">Here's an example:</span></span>

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.

        // Then delete the message after processing
        messageQueue.DeleteMessage(message);

    }

## <a name="get-the-queue-length"></a><span data-ttu-id="5fac6-149">Lengte van de wachtrij ophalen</span><span class="sxs-lookup"><span data-stu-id="5fac6-149">Get the queue length</span></span>
<span data-ttu-id="5fac6-150">U kunt een schatting ophalen van het aantal berichten in de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="5fac6-150">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="5fac6-151">De methode **FetchAttributes** vraagt de Queue-service de wachtrij-kenmerken, zoals het aantal berichten, op te halen.</span><span class="sxs-lookup"><span data-stu-id="5fac6-151">The **FetchAttributes** method asks the Queue service to retrieve the queue attributes, including the message count.</span></span> <span data-ttu-id="5fac6-152">De **ApproximateMethodCount** eigenschap retourneert de laatste waarde die is opgehaald door de **FetchAttributes** methode, zonder de Queue-service aanroepen.</span><span class="sxs-lookup"><span data-stu-id="5fac6-152">The **ApproximateMethodCount** property returns the last value retrieved by the **FetchAttributes** method, without calling the Queue service.</span></span>

    // Fetch the queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve the cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-the-async-await-pattern-with-common-azure-queue-apis"></a><span data-ttu-id="5fac6-153">De Async-Await-patroon gebruiken met algemene Azure Queue-API 's</span><span class="sxs-lookup"><span data-stu-id="5fac6-153">Use the Async-Await Pattern with common Azure Queue APIs</span></span>
<span data-ttu-id="5fac6-154">In dit voorbeeld laat zien hoe het Async-Await-patroon gebruiken met algemene Azure Queue-API's.</span><span class="sxs-lookup"><span data-stu-id="5fac6-154">This example shows how to use the Async-Await pattern with common Azure Queue APIs.</span></span> <span data-ttu-id="5fac6-155">Het voorbeeld roept de async-versie van elk van de opgegeven methoden, moeten deze kunnen worden gezien door de **asynchrone** na herstel van elke methode.</span><span class="sxs-lookup"><span data-stu-id="5fac6-155">The sample calls the async version of each of the given methods, this can be seen by the **Async** post-fix of each method.</span></span> <span data-ttu-id="5fac6-156">Wanneer u een async-methode gebruikt het async-await patroon lokale uitvoering wordt uitgesteld totdat de aanroep is voltooid.</span><span class="sxs-lookup"><span data-stu-id="5fac6-156">When an async method is used the async-await pattern suspends local execution until the call completes.</span></span> <span data-ttu-id="5fac6-157">Dit gedrag kan de huidige thread voor andere werk die knelpunten in de prestaties worden voorkomen en verbetert de algehele respons van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="5fac6-157">This behavior allows the current thread to do other work which helps avoid performance bottlenecks and improves the overall responsiveness of your application.</span></span> <span data-ttu-id="5fac6-158">Zie [Async en Await (C# en Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx) voor meer informatie over het gebruik van het Async-Await-patroon in .NET.</span><span class="sxs-lookup"><span data-stu-id="5fac6-158">For more details on using the Async-Await pattern in .NET see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

    // Create a message to put in the queue
    CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

    // Add the message asynchronously
    await messageQueue.AddMessageAsync(cloudQueueMessage);
    Console.WriteLine("Message added");

    // Async dequeue the message
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();
    Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

    // Delete the message asynchronously
    await messageQueue.DeleteMessageAsync(retrievedMessage);
    Console.WriteLine("Deleted message");

## <a name="delete-a-queue"></a><span data-ttu-id="5fac6-159">Een wachtrij verwijderen</span><span class="sxs-lookup"><span data-stu-id="5fac6-159">Delete a queue</span></span>
<span data-ttu-id="5fac6-160">Als u een wachtrij en alle berichten hierin wilt verwijderen, roept u de methode **Delete** aan in het wachtrijobject.</span><span class="sxs-lookup"><span data-stu-id="5fac6-160">To delete a queue and all the messages contained in it, call the **Delete** method on the queue object.</span></span>

    // Delete the queue.
    messageQueue.Delete();

## <a name="next-steps"></a><span data-ttu-id="5fac6-161">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5fac6-161">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

