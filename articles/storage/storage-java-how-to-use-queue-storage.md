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
# <a name="how-toouse-queue-storage-from-java"></a>Hoe toouse Queue storage met Java
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a>Overzicht
Deze handleiding leert u hoe tooperform algemene scenario's met behulp van hello Azure Queue storage-service. Hallo-voorbeelden zijn geschreven in Java en gebruiken van Hallo [Azure-opslag-SDK voor Java][Azure Storage SDK for Java]. Hallo scenario's worden behandeld: **invoegen**, **inspecteren**, **ophalen**, en **verwijderen** wachtrij berichten, evenals  **maken van** en **verwijderen** wachtrijen. Zie voor meer informatie over wachtrijen Hallo [Vervolgstappen](#Next-Steps) sectie.

Opmerking: Een SDK is beschikbaar voor ontwikkelaars die werken met Azure Storage op Android-apparaten. Zie voor meer informatie, Hallo [Azure-opslag-SDK voor Android][Azure Storage SDK for Android].

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a>Een Java-toepassing maken
In deze handleiding gebruikt u opslagfuncties die kunnen worden uitgevoerd binnen een Java-toepassing lokaal of in de code die wordt uitgevoerd binnen een Webrol of worker-rol in Azure.

toodo geval is, moet u tooinstall Hallo Java Development Kit (JDK) en een Azure storage-account maken in uw Azure-abonnement. Nadat u dit hebt gedaan, moet u tooverify dat uw ontwikkelsysteem voldoet aan de minimumvereisten Hallo en afhankelijkheden die worden vermeld in Hallo [Azure-opslag-SDK voor Java] [ Azure Storage SDK for Java] opslagplaats op GitHub. Als uw systeem aan deze vereisten voldoet, kunt u de instructies voor het downloaden en installeren van hello Azure Storage-bibliotheken voor Java op uw systeem vanuit die opslagplaats Hallo volgen. Nadat u deze taken hebt voltooid, kunt u zich kunt toocreate een Java-toepassing die gebruikmaakt van Hallo voorbeelden in dit artikel.

## <a name="configure-your-application-tooaccess-queue-storage"></a>Uw toepassing tooaccess wachtrij opslag configureren
Hallo importeren instructies toohello bovenaan Hallo Java bestand waar u toouse Azure storage-API's tooaccess wachtrijen volgende toevoegen:

```java
// Include hello following imports toouse queue APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.queue.*;
```

## <a name="setup-an-azure-storage-connection-string"></a>Een Azure-opslag-verbindingsreeks instellen
Een Azure-opslag-client maakt gebruik van een storage connection string toostore eindpunten en referenties voor toegang tot gegevens beheerservices. Wanneer een client-toepassing wordt uitgevoerd, moet u bieden Hallo verbindingsreeks voor opslag in Hallo indeling te volgen, met behulp van Hallo-naam van uw opslagaccount en primaire toegangssleutel voor opslagaccount Hallo die worden vermeld in Hallo Hallo [Azure Portal](https://portal.azure.com)voor Hallo *AccountName* en *AccountKey* waarden. Dit voorbeeld ziet hoe u een statisch veld toohold Hallo-verbindingsreeks kunt declareren:

```java
// Define hello connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

In een toepassing in een rol in Microsoft Azure wordt uitgevoerd, kan deze tekenreeks worden opgeslagen in Hallo serviceconfiguratiebestand, *ServiceConfiguration.cscfg*, en kunnen worden geopend met een aanroep van toohello  **RoleEnvironment.getConfigurationSettings** methode. Hier volgt een voorbeeld van het ophalen van Hallo-verbindingsreeks uit een **instelling** element met de naam *StorageConnectionString* in Hallo serviceconfiguratiebestand:

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

Hallo volgende voorbeelden wordt ervan uitgegaan dat u een van deze twee methoden tooget Hallo-opslagverbindingsreeks hebt gebruikt.

## <a name="how-to-create-a-queue"></a>Procedure: een wachtrij maken
Een **CloudQueueClient** object kunt u profiteren van reference-objecten voor wachtrijen. Hallo volgende code maakt een **CloudQueueClient** object. (Opmerking: Er zijn extra manieren toocreate **CloudStorageAccount** objecten; voor meer informatie Zie **CloudStorageAccount** in Hallo [Azure Storage Client SDK-naslaginformatie].)

Gebruik Hallo **CloudQueueClient** tooget een verwijzing toohello wachtrij die u wilt dat toouse object. U kunt Hallo wachtrij maken als deze niet bestaat.

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

## <a name="how-to-add-a-message-tooa-queue"></a>Procedure: een berichtenwachtrij tooa toevoegen
een bericht in een bestaande wachtrij tooinsert eerst maakt u een nieuwe **CloudQueueMessage**. Daarna roept Hallo **addMessage** methode. Een **CloudQueueMessage** kan worden gemaakt vanuit een tekenreeks (in UTF-8-indeling) of een byte-matrix. Hier volgt de code die een wachtrij maakt (als deze niet bestaat) en voegt het Hallo-bericht "Hallo, wereld".

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

## <a name="how-to-peek-at-hello-next-message"></a>Hoe: bekijken van volgende Hallo-bericht
U kunt bekijken van Hallo-bericht in Hallo begin van een wachtrij zonder het te verwijderen uit de wachtrij Hallo door aan te roepen **peekMessage**.

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

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>Hoe: Hallo inhoud van een bericht in de wachtrij wijzigen
U kunt Hallo inhoud van een bericht in-place in Hallo wachtrij wijzigen. Als het Hallo-bericht een werktaak vertegenwoordigt, kunt u deze functie tooupdate Hallo status van de werktaak hello gebruiken. Hallo na code Hallo-bericht van wachtrij bijgewerkt met nieuwe inhoud en sets Hallo zichtbaarheid time-out tooextend 60 seconden. Hallo-status van de werkitems die zijn gekoppeld aan het Hallo-bericht opgeslagen, en geeft Hallo-client een andere minuut toocontinue werkt op het Hallo-bericht. U kunt deze techniek tootrack meerdere stappen bestaande werkstromen op Wachtrijberichten, zonder toostart via van Hallo begin als een verwerkingsstap vanwege problemen met toohardware of software. Doorgaans houdt u ook een aantal voor nieuwe pogingen en als hello bericht opnieuw wordt geprobeerd meer dan  *n*  tijdstippen, verwijdert u het. Dit biedt bescherming tegen berichten die een toepassingsfout activeren telkens wanneer ze worden verwerkt.

Hallo volgende code voorbeeld doorzoekt Hallo wachtrij met berichten, zoekt de eerste Hallo-bericht die overeenkomt met "Hallo, wereld" voor Hallo inhoud, en vervolgens het Hallo-bericht inhoud wordt gewijzigd en wordt afgesloten.

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

U kunt ook updates hello codevoorbeeld alleen eerste zichtbaar welkomstbericht op Hallo wachtrij.

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

## <a name="how-to-get-hello-queue-length"></a>Hoe: Hallo wachtrijlengte ophalen
U kunt een schatting maken van het aantal berichten Hallo krijgen in een wachtrij. Hallo **downloadAttributes** methode vraagt Hallo Queue-service voor verschillende huidige waarden, met inbegrip van een telling van het aantal berichten in een wachtrij zijn. Hallo aantal is alleen een benadering omdat berichten kunnen worden toegevoegd of verwijderd nadat de Hallo Queue-service reageert tooyour aanvraag. Hallo **getApproximateMessageCount** methode retourneert de laatste waarde Hallo opgehaald door Hallo aanroep te**downloadAttributes**, zonder Hallo Queue-service aanroepen.

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

## <a name="how-to-dequeue-hello-next-message"></a>Procedure: het volgende Hallo-bericht in wachtrij
Uw code dequeues een bericht van een wachtrij in twee stappen. Als u aanroept **retrieveMessage**, krijgt u het volgende Hallo-bericht in een wachtrij. Een bericht dat wordt geretourneerd door **retrieveMessage** wordt onzichtbaar tooany andere codes die berichten lezen uit deze wachtrij. Standaard blijft het bericht onzichtbaar gedurende 30 seconden. toofinish verwijderen Hallo-bericht uit de wachtrij hello, moet u ook aanroepen **deleteMessage**. Dit proces in twee stappen van het verwijderen van een bericht zorgt ervoor dat als uw code mislukt tooprocess een bericht vanwege problemen toohardware of software, een ander exemplaar van uw code krijgt hetzelfde bericht Hallo en probeer het opnieuw. Uw code haalt **deleteMessage** direct nadat het Hallo-bericht is verwerkt.

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

## <a name="additional-options-for-dequeuing-messages"></a>Aanvullende opties voor berichten waarbij
Er zijn twee manieren waarop u het ophalen van berichten uit een wachtrij kunt aanpassen. U krijgt eerst een batch met berichten (omhoog too32). Ten tweede kunt u instellen een time-out voor onzichtbaarheid langer of korter, zodat uw code meer of minder tijd toofully elk bericht niet verwerken.

Hallo volgende codevoorbeeld maakt gebruik van Hallo **retrieveMessages** methode tooget 20 berichten in één aanroep. Vervolgens wordt verwerkt elke bericht met een **voor** lus. Hallo onzichtbaarheid time-out toofive minuten (300 seconden) voor elk bericht wordt ook ingesteld. Opmerking die Hallo vijf minuten wordt gestart voor alle berichten op Hallo dezelfde tijd, dus als u vijf minuten zijn verstreken sinds de aanroep hello te**retrieveMessages**, alle berichten die niet zijn verwijderd weer zichtbaar worden.

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

## <a name="how-to-list-hello-queues"></a>Procedure: lijst Hallo wachtrijen
een lijst met Hallo huidige wachtrijen aanroep Hallo tooobtain **CloudQueueClient.listQueues()** methode een verzameling van retourneert **CloudQueue** objecten.

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

## <a name="how-to-delete-a-queue"></a>Procedure: een wachtrij verwijderen
een wachtrij en alle Hallo-berichten toodelete opgenomen in deze aanroep Hallo **deleteIfExists** methode op Hallo **CloudQueue** object.

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

## <a name="next-steps"></a>Volgende stappen
Nu u Hallo basisprincipes van queue storage hebt geleerd, volgt u deze koppelingen toolearn over complexere opslagtaken.

* [Azure-opslag-SDK voor Java][Azure Storage SDK for Java]
* [Azure Storage Client SDK-naslaginformatie][Azure Storage Client SDK-naslaginformatie]
* [REST-API van Azure Storage-Services][Azure Storage Services REST API]
* [Azure Storage-teamblog][Azure Storage Team Blog]

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[Azure Storage Client SDK-naslaginformatie]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage Services REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
