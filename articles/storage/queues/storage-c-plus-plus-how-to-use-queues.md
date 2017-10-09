---
title: aaaHow toouse queue storage (C++) | Microsoft Docs
description: Meer informatie over hoe toouse Hallo queue storage-service in Azure. Voorbeelden zijn geschreven in C++.
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
ms.openlocfilehash: b0cddf017878e9fab87f47d24b2906e40c9f4ad5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-c"></a><span data-ttu-id="29534-104">Hoe toouse Queue Storage vanuit C++</span><span class="sxs-lookup"><span data-stu-id="29534-104">How toouse Queue Storage from C++</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="29534-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="29534-105">Overview</span></span>
<span data-ttu-id="29534-106">Deze handleiding leert u hoe tooperform algemene scenario's met behulp van hello Azure Queue storage-service.</span><span class="sxs-lookup"><span data-stu-id="29534-106">This guide will show you how tooperform common scenarios using hello Azure Queue storage service.</span></span> <span data-ttu-id="29534-107">Hallo-voorbeelden zijn geschreven in C++ en gebruiken van Hallo [Azure Storage-clientbibliotheek voor C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="29534-107">hello samples are written in C++ and use hello [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="29534-108">Hallo scenario's worden behandeld: **invoegen**, **inspecteren**, **ophalen**, en **verwijderen** wachtrij berichten, evenals  **maken en verwijderen van wachtrijen**.</span><span class="sxs-lookup"><span data-stu-id="29534-108">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

> [!NOTE]
> <span data-ttu-id="29534-109">Doel is van deze handleiding hello Azure Storage-clientbibliotheek voor C++ versie 1.0.0 en hoger.</span><span class="sxs-lookup"><span data-stu-id="29534-109">This guide targets hello Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="29534-110">Hallo aanbevolen versie is Storage-clientbibliotheek 2.2.0, die beschikbaar is via [NuGet](http://www.nuget.org/packages/wastorage) of [GitHub](http://github.com/Azure/azure-storage-cpp/).</span><span class="sxs-lookup"><span data-stu-id="29534-110">hello recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](http://github.com/Azure/azure-storage-cpp/).</span></span>
> 
> 

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="29534-111">Een C++-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="29534-111">Create a C++ application</span></span>
<span data-ttu-id="29534-112">In deze handleiding gebruikt u opslagfuncties die kunnen worden uitgevoerd binnen een C++-toepassing.</span><span class="sxs-lookup"><span data-stu-id="29534-112">In this guide, you will use storage features which can be run within a C++ application.</span></span>

<span data-ttu-id="29534-113">toodo geval is, moet u tooinstall hello Azure Storage-clientbibliotheek voor C++ en een Azure storage-account maken in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="29534-113">toodo so, you will need tooinstall hello Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>

<span data-ttu-id="29534-114">tooinstall hello Azure Storage-clientbibliotheek voor C++, kunt u Hallo volgende methoden:</span><span class="sxs-lookup"><span data-stu-id="29534-114">tooinstall hello Azure Storage Client Library for C++, you can use hello following methods:</span></span>

* <span data-ttu-id="29534-115">**Linux:** Hallo instructies gegeven in Hallo [Azure Storage-clientbibliotheek voor C++ Leesmij](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) pagina.</span><span class="sxs-lookup"><span data-stu-id="29534-115">**Linux:** Follow hello instructions given in hello [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>
* <span data-ttu-id="29534-116">**Windows:** In Visual Studio, klikt u op **Extra > NuGet Package Manager > Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="29534-116">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="29534-117">Type Hallo volgende opdracht in Hallo [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) en druk op **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="29534-117">Type hello following command into hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>

```  
Install-Package wastorage
```

## <a name="configure-your-application-tooaccess-queue-storage"></a><span data-ttu-id="29534-118">Uw toepassing tooaccess Queue Storage configureren</span><span class="sxs-lookup"><span data-stu-id="29534-118">Configure your application tooaccess Queue Storage</span></span>
<span data-ttu-id="29534-119">Toegevoegd Hallo volgende overzichten toohello boven in Hallo C++ bestand waar u toouse hello Azure storage-API's tooaccess wachtrijen bevatten:</span><span class="sxs-lookup"><span data-stu-id="29534-119">Add hello following include statements toohello top of hello C++ file where you want toouse hello Azure storage APIs tooaccess queues:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/queue.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="29534-120">Een Azure-opslag-verbindingsreeks instellen</span><span class="sxs-lookup"><span data-stu-id="29534-120">Set up an Azure storage connection string</span></span>
<span data-ttu-id="29534-121">Een Azure-opslag-client maakt gebruik van een storage connection string toostore eindpunten en referenties voor toegang tot gegevens beheerservices.</span><span class="sxs-lookup"><span data-stu-id="29534-121">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="29534-122">Wanneer een client-toepassing wordt uitgevoerd, moet u opgeven Hallo verbindingsreeks voor opslag in Hallo indeling te volgen, met behulp van Hallo-naam van uw storage-account en Hallo toegangssleutel voor opslag voor Hallo storage-account die worden vermeld in Hallo [Azure Portal](https://portal.azure.com)voor Hallo *AccountName* en *AccountKey* waarden.</span><span class="sxs-lookup"><span data-stu-id="29534-122">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello storage access key for hello storage account listed in hello [Azure Portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="29534-123">Zie voor informatie over de storage-accounts en toegangstoetsen, [over Azure Storage-Accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="29534-123">For information on storage accounts and access keys, see [About Azure Storage Accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json).</span></span> <span data-ttu-id="29534-124">Dit voorbeeld ziet hoe u een statisch veld toohold Hallo-verbindingsreeks kunt declareren:</span><span class="sxs-lookup"><span data-stu-id="29534-124">This example shows how you can declare a static field toohold hello connection string:</span></span>  

```cpp
// Define hello connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="29534-125">tootest uw toepassing in de lokale Windows-computer, kunt u Microsoft Azure Hallo [opslagemulator](../common/storage-use-emulator.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) die is geïnstalleerd met Hallo [Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="29534-125">tootest your application in your local Windows computer, you can use hello Microsoft Azure [storage emulator](../common/storage-use-emulator.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) that is installed with hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="29534-126">Hallo-opslagemulator is een hulpprogramma dat Hallo Blob, wachtrijen en tabellen services beschikbaar zijn in Azure op uw lokale ontwikkelcomputer simuleert.</span><span class="sxs-lookup"><span data-stu-id="29534-126">hello storage emulator is a utility that simulates hello Blob, Queue, and Table services available in Azure on your local development machine.</span></span> <span data-ttu-id="29534-127">Hallo volgende voorbeeld ziet u hoe u een statisch veld toohold Hallo connection string tooyour lokale opslagemulator kunt declareren:</span><span class="sxs-lookup"><span data-stu-id="29534-127">hello following example shows how you can declare a static field toohold hello connection string tooyour local storage emulator:</span></span>  

```cpp
// Define hello connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="29534-128">toostart hello Azure-opslagemulator Selecteer Hallo **Start** of drukt u op Hallo **Windows** sleutel.</span><span class="sxs-lookup"><span data-stu-id="29534-128">toostart hello Azure storage emulator, select hello **Start** button or press hello **Windows** key.</span></span> <span data-ttu-id="29534-129">Begint te typen **Azure-Opslagemulator**, en selecteer **Microsoft Azure-Opslagemulator** in Hallo lijst met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="29534-129">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from hello list of applications.</span></span>

<span data-ttu-id="29534-130">Hallo volgende voorbeelden wordt ervan uitgegaan dat u een van deze twee methoden tooget Hallo-opslagverbindingsreeks hebt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="29534-130">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="29534-131">De verbindingsreeks ophalen</span><span class="sxs-lookup"><span data-stu-id="29534-131">Retrieve your connection string</span></span>
<span data-ttu-id="29534-132">U kunt Hallo **cloud_storage_account** klasse toorepresent uw Storage-Account.</span><span class="sxs-lookup"><span data-stu-id="29534-132">You can use hello **cloud_storage_account** class toorepresent your Storage Account information.</span></span> <span data-ttu-id="29534-133">tooretrieve uw opslag accountgegevens van de opslagverbindingsreeks hello, kunt u Hallo **parseren** methode.</span><span class="sxs-lookup"><span data-stu-id="29534-133">tooretrieve your storage account information from hello storage connection string, you can use hello **parse** method.</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="how-to-create-a-queue"></a><span data-ttu-id="29534-134">Procedure: een wachtrij maken</span><span class="sxs-lookup"><span data-stu-id="29534-134">How to: Create a queue</span></span>
<span data-ttu-id="29534-135">Een **cloud_queue_client** object kunt u profiteren van reference-objecten voor wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="29534-135">A **cloud_queue_client** object lets you get reference objects for queues.</span></span> <span data-ttu-id="29534-136">Hallo volgende code maakt een **cloud_queue_client** object.</span><span class="sxs-lookup"><span data-stu-id="29534-136">hello following code creates a **cloud_queue_client** object.</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create a queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();
```

<span data-ttu-id="29534-137">Gebruik Hallo **cloud_queue_client** tooget een verwijzing toohello wachtrij die u wilt dat toouse object.</span><span class="sxs-lookup"><span data-stu-id="29534-137">Use hello **cloud_queue_client** object tooget a reference toohello queue you want toouse.</span></span> <span data-ttu-id="29534-138">U kunt Hallo wachtrij maken als deze niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="29534-138">You can create hello queue if it doesn't exist.</span></span>

```cpp
// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create hello queue if it doesn't already exist.
 queue.create_if_not_exists();  
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="29534-139">Procedure: een bericht in een wachtrij invoegen</span><span class="sxs-lookup"><span data-stu-id="29534-139">How to: Insert a message into a queue</span></span>
<span data-ttu-id="29534-140">een bericht in een bestaande wachtrij tooinsert eerst maakt u een nieuwe **cloud_queue_message**.</span><span class="sxs-lookup"><span data-stu-id="29534-140">tooinsert a message into an existing queue, first create a new **cloud_queue_message**.</span></span> <span data-ttu-id="29534-141">Daarna roept Hallo **add_message** methode.</span><span class="sxs-lookup"><span data-stu-id="29534-141">Next, call hello **add_message** method.</span></span> <span data-ttu-id="29534-142">Een **cloud_queue_message** kan worden gemaakt vanuit een tekenreeks of een **byte** matrix.</span><span class="sxs-lookup"><span data-stu-id="29534-142">A **cloud_queue_message** can be created from either a string or a **byte** array.</span></span> <span data-ttu-id="29534-143">Hier volgt de code die een wachtrij maakt (als deze niet bestaat) en voegt het Hallo-bericht 'Hello, World':</span><span class="sxs-lookup"><span data-stu-id="29534-143">Here is code which creates a queue (if it doesn't exist) and inserts hello message 'Hello, World':</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create hello queue if it doesn't already exist.
queue.create_if_not_exists();

// Create a message and add it toohello queue.
azure::storage::cloud_queue_message message1(U("Hello, World"));
queue.add_message(message1);  
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="29534-144">Hoe: bekijken van volgende Hallo-bericht</span><span class="sxs-lookup"><span data-stu-id="29534-144">How to: Peek at hello next message</span></span>
<span data-ttu-id="29534-145">U kunt bekijken van Hallo-bericht in Hallo begin van een wachtrij zonder het te verwijderen uit de wachtrij Hallo door aanroepen Hallo **peek_message** methode.</span><span class="sxs-lookup"><span data-stu-id="29534-145">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **peek_message** method.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Peek at hello next message.
azure::storage::cloud_queue_message peeked_message = queue.peek_message();

// Output hello message content.
std::wcout << U("Peeked message content: ") << peeked_message.content_as_string() << std::endl;
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="29534-146">Hoe: Hallo inhoud van een bericht in de wachtrij wijzigen</span><span class="sxs-lookup"><span data-stu-id="29534-146">How to: Change hello contents of a queued message</span></span>
<span data-ttu-id="29534-147">U kunt Hallo inhoud van een bericht in-place in Hallo wachtrij wijzigen.</span><span class="sxs-lookup"><span data-stu-id="29534-147">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="29534-148">Als het Hallo-bericht een werktaak vertegenwoordigt, kunt u deze functie tooupdate Hallo status van de werktaak hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="29534-148">If hello message represents a work task, you could use this feature tooupdate hello status of hello work task.</span></span> <span data-ttu-id="29534-149">Hallo na code Hallo-bericht van wachtrij bijgewerkt met nieuwe inhoud en sets Hallo zichtbaarheid time-out tooextend 60 seconden.</span><span class="sxs-lookup"><span data-stu-id="29534-149">hello following code updates hello queue message with new contents, and sets hello visibility timeout tooextend another 60 seconds.</span></span> <span data-ttu-id="29534-150">Hallo-status van de werkitems die zijn gekoppeld aan het Hallo-bericht opgeslagen, en geeft Hallo-client een andere minuut toocontinue werkt op het Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="29534-150">This saves hello state of work associated with hello message, and gives hello client another minute toocontinue working on hello message.</span></span> <span data-ttu-id="29534-151">U kunt deze techniek tootrack meerdere stappen bestaande werkstromen op Wachtrijberichten, zonder toostart via van Hallo begin als een verwerkingsstap vanwege problemen met toohardware of software.</span><span class="sxs-lookup"><span data-stu-id="29534-151">You could use this technique tootrack multi-step workflows on queue messages, without having toostart over from hello beginning if a processing step fails due toohardware or software failure.</span></span> <span data-ttu-id="29534-152">Doorgaans houdt u ook een aantal voor nieuwe pogingen en als het Hallo-bericht is meer dan n keren geprobeerd, verwijdert u het.</span><span class="sxs-lookup"><span data-stu-id="29534-152">Typically, you would keep a retry count as well, and if hello message is retried more than n times, you would delete it.</span></span> <span data-ttu-id="29534-153">Dit biedt bescherming tegen berichten die een toepassingsfout activeren telkens wanneer ze worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="29534-153">This protects against a message that triggers an application error each time it is processed.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_conection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get hello message from hello queue and update hello message contents.
// hello visibility timeout "0" means make it visible immediately.
// hello visibility timeout "60" means hello client can get another minute toocontinue
// working on hello message.
azure::storage::cloud_queue_message changed_message = queue.get_message();

changed_message.set_content(U("Changed message"));
queue.update_message(changed_message, std::chrono::seconds(60), true);

// Output hello message content.
std::wcout << U("Changed message content: ") << changed_message.content_as_string() << std::endl;  
```

## <a name="how-to-de-queue-hello-next-message"></a><span data-ttu-id="29534-154">Procedure: het volgende Hallo-bericht uit de wachtrij</span><span class="sxs-lookup"><span data-stu-id="29534-154">How to: De-queue hello next message</span></span>
<span data-ttu-id="29534-155">Met uw code wordt een bericht in twee stappen uit de wachtrij verwijderd.</span><span class="sxs-lookup"><span data-stu-id="29534-155">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="29534-156">Als u aanroept **get_message**, krijgt u het volgende Hallo-bericht in een wachtrij.</span><span class="sxs-lookup"><span data-stu-id="29534-156">When you call **get_message**, you get hello next message in a queue.</span></span> <span data-ttu-id="29534-157">Een bericht dat wordt geretourneerd door **get_message** wordt onzichtbaar tooany andere codes die berichten lezen uit deze wachtrij.</span><span class="sxs-lookup"><span data-stu-id="29534-157">A message returned from **get_message** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="29534-158">toofinish verwijderen Hallo-bericht uit de wachtrij hello, moet u ook aanroepen **delete_message**.</span><span class="sxs-lookup"><span data-stu-id="29534-158">toofinish removing hello message from hello queue, you must also call **delete_message**.</span></span> <span data-ttu-id="29534-159">Dit proces in twee stappen van het verwijderen van een bericht zorgt ervoor dat als uw code mislukt tooprocess een bericht vanwege problemen toohardware of software, een ander exemplaar van uw code krijgt hetzelfde bericht Hallo en probeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="29534-159">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="29534-160">Uw code haalt **delete_message** direct nadat het Hallo-bericht is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="29534-160">Your code calls **delete_message** right after hello message has been processed.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get hello next message.
azure::storage::cloud_queue_message dequeued_message = queue.get_message();
std::wcout << U("Dequeued message: ") << dequeued_message.content_as_string() << std::endl;

// Delete hello message.
queue.delete_message(dequeued_message);
```

## <a name="how-to-leverage-additional-options-for-de-queuing-messages"></a><span data-ttu-id="29534-161">Hoe: gebruikmaken van aanvullende opties voor berichten in de wachtrij plaatsen</span><span class="sxs-lookup"><span data-stu-id="29534-161">How to: Leverage additional options for de-queuing messages</span></span>
<span data-ttu-id="29534-162">Er zijn twee manieren waarop u het ophalen van berichten uit een wachtrij kunt aanpassen.</span><span class="sxs-lookup"><span data-stu-id="29534-162">There are two ways you can customize message retrieval from a queue.</span></span> <span data-ttu-id="29534-163">U krijgt eerst een batch met berichten (omhoog too32).</span><span class="sxs-lookup"><span data-stu-id="29534-163">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="29534-164">Ten tweede kunt u instellen een time-out voor onzichtbaarheid langer of korter, zodat uw code meer of minder tijd toofully elk bericht niet verwerken.</span><span class="sxs-lookup"><span data-stu-id="29534-164">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="29534-165">Hallo volgende codevoorbeeld maakt gebruik van Hallo **get_messages** methode tooget 20 berichten in één aanroep.</span><span class="sxs-lookup"><span data-stu-id="29534-165">hello following code example uses hello **get_messages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="29534-166">Vervolgens wordt verwerkt elke bericht met een **voor** lus.</span><span class="sxs-lookup"><span data-stu-id="29534-166">Then it processes each message using a **for** loop.</span></span> <span data-ttu-id="29534-167">Hallo onzichtbaarheid toofive minuten voor de time-out voor elk bericht wordt ook ingesteld.</span><span class="sxs-lookup"><span data-stu-id="29534-167">It also sets hello invisibility timeout toofive minutes for each message.</span></span> <span data-ttu-id="29534-168">Houd er rekening mee dat Hallo 5 minuten voor alle berichten op Hallo dezelfde time begint, betekent dat als er 5 minuten zijn verstreken sinds de aanroep hello te**get_messages**, alle berichten die niet zijn verwijderd weer zichtbaar worden.</span><span class="sxs-lookup"><span data-stu-id="29534-168">Note that hello 5 minutes starts for all messages at hello same time, so after 5 minutes have passed since hello call too**get_messages**, any messages which have not been deleted will become visible again.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Dequeue some queue messages (maximum 32 at a time) and set their visibility timeout to
// 5 minutes (300 seconds).
azure::storage::queue_request_options options;
azure::storage::operation_context context;

// Retrieve 20 messages from hello queue with a visibility timeout of 300 seconds.
std::vector<azure::storage::cloud_queue_message> messages = queue.get_messages(20, std::chrono::seconds(300), options, context);

for (auto it = messages.cbegin(); it != messages.cend(); ++it)
{
    // Display hello contents of hello message.
    std::wcout << U("Get: ") << it->content_as_string() << std::endl;
}
```

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="29534-169">Hoe: Hallo wachtrijlengte ophalen</span><span class="sxs-lookup"><span data-stu-id="29534-169">How to: Get hello queue length</span></span>
<span data-ttu-id="29534-170">U kunt een schatting maken van het aantal berichten Hallo krijgen in een wachtrij.</span><span class="sxs-lookup"><span data-stu-id="29534-170">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="29534-171">Hallo **download_attributes** methode vraagt Hallo wachtrij service tooretrieve Hallo wachtrij-kenmerken, zoals aantal Hallo-berichten.</span><span class="sxs-lookup"><span data-stu-id="29534-171">hello **download_attributes** method asks hello Queue service tooretrieve hello queue attributes, including hello message count.</span></span> <span data-ttu-id="29534-172">Hallo **approximate_message_count** methode Hallo kunt u het geschatte aantal berichten in wachtrij Hallo opgehaald.</span><span class="sxs-lookup"><span data-stu-id="29534-172">hello **approximate_message_count** method gets hello approximate number of messages in hello queue.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Fetch hello queue attributes.
queue.download_attributes();

// Retrieve hello cached approximate message count.
int cachedMessageCount = queue.approximate_message_count();

// Display number of messages.
std::wcout << U("Number of messages in queue: ") << cachedMessageCount << std::endl;  
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="29534-173">Procedure: een wachtrij verwijderen</span><span class="sxs-lookup"><span data-stu-id="29534-173">How to: Delete a queue</span></span>
<span data-ttu-id="29534-174">een wachtrij en alle Hallo-berichten die zijn opgenomen in deze aanroep Hallo toodelete **delete_queue_if_exists** methode op Hallo wachtrij-object.</span><span class="sxs-lookup"><span data-stu-id="29534-174">toodelete a queue and all hello messages contained in it, call hello **delete_queue_if_exists** method on hello queue object.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// If hello queue exists and delete it.
queue.delete_queue_if_exists();  
```

## <a name="next-steps"></a><span data-ttu-id="29534-175">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="29534-175">Next steps</span></span>
<span data-ttu-id="29534-176">Nu u Hallo basisprincipes van Queue storage hebt geleerd, volgt u deze koppelingen toolearn meer over Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="29534-176">Now that you've learned hello basics of Queue storage, follow these links toolearn more about Azure Storage.</span></span>

* [<span data-ttu-id="29534-177">Hoe toouse C++ Blob-opslag</span><span class="sxs-lookup"><span data-stu-id="29534-177">How toouse Blob Storage from C++</span></span>](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="29534-178">Hoe toouse Table Storage uit het C++</span><span class="sxs-lookup"><span data-stu-id="29534-178">How toouse Table Storage from C++</span></span>](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="29534-179">Lijst met Azure Storage-Resources in C++</span><span class="sxs-lookup"><span data-stu-id="29534-179">List Azure Storage Resources in C++</span></span>](../common/storage-c-plus-plus-enumeration.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)
* [<span data-ttu-id="29534-180">Opslagclientbibliotheek voor C++-verwijzing</span><span class="sxs-lookup"><span data-stu-id="29534-180">Storage Client Library for C++ Reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="29534-181">Documentatie bij Azure Storage</span><span class="sxs-lookup"><span data-stu-id="29534-181">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)