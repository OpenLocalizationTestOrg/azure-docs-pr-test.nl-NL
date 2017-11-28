---
title: aaaHow toouse Queue storage met Java | Microsoft Docs
description: Ontdek hoe toocreate toouse hello Azure Queue-service en delete-wachtrijen en invoegen, ophalen en verwijderen van berichten. Voorbeelden die zijn geschreven in Java.
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
ms.openlocfilehash: c2d5211ec5b6454f7dbc126aad4ba9950df13661
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-java"></a><span data-ttu-id="353cb-104">Hoe toouse Queue storage met Java</span><span class="sxs-lookup"><span data-stu-id="353cb-104">How toouse Queue storage from Java</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a><span data-ttu-id="353cb-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="353cb-105">Overview</span></span>
<span data-ttu-id="353cb-106">Deze handleiding leert u hoe tooperform algemene scenario's met behulp van hello Azure Queue storage-service.</span><span class="sxs-lookup"><span data-stu-id="353cb-106">This guide will show you how tooperform common scenarios using hello Azure Queue storage service.</span></span> <span data-ttu-id="353cb-107">Hallo-voorbeelden zijn geschreven in Java en gebruiken van Hallo [Azure-opslag-SDK voor Java][Azure Storage SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="353cb-107">hello samples are written in Java and use hello [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="353cb-108">Hallo scenario's worden behandeld: **invoegen**, **inspecteren**, **ophalen**, en **verwijderen** wachtrij berichten, evenals  **maken van** en **verwijderen** wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="353cb-108">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating** and **deleting** queues.</span></span> <span data-ttu-id="353cb-109">Zie voor meer informatie over wachtrijen Hallo [Vervolgstappen](#Next-Steps) sectie.</span><span class="sxs-lookup"><span data-stu-id="353cb-109">For more information on queues, see hello [Next steps](#Next-Steps) section.</span></span>

<span data-ttu-id="353cb-110">Opmerking: Een SDK is beschikbaar voor ontwikkelaars die werken met Azure Storage op Android-apparaten.</span><span class="sxs-lookup"><span data-stu-id="353cb-110">Note: An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="353cb-111">Zie voor meer informatie, Hallo [Azure-opslag-SDK voor Android][Azure Storage SDK for Android].</span><span class="sxs-lookup"><span data-stu-id="353cb-111">For more information, see hello [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="353cb-112">Een Java-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="353cb-112">Create a Java application</span></span>
<span data-ttu-id="353cb-113">In deze handleiding gebruikt u opslagfuncties die kunnen worden uitgevoerd binnen een Java-toepassing lokaal of in de code die wordt uitgevoerd binnen een Webrol of worker-rol in Azure.</span><span class="sxs-lookup"><span data-stu-id="353cb-113">In this guide, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="353cb-114">toodo geval is, moet u tooinstall Hallo Java Development Kit (JDK) en een Azure storage-account maken in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="353cb-114">toodo so, you will need tooinstall hello Java Development Kit (JDK) and create an Azure storage account in your Azure subscription.</span></span> <span data-ttu-id="353cb-115">Nadat u dit hebt gedaan, moet u tooverify dat uw ontwikkelsysteem voldoet aan de minimumvereisten Hallo en afhankelijkheden die worden vermeld in Hallo [Azure-opslag-SDK voor Java] [ Azure Storage SDK for Java] opslagplaats op GitHub.</span><span class="sxs-lookup"><span data-stu-id="353cb-115">Once you have done so, you will need tooverify that your development system meets hello minimum requirements and dependencies which are listed in hello [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="353cb-116">Als uw systeem aan deze vereisten voldoet, kunt u de instructies voor het downloaden en installeren van hello Azure Storage-bibliotheken voor Java op uw systeem vanuit die opslagplaats Hallo volgen.</span><span class="sxs-lookup"><span data-stu-id="353cb-116">If your system meets those requirements, you can follow hello instructions for downloading and installing hello Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="353cb-117">Nadat u deze taken hebt voltooid, kunt u zich kunt toocreate een Java-toepassing die gebruikmaakt van Hallo voorbeelden in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="353cb-117">Once you have completed those tasks, you will be able toocreate a Java application which uses hello examples in this article.</span></span>

## <a name="configure-your-application-tooaccess-queue-storage"></a><span data-ttu-id="353cb-118">Uw toepassing tooaccess wachtrij opslag configureren</span><span class="sxs-lookup"><span data-stu-id="353cb-118">Configure your application tooaccess queue storage</span></span>
<span data-ttu-id="353cb-119">Hallo importeren instructies toohello bovenaan Hallo Java bestand waar u toouse Azure storage-API's tooaccess wachtrijen volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="353cb-119">Add hello following import statements toohello top of hello Java file where you want toouse Azure storage APIs tooaccess queues:</span></span>

```java
// Include hello following imports toouse queue APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.queue.*;
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="353cb-120">Een Azure-opslag-verbindingsreeks instellen</span><span class="sxs-lookup"><span data-stu-id="353cb-120">Setup an Azure storage connection string</span></span>
<span data-ttu-id="353cb-121">Een Azure-opslag-client maakt gebruik van een storage connection string toostore eindpunten en referenties voor toegang tot gegevens beheerservices.</span><span class="sxs-lookup"><span data-stu-id="353cb-121">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="353cb-122">Wanneer een client-toepassing wordt uitgevoerd, moet u bieden Hallo verbindingsreeks voor opslag in Hallo indeling te volgen, met behulp van Hallo-naam van uw opslagaccount en primaire toegangssleutel voor opslagaccount Hallo die worden vermeld in Hallo Hallo [Azure Portal](https://portal.azure.com)voor Hallo *AccountName* en *AccountKey* waarden.</span><span class="sxs-lookup"><span data-stu-id="353cb-122">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello Primary access key for hello storage account listed in hello [Azure Portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="353cb-123">Dit voorbeeld ziet hoe u een statisch veld toohold Hallo-verbindingsreeks kunt declareren:</span><span class="sxs-lookup"><span data-stu-id="353cb-123">This example shows how you can declare a static field toohold hello connection string:</span></span>

```java
// Define hello connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="353cb-124">In een toepassing in een rol in Microsoft Azure wordt uitgevoerd, kan deze tekenreeks worden opgeslagen in Hallo serviceconfiguratiebestand, *ServiceConfiguration.cscfg*, en kunnen worden geopend met een aanroep van toohello  **RoleEnvironment.getConfigurationSettings** methode.</span><span class="sxs-lookup"><span data-stu-id="353cb-124">In an application running within a role in Microsoft Azure, this string can be stored in hello service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call toohello **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="353cb-125">Hier volgt een voorbeeld van het ophalen van Hallo-verbindingsreeks uit een **instelling** element met de naam *StorageConnectionString* in Hallo serviceconfiguratiebestand:</span><span class="sxs-lookup"><span data-stu-id="353cb-125">Here's an example of getting hello connection string from a **Setting** element named *StorageConnectionString* in hello service configuration file:</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="353cb-126">Hallo volgende voorbeelden wordt ervan uitgegaan dat u een van deze twee methoden tooget Hallo-opslagverbindingsreeks hebt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="353cb-126">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="353cb-127">Procedure: een wachtrij maken</span><span class="sxs-lookup"><span data-stu-id="353cb-127">How to: Create a queue</span></span>
<span data-ttu-id="353cb-128">Een **CloudQueueClient** object kunt u profiteren van reference-objecten voor wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="353cb-128">A **CloudQueueClient** object lets you get reference objects for queues.</span></span> <span data-ttu-id="353cb-129">Hallo volgende code maakt een **CloudQueueClient** object.</span><span class="sxs-lookup"><span data-stu-id="353cb-129">hello following code creates a **CloudQueueClient** object.</span></span> <span data-ttu-id="353cb-130">(Opmerking: Er zijn extra manieren toocreate **CloudStorageAccount** objecten; voor meer informatie Zie **CloudStorageAccount** in Hallo [Azure Storage Client SDK-naslaginformatie].)</span><span class="sxs-lookup"><span data-stu-id="353cb-130">(Note: There are additional ways toocreate **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in hello [Azure Storage Client SDK Reference].)</span></span>

<span data-ttu-id="353cb-131">Gebruik Hallo **CloudQueueClient** tooget een verwijzing toohello wachtrij die u wilt dat toouse object.</span><span class="sxs-lookup"><span data-stu-id="353cb-131">Use hello **CloudQueueClient** object tooget a reference toohello queue you want toouse.</span></span> <span data-ttu-id="353cb-132">U kunt Hallo wachtrij maken als deze niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="353cb-132">You can create hello queue if it doesn't exist.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

   // Create hello queue client.
   CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

   // Retrieve a reference tooa queue.
   CloudQueue queue = queueClient.getQueueReference("myqueue");

   // Create hello queue if it doesn't already exist.
   queue.createIfNotExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-add-a-message-tooa-queue"></a><span data-ttu-id="353cb-133">Procedure: een berichtenwachtrij tooa toevoegen</span><span class="sxs-lookup"><span data-stu-id="353cb-133">How to: Add a message tooa queue</span></span>
<span data-ttu-id="353cb-134">een bericht in een bestaande wachtrij tooinsert eerst maakt u een nieuwe **CloudQueueMessage**.</span><span class="sxs-lookup"><span data-stu-id="353cb-134">tooinsert a message into an existing queue, first create a new **CloudQueueMessage**.</span></span> <span data-ttu-id="353cb-135">Daarna roept Hallo **addMessage** methode.</span><span class="sxs-lookup"><span data-stu-id="353cb-135">Next, call hello **addMessage** method.</span></span> <span data-ttu-id="353cb-136">Een **CloudQueueMessage** kan worden gemaakt vanuit een tekenreeks (in UTF-8-indeling) of een byte-matrix.</span><span class="sxs-lookup"><span data-stu-id="353cb-136">A **CloudQueueMessage** can be created from either a string (in UTF-8 format) or a byte array.</span></span> <span data-ttu-id="353cb-137">Hier volgt de code die een wachtrij maakt (als deze niet bestaat) en voegt het Hallo-bericht "Hallo, wereld".</span><span class="sxs-lookup"><span data-stu-id="353cb-137">Here is code which creates a queue (if it doesn't exist) and inserts hello message "Hello, World".</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Create hello queue if it doesn't already exist.
    queue.createIfNotExists();

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    queue.addMessage(message);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="353cb-138">Hoe: bekijken van volgende Hallo-bericht</span><span class="sxs-lookup"><span data-stu-id="353cb-138">How to: Peek at hello next message</span></span>
<span data-ttu-id="353cb-139">U kunt bekijken van Hallo-bericht in Hallo begin van een wachtrij zonder het te verwijderen uit de wachtrij Hallo door aan te roepen **peekMessage**.</span><span class="sxs-lookup"><span data-stu-id="353cb-139">You can peek at hello message in hello front of a queue without removing it from hello queue by calling **peekMessage**.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Peek at hello next message.
    CloudQueueMessage peekedMessage = queue.peekMessage();

    // Output hello message value.
    if (peekedMessage != null)
    {
      System.out.println(peekedMessage.getMessageContentAsString());
   }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="353cb-140">Hoe: Hallo inhoud van een bericht in de wachtrij wijzigen</span><span class="sxs-lookup"><span data-stu-id="353cb-140">How to: Change hello contents of a queued message</span></span>
<span data-ttu-id="353cb-141">U kunt Hallo inhoud van een bericht in-place in Hallo wachtrij wijzigen.</span><span class="sxs-lookup"><span data-stu-id="353cb-141">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="353cb-142">Als het Hallo-bericht een werktaak vertegenwoordigt, kunt u deze functie tooupdate Hallo status van de werktaak hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="353cb-142">If hello message represents a work task, you could use this feature tooupdate hello status of hello work task.</span></span> <span data-ttu-id="353cb-143">Hallo na code Hallo-bericht van wachtrij bijgewerkt met nieuwe inhoud en sets Hallo zichtbaarheid time-out tooextend 60 seconden.</span><span class="sxs-lookup"><span data-stu-id="353cb-143">hello following code updates hello queue message with new contents, and sets hello visibility timeout tooextend another 60 seconds.</span></span> <span data-ttu-id="353cb-144">Hallo-status van de werkitems die zijn gekoppeld aan het Hallo-bericht opgeslagen, en geeft Hallo-client een andere minuut toocontinue werkt op het Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="353cb-144">This saves hello state of work associated with hello message, and gives hello client another minute toocontinue working on hello message.</span></span> <span data-ttu-id="353cb-145">U kunt deze techniek tootrack meerdere stappen bestaande werkstromen op Wachtrijberichten, zonder toostart via van Hallo begin als een verwerkingsstap vanwege problemen met toohardware of software.</span><span class="sxs-lookup"><span data-stu-id="353cb-145">You could use this technique tootrack multi-step workflows on queue messages, without having toostart over from hello beginning if a processing step fails due toohardware or software failure.</span></span> <span data-ttu-id="353cb-146">Doorgaans houdt u ook een aantal voor nieuwe pogingen en als hello bericht opnieuw wordt geprobeerd meer dan  *n*  tijdstippen, verwijdert u het.</span><span class="sxs-lookup"><span data-stu-id="353cb-146">Typically, you would keep a retry count as well, and if hello message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="353cb-147">Dit biedt bescherming tegen berichten die een toepassingsfout activeren telkens wanneer ze worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="353cb-147">This protects against a message that triggers an application error each time it is processed.</span></span>

<span data-ttu-id="353cb-148">Hallo volgende code voorbeeld doorzoekt Hallo wachtrij met berichten, zoekt de eerste Hallo-bericht die overeenkomt met "Hallo, wereld" voor Hallo inhoud, en vervolgens het Hallo-bericht inhoud wordt gewijzigd en wordt afgesloten.</span><span class="sxs-lookup"><span data-stu-id="353cb-148">hello following code sample searches through hello queue of messages, locates hello first message that matches "Hello, World" for hello content, then modifies hello message content and exits.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // hello maximum number of messages that can be retrieved is 32.
    final int MAX_NUMBER_OF_MESSAGES_TO_PEEK = 32;

    // Loop through hello messages in hello queue.
    for (CloudQueueMessage message : queue.retrieveMessages(MAX_NUMBER_OF_MESSAGES_TO_PEEK,1,null,null))
    {
        // Check for a specific string.
        if (message.getMessageContentAsString().equals("Hello, World"))
        {
            // Modify hello content of hello first matching message.
            message.setMessageContent("Updated contents.");
            // Set it toobe visible in 30 seconds.
            EnumSet<MessageUpdateFields> updateFields =
                EnumSet.of(MessageUpdateFields.CONTENT,
                MessageUpdateFields.VISIBILITY);
            // Update hello message.
            queue.updateMessage(message, 30, updateFields, null, null);
            break;
        }
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

<span data-ttu-id="353cb-149">U kunt ook updates hello codevoorbeeld alleen eerste zichtbaar welkomstbericht op Hallo wachtrij.</span><span class="sxs-lookup"><span data-stu-id="353cb-149">Alternatively, hello following code sample updates just hello first visible message on hello queue.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve hello first visible message in hello queue.
    CloudQueueMessage message = queue.retrieveMessage();

    if (message != null)
    {
        // Modify hello message content.
        message.setMessageContent("Updated contents.");
        // Set it toobe visible in 60 seconds.
        EnumSet<MessageUpdateFields> updateFields =
            EnumSet.of(MessageUpdateFields.CONTENT,
            MessageUpdateFields.VISIBILITY);
        // Update hello message.
        queue.updateMessage(message, 60, updateFields, null, null);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="353cb-150">Hoe: Hallo wachtrijlengte ophalen</span><span class="sxs-lookup"><span data-stu-id="353cb-150">How to: Get hello queue length</span></span>
<span data-ttu-id="353cb-151">U kunt een schatting maken van het aantal berichten Hallo krijgen in een wachtrij.</span><span class="sxs-lookup"><span data-stu-id="353cb-151">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="353cb-152">Hallo **downloadAttributes** methode vraagt Hallo Queue-service voor verschillende huidige waarden, met inbegrip van een telling van het aantal berichten in een wachtrij zijn.</span><span class="sxs-lookup"><span data-stu-id="353cb-152">hello **downloadAttributes** method asks hello Queue service for several current values, including a count of how many messages are in a queue.</span></span> <span data-ttu-id="353cb-153">Hallo aantal is alleen een benadering omdat berichten kunnen worden toegevoegd of verwijderd nadat de Hallo Queue-service reageert tooyour aanvraag.</span><span class="sxs-lookup"><span data-stu-id="353cb-153">hello count is only approximate because messages can be added or removed after hello Queue service responds tooyour request.</span></span> <span data-ttu-id="353cb-154">Hallo **getApproximateMessageCount** methode retourneert de laatste waarde Hallo opgehaald door Hallo aanroep te**downloadAttributes**, zonder Hallo Queue-service aanroepen.</span><span class="sxs-lookup"><span data-stu-id="353cb-154">hello **getApproximateMessageCount** method returns hello last value retrieved by hello call too**downloadAttributes**, without calling hello Queue service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

   // Download hello approximate message count from hello server.
    queue.downloadAttributes();

    // Retrieve hello newly cached approximate message count.
    long cachedMessageCount = queue.getApproximateMessageCount();

    // Display hello queue length.
    System.out.println(String.format("Queue length: %d", cachedMessageCount));
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-dequeue-hello-next-message"></a><span data-ttu-id="353cb-155">Procedure: het volgende Hallo-bericht in wachtrij</span><span class="sxs-lookup"><span data-stu-id="353cb-155">How to: Dequeue hello next message</span></span>
<span data-ttu-id="353cb-156">Uw code dequeues een bericht van een wachtrij in twee stappen.</span><span class="sxs-lookup"><span data-stu-id="353cb-156">Your code dequeues a message from a queue in two steps.</span></span> <span data-ttu-id="353cb-157">Als u aanroept **retrieveMessage**, krijgt u het volgende Hallo-bericht in een wachtrij.</span><span class="sxs-lookup"><span data-stu-id="353cb-157">When you call **retrieveMessage**, you get hello next message in a queue.</span></span> <span data-ttu-id="353cb-158">Een bericht dat wordt geretourneerd door **retrieveMessage** wordt onzichtbaar tooany andere codes die berichten lezen uit deze wachtrij.</span><span class="sxs-lookup"><span data-stu-id="353cb-158">A message returned from **retrieveMessage** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="353cb-159">Standaard blijft het bericht onzichtbaar gedurende 30 seconden.</span><span class="sxs-lookup"><span data-stu-id="353cb-159">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="353cb-160">toofinish verwijderen Hallo-bericht uit de wachtrij hello, moet u ook aanroepen **deleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="353cb-160">toofinish removing hello message from hello queue, you must also call **deleteMessage**.</span></span> <span data-ttu-id="353cb-161">Dit proces in twee stappen van het verwijderen van een bericht zorgt ervoor dat als uw code mislukt tooprocess een bericht vanwege problemen toohardware of software, een ander exemplaar van uw code krijgt hetzelfde bericht Hallo en probeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="353cb-161">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="353cb-162">Uw code haalt **deleteMessage** direct nadat het Hallo-bericht is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="353cb-162">Your code calls **deleteMessage** right after hello message has been processed.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve hello first visible message in hello queue.
    CloudQueueMessage retrievedMessage = queue.retrieveMessage();

    if (retrievedMessage != null)
    {
        // Process hello message in less than 30 seconds, and then delete hello message.
        queue.deleteMessage(retrievedMessage);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="additional-options-for-dequeuing-messages"></a><span data-ttu-id="353cb-163">Aanvullende opties voor berichten waarbij</span><span class="sxs-lookup"><span data-stu-id="353cb-163">Additional options for dequeuing messages</span></span>
<span data-ttu-id="353cb-164">Er zijn twee manieren waarop u het ophalen van berichten uit een wachtrij kunt aanpassen.</span><span class="sxs-lookup"><span data-stu-id="353cb-164">There are two ways you can customize message retrieval from a queue.</span></span> <span data-ttu-id="353cb-165">U krijgt eerst een batch met berichten (omhoog too32).</span><span class="sxs-lookup"><span data-stu-id="353cb-165">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="353cb-166">Ten tweede kunt u instellen een time-out voor onzichtbaarheid langer of korter, zodat uw code meer of minder tijd toofully elk bericht niet verwerken.</span><span class="sxs-lookup"><span data-stu-id="353cb-166">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span>

<span data-ttu-id="353cb-167">Hallo volgende codevoorbeeld maakt gebruik van Hallo **retrieveMessages** methode tooget 20 berichten in één aanroep.</span><span class="sxs-lookup"><span data-stu-id="353cb-167">hello following code example uses hello **retrieveMessages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="353cb-168">Vervolgens wordt verwerkt elke bericht met een **voor** lus.</span><span class="sxs-lookup"><span data-stu-id="353cb-168">Then it processes each message using a **for** loop.</span></span> <span data-ttu-id="353cb-169">Hallo onzichtbaarheid time-out toofive minuten (300 seconden) voor elk bericht wordt ook ingesteld.</span><span class="sxs-lookup"><span data-stu-id="353cb-169">It also sets hello invisibility timeout toofive minutes (300 seconds) for each message.</span></span> <span data-ttu-id="353cb-170">Opmerking die Hallo vijf minuten wordt gestart voor alle berichten op Hallo dezelfde tijd, dus als u vijf minuten zijn verstreken sinds de aanroep hello te**retrieveMessages**, alle berichten die niet zijn verwijderd weer zichtbaar worden.</span><span class="sxs-lookup"><span data-stu-id="353cb-170">Note that hello five minutes starts for all messages at hello same time, so when five minutes have passed since hello call too**retrieveMessages**, any messages which have not been deleted will become visible again.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve 20 messages from hello queue with a visibility timeout of 300 seconds.
    for (CloudQueueMessage message : queue.retrieveMessages(20, 300, null, null)) {
        // Do processing for all messages in less than 5 minutes,
        // deleting each message after processing.
        queue.deleteMessage(message);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-list-hello-queues"></a><span data-ttu-id="353cb-171">Procedure: lijst Hallo wachtrijen</span><span class="sxs-lookup"><span data-stu-id="353cb-171">How to: List hello queues</span></span>
<span data-ttu-id="353cb-172">een lijst met Hallo huidige wachtrijen aanroep Hallo tooobtain **CloudQueueClient.listQueues()** methode een verzameling van retourneert **CloudQueue** objecten.</span><span class="sxs-lookup"><span data-stu-id="353cb-172">tooobtain a list of hello current queues, call hello **CloudQueueClient.listQueues()** method, which will return a collection of **CloudQueue** objects.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient =
        storageAccount.createCloudQueueClient();

    // Loop through hello collection of queues.
    for (CloudQueue queue : queueClient.listQueues())
    {
        // Output each queue name.
        System.out.println(queue.getName());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="353cb-173">Procedure: een wachtrij verwijderen</span><span class="sxs-lookup"><span data-stu-id="353cb-173">How to: Delete a queue</span></span>
<span data-ttu-id="353cb-174">een wachtrij en alle Hallo-berichten toodelete opgenomen in deze aanroep Hallo **deleteIfExists** methode op Hallo **CloudQueue** object.</span><span class="sxs-lookup"><span data-stu-id="353cb-174">toodelete a queue and all hello messages contained in it, call hello **deleteIfExists** method on hello **CloudQueue** object.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Delete hello queue if it exists.
    queue.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="next-steps"></a><span data-ttu-id="353cb-175">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="353cb-175">Next steps</span></span>
<span data-ttu-id="353cb-176">Nu u Hallo basisprincipes van queue storage hebt geleerd, volgt u deze koppelingen toolearn over complexere opslagtaken.</span><span class="sxs-lookup"><span data-stu-id="353cb-176">Now that you've learned hello basics of queue storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="353cb-177">[Azure-opslag-SDK voor Java][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="353cb-177">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="353cb-178">[Azure Storage Client SDK-naslaginformatie][Azure Storage Client SDK-naslaginformatie]</span><span class="sxs-lookup"><span data-stu-id="353cb-178">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="353cb-179">[REST-API van Azure Storage-Services][Azure Storage Services REST API]</span><span class="sxs-lookup"><span data-stu-id="353cb-179">[Azure Storage Services REST API][Azure Storage Services REST API]</span></span>
* <span data-ttu-id="353cb-180">[Azure Storage-teamblog][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="353cb-180">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[Azure Storage Client SDK-naslaginformatie]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage Services REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
