---
title: Hoe Queue storage gebruiken met Java | Microsoft Docs
description: Informatie over het gebruik van de Azure Queue-service maken en verwijderen van wachtrijen, en invoegen, ophalen en verwijderen van berichten. Voorbeelden die zijn geschreven in Java.
services: storage
documentationcenter: java
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 68cecc8e-38c9-4a24-99e8-cb722bc63cf9
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 03faea986221453d1862ff0f0d6d1ec21f92f3bb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-queue-storage-from-java"></a><span data-ttu-id="d6b62-104">Queue Storage gebruiken met Java</span><span class="sxs-lookup"><span data-stu-id="d6b62-104">How to use Queue storage from Java</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a><span data-ttu-id="d6b62-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="d6b62-105">Overview</span></span>
<span data-ttu-id="d6b62-106">Deze handleiding leert u hoe u veelvoorkomende scenario's met behulp van de Azure Queue storage-service uitvoert.</span><span class="sxs-lookup"><span data-stu-id="d6b62-106">This guide will show you how to perform common scenarios using the Azure Queue storage service.</span></span> <span data-ttu-id="d6b62-107">De voorbeelden zijn geschreven in Java en gebruik de [Azure-opslag-SDK voor Java][Azure Storage SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="d6b62-107">The samples are written in Java and use the [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="d6b62-108">De scenario's worden behandeld: **invoegen**, **inspecteren**, **ophalen**, en **verwijderen** wachtrij berichten, evenals **maken** en **verwijderen** wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="d6b62-108">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating** and **deleting** queues.</span></span> <span data-ttu-id="d6b62-109">Zie voor meer informatie over wachtrijen de [Vervolgstappen](#Next-Steps) sectie.</span><span class="sxs-lookup"><span data-stu-id="d6b62-109">For more information on queues, see the [Next steps](#Next-Steps) section.</span></span>

<span data-ttu-id="d6b62-110">Opmerking: Een SDK is beschikbaar voor ontwikkelaars die werken met Azure Storage op Android-apparaten.</span><span class="sxs-lookup"><span data-stu-id="d6b62-110">Note: An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="d6b62-111">Zie voor meer informatie de [Azure-opslag-SDK voor Android][Azure Storage SDK for Android].</span><span class="sxs-lookup"><span data-stu-id="d6b62-111">For more information, see the [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="d6b62-112">Een Java-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="d6b62-112">Create a Java application</span></span>
<span data-ttu-id="d6b62-113">In deze handleiding gebruikt u opslagfuncties die kunnen worden uitgevoerd binnen een Java-toepassing lokaal of in de code die wordt uitgevoerd binnen een Webrol of worker-rol in Azure.</span><span class="sxs-lookup"><span data-stu-id="d6b62-113">In this guide, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="d6b62-114">Om dit te doen, moet u Java Development Kit (JDK) installeren en een Azure storage-account maken in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="d6b62-114">To do so, you will need to install the Java Development Kit (JDK) and create an Azure storage account in your Azure subscription.</span></span> <span data-ttu-id="d6b62-115">Als u dit hebt gedaan, moet u controleren of uw ontwikkelsysteem voldoet aan de minimale vereisten en afhankelijkheden die worden vermeld in de [Azure-opslag-SDK voor Java] [ Azure Storage SDK for Java] opslagplaats op GitHub.</span><span class="sxs-lookup"><span data-stu-id="d6b62-115">Once you have done so, you will need to verify that your development system meets the minimum requirements and dependencies which are listed in the [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="d6b62-116">Als uw systeem aan deze vereisten voldoet, kunt u de instructies voor het downloaden en installeren van de Azure Storage-bibliotheken voor Java op uw systeem vanuit die opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="d6b62-116">If your system meets those requirements, you can follow the instructions for downloading and installing the Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="d6b62-117">Nadat u deze taken hebt voltooid, kunt u zich kunt maken van een Java-toepassing die gebruikmaakt van de voorbeelden in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="d6b62-117">Once you have completed those tasks, you will be able to create a Java application which uses the examples in this article.</span></span>

## <a name="configure-your-application-to-access-queue-storage"></a><span data-ttu-id="d6b62-118">Uw toepassing configureren voor toegang tot opslag van de wachtrij</span><span class="sxs-lookup"><span data-stu-id="d6b62-118">Configure your application to access queue storage</span></span>
<span data-ttu-id="d6b62-119">De volgende importinstructies toevoegen aan het begin van de Java-bestand waarin u gebruiken van Azure storage-API's wilt voor toegang tot wachtrijen:</span><span class="sxs-lookup"><span data-stu-id="d6b62-119">Add the following import statements to the top of the Java file where you want to use Azure storage APIs to access queues:</span></span>

```java
// Include the following imports to use queue APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.queue.*;
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="d6b62-120">Een Azure-opslag-verbindingsreeks instellen</span><span class="sxs-lookup"><span data-stu-id="d6b62-120">Setup an Azure storage connection string</span></span>
<span data-ttu-id="d6b62-121">Een Azure-opslag-client gebruikt een verbindingsreeks voor opslag voor het opslaan van eindpunten en referenties voor toegang tot gegevens beheerservices.</span><span class="sxs-lookup"><span data-stu-id="d6b62-121">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="d6b62-122">Wanneer u in een clienttoepassing uitvoert, moet u opgeven de verbindingsreeks voor opslag in de volgende indeling met de naam van uw opslagaccount en de primaire toegangssleutel voor het opslagaccount vermeld in de [Azure Portal](https://portal.azure.com) voor de *AccountName* en *AccountKey* waarden.</span><span class="sxs-lookup"><span data-stu-id="d6b62-122">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the Primary access key for the storage account listed in the [Azure Portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="d6b62-123">Dit voorbeeld ziet hoe u een statisch veld voor het opslaan van de verbindingsreeks kunt declareren:</span><span class="sxs-lookup"><span data-stu-id="d6b62-123">This example shows how you can declare a static field to hold the connection string:</span></span>

```java
// Define the connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="d6b62-124">In een toepassing in een rol in Microsoft Azure wordt uitgevoerd, kan deze tekenreeks worden opgeslagen in het serviceconfiguratiebestand *ServiceConfiguration.cscfg*, en kunnen worden geopend met een aanroep naar de **RoleEnvironment.getConfigurationSettings** methode.</span><span class="sxs-lookup"><span data-stu-id="d6b62-124">In an application running within a role in Microsoft Azure, this string can be stored in the service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call to the **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="d6b62-125">Hier volgt een voorbeeld van het ophalen van de verbindingsreeks uit een **instelling** element met de naam *StorageConnectionString* in het configuratiebestand van de service:</span><span class="sxs-lookup"><span data-stu-id="d6b62-125">Here's an example of getting the connection string from a **Setting** element named *StorageConnectionString* in the service configuration file:</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="d6b62-126">De volgende voorbeelden wordt ervan uitgegaan dat u een van deze twee methoden hebt gebruikt om op te halen van de verbindingsreeks voor opslag.</span><span class="sxs-lookup"><span data-stu-id="d6b62-126">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="d6b62-127">Procedure: een wachtrij maken</span><span class="sxs-lookup"><span data-stu-id="d6b62-127">How to: Create a queue</span></span>
<span data-ttu-id="d6b62-128">Een **CloudQueueClient** object kunt u profiteren van reference-objecten voor wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="d6b62-128">A **CloudQueueClient** object lets you get reference objects for queues.</span></span> <span data-ttu-id="d6b62-129">De volgende code maakt een **CloudQueueClient** object.</span><span class="sxs-lookup"><span data-stu-id="d6b62-129">The following code creates a **CloudQueueClient** object.</span></span> <span data-ttu-id="d6b62-130">(Opmerking: Er zijn aanvullende manieren maken **CloudStorageAccount** objecten; voor meer informatie Zie **CloudStorageAccount** in de [naslaginformatie over Azure Storage Client SDK].)</span><span class="sxs-lookup"><span data-stu-id="d6b62-130">(Note: There are additional ways to create **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in the [Azure Storage Client SDK Reference].)</span></span>

<span data-ttu-id="d6b62-131">Gebruik de **CloudQueueClient** object verwijst naar de wachtrij die u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d6b62-131">Use the **CloudQueueClient** object to get a reference to the queue you want to use.</span></span> <span data-ttu-id="d6b62-132">U kunt de wachtrij maken als deze niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="d6b62-132">You can create the queue if it doesn't exist.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

   // Create the queue client.
   CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

   // Retrieve a reference to a queue.
   CloudQueue queue = queueClient.getQueueReference("myqueue");

   // Create the queue if it doesn't already exist.
   queue.createIfNotExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-add-a-message-to-a-queue"></a><span data-ttu-id="d6b62-133">Procedure: een bericht toevoegen aan een wachtrij</span><span class="sxs-lookup"><span data-stu-id="d6b62-133">How to: Add a message to a queue</span></span>
<span data-ttu-id="d6b62-134">Voor het invoegen van een bericht in een bestaande wachtrij maakt u eerst een nieuwe **CloudQueueMessage**.</span><span class="sxs-lookup"><span data-stu-id="d6b62-134">To insert a message into an existing queue, first create a new **CloudQueueMessage**.</span></span> <span data-ttu-id="d6b62-135">Daarna roept de **addMessage** methode.</span><span class="sxs-lookup"><span data-stu-id="d6b62-135">Next, call the **addMessage** method.</span></span> <span data-ttu-id="d6b62-136">Een **CloudQueueMessage** kan worden gemaakt vanuit een tekenreeks (in UTF-8-indeling) of een byte-matrix.</span><span class="sxs-lookup"><span data-stu-id="d6b62-136">A **CloudQueueMessage** can be created from either a string (in UTF-8 format) or a byte array.</span></span> <span data-ttu-id="d6b62-137">Deze code wordt een wachtrij maakt (als deze niet bestaat) en het bericht "Hallo, wereld".</span><span class="sxs-lookup"><span data-stu-id="d6b62-137">Here is code which creates a queue (if it doesn't exist) and inserts the message "Hello, World".</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Create the queue if it doesn't already exist.
    queue.createIfNotExists();

    // Create a message and add it to the queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    queue.addMessage(message);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="d6b62-138">Hoe: bekijken van het volgende bericht</span><span class="sxs-lookup"><span data-stu-id="d6b62-138">How to: Peek at the next message</span></span>
<span data-ttu-id="d6b62-139">U kunt het bericht vooraan in een wachtrij bekijken zonder het te verwijderen uit de wachtrij door aan te roepen **peekMessage**.</span><span class="sxs-lookup"><span data-stu-id="d6b62-139">You can peek at the message in the front of a queue without removing it from the queue by calling **peekMessage**.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Peek at the next message.
    CloudQueueMessage peekedMessage = queue.peekMessage();

    // Output the message value.
    if (peekedMessage != null)
    {
      System.out.println(peekedMessage.getMessageContentAsString());
   }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="d6b62-140">Procedure: de inhoud van een bericht in de wachtrij wijzigen</span><span class="sxs-lookup"><span data-stu-id="d6b62-140">How to: Change the contents of a queued message</span></span>
<span data-ttu-id="d6b62-141">U kunt de inhoud van een bericht in de wachtrij wijzigen.</span><span class="sxs-lookup"><span data-stu-id="d6b62-141">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="d6b62-142">Als het bericht een werktaak vertegenwoordigt, kunt u deze functie gebruiken om de status van de werktaak bij te werken.</span><span class="sxs-lookup"><span data-stu-id="d6b62-142">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="d6b62-143">Met de volgende code wordt het bericht in de wachtrij bijgewerkt met nieuwe inhoud en wordt de time-out voor de zichtbaarheid met 60 seconden verlengd.</span><span class="sxs-lookup"><span data-stu-id="d6b62-143">The following code updates the queue message with new contents, and sets the visibility timeout to extend another 60 seconds.</span></span> <span data-ttu-id="d6b62-144">Hiermee wordt de status van de werkitems die aan het bericht zijn gekoppeld, opgeslagen en krijgt de client een extra minuut om aan het bericht te blijven werken.</span><span class="sxs-lookup"><span data-stu-id="d6b62-144">This saves the state of work associated with the message, and gives the client another minute to continue working on the message.</span></span> <span data-ttu-id="d6b62-145">U kunt deze techniek gebruiken om uit meerdere stappen bestaande werkstromen in berichten in de wachtrij te volgen zonder dat u helemaal opnieuw hoeft te beginnen als een verwerkingsstap vanwege een hardware- of softwarefout is mislukt.</span><span class="sxs-lookup"><span data-stu-id="d6b62-145">You could use this technique to track multi-step workflows on queue messages, without having to start over from the beginning if a processing step fails due to hardware or software failure.</span></span> <span data-ttu-id="d6b62-146">Doorgaans houdt u ook het aantal nieuwe pogingen bij en als het bericht meer dan *n* keer opnieuw is geprobeerd, verwijdert u het.</span><span class="sxs-lookup"><span data-stu-id="d6b62-146">Typically, you would keep a retry count as well, and if the message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="d6b62-147">Dit biedt bescherming tegen berichten die een toepassingsfout activeren telkens wanneer ze worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="d6b62-147">This protects against a message that triggers an application error each time it is processed.</span></span>

<span data-ttu-id="d6b62-148">De volgende code voorbeeld gezocht in de wachtrij van berichten, zoekt de client het eerste bericht dat overeenkomt met "Hallo, wereld" voor de inhoud vervolgens wijzigt het bericht inhoud en wordt afgesloten.</span><span class="sxs-lookup"><span data-stu-id="d6b62-148">The following code sample searches through the queue of messages, locates the first message that matches "Hello, World" for the content, then modifies the message content and exits.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // The maximum number of messages that can be retrieved is 32.
    final int MAX_NUMBER_OF_MESSAGES_TO_PEEK = 32;

    // Loop through the messages in the queue.
    for (CloudQueueMessage message : queue.retrieveMessages(MAX_NUMBER_OF_MESSAGES_TO_PEEK,1,null,null))
    {
        // Check for a specific string.
        if (message.getMessageContentAsString().equals("Hello, World"))
        {
            // Modify the content of the first matching message.
            message.setMessageContent("Updated contents.");
            // Set it to be visible in 30 seconds.
            EnumSet<MessageUpdateFields> updateFields =
                EnumSet.of(MessageUpdateFields.CONTENT,
                MessageUpdateFields.VISIBILITY);
            // Update the message.
            queue.updateMessage(message, 30, updateFields, null, null);
            break;
        }
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

<span data-ttu-id="d6b62-149">U kunt ook updates het volgende codevoorbeeld alleen het eerste zichtbare bericht in de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="d6b62-149">Alternatively, the following code sample updates just the first visible message on the queue.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve the first visible message in the queue.
    CloudQueueMessage message = queue.retrieveMessage();

    if (message != null)
    {
        // Modify the message content.
        message.setMessageContent("Updated contents.");
        // Set it to be visible in 60 seconds.
        EnumSet<MessageUpdateFields> updateFields =
            EnumSet.of(MessageUpdateFields.CONTENT,
            MessageUpdateFields.VISIBILITY);
        // Update the message.
        queue.updateMessage(message, 60, updateFields, null, null);
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="d6b62-150">Hoe: lengte van de wachtrij ophalen</span><span class="sxs-lookup"><span data-stu-id="d6b62-150">How to: Get the queue length</span></span>
<span data-ttu-id="d6b62-151">U kunt een schatting ophalen van het aantal berichten in de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="d6b62-151">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="d6b62-152">De **downloadAttributes** methode vraagt de Queue-service voor verschillende huidige waarden, met inbegrip van een telling van het aantal berichten in een wachtrij zijn.</span><span class="sxs-lookup"><span data-stu-id="d6b62-152">The **downloadAttributes** method asks the Queue service for several current values, including a count of how many messages are in a queue.</span></span> <span data-ttu-id="d6b62-153">Het aantal is alleen een benadering omdat berichten kunnen worden toegevoegd of verwijderd nadat de Queue-service op uw aanvraag reageert.</span><span class="sxs-lookup"><span data-stu-id="d6b62-153">The count is only approximate because messages can be added or removed after the Queue service responds to your request.</span></span> <span data-ttu-id="d6b62-154">De **getApproximateMessageCount** methode retourneert de laatste waarde die is opgehaald door de aanroep **downloadAttributes**, zonder de Queue-service aanroepen.</span><span class="sxs-lookup"><span data-stu-id="d6b62-154">The **getApproximateMessageCount** method returns the last value retrieved by the call to **downloadAttributes**, without calling the Queue service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

   // Download the approximate message count from the server.
    queue.downloadAttributes();

    // Retrieve the newly cached approximate message count.
    long cachedMessageCount = queue.getApproximateMessageCount();

    // Display the queue length.
    System.out.println(String.format("Queue length: %d", cachedMessageCount));
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-dequeue-the-next-message"></a><span data-ttu-id="d6b62-155">Procedure: het volgende bericht in wachtrij</span><span class="sxs-lookup"><span data-stu-id="d6b62-155">How to: Dequeue the next message</span></span>
<span data-ttu-id="d6b62-156">Uw code dequeues een bericht van een wachtrij in twee stappen.</span><span class="sxs-lookup"><span data-stu-id="d6b62-156">Your code dequeues a message from a queue in two steps.</span></span> <span data-ttu-id="d6b62-157">Als u aanroept **retrieveMessage**, krijgt u het volgende bericht in een wachtrij.</span><span class="sxs-lookup"><span data-stu-id="d6b62-157">When you call **retrieveMessage**, you get the next message in a queue.</span></span> <span data-ttu-id="d6b62-158">Een bericht dat wordt geretourneerd door **retrieveMessage** wordt onzichtbaar voor andere codes die berichten lezen uit deze wachtrij.</span><span class="sxs-lookup"><span data-stu-id="d6b62-158">A message returned from **retrieveMessage** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="d6b62-159">Standaard blijft het bericht onzichtbaar gedurende 30 seconden.</span><span class="sxs-lookup"><span data-stu-id="d6b62-159">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="d6b62-160">Voor het voltooien van het bericht uit de wachtrij te verwijderen, moet u ook aanroepen **deleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="d6b62-160">To finish removing the message from the queue, you must also call **deleteMessage**.</span></span> <span data-ttu-id="d6b62-161">Dit proces in twee stappen voor het verwijderen van een bericht zorgt ervoor dat als de code er niet in slaagt een bericht te verwerken vanwege hardware- of softwareproblemen, een ander exemplaar van uw code hetzelfde bericht kan ophalen en het opnieuw kan proberen.</span><span class="sxs-lookup"><span data-stu-id="d6b62-161">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="d6b62-162">Uw code haalt **deleteMessage** direct nadat het bericht is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="d6b62-162">Your code calls **deleteMessage** right after the message has been processed.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve the first visible message in the queue.
    CloudQueueMessage retrievedMessage = queue.retrieveMessage();

    if (retrievedMessage != null)
    {
        // Process the message in less than 30 seconds, and then delete the message.
        queue.deleteMessage(retrievedMessage);
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="additional-options-for-dequeuing-messages"></a><span data-ttu-id="d6b62-163">Aanvullende opties voor berichten waarbij</span><span class="sxs-lookup"><span data-stu-id="d6b62-163">Additional options for dequeuing messages</span></span>
<span data-ttu-id="d6b62-164">Er zijn twee manieren waarop u het ophalen van berichten uit een wachtrij kunt aanpassen.</span><span class="sxs-lookup"><span data-stu-id="d6b62-164">There are two ways you can customize message retrieval from a queue.</span></span> <span data-ttu-id="d6b62-165">Ten eerste kunt u berichten batchgewijs (maximaal 32) ophalen.</span><span class="sxs-lookup"><span data-stu-id="d6b62-165">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="d6b62-166">Ten tweede kunt u een langere of kortere time-out voor onzichtbaarheid instellen, zodat uw code meer of minder tijd krijgt voor het volledig verwerken van elk bericht.</span><span class="sxs-lookup"><span data-stu-id="d6b62-166">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span>

<span data-ttu-id="d6b62-167">Het volgende codevoorbeeld wordt de **retrieveMessages** methode om 20 berichten in één aanroep.</span><span class="sxs-lookup"><span data-stu-id="d6b62-167">The following code example uses the **retrieveMessages** method to get 20 messages in one call.</span></span> <span data-ttu-id="d6b62-168">Vervolgens wordt verwerkt elke bericht met een **voor** lus.</span><span class="sxs-lookup"><span data-stu-id="d6b62-168">Then it processes each message using a **for** loop.</span></span> <span data-ttu-id="d6b62-169">De time-out voor onzichtbaarheid wordt ingesteld op vijf minuten (300 seconden) voor elk bericht.</span><span class="sxs-lookup"><span data-stu-id="d6b62-169">It also sets the invisibility timeout to five minutes (300 seconds) for each message.</span></span> <span data-ttu-id="d6b62-170">Denk eraan dat de vijf minuten wordt gestart voor alle berichten op hetzelfde moment, dus wanneer vijf minuten verstreken sinds de aanroep van **retrieveMessages**, alle berichten die niet zijn verwijderd weer zichtbaar worden.</span><span class="sxs-lookup"><span data-stu-id="d6b62-170">Note that the five minutes starts for all messages at the same time, so when five minutes have passed since the call to **retrieveMessages**, any messages which have not been deleted will become visible again.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve 20 messages from the queue with a visibility timeout of 300 seconds.
    for (CloudQueueMessage message : queue.retrieveMessages(20, 300, null, null)) {
        // Do processing for all messages in less than 5 minutes,
        // deleting each message after processing.
        queue.deleteMessage(message);
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-list-the-queues"></a><span data-ttu-id="d6b62-171">Procedure: de wachtrijen lijst</span><span class="sxs-lookup"><span data-stu-id="d6b62-171">How to: List the queues</span></span>
<span data-ttu-id="d6b62-172">Aanroepen voor een lijst van de huidige wachtrijen, de **CloudQueueClient.listQueues()** methode een verzameling van retourneert **CloudQueue** objecten.</span><span class="sxs-lookup"><span data-stu-id="d6b62-172">To obtain a list of the current queues, call the **CloudQueueClient.listQueues()** method, which will return a collection of **CloudQueue** objects.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient =
        storageAccount.createCloudQueueClient();

    // Loop through the collection of queues.
    for (CloudQueue queue : queueClient.listQueues())
    {
        // Output each queue name.
        System.out.println(queue.getName());
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="d6b62-173">Procedure: een wachtrij verwijderen</span><span class="sxs-lookup"><span data-stu-id="d6b62-173">How to: Delete a queue</span></span>
<span data-ttu-id="d6b62-174">Aanroepen voor het verwijderen van een wachtrij en alle berichten hierin de **deleteIfExists** methode op de **CloudQueue** object.</span><span class="sxs-lookup"><span data-stu-id="d6b62-174">To delete a queue and all the messages contained in it, call the **deleteIfExists** method on the **CloudQueue** object.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Delete the queue if it exists.
    queue.deleteIfExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="next-steps"></a><span data-ttu-id="d6b62-175">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d6b62-175">Next steps</span></span>
<span data-ttu-id="d6b62-176">Nu dat u de basisprincipes van queue storage hebt geleerd, volgt u deze koppelingen voor meer informatie over complexere opslagtaken.</span><span class="sxs-lookup"><span data-stu-id="d6b62-176">Now that you've learned the basics of queue storage, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="d6b62-177">[Azure-opslag-SDK voor Java][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="d6b62-177">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="d6b62-178">[naslaginformatie over Azure Storage Client SDK][naslaginformatie over Azure Storage Client SDK]</span><span class="sxs-lookup"><span data-stu-id="d6b62-178">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="d6b62-179">[REST-API van Azure Storage-Services][Azure Storage Services REST API]</span><span class="sxs-lookup"><span data-stu-id="d6b62-179">[Azure Storage Services REST API][Azure Storage Services REST API]</span></span>
* <span data-ttu-id="d6b62-180">[Azure Storage-teamblog][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="d6b62-180">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
<span data-ttu-id="d6b62-181">[naslaginformatie over Azure Storage Client SDK]: http://dl.windowsazure.com/storage/javadoc/</span><span class="sxs-lookup"><span data-stu-id="d6b62-181">[Azure Storage Client SDK Reference]: http://dl.windowsazure.com/storage/javadoc/</span></span>
[Azure Storage Services REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
