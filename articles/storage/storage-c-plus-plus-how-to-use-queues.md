---
title: Het gebruik van queue storage (C++) | Microsoft Docs
description: Informatie over het gebruik van de queue-service voor opslag in Azure. Voorbeelden zijn geschreven in C++.
services: storage
documentationcenter: .net
author: cbrooksmsft
manager: jahogg
editor: tysonn
ms.assetid: c8a36365-29f6-404d-8fd1-858a7f33b50a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: cpp
ms.topic: article
ms.date: 05/11/2017
ms.author: cbrooksmsft
ms.openlocfilehash: 85e4d95549ca5edd375f3b15971634e032a3962a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-queue-storage-from-c"></a><span data-ttu-id="96daa-104">Hoe Queue Storage gebruiken met C++</span><span class="sxs-lookup"><span data-stu-id="96daa-104">How to use Queue Storage from C++</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="96daa-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="96daa-105">Overview</span></span>
<span data-ttu-id="96daa-106">Deze handleiding leert u hoe u veelvoorkomende scenario's met behulp van de Azure Queue storage-service uitvoert.</span><span class="sxs-lookup"><span data-stu-id="96daa-106">This guide will show you how to perform common scenarios using the Azure Queue storage service.</span></span> <span data-ttu-id="96daa-107">De voorbeelden zijn geschreven in C++ en gebruik de [Azure Storage-clientbibliotheek voor C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="96daa-107">The samples are written in C++ and use the [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="96daa-108">De scenario's worden behandeld: **invoegen**, **inspecteren**, **ophalen**, en **verwijderen** wachtrij berichten, evenals **maken en verwijderen van wachtrijen**.</span><span class="sxs-lookup"><span data-stu-id="96daa-108">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

> [!NOTE]
> <span data-ttu-id="96daa-109">Deze handleiding is bedoeld voor de Azure Storage-clientbibliotheek voor C++ versie 1.0.0 en hoger.</span><span class="sxs-lookup"><span data-stu-id="96daa-109">This guide targets the Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="96daa-110">De aanbevolen versie is Storage-clientbibliotheek 2.2.0, die beschikbaar is via [NuGet](http://www.nuget.org/packages/wastorage) of [GitHub](http://github.com/Azure/azure-storage-cpp/).</span><span class="sxs-lookup"><span data-stu-id="96daa-110">The recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](http://github.com/Azure/azure-storage-cpp/).</span></span>
> 
> 

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="96daa-111">Een C++-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="96daa-111">Create a C++ application</span></span>
<span data-ttu-id="96daa-112">In deze handleiding gebruikt u opslagfuncties die kunnen worden uitgevoerd binnen een C++-toepassing.</span><span class="sxs-lookup"><span data-stu-id="96daa-112">In this guide, you will use storage features which can be run within a C++ application.</span></span>

<span data-ttu-id="96daa-113">Om dit te doen, moet u voor het installeren van de Azure Storage-clientbibliotheek voor C++ en een Azure storage-account maken in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="96daa-113">To do so, you will need to install the Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>

<span data-ttu-id="96daa-114">Voor het installeren van de Azure Storage-clientbibliotheek voor C++, kunt u de volgende methoden:</span><span class="sxs-lookup"><span data-stu-id="96daa-114">To install the Azure Storage Client Library for C++, you can use the following methods:</span></span>

* <span data-ttu-id="96daa-115">**Linux:** Volg de instructies in de [Azure Storage-clientbibliotheek voor C++ Leesmij](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) pagina.</span><span class="sxs-lookup"><span data-stu-id="96daa-115">**Linux:** Follow the instructions given in the [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>
* <span data-ttu-id="96daa-116">**Windows:** In Visual Studio, klikt u op **Extra > NuGet Package Manager > Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="96daa-116">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="96daa-117">Typ de volgende opdracht in de [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) en druk op **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="96daa-117">Type the following command into the [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>

```  
Install-Package wastorage
```

## <a name="configure-your-application-to-access-queue-storage"></a><span data-ttu-id="96daa-118">Uw toepassing configureren voor toegang tot opslag van de wachtrij</span><span class="sxs-lookup"><span data-stu-id="96daa-118">Configure your application to access Queue Storage</span></span>
<span data-ttu-id="96daa-119">Toevoegen aan dat de volgende instructies toe aan de bovenkant van het bestand C++ is waar u de Azure storage-API's gebruiken voor toegang tot wachtrijen instructies bevatten:</span><span class="sxs-lookup"><span data-stu-id="96daa-119">Add the following include statements to the top of the C++ file where you want to use the Azure storage APIs to access queues:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/queue.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="96daa-120">Een Azure-opslag-verbindingsreeks instellen</span><span class="sxs-lookup"><span data-stu-id="96daa-120">Set up an Azure storage connection string</span></span>
<span data-ttu-id="96daa-121">Een Azure-opslag-client gebruikt een verbindingsreeks voor opslag voor het opslaan van eindpunten en referenties voor toegang tot gegevens beheerservices.</span><span class="sxs-lookup"><span data-stu-id="96daa-121">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="96daa-122">Wanneer u in een clienttoepassing uitvoert, moet u opgeven de verbindingsreeks voor opslag in de volgende indeling met de naam van uw opslagaccount en de toegangssleutel voor opslag voor de storage-account wordt vermeld in de [Azure Portal](https://portal.azure.com) voor de *AccountName* en *AccountKey* waarden.</span><span class="sxs-lookup"><span data-stu-id="96daa-122">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the storage access key for the storage account listed in the [Azure Portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="96daa-123">Zie voor informatie over de storage-accounts en toegangstoetsen, [over Azure Storage-Accounts](storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="96daa-123">For information on storage accounts and access keys, see [About Azure Storage Accounts](storage-create-storage-account.md).</span></span> <span data-ttu-id="96daa-124">Dit voorbeeld ziet hoe u een statisch veld voor het opslaan van de verbindingsreeks kunt declareren:</span><span class="sxs-lookup"><span data-stu-id="96daa-124">This example shows how you can declare a static field to hold the connection string:</span></span>  

```cpp
// Define the connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="96daa-125">Testen van uw toepassing in uw lokale Windows-computer, kunt u de Microsoft Azure [opslagemulator](storage-use-emulator.md) die is geïnstalleerd met de [Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="96daa-125">To test your application in your local Windows computer, you can use the Microsoft Azure [storage emulator](storage-use-emulator.md) that is installed with the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="96daa-126">De opslagemulator is een hulpprogramma dat de services Blob, wachtrijen en tabellen beschikbaar zijn in Azure op uw lokale ontwikkelcomputer simuleert.</span><span class="sxs-lookup"><span data-stu-id="96daa-126">The storage emulator is a utility that simulates the Blob, Queue, and Table services available in Azure on your local development machine.</span></span> <span data-ttu-id="96daa-127">Het volgende voorbeeld ziet u hoe u een statisch veld voor het opslaan van de verbindingsreeks naar uw lokale opslagemulator kunt declareren:</span><span class="sxs-lookup"><span data-stu-id="96daa-127">The following example shows how you can declare a static field to hold the connection string to your local storage emulator:</span></span>  

```cpp
// Define the connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="96daa-128">Voor het starten van de Azure-opslagemulator, selecteer de **Start** of drukt u op de **Windows** sleutel.</span><span class="sxs-lookup"><span data-stu-id="96daa-128">To start the Azure storage emulator, select the **Start** button or press the **Windows** key.</span></span> <span data-ttu-id="96daa-129">Begint te typen **Azure-Opslagemulator**, en selecteer **Microsoft Azure-Opslagemulator** uit de lijst met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="96daa-129">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from the list of applications.</span></span>

<span data-ttu-id="96daa-130">De volgende voorbeelden wordt ervan uitgegaan dat u een van deze twee methoden hebt gebruikt om op te halen van de verbindingsreeks voor opslag.</span><span class="sxs-lookup"><span data-stu-id="96daa-130">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="96daa-131">De verbindingsreeks ophalen</span><span class="sxs-lookup"><span data-stu-id="96daa-131">Retrieve your connection string</span></span>
<span data-ttu-id="96daa-132">U kunt de **cloud_storage_account** klasse vertegenwoordigt de informatie van uw Opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="96daa-132">You can use the **cloud_storage_account** class to represent your Storage Account information.</span></span> <span data-ttu-id="96daa-133">Voor het ophalen van gegevens over uw storage-account van de verbindingsreeks voor opslag, kunt u de **parseren** methode.</span><span class="sxs-lookup"><span data-stu-id="96daa-133">To retrieve your storage account information from the storage connection string, you can use the **parse** method.</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="how-to-create-a-queue"></a><span data-ttu-id="96daa-134">Procedure: een wachtrij maken</span><span class="sxs-lookup"><span data-stu-id="96daa-134">How to: Create a queue</span></span>
<span data-ttu-id="96daa-135">Een **cloud_queue_client** object kunt u profiteren van reference-objecten voor wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="96daa-135">A **cloud_queue_client** object lets you get reference objects for queues.</span></span> <span data-ttu-id="96daa-136">De volgende code maakt een **cloud_queue_client** object.</span><span class="sxs-lookup"><span data-stu-id="96daa-136">The following code creates a **cloud_queue_client** object.</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create a queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();
```

<span data-ttu-id="96daa-137">Gebruik de **cloud_queue_client** object verwijst naar de wachtrij die u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="96daa-137">Use the **cloud_queue_client** object to get a reference to the queue you want to use.</span></span> <span data-ttu-id="96daa-138">U kunt de wachtrij maken als deze niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="96daa-138">You can create the queue if it doesn't exist.</span></span>

```cpp
// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create the queue if it doesn't already exist.
 queue.create_if_not_exists();  
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="96daa-139">Procedure: een bericht in een wachtrij invoegen</span><span class="sxs-lookup"><span data-stu-id="96daa-139">How to: Insert a message into a queue</span></span>
<span data-ttu-id="96daa-140">Als u wilt invoegen van een bericht in een bestaande wachtrij maakt een nieuwe **cloud_queue_message**.</span><span class="sxs-lookup"><span data-stu-id="96daa-140">To insert a message into an existing queue, first create a new **cloud_queue_message**.</span></span> <span data-ttu-id="96daa-141">Daarna roept de **add_message** methode.</span><span class="sxs-lookup"><span data-stu-id="96daa-141">Next, call the **add_message** method.</span></span> <span data-ttu-id="96daa-142">Een **cloud_queue_message** kan worden gemaakt vanuit een tekenreeks of een **byte** matrix.</span><span class="sxs-lookup"><span data-stu-id="96daa-142">A **cloud_queue_message** can be created from either a string or a **byte** array.</span></span> <span data-ttu-id="96daa-143">Met deze code wordt er een wachtrij gemaakt (als deze nog niet bestaat) en het bericht 'Hello, World' toegevoegd:</span><span class="sxs-lookup"><span data-stu-id="96daa-143">Here is code which creates a queue (if it doesn't exist) and inserts the message 'Hello, World':</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create the queue if it doesn't already exist.
queue.create_if_not_exists();

// Create a message and add it to the queue.
azure::storage::cloud_queue_message message1(U("Hello, World"));
queue.add_message(message1);  
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="96daa-144">Hoe: bekijken van het volgende bericht</span><span class="sxs-lookup"><span data-stu-id="96daa-144">How to: Peek at the next message</span></span>
<span data-ttu-id="96daa-145">U kunt het bericht vooraan in een wachtrij bekijken zonder het te verwijderen uit de wachtrij door het aanroepen van de **peek_message** methode.</span><span class="sxs-lookup"><span data-stu-id="96daa-145">You can peek at the message in the front of a queue without removing it from the queue by calling the **peek_message** method.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Peek at the next message.
azure::storage::cloud_queue_message peeked_message = queue.peek_message();

// Output the message content.
std::wcout << U("Peeked message content: ") << peeked_message.content_as_string() << std::endl;
```

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="96daa-146">Procedure: de inhoud van een bericht in de wachtrij wijzigen</span><span class="sxs-lookup"><span data-stu-id="96daa-146">How to: Change the contents of a queued message</span></span>
<span data-ttu-id="96daa-147">U kunt de inhoud van een bericht in de wachtrij wijzigen.</span><span class="sxs-lookup"><span data-stu-id="96daa-147">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="96daa-148">Als het bericht een werktaak vertegenwoordigt, kunt u deze functie gebruiken om de status van de werktaak bij te werken.</span><span class="sxs-lookup"><span data-stu-id="96daa-148">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="96daa-149">Met de volgende code wordt het bericht in de wachtrij bijgewerkt met nieuwe inhoud en wordt de time-out voor de zichtbaarheid met 60 seconden verlengd.</span><span class="sxs-lookup"><span data-stu-id="96daa-149">The following code updates the queue message with new contents, and sets the visibility timeout to extend another 60 seconds.</span></span> <span data-ttu-id="96daa-150">Hiermee wordt de status van de werkitems die aan het bericht zijn gekoppeld, opgeslagen en krijgt de client een extra minuut om aan het bericht te blijven werken.</span><span class="sxs-lookup"><span data-stu-id="96daa-150">This saves the state of work associated with the message, and gives the client another minute to continue working on the message.</span></span> <span data-ttu-id="96daa-151">U kunt deze techniek gebruiken om uit meerdere stappen bestaande werkstromen in berichten in de wachtrij te volgen zonder dat u helemaal opnieuw hoeft te beginnen als een verwerkingsstap vanwege een hardware- of softwarefout is mislukt.</span><span class="sxs-lookup"><span data-stu-id="96daa-151">You could use this technique to track multi-step workflows on queue messages, without having to start over from the beginning if a processing step fails due to hardware or software failure.</span></span> <span data-ttu-id="96daa-152">Doorgaans houdt u ook een aantal voor nieuwe pogingen en als het bericht is meer dan n keren geprobeerd, verwijdert u het.</span><span class="sxs-lookup"><span data-stu-id="96daa-152">Typically, you would keep a retry count as well, and if the message is retried more than n times, you would delete it.</span></span> <span data-ttu-id="96daa-153">Dit biedt bescherming tegen berichten die een toepassingsfout activeren telkens wanneer ze worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="96daa-153">This protects against a message that triggers an application error each time it is processed.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_conection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get the message from the queue and update the message contents.
// The visibility timeout "0" means make it visible immediately.
// The visibility timeout "60" means the client can get another minute to continue
// working on the message.
azure::storage::cloud_queue_message changed_message = queue.get_message();

changed_message.set_content(U("Changed message"));
queue.update_message(changed_message, std::chrono::seconds(60), true);

// Output the message content.
std::wcout << U("Changed message content: ") << changed_message.content_as_string() << std::endl;  
```

## <a name="how-to-de-queue-the-next-message"></a><span data-ttu-id="96daa-154">Procedure: het volgende bericht uit de wachtrij</span><span class="sxs-lookup"><span data-stu-id="96daa-154">How to: De-queue the next message</span></span>
<span data-ttu-id="96daa-155">Met uw code wordt een bericht in twee stappen uit de wachtrij verwijderd.</span><span class="sxs-lookup"><span data-stu-id="96daa-155">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="96daa-156">Als u aanroept **get_message**, krijgt u het volgende bericht in een wachtrij.</span><span class="sxs-lookup"><span data-stu-id="96daa-156">When you call **get_message**, you get the next message in a queue.</span></span> <span data-ttu-id="96daa-157">Een bericht dat wordt geretourneerd door **get_message** wordt onzichtbaar voor andere codes die berichten lezen uit deze wachtrij.</span><span class="sxs-lookup"><span data-stu-id="96daa-157">A message returned from **get_message** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="96daa-158">Voor het voltooien van het bericht uit de wachtrij te verwijderen, moet u ook aanroepen **delete_message**.</span><span class="sxs-lookup"><span data-stu-id="96daa-158">To finish removing the message from the queue, you must also call **delete_message**.</span></span> <span data-ttu-id="96daa-159">Dit proces in twee stappen voor het verwijderen van een bericht zorgt ervoor dat als de code er niet in slaagt een bericht te verwerken vanwege hardware- of softwareproblemen, een ander exemplaar van uw code hetzelfde bericht kan ophalen en het opnieuw kan proberen.</span><span class="sxs-lookup"><span data-stu-id="96daa-159">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="96daa-160">Uw code haalt **delete_message** direct nadat het bericht is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="96daa-160">Your code calls **delete_message** right after the message has been processed.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get the next message.
azure::storage::cloud_queue_message dequeued_message = queue.get_message();
std::wcout << U("Dequeued message: ") << dequeued_message.content_as_string() << std::endl;

// Delete the message.
queue.delete_message(dequeued_message);
```

## <a name="how-to-leverage-additional-options-for-de-queuing-messages"></a><span data-ttu-id="96daa-161">Hoe: gebruikmaken van aanvullende opties voor berichten in de wachtrij plaatsen</span><span class="sxs-lookup"><span data-stu-id="96daa-161">How to: Leverage additional options for de-queuing messages</span></span>
<span data-ttu-id="96daa-162">Er zijn twee manieren waarop u het ophalen van berichten uit een wachtrij kunt aanpassen.</span><span class="sxs-lookup"><span data-stu-id="96daa-162">There are two ways you can customize message retrieval from a queue.</span></span> <span data-ttu-id="96daa-163">Ten eerste kunt u berichten batchgewijs (maximaal 32) ophalen.</span><span class="sxs-lookup"><span data-stu-id="96daa-163">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="96daa-164">Ten tweede kunt u een langere of kortere time-out voor onzichtbaarheid instellen, zodat uw code meer of minder tijd krijgt voor het volledig verwerken van elk bericht.</span><span class="sxs-lookup"><span data-stu-id="96daa-164">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="96daa-165">Het volgende codevoorbeeld wordt de **get_messages** methode om 20 berichten in één aanroep.</span><span class="sxs-lookup"><span data-stu-id="96daa-165">The following code example uses the **get_messages** method to get 20 messages in one call.</span></span> <span data-ttu-id="96daa-166">Vervolgens wordt verwerkt elke bericht met een **voor** lus.</span><span class="sxs-lookup"><span data-stu-id="96daa-166">Then it processes each message using a **for** loop.</span></span> <span data-ttu-id="96daa-167">De time-out voor onzichtbaarheid wordt ingesteld op vijf minuten voor elk bericht.</span><span class="sxs-lookup"><span data-stu-id="96daa-167">It also sets the invisibility timeout to five minutes for each message.</span></span> <span data-ttu-id="96daa-168">Let op: de vijf minuten voor alle berichten op hetzelfde moment start dus na 5 minuten zijn verstreken sinds de aanroep van **get_messages**, alle berichten die niet zijn verwijderd weer zichtbaar worden.</span><span class="sxs-lookup"><span data-stu-id="96daa-168">Note that the 5 minutes starts for all messages at the same time, so after 5 minutes have passed since the call to **get_messages**, any messages which have not been deleted will become visible again.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Dequeue some queue messages (maximum 32 at a time) and set their visibility timeout to
// 5 minutes (300 seconds).
azure::storage::queue_request_options options;
azure::storage::operation_context context;

// Retrieve 20 messages from the queue with a visibility timeout of 300 seconds.
std::vector<azure::storage::cloud_queue_message> messages = queue.get_messages(20, std::chrono::seconds(300), options, context);

for (auto it = messages.cbegin(); it != messages.cend(); ++it)
{
    // Display the contents of the message.
    std::wcout << U("Get: ") << it->content_as_string() << std::endl;
}
```

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="96daa-169">Hoe: lengte van de wachtrij ophalen</span><span class="sxs-lookup"><span data-stu-id="96daa-169">How to: Get the queue length</span></span>
<span data-ttu-id="96daa-170">U kunt een schatting ophalen van het aantal berichten in de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="96daa-170">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="96daa-171">De **download_attributes** methode vraagt de Queue-service voor het ophalen van de wachtrij-kenmerken, zoals het aantal berichten.</span><span class="sxs-lookup"><span data-stu-id="96daa-171">The **download_attributes** method asks the Queue service to retrieve the queue attributes, including the message count.</span></span> <span data-ttu-id="96daa-172">De **approximate_message_count** methode het geschatte aantal berichten in de wachtrij opgehaald.</span><span class="sxs-lookup"><span data-stu-id="96daa-172">The **approximate_message_count** method gets the approximate number of messages in the queue.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Fetch the queue attributes.
queue.download_attributes();

// Retrieve the cached approximate message count.
int cachedMessageCount = queue.approximate_message_count();

// Display number of messages.
std::wcout << U("Number of messages in queue: ") << cachedMessageCount << std::endl;  
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="96daa-173">Procedure: een wachtrij verwijderen</span><span class="sxs-lookup"><span data-stu-id="96daa-173">How to: Delete a queue</span></span>
<span data-ttu-id="96daa-174">Aanroepen voor het verwijderen van een wachtrij en alle berichten hierin de **delete_queue_if_exists** methode voor het object in de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="96daa-174">To delete a queue and all the messages contained in it, call the **delete_queue_if_exists** method on the queue object.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// If the queue exists and delete it.
queue.delete_queue_if_exists();  
```

## <a name="next-steps"></a><span data-ttu-id="96daa-175">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="96daa-175">Next steps</span></span>
<span data-ttu-id="96daa-176">Nu u de basisprincipes van Queue storage hebt geleerd, volgt u deze koppelingen voor meer informatie over Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="96daa-176">Now that you've learned the basics of Queue storage, follow these links to learn more about Azure Storage.</span></span>

* [<span data-ttu-id="96daa-177">Het Blob Storage gebruiken met C++</span><span class="sxs-lookup"><span data-stu-id="96daa-177">How to use Blob Storage from C++</span></span>](storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="96daa-178">Hoe Table Storage gebruiken met C++</span><span class="sxs-lookup"><span data-stu-id="96daa-178">How to use Table Storage from C++</span></span>](storage-c-plus-plus-how-to-use-tables.md)
* [<span data-ttu-id="96daa-179">Lijst met Azure Storage-Resources in C++</span><span class="sxs-lookup"><span data-stu-id="96daa-179">List Azure Storage Resources in C++</span></span>](storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="96daa-180">Opslagclientbibliotheek voor C++-verwijzing</span><span class="sxs-lookup"><span data-stu-id="96daa-180">Storage Client Library for C++ Reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="96daa-181">Documentatie bij Azure Storage</span><span class="sxs-lookup"><span data-stu-id="96daa-181">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)