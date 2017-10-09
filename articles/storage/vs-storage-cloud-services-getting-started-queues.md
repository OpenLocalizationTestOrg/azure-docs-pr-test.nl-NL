---
title: aaaGet gestart met de opslag van de wachtrij en Visual Studio verbonden services (cloudservices) | Microsoft Docs
description: Hoe tooget gestart met Azure Queue storage in een cloud service-project in Visual Studio nadat tooa storage-account met Visual Studio verbinding services verbonden
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: da587aac-5e64-4e9a-8405-44cc1924881d
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 8ba3d830cb83e3d75102b8a09363f1dc200ff1c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-cloud-services-projects"></a>Aan de slag met Azure Queue storage en Visual Studio verbonden services (cloud services-projecten)
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Overzicht
Dit artikel wordt beschreven hoe tooget gestart met Azure Queue storage in Visual Studio nadat u hebt gemaakt of een Azure storage-account in een cloud services-project waarnaar wordt verwezen met behulp van Visual Studio Hallo **verbonden Services toevoegen** dialoogvenster .

Leert u hoe een wachtrij in code toocreate. Ook ziet u hoe tooperform basic wachtrij-bewerkingen, zoals het toevoegen, wijzigen, lezen en verwijderen van Wachtrijberichten. Hallo-voorbeelden zijn geschreven in C#-code en gebruiken van Hallo [Microsoft Azure Storage-clientbibliotheek voor .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).

Hallo **verbonden Services toevoegen** bewerking installeert Hallo juiste NuGet-pakketten tooaccess Azure-opslag in uw project en voegt Hallo-verbindingsreeks voor hello storage account tooyour project configuratiebestanden.

* Zie [aan de slag met Azure Queue storage met .NET](storage-dotnet-how-to-use-queues.md) voor meer informatie over het bewerken van wachtrijen in code.
* Zie [documentatie Storage](https://azure.microsoft.com/documentation/services/storage/) voor algemene informatie over Azure Storage.
* Zie [Cloud Services-documentatie](https://azure.microsoft.com/documentation/services/cloud-services/) voor algemene informatie over Azure-cloudservices.
* Zie [ASP.NET](http://www.asp.net) voor meer informatie over het programmeren van ASP.NET-toepassingen.

Azure Queue storage is een service voor het opslaan van grote aantallen berichten die toegankelijk zijn vanaf een willekeurige plaats in Hallo wereld via geverifieerde aanroepen via HTTP of HTTPS. Een enkel wachtrijbericht mag up too64 KB groot en een wachtrij kan miljoenen berichten up toohello totale capaciteitslimiet van een opslagaccount bevatten.

## <a name="access-queues-in-code"></a>Toegang tot wachtrijen in code
tooaccess wachtrijen in Visual Studio Cloud Services-projecten, moet u tooinclude Hallo volgende items tooany C#-bronbestand die toegang hebben tot Azure Queue storage.

1. Zorg ervoor dat de naamruimtedeclaraties Hallo Hallo bovenaan Hallo C#-bestand in deze **met** instructies.
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
2. Ophalen van een **CloudStorageAccount** -object met gegevens over uw storage-account. Gebruik Hallo na code tooget Hallo uw verbindingsreeks voor opslag en de accountgegevens van de opslag van Azure Hallo-serviceconfiguratie.
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. Ophalen van een **CloudQueueClient** object tooreference Hallo wachtrij-objecten in uw opslagaccount.  
   
        // Create hello queue client.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. Ophalen van een **CloudQueue** tooreference een specifieke wachtrij-object.
   
        // Get a reference tooa queue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

**Opmerking:** alle Hallo bovenstaande code voor het Hallo-code in Hallo volgen voorbeelden gebruiken.

## <a name="create-a-queue-in-code"></a>Een wachtrij in code maken
toocreate hello wachtrij in code, voegt u toe een aanroep te**CreateIfNotExists**.

    // Create hello CloudQueue if it does not exist
    messageQueue.CreateIfNotExists();

## <a name="add-a-message-tooa-queue"></a>Een berichtenwachtrij tooa toevoegen
tooinsert een bericht in een bestaande wachtrij maakt u een nieuwe **CloudQueueMessage** object en vervolgens aanroep Hallo **AddMessage** methode.

Een **CloudQueueMessage** object kan worden gemaakt vanuit een tekenreeks (in UTF-8-indeling) of een byte-matrix.

Hier volgt een voorbeeld waarmee het Hallo-bericht 'Hello, World' invoegt.

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    messageQueue.AddMessage(message);

## <a name="read-a-message-in-a-queue"></a>Een bericht in een wachtrij lezen
U kunt bekijken van Hallo-bericht in Hallo begin van een wachtrij zonder het te verwijderen uit de wachtrij Hallo door aanroepen Hallo **PeekMessage** methode.

    // Peek at hello next message
    CloudQueueMessage peekedMessage = messageQueue.PeekMessage();

## <a name="read-and-remove-a-message-in-a-queue"></a>Lezen en verwijderen van een bericht in een wachtrij
Uw code kunt verwijderen (uit de wachtrij) een bericht van een wachtrij in twee stappen.

1. Roep **GetMessage** tooget Hallo volgende bericht in een wachtrij. Een bericht dat wordt geretourneerd door **GetMessage** wordt onzichtbaar tooany andere codes die berichten lezen uit deze wachtrij. Standaard blijft het bericht onzichtbaar gedurende 30 seconden.
2. Hallo-bericht verwijderen uit Hallo wachtrij aanroep toofinish **DeleteMessage**.

Dit proces in twee stappen van het verwijderen van een bericht zorgt ervoor dat als uw code mislukt tooprocess een bericht vanwege problemen toohardware of software, een ander exemplaar van uw code krijgt hetzelfde bericht Hallo en probeer het opnieuw. Hallo volgende code aanroepen **DeleteMessage** direct nadat het Hallo-bericht is verwerkt.

    // Get hello next message in hello queue.
    CloudQueueMessage retrievedMessage = messageQueue.GetMessage();

    // Process hello message in less than 30 seconds

    // Then delete hello message.
    await messageQueue.DeleteMessage(retrievedMessage);


## <a name="use-additional-options-tooprocess-and-remove-queue-messages"></a>Aanvullende opties tooprocess gebruiken en verwijderen van Wachtrijberichten
Er zijn twee manieren waarop u het ophalen van berichten uit een wachtrij kunt aanpassen.

* U kunt een batch met berichten (omhoog too32) ophalen.
* U kunt een time-out langer of korter onzichtbaarheid instellen zodat uw code meer of minder tijd toofully elk bericht niet verwerken. Hallo volgende codevoorbeeld wordt de **GetMessages** methode tooget 20 berichten in één aanroep. Vervolgens wordt elk bericht verwerkt met behulp van een **foreach**-lus. Hallo onzichtbaarheid toofive minuten voor de time-out voor elk bericht wordt ook ingesteld. Houd er rekening mee dat Hallo 5 minuten voor alle berichten op Hallo dezelfde time begint, betekent dat als er 5 minuten zijn verstreken sinds de aanroep hello te**GetMessages**, alle berichten die niet zijn verwijderd weer zichtbaar worden.

Hier volgt een voorbeeld:

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.

        // Then delete hello message after processing
        messageQueue.DeleteMessage(message);

    }

## <a name="get-hello-queue-length"></a>Hallo-wachtrijlengte ophalen
U kunt een schatting maken van het aantal berichten Hallo krijgen in een wachtrij. De **FetchAttributes** methode vraagt de Queue-service Hallo Hallo wachtrij-kenmerken, zoals aantal Hallo-berichten ophalen. Hallo **ApproximateMethodCount** eigenschap retourneert de laatste waarde Hallo opgehaald door de **FetchAttributes** methode zonder Hallo Queue-service aanroepen.

    // Fetch hello queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve hello cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-hello-async-await-pattern-with-common-azure-queue-apis"></a>Hallo Async-Await-patroon gebruiken met algemene Azure Queue-API 's
Dit voorbeeld toont hoe toouse Hallo Async-Await patroon met algemene Azure Queue-API's. Hallo voorbeeld Hallo async-versie van elk Hallo opgegeven methoden aanroept, deze kunnen worden gezien door Hallo **asynchrone** na herstel van elke methode. Wanneer een async-methode is gebruikte Hallo async-await patroon lokale uitvoering wordt onderbroken totdat het Hallo-aanroep is voltooid. Hierdoor kunnen de huidige thread toodo Hallo andere taken die knelpunten in de prestaties worden voorkomen en verbetert de algehele respons van uw toepassing hello. Zie voor meer informatie over het gebruik van Hallo Async-Await-patroon in .NET [Async en Await (C# en Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)

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

## <a name="delete-a-queue"></a>Een wachtrij verwijderen
een wachtrij en alle Hallo-berichten die zijn opgenomen in deze aanroep Hallo toodelete **verwijderen** methode op Hallo wachtrij-object.

    // Delete hello queue.
    messageQueue.Delete();

## <a name="next-steps"></a>Volgende stappen
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

