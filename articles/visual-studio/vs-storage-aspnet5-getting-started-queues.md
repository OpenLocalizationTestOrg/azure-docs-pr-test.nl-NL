---
title: aaaGet gestart met de opslag van de wachtrij en Visual Studio verbonden services (ASP.NET Core) | Microsoft Docs
description: Hoe tooget gestart met behulp van Azure queue storage in een ASP.NET Core-project in Visual Studio
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
ms.openlocfilehash: 90c1ebcb6a2eac6bc4f6b69133bdf3135d359a72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-queue-storage-and-visual-studio-connected-services-aspnet-core"></a>Aan de slag met de opslag van de wachtrij en Visual Studio verbonden services (ASP.NET Core)
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Overzicht
Dit artikel wordt beschreven hoe tooget gestart met Azure Queue storage in Visual Studio nadat u hebt gemaakt of een Azure storage-account in een ASP.NET Core-project waarnaar wordt verwezen met behulp van Visual Studio Hallo **verbonden Services toevoegen** dialoogvenster. Hallo **verbonden Services toevoegen** bewerking installeert Hallo juiste NuGet-pakketten tooaccess Azure-opslag in uw project en voegt Hallo-verbindingsreeks voor hello storage account tooyour project configuratiebestanden.

Azure queue storage is een service voor het opslaan van grote aantallen berichten die toegankelijk zijn vanaf een willekeurige plaats in Hallo wereld via geverifieerde aanroepen via HTTP of HTTPS. Een enkel wachtrijbericht mag up too64 kilobytes (KB) groot en een wachtrij kan miljoenen berichten up toohello totale capaciteitslimiet van een opslagaccount bevatten.

tooget gestart, moet u eerst een Azure-wachtrij toocreate in uw opslagaccount. Leert u hoe een wachtrij in code toocreate. Ook ziet u hoe tooperform basic wachtrij-bewerkingen, zoals het toevoegen, wijzigen, lezen en verwijderen van Wachtrijberichten. Hallo-voorbeelden zijn geschreven in C\# code en hello Azure Storage-clientbibliotheek voor .NET. Zie voor meer informatie over ASP.NET [ASP.NET](http://www.asp.net).

**Opmerking:** aantal Hallo API's die aanroepen tooAzure opslag in ASP.NET Core uitvoeren zijn asynchroon. Zie [asynchrone programmering met Async en Await](http://msdn.microsoft.com/library/hh191443.aspx) voor meer informatie. Hallo-code hieronder wordt ervan uitgegaan programming async-methoden worden gebruikt.

* Zie [aan de slag met Azure Queue storage met .NET](../storage/queues/storage-dotnet-how-to-use-queues.md) voor meer informatie over het bewerken van programmatisch wachtrijen.
* Zie [documentatie Storage](https://azure.microsoft.com/documentation/services/storage/) voor algemene informatie over Azure Storage.
* Zie [Cloud Services-documentatie](https://azure.microsoft.com/documentation/services/cloud-services/) voor algemene informatie over Azure-cloudservices.
* Zie [ASP.NET](http://www.asp.net) voor meer informatie over het programmeren van ASP.NET-toepassingen.

## <a name="access-queues-in-code"></a>Toegang tot wachtrijen in code
tooaccess wachtrijen in ASP.NET Core projecten, moet u tooinclude Hallo volgende items tooany C#-bronbestand dat Azure queue storage opent.

1. Zorg ervoor dat de naamruimtedeclaraties Hallo Hallo bovenaan Hallo C#-bestand in deze **met** instructies.
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. Ophalen van een **CloudStorageAccount** -object met gegevens over uw storage-account. Gebruik Hallo na code tooget Hallo uw verbindingsreeks voor opslag en de accountgegevens van de opslag van Azure Hallo-serviceconfiguratie.
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. Ophalen van een **CloudQueueClient** object tooreference Hallo wachtrij-objecten in uw opslagaccount.  
   
        // Create hello CloudQueueClient object for hello storage account.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. Ophalen van een **CloudQueue** tooreference een specifieke wachtrij-object.
   
        // Get a reference toohello CloudQueue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

**Opmerking:** alle Hallo bovenstaande code voor het Hallo-code in Hallo volgen voorbeelden gebruiken.

### <a name="create-a-queue-in-code"></a>Een wachtrij in code maken
toocreate hello Azure wachtrij in code, voegt u toe een aanroep te**CreateIfNotExistsAsync**.

    // Create hello CloudQueue if it does not exist.
    await messageQueue.CreateIfNotExistsAsync();

## <a name="add-a-message-tooa-queue"></a>Een berichtenwachtrij tooa toevoegen
tooinsert een bericht in een bestaande wachtrij maakt u een nieuwe **CloudQueueMessage** object en vervolgens aanroep Hallo **AddMessageAsync** methode.

Een **CloudQueueMessage** object kan worden gemaakt vanuit een tekenreeks (in UTF-8-indeling) of een byte-matrix.

Hier volgt een voorbeeld waarmee het Hallo-bericht 'Hello, World' invoegt.

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    await messageQueue.AddMessageAsync(message);

## <a name="read-a-message-in-a-queue"></a>Een bericht in een wachtrij lezen
U kunt bekijken van Hallo-bericht in Hallo begin van een wachtrij zonder het te verwijderen uit de wachtrij Hallo door aanroepen Hallo **PeekMessageAsync** methode.

    // Peek hello next message in hello queue. 
    CloudQueueMessage peekedMessage = await messageQueue.PeekMessageAsync();


## <a name="read-and-remove-a-message-in-a-queue"></a>Lezen en verwijderen van een bericht in een wachtrij
Uw code kunt verwijderen (in wachtrij) een bericht van een wachtrij in twee stappen.

1. Roep **GetMessageAsync** tooget Hallo volgende bericht in een wachtrij. Een bericht dat wordt geretourneerd door **GetMessageAsync** wordt onzichtbaar tooany andere codes die berichten lezen uit deze wachtrij. Standaard blijft het bericht onzichtbaar gedurende 30 seconden.
2. Hallo-bericht verwijderen uit Hallo wachtrij aanroep toofinish **DeleteMessageAsync**.

Dit proces in twee stappen van het verwijderen van een bericht zorgt ervoor dat als uw code mislukt tooprocess een bericht vanwege problemen toohardware of software, een ander exemplaar van uw code krijgt hetzelfde bericht Hallo en probeer het opnieuw. Hallo volgende code aanroepen **DeleteMessageAsync** direct nadat het Hallo-bericht is verwerkt.

    // Get hello next message in hello queue.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();

    // Process hello message in less than 30 seconds.

    // Then delete hello message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);

## <a name="leverage-additional-options-for-dequeuing-messages"></a>Gebruikmaken van aanvullende opties voor berichten waarbij
Er zijn twee manieren waarop u het ophalen van berichten uit een wachtrij kunt aanpassen.
U krijgt eerst een batch met berichten (omhoog too32). Ten tweede kunt u instellen een time-out voor onzichtbaarheid langer of korter, zodat uw code meer of minder tijd toofully elk bericht niet verwerken. Hallo volgende codevoorbeeld wordt de **GetMessages** methode tooget 20 berichten in één aanroep. Vervolgens wordt elk bericht verwerkt met behulp van een **foreach**-lus. Hallo onzichtbaarheid too5 minuten voor de time-out voor elk bericht wordt ook ingesteld. Opmerking dat Hallo 5 minuten start voor alle op Hallo dezelfde berichten tijd, betekent dat als er 5 minuten zijn verstreken na de aanroep hello te**GetMessages**, alle berichten die niet zijn verwijderd weer worden weergegeven.

    // Retrieve 20 messages at a time, keeping those messages invisible for 5 minutes, 
    //   delete each message after processing.

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.
        queue.DeleteMessage(message);
    }

## <a name="get-hello-queue-length"></a>Hallo-wachtrijlengte ophalen
U kunt een schatting maken van het aantal berichten Hallo krijgen in een wachtrij. De **FetchAttributes** methode vraagt de queue-service Hallo Hallo wachtrij-kenmerken, zoals aantal Hallo-berichten ophalen. Hallo **ApproximateMethodCount** eigenschap retourneert de laatste waarde Hallo opgehaald door de **FetchAttributes** methode zonder Hallo queue-service aanroepen.

    // Fetch hello queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve hello cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display hello number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-hello-async-await-pattern-with-common-queue-apis"></a>Hallo Async-Await-patroon gebruiken met de gemeenschappelijke wachtrij API 's
Dit voorbeeld toont hoe toouse Hallo Async-Await-patroon met gemeenschappelijke wachtrij API's. Hallo voorbeeld aanroepen Hallo asynchrone versie van elk Hallo opgegeven methoden. Deze kunnen worden gezien door Hallo Async na herstel van elke methode. Wanneer een async-methode wordt gebruikt, wordt Hallo Async-Await-patroon lokale uitvoering onderbroken totdat het Hallo-aanroep is voltooid. Hierdoor kunnen de huidige thread toodo Hallo andere taken die knelpunten in de prestaties worden voorkomen en verbetert de algehele respons van uw toepassing hello. Zie voor meer informatie over het gebruik van hello Async-Await-patroon in .NET, [Async en Await (C# en Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)

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
## <a name="delete-a-queue"></a>Een wachtrij verwijderen
toodelete een wachtrij en alle Hallo-berichten die dit, neemt u contact de **verwijderen** methode op Hallo wachtrij-object.

    // Delete hello queue.
    messageQueue.Delete();


## <a name="next-steps"></a>Volgende stappen
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

